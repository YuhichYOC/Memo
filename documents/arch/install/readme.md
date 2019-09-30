|項番|概要|打鍵内容|
|:--|:--|:--|
|1.|EFI を使ってはならない||
|1.|キーボードレイアウトを読み込ませる|loadkeys jp 106|
|1.|起動モードの確認|ls /sys/firmware/efi/efivars|
|1.|パーティションの作成・ディスクの確認 ( 全体 )|fdisk -l|
|1.|パーティションの作成・ディスク 1 の確認|fdisk -l /dev/sda|
|1.|/dev/sda にパーティション作成開始|fdisk /dev/sda|
|1.|/(/dev/sda1) の作成|n|
|1.|パーティションタイプの指定|p ... デフォルト & 打鍵なし|
|1.|パーティション番号の指定|1 ... デフォルト & 打鍵なし|
|1.|開始セクタの指定|2048 ... デフォルト & 打鍵なし|
|1.|終了セクタの指定|ディスク末尾 ... デフォルト & 打鍵なし|
|1.|パーティションの作成終了|w|
|1.|/etc/mke2fs.conf 設定変更|vi /etc/mke2fs.conf|
|1.|フォーマットオプション 64 bit を除外|ext の "64bit" を削除|
|1.|/dev/sda1 のフォーマット|mkfs.ext4 /dev/sda1|
|1.|マウント|mount /dev/sda1 /mnt|
|1.|インターネットへの接続状態確認|ping google.com|
|1.|システムクロックの更新|timedatectl set-ntp true|
|1.|システムインストール|pacstrap /mnt base base-devel|
|1.|マウントテーブル作成|genfstab -U /mnt >> /mnt/etc/fstab|
|1.|マウントテーブルの確認|vi /mnt/etc/fstab|
|1.|chroot|arch-chroot /mnt|
|1.|タイムゾーンの変更|ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime|
|1.|タイムゾーンの変更|hwclock --systohc --utc|
|1.|ロケール変更のため locale.gen を修正|vi /etc/locale.gen|
|1.|ロケール en_US の有効化|"en_US.UTF-8 UTF-8" をコメント復帰|
|1.|ロケール ja_JP の有効化|"ja_JP.UTF-8 UTF-8" をコメント復帰|
|1.|ロケールの変更|locale-gen|
|1.|ホスト名の設定 1|echo arch1 > /etc/hostname|
|1.|ホスト名の設定 2|vi /etc/hosts|
|1.|ホスト名の設定 3|"127.0.1.1 arch1.localdomain arch1" の行を追加|
|1.|root ユーザーのパスワードを作成|passwd|
|1.|パスワードの入力|[パスフレーズ]|
|1.|Syslinux インストール|pacman -S syslinux|
|1.|使用準備|syslinux-install_update -i -a -m|
|1.|/boot/syslinux/syslinux.cfg の編集|vi /boot/syslinux/syslinux.cfg|
|1.|LABEL arch のブートドライブ番号を修正|/dev/sda3 → /dev/sda1 に修正|
|1.|LABEL archfallback のブートドライブ番号を修正|/dev/sda3 → /dev/sda1 に修正|
|1.|システム更新|pacman -Syu|
|1.|X Server のインストール|pacman -S xorg-server xorg-server-devel|
|1.|ビデオドライバのインストール|デフォルト & 打鍵なし|
|1.|MATE のインストール|pacman -S mate mate-extra|
|1.|lightDM のインストール|pacman -S lightdm lightdm-gtk-greeter|
|1.|キーボードレイアウトの設定 1|vi /usr/share/X11/xorg.conf.d/40-libinput.conf|
|1.|キーボードレイアウトの設定 2|Option "XkbModel" "pc106" の行を追加|
|1.|キーボードレイアウトの設定 3|Option "XkbLayout" "jp" の行を追加|
|1.|/etc/locale.conf の編集|vi /etc/locale.conf|
|1.|LANG の指定|LANG=ja_JP.UTF-8 の行を追加|
|1.|LC_NUMERIC の指定|LC_NUMERIC=ja_JP.UTF-8 の行を追加|
|1.|LC_TIME の指定|LC_TIME=ja_JP.UTF-8 の行を追加|
|1.|LC_MONETARY の指定|LC_MONETARY=ja_JP.UTF-8 の行を追加|
|1.|LC_PAPER の指定|LC_PAPER=ja_JP.UTF-8 の行を追加|
|1.|LC_MEASUREMENT の指定|LC_MEASUREMENT=ja_JP.UTF-8 の行を追加|
|1.|日本語フォントのインストール|sudo pacman -S otf-ipafont|
|1.|/mnt へのルートディレクトリ変更を解除|exit|
|1.|再起動|shutdown -r now|
|1.|ネットワークへの再接続|systemctl start dhcpcd.service|
|1.|GUI ログインユーザーの作成|useradd -m -G wheel -s /bin/bash [ユーザー名]|
|1.|GUI ログインユーザーのパスワードを設定|passwd [ユーザー名]|
|1.|パスワードの入力|[パスフレーズ]|
|1.|/etc/sudoers の編集|visudo|
|1.|wheel グループへの権限付与|"%wheel ALL=(ALL) ALL" の行をコメント復帰|
|1.|GUI ログイン画面の起動|systemctl start lightdm|
|1.|日本語入力システムのインストール|sudo pacman -S fcitx fcitx-mozc fcitx-configtool fcitx-im|
|1.|.xprofile の作成|vi .xprofile|
|1.|GTK_IM_MODULE の指定|export GTK_IM_MODULE=fcitx|
|1.|QT_IM_MODULE の指定|export QT_IM_MODULE=fcitx|
|1.|XMODIFIERS の指定|export XMODIFIERS="@im=fcitx"|
|1.|DefaultIMModule の指定|export DefaultIMModule=fcitx|
|1.|VMWare tools のインストール|sudo pacman -S open-vm-tools|
