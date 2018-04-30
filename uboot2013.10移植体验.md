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
4)ls -l uboot.bin  
5)du -h uboot.bin  

  - 1.1.uboot源码->uboot.bin
    - 1.1.1.uboot目录结构基本了解； 
    - 1.1.1.1.基于文件目录结构和作用的了解，windows中分析时删减相关无影响文件；找到和我们开发板最适配的文件；在sourceinsight中便于查找；
    - 注意： 1.3.4version:
      - lib_arm(cpu架构相关的目录文件)；
        - lib_generic(通用库目录文件)；
            2013.10version:
              arch(cpu架构目录文件)；
              board(支持开发板目录文件)；
              include(包含的头文件相关目录）；
    1.1.2.uboot（makefile,board.cfg,mkconfig）：
     1.1.2.1注意几点：
            1.board.cfg文件中传递给mkconfig的参数作用;
            2.mkconfig文件基本过程，相关符号文件，config.h创建；
            3.烧录文件的添加sd_fusing，makefile中交叉编译工具链的创建；
小结: 第一步：完成上述前期基本工作，在linux环境编译得到我们需要的可烧写文件uboot.bin;

二、移植过程分析：
  2.1.
