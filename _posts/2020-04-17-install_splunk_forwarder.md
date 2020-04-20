---
layout: post
author: kenji
category: splunk
---
Followed the instruction on this page.
https://docs.splunk.com/Documentation/Forwarder/8.0.3/Forwarder/HowtoforwarddatatoSplunkEnterprise


# Steps
1. Configure receiving on a Splunk Enterprise instance or cluster.
2. Download and install the universal forwarder.
3. Start the universal forwarder and accept the license agreement. Some installers do this for you.
4. (Optional) Change the credentials on the universal forwarder from their defaults.
5. Configure the universal forwarder to send data to the Splunk Enterprise instance.
6. (Optional) Configure the universal forwarder to act as a deployment client.
7. Configure the universal forwarder to collect data from the host it is on.

# Configure receiving on Splunk Enterprise
Run this command:
> splunk enable listen <port> -auth <username>:<password>
Use port `9997`. This is the convention.

Or add the following setting in `inputs.conf` in `$SPLUNK_HOME/etc/system/local`.
```
[splunktcp://9997]
disabled = 0
```
Then restart.



# Download and install the universal forwarder
[From this page, ](https://www.splunk.com/en_us/download/universal-forwarder.html#tabs/linux)

# Start the universal forwarder
> cd $SPLUNK_HOME/bin ./splunk start

## Start the forwarder as root

## Configure the universal forwarder to send data to the Splunk Enterprise indexer
```
./splunk add forward-server ip_of_splunk_enterprise:9997
```

## Configure the universal forwarder as a deployment client
```
./splunk set deploy-poll ip_of_splunk_enterprise:8089

```

## Check data is coming from the forwarder
Running search 
```
index=_internal
```
now shows multiple hosts.

## Remark
I have to expand the disksize and partition of ec2 instance
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/recognize-expanded-volume-linux.html

```
[root@ip-123-45-67-891 ec2-user]# df -h
Filesystem      Size  Used Avail Use% Mounted on
devtmpfs        391M     0  391M   0% /dev
tmpfs           410M     0  410M   0% /dev/shm
tmpfs           410M   32M  379M   8% /run
tmpfs           410M     0  410M   0% /sys/fs/cgroup
/dev/xvda2       10G  5.5G  4.6G  55% /
tmpfs            82M     0   82M   0% /run/user/1000
[root@ip-123-45-67-891 ec2-user]# fdisk -l
Disk /dev/xvda: 20 GiB, 21474836480 bytes, 41943040 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xe6e324f2

Device     Boot Start      End  Sectors Size Id Type
/dev/xvda1       2048     4095     2048   1M 83 Linux
/dev/xvda2 *     4096 20971486 20967391  10G 83 Linux
[root@ip-123-45-67-891 ec2-user]# lsblk
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0  20G  0 disk
|-xvda1 202:1    0   1M  0 part
-xvda2 202:2    0  20G  0 part /
[root@ip-123-45-67-891 ec2-user]# l

sudo xfs_growfs -d /
```