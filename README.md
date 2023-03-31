# TP-Link Tapo C200 Camera Reverse Engineering

This document provides technical details on the reverse engineering process of the TP-Link Tapo C200 camera.

There is an another great resource about reverse engineering the camera by [DrmnSamoLiu](https://github.com/DrmnSamoLiu) that can be found here:
https://drmnsamoliu.github.io/

## Components

The camera consists of the following components:

| Name         | Component           | Description                                               |
| ------------ | -------------       | --------------------------------------------------------- | 
| SoC          | Realtek RTS3903     | CPU: 500MHz, rx5281 prid=0xdc02                           | 
| RAM          | N/A                 | 64 MiB @ 1066 MHz                                         |
| Serial Flash | XMC XM25QH64A       | Page size: 256 Bytes, erase size: 64 KiB, total: 8 MiB.   |
| Sensor       | SC2232H             |                                                           | 

## Flash Layout

| dev	  | start	           | end              | size            |  erasesize    | name          |
| ----- | ---------------  | ---------------- | --------------- | ------------- | ------------- | 
| mtd0	| 0x000000000000   | 0x00000001d800   | x               | x	            | factory_boot  |
| mtd1	| 0x00000001d800   | 0x000000020000   | x               | x             | factory_info  |
| mtd2	| 0x000000020000   | 0x000000040000   | x               | x	            | art           |
| mtd3	| 0x000000040000   | 0x000000050000   | x               | x             | config        |
| mtd4	| 0x000000050000   | 0x000000060000   | x               | x             | boot          |
| mtd5  | 0x000000060000   | 0x0000001c6400   | x               | x             | kernel        | 
| mtd6  | 0x0000001c6400   | 0x000000710000   | x               | x             | rootfs        |
| mtd7  | 0x000000710000   | 0x000000800000   | x               | x             | rootfs_data   | 
| mtd8  | 0x000000060000   | 0x000000800000   | x               | x             | firmware      |

## Default Root Password and U-Boot Console

The default root password is `slprealtek` and the U-Boot stop keyword is `slp`. Thanks to Kubik369 for this [discovery](https://github.com/nervous-inhuman/tplink-tapo-c200-re/issues/1#issuecomment-742609974).

## Ethernet

The pinout for the camera ethernet port was provided by Kubik369. It is a Molex Picoblade connector (1.27mm pitch, 4-pin). The numbering is T-568A.
<br>
<img src="https://user-images.githubusercontent.com/4379661/101809993-8c0f5100-3b18-11eb-9080-01ac77437e04.jpg" width="300px">

## Links

- [TE7C200 - FCCid.io](https://fccid.io/TE7C200)
- [C100 - GPL Sources](https://static.tp-link.com/resources/gpl/c100_GPL_v1.tar.bz2)
- [C200 - GPL Sources](https://static.tp-link.com/resources/gpl/camera_slp_realtek_c200.tar.bz2)
