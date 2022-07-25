cloudready-free-89.4.44-64bit.zip


## Enable developer mode on CrOS Flex/CloudReady 96+

Edit GRUB config
Mount the EFI partition of CrOS Flex (paste the following to the terminal and press Enter): 

```if [ -b /dev/nvme0n1p12 ]; then sudo mount /dev/nvme0n1p12 /mnt elif [ -b /dev/mmcblk0p12 ]; then sudo mount /dev/mmcblk0p12 /mnt elif [ -b /dev/sda12 ]; then sudo mount /dev/sda12 /mnt fi ```

Append cros_debug flag to GRUB config files (parse the following to the terminal and press Enter) 

``` cd /mnt find . -name *.cfg -exec sudo sed -i 's,\(cros_legacy\|cros_efi\),\1 cros_debug,g' {} \;  ```





## Linux (Beta), also referred to as Crostini, is not officially supported on CloudReady and may malfunction or break across updates. However, on some models it may function.
 

How do I enable Linux (Beta) on CloudReady?

In order to use Linux (Beta) on CloudReady:

The device must support virtualization
All virtualization settings must be enabled in BIOS
Device cannot have unmitigated CPU vulnerabilities  
To turn on Linux (Beta) follow the instructions here (Home Edition Only): https://support.google.com/chromebook/answer/9145439?hl=en

If the Linux (Beta) menu isn’t available, it is most likely because your device doesn’t support virtualization or virtualization isn’t enabled. 

If the installation fails, it is possible that your device has unmitigated CPU vulnerabilities, or that CloudReady doesn’t currently support this feature on your device.  


How do I enable virtualization?

To enable virtualization enter your device’s BIOS on boot and look for a virtualization settings. Make sure all of those are enabled. Terms like "virtualization", "virtual machines", "vt-x", and "vt-d" may all apply.

If your BIOS settings do not show any relevant settings, and the Linux (Beta) menu is not available as described previously, virtualization may not be supported on your device.

How do I check if my device has any unmitigated CPU vulnerabilities? 

The following steps can only be done on CloudReady Home Edition.
To check whether you have unmitigated vulnerabilities preventing virtualization:

Log in on a CloudReady Home Edition device 
Enter crosh by pressing ```Ctrl + Alt + t``` 
Enter shell by typing shell and pressing enter
Type  ```cat /sys/devices/system/cpu/vulnerabilities/l1tf ```and press enter
If the output doesn’t contain: 

```VMX: cache flushes or VMX: flush not necessary```  the device has unmitigated CPU vulnerabilities. 

Examples of bad results:  

```
Mitigation: PTE Inversion; VMX: conditional cache flushes, SMT disabled
Mitigation: PTE Inversion; VMX: conditional cache flushes, SMT vulnerable
```

What can I do if my device has any unmitigated CPU vulnerabilities?
CPU vulnerabilities are patched via microcode updates. CloudReady does not offer microcode updates at this time. For some models, updating your BIOS will apply the needed patches. Check on your device’s manufacturer’s site to see if they offer BIOS updates and follow their instructions to update the latest BIOS available. 

After a successful update, Linux (Beta) should work if the /sys/devices/system/cpu/vulnerabilities/l1tf file contains any of the following:

```
VMX: cache flushes 
VMX: flush not necessary
Not affected
```




















Steps to disable rootfs verification:

1) Log in

2) Press ```ctl+alt+t``` to open a terminal

3) Type in ```shell``` and hit enter

4) Confirm that the yellow ```crosh``` prompt is now a green ```chronos@localhost``` prompt

5) Disable rootfs verification:

```sudo disable_verity```

6) Reboot your device:

```sudo reboot```

7) Now you can log in and proceed with rootfs edits as you normally would. You will still need to remount root as read/write:

```sudo mount -o rw,remount /```


Home-Edition Users:

For home edition users and users whose machines are un-managed you can halt the updates via command line or by blocking the following urls in your filtering device/firewall :

Update Server: cloudready-paid-update-server-2.neverware.com 

Update Storage URLs: cloudready-paid-update-storage.neverware.com

Legacy Update Server: cloudready-update-server-2015-03-12.neverware.com

Home Edition Update Server: cloudready-free-update-server-2.neverware.com
