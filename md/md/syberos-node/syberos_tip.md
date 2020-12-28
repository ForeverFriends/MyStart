# just do it

## 卸载sop应用程序

```
su install
ins-tool -rm com.syberos.eim
```

## 链接虚拟设备

```
ssh -p 5555 developer@localhost  
"system"
```

## 连接元心设备

```
ssh developer@192.168.100.100
"system"

developer@192.168.100.100:/data/developer
```

## 操作RPM

### 安装

```
rpm -ivh --force xxx.rpm
```

 ### 卸载

## 查看DBus

## zypper指令

### 查找文件

 ``` 
zypper se xxx
 ```

### 安装

``` 
zypper --no-gpg-check install xxx
```

### 查看软件源

`zypper lr --uri`

### 刷新

`zypper ref`

### 切换源（4-1）

```
zypper ar http://repo2.insyber.com/syberos:/os4.1.1:/applications/standard_armv7tnhl/  applications_2   

zypper ar  http://repo2.insyber.com/syberos:/os4.1.1:/base/standard_armv7tnhl/         base_2

zypper ar  http://repo2.insyber.com/syberos:/os4.1.1:/hw/standard_armv7tnhl/        hw_2   

zypper ar  http://repo2.insyber.com/syberos:/os4.1.1:/mw/standard_armv7tnhl/         mw_2

zypper ar  http://repo2.insyber.com/syberos:/os4.1.1:/nonbase/standard_armv7tnhl/    nonbase_2

zypper ar  http://repo2.insyber.com/syberos:/os4.1.1:/qt/standard_armv7tnhl/           qt_2

zypper ar  http://repo2.insyber.com/syberos:/os4.1.1:/soservice/standard_armv7tnhl/    soservice_2

zypper ar  http://repo2.insyber.com/syberos:/os4.1.1:/tools/standard_armv7tnhl/  tools_2


zypper mr -d  applications base hw mw nonbase qt soservice tools
```



### 切换源（2-1）

```
zypper ar http://repo2.insyber.com/syberos:/os2.1lts:/applications/standard_armv7tnhl/  applications_2   

zypper ar  http://repo2.insyber.com/syberos:/os2.1lts:/base/standard_armv7tnhl/         base_2

zypper ar  http://repo2.insyber.com/syberos:/os2.1lts:/hw/standard_armv7tnhl/        hw_2   

zypper ar  http://repo2.insyber.com/syberos:/os2.1lts:/mw/standard_armv7tnhl/         mw_2

zypper ar  http://repo2.insyber.com/syberos:/os2.1lts:/nonbase/standard_armv7tnhl/    nonbase_2

zypper ar  http://repo2.insyber.com/syberos:/os2.1lts:/qt/standard_armv7tnhl/           qt_2

zypper ar  http://repo2.insyber.com/syberos:/os2.1lts:/soservice/standard_armv7tnhl/    soservice_2

zypper ar  http://repo2.insyber.com/syberos:/os2.1lts:/tools/standard_armv7tnhl/  tools_2


zypper mr -d  applications base hw mw nonbase qt soservice tools
```



### 切换源（2-1-multimode)

```
zypper ar http://repo2.insyber.com/syberos:/os2.1_lts_multimode:/applications/standard_armv7tnhl/  applications_2   

zypper ar  http://repo2.insyber.com/syberos:/os2.1_lts_multimode:/base/standard_armv7tnhl/         base_2

zypper ar http://repo2.insyber.com/syberos:/os2.1_lts_multimode:/hw/standard_armv7tnhl/        hw_2   

zypper ar  http://repo2.insyber.com/syberos:/os2.1_lts_multimode:/mw/standard_armv7tnhl/         mw_2

zypper ar  http://repo2.insyber.com/syberos:/os2.1_lts_multimode:/nonbase/standard_armv7tnhl/    nonbase_2

zypper ar  http://repo2.insyber.com/syberos:/os2.1_lts_multimode:/qt/standard_armv7tnhl/           qt_2

zypper ar  http://repo2.insyber.com/syberos:/os2.1_lts_multimode:/soservice/standard_armv7tnhl/    soservice_2

zypper ar  http://repo2.insyber.com/syberos:/os2.1_lts_multimode:/tools/standard_armv7tnhl/  tools_2


zypper mr -d  applications base hw mw nonbase qt soservice tools
```





## 元心应用开机自启动

