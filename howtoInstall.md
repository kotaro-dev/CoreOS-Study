# my condition:
  - host os : windows7
  - vm tool : virtualbox (4.3.18 r96516)
  - coreos  : coreos_production_iso_image.iso (CoreOS 444.5.0)

## virtual box setting

1. vbox 作成時のポイント
   ネットワーク アダプターを2つ用意。(nat,host only)

## CoreOS install step

1. check ip address for connect ssh
   teraterm で SSH 接続して作業するための ip addressを確認しておきます。  
   teraterm 使わなくても作業できますが、利用した方が何かと楽かと。  
   (以下の作業では、利用していないです。)
   
   ifconfig

1. change core user password
   仮 Install の時点で作成されている core user のpasswdを変更します。  
   この作業は、teraterm でSSH login するために必要です。  
   teraterm を利用しない場合は、作業不要かと。  
   
   sudo passwd core
   
   ※新しいパスワードは 5文字以上、大文字、小文字、数字を混在させること！とのこと。  
     キーボードがus用なので注意！  
     
1. create cloud-config.
   まず、平文でpassword file を作成。  
```
   sudo vim mypasswd
   [mypasswd]
   Core0s  
```   
   今回は password を Core0s とします。  
   
   次に、-1 (MD5-based password algorithm) で暗号化。  
   
  openssl passwd -1 -in mypasswd>cloud-config
  
  平文を削除。  
  rm mypasswd
  
  最後に、cloud-config を編集。  
```  
  sudo vim cloud-config
  [cloud-config]
   #cloud-config  
   
  users:  
    - name: core
      passwd: {hashed mypasswd}
```  
1. install coreos  
   sudo coreos-install -d /dev/sda -C stable -c cloud-config
   
1. enject iso image (or umount cdrom)  
   sudo eject

1. reboot and login core user using mypasswd  
   sudo reboot
   
   (login)  
   user   : core  
   passwd : Core0s  
  
