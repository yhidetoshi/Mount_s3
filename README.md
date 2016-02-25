# mount_s3
### Mac上のローカルVMからs3へマウントする方法

#### s3コンソールで設定
 - s3 IAMでs3接続するためのユーザを作成
 
#### Linux側での設定
```
yum -y update
yum -y groupinstall "Development Tools" 
yum -y install openssl-devel 
yum -y install libcurl-devel 
```
