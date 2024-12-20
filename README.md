# Домашнее задание к занятию «Уязвимости и атаки на информационные системы» - `Пронин Дмитрий Андреевич`

---



### Задание 1

Задание 1
Установите eCryptfs.
Добавьте пользователя cryptouser.
Зашифруйте домашний каталог пользователя с помощью eCryptfs.
В качестве ответа пришлите снимки экрана домашнего каталога пользователя с исходными и зашифрованными данными.


Установка и создание юзера
```
root@k3s-server:~# apt-get install ecryptfs-utils
root@k3s-server:~# useradd -m cryptouser
root@k3s-server:~# passwd cryptouser
New password:
BAD PASSWORD: The password fails the dictionary check - it is based on a dictionary word
Retype new password:
passwd: password updated successfully
root@k3s-server:~# ls -la /home/
total 20
drwxr-xr-x  5 root       root       4096 дек 20 21:04 .
drwxr-xr-x 20 root       root       4096 фев 11  2024 ..
drwxr-x---  2 cryptouser cryptouser 4096 дек 20 21:04 cryptouser
drwxr-x---  5 developer  developer  4096 июл 24 21:33 developer
drwxr-x--- 21 dmitriy    dmitriy    4096 дек 20 20:56 dmitriy

root@k3s-server:~# ls -la /home/
total 20
drwxr-xr-x  5 root       root       4096 дек 20 21:04 .
drwxr-xr-x 20 root       root       4096 фев 11  2024 ..
drwxr-x---  2 cryptouser cryptouser 4096 дек 20 21:04 cryptouser
drwxr-x---  5 developer  developer  4096 июл 24 21:33 developer
drwxr-x--- 21 dmitriy    dmitriy    4096 дек 20 20:56 dmitriy


drwxr-x--- 5 cryptouser cryptouser 4096 дек 20 21:06 .
drwxr-xr-x 5 root       root       4096 дек 20 21:04 ..
-rw-r--r-- 1 cryptouser cryptouser  220 янв  6  2022 .bash_logout
-rw-r--r-- 1 cryptouser cryptouser 3771 янв  6  2022 .bashrc
drwx------ 3 cryptouser cryptouser 4096 дек 20 21:06 .cache
drwx------ 3 cryptouser cryptouser 4096 дек 20 21:06 .config
-rw-r--r-- 1 cryptouser cryptouser  807 янв  6  2022 .profile
drwx------ 3 cryptouser cryptouser 4096 дек 20 21:06 snap
-rw------- 1 cryptouser cryptouser   56 дек 20 21:06 .Xauthority
```

