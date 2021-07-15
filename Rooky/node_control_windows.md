# Управление Rooky через узел ROS на Ubuntu 16.04
## Подготовка 
1. Установить [git](https://git-scm.com/download/win)
2. Установить [Python 3.5.4](https://www.python.org/ftp/python/3.5.4/python-3.5.4-amd64.exe) (При установке поставить галочку **"Add Python 3.5 to PATH"**)
3. **Создать и перейти** в папку где будут храниться клонированные репозитории (например: C:\git)
4. Нажать **Shift + правая кнопка мыши**
5. Выбрать **Открыть окно PowerShell здесь**
6. Клонировать репозиторий Rooky командой:
   ```PowerShell
   git clone https://github.com/Promobot-education/Rooky.git
   ```
7. Перейти в папку с установочным скриптом командой:
   ```PowerShell
   cd .\Rooky\python
   ```
8. Запустить скрипт установки библиотек командой:
   ```PowerShell
   python.exe setup.py .\setup.py
   ```
9. Установить [драйвера](/Rooky/res/drivers/CDM21228_Setup.exe) для интерфейсной платы
10. Выполнить [подготовку Windows](/WSL2/preparing_windows)
11. Скачать ROS Kinetic ~2Gb:
   * Нажать **Win + X**
   * Выбрать окно **PowerShell (админ)**
   * Подать следующие команды:
     ```PowerShell
     wsl
     sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
     sudo apt install curl # Если curl не установлен
     curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
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
       source ~/.bashrc
       ```
12. **Настройка закончена**

## Запуск (Поддерживается симуляция)
1. [Корректный запуск WSL](/WSL2/true_start)
2. Запустить новое окно PowerShell:
   * нажать **Win + X**
   * выбрать **PowerShell (админ)**
3. Запустить Linux командой:
   ```PowerShell
   wsl
   ```
4. В зависимости от стороны руки запустить ROS командой:
   ```sh
   roslaunch promobot_control promobot_hardware.launch side:=left
   ```
   или 
   ```sh
   roslaunch promobot_control promobot_hardware.launch side:=right
   ```
5. Запустить еще одно новое окно PowerShell:
   * нажать **Win + X**
   * выбрать **PowerShell (админ)**
6. Запустить Linux командой:
   ```PowerShell
   wsl
   ```
7. Запустить пример узла ROS командой в PowerShell:
   ```PowerShell
   python /mnt/c/git/Rooky/ros/joints.py
   ```

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