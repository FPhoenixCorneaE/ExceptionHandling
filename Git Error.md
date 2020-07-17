**一、Error：RPC failed; curl 56 OpenSSL SSL_read: SSL_ERROR_SYSCALL, errno 10054
fatal: the remote end hung up unexpectedly
fatal: protocol error: bad pack header**

解决方案：   <br>
git config --global pack.windowMemory "100m"   <br>
git config --global pack.SizeLimit "100m"   <br>
git config --global pack.threads "1"   <br>
git config --global pack.window "0"   <br>

**二、Error：RPC failed; curl 18 transfer closed with outstanding read data remaining**

- **原因1：缓存区溢出**   <br>
解决方法：命令行输入   <br>
git config --global http.postBuffer 524288000   <br>

- **原因2：服务器的SSL证书没有经过第三方机构的签署**   <br>
git config --global http.sslVerify "false"

- **原因3：网络下载速度缓慢**   <br>
解决方法：命令行输入   <br>
git config --global http.lowSpeedLimit 0   <br>
git config --global http.lowSpeedTime 999999   <br>

- **如果依旧clone失败，则首先浅层clone，然后更新远程库到本地**   <br>
git clone --depth=1 https://github.com/xxx/xxx.git   <br>
git fetch --unshallow   <br>