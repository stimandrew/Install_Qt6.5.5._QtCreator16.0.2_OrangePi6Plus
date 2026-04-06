# Install_Qt6.5.5._QtCreator16.0.2_OrangePi6Plus
Установка Qt 6.5.5 и Qt Creator 16.0.2 на Orange Pi 6 Plus
### Обновите систему.
```
sudo apt update
sudo apt upgrade
sudo reboot
```
### Установите зависимости из файла install_packages_target.sh
```
cd ~
wget https://raw.githubusercontent.com/stimandrew/CrossCompileQtForOrangePi5Ultra/main/install_packages_target.sh
chmod +x install_packages_target.sh
sudo ./install_packages_target.sh
```
### Установите зависимости из файла install_packages_host.sh
```
cd ~
wget https://raw.githubusercontent.com/stimandrew/CrossCompileQtForOrangePi5Ultra/main/install_packages_host.sh
chmod +x install_packages_host.sh
sudo ./install_packages_host.sh
```
```
sudo apt install llvm-dev libclang-dev clang
```

