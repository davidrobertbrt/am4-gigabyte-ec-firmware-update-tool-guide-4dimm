_revision May 3rd 2024_
# DISCLAIMER

**I am not responsible for bricked motherboard, dead CPU / RAM, loss of data. If you are unsure about anything in this guide and don't want to risk, please contact GIGABYTE SUPPORT about the process of updating EC Firmware Tool of your specific motherboard or any other issue you may have. Please ALWAYS BACKUP YOUR DATA BEFORE DOING ANY TYPE OF UPDATE ON MOTHERBOARD FIRMWARE / BIOS.**

## Description

This repo contains a guide on solving 4 DIMM DRAM problems on X370 / X470 / B350 / B450 / etc.. AM4 motherboards from Gigabyte. This solved my issue of crashing while using 4 DIMMs on a Ryzen 5000 series processor and Ryzen 3000 series.

## Prequisite

1. Update your bios based on the procedure on the Gigabyte website to the latest version. **If you have DUAL BIOS please update both chips (Backup and Main)!** _Running the tool will switch your motherboard to the backup BIOS._ 
2. **Make sure motherboard is set in SINGLE BIOS mode before making the update.** _If you have it set in DUAL BIOS mode it will not switch to the Backup BIOS. The update might fail and not reboot your computer or the computer will crash without doing the update._
3. **Make sure Secure Boot and TPM have been disabled before proceeding.** _The driver used to update the EC will not be loaded by Windows_
4. If running Windows 11, **disable Microsoft Vulnerable Driver Blocklist from Device Security and also SAC (Smart App Control)**.
5. Recommended to turn off temporarily your anti-virus or Windows Defender.
6. Turn off your internet connection (disconnect from Wi-Fi or unplug LAN from PC based on which type of connection you are using)
7. **STRONGLY RECOMMENDED TO USE WINDOWS 10 FULLY UPDATED AND AMD CHIPSET DRIVERS TO LATEST VERSION!** (you can find them on AMD official website)
8. **UNINSTALL ANY ANTI-CHEAT YOU ARE USING FOR YOUR GAMES (FACEIT OR VANGUARD)** Not doing so will result in `Load Flash.dll failed!` error and the update will not work!

## Instructions

1. Download from official Gigabyte website EC Firmware Update Tool from the section Utility from the download page of your motherboard. If you can't find it or it has been deleted, you can download the `ECFwUpdateB19.0624.1.zip` from this repository.

_The `mb_utility_ecfwupdate_B19.0606.1.zip` is for X370 Gaming K7 motherboard only!_

2. Extract the files on your main OS drive. (root of the partition)

3. Open the `uiset.ini` file.

4. Find the line with `AutoFlash=1` and set it to `AutoFlash=0`.

5. Open the `IFU_XE32_v1310.exe` file. **DO NOT OPEN ECFwUpdate.exe!**

6. Load the latest bin file which is `V817.bin`.

7. Press the flash button and wait until it finishes.

8. Wait 30 seconds for the computer to reboot. If it does not reboot after 2 minutes it means that the update failed!

9. After rebooting, turn off the computer and reset BIOS using Clear CMOS button or remove the CMOS battery. 

10. Wait 5 minutes and reinsert the battery (if you removed it at step 9).

11. Boot back into Windows. If everything works, the update is done! If you are unsure, check the next section of this guide.

12. Reconfigure your BIOS (enable Secure Boot, TPM, ReBar, etc..)

## Checking if the update was successful

I have seen on many forums that most people can't seem to find a way to check if the firmware update was successful. To do this, we can use the same `IFU_XE32_v1310.exe` file to check the checksums of the EC ROM and the bin file we just flashed.

1. Load the `V817.bin` file into the tool. Don't click flash, go to the next tab called setting.
2. At the next tab, under the section `CheckSUM Test` press the GET button on both BIN and ROM section. If the numbers match then the update was successful. If not, please check you did all the steps from the guide correctly.

![Verify CHECKSUM in Setting Tab](https://i.imgur.com/1DK5QxW.png)

- Another method of checking is to set in `uiset.ini` file the variable `FW VERSION SHOW` to 1. 

E.g. `FW VERSION SHOW=0` to `FW VERSION SHOW=1`

Running the tool will show on the main page which verison you are running as shown in the picture below.

![Check version with FW VERSION SHOW](https://i.imgur.com/0wwenyt.png)
