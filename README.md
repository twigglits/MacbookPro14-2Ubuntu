# MacbookPro14-2Ubuntu
A guide for installing Ubuntu LTS 20.04 on the Macbook Pro 14,2 Model

1. Install modified iso from here:

https://github.com/marcosfad/mbp-ubuntu/releases

This modified iso includes drivers for the macbookpro's touchpad, touchbar, keyboard as well as other drivers

Once you've booted into ubuntu:

2. Enable external storage/ethernet adapter

If you have an adapter plugged into your macbook, you will need to run the following command to enable it:

```
sudo lspci -nnk | grep -i net -A3
```
3. Install audio (Enables Audio Output)

Run the following commands as root in your terminal:
```
git clone https://github.com/davidjo/snd_hda_macbookpro.git
cd snd_hda_macbookpro/
#run the following command as root or with sudo
./install.cirrus.driver.sh
reboot
```
4. Enable native microphone (Enables audio input)

Run the following command in the terminal:
```
arecord -l
```

5. Wifi drivers

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



