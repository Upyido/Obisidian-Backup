Gemini prompt
Can you make me a python script for linux, or suggest a better alternative to make audacity recordings from google text to speech. The scripts needs to first request the Customer site, second it needs to request what the event type is. third it needs to request the site location. fourth it needs to create a prompt for gemini ai based on the site name and event type and location. fifth it needs copy the prompt. sixth it needs to go to google gemini ai and send the prompt. note that the prompt should be structured in a way that only the return from gemini includes the text for the voicemail greeting. seventh it needs to copy the voicemail output. eighth its needs to open google text to speech. ninth make sure the google text to speech demo is set for "sulafat". tenth it needs to make sure the text to speech demo is set to interactive voice recording (IVR). eleventh it needs to paste the voicemail greeting into the google text to speech demo field. twelfth it needs to play the audio and verify with user that it is good before continuing. 13th its needs to make sure audacity is running. if it is not it needs to open it. then make sure it clears the recovery window if present. then clears any present audio in the file. if it is open it needs to clear any present audio. 14th it needs to record the google text to speech output. 15th it needs to stop recording when the google text to speech output finished. 16th it needs to export as .wav. 17th it needs to set the file name as the event type. 18th the program needs a reset button to allow the process to start over and a button next to it to close the program.


Okay, this is an ambitious project that blends user input, AI interaction, web automation, and desktop application control. Creating a single Python script that flawlessly handles all these steps on Linux can be quite complex, especially the parts involving direct GUI manipulation of web pages (Google Gemini, Google Text-to-Speech demo) and Audacity without official APIs for such granular control.

Here's a breakdown of the challenges and a conceptual Python script outline using `tkinter` for the GUI and `webbrowser` and `pyperclip` for some interactions. For the more complex GUI automation, dedicated tools are often better, but I'll provide a Python-centric approach where possible, highlighting limitations.

**Challenges and Considerations:**

1. **Web Page Automation (Steps 6, 8, 9, 10, 11, 12, 14, 15):**
    
    - Directly controlling specific elements (like voice selection "sulafat", IVR mode, pasting text, clicking play) on a public Google demo page is prone to breaking if Google updates its website structure.
    - Reliable web automation usually requires tools like Selenium, which involves installing a browser WebDriver and can be more complex to set up.
    - Capturing audio playing from a specific browser tab programmatically and knowing when it finishes is non-trivial.
