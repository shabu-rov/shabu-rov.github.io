# Установка и запуск TestDevices на Ubuntu 16.04
## Установка
#### Вариант №1, рекомендуемый (использование ppa):
* Открыть терминал (**Ctrl + Alt + T**)
* Добавить в систему ppa репозиторий (если не добавлен) командой:
  ```sh
  curl -s --compressed "https://Promobot-education.github.io/ppa/KEY.gpg" | sudo apt-key add -
  sudo curl -s -o /etc/apt/sources.list.d/promobot-education.list "https://Promobot-education.github.io/ppa/promobot-education.list"
  ```
* Установить пакет:
  ```sh
  sudo apt update
  sudo apt install promobot-test-devices
  ```

#### Вариант №2:
* Вручную скачать **deb** пакет из последнего [релиза](https://github.com/Promobot-education/TestDevices/releases)
* Открыть пакет с помощью **"Установка приложений"**

или установить пакет с помощью команды: 

* Открыть директорию с **deb** пакетом
* Нажать правую кнопку мыши -> **Открыть терминал**
* Ввести команду:
```
sudo apt install ./promobot-test-devices<...>.deb
```

## Запуск
* Запустить TestDevices из приложений Ubuntu

или командой
* Открыть терминал (**Ctrl + Alt + T**)
* Написать команду
  ```sh
  /opt/promobot/TestDevices/TestDevices
  ```

## Обновление
* Следовать [инструкции](https://github.com/Promobot-education/ppa/wiki) по обновлению из ppa репозитория