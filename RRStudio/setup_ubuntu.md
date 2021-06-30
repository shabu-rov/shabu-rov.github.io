# Установка и запуск RRStudio на Ubuntu 16.04
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
  sudo apt install promobot-rrstudio
  ```

#### Вариант №2:
* вручную скачать **deb** пакет "[promobot-rrstudio](https://github.com/shabu-rov/RRStudio/releases)"
* открыть пакет с помощью **"Установка приложений"**

  или установить пакет с помощью команды в **терминале из дирректории с deb пакетом**:
 
  ```
  sudo apt install ./promobot-rrstudio<...>.deb
  ```

## Запуск
* Запустить RRStudio из приложений
* Выбрать устройство и подключиться **напрямую** или к **серверу по IP**

  если серверное ПО развернуто на этом же компьютере IP адресс: ``127.0.0.1``

## Обновление
* Следовать [инструкции](https://github.com/Promobot-education/ppa/wiki) по обновлению из ppa репозитория