Зашифровываю
```
root@k3s-server:~# ls -la /home/cryptouser/
total 36
drwxr-x--- 5 cryptouser cryptouser 4096 дек 20 21:06 .
drwxr-xr-x 5 root       root       4096 дек 20 21:04 ..
-rw-r--r-- 1 cryptouser cryptouser  220 янв  6  2022 .bash_logout
-rw-r--r-- 1 cryptouser cryptouser 3771 янв  6  2022 .bashrc
drwx------ 3 cryptouser cryptouser 4096 дек 20 21:06 .cache
drwx------ 3 cryptouser cryptouser 4096 дек 20 21:06 .config
-rw-r--r-- 1 cryptouser cryptouser  807 янв  6  2022 .profile
drwx------ 3 cryptouser cryptouser 4096 дек 20 21:06 snap
-rw------- 1 cryptouser cryptouser   56 дек 20 21:06 .Xauthority
root@k3s-server:~# ecryptfs-migrate-home -u cryptouser
INFO:  Checking disk space, this may take a few moments.  Please be patient.
INFO:  Checking for open files in /home/cryptouser
lsof: WARNING: can't stat() fuse.portal file system /run/user/1000/doc
      Output information may be incomplete.
lsof: WARNING: can't stat() fuse.gvfsd-fuse file system /run/user/1000/gvfs
      Output information may be incomplete.
Enter your login passphrase [cryptouser]:
ERROR:  Your login passphrase is incorrect
Enter your login passphrase [cryptouser]:

************************************************************************
YOU SHOULD RECORD YOUR MOUNT PASSPHRASE AND STORE IT IN A SAFE LOCATION.
  ecryptfs-unwrap-passphrase ~/.ecryptfs/wrapped-passphrase
THIS WILL BE REQUIRED IF YOU NEED TO RECOVER YOUR DATA AT A LATER TIME.
************************************************************************


Done configuring.

chown: cannot access '/dev/shm/.ecryptfs-cryptouser': No such file or directory
INFO:  Encrypted home has been set up, encrypting files now...this may take a while.
sending incremental file list
./
.Xauthority
             56 100%    0,00kB/s    0:00:00 (xfr#1, to-chk=83/85)
.bash_logout
            220 100%  214,84kB/s    0:00:00 (xfr#2, to-chk=82/85)
.bashrc
          3.771 100%    3,60MB/s    0:00:00 (xfr#3, to-chk=81/85)
.profile
            807 100%  788,09kB/s    0:00:00 (xfr#4, to-chk=80/85)
.cache/
.cache/motd.legal-displayed
              0 100%    0,00kB/s    0:00:00 (xfr#5, to-chk=76/85)
.cache/gstreamer-1.0/
.cache/gstreamer-1.0/registry.x86_64.bin
        394.232 100%   47,00MB/s    0:00:00 (xfr#6, to-chk=74/85)
.config/
.config/pulse/
.config/pulse/be8edc8cab394089a12f1d50b4f7de7e-card-database.tdb
            696 100%   84,96kB/s    0:00:00 (xfr#7, to-chk=72/85)
.config/pulse/be8edc8cab394089a12f1d50b4f7de7e-default-sink
              1 100%    0,12kB/s    0:00:00 (xfr#8, to-chk=71/85)
.config/pulse/be8edc8cab394089a12f1d50b4f7de7e-default-source
              1 100%    0,12kB/s    0:00:00 (xfr#9, to-chk=70/85)
.config/pulse/be8edc8cab394089a12f1d50b4f7de7e-device-volumes.tdb
          8.192 100% 1000,00kB/s    0:00:00 (xfr#10, to-chk=69/85)
.config/pulse/be8edc8cab394089a12f1d50b4f7de7e-stream-volumes.tdb
            696 100%   84,96kB/s    0:00:00 (xfr#11, to-chk=68/85)
.config/pulse/cookie
            256 100%   31,25kB/s    0:00:00 (xfr#12, to-chk=67/85)
snap/
snap/snapd-desktop-integration/
snap/snapd-desktop-integration/current -> 253
snap/snapd-desktop-integration/253/
snap/snapd-desktop-integration/253/.last_revision
             31 100%    3,78kB/s    0:00:00 (xfr#13, to-chk=62/85)
snap/snapd-desktop-integration/253/.themes -> /snap/snapd-desktop-integration/253/data-dir/themes
snap/snapd-desktop-integration/253/.config/
snap/snapd-desktop-integration/253/.config/user-dirs.dirs
            633 100%   77,27kB/s    0:00:00 (xfr#14, to-chk=50/85)
snap/snapd-desktop-integration/253/.config/user-dirs.locale
              5 100%    0,61kB/s    0:00:00 (xfr#15, to-chk=49/85)
snap/snapd-desktop-integration/253/.config/fontconfig/
snap/snapd-desktop-integration/253/.config/fontconfig/fonts.conf
            415 100%   50,66kB/s    0:00:00 (xfr#16, to-chk=44/85)
snap/snapd-desktop-integration/253/.config/gtk-2.0/
snap/snapd-desktop-integration/253/.config/gtk-2.0/gtkfilechooser.ini -> /home/cryptouser/.config/gtk-2.0/gtkfilechooser.ini
snap/snapd-desktop-integration/253/.config/gtk-3.0/
snap/snapd-desktop-integration/253/.config/gtk-3.0/bookmarks -> /home/cryptouser/.config/gtk-3.0/bookmarks
snap/snapd-desktop-integration/253/.config/gtk-3.0/gtk.css -> /home/cryptouser/.config/gtk-3.0/gtk.css
snap/snapd-desktop-integration/253/.config/gtk-3.0/settings.ini -> /home/cryptouser/.config/gtk-3.0/settings.ini
snap/snapd-desktop-integration/253/.config/ibus/
snap/snapd-desktop-integration/253/.config/ibus/bus -> /home/cryptouser/.config/ibus/bus
snap/snapd-desktop-integration/253/.local/
snap/snapd-desktop-integration/253/.local/share/
snap/snapd-desktop-integration/253/.local/share/themes -> /snap/snapd-desktop-integration/253/data-dir/themes
snap/snapd-desktop-integration/253/.local/share/glib-2.0/
snap/snapd-desktop-integration/253/.local/share/glib-2.0/schemas/
snap/snapd-desktop-integration/253/.local/share/icons/
snap/snapd-desktop-integration/253/Desktop/
snap/snapd-desktop-integration/253/Documents/
snap/snapd-desktop-integration/253/Downloads/
snap/snapd-desktop-integration/253/Music/
snap/snapd-desktop-integration/253/Pictures/
snap/snapd-desktop-integration/253/Public/
snap/snapd-desktop-integration/253/Templates/
snap/snapd-desktop-integration/253/Videos/
snap/snapd-desktop-integration/common/
snap/snapd-desktop-integration/common/.cache/
snap/snapd-desktop-integration/common/.cache/gdk-pixbuf-loaders.cache
          3.900 100%  423,18kB/s    0:00:00 (xfr#17, to-chk=32/85)
snap/snapd-desktop-integration/common/.cache/fontconfig/
snap/snapd-desktop-integration/common/.cache/fontconfig/064af4f2c4d6b9397a4b1c96c30800ef-le64.cache-7
          2.864 100%  310,76kB/s    0:00:00 (xfr#18, to-chk=28/85)
snap/snapd-desktop-integration/common/.cache/fontconfig/39d807eeea95c2ac7d8772ed62bded7a-le64.cache-7
            352 100%   38,19kB/s    0:00:00 (xfr#19, to-chk=27/85)
snap/snapd-desktop-integration/common/.cache/fontconfig/636e39dd-4582-4fa9-ae56-e06fa08675a2-le64.cache-7
          2.456 100%  266,49kB/s    0:00:00 (xfr#20, to-chk=26/85)
snap/snapd-desktop-integration/common/.cache/fontconfig/CACHEDIR.TAG
            200 100%   21,70kB/s    0:00:00 (xfr#21, to-chk=25/85)
snap/snapd-desktop-integration/common/.cache/fontconfig/a704df002d997bbd1bdaa99b50d07a5e-le64.cache-7
            240 100%   26,04kB/s    0:00:00 (xfr#22, to-chk=24/85)
snap/snapd-desktop-integration/common/.cache/fontconfig/fc00a55f7c3237a73f3e9bf08673f589-le64.cache-7
         15.904 100%    1,69MB/s    0:00:00 (xfr#23, to-chk=23/85)
snap/snapd-desktop-integration/common/.cache/gio-modules/
snap/snapd-desktop-integration/common/.cache/gio-modules/giomodule.cache
            196 100%   21,27kB/s    0:00:00 (xfr#24, to-chk=22/85)
snap/snapd-desktop-integration/common/.cache/gio-modules/libdconfsettings.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gio/modules/libdconfsettings.so
snap/snapd-desktop-integration/common/.cache/gio-modules/libgioenvironmentproxy.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gio/modules/libgioenvironmentproxy.so
snap/snapd-desktop-integration/common/.cache/gio-modules/libgiognomeproxy.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gio/modules/libgiognomeproxy.so
snap/snapd-desktop-integration/common/.cache/gio-modules/libgiognutls.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gio/modules/libgiognutls.so
snap/snapd-desktop-integration/common/.cache/gio-modules/libgiolibproxy.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gio/modules/libgiolibproxy.so
snap/snapd-desktop-integration/common/.cache/immodules/
snap/snapd-desktop-integration/common/.cache/immodules/im-am-et.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules/im-am-et.so
snap/snapd-desktop-integration/common/.cache/immodules/im-broadway.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules/im-broadway.so
snap/snapd-desktop-integration/common/.cache/immodules/im-cedilla.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules/im-cedilla.so
snap/snapd-desktop-integration/common/.cache/immodules/im-cyrillic-translit.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules/im-cyrillic-translit.so
snap/snapd-desktop-integration/common/.cache/immodules/im-fcitx.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules/im-fcitx.so
snap/snapd-desktop-integration/common/.cache/immodules/im-ibus.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules/im-ibus.so
snap/snapd-desktop-integration/common/.cache/immodules/im-inuktitut.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules/im-inuktitut.so
snap/snapd-desktop-integration/common/.cache/immodules/im-ipa.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules/im-ipa.so
snap/snapd-desktop-integration/common/.cache/immodules/im-multipress.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules/im-multipress.so
snap/snapd-desktop-integration/common/.cache/immodules/im-thai.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules/im-thai.so
snap/snapd-desktop-integration/common/.cache/immodules/im-ti-er.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules/im-ti-er.so
snap/snapd-desktop-integration/common/.cache/immodules/im-ti-et.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules/im-ti-et.so
snap/snapd-desktop-integration/common/.cache/immodules/im-viqr.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules/im-viqr.so
snap/snapd-desktop-integration/common/.cache/immodules/im-wayland.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules/im-wayland.so
snap/snapd-desktop-integration/common/.cache/immodules/im-waylandgtk.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules/im-waylandgtk.so
snap/snapd-desktop-integration/common/.cache/immodules/im-xim.so -> /snap/snapd-desktop-integration/253/gnome-platform/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules/im-xim.so
snap/snapd-desktop-integration/common/.cache/immodules/immodules.cache
          5.217 100%  509,47kB/s    0:00:00 (xfr#25, to-chk=0/85)
Could not unlink the key(s) from your keying. Please use `keyctl unlink` if you wish to remove the key(s). Proceeding with umount.

========================================================================
Some Important Notes!

 1. The file encryption appears to have completed successfully, however,
    cryptouser MUST LOGIN IMMEDIATELY, _BEFORE_THE_NEXT_REBOOT_,
    TO COMPLETE THE MIGRATION!!!

 2. If cryptouser can log in and read and write their files, then the migration is complete,
    and you should remove /home/cryptouser.1NEhz1Mx.
    Otherwise, restore /home/cryptouser.1NEhz1Mx back to /home/cryptouser.

 3. cryptouser should also run 'ecryptfs-unwrap-passphrase' and record
    their randomly generated mount passphrase as soon as possible.

 4. To ensure the integrity of all encrypted data on this system, you
    should also encrypt swap space with 'ecryptfs-setup-swap'.
========================================================================

root@k3s-server:~# ls -la /home/cryptouser/
total 8
dr-x------ 2 cryptouser cryptouser 4096 дек 20 21:18 .
drwxr-xr-x 7 root       root       4096 дек 20 21:17 ..
lrwxrwxrwx 1 cryptouser cryptouser   56 дек 20 21:18 Access-Your-Private-Data.desktop -> /usr/share/ecryptfs-utils/ecryptfs-mount-private.desktop
lrwxrwxrwx 1 cryptouser cryptouser   36 дек 20 21:17 .ecryptfs -> /home/.ecryptfs/cryptouser/.ecryptfs
lrwxrwxrwx 1 cryptouser cryptouser   35 дек 20 21:17 .Private -> /home/.ecryptfs/cryptouser/.Private
lrwxrwxrwx 1 cryptouser cryptouser   52 дек 20 21:18 README.txt -> /usr/share/ecryptfs-utils/ecryptfs-mount-private.txt
```




