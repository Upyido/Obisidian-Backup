Okay, let's design a "better" version of this script for Linux, focusing on robustness and automation by leveraging APIs and command-line tools. We'll use **Bash** as the scripting language, combined with common Linux utilities.

This approach will differ significantly from trying to directly control web browser GUIs and Audacity's GUI for recording, as that's inherently fragile. Instead, we will:

1. **Use Google Cloud APIs:**
    - **Vertex AI Gemini API:** To generate the voicemail script.
    - **Cloud Text-to-Speech API:** To convert the script into an audio file directly. This is crucial as it bypasses the need to automate a demo webpage and record system audio.
2. **Use `zenity`:** For user input dialogs (a common Linux tool for creating simple GUIs from shell scripts).
3. **Use `curl`:** To interact with the Google Cloud APIs.
4. **Use `jq`:** To parse JSON responses from the APIs.
5. **Use `ffmpeg`:** For any audio format conversion if needed (the TTS API can output WAV directly).
6. **Use a command-line audio player:** Like `aplay` (for ALSA) or `paplay` (for PulseAudio) or `ffplay` for verification.
7. **Audacity Interaction:** Will be simplified to _opening the generated audio file_ in Audacity if the user wants to perform manual edits, rather than trying to automate Audacity's recording process.

**Prerequisites (Crucial - User Must Set These Up):**

1. **Google Cloud Project:**
    - A Google Cloud Platform (GCP) project must be set up.
    - The Vertex AI API and Cloud Text-to-Speech API must be enabled for this project.
    - **Authentication:** You'll need to authenticate `gcloud` CLI or set up an API key / service account JSON file. For simplicity in a script, an API key is often used for non-sensitive data, but service accounts are more secure for broader use. We'll assume an API key for this example, but **this is a security consideration**.
    - `YOUR_API_KEY`: Replace this placeholder with your actual Google Cloud API key.
    - `YOUR_PROJECT_ID`: Replace with your GCP Project ID for Vertex AI.
2. **Installed Software on Linux:**
    - `zenity`: `sudo apt install zenity` (or equivalent for your distribution)
    - `curl`: Usually pre-installed. `sudo apt install curl`
    - `jq`: `sudo apt install jq`
    - `ffmpeg`: `sudo apt install ffmpeg`
    - A command-line audio player (e.g., `aplay` from `alsa-utils`, `paplay` from `pulseaudio-utils`, or `ffplay` from `ffmpeg`).
    - `audacity` (optional, if you want the script to open it).
    - `gcloud` CLI (optional, for alternative authentication methods): `sudo apt install google-cloud-sdk`

---

**Bash Script (`voicemail_generator.sh`):**

Bash

