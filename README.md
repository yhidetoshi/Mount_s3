# Fuseとs3fsを使ってCentOSからマウントさせる

### Mac上のローカルVMからs3へマウントする方法
 - VirtualBox
 - CentOS6.7

#### s3コンソールで設定
 - s3 IAMでs3接続するためのユーザを作成
 
#### Linux側(Client)での設定
```
-- fuse download&install --
# yum -y update
# yum -y groupinstall "Development Tools" 
# yum -y install openssl-devel 
# yum -y install libcurl-devel 
# yum -y install libxml2-devel
# cd /usr/local/
# wget https://github.com/libfuse/libfuse/releases/download/fuse_2_9_5/fuse-2.9.5.tar.gz
# tar xvzf fuse-2.9.5.tar.gz
# cd fuse-2.9.5
# ./configure --prefix=/usr
# make
# make install
# ldconfig
# modprobe fuse

-- s3fs download&install --
# cd/usr/local/src
# mkdir /mnt/s3
# git clone https://github.com/s3fs-fuse/s3fs-fuse.git
# yum -y install gcc-c++ fuse fuse-devel libcurl-devel libxml2-devel  openssl-devel

# cd s3fs-fuse/
# ./configure --prefix=/usr
# make
# make install
# whereis s3fs

-- s3fs setting (/mnt/s3にマウントする場合)--
# echo 'Access Key ID:Secret Access Key' > /etc/passwd-s3fs
 → Access Key ID と Secret Access KeyはAWSコンソールのIAMから参照
# chmod 640 /etc/passwd-s3fs
# s3fs <バケット名> /mnt/s3/ -o allow_other,default_acl=private-read
 → マウント時にこのエラーができたら下記の2行を実施<library too old, some operations may not not work>
 1: # yum erase fuse-devel fuse-libs
 2: # fusermount -u /mnt/s3

再度マウントを実行
# s3fs <bucket_name> /mnt/s3/ -o allow_other,default_acl=private-read
```

 - ファイルシステムを見てるみと
```
# df -h
Filesystem            Size  Used Avail Use% Mounted on
/dev/mapper/vg_test01-lv_root
                      6.5G  3.1G  3.2G  50% /
tmpfs                 372M   76K  372M   1% /dev/shm
/dev/sda1             477M   70M  382M  16% /boot
s3fs                  256T     0  256T   0% /mnt/s3
```

- OS再起動しても自動マウントさせるためにfstabに書き込む
```
s3fs#<bucket_name>      /mnt/s3               fuse    defaults        0 0
```
