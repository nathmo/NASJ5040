# NASJ5040
AsRock J5040 NAS setup with 32Gb RAM and LSI RAID card support

the goal is to build a low power NAS (<30W) with enough RAM (32Gb)
LSI RAID card are too power hungry (>10W) and SAS drive are not better but I wanted to try to see if I could make it work.

# Hardware
## RAM + motherboard
1X J5040-ITX motherboard : https://www.asrock.com/mb/Intel/J5040-ITX/index.fr.asp
2X G.Skill Ripjaws 16GB, 2400 MHz, DDR4-RAM, SO-DIMM https://www.digitec.ch/en/s1/product/gskill-ripjaws-2-x-16gb-2400-mhz-ddr4-ram-so-dimm-ram-11230127
1X sata SSD 120 Gb

for the data storage, I have 2 variant :
## Data 1
1X PCIe LSI raid card : https://fr.aliexpress.com/item/1005004679780618.html
1X PCIe X1 X16 with power injector : https://fr.aliexpress.com/item/1005001382338955.html
2X SAS cable : https://fr.aliexpress.com/item/1005004403091207.html
6-8X SATA HDD
## Data 2
1X PCie SATA Expander : https://fr.aliexpress.com/item/4000433243029.html
6X SATA HDD

for the power supply I have 2 variant :
## power 1
1X PSU jack to molex adapter : https://www.digitec.ch/en/s1/product/intertech-mini-itx-psu-nas-200-w-power-supply-pc-15658837
1X power brick 12 V Barrel Jack (50-100 W)
1X Molex to SATA expender : https://fr.aliexpress.com/item/1005002534885657.html
## power 2
1X stadard ATX PSU

# RAM
the official specs says that the J5040 only support up 8Gb or RAM. but it works with 32 Gb too
you just need to have the right kind of ram stick. I could find a few thread online that reported that 
theses two model worked :

- corsair vengeance 2 x 16gb 2400 mhz ddr4 : https://www.digitec.ch/en/s1/product/corsair-vengeance-2-x-16gb-2400-mhz-ddr4-ram-so-dimm-ram-5784604

- gskill ripjaws 2 x 16gb 2400 mhz ddr4 : https://www.digitec.ch/en/s1/product/gskill-ripjaws-2-x-16gb-2400-mhz-ddr4-ram-so-dimm-ram-11230127

when I plugged the ripjaws in the motherboard it didnt work. I had to remove the battery, short the CMOS reset jumper and wait a while (like a minute or two for the first boot)
after a few trial it booted and could see the 32 Gb in the bios

# LSI Raid card
I tried to use the webbios of the LSI card but I dont see the press ctrl-H during the BIOS. but when ubuntu booted i could see the LSI card in the PCIe device.
I never used it before but it was also posible to control the card from the OS via a script from broadcom (https://www.broadcom.com/support/knowledgebase/1211161500661/installing-megacli-in-debian-or-ubuntu)
I installed MegaCli64 and can list the drive but can't create a pool.
I'm trying again with storcli but had no time to experiment more.

# Setup

I installed a stock Ubuntu server on the SSD with SSH.

from there I installed docker, ZFS, pihole + pivpn, dynddns 
it's close from the instruction on another NAS build i did ( ARM based)
- https://github.com/nathmo/Quartz64_NAS

