# Odroid HC-1 Cluster Build

With a little inspiration from the [200TB Glusterfs Odroid HC-2 Build](https://www.reddit.com/r/DataHoarder/comments/8ocjxz/200tb_glusterfs_odroid_hc2_build/) posted to [/r/DataHoarder/](https://www.reddit.com/r/DataHoarder/) a while back and a whole lot of [bonus.ly](https://bonus.ly/) dollars from work, I have finally completed my 3 node HC-1 cluster build and want to share my experiences with anyone else wanting to checkout single board computing for themselves.  Unlike the massive amount of storage provided by the [Odroid HC-2](https://www.hardkernel.com/main/products/prdt_info.php?g_code=G151505170472) build, I am using the [Odroid HC-1](https://www.hardkernel.com/main/products/prdt_info.php?g_code=G150229074080).  The main difference being, it will only fit a 2.5" drive, where the HC-2 will fit a full size 3.5 inch HDD.  The purpose of this build is not a NAS, but rather a focus on clustering software itself.  Primarily, Docker Swarm backed by Gluster.  Future plans also include testing Elasticsearch, Hadoop, and any other clustering software that [sparks](https://spark.apache.org/) my interest.

![Odroid Front](https://github.com/jahrik/odroid_cluster/blob/master/pics/odroid_02.jpg)

## Parts List
Here is the complete parts list and prices in US $.  There are a couple of ways you could go with powering this, so I will create two lists for power, including tools and other things I bought to make the build a little better, but are not necessary for it to work.  All of it was purchased from Amazon, so prices may vary a bit.

### Odroid
| Part        |  Amount  |  Price  | Total |
|:----------- |:--------:|:-------:| -----:|
| [Odroid HC-1](https://www.amazon.com/gp/product/B075TGWW8N/ref=oh_aui_detailpage_o01_s00?ie=UTF8&psc=1) | 3 | $59.95 + $7.15 shipping | $192.31 if purchased and shipped together |
| [32GB MicroSD](https://www.amazon.com/gp/product/B06XWN9Q99/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1) | 3 | $11.49 | $34.47 |
| [240GB SSD](https://www.amazon.com/gp/product/B01M61OWRI/ref=oh_aui_detailpage_o00_s01?ie=UTF8&psc=1) | 3 | $47.99 | $143.97 |
| [80mm Fan](https://www.amazon.com/gp/product/B07DXNT9J9/ref=oh_aui_detailpage_o02_s00?ie=UTF8&psc=1) | 1 | $15.95 | $15.95 |
| [6 pack Cat 6 Ethernet Cable 1 ft](https://www.amazon.com/gp/product/B01IQWGKQ6/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1) | 1 | $8.90 | $8.90 |
|**Total**|||**$395.60**|

### Power option #1 - Standard Odroid power supplies
| Part        |  Amount  |  Price  | Total |
|:----------- |:--------:|:-------:| -----:|
| [5V 4A Power Supply US Plug](https://www.amazon.com/gp/product/B0749668H2/ref=oh_aui_detailpage_o04_s00?ie=UTF8&psc=1) | 3 | $15.95 | $47.85 |
|**Total**|||**$47.85**|

### Power option #2 - What I did.
| Part        |  Amount  |  Price  | Total |
|:----------- |:--------:|:-------:| -----:|
| [5V 20A Power Supply](https://www.amazon.com/gp/product/B06XK2DDW4/ref=oh_aui_detailpage_o04_s01?ie=UTF8&psc=1) | 1 | $17.99 | $17.99 |
| [9 Port 40A Power Splitter](https://www.amazon.com/gp/product/B074QMRBPB/ref=od_aui_detailpages00?ie=UTF8&psc=1) | 1 | $58.00 | $58.00 |
| [20 pack 10 inch 2.1 x 5.5mm Male DC Power Pigtail Connectors](https://www.amazon.com/gp/product/B0725BCVH1/ref=od_aui_detailpages00?ie=UTF8&psc=1) | 1 | $9.99 | $9.99 |
| [Wire Crimping Tool for Powerpole](https://www.amazon.com/gp/product/B01MZZZ19P/ref=od_aui_detailpages00?ie=UTF8&psc=1) | 1 | $34.99 | $34.99 |
| [15 Amp Unassembled Red/Black Anderson Powerpole Connectors](https://www.amazon.com/gp/product/B01HDZ1ERC/ref=oh_aui_detailpage_o03_s00?ie=UTF8&psc=1) | 1 | $16.47 | $16.47 |
| [Heat Gun](https://www.amazon.com/gp/product/B000X4SMRQ/ref=od_aui_detailpages00?ie=UTF8&psc=1) | 1 | $23.94 | $23.94 |
| [Heat Shrink Tubing](https://www.amazon.com/gp/product/B072PCQ2LW/ref=od_aui_detailpages00?ie=UTF8&psc=1) | 1 | $8.99 | $8.99 |
| [10 pack 4 Amp Two Prong Blade Plug-in ATC Fuses](https://www.amazon.com/gp/product/B01HDUCOT4/ref=oh_aui_detailpage_o05_s00?ie=UTF8&psc=1) | 1 | $6.30 | $6.30 |
|**Total**|||**$176.67**|

## Putting it all together

### Power

![Power Supply](https://github.com/jahrik/odroid_cluster/blob/master/pics/power_supply.jpg)

The [5V 20A Power Supply](https://www.amazon.com/gp/product/B06XK2DDW4/ref=oh_aui_detailpage_o04_s01?ie=UTF8&psc=1) I went with, should be enough to power 5 HC-1's at load, which is good enough for what I have planned.  I used a Powerpole power splitter for the first time ever and am pretty happy with how it turned out.  I can easily make a new power cable, add a 4 Amp fuse and add another node to the cluster.

![Odroid Front](https://github.com/jahrik/odroid_cluster/blob/master/pics/odroid_01.jpg)

The 5V 4A power brick you can order with the HC-1 works just fine and that's what I used while evaluating the first one.  I don't want to manage 3 to 5 of those blocks in my already filling up power strip on the bottom shelf of the rack, so that is why I went with a solution that should scale with the number of nodes I want and then some.

From failed attempts at trying to power up the HC-1 with it plugged into USB power bricks, I discovered that even if you buy a USB power supply that advertises 12 Amps, they're still most likely limited to 2.5 Amps per USB port.  This is great for a Pi, but will not run the HC-1.

**This will not work**

![USB Power Supply](https://github.com/jahrik/odroid_cluster/blob/master/pics/usb_power_supply.jpg)

### Cooling

I bought the 5V USB model and tested it plugged in to the front of one of the HC-1 and it worked great, but I opted to take a spare connector and plug it directly in to the power splitter.  This means it runs at full speed at all times, but so far, that hasn't been a problem.  Things stay very cool and the fan barely makes any noise, even at full speed. I've been happy with every Noctua fan I've bought.

![Odroid Back](https://github.com/jahrik/odroid_cluster/blob/master/pics/odroid_03.jpg)

### OS

I started with a single HC-1 to see how it worked before purchasing another two.  I wanted a quick comparison from the couple of Raspberry Pi 3B+ I have been playing around with and was happy with what I found.  So far, I've been able to get ubuntu 16.04 and 18.04 running, from [images found on the Odroid site](https://wiki.odroid.com/odroid-xu4/os_images/os_images).  I tested [Armbian](https://www.armbian.com/odroid-hc1/), but wasn't able to get a shell onto the box after.  Not sure if ssh is enabled by default or not.  Also, tested [Arch](https://archlinuxarm.org/platforms/armv7/samsung/odroid-xu4) without success, so far.  I'm happy with ubuntu 18.04 right now because Docker Swarm seams to be working as it should with armhf 32 bit applications.  I was having weird Kernel errors when I tested Docker swarm on ubuntu 16.04 and wasn't ever able to get Swarm mode working, however was able to start Docker containers in stand alone Docker mode.

**example error output for ubuntu 16.04 in swarm mode**

    docker service ps --no-trunc ubuntu_ubuntu

    ID                          NAME                  IMAGE                                                                                               NODE                DESIRED STATE       CURRENT STATE             ERROR                                                                                                                   PORTS
    jip55rydfymv3leidoxfc2fiy   ubuntu_ubuntu.1       armv7/armhf-ubuntu:latest@sha256:fc32949ab8547c9400bb804004aa3d36fd53d2fedba064a9594a173a6ed4a3b6   ninjara.dojo.io     Ready               Rejected 1 second ago     "subnet sandbox join failed for "10.0.0.0/24": error creating vxlan interface: operation not supported"

But, things seam to work great in 18.04, so that's what I'm sticking with for now.

