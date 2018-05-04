# 朱老师嵌入式课程系列学习-uboot-version-2013.10移植体验  
## 一、具体移植前注意环节： 
### 交叉编译工具链：
1）解压tar -jxvf xx.bz2到指定的目录; /bin：系统自带安装的软件；/sbin系统管理方面的应用程序；在/usr/local/arm/arm-2009/bin目录下， 但只会在当前的目录下能执行可执行程序，其他目录下并不能找到可执行程序。  
2）导入环境变量：相当于系统的全局变量-系统查找可执行程序的路径，当在不同的目录下都能执行这可执行程序；  
    echo $PATH  
    export PATH=/usr/local/arm/arm-2009q3/bin:$PATH  
    当前宿主目录下/root的.bashrc，不同的用户进入终端的时候都自动执行.bashrc；在.bashrc中添加上诉环境变量后，source .bashrc  
3）创建符号链接：  
    ln arm-none-linux-gnueabi-gcc -s arm-linux-gcc  

### X210官方配置编译实践
#### Uboot源码获取途径：(uboot官方、SOC官方（SMDKV210三星官方的开发板移植好的uboot）、具体开发板供应商九鼎科技)
1）配置uboot(uboot、kernel等复杂系统都是先配置然后编译)编译前应先检查是否安装交叉编译工具链；  
2）当前uboot中的主Makefile会设置交叉编译工具工具链的路径和名字147CROSS_COMPILE=/usr/local/arm/arm-2009q3/bin/arm-none-linux-gnueabi-  
3）make -j2 表示多线程编译，在当前目录下生成u-boot.bin.  
4)ls -l uboot.bin()  
5)du -h uboot.bin(384k)  

### 1.1.uboot源码->uboot.bin
- 1.1.1.uboot目录结构基本了解;   
  - Uboot文件说明：  
.gitignore.：git版本管理工具  
Arm_config.mk:.mk是一个Makefile文件，将来在某个Makefile中回去调用它；  
Changelog：文件修改文件记录；  
Config.mk:    
COPYING:GPL版权  
CREDITS：鸣谢  
Image-split(自添加的脚本)：  
MAINTAINERS: 维护者  
Makefile: 主uboot管理编译的  
Mkconfig：uboot配置脚本  
Mkmovi: inand/SD相关  
README:  
Rules.mk: uboot的makefile使用的规则；  

  - 1.1.2.uboot文件夹目录  
api: 硬件无关的功能函数的API，移植时基本不用管。  
api_examples:  
board: board文件夹下每一个文件都代表一个开发板，这个文件夹下面放的文件就是用来描述一个开发板的。  
开发板越来越多，board目录下文件夹越来越多不方便管控，于是乎uboot新增了一种机制，可以在board目录下不直接放开发板目录，而是在board下放厂家目录（具体厂家的名字为目录）   
common: 普通的与具体硬件无关的普遍适用的一些代码。      
cpu: 这个目录是SOC相关的，里面存放的代码都是SOC相关初始化和控制代码，同一块SOC  
disk: 磁盘相关的  
doc: 文档目录存放很多uboot相关目录；  
drivers: linux源码中的驱动代码，flash、network.  
examples: 示例代码  
fs: filesystem文件系统，从linux源代码中移植过来的管理flash等资源。    
include: 所有的头文件都集中存放在include目录下。  
lib_开头的文件：具体cpu架构相关的库文件；lib_arm  
libfdt: 设备树有关的。kernel-3.4  
nand_spl:  
net: 网络相关的代码tftp;  
onenand:   
post:  
sd_fusing: 烧录uboot镜像到SD卡。
tools: 工具类的代码；



小结: 第一步：完成上述前期基本工作，在linux环境编译得到我们需要的可烧写文件uboot.bin; 

二、移植过程分析：
  2.1.