---


### Задание 2
Установите поддержку LUKS.
Создайте небольшой раздел, например, 100 Мб.
Зашифруйте созданный раздел с помощью LUKS.

Подключил отдельный диск sdb к машине
```
root@k3s-server:~# lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0    7:0    0  63,9M  1 loop /snap/core20/2318
loop1    7:1    0     4K  1 loop /snap/bare/5
loop2    7:2    0 268,9M  1 loop /snap/firefox/4630
loop3    7:3    0  73,9M  1 loop /snap/core22/1722
loop4    7:4    0 268,4M  1 loop /snap/firefox/4650
loop5    7:5    0 349,7M  1 loop /snap/gnome-3-38-2004/143
loop6    7:6    0  91,7M  1 loop /snap/gtk-common-themes/1535
loop7    7:7    0  74,3M  1 loop /snap/core22/1612
loop8    7:8    0 505,1M  1 loop /snap/gnome-42-2204/176
loop9    7:9    0  63,7M  1 loop /snap/core20/2434
loop10   7:10   0  12,9M  1 loop /snap/snap-store/1113
loop11   7:11   0   497M  1 loop /snap/gnome-42-2204/141
loop12   7:12   0  38,8M  1 loop /snap/snapd/21759
loop14   7:14   0  44,3M  1 loop /snap/snapd/23258
loop15   7:15   0   568K  1 loop /snap/snapd-desktop-integration/253
loop16   7:16   0   500K  1 loop /snap/snapd-desktop-integration/178
loop17   7:17   0  12,2M  1 loop /snap/snap-store/1216
sda      8:0    0    90G  0 disk
├─sda1   8:1    0     1M  0 part
├─sda2   8:2    0   513M  0 part /boot/efi
└─sda3   8:3    0  89,5G  0 part /var/snap/firefox/common/host-hunspell
                                 /
sdb      8:16   0   100M  0 disk
sr0     11:0    1  1024M  0 rom
```

