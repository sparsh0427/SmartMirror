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
  


