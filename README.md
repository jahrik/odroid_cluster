# Odroid HC-1 Cluster Build

With a little inspiration from the [200TB Glusterfs Odroid HC-2 Build](https://www.reddit.com/r/DataHoarder/comments/8ocjxz/200tb_glusterfs_odroid_hc2_build/) posted to [/r/DataHoarder/](https://www.reddit.com/r/DataHoarder/) a while back and a whole lot of [bonus.ly](https://bonus.ly/) dollars from work, I have finally completed my 3 node HC-1 cluster build and want to share my experiences with anyone else wanting to checkout single board computing for themselves.  Unlike the massive amount of storage provided from the [Odroid HC-2](https://www.hardkernel.com/main/products/prdt_info.php?g_code=G151505170472) build, I am using the [Odroid HC-1](https://www.hardkernel.com/main/products/prdt_info.php?g_code=G150229074080).  The main difference being, it will only fit a 2.5" drive, where the HC-2 will fit a full size 3.5 inch HDD.  The purpose of this build is not a NAS, but rather a focus on clustering software itself.  Primarily, Docker Swarm backed by Gluster.  Future plans also include testing Elasticsearch, Hadoop, and any other clustering software that [sparks](https://spark.apache.org/) my interest.


