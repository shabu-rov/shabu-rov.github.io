# Управление Rooky через RRStudio на Ubuntu 16.04
## Подготовка
* Открыть терминал: **Ctrl + Alt + T**
* Потребуется скачать ROS Kinetic ~2Gb
  ```sh
  sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
  sudo apt install curl # Если curl не установлен
  curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
  sudo apt-get update
  sudo apt-get install ros-kinetic-desktop-full
  sudo apt install python-rosdep
  sudo rosdep init
  rosdep update
  echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
  source ~/.bashrc
  ```
* Установить пакет с серверным ПО **promobot-edu-control**
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
    source ~/.bashrc
    ```
  * Проверить зависимости
    ```sh
    cd /opt/promobot/EduControl
    rosdep install --from-paths install --ignore-src -r -y
    ```
* **Подготовка для работы с ROS закончена.**

## Запуск для работы с реальным устройством
- Подключить манипулятор Rooky к ПК
- Открыть терминал: **Ctrl + Alt + T**
- В зависимости от типа Rooky запустить ROS командой:
  * **Для левой Rooky:**
    ```sh
    roslaunch promobot_control promobot_hardware.launch side:=left
    ```
  * **Для правой Rooky:**
    ```sh
    roslaunch promobot_control promobot_hardware.launch side:=right
    ```
- Запустить [RRStudio](/RRStudio/setup_ubuntu)
- Выбрать в RRStudio соответствующее устройство.

## Запуск для работы в режиме симуляции, без реального устройства
Запуск симуляции происходит аналогично запуску с реальным устройством.  
Отличаются только команды на запуск серверного ПО (ROS):  
* **Для левой Rooky:**
  ```sh
  roslaunch promobot_control start_simulation.launch side:=left
  ```
* **Для правой Rooky:**
  ```sh
  roslaunch promobot_control start_simulation.launch side:=right
  ```