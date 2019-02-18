# Meraki-Firmware-MTD
I could not find a way to contact you so Ive reached out this way.  I've written a new machine for QEMU that emulates the Atheros AR9344.  It can boot from NAND device.  I was able to use the Meraki mtd dumps from your github repository to test it, required adding the OOB/ECC to the image but i can boot up to the point of loading mtd4(the UBI partition/rootfs). Do you by chance have the missing mtd partitions.  I would like to see if the emulation will get me to linux shell?

Screen Dump:
jloyamd@ubuntu:~/Desktop/qemu$ make
  CC      mips-softmmu/hw/mips/ath_nand.o
  LINK    mips-softmmu/qemu-system-mips
jloyamd@ubuntu:~/Desktop/qemu$ ./mips-softmmu/qemu-system-mips -M ar71xx -m 512M -no-reboot -nographic -bios ../uboot-mdb-dump/wasp_bootrom.bin  -mtdblock ../sunxi-tools/meraki_nand_new.img -serial null -serial mon:stdio -s -S
WARNING: Image format was not specified for '../sunxi-tools/meraki_nand_new.img' and probing guessed raw.
         Automatically detecting the format is dangerous for raw images, write operations on block 0 will be restricted.
         Specify the 'raw' format explicitly to remove the restrictions.
find_hif: bootstrap = 0x2f051b
WASP BootROM Ver. 1.3
Nand Flash init
otp_get_nand_table: 0xde 0xad 0xbe 0xef 0xde 0xad 0xbe 0xef 
ONFI: Control Setting = 0xb45
hdr: [0xbd001000 : 0xbd001000 : 0x6104 : 0xb8a746df]
nand_load_fw: read 12 pages
nand_load_fw: 0x10000 0x800 0xbd0017f0
nand_load_fw: 0x20000 0x800 0xbd001ff0
nand_load_fw: 0x30000 0x800 0xbd0027f0
nand_load_fw: 0x40000 0x800 0xbd002ff0
nand_load_fw: 0x50000 0x800 0xbd0037f0
nand_load_fw: 0x60000 0x800 0xbd003ff0
nand_load_fw: 0x70000 0x800 0xbd0047f0
nand_load_fw: 0x80000 0x800 0xbd004ff0
nand_load_fw: 0x90000 0x800 0xbd0057f0
nand_load_fw: 0xa0000 0x800 0xbd005ff0
nand_load_fw: 0xb0000 0x800 0xbd0067f0
nand_load_fw: 0xc0000 0x800 0xbd006ff0
f/w 0 read complete, jumping to 0xbd001000



Meraki Atheros LinuxLoader built Jul 23 2012 15:31:10
init_ddr ok
test_memory ok
D-cache size: 2K
I-cache size: 2K
init_dram_uncached ok
init_icache ok
init_dcache ok
enable_caches ok
test_memory ok
init_usb_phy ok
init_pcie_plls ok
nand_flash_init ok
loading fw at 64
hdr: [0x4d495053 : 0x80002000 : 0x3d9b80 : 0x80277610, : 0xf38c2a82]
..............................
Linux version 2.6.32.59-svn95486 (jdizzle@delilah) (gcc version 4.5.3 (GCC) ) #13 Fri Oct 5 17:19:32 PDT 2012
flash_size passed from bootloader = 2111
bootconsole [early0] enabled
CPU revision is: 00019700 (MIPS 74Kc)
FPU revision is: 00739300
ath_sys_frequency: cpu srif ddr srif cpu 560 ddr 400 ahb 200
Booting Atheros AR934x
Determined physical RAM map:
 memory: 02000000 @ 00000000 (usable)
User-defined physical RAM map:
 memory: 07ffc000 @ 00000000 (usable)
Initrd not found or empty - disabling initrd
Zone PFN ranges:
  Normal   0x00000000 -> 0x00007ffc
Movable zone start PFN for each node
early_node_map[1] active PFN ranges
    0: 0x00000000 -> 0x00007ffc
