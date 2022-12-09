# nvidia-reset

`nvidia-smi` was not working e.g. `Failed to initialize NVML: Driver/library version mismatch`

1. `sudo su`
2. `apt update`
3. `apt upgrade`
4. `apt autoremove $(dpkg -l nvidia-driver* |grep ii |awk '{print $2}')`
5. `apt autoremove $(dpkg -l xserver-xorg-video-nvidia* |grep ii |awk '{print $2}')`
6. `apt reinstall xserver-xorg-video-nouveau`
7. `reboot`
8. `apt install linux-headers-$(uname -r) gcc make acpid dkms libglvnd-core-dev libglvnd0 libglvnd-dev dracut`
9. `echo "blacklist nouveau" >> /etc/modprobe.d/blacklist.conf`
10. `cat /etc/modprobe.d/blacklist.conf`
11. `vi /etc/default/grub` and add `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash rd.driver.blacklist=nouveau"`
12. `update-grub2`
13. `mv /boot/initrd.img-$(uname -r) /boot/initrd.img-$(uname -r)-nouveau`
14. `dracut -q /boot/initrd.img-$(uname -r) $(uname -r)`
15. `systemctl set-default multi-user.target`
16. `reboot` 
(now in startup terminal, not in desktop)
18. `sudo su`
19. `cd path/to/.run file`
20. `./NVIDIA-Linux-x86_64-{version}.run` e.g. `./NVIDIA-Linux-x86_64-525.60.11.run` - must be executable, if not `chmod +x NVIDIA-Linux-x86_64-525.60.11.run`
21. `systemctl set-default graphical.target`
22. `reboot`
