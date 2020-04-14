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
