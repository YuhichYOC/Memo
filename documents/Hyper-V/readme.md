## Hyper-V の無効化  
  
```bash
bcdedit /set hypervisorlaunchtype off
```
  
## Hyper-V の有効化  
  
```bash
bcdedit /set hypervisorlaunchtype auto
```
  
## Windows の再起動 ( 即時 )  
  
```bash
shutdown /r /t 0
```
  
## 管理者権限で実行  
  
```bash
powershell start-process [command] -verb runas
```