​	在event中增加BOOT_COMPLETE

​	/usr/binboard_init.sh

## strace

``` 
strace /usr/sbin/telnetd >/data/developer/trace.txt
strace /usr/sbin/telnetd 2&>1 >/data/developer/trace.txt
```

## git常用指令

### 提交

```# git push origin local_dev:refs/for/remoute_dev
git push origin os4.1.1_207_pad:refs/for/os4.1.1_207_pad
```

## 查看按键等系统事件

 `toolbox getevent`

## 查找

find -type f -name '*.cpp'|xargs grep -niw 'GroupRecord'

## 安装微信

 [安装说明]()



## 关闭元心设备防火墙

- 链接元心设备

- 修改fw_policy.rule

  `vi /data/etc/fw_policy.rule`

  ```2.default policy
  # 2.default policy
  #/sbin/iptables -P INPUT DROP
  #/sbin/iptables -P FORWARD DROP
  #/sbin/iptables -P OUTPUT DROP
  
  
  
  ```

## DDbus调试

- 查看bus上挂载的service

  ```
  dbus-send --session --print-reply --dest=org.freedesktop.DBus /org/freedesktop/DBus org.freedesktop.DBus.ListNames
  ```

- 查看接口

  ```
  dbus-send --session --print-reply --dest=com.mycompany.SOS / org.freedesktop.DBus.Introspectable.Introspect
  ```

- 关闭pingpong

  ```
  dbus-send --session --print-reply=literal --dest=com.syberos.processmanager.session /com/syberos/processmanager/session com.syberos.processmanager.session.Interface.enablePingPong boolean:false
  ```

- 自组网服务查询方法

  ```
  dbus-send --session --print-reply --dest=com.hg.zzwservice /com/hg/zzwservice com.hg.zzwservice.Interface.queryNetworkStatus
  
  # 飞行模式
  dbus-send --session --print-reply --dest=com.hg.zzwservice /com/hg/zzwservice com.hg.zzwservice.Interface.getFlyModeSwitchStatus
  
  dbus-send --session --print-reply --dest=com.hg.zzwservice /com/hg/zzwservice com.hg.zzwservice.Interface.queryAdhocModuleStatus
  
  #自检
    dbus-send --session --print-reply --dest=com.hg.zzwservice /com/hg/zzwservice com.hg.zzwservice.Interface.getAdhocSelfCheckStatus
  
  ```
  
- dbus 发送信号
  
```
  dbus-send --session --type=signal --print-reply --dest=com.syberos.zzwdbusserver "/com/syberos/zzwdbusserver" com.syberos.zzwdbusserver.Interface.textPropertyChanged
```

  

- dbus 调用函数
  
``` 
  dbus-send --session --type=method_call --print-reply --dest=com.syberos.zzwdbusserver "/com/syberos/zzwdbusserver" com.syberos.zzwdbusserver.Interface.textPropertyChanged
  
  #  锁屏状态
  dbus-send --system --type=method_call --print-reply --dest=com.syberos.user.authentication "/com/syberos/user/authentication" com.syberos.user.authentication.interface.getScreenState
```

  

- dbus 查看信号和方法注册详情
  
```
  dbus-send --session --print-reply --dest=com.syberos.zzwdbusserver /com/syberos/zzwdbusserver org.freedesktop.DBus.Introspectable.Introspect
```

  

- 查看名称
  
```
  dbus-send --session --print-reply --dest=org.freedesktop.DBus /org/freedesktop/DBus org.freedesktop.DBus.ListActivatableNames
```

  

- 查看所有dbus的信息
  
  ```
  dbus-send --session --print-reply --dest=org.freedesktop.DBus /org/freedesktop/DBus org.freedesktop.DBus.ListNames
  ```
  
