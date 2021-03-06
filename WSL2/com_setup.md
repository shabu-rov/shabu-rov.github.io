# Настройка COM порта подключенной интерфейсной платы
## Общая информация
При подключении интерфейсной платы к компьютеру с ОС Windows появляется новое устройство. Это устройство определяется как последовательный порт (COM порт), его необходимо настроить.

ℹ️  В случае переподключения устройства, настройки порта могут не сохраниться и потребуется повторная настройка нового порта.

### Настройка COM порта:
1. Установить [драйвера](/Rooky/res/drivers/CDM21228_Setup.exe) интерфейсной платы, если не установлены
2. Нажать **Win + X**
3. Выбрать "Диспетчер устройств"
4. Найти группу **Порты (COM и LPT)**
5. Подключить устройство

   Отобразится **USB Serial Port (COM<..>)**

   ![com_group](/WSL2/res/com_group.png)

6. Открыть **"Свойства"** этого порта
7. Открыть вкладку **"Параметры порта"**
8. Выбрать **"Дополнительно"**

   ![com_settings](/WSL2/res/com_settings.png)

9. Изменить **Время ожидания** на **1мс**

   ![com_delay](/WSL2/res/com_delay.png)

10. Подтвердить настройки кнопкой **ОК**