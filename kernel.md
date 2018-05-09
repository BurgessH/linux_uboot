# 内核的配置和编译过程  
## linux内核源码目录结构1-2  
### 文件目录：  
  - 源码获取的渠道2.6.35.7版本的内核（三星移植过和九鼎移植过的内核）一共三个版本：kernel.org版本；三星移植过的版本（移植实验使用）；九鼎移植过的版本（我们使用的是：B/linux/QT4.8/bsp/qt_x210v3_130807）;  
  - **.gitignore**:版本控制  
  - **.mailmap**：维护  
  - **COPYING**: 版权  
  - **CREDITS**: 鸣谢  
  - **initrd.img.cpio**:设备树传参  
  - **Kbuild**: kernel编译（管理内核配置）  
  - **MAINTAINERS**:   
  - **makefile**: 管理kernel编译的  
  - **mk**(九鼎移植时自己添加的整体管理kernel配置和编译）  
  - **README**：说明  
  - **Kconfig**: 
  
### 文件夹目录：  
  - **arch**:(好多个不同架构的cpu的子目录，譬如arch/arm)  
  - **block**:在linux中block表示块设备管理的代码；  
  - **crypto**: 常用加密算法      
  - **Documentation**: 文档    
  - **driver**: 驱动目录（分门别类的列出了linux所支持的所有驱动）  
  - **firmware**: 固件    
  - fs: 文件系统支持所有的文件系统    
  - include: 头文件目录各种cpu架构共用的头文件都在这里；    
  - init:内核本身的初始化；     
  - ipc: 进程间通信    
  - kernel:linux内核本身需要的文件；      
  - lib：共用的有用库函数；    
  - mm: 内存管理相关的；    
  - net : 网络相关的代码tip/ip;    
  - script: 脚本辅助linux内核配置编译生产的；  
  - security:安全  
  - sound: 音频  
  - tools:工具  
  - usr:  initramfs相关的
  - virt:  虚拟机
   
## linux内核配置和编译体验   
### 配置和编译操作过程  
  - 1.**Makefile**: 确认交叉编译工具链是否安装、确认arch=arm(确认找到arch/arm目录);    
  - 2.make x210ii_qt_defconfig(configuration written to .config-->生产.config文件);        
  - 3.make menuconfig  
  - 4.make  
## 内核的配置原理1-2  
