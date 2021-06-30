# Прямое управление Rooky на Ubuntu 16.04
## Подготовка
* Открыть терминал: **Ctrl + Alt + T**
* Написать следующие команды:
```sh
cd ~
git clone https://github.com/Promobot-education/Rooky.git
cd ./Rooky
chmod +x ./install.sh
./install.sh
```
* **Подготовка для прямого управления закончена.**

## Работа
* Подключить манипулятор Rooky к ПК
* Открыть терминал: **Ctrl + Alt + T**
* Перейти в директорию с примером:
  ```sh
  cd ~/Rooky/python/examples
  ```
* Запустить пример:
  ```
  python arm_test.py
  ```