- 查看电池状态

  ```
    dbus-send --system --type=method_call --print-reply --dest=org.freedesktop.UPower "/org/freedesktop/UPower" org.freedesktop.UPower.Properties
     dbus-send --system --type=method_call --print-reply --dest=org.freedesktop.UPower "/org/freedesktop/UPower" org.freedesktop.UPower.EnumerateDevices
    dbus-send --system --type=method_call --print-reply --dest=org.freedesktop.UPower "/org/freedesktop/UPower/devices/line_power_ac" org.freedesktop.UPower.Device.GetStatistics
    
     dbus-send --system --type=method_call --print-reply --dest=org.freedesktop.UPower        /org/freedesktop/UPower/devices/battery_rk_bat  org.freedesktop.DBus.Properties.GetAll
     
      dbus-send --system --type=method_call --print-reply --dest=org.freedesktop.UPower "/org/freedesktop/UPower" org.freedesktop.UPower.Devices
     
     
     
     
      dbus-send --system --type=method_call --print-reply --dest=org.freedesktop.UPower        /org/freedesktop/UPower/devices/battery_rk_bat   org.freedesktop.UPower.Device.property string:Capacity
      
      org.freedesktop.UPower.Device
     
     
   # dbus-monitor --session \ "type='signal',interface='org.freedesktop.UPower.Device',member='DeviceChanged'"
    
      dbus-monitor --system interface=org.freedesktop.Upower
      dbus-monitor --system interface=org.freedesktop.Upower.Device 
      dbus-monitor --system interface=org.freedesktop.DBus.Properties 
  
  ```

- 查看服务提供的接口

  ```
  dbus-send --system --type=method_call --print-reply --dest=com.syberos.myservice / org.freedesktop.DBus.Introspectable.Introspect
  
  dbus-send --system --type=method_call --print-reply --dest=org.freedesktop.UPower / org.freedesktop.DBus.Introspectable.Introspect
  
  dbus-send --system --type=method_call --print-reply --dest=org.freedesktop.UPower "/org/freedesktop/UPower" org.freedesktop.DBus.Introspectable.Introspect
  
  dbus-send --system --type=method_call --print-reply --dest=org.freedesktop.UPower "/org/freedesktop/UPower/devices/line_power_ac" org.freedesktop.DBus.Introspectable.Introspect
  
  ```

  



  


## 命令行启动app

sdk-invoker [time] sopid:appid:类型

  ```
sdk-invoker 0 com.mycompany.SOS:SOS:uiapp
  ```

## 查看进程状态

- 如果想查看包含其他使用者的进程，和PID，CPU占有率，记忆体使用情况，运行状态等，可以输入ps -aux

  > USER：进程拥有者,示例中是root。
  >
  > PID：进程ID，用户ID为UID，父进程ID为PPID
  >
  > %CPU：占用的CPU使用率，ID号为1的进程为0
  >
  > %MEM：占用的物理内存百分比，ID号为1的进程为0
  >
  > VSZ：占用的虚拟内存量，ID号为1的进程为194184
  >
  > RSS：占用的固定的内存量，ID号为1的进程为6536
  >
  > TTY：终端的次要装置号码（minor device number of tty），示例中的TTY列都是“？”，是表示这些进程不属于任何TTY，因为它们是由系统启动的，tty1-tty6 是本机上面的登入者程序，若为 pts/0 等等的，则表示为由网络连接进主机的程序。
  >
  > STAT：该进程的状态，有下一个板块的几个状态，D，R，S，T，Z是ps指令标识进程的5种状态码
  >
  > TIME：进程已消耗的CPU时间
  >
  > CMD：启动进程的命令

- 当前所有的进程. 包括显示创建进程的用户标识uid, 进程标识pid, 父进程标识ppid, 创建时间,所执行程序，可以用ps -ef

- ps -lax可以提供进程ID，父进程PPID，谦让度和等待的资源

  > NI：谦让度
  >
  > WCHAN：正在等待的进程资源
  >
  >  
  >
  > Linux上进程的五种状态：
  >
  > 1.R——Runnable（运行）：正在运行或在运行队列中等待
  >
  > 2.S——sleeping（中断）：休眠中，受阻，在等待某个条件的形成或接收到信号
  >
  > 3.D——uninterruptible sleep(不可中断)：收到信号不唤醒和不可运行，进程必须等待直到有中断发生
  >
  > 4.Z——zombie（僵死）：进程已终止，但进程描述还在，直到父进程调用wait4()系统调用后释放
  >
  > 5.T——traced or stoppd(停止)：进程收到SiGSTOP,SIGSTP,SIGTOU信号后停止运行
  >
  >  
  >
  > 状态后缀表示：
  >
  > <：优先级高的进程
  >
  > N：优先级低的进程
  >
  > L：有些页被锁进内存
  >
  > s：进程的领导者（在它之下有子进程）
  >
  > l：ismulti-threaded (using CLONE_THREAD, like NPTL pthreads do)
  >
  > +：位于后台的进程组



## 查看元心os的qt版本号

