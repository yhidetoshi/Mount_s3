# mount_s3
### Mac上のローカルVMからs3へマウントする方法

#### s3コンソールで設定
 - s3 IAMでs3接続するためのユーザを作成
 
#### Linux側での設定
```
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
```
