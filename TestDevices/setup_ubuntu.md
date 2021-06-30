# Установка и запуск TestDevices на Ubuntu 16.04
## Установка
#### Рекомендуемый Вариант №1 (использование ppa):
* Добавить в систему ppa репозиторий (если не добавлен)
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

  или установить пакет с помощью команды в **терминале из дирректории с deb пакетом**:
 
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