2. **Audacity Automation (Steps 13, 14, 15, 16, 17):**
    
    - Audacity doesn't have a simple, universally accessible Python API for direct control in the way you've described (clearing recovery, clearing tracks, recording system audio, exporting with a specific name from an external script).
    - Audacity _does_ have a scripting capability (using Nyquist or Python, but it's typically run from _within_ Audacity). Controlling it externally to start/stop recording of system audio and then export is complex. One might need to use `mod-script-pipe` for Audacity, which allows external scripts to send commands.
    - Alternatively, you could use command-line audio recording tools available on Linux (like `arecord` or `sox`) if you can route the browser's audio output appropriately, and then import that into Audacity or process it directly.
3. **Google Gemini and Text-to-Speech APIs:**
    
    - Instead of automating the web demos, using the official Google Cloud AI Gemini API and Google Cloud Text-to-Speech API would be a much more robust and reliable solution. This requires setting up a Google Cloud Project, enabling the APIs, and handling authentication. This is the **"better alternative"** for these parts.

**Suggested Approach and Python Script Outline:**

This script will use:

- `tkinter` for the GUI.
- `webbrowser` to open web pages.
- `pyperclip` to copy text to the clipboard.
- `subprocess` to potentially open Audacity.

**It will have limitations, especially in interacting directly with web page elements and Audacity's recording process without manual intervention or more advanced tools.**

Python

```
import tkinter as tk
from tkinter import messagebox, simpledialog
import webbrowser
import pyperclip
import subprocess
import os
import time # For potential delays, if attempting direct control

# --- Configuration (Better to use APIs for these) ---
GEMINI_URL = "https://gemini.google.com/app" # Or the specific chat interface
TTS_DEMO_URL = "https://cloud.google.com/text-to-speech#demo" # This is the general demo page

# --- Global Variables for GUI state ---
customer_site_var = None
event_type_var = None
site_location_var = None
prompt_text_widget = None
voicemail_text_widget = None
root = None

def generate_gemini_prompt():
    """ 4. Create a prompt for Gemini AI """
    site = customer_site_var.get()
    event = event_type_var.get()
    location = site_location_var.get()

    if not site or not event or not location:
        messagebox.showerror("Error", "Please fill in all site, event, and location fields.")
        return None

    # This prompt structure aims for Gemini to *only* return the greeting.
    # You might need to refine this based on how Gemini typically responds.
    prompt = (
        f"Generate a concise and professional voicemail greeting for a business. "
        f"The business is: {site}. "
        f"The current situation or event is: {event}. "
        f"The specific location related to this greeting (if applicable, otherwise use the main business) is: {location}. "
        f"Please provide *only* the text for the voicemail greeting itself, with no introductory or concluding phrases from you (the AI). "
        f"For example, if asked for a holiday greeting, just output 'Thank you for calling [Business Name]. We are currently closed for the [Holiday] holiday.' "
        f"and nothing else."
    )
    prompt_text_widget.delete("1.0", tk.END)
    prompt_text_widget.insert(tk.END, prompt)
    return prompt

def step_5_copy_prompt():
    """ 5. Copy the prompt """
    prompt = prompt_text_widget.get("1.0", tk.END).strip()
    if prompt:
        pyperclip.copy(prompt)
        messagebox.showinfo("Info", "Prompt copied to clipboard.")
    else:
        messagebox.showerror("Error", "No prompt generated to copy.")

def step_6_go_to_gemini():
    """ 6. Go to Google Gemini AI """
    webbrowser.open_new_tab(GEMINI_URL)
    messagebox.showinfo("Next Steps",
                        "Gemini has been opened.\n"
                        "1. Paste the prompt (Ctrl+V or Cmd+V).\n"
                        "2. Send the prompt to Gemini.\n"
                        "3. Once Gemini responds with *only* the voicemail greeting, carefully copy *only* that greeting text.")

def step_7_paste_voicemail_output_from_clipboard():
    """ 7. Copy the voicemail output (User does this manually, script prepares to receive) """
    try:
        voicemail_greeting = pyperclip.paste()
        if voicemail_greeting:
            voicemail_text_widget.delete("1.0", tk.END)
            voicemail_text_widget.insert(tk.END, voicemail_greeting)
            messagebox.showinfo("Info", "Voicemail greeting pasted from clipboard into the field below.")
        else:
            messagebox.showwarning("Warning", "Clipboard is empty or contains no text.")
    except pyperclip.PyperclipException as e:
        messagebox.showerror("Clipboard Error",
                             f"Could not access clipboard: {e}\n"
                             "Please ensure you have a clipboard tool installed "
                             "(e.g., 'xclip' or 'xsel' on Linux) and then manually paste into the field.")


def step_8_to_11_google_tts_setup():
    """
    8. Open Google Text-to-Speech.
    9. Ensure "sulafat" voice (MANUAL - hard to automate demo page).
    10. Ensure IVR mode (MANUAL - hard to automate demo page).
    11. Paste voicemail greeting.
    """
    greeting = voicemail_text_widget.get("1.0", tk.END).strip()
    if not greeting:
        messagebox.showerror("Error", "No voicemail greeting to use for Text-to-Speech.")
        return

    pyperclip.copy(greeting) # Copy greeting for easy pasting by user
    webbrowser.open_new_tab(TTS_DEMO_URL)
    messagebox.showinfo("Next Steps: Google Text-to-Speech",
                        "Google Text-to-Speech demo opened.\n"
                        "1. **Manually select the 'Wavenet' voice type if not default.**\n"
                        "2. **Manually search for and select the 'ar-XA-Wavenet-D' voice (this is often how voices like 'Sulafat' might be listed, check Google's current naming, as 'Sulafat' itself might not be a direct selectable name in the public demo without specific API codes).**\n"
                        "3. **Manually select settings equivalent to 'Interactive Voice Recording (IVR)' if available, or adjust pitch/speed as needed. The demo page might not have an explicit 'IVR' profile; you might need to use SSML input for advanced control, which is beyond simple pasting.**\n"
                        "4. Paste the voicemail greeting into the text field on the demo page.\n"
                        "5. Click the 'Speak It' or play button on the demo page to listen.")

def step_12_verify_audio():
    """ 12. Verify with user that audio is good """
    return messagebox.askyesno("Verification",
                               "Did the audio from Google Text-to-Speech sound correct and meet your expectations?\n\n"
                               "If NO, you might need to adjust the text, voice, or settings on the TTS demo page and try again, "
                               "or refine the Gemini prompt for a better script.")

def check_audacity_running():
    try:
        # Try a Linux command to check for audacity process
        subprocess.check_output(["pidof", "audacity"])
        return True
    except subprocess.CalledProcessError:
        return False
    except FileNotFoundError: # pidof not found
        messagebox.showwarning("Warning", "'pidof' command not found. Cannot reliably check if Audacity is running.")
        return False # Assume not running or ask user

def open_audacity():
    try:
        subprocess.Popen(["audacity"]) # Try to open Audacity
        messagebox.showinfo("Audacity", "Attempting to open Audacity. Please wait for it to load.")
        time.sleep(5) # Give Audacity some time to open
    except FileNotFoundError:
        messagebox.showerror("Error", "Audacity command not found. Please ensure Audacity is installed and in your system's PATH.")
        return False
    return True

def step_13_manage_audacity():
    """
    13. Ensure Audacity is running. Clear recovery/audio.
    This is VERY hard to automate reliably without Audacity's scripting pipe.
    This function will mostly guide the user.
    """
    if not check_audacity_running():
        if not open_audacity():
            return False

    messagebox.showinfo("Audacity Setup (Manual Steps)",
                        "Audacity should now be open.\n"
                        "1. **If a 'Crash Recovery' dialog appears, deal with it as appropriate (usually 'Don't Recover' for a clean slate).**\n"
                        "2. **Ensure there are no existing audio tracks. If there are, select them (Ctrl+A) and delete them (Delete key or Edit > Delete), or File > Close and then create a new project.**\n"
                        "3. **IMPORTANT: Set Audacity's recording input to capture system audio output (e.g., 'Stereo Mix', 'WASAPI loopback', 'PulseAudio Volume Control' settings for loopback, depending on your Linux audio setup). This is crucial for recording the TTS.**\n"
                        "4. Get ready to press the Record button in Audacity.")
    return True

def step_14_to_17_record_and_export():
    """
    14. Record TTS output.
    15. Stop recording.
    16. Export as .wav.
    17. Set filename as event type.
    These steps are best done MANUALLY by the user after the script prompts them,
    or via Audacity's mod-script-pipe if set up.
    """
    event = event_type_var.get()
    if not event:
        messagebox.showerror("Error", "Event type is not set. Cannot determine filename.")
        return

    filename = f"{event.replace(' ', '_')}.wav"

    proceed = messagebox.askyesno("Record Audio",
                                  "You are about to record the audio from Google Text-to-Speech in Audacity.\n"
                                  "1. Go back to the Google Text-to-Speech browser tab.\n"
                                  "2. In Audacity, press the RECORD button.\n"
                                  "3. Quickly switch to the browser and play the Text-to-Speech audio.\n"
                                  "4. Once the audio finishes playing, switch back to Audacity and press STOP.\n\n"
                                  "Are you ready to proceed with these manual steps?")
    if not proceed:
        return

    # The script cannot directly control record/stop/export here without advanced setup.
    # We will prompt the user to do it.

    messagebox.showinfo("Post-Recording (Manual Steps)",
                        f"After you have recorded and stopped in Audacity:\n"
                        f"1. Go to 'File' > 'Export' > 'Export as WAV'.\n"
                        f"2. Save the file as: '{filename}'\n"
                        f"3. Ensure WAV format is selected (default is often 16-bit PCM).")
    print(f"User prompted to record and save as {filename}")


def process_all():
    """ Main workflow """
    if not generate_gemini_prompt():
        return

    # User interaction for steps 5, 6, 7 (manual copy/paste from Gemini)
    messagebox.showinfo("Next: Gemini Interaction",
                        "A prompt has been generated and shown in the text box.\n"
                        "1. Click 'Copy Gemini Prompt'.\n"
                        "2. Click 'Open Gemini'.\n"
                        "3. In Gemini, paste the prompt and get the voicemail greeting.\n"
                        "4. Copy ONLY the greeting text from Gemini to your clipboard.\n"
                        "5. Come back to this application and click 'Paste Voicemail from Clipboard'.")
    # User will then click buttons for these steps.

def handle_tts_and_audacity_flow():
    greeting = voicemail_text_widget.get("1.0", tk.END).strip()
    if not greeting:
        messagebox.showerror("Error", "No voicemail greeting available to proceed.")
        return

    step_8_to_11_google_tts_setup() # Opens browser, user does manual setup

    # Wait for user to confirm TTS setup and playback before proceeding to Audacity
    messagebox.showinfo("Listen to TTS", "Please listen to the generated audio in the browser. Click OK when you are ready to verify it.")

    if step_12_verify_audio():
        if step_13_manage_audacity(): # Opens Audacity, user does manual setup
            step_14_to_17_record_and_export() # User manually records and exports
    else:
        messagebox.showinfo("Process Halted", "Audio not verified. Please adjust TTS settings or the greeting text and try the TTS step again.")


def reset_program():
    """ 18. Reset button """
    customer_site_var.set("")
    event_type_var.set("")
    site_location_var.set("")
    if prompt_text_widget:
        prompt_text_widget.delete("1.0", tk.END)
    if voicemail_text_widget:
        voicemail_text_widget.delete("1.0", tk.END)
    messagebox.showinfo("Reset", "Fields cleared. Ready to start over.")

def close_program():
    """ 18. Close button """
    if messagebox.askokcancel("Quit", "Do you want to exit the program?"):
        root.destroy()

def main_gui():
    global customer_site_var, event_type_var, site_location_var
    global prompt_text_widget, voicemail_text_widget, root

    root = tk.Tk()
    root.title("Voicemail Greeting Automator")

    # --- Input Fields ---
    tk.Label(root, text="Customer Site:").grid(row=0, column=0, sticky="w", padx=5, pady=2)
    customer_site_var = tk.StringVar()
    tk.Entry(root, textvariable=customer_site_var, width=50).grid(row=0, column=1, columnspan=2, padx=5, pady=2)

    tk.Label(root, text="Event Type:").grid(row=1, column=0, sticky="w", padx=5, pady=2)
    event_type_var = tk.StringVar()
    tk.Entry(root, textvariable=event_type_var, width=50).grid(row=1, column=1, columnspan=2, padx=5, pady=2)

    tk.Label(root, text="Site Location:").grid(row=2, column=0, sticky="w", padx=5, pady=2)
    site_location_var = tk.StringVar()
    tk.Entry(root, textvariable=site_location_var, width=50).grid(row=2, column=1, columnspan=2, padx=5, pady=2)

    # --- Gemini Prompt Area ---
    tk.Button(root, text="1. Generate Gemini Prompt", command=generate_gemini_prompt).grid(row=3, column=0, columnspan=3, pady=5)
    tk.Label(root, text="Generated Gemini Prompt:").grid(row=4, column=0, sticky="nw", padx=5, pady=2)
    prompt_text_widget = tk.Text(root, height=6, width=60, wrap=tk.WORD)
    prompt_text_widget.grid(row=5, column=0, columnspan=3, padx=5, pady=2)
    prompt_scrollbar = tk.Scrollbar(root, command=prompt_text_widget.yview)
    prompt_scrollbar.grid(row=5, column=3, sticky='nsew')
    prompt_text_widget['yscrollcommand'] = prompt_scrollbar.set

    # --- Gemini Interaction Buttons ---
    tk.Button(root, text="2. Copy Gemini Prompt", command=step_5_copy_prompt).grid(row=6, column=0, pady=5, sticky="ew")
    tk.Button(root, text="3. Open Gemini (Manual)", command=step_6_go_to_gemini).grid(row=6, column=1, pady=5, sticky="ew")
    tk.Button(root, text="4. Paste Voicemail from Clipboard", command=step_7_paste_voicemail_output_from_clipboard).grid(row=6, column=2, pady=5, sticky="ew")


    # --- Voicemail Greeting Area ---
    tk.Label(root, text="Voicemail Greeting (from Gemini):").grid(row=7, column=0, sticky="nw", padx=5, pady=2)
    voicemail_text_widget = tk.Text(root, height=6, width=60, wrap=tk.WORD)
    voicemail_text_widget.grid(row=8, column=0, columnspan=3, padx=5, pady=2)
    voicemail_scrollbar = tk.Scrollbar(root, command=voicemail_text_widget.yview)
    voicemail_scrollbar.grid(row=8, column=3, sticky='nsew')
    voicemail_text_widget['yscrollcommand'] = voicemail_scrollbar.set

    # --- TTS and Audacity Flow Button ---
    tk.Button(root, text="5. Proceed to TTS & Audacity (Manual Steps)", command=handle_tts_and_audacity_flow).grid(row=9, column=0, columnspan=3, pady=10)

    # --- Control Buttons ---
    tk.Button(root, text="RESET ALL FIELDS", command=reset_program, bg="orange").grid(row=10, column=0, pady=10, padx=5, sticky="ew")
    tk.Button(root, text="CLOSE PROGRAM", command=close_program, bg="red", fg="white").grid(row=10, column=2, pady=10, padx=5, sticky="ew")

    # Initial placeholder message
    # process_all() # Removed to allow user to fill fields first

    root.mainloop()

if __name__ == "__main__":
    # Ensure pyperclip dependencies are met or inform user
    try:
        pyperclip.paste()
    except pyperclip.PyperclipException as e:
        print(f"Prerequisite missing for clipboard: {e}")
        print("Please install 'xclip' or 'xsel' on Linux (e.g., 'sudo apt install xclip') for clipboard functions.")
        # Optionally, you could disable clipboard-dependent buttons if this fails
        # For now, the program will still run, but clipboard ops might fail with Tkinter's built-in clipboard.
        # pyperclip is generally more robust across systems.

    main_gui()
```

**How to Use This Script:**

1. **Save:** Save the code as a Python file (e.g., `voicemail_helper.py`).
2. **Install Libraries:**
    - `tkinter` is usually part of Python's standard library.
    - `pyperclip`: `pip install pyperclip`
    - On Linux, `pyperclip` often needs `xclip` or `xsel`: `sudo apt install xclip` or `sudo apt install xsel`.
3. **Run:** `python voicemail_helper.py`
4. **Follow On-Screen Prompts:** The script will guide you through the steps. Many steps require you to manually interact with your web browser and Audacity.

**Better Alternatives / Improvements:**

1. **Google Cloud APIs:**
    
    - **Gemini API:** Use the official Google Cloud Vertex AI Gemini API. You'd make an HTTP request with your prompt and parse the JSON response. This gives you the greeting text directly without browser interaction.
        - Python library: `google-cloud-aiplatform`
    - **Google Cloud Text-to-Speech API:** Submit the greeting text to this API and specify the voice (e.g., `ar-XA-Wavenet-D` which might correspond to "Sulafat" or a similar Arabic voice, you'd need to check the voice list) and audio profile (like "telephony-recording" which is similar to IVR). The API returns an audio file directly (e.g., MP3 or WAV).
        - Python library: `google-cloud-texttospeech`
    - This approach bypasses the browser demo pages entirely, is more robust, and gives you direct control over voice and audio format.
2. **Audacity Scripting Pipe:**
    
    - For Audacity automation, set up `mod-script-pipe`. You can then send commands to Audacity from Python to start recording, stop recording, and export. This is more advanced.
    - Example commands via pipe:
        - `New:` (clears project)
        - `Record1stChoice:` (starts recording)
        - `Stop:`
        - `Export2: Filename="{filename}" NumChannels=1` (Exports as WAV, you might need to specify more parameters)
    - This still requires you to configure system audio routing so Audacity records the correct output.
3. **Command-Line Audio Recording:**
    
    - Instead of Audacity for the initial recording, use a command-line tool like `parec` (PulseAudio) or `arecord` (ALSA) on Linux to record the system audio output while the TTS is playing (if using the demo page). Then you can either tell Audacity to import this file or use `ffmpeg` or `sox` to convert/process it. This is still tricky for timing the start/stop with the TTS demo's playback. Using the TTS API (which gives you an audio file directly) is far superior.

**Why the provided script relies on manual steps for web/Audacity:**

- **Reliability:** Automating specific clicks and selections on ever-changing public demo websites with Python (without something heavy like Selenium) is very fragile.
- **Simplicity of the Script:** Introducing Selenium or complex Audacity IPC (Inter-Process Communication) would make the script significantly more complex to write, set up, and maintain for an average user.
- **Security:** Granting a script full control over your browser or desktop applications can have security implications if not done carefully.

The provided script acts more as a "helper" that organizes the workflow and automates what's easily automatable (text generation, clipboard, opening apps), while guiding the user through the more complex interactions. If you need full automation, investing time in learning the official APIs and possibly Audacity's scripting pipe is the recommended path.