## 1. cron による再起動スケジューリング
```bash
sudo crontab -e
```
### 例 : 毎日夜 0 時 1 分に再起動を行う
| mm | HH | dd | mm | day | command |
| -- | -- | -- | -- | --- | ------- |
|  1 |  0 |  * |  * |   * | reboot  |

## 2. 温度測定
```bash
vcgencmd measure_temp
cat /sys/class/thermal/thermal_zone0/temp
```

## 3. ディスクバックアップ
```bash
dump -j -f [宛先ファイルパス] [バックアップ対象デバイス]
sudo dump -j -f /home/pi/backup/yyyymmdd/sdb1.dump /dev/sdb1
```

## 4. リカバリ
```bash
restore -rf [バックアップファイルパス]
# カレントディレクトリへ展開を行う
sudo restore -rf /home/pi/backup/yyyymmdd/sdb1.dump
```

## 5. ディスクパーティション全体のコピー
```bash
# コピー元の指定時にはディレクトリ「以下/自体」か気を付けること
# 外付け SSD によるブートを行う場合はディレクトリ以下のコピーを行う必要がある
rsync -a [コピー元 マウントポイント] [コピー先 マウントポイント]
```

## 6. ファイルシステムの表示
```bash
lsblk --fs
```
