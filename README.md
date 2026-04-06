# Install_Qt6.5.5._QtCreator16.0.2_OrangePi6Plus
Установка Qt 6.5.5 и Qt Creator 16.0.2 на Orange Pi 6 Plus
### Обновите систему.
```
sudo apt update
sudo apt upgrade
sudo reboot
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
### Скачайте Qt6.5.5
```
cd ~/Downloads
wget https://github.com/stimandrew/Install_Qt6.5.5._QtCreator16.0.2_OrangePi6Plus/releases/download/v1.0.1/qt6.5.5-orangepi6plus.tar.gz
```
### Распакуйте архив в директорию Qt6.5.5
```
mkdir ~/Qt6.5.5
cd ~/Qt6.5.5
tar -xzf ~/Downloads/qt6.5.5-orangepi6plus.tar.gz
```
### Чтобы система и пакеты находили Qt, добавьте его в пути ```PATH```, ```LD_LIBRARY_PATH``` и ```PKG_CONFIG_PATH```.
```
echo 'export PATH="/home/$USER/Qt6.5.5/bin:$PATH"' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH="/home/$USER/Qt6.5.5/lib:$LD_LIBRARY_PATH"' >> ~/.bashrc
echo 'export PKG_CONFIG_PATH="/home/$USER/Qt6.5.5/lib/pkgconfig:$PKG_CONFIG_PATH"' >> ~/.bashrc
source ~/.bashrc
```
### Добавить путь к библиотекам. (Измените имя пользователя на то, которое у вас в системе)
```
echo '/home/orangepi/Qt6.5.5/lib' | sudo tee /etc/ld.so.conf.d/qt6_5_5.conf
sudo ldconfig
```
### Проверим настройки ```qmake``` как системный.
```
qmake --version
pkg-config --modversion Qt6Core
qt-cmake --version
```
Должно вывести ```QMake version 3.1 Using Qt version 6.5.5 in /home/orangepi/Qt6.5.5/lib```,```6.5.5``` и ```cmake version 3.28.3``` соответственно.
### Проверка путей
```
ldconfig -p | grep Qt6
```
-------------------------------------------------------
### Скачайте QtCreator 16.0.2
```
cd ~/Downloads
wget https://github.com/stimandrew/Install_Qt6.5.5._QtCreator16.0.2_OrangePi6Plus/releases/download/v1.0.0/qtcreator-16.0.2-orangepi6plus.tar.gz
```
### Распакуйте архив в директорию qtcreator
```
mkdir /opt/qtcreator
cd /opt/qtcreator
tar -xzf ~/Downloads/qtcreator-16.0.2-orangepi6plus.tar.gz
```
### Создать скрипт в /usr/local/bin
```
sudo bash -c 'cat > /usr/local/bin/qtcreator << EOF
#!/bin/bash
export LD_LIBRARY_PATH=/home/orangepi/Qt6.5.5/lib:\$LD_LIBRARY_PATH
export QT_PLUGIN_PATH=/home/orangepi/Qt6.5.5/plugins
export QML_IMPORT_PATH=/home/orangepi/Qt6.5.5/qml
export QML2_IMPORT_PATH=/home/orangepi/Qt6.5.5/qml
exec /opt/qtcreator/bin/qtcreator "\$@"
EOF'

sudo chmod +x /usr/local/bin/qtcreator

# Проверить
which qtcreator
qtcreator --version
```