Создание и монтирование
```
root@k3s-server:~# parted /dev/sdb
GNU Parted 3.4
Using /dev/sdb
Welcome to GNU Parted! Type 'help' to view a list of commands.

Тут я решил вызвать помощь, потому что чуть забыл команды

(parted) help
  align-check TYPE N                       check partition N for TYPE(min|opt) alignment
  help [COMMAND]                           print general help, or help on COMMAND
  mklabel,mktable LABEL-TYPE               create a new disklabel (partition table)
  mkpart PART-TYPE [FS-TYPE] START END     make a partition
  name NUMBER NAME                         name partition NUMBER as NAME
  print [devices|free|list,all|NUMBER]     display the partition table, available devices, free space, all found partitions, or a particular partition
  quit                                     exit program
  rescue START END                         rescue a lost partition near START and END
  resizepart NUMBER END                    resize partition NUMBER
  rm NUMBER                                delete partition NUMBER
  select DEVICE                            choose the device to edit
  disk_set FLAG STATE                      change the FLAG on selected device
  disk_toggle [FLAG]                       toggle the state of FLAG on selected device
  set NUMBER FLAG STATE                    change the FLAG on partition NUMBER
  toggle [NUMBER [FLAG]]                   toggle the state of FLAG on partition NUMBER
  unit UNIT                                set the default unit to UNIT
  version                                  display the version number and copyright information of GNU Parted
(parted) mklabel gpt


(parted) mkpart primary ext4 0 100
Warning: The resulting partition is not properly aligned for best performance: 34s % 2048s != 0s
Ignore/Cancel?
Ignore/Cancel? ignore
(parted) print
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdb: 105MB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags:

Number  Start   End    Size   File system  Name     Flags
 1      0,02MB  100MB  100MB  ext4         primary

(parted) quit
```

