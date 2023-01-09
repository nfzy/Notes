## 常用命令

#### Linux文件类型颜色

* **目录------蓝色**
* **一般性文件，如文件文件，配置文件，源码文件等------白色**
* **链接文件-----淡蓝色**
* **可执行文件，可执行程序------绿色**
* **压缩文件或者包文件------红色**

#### Linux字符文件类型

* **-: 一般文件**
* **d: 目录文件**
* **l: 链接文件**
* **b: 块设备文件**
* **c: 字符设备文件**
* **p: 管道文件**

#### 关机和重启

* **shutdown**
* **reboot**
* **halt**
* **poweroff**

#### grep[^0]

* ```bash
  grep -l "thing" * #显示所有包含thing字段的文件名
  ```

* ```bash
  grep -n "thing" file #在匹配字符行之前加行号
  ```

* ```bash
  grep -i "thing" file #显示匹配字符行，不区分大小写
  ```

* ```bash
  grep -v "thing" file #显示所有不匹配的字符行
  ```

* ```bash
  grep -c "thing" file #只显示匹配到字符行的行数
  ```

#### df[^1]

* ```bash
  df -h 
  文件系统		 总容量 已用  可用   已用% 挂载点	
  Filesystem      Size  Used Avail Use% Mounted on
  dev             7.8G     0  7.8G   0% /dev
  run             7.8G  1.6M  7.8G   1% /run
  /dev/sda6       147G   15G  125G  11% /
  tmpfs           7.8G  220M  7.6G   3% /dev/shm
  tmpfs           7.8G     0  7.8G   0% /sys/fs/cgroup
  tmpfs           7.8G   12M  7.8G   1% /tmp
  /dev/sda7       500M  280K  499M   1% /boot/efi
  tmpfs           1.6G  576K  1.6G   1% /run/user/1000
  ```

* ```bash
  df -i
  文件系统		文件元信息 已用   可用    已用% 挂载点
  Filesystem      Inodes  IUsed   IFree IUse% Mounted on
  dev            2031321    609 2030712    1% /dev
  run            2033778    998 2032780    1% /run
  /dev/sda6      9830400 429770 9400630    5% /
  tmpfs          2033778    147 2033631    1% /dev/shm
  tmpfs          2033778     18 2033760    1% /sys/fs/cgroup
  tmpfs          2033778    316 2033462    1% /tmp
  /dev/sda7            0      0       0     - /boot/efi
  tmpfs          2033778    176 2033602    1% /run/user/1000
  ```

#### du[^2]

* ```bash
  du -sh #显示当前目录总大小，单位为KB
  ```

* ```bash
  du -sh / #显示‘/’下所有文件总大小
  ```

#### ln[^3]

* ```bash
  ln 源文件 目标文件 #硬链接，不能链接目录和跨文件系统文件，实际上和源文件是同一个
  ```

* ```bash
  ln -s 源文件 目标文件 # -s 软链接，支持跨文件系统，只是指向源文件，相当与快捷方式
  ```

#### 用户和用户组

* ```bash
  id -a #显示此用户真实有效的UID和GID
  uid=1000(zhouan) gid=1000(zhouan) groups=1000(zhouan),998(wheel)
  ```

* ```bash
  id -G #输出有效的，真实的和补充的组ID
  id -g #只输出有效组ID
  ```

* **只有在使用-u -g -G时才能使用-n(name) -r(打印真实D)**

[^0]: **匹配文本字符**
[^1]: **列出文件系统的整体磁盘使用情况**
[^2]: **列出目录所占空间**
[^3]: **链接文件(快捷方式)**