# LXDE Kurulum ve Uzaktan Erişim (XRDP) Rehberi

Bu rehberde, Ubuntu (veya Ubuntu tabanlı dağıtımlarda) LXDE masaüstü ortamını kurmayı ve uzaktan masaüstü erişimi için XRDP yapılandırmasını adım adım anlatacağız.

---

## 1. Sistem Güncelleme

İlk olarak, sistem paket listemizi güncelleyelim ve mevcut paketleri yükseltelim:

```bash
sudo apt update && sudo apt upgrade -y
```
```
sudo apt install curl iptables build-essential git wget jq make gcc nano tmux htop nvme-cli pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev screen -y
```

## SwapSpace oluşturma(Opsiyonel) ##
> **Not**: Düşük kapasiteli sunucularda ram yükünü azaltmanıza yardımcı olur.

Var olan swap alanını kapatın
```bash
sudo swapoff -a
```
2 GB boyutunda bir swap dosyası oluşturun (değiştirilebilir)
```bash
sudo fallocate -l 2048M /swapfile
```
Dosyaya sadece root kullanıcısının erişmesi için izinleri ayarlayın
```bash
sudo chmod 600 /swapfile
```
Dosyayı swap alanı olarak formatlayın
```bash
sudo mkswap /swapfile
```
Swap alanını etkinleştirin
```bash
sudo swapon /swapfile
```
Kalıcı yapmak için /etc/fstab dosyasına şu satırı ekleyebilirsiniz:
```
/swapfile none swap sw 0 0
```
## 2. LXDE Masaüstü Kurulumu ve Yeni Kullanıcı Ekleme ##

Yeni bir kullanıcı oluşturun(örnek kullanıcı adı: `k`):

```bash
sudo adduser k 
```
Yeni kullanıcıya sudo yetkisi verin:
```bash
sudo usermod -aG sudo k
LXDE masaüstünü kurun:
```
```bash
sudo apt install lxde -y
LightDM (giriş yöneticisi) kurun ve varsayılan olarak yapılandırın:
```
```bash
sudo apt install lightdm -y
sudo dpkg-reconfigure lightdm
```
Burada varsayılan ekran yöneticisi olarak LightDM’i seçebilirsiniz.

## 4. XRDP Kurulumu

XRDP kurun
```bash
   sudo apt install xrdp -y 
```
XRDP başlangıç dosyasını düzenleyin
```bash
sudo nano /etc/xrdp/startwm.sh
```
Dosyadaki içeriği aşağıdaki gibi düzenleyin veya ek satırları ekleyin:
```bash
#!/bin/sh
# xrdp X session start script (c) 2015, 2017, 2021 mirabilos
# published under The MirOS Licence

if test -r /etc/profile; then
    . /etc/profile
fi

if test -r ~/.profile; then
    . ~/.profile
fi

# Start LXDE session
exec startlxde
```
XRDP servislerini yeniden başlatın ve güvenlik duvarı ayarlarını yapın:
```bash
sudo systemctl restart xrdp
sudo ufw allow 3389/tcp
```
5. Tarayıcı Kurulumu
Chrome
Brave
Edge

