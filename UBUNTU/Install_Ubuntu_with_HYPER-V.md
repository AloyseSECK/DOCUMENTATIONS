# How to install ubuntu virtual machine using HYPER-V manager on windows

### This [youtube tutorial](https://www.youtube.com/watch?v=k_G4Mb-M9Fc&t=528s) will help you from beginning to end. 

## Activate fullscreen mode 
- open terminal
- type `sudo nano /etc/default/grub`
- find the line `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"`
- change it to `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash video=hyperv_fb:1920x1080"`
- type `Ctrl + O` to save the file then `Enter` and `Ctrl + X` to exit
- type `sudo update-grub`
- restart the virtual machine