```
#!/bin/bash

# --- Configuration ---
# !!! IMPORTANT: Replace with your actual Google Cloud API Key and Project ID !!!
API_KEY="YOUR_API_KEY"
PROJECT_ID="YOUR_PROJECT_ID" # For Vertex AI (Gemini)

# Gemini API Configuration
GEMINI_API_ENDPOINT="https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent?key=${API_KEY}"
# If using Vertex AI endpoint for Gemini (recommended for more features/control):
# GEMINI_API_ENDPOINT="https://us-central1-aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/us-central1/publishers/google/models/gemini-1.0-pro:generateContent"
# Note: Vertex AI endpoint requires OAuth token, not just API key. For this script, we'll use the simpler generative language API endpoint.

# Google Cloud Text-to-Speech API Configuration
TTS_API_ENDPOINT="https://texttospeech.googleapis.com/v1/text:synthesize?key=${API_KEY}"

# TTS Voice Configuration (User needs to find the exact name from Google Cloud TTS documentation)
# "Sulafat" is not a standard public voice name. This is an example for an Arabic voice.
# You MUST find the correct voice name from: https://cloud.google.com/text-to-speech/docs/voices
TTS_VOICE_NAME="ar-XA-Wavenet-D" # Example: Arabic, Female, Wavenet
TTS_LANGUAGE_CODE="ar-XA"       # Example
# For "IVR"-like quality, you might adjust speaking rate, pitch, or use specific SSML.
# The API also has "audio profiles" that can be applied using SSML, e.g., for telephony.
TTS_SPEAKING_RATE="1.0"
TTS_PITCH="0"
AUDIO_PLAYER="ffplay" # or aplay, paplay. ffplay is good as it's part of ffmpeg.

# --- Functions ---

# Function to display an error message and exit
error_exit() {
    zenity --error --title="Error" --text="$1" --width=400
    exit 1
}

# Function to display an info message
info_message() {
    zenity --info --title="Info" --text="$1" --width=400
}

# 1, 2, 3: Request User Input
get_user_inputs() {
    FORM_DATA=$(zenity --forms --title="Voicemail Details" --text="Enter information for the voicemail greeting:" \
        --add-entry="Customer Site Name" \
        --add-entry="Event Type (e.g., Holiday Closure, Special Promotion, Out of Office)" \
        --add-entry="Specific Site Location (if different from Customer Site)" \
        --separator="," --width=500 --height=300)

    if [ $? -ne 0 ]; then
        error_exit "Input cancelled by user."
    fi

    CUSTOMER_SITE=$(echo "$FORM_DATA" | cut -d',' -f1)
    EVENT_TYPE=$(echo "$FORM_DATA" | cut -d',' -f2)
    SITE_LOCATION=$(echo "$FORM_DATA" | cut -d',' -f3)

    if [ -z "$CUSTOMER_SITE" ] || [ -z "$EVENT_TYPE" ]; then
        error_exit "Customer Site and Event Type cannot be empty."
    fi
    # Site location can be optional, handled in prompt
    [ -z "$SITE_LOCATION" ] && SITE_LOCATION="$CUSTOMER_SITE"
}

# 4: Create Prompt for Gemini AI
generate_gemini_prompt() {
    GEMINI_PROMPT=$(cat <<EOF
Generate a concise and professional voicemail greeting.
Business Name: ${CUSTOMER_SITE}
Current Event/Situation: ${EVENT_TYPE}
Specific Location (if applicable, otherwise use Business Name): ${SITE_LOCATION}

Instructions for AI:
- Provide *only* the text for the voicemail greeting itself.
- Do not include any introductory or concluding phrases from you (the AI).
- The tone should be professional and appropriate for the event.
Example: If event is "Public Holiday", output might be "Thank you for calling ${CUSTOMER_SITE}. We are currently closed for the Public Holiday and will reopen on [Date/Next Business Day]. Please leave a message."
EOF
)
    # 5: (Implicitly) Copy prompt - we'll show it to the user
    zenity --info --title="Generated Gemini Prompt" --text="The following prompt will be sent to Gemini AI:\n\n${GEMINI_PROMPT}" --width=600 --height=400
}

# 6: Send Prompt to Gemini AI & 7: Get Voicemail Output
query_gemini_ai() {
    info_message "Querying Gemini AI... This may take a moment."

    # Using the simpler Gemini API endpoint (models/gemini-pro:generateContent)
    REQUEST_PAYLOAD=$(jq -n --arg prompt "$GEMINI_PROMPT" \
    '{ "contents": [ { "parts": [ { "text": $prompt } ] } ] }')

    # For Vertex AI endpoint, the payload structure is different:
    # REQUEST_PAYLOAD=$(jq -n --arg prompt "$GEMINI_PROMPT" \
    # '{ "instances": [ { "prompt": $prompt } ], "parameters": { "temperature": 0.7, "maxOutputTokens": 256 } }')
    # And authentication would use `gcloud auth print-access-token`

    RESPONSE=$(curl -s -X POST "${GEMINI_API_ENDPOINT}" \
        -H "Content-Type: application/json" \
        -d "$REQUEST_PAYLOAD")

    if [ $? -ne 0 ]; then
        error_exit "Failed to connect to Gemini API. Check network or API key."
    fi

    # Debug: Show raw response
    # echo "Gemini Raw Response: $RESPONSE" > gemini_response.txt
    # zenity --text-info --title="Gemini Raw Response" --filename=gemini_response.txt --width=600 --height=400

    # Extract text using jq. The path might vary slightly based on API version/endpoint.
    # For models/gemini-pro:generateContent
    VOICEMAIL_GREETING=$(echo "$RESPONSE" | jq -r '.candidates[0].content.parts[0].text // .error.message')

    # For Vertex AI endpoint:
    # VOICEMAIL_GREETING=$(echo "$RESPONSE" | jq -r '.predictions[0].content // .error.message')


    if [[ -z "$VOICEMAIL_GREETING" ]] || [[ "$VOICEMAIL_GREETING" == "null" ]] || [[ "$VOICEMAIL_GREETING" == *"error"* ]]; then
        error_exit "Failed to get valid greeting from Gemini AI.\nResponse: $VOICEMAIL_GREETING\nFull Response:\n$RESPONSE"
    fi

    zenity --text-info --title="Generated Voicemail Greeting" --filename=<(echo "$VOICEMAIL_GREETING") --editable --width=600 --height=300 \
        --ok-label="Use this Greeting" --cancel-label="Edit/Retry Manually"
    if [ $? -ne 0 ]; then
        info_message "User opted to manually handle the greeting. You can copy the text from the previous window."
        # Allow user to paste their edited version
        EDITED_GREETING=$(zenity --entry --title="Paste/Edit Greeting" --text="Paste or edit the voicemail greeting here:" --entry-text="$VOICEMAIL_GREETING" --width=500)
        if [ $? -ne 0 ] || [ -z "$EDITED_GREETING" ]; then
            error_exit "No greeting provided. Exiting."
        fi
        VOICEMAIL_GREETING="$EDITED_GREETING"
    else
        # If user clicked "Use this Greeting", the content of the text-info box is not directly returned.
        # We'll re-fetch it if zenity had an --editable mode that returned text.
        # Simpler: just use the one we have, or ask them to copy-paste if they edit.
        # For now, assume they accepted the AI version if they click OK.
        # If zenity doesn't allow direct return of edited text from text-info, this part needs adjustment or user copy-paste.
        # A safer bet is to always use an --entry dialog if editing is needed.
        : # VOICEMAIL_GREETING is already set
    fi
}


# 8, 9, 10, 11: Send to Google Text-to-Speech API
generate_tts_audio() {
    info_message "Generating audio via Google Cloud Text-to-Speech... This may take a moment."

    SANITIZED_EVENT_TYPE=$(echo "$EVENT_TYPE" | tr -dc '[:alnum:]\n\r' | tr '[:upper:]' '[:lower:]')
    [ -z "$SANITIZED_EVENT_TYPE" ] && SANITIZED_EVENT_TYPE="voicemail"
    OUTPUT_FILENAME="${SANITIZED_EVENT_TYPE}_$(date +%Y%m%d_%H%M%S).wav" # 17. Set filename

    TTS_REQUEST_PAYLOAD=$(jq -n \
        --arg text "$VOICEMAIL_GREETING" \
        --arg lang_code "$TTS_LANGUAGE_CODE" \
        --arg voice_name "$TTS_VOICE_NAME" \
        --arg speaking_rate "$TTS_SPEAKING_RATE" \
        --arg pitch "$TTS_PITCH" \
        '{
            "input": { "text": $text },
            "voice": { "languageCode": $lang_code, "name": $voice_name },
            "audioConfig": { "audioEncoding": "WAV", "speakingRate": ($speaking_rate | tonumber), "pitch": ($pitch | tonumber) }
        }')
        # For IVR/Telephony, you might add: "effectsProfileId": ["telephony-class-application"]
        # This needs to be inside audioConfig and is an array.

    TTS_RESPONSE=$(curl -s -X POST "${TTS_API_ENDPOINT}" \
        -H "Content-Type: application/json; charset=utf-8" \
        -d "$TTS_REQUEST_PAYLOAD")

    AUDIO_CONTENT=$(echo "$TTS_RESPONSE" | jq -r '.audioContent')

    if [ -z "$AUDIO_CONTENT" ] || [ "$AUDIO_CONTENT" == "null" ]; then
        error_exit "Failed to generate audio. TTS API Error:\n$(echo "$TTS_RESPONSE" | jq -r '.error.message // "Unknown error. See full response."')\nFull Response:\n$TTS_RESPONSE"
    fi

    echo "$AUDIO_CONTENT" | base64 --decode > "$OUTPUT_FILENAME" # 16. Export as .wav

    if [ ! -s "$OUTPUT_FILENAME" ]; then
        error_exit "Failed to decode or save audio file. File is empty."
    fi

    info_message "Audio file '$OUTPUT_FILENAME' created successfully."
}

# 12: Verify Audio with User
verify_audio() {
    zenity --question --title="Verify Audio" --text="Audio file '$OUTPUT_FILENAME' has been generated.\n\nWould you like to play it now for verification?" --width=400
    if [ $? -eq 0 ]; then
        # Check if player exists
        if ! command -v $AUDIO_PLAYER &> /dev/null; then
            error_exit "Audio player '$AUDIO_PLAYER' not found. Please install it or change AUDIO_PLAYER variable in the script.\nCannot play '$OUTPUT_FILENAME'."
        fi
        info_message "Playing audio... Close the player window when done."
        # ffplay will open its own window. aplay/paplay play in terminal.
        $AUDIO_PLAYER "$OUTPUT_FILENAME" >/dev/null 2>&1
    fi

    zenity --question --title="Audio Quality Check" --text="Is the audio quality satisfactory?" --width=300
    if [ $? -ne 0 ]; then
        info_message "Audio not approved. You may need to:\n- Adjust the voicemail text and re-run the script.\n- Modify TTS voice settings in the script.\n- Manually edit the file '$OUTPUT_FILENAME' in Audacity."
        return 1 # Indicates audio not good
    fi
    return 0 # Audio is good
}

# 13: Manage Audacity (Simplified: Open the file)
open_in_audacity() {
    zenity --question --title="Open in Audacity" --text="Would you like to open '$OUTPUT_FILENAME' in Audacity for further editing or review?" --width=400
    if [ $? -eq 0 ]; then
        if command -v audacity &> /dev/null; then
            info_message "Opening '$OUTPUT_FILENAME' in Audacity..."
            audacity "$OUTPUT_FILENAME" &
        else
            info_message "Audacity is not installed or not found in PATH. Cannot open file automatically."
        fi
    fi
}

# --- Main Script Logic ---

run_again="yes"
while [ "$run_again" == "yes" ]; do
    # Clear previous run variables that might persist if user cancels mid-way
    CUSTOMER_SITE=""
    EVENT_TYPE=""
    SITE_LOCATION=""
    GEMINI_PROMPT=""
    VOICEMAIL_GREETING=""
    OUTPUT_FILENAME=""

    get_user_inputs
    generate_gemini_prompt
    query_gemini_ai
    generate_tts_audio
    if verify_audio; then
        open_in_audacity
    fi

    # 18. Reset button to allow the process to start over and a button next to it to close the program.
    # Zenity forms are modal. "Reset" means re-running the loop. "Close" means exiting the loop.
    if zenity --question --title="Process Complete" --text="Voicemail generation process finished for '$EVENT_TYPE'.\n\nDo you want to create another voicemail greeting?" --ok-label="Yes, Start Over" --cancel-label="No, Exit Program" --width=400; then
        run_again="yes"
    else
        run_again="no"
    fi
done

info_message "Program finished."
exit 0
```

