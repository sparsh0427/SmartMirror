# SmartMirror / MagicMirror

### This guide will explain how anyone can build a Smart Mirror with only a bit of effort . This guide will give you all the steps and all the modules that I have used in my Smart Mirror . 

##### OK, so starting with some basics , the magic mirror will consist of the MagicMirror^2 operating system that runs on a Raspberry pi 3b+ and monitor behind a two way mirror encased in a wooden enclosure. I have installed the following cool modules in my magic mirror -clock , news feed , current weather , weather forecast , Holidays , YouTube , Spotify , Google Assistant . 

###### PS: You can modify the modules on the basis of your own interest . I will also attach the list of all the modules available with the magic mirror operating system which you can follow to build your own personalised magic mirror . 

##### It took me approx. 3 weeks to finish with this project . 

## EQUIPMENT - 
##### 1) Raspberry Pi Model 3B + (Model 3B would also work) *1 [https://www.amazon.in/iONiQ-Raspberry-Pi-LPDDR2-Bluetooth/dp/B07CWVSMLS/ref=sr_1_6?crid=1R7WUGYYO1U05&keywords=raspberry+pi+3b%2B&qid=1563791459&s=gateway&sprefix=raspberry+pi+3%2Caps%2C450&sr=8-6]
##### 2) MicroSD Card *1 (atlest 8 GB)
##### 3) Raspberry Pi Power Cable *1 
##### 4) Monitor *1
##### 5) HDMI Cable *1
##### 6) Mouse and Keyboard *1
##### 7) USB Mic (For Google Assistant) [https://www.amazon.in/LipiWorld%C2%AE-Portable-Studio-Speech-Mic/dp/B07MR9KM4X/ref=sr_1_1_sspa?keywords=usb+mic&qid=1563791417&s=gateway&sr=8-1-spons&psc=1]

## STEP 1 :
### SETTING UP RASPBERRY PI :
#### First you will need to install the latest version of Raspbian, the officical Raspberrypi operating system. When I installed the magic mirror the latest OS was Raspbian Buster. The OS can be found on the official site of the Raspberry pi (https://www.raspberrypi.org/downloads/raspbian/) . You  need to flash the image file on SD card . You can use ETCHER for flashing purpose (https://www.balena.io/etcher/)

## STEP 2:
### BOOT UP YOUR PI
#### Unmount the SD card from your computer and insert it into your Pi. Connect your keyboard, mouse, HDMI cable and lastly the PI's power cable. Now you would be able to see the Raspbian Pixel Desktop on your television .(or other screen that you may have used ).

#### Once the pi starts up and you have configured it , run the following commands in the terminal - 
##### ```sudo apt-get update ```
##### ```sudo apt-get upgrade ```

##### Now once the raspberry pi is updated we can install the magicmirror. First, open a browser and go to the following URL “https://magicmirror.builders”. Scroll down to the section labeled “Easy to install” and copy the following bash command: 

##### ```bash -c "$(curl -sL https://raw.githubusercontent.com/MichMich/MagicMirror/master/installers/raspberry.sh) ```

##### Next, open a terminal and paste the above code. Press enter to execute the command.  
 
##### When the installation is finished execute the following command in the terminal to start the “MagicMirror2” software:  
 
 ##### ```  cd ~/MagicMirror ```
#####    ```npm start  ```
  
##### This will run your Magic Mirror with some pre installed modules.You can edit the preinstalled modules by settig the news feed of your location , weather of your area etc. by modifying the config.js file in MagicMirror directory. Now if you want to customize your magic mirror you have to install / clone some modules and then add some channgesto config.js folder in MagicMirror directory in home/pi . 

## SPOTIFY MODULE 

Open a new terminal and execute the following commands: 
```  curl -sL https://dtcooper.github.io/raspotify/install.sh | sh  ```

The module “Raspotify” allows connection to “Spotify”. It comes pre-configured and will be discoverable on the local network as a “Spotify Connect” device. However, it can be configured by editing the “/etc/default/raspotify” file which passes arguments to the “librespot” function. 