进入PDK环境 执行**qmake -v**

```
pdk
sb2-config -l
sb2 -t target-armv7tnhl-os4_1_1 -R
qmake -v
```



## 元心app异常退出原因查询

```
 typedef enum {
        UNKNOW = 0,
        TASKMANAGERQUIT =1,
        LOWMEMORYQUIT,
        SWITCHSYSTEMQUIT,
        PINGPONGQUIT,
        DEBUGNEWSTART,
        DEBUGQUIT,
        QUITSAMEUIDAPP,
        UPDATEAPP
    } QuitReason;
    
    # cprocessmanager.h
```

## 再也不用担心找不到XXX

http://192.168.160.111:8080/source/

## 开启wayland日志

```
vi /etc/environment/10-syberos.conf
WAYLAND_DEBUG="1"
```

## rpm编译未生成debugInfo

.spec 文件中定义 %define debugs {nil}

## 引用第三方库

- ldd MyApp      xxx=> not found
- 将需要依赖的库安装到libs目录下

```
#APP_DIR = /data/apps
#INSTALL_DIR = $$APP_DIR/com.mycompany.myApp

ffmpeg.files = ffmpeg/lib/*
ffmpeg.path = $$INSTALL_DIR/libs/
INSTALLS += ffmpeg

#安装到$$INSTALL_DIR/libs/目录后，系统会自动拷贝一份至/data/app-libs/com.mycompany.myApp
```



- 在pro 文件中配置QMAKE_LFAGS

```
QMAKE_LFLAGS += -Wl,-rpath=/data/app-libs/com.mycompany.myApp -Wl,-Bsymbolic
QMAKE_LFLAGS += -Wl,-rpath-link=/data/app-libs/com.mycompany.myApp -Wl,-Bsymbolic
```

## 手动编译sop包及安装

- 编译

```
  pdk 
  sb2 -t xxx -R
  qmake xxx.pro
  make
  buildpkg xxx.pro
```

- 安装

```
  scp xxx.sop developer@192.168.100.100:/data/developer
  # 切换到install用户
  su install 
  sop -iu xxx.sop
```

- 卸载
```
  su install
  ins-tool -rm com.syberos.eim
```

  

## 查看电池电量信息

  ```
# /sys/class/power_supply/
battery - 电池
/sys/class/power_supply/battery/capacity
/sys/class/power_supply/battery/status
usc -　USB
ac - DC口设备


udevadm monitor #　查看event信息
  ```

## 默认壁纸存储位置

- home-screen 中初始化　WallpaperSettings　

- `_q_updateWallpaper`　获取当前壁纸信息

- 在 qt-base 工程中使用dbus获取confd中/data/systemdata/confd/syberos-confd.db　的数据

```
   QDBusMessage message = QDBusMessage::createMethodCall(
                  STORAGE_SERVICE,  "com.syberos.confd"
                  STORAGE_PATH,   "/confd"
                  STORAGE_INTERFACE, "com.syberos.confd"
                  STORAGE_METHOD_GETVALUE);  "getValue"
      message << section << group << key << STORAGE_TYPE_SOURCE_SYS;     
      "com.syberos.home"     "SYSTEM_HOME_WALLPAPER_URL"   "10"  "system"  
       QDBusReply<QVariantMap>reply = QDBusConnection::systemBus().call(message);
       
```

- sqlite3

  ```
  sqlite3 /data/systemdata/confd/syberos-confd.db 
  #看看有创建了多少表
  .tables
  #看表结构
  .schema 表名
  #看看目前的数据库
  .database
  #如果要把查询输出到文件
  .output 文件名

  ```



## 修改系统时间

  ```
date -s 26/8/2020 
date -s 14:41
  ```



## 设置系统分辨率

- framework -> system-main -> compositor.qml
- /etc/environment/10-syberos.conf   QT_QPA_EGLFS_PHYSICAL_WIDTH=62  QT_QPA_EGLFS_PHYSICAL_HEIGHT=110



## 打印内核日志

```
dmesg
cat /dev/kmsg
```

## 存储信息

```
cat /proc/meminfo
```

## CPU信息

```
#信息
cat /usr/share/about-contents/about-content.conf
#最大频率
cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_max_freq
＃当前频率
cat /sys/device/system/cpu/cpu0/cpufreq/stats/time_in_state
```

## rootfs下空间不足导致rpm安装失败