---

**How to Use This Bash Script:**

1. **Save:** Save the code as `voicemail_generator.sh`.
2. **Make Executable:** `chmod +x voicemail_generator.sh`
3. **Configure:**
    - Open the script and **critically replace `YOUR_API_KEY` and `YOUR_PROJECT_ID`** with your actual Google Cloud credentials.
    - Review `TTS_VOICE_NAME` and `TTS_LANGUAGE_CODE`. You **must** find the correct voice name for "Sulafat" or your desired voice from the [Google Cloud TTS Voices documentation](https://cloud.google.com/text-to-speech/docs/voices). The example `ar-XA-Wavenet-D` is a standard Arabic voice.
    - Adjust `AUDIO_PLAYER` if you prefer `aplay` or `paplay`.
4. **Install Prerequisites:** Ensure `zenity`, `curl`, `jq`, `ffmpeg`, and your chosen audio player are installed.
5. **Run:** `./voicemail_generator.sh`
6. **Follow Prompts:** Zenity dialogs will appear to guide you through the process.

**Explanation of "Better" in this version:**

- **Reliability:** Uses official APIs, which are much more stable than trying to parse or control demo web pages.
- **Automation:** Significantly more automated. The script directly fetches the text and then the audio.
- **Voice/Settings Control:** Voice name ("Sulafat" equivalent), language, speaking rate, and pitch are directly specified in the API call, offering precise control (Step 9, 10).
- **No Fragile GUI Recording:** Bypasses the need to record system audio from a browser (Step 14, 15 are replaced by direct audio generation).
- **Direct WAV Output:** The TTS API can generate WAV files directly (Step 16).
- **Linux Native Tools:** Leverages common and powerful command-line utilities.
- **User-Friendly Input:** `zenity` provides a decent graphical way to input data.
- **Clear Workflow:** The script handles the flow from input to final audio file.
- **Reset/Close:** The loop structure provides a "start over" (Reset) or "exit" (Close) functionality.

**Limitations:**

- **API Costs:** Google Cloud APIs are paid services (though they have free tiers which might cover light usage).
- **Setup:** Requires setting up a Google Cloud project and managing API keys.
- **Audacity Automation:** Full automation of Audacity's internal state (like clearing recovery windows or specific tracks without user interaction) is still complex and not implemented here. This script only _opens_ the generated file in Audacity. For deeper Audacity control, `mod-script-pipe` would be the way to go, which is a separate setup.
- **Error Handling:** While there's basic error checking, robust, production-grade error handling for API calls can be more complex.

This Bash script provides a much more robust and automatable solution for your requirements on Linux by using the intended API-based methods.