## X4driver example for raspbian

The objective of this project is to transplant X4driver from xtXEP(based on FreeRTOS on Atmel controller) to Raspberry Pi(test on Raspbian scratch), so the Raspberry Pi is able to read raw data from X4M05 module.

## Features:
* src->X4Driver contains X4Driver, x4driver.c is exactly the same with XDriver inside xtXEP.
* src->hal contains hardware functions supported by Raspberry Pi.
* src->Radar contains radar task functions, they are modified from radar task functions from xtXEP.

## Deployment steps:
1. Make cable and connect X4M05 and RPI by following "X4M05RPIconnection.pdf".
2. Enable SPI at RPI configuration, Change SPI buffer from default 4096B to maxium 65536B, see how-to in the end.
3. Compile the source code by using make command under source code folder in terminal.
4. Run "./Runme" under raspbian_x4driver/raspbian_x4driver/bin,radar data will be printed out. 


## How to

### How to change RPI SPI buffer:
1. add spidev.bufsiz=65536 to /boot/cmdline.txt, the modified file looks like this:
'dwc_otg.lpm_enable=0 console=serial0,115200 console=tty1 root=PARTUUID=2277ac3d-02 rootfstype=ext4 elevator=deadline fsck.repair=yes spidev.bufsiz = 65536 rootwait quiet splash plymouth.ignore-serial-consoles'
2. save and reboot
3. check that parameter is okay:
cat /sys/module/spidev/parameters/bufsiz
65536