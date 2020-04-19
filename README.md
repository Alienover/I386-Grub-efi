# I386-Grub-efi
Grub files for those with 32 bit efi systems attempting to boot a 64 bit OS. 
---------------------------------------------------------------------------------------

# Requirements
- 4GB or higher compacity USB driver

# Preparation
- Format the USB driver to **`FAT32`**

- Clone this repo. Which should contain folder **`efi`** and file **`i386-efi.7z`**

- Copy all the files in `/efi` to the root of the USB driver (‼️Do not change any file in it)

```bash
$ cp -r <path-to-repo>/efi/* <path-to-usb-driver>
```

- Copy the compressed file `i386-efi.7z` to root of the USB driver

```bash
$ cp <path-to-repo>/i386-efi.7z <path-to-usb-driver>
```

- Download your favorite system ISO and rename it to `boot.iso`

- Copy the system image to `/boot/boot-isos`

```bash
$ cp <path-to-image>/boot.iso <path-to-usb-driver>/boot/boot-isos/boot.iso
```

# Start on Machine
> The demo is using [Manjaro-xfce-64bit](https://manjaro.org/downloads/official/xfce/)

- Set your computer boot from USB and make sure the `secure boot` is disabled

- Two situation in this step

  - If works well, we should see `Boot manjaro for 32Bit EFI` at the screen
  
  - If not, we might see `grub > prompt`. Then, use your grub command line skill🤣
  
    - Try `ls` to check which partition is your USB driver
    
    - Then run the following command to load the `grub` config
    
    ```bash
    # (hdx,gptx) is the partition of your USB driver with GPT
    # If with MBR, would be (hdx,msdosx)
    # x is a number
    grub > configfile (hdx,gptx)/boot/grub/grub.cfg
    ```
    
    - You would see `Boot manjaro for 32Bit EFI` now

- Yohooo! The installer is there. Go get to install

- After the installation, ‼️**Do not restart now**

- Remenber the `i386-efi.7z` file? Unzip it to `/home/manjaro/Downloads` on the live system

- Copy the `i386-efi` folder to `<path-to-hard-drive>/usr/lib/grub/` (`<path-to-hard-drive>` should be in `/run/xxx/xxx` normally)

```bash
$ sudo cp -r /home/manjaro/Downloads/i386-efi <path-to-hard-drive>/usr/lib/grub
```

- Run `manjaro-chroot -a`

- Run `lsblk` to get the location of your EFI/ESP partition

- Run `grub-install --target i386-efi <efi-partition>`

- If there's no error, run `update-grub`

- Reboot it. And enjoy your linux👨‍💻



----

-If you are using manjaro, just follow this guide https://forum.manjaro.org/t/tutorial-install-manjaro-on-a-32-bit-efi-64-bit-cpu-system/77361

If you are using ubuntu, use http://www.jfwhome.com/2016/01/04/latest-steps-to-install-ubuntu-on-the-asus-t100ta/ as a guide

# Referrence

[jswells/linux-asus-t100ta](https://github.com/jfwells/linux-asus-t100ta)

[Overlocker/I386-Grub-efi](https://github.com/Overc1ocker/I386-Grub-efi)
