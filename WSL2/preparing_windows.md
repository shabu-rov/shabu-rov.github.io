# Подготовка системы Windows 10 для работы с ROS
❗ Требуется **Windows 10**

Для полноценной и стабильной работы ROS требуется Ubuntu Linux 16.04.
В связи с этим, необходимо подготовить Windows к работе с ROS.

## Настройка подсистемы Linux

ℹ️ Команды выполняются в PowerShell от имени администратора
1. Нажать **Win + X**
2. Выбрать **PowerShell(админ)**
3. Ввести команды:
```PowerShell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```
```PowerShell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

4. **Перезагрузить ПК**

5. Скачать и установить последнее обновление необходимых компонентов. [Ссылка](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

6. Сделать использование WSL2 по умолчанию (команда выполняется в PowerShell от имени администратора):
   * нажать **Win + X**
   * выбрать **PowerShell(админ)**
   * ввести команду:
   ```PowerShell 
   wsl --set-default-version 2
   ```
7. Скачать и установить (запустить если уже есть в системе) дистрибутив (200 MB) Ubuntu 16.04. [Ссылка](https://aka.ms/wsl-ubuntu-1604) 

8. Ввести желаемое имя пользователя и пароль для учетной записи WSL

9. Подсистема **Ubuntu Linux** готова к работе

   ![start](/WSL2/res/start.png)

## Подготовка для запуска графических приложений (X-сервер)
ℹ️ Для запуска в WSL любых приложений с графическим интерфейсом необходимо донастроить дополнительное ПО:

1. Скачать и установить на системе Windows ПО "[X-сервер](https://sourceforge.net/projects/vcxsrv/files/latest/download)"

2. В Windows запустить на рабочем столе ярлык XLaunch и выставить параметры как указано на изображениях ниже:

   ![step_1](/WSL2/res/step_1.png)

   ![step_2](/WSL2/res/step_2.png)

   ![step_3](/WSL2/res/step_3.png)

3. Сохранить конфигурацию на рабочий стол.

   ![step_4](/WSL2/res/step_4.png)

4. Нажать **Win + X**
5. Выбрать **PowerShell(админ)**
6. Ввести команды:
   ```PowerShell
   wsl
   echo "export LIBGL_ALWAYS_INDIRECT=0" >> ~/.bashrc 
   echo "export DISPLAY=\$(awk '/nameserver / {print \$2; exit}' /etc/resolv.conf 2>/dev/null):0" >> ~/.bashrc 
   echo "export HOST_ADDR=\$(awk '/nameserver / {print \$2; exit}' /etc/resolv.conf 2>/dev/null) " >> ~/.bashrc 
   ```

7. **Настройка закончена. Все окна можно закрыть**

ℹ️ После всех выполненных настроек подсистема Linux запускается одной командой в **PowerShell**:
```PowerShell
wsl
```
или в меню Пуск: **Пуск -> Ubuntu 16.04 LTS**

⚠️ Если X-сервер отсутствует в трее, перед запуском WSL необходимо запустить (двойной клик) сохраненную в п.3 конфигурацию. 

Запущенный X-сервер в трее Windows:

 ![tray](/WSL2/res/tray.png)

## Подготовка к работе с реальным устройством

По умолчанию WSL2 не позволяет подключаться к каким-либо устройствами по USB.

Для возможности работать с реальными устройствами по USB необходимо:

1. Подключить устройство (интерфейсный блок Robox или Rooky) к ПК

2. Установить [драйвера](/Rooky/res/drivers/CDM21228_Setup.exe) интерфейсной платы, если не установлены

3. [Настроить COM порт](/WSL2/com_setup)

3. Скачать архив [сервер (TCP <-> COM)](https://github.com/Promobot-education/WSL2/archive/refs/heads/main.zip)

4. Создать папку, если она отсутствует ``C:\Program Files (x86)\Promobot``

5. Распаковать скачанный архив в папку из **п.3**

6. Установить, если не установлен, [Python 3.5.4](https://www.python.org/ftp/python/3.5.4/python-3.5.4-amd64.exe) (При установке поставить галочку **"Add Python 3.5 to PATH"**)

7. Запустить Ubuntu Linux 16.04:
   * нажать **Win + X**
   * выбрать **PowerShell(админ)**
   * написать команду:
   ```sh
   wsl
   ```

8. Написать в Linux следующие команды:
```sh
sudo apt update
sudo apt install socat
```
9. **Настройка закончена. Все окна можно закрыть**