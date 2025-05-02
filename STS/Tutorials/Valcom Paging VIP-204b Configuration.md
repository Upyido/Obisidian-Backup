- First open VIP-102b Folder
- Locate the program file "VIP 102BTool. Exe"
- Run the tool
- Once launched select the Communications drop down menu
- Select Scan All Devices
- In the left window pane select the paging gateway that is to be configured
- Once Selected it will display the summary page and the selected gateway will highlight blue in the left window pane as seen in the picture below
![[204b-summary.png]]
- Select the network tab if the device requires a static ip configuration, otherwise leave default as DHCP
- Select the Channels Tab
- Select the dial code field and input the EXT. # programmed in intermedia
- Select apply at the bottom of the page to save the current settings
![[204b-Channels.png]]
- Select the Group Membership tab
- In the group window select the Group # (999)box to ensure it has a check mark
- Select Apply


![[204b-GroupMembership.png]]
- Select SIP tab
- Input the SIP id to the phone number field
	-  Input the SIP id:
		- Go to intermedia portal
		- Look in customer profile
		- Select Devices
		- Select the device
		- Look for SIP credentials and next to it select get credentials
		- Copy Authentication ID & input it to the phone number field 
- Input the description of the device
- Input the SIP id to the authentication name field
	-  Input the SIP id:
		- Go to intermedia portal
		- Look in customer profile
		- Select Devices
		- Select the device
		- Look for SIP credentials and next to it select get credentials
		- Copy Authentication ID & input it to the Authentication Name field 
- Input the secret value:
	- Go to intermedia portal
	- Look in customer profile
	- Select Devices
	- Select the device
	- Look for SIP credentials and next to it select get credentials
	- Copy password & input it to the Secret field
- Primary SIP Server should be hpbx155.Telecomsvc.Com
- Backup 1 should be hpbx155.Telecomsvc.Com 
- Ensure Register is checked
![[Valcom VIP-204b settings.png]]



EXTREME EMERGENCIES FIND SOMEONE TO REACH OUT TO DON