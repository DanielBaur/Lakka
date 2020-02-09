
Authors: D.B. (nequiem57@googlemail.com), P.M., A.B. 
Last edited: 09th February 2020 by D.B.


This README is meant to provide documentation on how I set up a raspberry pi computer for retro gaming utilizing Lakka.
I was mainly focussing on playing N64 games with corresponding N64 USB controllers.
Setting up the system took quite some time due to insufficient documentation.
Hence I decided to document the setup process (working for both my requirements and hardware) so you and anyone could reliably reproduce it.





###############################################
###### Contents ###############################
###############################################

  * Introduction
  * The Components I Used
  * Using Balena Etcher to Install Lakka
  * Installing Roms
  * Controller Configuration
  * Comments & Problems





###############################################
###### Introduction ###########################
###############################################


Hier könnte ihre Werbung stehen.





###############################################
###### The Components I Used ##################
###############################################


- my laptop (Ubuntu 18.04)
- a Raspberry Pi 4 bundle
  (version: 4GB;
   including: microHDMI to HDMI cable, power supply, micro SD card, case;
   link: https://www.reichelt.de/das-reichelt-raspberry-pi-4-b-4-gb-all-in-bundle-rpi-4b-4gb-allin-p263086.html?&trstct=pos_0&nbc=1)
- N64 controllers
  (link1: https://smile.amazon.de/gp/product/B07KSZ8DPV/ref=ppx_yo_dt_b_asin_title_o05_s00?ie=UTF8&psc=1;
   link2: https://smile.amazon.de/gp/product/B0779SXXL4/ref=ppx_yo_dt_b_asin_title_o07_s00?ie=UTF8&psc=1)
- an installation of Balena Etcher ('./software/balena-etcher-electron-1.5.70-linux-x64.zip'; see below)
- a Lakka image ('./software/Lakka-RPi2.RPi4.arm-2.3.1.img')
- roms ('./roms/*')
- my configuration files ('./software/joypads/*', './software/remappings/*', './software/retroarch.cfg')





###############################################
###### Using Balena Etcher to Install Lakka ###
###############################################


- GENERAL INFORMATION:
  Balena Etcher is used to write images (e.g. of operating systems) to a micro SD card.
  In the context of setting up a RaspBerry Pi computer it is used to flash an operating system onto a micro SD card from where the RaspBerry Pi is running it.


- Either download (from https://www.balena.io/etcher/) or copy the Balena Etcher zip file to its designated folder (e.g. to /usr/local/).


- Unzip the balena-etcher-electron-1.5.70-linux-x64.zip file:
  $ unzip balena-etcher-electron-1.5.70-linux-x64.zip
  (How to unzip .zip files via command line: https://askubuntu.com/questions/86849/how-to-unzip-a-zip-file-from-the-terminal)


- Make the executable executable:
  $ sudo chmod a+xwr ./usr/local/balenaEtcher-1.5.70-x64.AppImage


- Execute the executable and start Balena Etcher:
  $ /usr/local/balenaEtcher-1.5.70-x64.AppImage 


- Select the Lakka image and flash it onto the micro SD card (! make sure you really chose the designated SD card !).
  (Balena Etcher can also be used to flash any other image (e.g. Raspbian) onto the micro SD card for the Raspberry Pi.)


- Afterwards insert the micro SD card into the Raspberry Pi.
  Boot and set up the WLAN connection - this is important as Lakka needs to boot in order to set up the file structure.





###############################################
###### Installing Roms ########################
###############################################


- GENERAL INFORMATION:
  By inserting the Lakka micro SD card into your computer you can access the Lakka file system (LAKKA_DISC).
  This allows you to add, remove and modify the data stored within it.


- In order to add roms to Lakka, just copy the desired file into the "roms" folder.
  Thereby you can create subfolder structures (e.g. "roms/gameboy_advance").


- Then boot into Lakka, navigate to the '+' sign and scan the 'roms' directory. The roms you just added are then compared against internal database entries and should be selectable in the main menu.





###############################################
###### Controller Configuration ###############
###############################################


- GENERAL INFORMATION:
  Within Retroarch there are three configuration files relevant for the proper use of any controller:
    - the controller-specific key bindings ():
      This file contains the information on which key of your controller provides what input signal for Retroarch
      (e.g. whether clicking the green butten labelled "B" on your N64 USB controller actually provides the input "A", "B" or anything else).
      When you attach both your new controller and a keyboard to the Raspberry Pi hosting Lakka you can generate this file by navigating to
      ---> Input ---> Player Binds.
    - the core- or game-specifig remappings ():
      Now that Retroarch is aware of what inputs your controller can actually provide there is also the option of telling it how to use those for the emulation of
      a specific emulator/core or even within a specific game. You can generate those files by XXX.
    - the global configuration file ():
      That is almost it - wouldn't it be for the global configuration file. This file is always loaded on top of the just mentioned configuration files. Accordingly
      you have to make sure that the configurations you just made are not overwritten.


In order to set up the controls for your Lakka Raspberry Pi system do the following within the micro SD file system (LAKKA_DISC):

  - Copy the contents of the folder 'joypads' (this folder contains the controller-specifig key bindings) from 'software' into the 'joypad' folder within the LAKKA_DISC root directory.
  
  - Copy the contents of the folder 'remappings' (this folder contains the core-/game-specifig remappings) from 'software' into the 'remappings' folder within the LAKKA_DISC root directory.

  - Replace the file './.config/retroarch/retroarch.cfg' within the LAKKA_DISC root directory with the file 'retroarch.cfg' (this is the global configuration file).





###############################################
###### Comments & Problems ####################
###############################################


- 2020-01-25 (Daniel): 
  Nintendo DS cores don't run smoothly.
  Everything works but the games run incredibly slow.
  This should be fixed in the future.
  (One should anyhow emulate NDS games with a NDS console and a flashcard (e.g. EDGE).)


- 2020-02-06 (Daniel):
  Some Nintendo 64 games suffer from low frame rates.
  E.g.: "Conker's Bad Fur Day" and "Super Smash Brothers" (with four players at lowest resolution) both run at ~20 fps.
  According to the community this is due to the fact that the current version of Lakka is not yet optimized for the Raspberry Pi 4 architechture.
  Future software updates are likely to improve these issues.





