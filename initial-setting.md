## timezone

[UTC から Japan に変更]
 
 (現状確認):
 ls -alF /etc/localtime  
 lrwxrwxrwx 1 root root 27 Nov 26 13:05 /etc/localtime -> ../usr/share/zoneinfo/UTC
 
 (候補確認):
 ls -a /usr/share/zoneinfo  

 (置き換え)：
 sudo ln -sf ../usr/share/zoneinfo/Japan /etc/localtime
 
 (変更確認)：
 date

## Locale & keymap
 
 /etc/sysconfig/... がなかったので。  
 localectl を試すと。。。  
 \-----  
    System Locale: n/a  
       VC Keymap: n/a  
      X11 Layout: n/a  
 \-----  
 と表示された。使えそう。  
 
 [Locale]  
 sudo localectl set-locale LANG=ja_JP.utf8  
 -> /etc/locacle.conf  
 
 [keymap]  
 sudo localectl set-keymap jp106  
 -> /etc/vconsole.conf  
 
 ※locale はともかく、keymap はteraterm 越しの場合、  
   teraterm の設定が有効だったので、keymapの設定不要かも。  
 ※ virtualbox のconsoleでは、上記を設定しても keymapはus のまま。  
