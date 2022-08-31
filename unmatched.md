# SiFive Unmatched 的资料整理

### Unmatched板子官方资料<br>
https://www.sifive.com/boards/hifive-unmatched

### Unmatched板子官方源代码仓库<br>
https://github.com/sifive/freedom-u-sdk

* 编译：
https://github.com/sifive/freedom-u-sdk#building-disk-images

* 系统镜像烧写至SD卡命令：
```
xzcat demo-coreip-cli-freedom-u540.wic.xz | sudo dd of=/dev/sdX bs=512K iflag=fullblock oflag=direct conv=fsync status=progress
```
_注: 必须下载.rootfs.wic.xz结尾的镜像, 才能通过`dd`到SDCard启动_
<br>_登入用户#密码: root # sifive_

### Unmatched板子运行ubuntu教程
* Ubuntu 21.04
https://discourse.ubuntu.com/t/risc-v-on-ubuntu/22450
* Ubuntu 22.04
https://discourse.ubuntu.com/t/ubuntu-installation-on-the-sifive-hifive-unmatched-board-using-a-server-install-image/27804
_注: ubuntu # ubuntu 首次需要重设密码_

* 启动系统后烧写到nvme教程 
https://discourse.ubuntu.com/t/installing-ubuntu-21-04-on-the-hifive-unmatched/22456
```
dd if=/ubuntu-21.04-preinstalled-server-riscv64+unmatched.img of=/dev/nvme0n1 bs=1M status=progress

# 挂载nvme上的rootfs
mount /dev/nvme0n1p1 /mnt
chroot /mnt

# 编辑 /etc/default/u-boot
U_BOOT_ROOT="root=/dev/nvme0n1p1"

u-boot-update
```

### TTH童鞋移植uCore到unmatched：
* 从sdcard启动：
https://github.com/TianhuaTao/uCore-SMP/blob/fu740/doc/boot.md


### TKF童鞋对移植zCore到unmatched u740的文档：
* Port zCore
https://github.com/tkf2019/zCore2HiFive

* S7核启动与多核通信:
https://github.com/tkf2019/tCore/blob/report/doc/S7%E6%A0%B8%E5%90%AF%E5%8A%A8%E4%B8%8E%E5%A4%9A%E6%A0%B8%E9%80%9A%E4%BF%A1.pdf


### LSM和YZC童鞋的zCore多核适配U740文档
https://github.com/OSLab-zCore/OSLab-Docs/blob/main/zCore%E5%A4%9A%E6%A0%B8%E9%80%82%E9%85%8DU740%E6%96%87%E6%A1%A3.md

### BHY童鞋的Maturin启动于u740
https://github.com/scPointer/maturin/blob/master/doc/fu740%E5%90%AF%E5%8A%A8/%E9%80%9A%E7%94%A8%E7%8E%AF%E5%A2%83%E5%90%AF%E5%8A%A8%E6%96%87%E6%A1%A3.md

### 国外用户自制的为unmatched构建自定义Linux内核
https://github.com/carlosedp/riscv-bringup/tree/master/unmatched

### CX unmatched u740调试
* 调试
https://github.com/GCYYfun/DraftDoc/blob/master/umatched_debug.md
https://www.reddit.com/r/RISCV/comments/no4a3e/hifive_unmatched_openocd_gdb_beginning_bare_metal/
* 移植
https://github.com/GCYYfun/DraftDoc/blob/master/zCore/zcore.md

### nxos操作系统运行于unmatched u740文档
https://gitee.com/BookOS/nxos-documentation/blob/master/programing-manual/platform/hifive_unmached.md

* 设置
```
u-boot> setenv nxos 'dhcp; setenv serverip 10.0.1.5; tftp 0x84000000 nxos.elf; bootelf'
# 这样启动的kernel无法通过a0获取hartid

#替换 bootcmd
u-boot> setenv bootcmd 'run nxos'
```

### 支持u740的bootloader和rust库
* rustsbi
https://github.com/rustsbi/rustsbi-hifive-unmatched
* fu740-pac
https://github.com/riscv-rust/fu740-pac


