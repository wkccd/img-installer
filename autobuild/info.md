[![Github](https://img.shields.io/badge/Release文件可在国内加速站下载-FC7C0D?logo=github&logoColor=fff&labelColor=000&style=for-the-badge)](https://wkdaily.cpolar.top/archives/1) 

#### 格式ISO: 此文件是通过AutoBuildImmortalWrt项目构建的
#### 适用范围：所有虚拟机和物理机通用 皆可引导 用于安装ImmortalWrt
#### 使用方法：
- 虚拟机使用：各种虚拟机直接选择iso 作为开机引导即可
- 物理机使用：建议将iso放入ventoy的U盘中
#### 运行ISO的中的debian live系统 大概10几秒后 输入命令 `ddd` 即可调用安装菜单 选择需要安装的硬盘迅速完成安装
<img width="50%" height="50%" alt="image" src="https://github.com/user-attachments/assets/b47821ed-dc1d-41b5-8a6e-814bf222a2f4" />

#### 安装后 默认情况 若没有更改 则固件信息如下
- 用户名root 密码 无
- 该固件刷入【单网口设备】默认采用DHCP模式,自动获得ip。类似NAS的做法 可在上一级路由器查询，若是虚拟机则输入 `ip a` 查看
- 该固件刷入【多网口设备】默认WAN口采用DHCP模式，LAN 口ip为  `192.168.100.1 `其中eth0为WAN 其余网口均为LAN
#### ip为什么这样设计
- 因为很多人在第一次刷入固件后 都做了很多重复的工作 要编辑`/etc/config/network` 不适合手残党和新手。而且我觉得每次这样修改有点傻 千年不变的糟糕用户体验要变一变 为什么不去web页面里修改呢 有界面操作更简单啊
- 【单网口】设备直接就是自动获得ip 则不需要你每次都在命令行里修改了。尤其在虚拟机里，ip a 就能查看ip 用此ip就能访问。web页面在修改任何东西 都很简单了。尤其旁路用户 进web页再设置
- 【多网口】设备用 192.168.100.1 访问web ui

#### 和传统的NAS虚拟机导入img有什么区别
许多人会有疑问：现如今NAS虚拟机明明支持直接导入img镜像，为什么还要使用此安装器？
事实并非表面那样，各类NAS、虚拟机自带的img导入功能，本质只是将raw格式的img，自动转换为qcow2等虚拟磁盘格式。转换完成后，磁盘容量会严格锁定为原img的固定体积，无法自由扩容。

该模式会严重限制后续固件升级：在后台网页升级界面刷写新版固件时，只要新固件体积大于原版img固件，**即便关闭保留配置选项，依旧会刷写失败、引导跑码卡死**。核心原因就是虚拟磁盘空间被固化限制，大容量的新固件，无法写入固定小容量的磁盘内。

而我们的ISO安装器逻辑完全不同。
安装过程仅占用目标磁盘的部分空间，不会锁死磁盘上限，后续新版固件可直接覆盖写入。安装时还能自主提前设定虚拟磁盘大小，只要磁盘预留空间充足，后期可以随意更换、升级固件。

整体原理和安装传统 Windows、Linux 原版系统保持一致，解决了传统IMG导入固化容量的硬伤。

#### 新手视频教学
- 【第一集 ESXI虚拟机 和 物理机使用】https://www.bilibili.com/video/BV1DQXVYFENr
- 【第二集 飞牛NAS】https://www.bilibili.com/video/BV1gPXCYyEc2
- 【第三集 Hyper-V、绿联NAS虚拟机、飞牛虚拟机使用教程】 https://www.bilibili.com/video/BV1BoZVYsE7b
- 【第四集 PVE虚拟机里如何使用img安装器】https://www.bilibili.com/video/BV1Rx5Qz4EZB
