Sgx+Fabric 智能合约开发

首先需要了解fabric2.0的智能合约编译步骤。这种编译方式在没有sgx的情况下效果很好，不过有sgx，就没什么优势了。（因为ccenv和baseos都需要sgxsdk套装）

所有的输出文件都要放在/chaincode/output中
Go build不需要写到Makefile中，因为fabric会帮你build
用.a 还是 .so 暂时没有什么区别。可能.a 好一点?
目录结构，sgx的c文件都放在sgx目录里面，sgx里面写一个Makefile，基本抄一抄sgx的demo就可以了。
Sgx的Makefile里，enclave.signed.so相关的都不用动，App端的需要修改。首先App端的入口函数不用写了，写成一个普通的函数，然后封装成.a文件。

可以看一下github上我的修改，就明白了

Docker image改成ubuntu有3个原因：
1.fabric-private-chaincode用的是ubuntu
2.安装sgx sdk不需要从头编译，用deb安装
3.可以动态链接

/var/run/Aesmd我都会挂到docker container里面，这是改了源码的
/dev/isgx也一样，也是会挂到docker container

修改后的fabric，一样可以兼容不用sgx的场景

如果你需要从头build 容器，需要把一个golang的压缩包放到images/ccenv目录下。注意名字和dockerfile里面一样。为了节省下载golang安装包的时间。但是golang压缩包>100M，无法放到github上面。

需要哪些sgxsdk的so，需要查一下文档

如果写cgo的时候，爆undefined reference错误，尝试修改一下LDFLAG的顺序。把libapp.a放在最后。
