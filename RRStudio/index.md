# RRStudio
## Общая информация
![logo](/RRStudio/res/logo.png "Robox")

**RRStudio** - приложение для создания алгоритмов из блоков для взаимодействия с Promobot Rooky и Promobot Robox.

## Подготовка для работы RRStudio с Rooky
Для работы RRStudio с Rooky требуется серверное программное обеспечение и ROS. 

Серверное ПО может быть развернуто как на компьютере где находится RRStudio, так и на любом другом компьютере доступном в сети (необходимо знать IP адрес).

  ℹ️ [Развертывание серверного ПО на машине с Windows 10](/Rooky/rrs_control_windows)

  ℹ️ [Развертывание серверного ПО на машине с Ubuntu 16.04](/Rooky/rrs_control_ubuntu)

## Подготовка для работы RRStudio с Robox
Для работы RRStudio с Robox достаточно вручную установить:

* Для Windows [драйвера](/Robox/res/drivers/CDM21228_Setup.exe)
* Для Ubuntu [установка правил USB устройства](/Robox/setup_usb_rules).
  
  или

* Установить приложение для тестирования оборудования - [TestDevices](/TestDevices), которое, в том числе, автоматически устанавливает **драйвера** или **правила** в зависимости от системы.

## Установка и запуск RRStudio
  ℹ️ [Установка и запуск RRStudio на Ubuntu 16.04](/RRStudio/setup_ubuntu)

  ℹ️ [Установка и запуск RRStudio на Windows](/RRStudio/setup_windows)