# MacbookPro14-2Ubuntu
A guide for installing Ubuntu LTS 20.04 on the Macbook Pro 14,2 Model.

What works:
  * Brightness control
  * Camera input
  * Keyboard
  * Trackpad
  * Audio I/O
  * Sleep
  * 5 GHz Wifi band only

What doesn't work:
  * 2.4 GHz Wifi band (Please check out Sources section of this README to find current progress on this issue)

To be improved:
  Any help with instructions for getting 2.4 GHz wifi networking enabled will be greatly appreciated!

INSTRUCTIONS:

1. Create bootable usb using the modified iso located here:

  https://github.com/marcosfad/mbp-ubuntu/releases

  This modified iso includes drivers for the macbookpro's touchpad, touchbar, keyboard as well as other drivers.

  Once you've booted into ubuntu:

2. Enable external storage/ethernet adapter

  If you have an adapter plugged into your macbook, you will need to run the following command to enable it:

  ```
  sudo lspci -nnk | grep -i net -A3
  ```
3. Install audio (Enables Audio Speaker Output)

  Run the following commands as root in your terminal:
  ```
  git clone https://github.com/davidjo/snd_hda_macbookpro.git
  cd snd_hda_macbookpro/
  #run the following command as root or with sudo
  ./install.cirrus.driver.sh
  reboot
  ```
4. Enable native microphone (Enables Audio Microphone Input)

  Run the following command in the terminal:
  ```
  arecord -l
  ```

5. Wi-Fi drivers

  To get the wifi adapter to show up run in the terminal:
  ```
  sudo apt-get purge bcmwl-kernel-source
  sudo apt update
  sudo update-pciids
  sudo apt install firmware-b43-installer
  sudo reboot
  ```

  type the following into the terminal:
  ```
  cd Downloads
  wget https://bugzilla.kernel.org/attachment.cgi?id=290569
  sudo cp brcmfmac43602-pice.txt /lib/firmware/brcm/
  sudo reboot
  ```
  Then once booted back in, you need to run:
  ```
  sudo rmmod brcmfmac && modprobe brcmfmac
  ```
6. Hibernation and Sleep

  First we will give full read, write and execute permissions the to system file that we want to change, by typing below:
  ```
  sudo chmod 777  /sys/bus/pci/devices/0000\\:01\\:00.0/d3cold_allowed
  ```
  Then, type the following to disable cold boot, so that we can hibernation works:
  ```
  sudo echo 0 > /sys/bus/pci/devices/0000\\:01\\:00.0/d3cold_allowed
  ```
Sources:

A Big Thank You! To all of the people that have worked on solving this:

  ISO Image:
    @marcosfad for the modified ubuntu iso located located here:
    https://github.com/marcosfad/mbp-ubuntu/releases

  Audio Drivers:
    @davidjo for his contribution of the audio driver located here:
    https://github.com/davidjo/snd_hda_macbookpro

  Wi-Fi Drivers:
    nonylus, Andy Holst, Simon Siebert for their contributions here: 
    https://bugzilla.kernel.org/show_bug.cgi?id=193121#c52
    
    






