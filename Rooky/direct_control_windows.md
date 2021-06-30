# Прямое управление Rooky на Windows
## Подготовка
* Установить [git](https://git-scm.com/download/win)
* Установить [Python 3.5.4](https://www.python.org/ftp/python/3.5.4/python-3.5.4-amd64.exe) (При установке поставить галочку **"Add Python 3.5 to PATH"**)
* **Создать и перейти** в папку где будут храниться клонированные репозитории (например: C:\git)
* Нажать **Shift + правая кнопка мыши**
* Выбрать **Открыть окно PowerShell здесь**
* Клонировать репозиторий Rooky командой:
```bash
git clone https://github.com/Promobot-education/Rooky.git
```
* Перейти в папку с установочным скриптом командой:
```bash
cd .\Rooky\python
```
* Запустить скрипт установки библиотек командой:
```bash
python.exe setup.py .\setup.py
```
* Установить [драйвера](/Rooky/res/drivers/CDM21228_Setup.exe) для интерфейсной платы
* **Настройка закончена**

## Запуск примеров Python

* Запустить программу **IDLE (Python 3.5)**(находится в меню Пуск)
* Открыть файл arm_test.py (**Ctrl + O**) из папки **Rooky\python\examples**
* Заменить порт на соответствующий порт подключенной интерфейсной платы, например: 
  
  ``arm = Rooky.Rooky('COM2','left')``
* Запустить модуль (**F5**)