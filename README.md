# tplink-tapo-c200-re
Reverse Engineering the TP-Link Tapo C200 camera


### Components
| Name         | Component           | Description                                               |
| ------------ | -------------       | --------------------------------------------------------- | 
| SoC          | Realtek RTS3903     | CPU: 500MHz :rx5281 prid=0xdc02                           | 
| RAM          | x                   | 64 MiB @ 1066 MHz                                         |
| Serial Flash | XMC XM25QH64A       | with page size 256 Bytes, erase size 64 KiB, total 8 MiB. |

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