Built 1 zonelists in Zone order, mobility grouping on.  Total pages: 32508
Kernel command line: console=ttyS0,115200 mtdparts=ath-nand:128K(loader1),8064K(bootkernel1),128K(loader2),8064K(bootkernel2),114560K(ubi),128K(origcaldata) ubi.mtd=ubi mem=131056K
PID hash table entries: 512 (order: -1, 2048 bytes)
Dentry cache hash table entries: 16384 (order: 4, 65536 bytes)
Inode-cache hash table entries: 8192 (order: 3, 32768 bytes)
Primary instruction cache 2kB, VIPT, 2-way, linesize 16 bytes.
Primary data cache 2kB, 2-way, VIPT, no aliases, linesize 16 bytes
Writing ErrCtl register=00000000
Readback ErrCtl register=00000000
Memory: 125696k/131056k available (2555k kernel code, 5176k reserved, 698k data, 688k init, 0k highmem)
Hierarchical RCU implementation.
NR_IRQS:128
plat_time_init: plat time init done
Calibrating delay loop... 2646.01 BogoMIPS (lpj=5292032)
Mount-cache hash table entries: 512
NET: Registered protocol family 16
***** Warning *****: PCIe WLAN H/W not found !!!
bio: create slab <bio-0> at 0
vgaarb: loaded
SCSI subsystem initialized
usbcore: registered new interface driver usbfs
usbcore: registered new interface driver hub
usbcore: registered new device driver usb
Switching to clocksource MIPS
ATHR_GMAC: Length per segment 512
ATHR_GMAC: fifo cfg 3 01f00140
ATHR_GMAC: RX TASKLET - Pkts per Intr:100
ATHR_GMAC: Mac address for unit 0:bfff0000
ATHR_GMAC: 00:00:00:00:00:00 
ATHR_GMAC: Max segments per packet :   1
ATHR_GMAC: Max tx descriptor count :   100
ATHR_GMAC: Max rx descriptor count :   252
ATHR_GMAC: Mac capability flags    :   2381
WASP  ----> S17 PHY *
ATHR_GMAC: Powered down LAN port phys
NET: Registered protocol family 2
IP route cache hash table entries: 1024 (order: 0, 4096 bytes)
TCP established hash table entries: 4096 (order: 3, 32768 bytes)
TCP bind hash table entries: 4096 (order: 2, 16384 bytes)
TCP: Hash tables configured (established 4096 bind 4096)
TCP reno registered
NET: Registered protocol family 1
MERAKI GLUON INIT
ATH GPIOC major 0
squashfs: version 4.0 (2009/01/31) Phillip Lougher
Registering unionfs 2.5.10 (for 2.6.32.46)
msgmni has been set to 245
io scheduler noop registered
io scheduler deadline registered (default)
Trying to register dev faulty etc
Serial: 8250/16550 driver, 1 ports, IRQ sharing disabled
serial8250.0: ttyS0 at MMIO 0xb8020000 (irq = 19) is a 16550A
console [ttyS0] enabled, bootconsole disabled
console [ttyS0] enabled, bootconsole disabled
brd: module loaded
ONFI flash detected
ONFI param page 0 valid
NAND device: Manufacturer ID: 0xad, Chip ID: 0xda (Hynix H27U2G8F2CTR-BC)
Scanning device for bad blocks
6 cmdlinepart partitions found on MTD device ath-nand
Creating 6 MTD partitions on "ath-nand":
0x000000000000-0x000000020000 : "loader1"
0x000000020000-0x000000800000 : "bootkernel1"
0x000000800000-0x000000820000 : "loader2"
0x000000820000-0x000001000000 : "bootkernel2"
0x000001000000-0x000007fe0000 : "ubi"
0x000007fe0000-0x000008000000 : "origcaldata"
UBI: attaching mtd4 to ubi0
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
UBI: physical eraseblock size:   131072 bytes (128 KiB)
UBI: logical eraseblock size:    129024 bytes
UBI: smallest flash I/O unit:    2048
UBI: sub-page size:              512
UBI: VID header offset:          512 (aligned 512)
UBI: data offset:                2048
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
UBI error: ubi_io_read: error -77 (ECC error) while reading 64 bytes from PEB 0:0, read 64 bytes
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
UBI error: ubi_io_read: error -77 (ECC error) while reading 512 bytes from PEB 0:512, read 512 bytes
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
UBI error: ubi_io_read: error -77 (ECC error) while reading 64 bytes from PEB 1:0, read 64 bytes
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
ecc unrecoverable error
UBI error: ubi_io_read: error -77 (ECC error) while reading 512 bytes from PEB 1:512, read 512 bytes
UBI: max. sequence number:       0
UBI error: ubi_read_volume_table: the layout volume was not found
UBI error: ubi_init: cannot attach mtd4
Atheros(R) L2 Ethernet Driver - version 2.2.3
Copyright (c) 2007 Atheros Corporation.
input: gpio-keys as /class/input/input0
usbcore: registered new interface driver usbhid
usbhid: v2.6:USB HID core driver
TCP cubic registered
Initializing XFRM netlink socket
NET: Registered protocol family 17
NET: Registered protocol family 15
802.1Q VLAN Support v1.8 Ben Greear <greearb@candelatech.com>
All bugs added by David S. Miller <davem@redhat.com>
athwdt_init: Registering WDT success
ath_otp_init: Registering OTP success
ath_clksw_init: Registering Clock Switch Interface success
Freeing unused kernel memory: 688k freed
  
  Thanks!