``` # /etc/default/raspotify -- Arguments/configuration for librespot 
 
# Device name on Spotify Connect #DEVICE_NAME="raspotify" 
 
# Bitrate, one of 96 (low quality), 160 (default quality), or 320 (high quality) #BITRATE="160" 
 
# Additional command line arguments for librespot can be set below.
# See `librespot -h` for more info. Make sure whatever arguments you specify 
# aren't already covered by other variables in this file. (See the daemon's 
# config at `/lib/systemd/system/raspotify.service` for more technical details.) 
# 
# To make your device visible on Spotify Connect across the Internet add your 
# username and password which can be set via "Set device password", on your 
# account settings, use `--username` and `--password`. 
# 
# To choose a different output device (ie a USB audio dongle or HDMI audio out), 
# use `--device` with something like `--device hw:0,1`. Your mileage may vary. 
# 
#OPTIONS="--username <USERNAME> --password <PASSWORD>" 
 
# Uncomment to use a cache for downloaded audio files. Cache is disabled by 
# default. It's best to leave this as-is if you want to use it, since 
# permissions are properly set on the directory `/var/cache/raspotify'. 
#CACHE_ARGS="--cache /var/cache/raspotify" 
 
# By default, the volume normalization is enabled, add alternative volume 
# arguments here if you'd like, but these should be fine. 
#VOLUME_ARGS="--enable-volume-normalisation --linear-volume --initial-volume=100" 
# /etc/default/raspotify -- Arguments/configuration for librespot ```
 
The user’s “Spotify” account can be added by uncommenting the line shown below and replacing the “<USERNAME>” and “<PASSWORD>” sections with the user’s “Spotify” account credentials. 

``` #OPTIONS="--username <USERNAME> --password <PASSWORD>"  ```
```
#### “Last.fm” Scrobbler Installation and Configuration 
The “Last.fm Scrobbler” will display track information such as the album cover art, song name, and artists for the currently playing song on the “Raspotify” module. 
 Open a new terminal and execute the following commands: 
 
 ``` cd  ~/MagicMirror/modules ```
 ```git clone https://github.com/PtrBld/MMM-Scrobbler.git  ```

Open a web browser and go to the URL “https://www.last.fm/join” and register for a “Last.fm” “API account”. 
Copy the generated API key and place it into an empty text file for future use. 
 
A23 
 
Add the following code to the “config.js” file which is located in the “~/MagicMirror/config” directory and change the “username” and “apikey” sections to the username and API key that was created in the previous steps: 
 
 ```
 {     
 module: 'MMM-Scrobbler',
 position: 'top_right', 
 config: { 
 
username: 'Last.fm username', 
apikey: 'Last.fm api key', 
//time interval to search for new song (every 15 seconds)    
updateInterval: 15 * 1000,    
//how often should we try to retrieve a song if not listening    
delayCount: 5,    
//time interval to search for new song if the 5 times not listening is received.    
//set this to the same number as updateInterval to ignore this option  
 
  delayInterval: 120*1000,   
  animationSpeed: 1000,   
  showAlbumArt: true,       
  showMetaData: true, 
 
  //Determines the position of the meta text. Possible values: top, bottom, left, right    alignment: "bottom",         }   
  } 
  ```

## YOUTUBE MODULE
A module to cast to the MagicMirror². Currently, only YouTube casting is supported. Hopefully, I will have time to add more casting options.

### Using the module:

-> Navigate to the modules directory via the follow command: cd MagicMirror/modules
-> Clone the module from github: git clone https://github.com/kevinatown/MMM-Screencast.git
-> Navigate to the MMM-Screencast directory: cd MMM-Screencast
-> Install the dependencies: npm install
-> Add the following configuration to the modules array in the config/config.js file:

```
var config = {
    modules: [
        {
		module: 'MMM-Screencast',
		position: 'bottom_right', // This position is for a hidden <div /> and not the screencast window
		config: {
			position: 'bottomRight',
			height: 300,
			width: 500,
		}
        }
    ]
} 
```

## Google Assistant Module
So here comes the most tricky part , THE GOOGLE ASSISTANT MODULE . I would say it was the most difficult module to install and took me a lot of time to run Google Assistant on my magic mirror . I too refered it from my youtube and I would be posting the link after my version of installation but please go through the video(s) as it might contain some parts I might have skipped in the explanantion below like you need to create an AUTOSTART script to run google assistant, the link of which tutorial I would upload . 

