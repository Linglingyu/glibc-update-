glibc升级从2.13到2.29
查看glibc版本 cd /lib
1.	首先从下载glibc源码。http://ftp.gnu.org/gnu/libc/
2.	使用交叉编译工具编译glibc的动态链接库。
  I.	注意：不能在glibc源码所在的文件夹编译，可以在glibc源码的上一级目录建立glibc_build目录。需要指定--prefix参数。
  II.	在glibc_build目录下执行：
  III.	../glibc-glibc-INTEL_RELEASE/configure --prefix=/home/liulingyu/tmp host=armv5-unknown-linux-gnueabi
  IV.	Make & make check
  V.	Glibc的动态链接库包含多个.so文件。（glibc各个库的作用介绍https://www.cnblogs.com/cute/archive/2011/05/03/2035645.html）
3.	使用原本的交叉编译工具链：很多工具没有或者版本太老（gcc version 4.7.1）。需要升级交叉编译工具链的版本。
 
 
4.	使用crosstool-NG生成交叉编译工具链。（http://crosstool-ng.github.io/）下载安装crosstool-ng。10.239.56.191上有一个安装好的版本可以直接拿来用。（查看版本号：ct-ng version）
5.	新建一个目录，在其中执行ct-ng menuconfig 配置host型号，操作系统版本号等。保存后当前目录里会生成一个.config文件。（查看示例配置：ct-ng list-samples。Menuconfig之前先生成一个原始版本的配置：ct-ng arm-unknown-linux-gnueabi）
6.	执行Ct-ng build生成交叉编译工具链。生成的交叉编译工具链存放在~/x-tools/armv5-unknown-linux-gnueabi目录（该地址通过ct-ng menuconfig里的Prefix directory配置）。
7.	使用新生成的交叉编译工具链编译glibc，具体参考步骤2.



参考：
crosstool-ng详解
From <https://www.crifan.com/files/doc/docbook/crosstool_ng/release/html/crosstool_ng.html>
