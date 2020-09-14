# tplink-tapo-c200-re
Reverse Engineering the TP-Link Tapo C200 camera


### Components
| Name         | Component           | Description                                               |
| ------------ | -------------       | --------------------------------------------------------- | 
| SoC          | Realtek RTS3903     | CPU: 500MHz :rx5281 prid=0xdc02                           | 
| RAM          | x                   | 64 MiB @ 1066 MHz                                         |
| Serial Flash | XMC XM25QH64A       | with page size 256 Bytes, erase size 64 KiB, total 8 MiB. |
| Sensor       | SC2232H             |                                                           | 

### Flash Layout

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


- - - - -

### Notes

Turning on Diagnostics in the Tapo app results in a `root` login on `pts/0`

**TODOs:**
* Do we need an internet connection to trigger this, can we do the same from local network with internet access ?  

```
[   58.336000] Erase from 0X40000 to 0X50000:
[   58.348000] .
[   58.353000] Program from 0X40000 to 0X50000:
[   58.560000] .
write successfully
1600115448305|696|3|cloud_interface.c:720:tlcc_refresh_helloCloud| - tlcc_refresh_helloCloud called
1600115448307|543|3|cloud_client_handle.c:1087:cloud_client_handle_refresh_helloCloud| - cloud_client_handle_refresh_helloCloud called
1600115448343|696|3|cloud_register.c:847:register_handle_refresh_hellocloud_request| - register_handle_refresh_hellocloud_request called
Sep 14 22:30:48 login[1274]: root login on 'pts/0'
```
* Dump the Flash (CLIP + Flash Reader, or can we get somehow access to the U-Boot console and read it out?)

- - - - -

### Links

[TE7C200 - FCCid.io](https://fccid.io/TE7C200)
