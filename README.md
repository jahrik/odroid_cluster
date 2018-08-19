# Odroid HC-1 Cluster Build

With a little inspiration from the [200TB Glusterfs Odroid HC-2 Build](https://www.reddit.com/r/DataHoarder/comments/8ocjxz/200tb_glusterfs_odroid_hc2_build/) posted to [/r/DataHoarder/](https://www.reddit.com/r/DataHoarder/) a while back and a whole lot of [bonus.ly](https://bonus.ly/) dollars from work, I have finally completed my 3 node HC-1 cluster build and want to share my experiences with anyone else wanting to checkout single board computing for themselves.  Unlike the massive amount of storage provided from the [Odroid HC-2](https://www.hardkernel.com/main/products/prdt_info.php?g_code=G151505170472) build, I am using the [Odroid HC-1](https://www.hardkernel.com/main/products/prdt_info.php?g_code=G150229074080).  The main difference being, it will only fit a 2.5" drive, where the HC-2 will fit a full size 3.5 inch HDD.  The purpose of this build is not a NAS, but rather a focus on clustering software itself.  Primarily, Docker Swarm backed by Gluster.  Future plans also include testing Elasticsearch, Hadoop, and any other clustering software that [sparks](https://spark.apache.org/) my interest.

## Pics
![Odroid Front](https://github.com/jahrik/odroid_cluster/blob/master/pics/odroid_01.jpg)
![Odroid Front](https://github.com/jahrik/odroid_cluster/blob/master/pics/odroid_02.jpg)
![Odroid Back](https://github.com/jahrik/odroid_cluster/blob/master/pics/odroid_03.jpg)

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


### Power option #1 - What I did.
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

### Power option #2 - Standard Odroid power supplies
| Part        |  Amount  |  Price  | Total |
|:----------- |:--------:|:-------:| -----:|
| [5V 4A Power Supply US Plug](https://www.amazon.com/gp/product/B0749668H2/ref=oh_aui_detailpage_o04_s00?ie=UTF8&psc=1) | 3 | $15.95 | $47.85 |
|**Total**|||**$47.85**|
