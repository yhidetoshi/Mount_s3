# mount_s3
### Mac上のローカルVMからs3へマウントする方法

#### s3コンソールで設定
 - s3 IAMでs3接続するためのユーザを作成
 
#### Linux側での設定
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
# git clone https://github.com/s3fs-fuse/s3fs-fuse.git
# cd s3fs-fuse/
# ./autogen.sh
# make
# make install

-- s3fs setting --
# echo '(Access Key ID):(Secret Access Key)' > /etc/passwd-s3fs

```
