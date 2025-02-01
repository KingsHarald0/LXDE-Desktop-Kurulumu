## Chrome ##

Kurulum dosyasını indirin
```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```
Kurulumunu yapın
```bash
sudo dpkg -i google-chrome-stable_current_amd64.deb
```
Eğer bağımlılık hatası alırsanız
```bash
sudo apt --fix-broken install -y
```
```bash
sudo dpkg -i google-chrome-stable_current_amd64.deb
```

## Brave ##
 
Gerekli paketleri kurun
```bash
sudo apt install apt-transport-https curl -y
```
Brave imza anahtarını ekleyin
```bash
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
```
Brave depolarını ekleyin
```bash
echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main" | sudo tee /etc/apt/sources.list.d/brave-browser-release.list
```
Paket listelerini güncelleyin ve Brave’i kurun
```bash
sudo apt update
```
```bash
sudo apt install brave-browser -y
```

## Edge ##

Microsoft’un imza anahtarını indirin ve sisteme ekleyin
```bash
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo install -o root -g root -m 644 microsoft.gpg /usr/share/keyrings/
rm microsoft.gpg
```
Microsoft Edge deposunu ekleyin
```bash
sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft.gpg] https://packages.microsoft.com/repos/edge stable main" > /etc/apt/sources.list.d/microsoft-edge.list'
```
Paket listelerini güncelleyin ve Microsoft Edge’i kurun
```bash
sudo apt update
```
```bash
sudo apt install microsoft-edge-stable -y
```