`resize2fs -f /dev/byname/syberfs`

## 语音播报

```
#system 
paplay /usr/tts/zzwcheckin.wav
```





## 5.0下编译

```
source build/envsetup.sh
lunch
make syberos-settings


//////////////////
mm -j4
....

sop: /workarea/lihao/SyberOS_5.0_S_P_sp9863a-509_devel/out/target/alpha_s9863a1h10_sharkl3/system/usr/apps
```

## 播放MP4缺少gstreamer插件

sudo apt install gstreamer1.0-libav/bionic-updates

sudo apt install gstreamer1.0-plugins-bad/bionic-updates

## 关闭电脑关盖睡眠功能

sudo vim /etc/systemd/logind.conf

设置 HandleLidSwitch=ignore



## 5.0代码同步

```
#安装 repo
sudo apt install repo
# 安装配置环境
sudo apt-get install -y python3 make gcc gyp cmake bison pkg-config autoconf autoconf-archive python-lxml
sudo apt-get install -y gperf gawk texinfo autopoint intltool libwayland-bin libglib2.0-dev-bin libtool git-lfs ninja-build
sudo apt-get install -y libdbus-glib-1-dev libexpat1-dev gtk-doc-tools android-tools-mkbootimg android-tools-fsutils
sudo apt-get install -y libc6:i386 flex libnspr4-dev libnss3-dev gcc-multilib liborc-dev tcl texlive zip
sudo apt-get install -y qt5-default valac libssl-dev
```

代码下载
(1)在repo文件中，开头定义REPO_URL，其中$USERNAME需要替换为自己的gerrit账户名

REPO_URL='ssh://$USERNAME@gerrit.insyber.com:29418/git-repo' 
REPO_REV = 'stable'

(2)初始化相应分支代码下载
/usr/bin/repo init -u ssh://$USERNAME@gerrit.insyber.com:29418/manifests -b 分支名
例如：
/usr/bin/repo init -u ssh://yongpeng_zhang_dev@gerrit.insyber.com:29418/manifests -b os5.0_rk3399-zt_devel

(3)同步代码下载
repo sync -c



## fastboot模式

重启进入fastboot,可以通过以下命令：

`setprop sys.powerctl reboot,bootloader`

`fastboot devices #列出设备`

`fastboot flash recovery recovery.img #刷新recovery `

`fastboot flash boot  boot.img    # 刷入 boot 分区`









## 制作boot.img

修改相关代码（init.rc）之后，重新生成root.cpio.gz

~~~
cd ./out/target/<lunch_name>/root
find ./ | cpio -o -H newc -R root:root | gzip -n -9 -f > ../root.cpio.gz
~~~

重新生成boot_yx.img

~~~
./out/target/alpha_rk3399_laptop/host/usr/bin/mkbootimg --kernel ./out/target/alpha_rk3399_laptop/obj/kernel/arch/arm64/boot/Image \
                    --ramdisk ./out/target/alpha_rk3399_laptop/root.cpio.gz \
                      --second ./out/target/alpha_rk3399_laptop/obj/kernel/resource.img \
                      --os_version 9 \
                      --header_version 1 \
                      --os_patch_level 2019-12-05 \
                      --cmdline 'console=ttyFIQ0 androidboot.baseband=N/A androidboot.wificountrycode=US androidboot.veritymode=enforcing androidboot.hardware=rk30board androidboot.console=ttyFIQ0 firmware_class.path=/vendor/etc/firmware init=/init rootwait ro init=/init root=PARTUUID=af01642c-9b84-11e8-9b2a-234eb5e198a0 loop.max_part=7 androidboot.selinux=permissive' \
		      --output boot_yx.img
~~~

可参考`device/rockchip/rk3399/rk3399_laptop.mk` (不同芯片路径不同)文件

使用 **dd** 烧录boot.img

```
dd if=boot.img of=/dev/byname/boot
```



## os5.1修改分区为读写操作

如果需要调试，可以使用下面命令重挂载为可读写
/system/bin/mount -o remount,rw /raw_system
也可只挂载下面需要修改的节点
/system/bin/mount -o remount,rw /lib
/system/bin/mount -o remount,rw /lib64
/system/bin/mount -o remount,rw /etc
/system/bin/mount -o remount,rw /usr
/system/bin/mount -o remount,rw /tls