Вызвал команду, чтобы проверить что диск я смонтировал

```
root@k3s-server:~# lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0    7:0    0  63,9M  1 loop /snap/core20/2318
loop1    7:1    0     4K  1 loop /snap/bare/5
loop2    7:2    0 268,9M  1 loop /snap/firefox/4630
loop3    7:3    0  73,9M  1 loop /snap/core22/1722
loop4    7:4    0 268,4M  1 loop /snap/firefox/4650
loop5    7:5    0 349,7M  1 loop /snap/gnome-3-38-2004/143
loop6    7:6    0  91,7M  1 loop /snap/gtk-common-themes/1535
loop7    7:7    0  74,3M  1 loop /snap/core22/1612
loop8    7:8    0 505,1M  1 loop /snap/gnome-42-2204/176
loop9    7:9    0  63,7M  1 loop /snap/core20/2434
loop10   7:10   0  12,9M  1 loop /snap/snap-store/1113
loop11   7:11   0   497M  1 loop /snap/gnome-42-2204/141
loop12   7:12   0  38,8M  1 loop /snap/snapd/21759
loop14   7:14   0  44,3M  1 loop /snap/snapd/23258
loop15   7:15   0   568K  1 loop /snap/snapd-desktop-integration/253
loop16   7:16   0   500K  1 loop /snap/snapd-desktop-integration/178
loop17   7:17   0  12,2M  1 loop /snap/snap-store/1216
sda      8:0    0    90G  0 disk
├─sda1   8:1    0     1M  0 part
├─sda2   8:2    0   513M  0 part /boot/efi
└─sda3   8:3    0  89,5G  0 part /var/snap/firefox/common/host-hunspell
                                 /
sdb      8:16   0   100M  0 disk
└─sdb1   8:17   0  95,4M  0 part
sr0     11:0    1  1024M  0 rom
```

Да диск смонтировал, все ок, двигаюсь далее.

```
root@k3s-server:~# cryptsetup luksFormat /dev/sdb1

WARNING!
========
This will overwrite data on /dev/sdb1 irrevocably.

Are you sure? (Type 'yes' in capital letters): YES
Enter passphrase for /dev/sdb1:
Verify passphrase:
```
Двигаюсь далее
Шифрую и прикручиваю монтирование

```
root@k3s-server:~# cryptsetup luksOpen /dev/sdb1 my_encrypted
Enter passphrase for /dev/sdb1:
root@k3s-server:~# mkfs.ext4 /dev/mapper/my_encrypted
mke2fs 1.46.5 (30-Dec-2021)
Creating filesystem with 20313 4k blocks and 20320 inodes

Allocating group tables: done
Writing inode tables: done
Creating journal (1024 blocks): done
Writing superblocks and filesystem accounting information: done

root@k3s-server:~# mkdir /mnt/my_encrypted_partition
root@k3s-server:~# mount /dev/mapper/my_encrypted /mnt/my_encrypted_partition
```

