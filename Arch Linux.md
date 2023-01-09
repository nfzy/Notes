## Arch安装教程

1. **检查是什么类型的引导**

   ```bash
   ls /sys/firmware/efi/efivars 	#有表示可以uefi启动，没有则是boot启动
   ```

2. **连接网络**

   ```bash
   dhcpcd #有线连接
   wifi-menu #无限网络
   ping baidu.com #检查网络连接是否成功
   ```

3. **更新系统时间**

   ```bash
   timedatectl status #查看系统时间有没有误
   
   timedatectl set-ntp  true #设置正确时间
   ```

4. **分区**

   1. **检查分区情况**

      ```bash
      lsblk 
      NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
      sda           8:0    0 931.5G  0 disk 
      ├─sda1        8:1    0    20G  0 part [SWAP]
      └─sda2        8:2    0 911.5G  0 part /
      sdb           8:16   1  14.3G  0 disk 
      ├─sdb1        8:17   1   649M  0 part 
      └─sdb2        8:18   1    64M  0 part 
      nvme0n1     259:0    0   477G  0 disk 
      └─nvme0n1p1 259:1    0   500M  0 part /boot/EFI
      ```

   2. **开始分区**

      ```bash
      cfdisk /dev/sd? #你想要分区的硬盘
      fdisk /dev/sd? #另一种分区方式
      ```

   3. **格式化分区**

      ```bash
      #SWAP分区，/根分区，引导uefi分区
      
      mkfs.vfat /devsd?1 #引导分区
      mkfs.ext4 /dev/sd?2 #根分区
      mkswap /dev/sd?3 
      swapon /dev/sd?3 #打开SWAP，如果内存足够大，超过8g可以不要swap分区
      ```

5. **挂载**

   ```bash
   mount /dev/sd?2 /mnt #挂载根分区
   mkdir -p /mnt/boot/EFI  #创建EFI文件夹
   mount /dev/sd?1  #挂载引导
   ```

6. **安装**

   1. **选择镜像源**

      ```bash
      vim /etc/pacman.d/mirrorlist
      
      
      1. 按下'/'然后在后面搜索China,选择清华大学镜像或者别的
      2. 移到源那行，按下d后在按一下d，移动到最上方yy(同dd)
      3. 最好多选择几个，以防镜像不能使用
      ```

   2. **安装基本系统**

      ```bash
      pacstrap /mnt base base-devel linux linux-firmware vim dhcpcd
      ```

   3. **配置系统**

      ```bash
      genfstab -U /mnt >> /mnt/etc/fstab
      ```

   4. **root系统**

      ```bash
      arch-chroot /mnt
      ```

   5. **设置时区**

      ```bash
      ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
      hwclock --systohc
      ```

   6. **本地化**

      ```bash
      vim /etc/locale.gen #将下面2个前面的#删除
      en_US.UTF-8 UTF-8
      zh_CN.UTF-8 UTF-8
      
      locale-gen
      
      echo LANG=en_US.UTF-8 > /etc/locale.conf
      ```

   7. **网络**

      ```bash
      echo 主机名 > /etc/hostname
      
      vim /etc/hosts
      127.0.0.1	localhost
      ::1		localhost
      127.0.1.1	myhostname.localdomain	myhostname
      ```

   8. **设置root密码**

      ```bash
      passwd
      #然后会让你输入密码，并且要再次确认
      ```

   9. **安装引导**

      ```bash
      pacman -S grub efibootmgr ntfs-3g os-prober #ntf3-3g是windows文件系统，os-prober，如果只想装一个系统后面两个可以不要
      
      grub-install --target=i386-pc /dev/sdx  #不是UEFI启动
      grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=grub #注意挂载efi的分区是最开始分好的
      
      grub-mkconfig -o /boot/grub/grub.cfg #生成主配置文件
      ```

   10. **安装编码**

       ```bash
       pacman -S intel-ucode #intel
       pacman -S amd-ucode #amd
       ```

   11. **网络连接**

       ```bash
       pacman -S iw wpa_supplicant dialog dhcpcd
       systemctl enable dhcpcd #设置开机自动启动
       ```

   12. **退出系统**

       ```bash
       exit
       umout -R /mnt
       reboot 
       ```

   13. **配置新系统**

       ```bash
       useradd -m -G wheel /bin/bash youname 
       passwd yourname #为你自己设置密码
       ```

   14. **设置权限**

       ```bash
       vim /etc/sudoers
       
       在 root ALL=(ALL) ALL 下面添加
       用户名 ALL=(ALL) ALL
       为你刚才创建的用户 添加sudo权限
       ```

   15. **配置archlinuxcn源**

       ```bash
       vim /etc/pacman.conf
       
       [archlinuxcn]
       Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch #有些东西只有在这个源里才有
       
       pacman -S archlinxcn-kerying #导入gpk秘钥
       ```

   16. **常用软件安装**

       ```bash
       pacman -S git vim  zsh networkmanager net-tools typora visual-studio-code-bin gimp vlc 
       #你自己想装什么找到包名就可以了
       
       pacman -Ss xxx #可以列出有哪些软件包
       ```

   17. **安装桌面环境(很重要)**

       ```bash
       sudo pacman -S xorg  plasma kde-applications #kde桌面,建议安装
       sudo pacman -S sddm #桌面管理器
       systemctl enable sddm #设置开机自启
       ```

   18. **输入法**

       ```bash
       sudo pacman -S fcitx fcitx-im fcitx-googlepinyin fcitx-configtool #sogou拼音很麻烦不建议安装
       
       vim ~/.xprofile #写入下面的内容到新创建的文件中
       
       export XMODIFIERS="@im=fcitx"
       export GTK_IM_MODULE="fcitx"
       export QT_IM_MODULE="fcitx"
       ```

       