# Управление Rooky через RRStudio на Windows
## Подготовка
1. Выполнить [подготовку Windows](/WSL2/preparing_windows)
2. Потребуется скачать ROS Kinetic ~2Gb:
   * Нажать **Win + X**
   * Выбрать окно **PowerShell (админ)**
   * Подать следующие команды:
     ```PowerShell
     wsl
     sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
     sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
     sudo apt-get update
     sudo apt-get install ros-kinetic-desktop-full
     echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
     source ~/.bashrc
     ```
   * Установить пакет с серверным ПО **promobot-edu_control**
     * Добавить в систему ppa репозиторий (если не добавлен)
       ```sh
       curl -s --compressed "https://Promobot-education.github.io/ppa/KEY.gpg" | sudo apt-key add -
       sudo curl -s -o /etc/apt/sources.list.d/promobot-education.list "https://Promobot-education.github.io/ppa/promobot-education.list"
       ```
     * Установить пакет:
       ```sh
       sudo apt update
       sudo apt install promobot-edu-control
       ```
     * Добавить путь до файлов серверного ПО
       ```sh
       echo "source /opt/promobot/EduControl/install/setup.bash" >> ~/.bashrc
       source ~/.bas
       ```

## Запуск (Поддерживается симуляция)
1. [Корректно запустить WSL](/WSL2/true_start)
2. Запустить новое окно PowerShell:
   * нажать **Win + X**
   * выбрать **PowerShell (админ)**
3. Запустить Linux командой:
   ```PowerShell
   wsl
   ```
4. В зависимости от типа Rooky запустить ROS командой:
   ```sh
   roslaunch promobot_control promobot_hardware.launch side:=left
   ```
   или 
   ```sh
   roslaunch promobot_control promobot_hardware.launch side:=right
   ```
5. Запустить [RRStudio в Windows](/RRStudio/setup_windows)
6. Подключиться в RRStudio к серверу по адресу: **127.0.0.1**

## Запуск симуляции
Запуск симуляции происходит аналогично запуску с реальным устройством:

В зависимости от стороны руки симуляция запускается командой:
```sh
roslaunch promobot_control start_simulation.launch side:=left
```
или 
```sh
roslaunch promobot_control start_simulation.launch side:=right
```