**通过mount命令重挂载成读写并修改system分区的文件后，
重启前执行一下下面命令，避免在重启后再次挂载会失败的问题。
e2fsck -pf /dev/block/platform/soc/by-name/system **



# so easy

##  查看未定义符号

```
c++filt xxx
```



## double free

/usr/bin/SOSService: double free or corruption (out): 0x0003df60

## 窗口反复show in show out

- 现象

  窗口反复闪烁

```
  log:
  Recieve deactive message from PM
  Recieve active message from PM
  Recieve deactive message from PM
  Recieve active message from PM
  QWindow::show in
  QWindow::show out
  // 反复出现 active deactive
```

- 多次触发RedayRead()且**ApplicationStatus** 为 PAUSE 

## qml中槽函数链接不上c++中的信号

在c++中产生信号的实例非注册在qml中的实例，建议将该类实现为单类模式。

## 找不到系统库

- ` err adding symbols: DSO missing from command line`

- 原因

  在binutils<2.22时，ld正常完成了，bin_c对于foo的调用经由libB，传递到了libA，链接成功。
   但是当binutils>=2.22时，编译出错了，ld会报上面的错，告诉你foo这个symbol解析不到，这时，我们需要编译bin_c时，显示地链接libA才可以通过。
  binutils2.22开始，其中的ld开始把--no-copy-dt-needed-entries默认打开，这样一来，ld不会再自动递归地解析链接的lib，而需要由用户来一一指定

  `ld -v`

- 在.pro 中增加　LIBS　+= -lxxx

> ​	md5sum
>
>    readelf -a xxxx

# so so easy

## 使用rpm编译busybox

​		busybox 编译时将根据.config文件中的配置设置相关的命令，可以使用**make config** 逐个确认是否配置为可用，也可以使用**make allyesconfig**设置为全部可用， **make allnoconfig** 设置为全部不可用，可以通过 **make help** 查看。

​		使用rpm编译时是基于以上命令实现的，在.spec文件中配置.config的备份文件，在编译前将**busybox-static.config** 和 **busybox-sailfish.config** 覆盖.config文件。

- 将**rpm/busybox-static.config** 和 **rpm/udhcpd.service** 文件拷贝到 SORCE目录下

- 修改**busybox-sailfish.config** 文件中对应的模块，如：将# CONFIG_TELNET is not set改为CONFIG_TELNET=y（开启状态）;

- 在busybox.spec文件中增加 对应的**%package，%files**  路径应与 自动生成的 **busybox.links**  文件中对应的路径保持一致；

  ```
  #busybox.links
  /bin/gunzip
  /bin/gzip
  /usr/bin/telnet
  /usr/bin/tftp
  /usr/sbin/tftpd
  /sbin/udhcpc
  /usr/sbin/udhcpd
  /bin/zcat
  /usr/sbin/udhcpc
  ```

- 改为多次修改模块配置在编译前使用 **make distclean** 清理，否则有可能无效；

- 将对应的rpm包拷贝到目标设备中按转即可使用，不要遗漏**busybox-1.21.0.skytree33-1.armv7tnhl.rpm**；

- 使用**busybox xxx** （busybox telnet）测试是否生效；

- 注意：telnet作为服务端应开启telnetd，在设备安装完成后，须执行telnetd命令开启服务端



# others

## vmware扩容

- 在VMware中点击硬盘->扩容

- 进入系统，安装gparted，`sudo apt-get install gparted` 类似于windows下的DiskGenius

- 删除新增分区，对/dev/sda1扩容，完成后点击对号

- 使用fdisk /dev/sda1 查看

  - lsblk

  -  df -PTh

      

gerrite  UX6[/1CJ^

v2c-pu7gb-uf

## 解析syberos相关域名

  ```
199.232.68.133 raw.githubusercontent.com
192.168.160.124 gerrit.insyber.com
192.168.160.123 jenkins.insyber.com
192.168.160.133 image2.insyber.com
192.168.160.239 repo2.insyber.com
192.168.160.120 obs.insyber.com
192.168.11.30 sdk.insyber.com


# /etc/resolv.config
nameserver 192.168.160.9
  ```

### 关闭盖子不处理

sudo vi /etc/systemd/logind.conf

主要是修改其HandleLidSwitch项，把它改成ignore值即可

方法是把#HandleLidSwitch=suspend项改成HandleLidSwitch=ignore

修改完成后重新启动服务systemd-logind：sudo service systemd-logind restart

