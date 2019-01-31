### 1. 镜像文件选择 quay.io/external_storage/nfs-client-provisioner:latest
### 2.采用动态生成pv的方式特别要注意nfs服务端和客户端的配置
* nfs服务端的配置
```css
安装nfs-utils和rpcbind:yum -y install nfs-utils rpcbind
```
```css
配置/etc/exports,如：/app/share *(rw,no_subtree_check,no_root_squash)
```
```css
启动nfs和rpcbind服务：systemctl start rpcbind,systemctl start nfs
执行exportfs -ar命令可以使修改的/etc/exports立即生效，不需要重启nfs服务
```
* nfs客户端配置（每个节点都要安装）
```css
安装nfs-utils:yum -y install nfs-utils
```
### 3. nfs安装和配置具体可参照：https://www.cnblogs.com/liuyisai/p/5992511.html
### 4. FAQ

```css
nfs环境搭建报错clnt_create: RPC: Program not registered
有时候搭建完成后，使用showmount -e ip检测服务端服务器情况的是，会出现clnt_create: RPC: Program not registered
这个错误，表示rpc程序为注册成功，解决方案就是：
以此关闭nfs和rpcbind
命令:
/etc/init.d/nfs stop
/etc/init.d/rpcbind stop
再依次启动服务：
命令：(注意先启动rpc)
/etc/init.d/rpcbind start
/etc/init.d/nfs start
```
