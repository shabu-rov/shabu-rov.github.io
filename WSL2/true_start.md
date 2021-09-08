# Правильный запуск WSL2 на Windows
## при работе с реальным устройством

ℹ️ Первоначально необходимо убедиться в правильных [настройках COM порта](/WSL2/com_setup)

ℹ️ Для корректной работы с реальным устройством, подключенным по USB необходимо всегда запускать две утилиты:

1. На стороне **Windows** запустить сервер:
  * нажать **Win + X**
  * выбрать **PowerShell (админ)**
  * подать команду:
    ```PowerShell
    python.exe 'C:\Program Files (x86)\Promobot\WSL2-main\utils\Server.py'
    ```
    > Если происходит ошибка на этапе import serial, необходимо подать команду в PowerShell:
    ```PowerShell
    pip install pyserial
    ```
  * свернуть окно PowerShell
2. На стороне **Linux** запустить клиент (в **новом** окне PowerShell)
  * запустить WSL командой:
  ```PowerShell
  wsl
  ```
  * подать команду:
  ```sh
  sudo socat -d -d pty,link=/dev/RS_485,raw,echo=0,perm=0666 tcp:$HOST_ADDR:5000
  ```
3. Оба запущенных окна можно **свернуть**, чтобы не мешались.

ℹ️ Не стоит забывать про [X-сервер](/WSL2/preparing_windows#запуск-x-сервера), он всегда должен быть запущен.

![tray](/WSL2/res/tray.png)