### Google Assistant” Module Installation and Configuration

Open a new terminal and execute the following commands: 
```
cd ~/MagicMirror/modules  
git clone https://github.com/gauravsacc/MMM-GoogleAssistant.git 
```
After the module has been downloaded use the terminal and run the following commands: 
```
cd into MMM-GoogleAssistant   
npm install 
```
Open a web browser and go to the URL “https://developers.google.com/assistant/sdk/” and sign in using a “Google” account. If no previous “Google” account exists, register for one.  
 
Click the “Guides” tab and navigate to the “Google Assistant Library” section. Click the “Configure a Developer Project” tab on the drop down menu and then click the tab “Developer and Account Settings”

###  Configure a “Developer Project and Account Settings” 
####  Configure an “Actions Console” project 

A “Google Cloud Platform” project, managed by the “Actions Console”, gives the device access 
to the “Google Assistant API”. The project tracks quota usage and gives valuable metrics for the 
requests made from the device. 

To enable access to the “Google Assistant API”, do the following: 
1. Open the “Actions Console”. 
2. GO TO THE “ACTIONS CONSOLE” 
3. Click on “Add/import project”. 
4. To create a new project, type a name in the “Project Name” box and click “Create Project”. 

NOTE: If a “Google Cloud Platform” project already exists, select that project and import it instead. 

5. Enable the “Google Assistant API” on the selected project. Do this in the Cloud Platform Console. 
6. Click “Enable”. 

#### Set activity controls for the account 
In order to use the “Google Assistant”, certain activity data must be shared with “Google”. The “Google Assistant” needs this data to function properly; this is not specific to the SDK. 

Open the “Activity Controls” page for the “Google” account that will be used with the “Assistant”. Any “Google” account can be used, it does not need to be the developer account. 

Ensure the following toggle switches are enabled (blue): 
● Web & App Activity ○ In addition, be sure to select the Include “Chrome” browsing history and activity from websites and apps that use “Google” services checkbox. 
● Device Information 
● Voice & Audio Activity 

#### Register the Device Model 
In order for the “Google Assistant” to respond to commands appropriate to the device and the given context, the “Assistant” needs information about that particular device. Provide this information, which includes fields like device type and manufacturer, as a device model. Think of this model as a general class of device - like a light, speaker, or toy robot. 
This information is then accessible to the “Google Assistant” and is associated with the “Actions Console” project. No other projects have access to the model and device information.

#### Use the “Registration UI
Use the “Registration UI” in the “Actions Console to register a device model. 
1. Open the “Actions Console”. 
2. Select the project that was created previously from the menu near the top of the screen. 
3. Select the “Connected properties” tab from the left “navbar”. 
4. Select the “Device Models” tab. 
5. Click the “Register Model” button. 

####  Create model
1. Fill out all of the fields for the device. 
2. See the device model JSON reference for more information on these fields. 
3. When finished, click “Register Model”. 

#### Download credential file
The “credentials.json” file must be located on the device. Later, an authorization tool will be ran and it will reference this file in order to authorize the “Google Assistant SDK” sample to make “Google Assistant” queries. Do not rename this file. 
Download this file and transfer it to the device. Click “Next”. For the Raspberry Pi only: 
Make sure this file is located in “/home/pi". If it is desired to upload the file to the device, do the following: 

1. Open a new terminal window. Run the following command in this new terminal: 
 
Note: Do not run the following command in an SSH session connected to the device. This command transfers the JSON file from a directory on the development machine to the device. An SSH session cannot access the local directories. 
 
```
scp ~/Downloads/credentials.json pi@raspberry-pi-ip-address:/home/pi/ password: password-for-device 
```

2. Close the terminal window.

#### Install the SDK and Sample Code 
Follow these instructions to install the SDK and sample code on the device. Run all of the commands on this page in a terminal on the device (either directly or via an SSH connection). 

#### Configure a new Python virtual environment 

Use a “Python” virtual environment to isolate the SDK and its dependencies from the system “Python” packages. Note: For the Raspberry Pi, run the following commands from the /home/pi directory. 

