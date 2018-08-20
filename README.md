# Odroid HC-1 Cluster Build

With a little inspiration from the [200TB Glusterfs Odroid HC-2 Build](https://www.reddit.com/r/DataHoarder/comments/8ocjxz/200tb_glusterfs_odroid_hc2_build/) posted to [/r/DataHoarder/](https://www.reddit.com/r/DataHoarder/) a while back and a whole lot of [bonus.ly](https://bonus.ly/) dollars from work, I have finally completed my 3 node HC-1 cluster build am sharing my experience with anyone else wanting to check out single board computing for themselves.  Unlike the massive amount of storage provided by the [Odroid HC-2](https://www.hardkernel.com/main/products/prdt_info.php?g_code=G151505170472) build, I am using the [Odroid HC-1](https://www.hardkernel.com/main/products/prdt_info.php?g_code=G150229074080).  The main difference being, it will only fit a 2.5" drive, where the HC-2 will fit a full size 3.5 inch HDD.  The purpose of this build is not a NAS, but rather a focus on clustering software itself.  Primarily, Docker Swarm backed by Glusterfs.  Future plans also include testing Elasticsearch, Hadoop, and any other clustering software that [sparks](https://spark.apache.org/) my interest.

![Odroid Front](https://github.com/jahrik/odroid_cluster/blob/master/pics/odroid_01.jpg)

## Parts List
Here is the complete parts list and prices in US dollars.  There are a couple of ways you could go with powering this, so I will create two lists for power, including tools and other things I bought to make the build a little better, but are not necessary for it to work.  All of it was purchased from Amazon, so prices may vary a bit.

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

## Putting it together

I started with one Odroid and added to it over a few months.  I have been tinkering with a couple of Raspberry Pi 3B+ and having fun, but wanted something a bit more powerful for running tests and possibly use as a logging and analytics back end, down the road when I get bored with it and just make it do a thing for a while. 

### Power

![Power Supply](https://github.com/jahrik/odroid_cluster/blob/master/pics/power_supply.jpg)

The [5V 20A Power Supply](https://www.amazon.com/gp/product/B06XK2DDW4/ref=oh_aui_detailpage_o04_s01?ie=UTF8&psc=1) I went with, should be enough to power 5 HC-1's at load, which is good enough for what I have planned.  I used a Powerpole power splitter for the first time ever and am pretty happy with how it turned out.  I can easily make a new power cable, add a 4 Amp fuse, and add another node to the cluster.  Be sure and use the 15 Amp connectors, the 30 Amp connectors that came with the crimper are too big for these small wires.

![Odroid Front](https://github.com/jahrik/odroid_cluster/blob/master/pics/plug_parts.jpg)

The 5V 4A power brick you can order with the HC-1 works just fine and that's what I used while evaluating the first one, but I don't want to manage 3 to 5 of those blocks in my already filling up power strip on the bottom shelf of the rack, so that is why I went with a solution that will scale with the number of nodes I add and then some.

From failed attempts at trying to power up the HC-1 with it plugged into USB power bricks, I discovered that even if you buy a USB power supply that advertises 12 Amps, they're still most likely limited to 2.5 Amps per USB port.  This is great for a Pi, but will not run the HC-1.

**This will not work**

![USB Power Supply](https://github.com/jahrik/odroid_cluster/blob/master/pics/usb_power_supply.jpg)

### Cooling

I went with a 5V USB powered fan and tested it plugged in to the front of one of the HC-1 and it worked great, but I opted to take a spare connector and plug it directly in to the power splitter.  This means it runs at full speed at all times, but so far, that hasn't been a problem.  Things stay very cool and the fan barely makes any noise, even at full speed. I've been happy with every Noctua fan I've bought.

![Odroid Back](https://github.com/jahrik/odroid_cluster/blob/master/pics/odroid_03.jpg)

### OS

So far, I've been able to get ubuntu 16.04 and 18.04 running, from [images found on the Odroid site](https://wiki.odroid.com/odroid-xu4/os_images/os_images).  I tested [Armbian](https://www.armbian.com/odroid-hc1/), but wasn't able to get a shell onto the box after.  Not sure if ssh is enabled by default or not.  Also, tested [Arch](https://archlinuxarm.org/platforms/armv7/samsung/odroid-xu4) without success, so far.  I'm happy with ubuntu 18.04 right now because Docker Swarm seems to be working as it should with armhf 32 bit applications.  I was having weird Kernel errors when I tested Docker Swarm on ubuntu 16.04 and wasn't ever able to get Swarm services started, however was able to start Docker containers in stand alone Docker mode.

**example error output for ubuntu 16.04 in Swarm mode**

"subnet sandbox join failed for "10.0.0.0/24": error creating vxlan interface: operation not supported"

    docker service ps --no-trunc ubuntu_ubuntu

    ID                          NAME                  IMAGE                                                                                               NODE                DESIRED STATE       CURRENT STATE             ERROR                                                                                                                   PORTS
    jip55rydfymv3leidoxfc2fiy   ubuntu_ubuntu.1       armv7/armhf-ubuntu:latest@sha256:fc32949ab8547c9400bb804004aa3d36fd53d2fedba064a9594a173a6ed4a3b6   ninja.dojo.io     Ready               Rejected 1 second ago     "subnet sandbox join failed for "10.0.0.0/24": error creating vxlan interface: operation not supported"

But, things seem to work great in 18.04, so that's what I'm sticking with, for now.  I've had mixed results with Docker Swarm, so far, but standalone docker seams to work fine.  Glusterfs has been working very well on both 16.04 and 18.04 and kept working just fine on an upgrade from 16.04 to 18.04 without error.  So did Docker.  Elasticsearch 5.0.1 and 6.3.1 tested running well on the Odroid.  It was able to keep up with 3 packetbeat clients hitting it with network traffic, as well as, Kibana  and Grafana querying it on the front end.  I started putting that together in an Ansible role, [arm-elasticsearch](https://gitlab.com/jahrik/arm-elasticsearch).

#### Installation

With image at hand, installation is pretty simple.  Mount the micro SD and use dd to copy the image.

    sudo dd if=ubuntu-18.04-4.14-minimal-odroid-xu4-20180531.img of=/dev/mmcblk0 bs=4M status=progress                     
    1577058304 bytes (1.6 GB, 1.5 GiB) copied, 1 s, 1.6 GB/s
    499+1 records in
    499+1 records out
    2094006272 bytes (2.1 GB, 2.0 GiB) copied, 85.9404 s, 24.4 MB/s

Plug it in and connect an Ethernet cable.  You'll want a DHCP server running to give this new box an IP address.  Ping for 'odroid' until you see it come online, then ssh in to update the hostname, add a user, etc..  I'm leaving DHCP enabled and just relying on a hostname.

Defaults:
* user = root
* pass = odroid

Update /etc/hosts and /etc/hostname, ex. host 'ninja'

    root@odroid:~# cat /etc/hostname 
    ninja

    root@odroid:~# cat /etc/hosts
    127.0.0.1	ninja

Add a user, where user == your user

    root@odroid:~# adduser user

If you want ansible to have passwordless sudo, where user == your user

    root@odroid:~# cat /etc/sudoers.d/user
    user ALL=(ALL) NOPASSWD: ALL

Install a few dependencies, upgrade, and reboot.  Do this with all three nodes.

    apt update
    apt upgrade
    apt install vim
    apt install python

If you want passwordless ssh access, add an ssh key to each host.

    ssh-copy-id ninja
    ssh-copy-id oroku
    ssh-copy-id venus

Now that each node has an identity, a user with sudo and ssh access, and python installed, they are ready for Ansible provisioning.

### Glusterfs

One of the main purposes of this build is to test [Glusterfs](https://docs.gluster.org/en/latest/) as an alternative to mounting persistent Docker volumes to an NFS share.  Gluster seams to scale well enough and should keep up with scaling Docker Swarm nodes, as needed.  An NFS server is a valid solution for data persistence, but leaves a single point of failure.  If the NFS server goes down, it wouldn't matter how many nodes I had in my Swarm cluster, 3 or 30, I will have just lost any data that was stored on the NFS.  Replicating storage across all Swarm nodes would mean a Docker service could fail on node 00 and be automatically brought back up on node 01, where the data has been replicated, the volume would remount any directories from the gluster-client, and start back up with minimal down-time.  If configured with enough nodes and replication, you can potentially lose a hardware node or two and have things keep running normally, while you replace the underlying failed hardware.

Once I had the second Odroid, I started testing Glusterfs across two machines with 1 brick and a replication factor of 2.  Now that I have a third node, I've been testing a dispersed volume, but have been experiencing a lot of gluster-client connection issues.  Not sure what to chalk this up to just yet.  I have a lot more learning to do.  So, currently, I am running it across the three nodes with a replica factor of 3.  Meaning any file I write/delete to the SSD on node 00 will be written/deleted to the SSD on both nodes 01 and 02.  If I start a mysql Docker service with a mounted volume to this share, it should work on which ever node it starts on.

While Gluster isn't bad at all to set up manually, there is an Ansible module for [gluster_volume](https://docs.ansible.com/ansible/2.6/modules/gluster_volume_module.html) that makes setup way easier!  I followed Jeff Geerling's post on a [Simple GlusterFS Setup with Ansible](https://www.jeffgeerling.com/blog/simple-glusterfs-setup-ansible) to get started.  I also added in some tasks to handle disk partitioning and formatting for me.

* [gitlab.com/jahrik/arm-gluster](https://gitlab.com/jahrik/arm-gluster)

Each node has the following:
* python installed
* ansible user with ssh key access
* ansible user has sudo access

Starting with an inventory.ini file to define the hosts.

**inventory.ini**

    [gluster]
    ninja
    venus
    oroku

Test a connection

    ansible -i inventory.ini all -m ping

    oroku | SUCCESS => {
        "changed": false,
        "ping": "pong"
    }
    ninja | SUCCESS => {
        "changed": false,
        "ping": "pong"
    }
    venus | SUCCESS => {
        "changed": false,
        "ping": "pong"
    }

Create a playbook that will configure as many nodes as I add to this inventory.

First, define a couple of variables.

**playbook.yml**

    ---
    - hosts: gluster
      become: true
      vars:
        gluster_mount_dir: /mnt/g1
        gluster_brick_dir: /bricks/brick1
        gluster_brick_name: g1

With hosts being called and variables set, add tasks to partition the SSD drives.  Parted will be installed and used to Create a primary partition on /dev/sda, which is what the SSD card shows up at.  The micro SD will shows up as /dev/mmcblk0.

    tasks:

      - name: Install parted
        package:
          name: parted
          state: present
        tags:
          - setup

      - name: Create Primary partition
        parted:
          device: /dev/sda
          number: 1
          state: present
        tags:
          - setup

An ext4 file system is then created,

      - name: Create a ext4 filesystem on /dev/sda1
        filesystem:
          fstype: ext4
          dev: /dev/sda1
        tags:
          - setup

As well as any mount and volume directories.

      - name: Ensure Gluster brick and mount directories exist.
        file:
          path: "{{ item }}"
          state: directory
          mode: 0775
        with_items:
          - "{{ gluster_brick_dir }}"
          - "{{ gluster_mount_dir }}"


Which are then mounted and added to the /etc/fstab file.

      - name: Mount "{{ gluster_brick_dir }}"
        mount:
          path: "{{ gluster_brick_dir }}"
          src: /dev/sda1
          fstype: ext4
          state: present
        tags:
          - setup

The real magic happens with the gluster_volume module.  It will create the defined brick and reach out to any and all other nodes defined in the inventory file to add them to the cluster and start replication.  `force: yes` is only used because this is happening on the /dev/sda partition, which gluster assumes is the root partition, but in this case is not.

      - name: Configure Gluster volume.
        gluster_volume:
          state: present
          name: "{{ gluster_brick_name }}"
          brick: "{{ gluster_brick_dir }}"
          replicas: "{{ groups.gluster | length }}"
          cluster: "{{ groups.gluster | join(',') }}"
          host: "{{ inventory_hostname }}"
          force: yes
        run_once: true

Finally, mount the volume with the gluster-client.

      - name: Ensure Gluster volume is mounted.
        mount:
          name: "{{ gluster_mount_dir }}"
          src: "{{ inventory_hostname }}:/{{ gluster_brick_name }}"
          fstype: glusterfs
          opts: "defaults,_netdev,log-level=WARNING,log-file=/var/log/gluster.log"
          state: mounted

Run it with:

    ansible-playbook -i inventory.ini playbook.yml

    PLAY [gluster] ********************************************************************************************************

    TASK [Gathering Facts] ************************************************************************************************
    ok: [oroku]
    ok: [ninjara]
    ok: [venus]

    ...
    ...
    ...

    TASK [Configure Gluster volume.] **************************************************************************************
    ok: [ninjara]

    TASK [Ensure Gluster volume is mounted.] ******************************************************************************
    ok: [oroku]
    ok: [venus]
    ok: [ninjara]

    PLAY RECAP ************************************************************************************************************
    ninjara                    : ok=9    changed=0    unreachable=0    failed=0   
    oroku                      : ok=8    changed=0    unreachable=0    failed=0   
    venus                      : ok=8    changed=0    unreachable=0    failed=0  

Verify peers with:

    root@oroku:~# gluster peer status
    Number of Peers: 2

    Hostname: ninjara
    Uuid: 19c60517-d584-4cf2-9dcb-fedca9463507
    State: Peer in Cluster (Connected)

    Hostname: venus
    Uuid: f582eb76-97f0-483d-9a31-91c272915940
    State: Peer in Cluster (Connected)

Verify volume with:

    root@oroku:~# gluster volume status 
    Status of volume: g1
    Gluster process                             TCP Port  RDMA Port  Online  Pid
    ------------------------------------------------------------------------------
    Brick ninja:/bricks/brick1                  49152     0          Y       1689 
    Brick venus:/bricks/brick1                  49152     0          Y       1019 
    Brick oroku:/bricks/brick1                  49152     0          Y       10326
    NFS Server on localhost                     N/A       N/A        N       N/A  
    Self-heal Daemon on localhost               N/A       N/A        Y       10317
    NFS Server on ninjara                       N/A       N/A        N       N/A  
    Self-heal Daemon on ninjara                 N/A       N/A        Y       1680 
    NFS Server on venus                         N/A       N/A        N       N/A  
    Self-heal Daemon on venus                   N/A       N/A        Y       973  
     
    Task Status of Volume g1
    ------------------------------------------------------------------------------
    There are no active volume tasks

### Docker Swarm

Setting up Docker Swarm is easy enough, so I won't go in to too much detail and will do a lazy set up for this example.

### Mysql test

Where `/mnt/g1` is the mounted gluster share on every box.

**mysql-stack.yml**

    version: '3'

    services:

      mysql:
        image: hypriot/rpi-mysql
        environment:
          - MYSQL_ROOT_PASSWORD=root
          - MYSQL_DATABASE=test
          - MYSQL_USER=test
          - MYSQL_PASSWORD=test
        volumes:
          - /mnt/g1/mysql:/var/lib/mysql/
        ports:
          - 3306:3306

Deployed with:

    mkdir -p /mnt/g1/mysql
    docker stack deploy -c mysql-stack.yml mysql

With 3 nodes running, you can see the mysql directory is replicating to all 3 nodes

* ninja

    root@ninja:~# ls -list /mnt/g1/mysql/
    total 28684
    12866449624579713480  5120 -rw-rw---- 1 999 docker  5242880 Aug 19 09:04 ib_logfile0
     9617335984120224053     4 drwx------ 2 999 docker     4096 Aug 18 11:31 test
    13443460668165679553 18432 -rw-rw---- 1 999 docker 18874368 Aug 18 11:31 ibdata1
    10905877464947696036  5120 -rw-rw---- 1 999 docker  5242880 Aug 18 11:31 ib_logfile1
    12433439431064392233     4 drwx------ 2 999 docker     4096 Aug 18 11:31 mysql
    13446363851844762839     4 drwx------ 2 999 docker     4096 Aug 18 11:31 performance_schema

* venus

    root@venus:~# ls -list /mnt/g1/mysql/
    total 28684
    12866449624579713480  5120 -rw-rw---- 1 999 docker  5242880 Aug 19 09:04 ib_logfile0
     9617335984120224053     4 drwx------ 2 999 docker     4096 Aug 18 11:31 test
    13443460668165679553 18432 -rw-rw---- 1 999 docker 18874368 Aug 18 11:31 ibdata1
    10905877464947696036  5120 -rw-rw---- 1 999 docker  5242880 Aug 18 11:31 ib_logfile1
    12433439431064392233     4 drwx------ 2 999 docker     4096 Aug 18 11:31 mysql
    13446363851844762839     4 drwx------ 2 999 docker     4096 Aug 18 11:31 performance_schema

* oroku

    root@oroku:~# ls -list /mnt/g1/mysql/
    total 28684
    12866449624579713480  5120 -rw-rw---- 1 999 docker  5242880 Aug 19 09:04 ib_logfile0
     9617335984120224053     4 drwx------ 2 999 docker     4096 Aug 18 11:31 test
    13443460668165679553 18432 -rw-rw---- 1 999 docker 18874368 Aug 18 11:31 ibdata1
    10905877464947696036  5120 -rw-rw---- 1 999 docker  5242880 Aug 18 11:31 ib_logfile1
    12433439431064392233     4 drwx------ 2 999 docker     4096 Aug 18 11:31 mysql
    13446363851844762839     4 drwx------ 2 999 docker     4096 Aug 18 11:31 performance_schema

I'm thinking if all three of these nodes are running in Docker Swarm mode and the service dies and is restarted on any of the nodes, It will continue to have the same data on all three.  Have not tested this, yet.