Проверяю что получилось
```
root@k3s-server:~# lsblk
NAME             MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINTS
loop0              7:0    0  63,9M  1 loop  /snap/core20/2318
loop1              7:1    0     4K  1 loop  /snap/bare/5
loop2              7:2    0 268,9M  1 loop  /snap/firefox/4630
loop3              7:3    0  73,9M  1 loop  /snap/core22/1722
loop4              7:4    0 268,4M  1 loop  /snap/firefox/4650
loop5              7:5    0 349,7M  1 loop  /snap/gnome-3-38-2004/143
loop6              7:6    0  91,7M  1 loop  /snap/gtk-common-themes/1535
loop7              7:7    0  74,3M  1 loop  /snap/core22/1612
loop8              7:8    0 505,1M  1 loop  /snap/gnome-42-2204/176
loop9              7:9    0  63,7M  1 loop  /snap/core20/2434
loop10             7:10   0  12,9M  1 loop  /snap/snap-store/1113
loop11             7:11   0   497M  1 loop  /snap/gnome-42-2204/141
loop12             7:12   0  38,8M  1 loop  /snap/snapd/21759
loop14             7:14   0  44,3M  1 loop  /snap/snapd/23258
loop15             7:15   0   568K  1 loop  /snap/snapd-desktop-integration/253
loop16             7:16   0   500K  1 loop  /snap/snapd-desktop-integration/178
loop17             7:17   0  12,2M  1 loop  /snap/snap-store/1216
sda                8:0    0    90G  0 disk
├─sda1             8:1    0     1M  0 part
├─sda2             8:2    0   513M  0 part  /boot/efi
└─sda3             8:3    0  89,5G  0 part  /var/snap/firefox/common/host-hunspell
                                            /
sdb                8:16   0   100M  0 disk
└─sdb1             8:17   0  95,4M  0 part
  └─my_encrypted 252:0    0  79,4M  0 crypt /mnt/my_encrypted_partition
sr0               11:0    1  1024M  0 rom
```

Проверка статуса шифрования
```
root@k3s-server:~# cryptsetup status my_encrypted
/dev/mapper/my_encrypted is active and is in use.
  type:    LUKS2
  cipher:  aes-xts-plain64
  keysize: 512 bits
  key location: keyring
  device:  /dev/sdb1
  sector size:  512
  offset:  32768 sectors
  size:    162511 sectors
  mode:    read/write
root@k3s-server:~# lsblk
NAME             MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINTS
loop0              7:0    0  63,9M  1 loop  /snap/core20/2318
loop1              7:1    0     4K  1 loop  /snap/bare/5
loop2              7:2    0 268,9M  1 loop  /snap/firefox/4630
loop3              7:3    0  73,9M  1 loop  /snap/core22/1722
loop4              7:4    0 268,4M  1 loop  /snap/firefox/4650
loop5              7:5    0 349,7M  1 loop  /snap/gnome-3-38-2004/143
loop6              7:6    0  91,7M  1 loop  /snap/gtk-common-themes/1535
loop7              7:7    0  74,3M  1 loop  /snap/core22/1612
loop8              7:8    0 505,1M  1 loop  /snap/gnome-42-2204/176
loop9              7:9    0  63,7M  1 loop  /snap/core20/2434
loop10             7:10   0  12,9M  1 loop  /snap/snap-store/1113
loop11             7:11   0   497M  1 loop  /snap/gnome-42-2204/141
loop12             7:12   0  38,8M  1 loop  /snap/snapd/21759
loop14             7:14   0  44,3M  1 loop  /snap/snapd/23258
loop15             7:15   0   568K  1 loop  /snap/snapd-desktop-integration/253
loop16             7:16   0   500K  1 loop  /snap/snapd-desktop-integration/178
loop17             7:17   0  12,2M  1 loop  /snap/snap-store/1216
sda                8:0    0    90G  0 disk
├─sda1             8:1    0     1M  0 part
├─sda2             8:2    0   513M  0 part  /boot/efi
└─sda3             8:3    0  89,5G  0 part  /var/snap/firefox/common/host-hunspell
                                            /
sdb                8:16   0   100M  0 disk
└─sdb1             8:17   0  95,4M  0 part
  └─my_encrypted 252:0    0  79,4M  0 crypt /mnt/my_encrypted_partition
```