For Python 3: 
```
sudo apt-get update 
sudo apt-get install python3-dev python3-venv # Use python3.4-venv if the package cannot be found. 
python3 -m venv env 
env/bin/python -m pip install --upgrade pip setuptools wheel 
source env/bin/activate 
```

#### Get the package 
The “Google Assistant SDK” package contains all the code required to get the “Google Assistant” running on the device, including the sample code. 
Install the package's system dependencies: 
```
sudo apt-get install portaudio19-dev libffi-dev libssl-dev 
```
Use “pip” to install the latest version of the “Python” package in the virtual environment: 
```
python -m pip install --upgrade google-assistant-library 
python -m pip install --upgrade google-assistant-sdk[samples] 
```
#### Generate credentials
1. Install or update the authorization tool: 
```
python -m pip install --upgrade google-auth-oauthlib[tool] 
```
2. Generate credentials to be able to run the sample code and tools. Reference the JSON file that was downloaded in a previous step; it may need to be copied to the device. Do not rename this file. 
 ```
 google-oauthlib-tool --scope https://www.googleapis.com/auth/assistant-sdk-prototype \--save --headless --client-secrets /path/to/credentials.json 
 ```
3. A URL will be displayed in the terminal: 
```
Please visit this URL to authorize this application: https://... 
```
4. Copy the URL and paste it into a browser (this can be done on any machine). The page will ask to sign in to the “Google” account. Sign into the “Google” account that created the developer project in the previous step. 
5. Note: To use other accounts, first add those accounts to the “Actions Console” project as “Owners”. 
6. After approve the permission request from the API, a code will appear in the browser, such as "4/XXXX". Copy and paste this code into the terminal: 
```
Enter the authorization code: 
```

7. If authorization was successful, a response similar to the following will appear: 
 ```
credentials saved:/path/to/.config/google-oauthlib-tool/credentials.json 
 ```
8. If instead the “InvalidGrantError” error occurs, then an invalid code was entered. Try again, taking care to copy and paste the entire code. 

#### Run the Sample Code 
At this point, the sample is ready to run and make a query. 
In the following command: 
● Replace “my-dev-project” with the “Google Cloud Platform” project ID for the “Actions Console” project that was created. To find the project ID in the “Actions Console”, select the project, click the gear icon, and select “Project settings”. 
● Replace “my-model” with the name of the model that was created in the previous step. 
``` 
googlesamples-assistant-hotword --project_id my-dev-project --device_model_id my-model 
```
Say “Ok Google” or “Hey Google”, followed by a query. Try some of the following voice queries: 

● “Who am I?” 
● “What time is it?” 
● “What is the weather in San Francisco?” 

Note: Want to change the language for the “Google Assistant”? Use the “Google Assistant” app on a mobile phone. 

#### Get the device instance ID 

When the sample is ran, it will generate a device instance for that particular device. This device instance will be associated with the device model that was specified to run the sample. Find the device instance ID in the output for the sample. This ID will be used when running the sample so “Device actions” will be used. 
```
device_model_id: my-model 
device_id: 1C3E1558B0023E49F71CA0D241DA03CF # Device instance ID 
ON_MUTED_CHANGED:  
 {'is_muted': False} 
ON_START_FINISHED 
... 
 ```
Register for a free developer account at the URL “https://admin.pubnub.com/#/register”. Once registered, create an app and retrieve the “Publish” and “Subscriber” keys. 
 
Replace the keys in following files on the “MMM-GoogleAssistant” directory with the keys that were retrieved in the previous step: 
● “node_helper.js” 
● “MMM-GoogleAssistant.js” 
● “pi/assistant.py” 
 
Add the following code to the “config.js” file which is located in the “~/MagicMirror/config” directory. 
 ```
 {     module: "MMM-GoogleAssistant", 
    position: "top_right",     
    config: {         
    maxWidth: "100%", 
    header: ""     
    } 
 }, 
 ```


## MAGIC MIRROR 3RD 
PARTY MODULES :
#### Download credential file
https://github.com/MichMich/MagicMirror/wiki/3rd-party-module
s
