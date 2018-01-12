# HUD-Anywhere-V2
Using 2 Android devices to create a Heads Up Display
Notes:

This is the second vesion of the HUD Anywhere Tasker project.

This version uses video cast from one device and opened in an AutoTools webscreen in a reversed or flipped view.

The project requires:
Two(2) Android devices Device 1(D1) and Device 2(D2)
Wifi tether capabilities
Tasker: https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm&hl=en
AutoInput: https://play.google.com/store/apps/details?id=com.joaomgcd.autoinput&hl=en
AutoRemote: https://play.google.com/store/apps/details?id=com.joaomgcd.autoremote&hl=en
AutoTools: https://play.google.com/store/apps/details?id=com.joaomgcd.autotools&hl=en
Screen Stream: https://play.google.com/store/apps/details?id=info.dvkr.screenstream&hl=en

Description:
The project uses Tasker to open Screen Stream on D1, and then to open another (your choice) app to be displayed in reflection on D2.
  The tether between the devices goes from D2 to D1.  That is to say, D2 creates a wifi hotspot which D1 connects to.
  Screen Stream is used to capture the D1 display and send the information to a local URL.
  AutoInput and AutoRemote coordinate the communication between devices.
  The AutoTools webscreen reverses the images and displays them.
    
Before running the project, it is necesssary to identify the URL which D1 will post the screen capture to and modify the 
HUD_anywhere.html file with that URL. On my D2 I have placed the HUD_anywhere.html file in the AutoTools directory, but you 
may move it elsewhere.  If you do, please make sure to modify the D2-HUD task accordingly.

Both the D1 and D2 Tasker Projects contain preparatory and shutdown tasks.  These tasks, as expected, get the devices ready to display 
the HUD.  In each of these (HudPrep and HudUnPrep) I have included a network restrictions task.  I have found that restricting the 
network usage of most other apps while running the HUD increases the speed and responsivness of the project.  YMMV.  In order to 
use this feature, please go into the tasks and identify the apps that you wish to be disallowed from network access while running 
the HUD.

Once all the files and apps are in order, the HUD is started by running the HudPrep task in D2. This will start the tether, and wait 
until D1 has connected to the D2 wifi hotspot (through an AutoInput UI query).  Please note that the task looks for "1 device conncted." 
If your D2 has more than one device connecting to the hotspot, it will probably not move to the next step.  When D1 has connected to D2, 
the project will register and sync the AutoRemote information between the devices and start the Autoremote wifi and bluetooth services on
both devices.  Upon completion, D2 sends an AutoRemote message to D1 telling it to start Screen Stream, the app to displayed in the HUD 
and show a semi-transparent scene containing a "power button" and a "pause button."  Both the power button and pause shut Screen Stream, 
the displayed app and sends a message to D2 to close the Autotools webscreen.  The power button sends an additional command that runs the
HudUnPrep commands on both devices, stopping the wifi and bluetooth services, ending the network restrictions and shutting off the 
tether.
