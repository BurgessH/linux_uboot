# 朱老师嵌入式课程系列学习-------uboot-version-2013.10移植体验
## 一、具体移植前注意环节：
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
