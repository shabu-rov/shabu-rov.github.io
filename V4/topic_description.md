# Работа с основными топиками робота
## Общая информация

Получить информацию о топике:

`$ rostopic info <имя топика>`

Получить информацию о типе сообщения:

`$ rosmsg show <тип сообщения>`


## Управление передвижением робота

### Данные с колес  wheel
Топик выводит информацию о данных с колес робота.

Данные с топика:

```python
rostopic echo /wheel/left/sensors/core  #левое колесо
rostopic echo /wheel/right/sensors/core  #правое колесо
#полученные данные
header:
  seq: 40816  #кол-во итераций опроса с момента запуска
  stamp:  #текущее время
    secs: 1619435012
    nsecs: 708189702
  frame_id: ''  #идентификатор топика (отсутствует)
state:
  voltage_input: 28.1  #напряжение на входе
  temperature_pcb: 0.0  #температура платы управления колесом
  current_motor: 0.0  #ток на моторе
  current_input: 0.0  #ток на плате управления колесом
  speed: 0.0  #скорость
  duty_cycle: 0.0  #параметр платы управления колесом
  charge_drawn: 10.0  #параметр платы управления колесом
  charge_regen: 0.0  #параметр платы управления колесом
  energy_drawn: 299.0  #параметр платы управления колесом
  energy_regen: 0.0  #параметр платы управления колесом
  displacement: 1814.0  #смещение относительно место включения робота
  distance_traveled: 4745.0  #пройденное расстояние
  fault_code: 0  #код ошибки
---
```

### **Топик /twist**
_Тип_ [geometry_msgs/Twist]

Данный топик позволяет управлять передвижением робота в пространстве. В данный топик публикуются сообщения с типом geometry_msgs/Twist которые имеют следующую структуру:

```python
geometry_msgs/Vector3 linear
  float64 x # линейная скорость робота указывается в м/с
  float64 y
  float64 z

geometry_msgs/Vector3 angular
  float64 x
  float64 y
  float64 z # угловая скорость робота указывается в рад/с
```

Примечание:
- При задании отрицательной угловой скорости робот будет двигаться по часовой стрелке, если смотреть на робота сверху.
- Сообщения в топик должны приходить с частотой не менее 10 Hz.

Пример:
```python
rostopic pub /twist geometry_msgs/Twist "linear:
  x: 0.0
angular:
  z: -0.5" -r 10
```

_Результат:_ После запуска данной команды, робот начнет крутиться вокруг своей оси по часовой стрелке, со скоростью 0.5 рад/с

### Режим езды drive: 
Топик выводит информацию о режиме езды, паузе, радиусе движения. Через топик можно отправить робота на зарядную станцию.

Данные с топика:

```python
rostopic echo /drive/mode
#полученные данные
data: 0 #режим джойстика
---
data: 1 #режим авто
---
 
rostopic echo /drive/radius
#полученные данные
data: 5 #радиус в метрах
---
 
rostopic echo /drive/pause
#полученные данные
data: False #робот собирается поехать / едет
---
data: True #робот на паузе
---
 
rostopic echo /drive/station
#полученные данные
data: True #робот едет на зарядную станцию
---
data: False #робот не пытается ехать на зарядную станцию
---
 
rostopic echo /drive/status
#полученные данные
data: X
---
X - статусы:
0 - ожидание
1 - начало движения
2 - конец движения
3 - отмена
4 - препятствие
5 - робот не может повернуться
6 - робот вне радиусе движения
7 - модуль завершил свою работу по таймауту
8 - модуль завершил свою работу с ошибкой
9 - модуль успешно завершил свою работу
```
**Публикация данных в топик:**

```python
rostopic pub /drive/mode std_msgs/UInt16 "data: 0" -1 #активировать режим джойстик
 
 
rostopic pub /drive/mode std_msgs/UInt16 "data: 1" -1 #активировать режим авто
 
 
rostopic pub /drive/mode/switch std_msgs/Empty "{}" -1 #переключить режим
 
 
rostopic pub /drive/radius std_msgs/UInt8 "data: X" -1 #задать радиус (в метрах)
 
 
rostopic pub /drive/station std_msgs/Bool "data: true" -1 #включить алгоритм поиска зарядной станции
 
 
rostopic pub /drive/station std_msgs/Bool "data: false" -1 #отключить алгоритм поиска зарядной станции
 
 
rostopic pub /drive/pause std_msgs/Bool "data: false" -1 #снять робота с паузы
 
 
rostopic pub /drive/pause std_msgs/Bool "data: true" -1 #поставить робота на паузу
 
 
rostopic pub /drive/point std_msgs/UInt16 "data: X" -1 #отправить робота на точку X (int) (используется в навигации)

```

## Управление сервоприводами робота

### Просмотр версии прошивки с плат управления узлами робота
Параметр выводит информацию о версии прошивок:

* всех плат управления двигателями
* платы питания
* платы лица
* платы ушей робота

```python 
rosparam get /main_controller/firmwares 

#полученные данные
['Servo 31: 56', 'Servo 32: 56', 'Servo 33: 56', 'Servo 34: 56', 'Servo 35: 56', 'Servo
    36: 13', 'Servo 21: 56', 'Servo 22: 56', 'Servo 23: 56', 'Servo 24: 56', 'Servo
    25: 56', 'Servo 26: 13', 'Servo 11: 56', 'Servo 12: 56', 'Servo 13: 56', 'Servo
    41: 56', 'Servo 42: 56', 'Power_board: 229', 'Ear_left: 7', 'Ear_right: 7', 'Face_board:
    10001']
'Servo XX: XX' - версия прошивки плат управления двигателем робота
'Power_board: XXX' - версия прошивки платы питания робота
'Ear_left: X' - версия прошивки платы уха робота
'Face_board: XXXXX' - версия прошивки лица робота

```

### Статусы калибровки сервоприводов
Топик выводит информацию о текущем статусе калибровки.

Данные с топика:
```python 
rostopic echo /promobot_servos/calibration_step
#полученные данные
data: X
---
X - статусы:
0 - сброс текущей позиции в 0
1 - активация питания мотора на сервоприводах
2 - старт движения всех узлов до срабатывания датчика холла (ограничителя движения)
3 - возвращение сервоприводов в калибровочное значение
4 - сброс текущей позиции в 0
5 - отключение датчиков холла
6 - активация питания мотора на сервоприводах
```

### **Топик /left_arm_controller/command**
_Тип_ [trajectory_msgs/JointTrajectory]

Данный топик позволяет управлять контроллером положения левой руки.

В контроллер левой руки входят суставы:  left_arm_1_joint, left_arm_2_joint, left_arm_3_joint, left_arm_4_joint, left_arm_5_joint,  left_arm_6_joint, left_arm_7_joint.

В данный топик публикуются сообщения с типом trajectory_msgs/JointTrajectory которые имеют следующую структуру:

```python
[std_msgs/Header] header # http://docs.ros.org/api/std_msgs/html/msg/Header.html
  uint32 seq
  time stamp # время должно быть синхронно с временем ros
  string frame_id # не используется
string[] joint_names # массив имен джойнов которым будет подаваться задание для управления.
trajectory_msgs/JointTrajectoryPoint[] points # точки траектории в которой находятся позиции, скорости, ускорения и сила (так как контроллер для управления рук работает в режиме управления позицией, то нужно указывать только позиции для каждого джойнта). если тип джойнта revolute или continuous положение задается в радианах. если тип джойнта prismatic положение задается в метрах.
  float64[] positions # массив позиций каждого джойнта размерность массива и порядок этих позиций должны совпадать с размерностью и порядком джойнтов в массиве joint_names.
  float64[] velocities
  float64[] accelerations
  float64[] effort
  duration time_from_start # время завершения команды. контролер рассчитает траекторию от текущего положения джойнтов до желаемого за время t(i) - t(i-1).

```

Пример:
```python
rostopic pub /left_arm_controller/command trajectory_msgs/JointTrajectory "header: auto
joint_names:
- 'left_arm_4_joint'
points:
- positions: [1.57]
  time_from_start: {secs: 1, nsecs: 0}
- positions: [0.0]
  time_from_start: {secs: 6, nsecs: 0}" -1
```

_Результат:_
После запуска данной команды, робот согнет левый локтевой сустав, в течении 1ой секунды, на 90 градусов.
Затем, в течении 6ти секунд вернет локтевой сустав обратно в положение 0 градусов.

### **Топик /right_arm_controller/command**
_Тип_ [trajectory_msgs/JointTrajectory]

Данный топик позволяет управлять контроллером положения правой руки. В контроллер правой руки входят суставы:  right_arm_1_joint, right_arm_2_joint, right_arm_3_joint, right_arm_4_joint, right_arm_5_joint,  right_arm_6_joint, right_arm_7_joint.

Описание аналогично с /left_arm_controller/command

### **Топик /head_controller/command**
_Тип_ [trajectory_msgs/JointTrajectory]

Данный топик позволяет управлять контроллером положения головы. В контроллер головы входят суставы:  head_1_joint, head_2_joint.

Расположение джойнтов и направления движений:
head_1_joint: подъем головы вверх, вниз. значения > 0 - вверх, значения < 0 - вниз.

head_2_joint: поворот головы по и против часовой стрелки. значения > 0 - по часовой, значения < 0 - против часовой. (если смотреть на робота сверху)

Описание аналогично с /left_arm_controller/command

### **Топик /torso_controller/command**
_Тип_ [trajectory_msgs/JointTrajectory]

Данный топик позволяет управлять контроллером положения торса. В контроллер торса входят суставы:  torso_1_joint, torso_2_joint, torso_3_joint.

Расположение джойнтов и направления движений:
torso_1_joint: наклон торса вперед, назад. значения > 0 - наклон назад, значения < 0 - наклон вперед.

torso_2_joint: наклон торса влево, вправо. значения > 0 - наклон вправо, значения < 0 - наклон влево.

torso_3_joint: подъем торса вверх, вниз. 0 - нижнее положение, значения > 0 подъем торса вверх

Описание аналогично с /left_arm_controller/command

## Получения данных с датчиков робота

### **Датчики препятствий**
_Тип_ [promobot_msgs/Ranges3s]

Топик выводит значения с комбинированных сенсоров (us + tof). Значения указаны в см. Данный топик имеет тип сообщений promobot_msgs/Ranges3s (для робота версии 4), который имеет следующую структуру:

```python
uint8 s_1
uint8 s_2
uint8 s_3
uint8 s_4
uint8 s_5
uint8 s_6
uint8 s_7
uint8 s_8
uint8 s_9
uint8 s_10
uint8 s_11
uint8 s_12
uint8 s_13
uint8 s_14
uint8 s_15
uint8 s_16
uint8 s_66
```
Максимальное значение у каждого датчика 255 см, минимальное 25 см



### **Топик  /rangesTOF**
_Тип_ [promobot_msgs/Ranges3s]

Топик выводит значения только с tof сенсоров. Значения указаны в см. Данный топик имеет тип сообщений promobot_msgs/Ranges3s (для робота версии 4)

Максимальное значение у каждого датчика 255 см, минимальное 5 см

Описание аналогично с /ranges

### **Топик  /rangesUS**
_Тип_ [promobot_msgs/Ranges3s]

Топик выводит значения только с ультразвуковых сенсоров. Значения указаны в см. Данный топик имеет тип сообщений promobot_msgs/Ranges3s (для робота версии 4)

Максимальное значение у каждого датчика 255 см, минимальное 5 см

Описание аналогично с /ranges


### **Топик /camera/depth/image_raw**
_Тип_ [sensor_msgs/Image]

Топик выводит карту глубины  с датчика RealSense. Данный топик имеет тип сообщений sensor_msgs/Image, который имеет следующую структуру:
```python
# This message contains an uncompressed image
# (0, 0) is at top-left corner of image
#

Header header # Header timestamp should be acquisition time of image
 # Header frame_id should be optical frame of camera
 # origin of frame should be optical center of cameara
 # +x should point to the right in the image
 # +y should point down in the image
 # +z should point into to plane of the image
 # If the frame_id here and the frame_id of the CameraInfo
 # message associated with the image conflict
 # the behavior is undefined
 
uint32 height # image height, that is, number of rows
uint32 width # image width, that is, number of columns
 
# The legal values for encoding are in file src/image_encodings.cpp
# If you want to standardize a new string format, join
# ros-users@lists.sourceforge.net and send an email proposing a new encoding.
 
string encoding # Encoding of pixels -- channel meaning, ordering, size
 # taken from the list of strings in include/sensor_msgs/image_encodings.h
 
uint8 is_bigendian # is this data bigendian?
uint32 step # Full row length in bytes
uint8[] data # actual matrix data, size is (step * rows)
```

### **Топик /depthcamera/ranges**
_Тип_ [promobot_msgs/RealSenseRanges]

Топик выводит показания  с датчика RealSense, топик формируется из карты глубины, для определения расстояния, карта глубины делится на сектора. Значения указаны в см. Данный топик имеет тип сообщений promobot_msgs/RealSenseRanges, который имеет следующую структуру:
```python
uint8 s_all #минимальное расстояние по всему кадру
uint8 s_l #минимальное расстояние по 1 колонке (левая)
uint8 s_m #минимальное расстояние по 2 колонке (средняя)
uint8 s_r #минимальное расстояние по 3 колонке (правая)
uint8 s_1 #минимальное расстояние по 1 строке (верхняя)
uint8 s_2 #минимальное расстояние по 2 строке
uint8 s_3 #минимальное расстояние по 3 строке
uint8 s_4 #минимальное расстояние по 4 строке (нижняя)
uint8 s_1_1 #минимальное расстояние в секторе 1 1
uint8 s_1_2 #минимальное расстояние в секторе 1 2
uint8 s_1_3 #минимальное расстояние в секторе 1 3
uint8 s_2_1 #минимальное расстояние в секторе 2 1
uint8 s_2_2 #минимальное расстояние в секторе 2 2
uint8 s_2_3 #минимальное расстояние в секторе 2 3
uint8 s_3_1 #минимальное расстояние в секторе 3 1
uint8 s_3_2 #минимальное расстояние в секторе 3 2
uint8 s_3_3 #минимальное расстояние в секторе 3 3
uint8 s_4_1 #минимальное расстояние в секторе 4 1
uint8 s_4_2 #минимальное расстояние в секторе 4 2
uint8 s_4_3 #минимальное расстояние в секторе 4 3
```

### **Топик /realsense/scan**
_Тип_ [sensor_msgs/LaserScan]

Топик выводит показания  с датчика RealSense в виде LaserScan, топик формируется из карты глубины с помощью пакета depthimage_to_laserscan . Данный топик имеет тип сообщений sensor_msgs/LaserScan, который имеет следующую структуру:
```python
# Single scan from a planar laser range-finder
#
# If you have another ranging device with different behavior (e.g. a sonar
# array), please find or create a different message, since applications
# will make fairly laser-specific assumptions about this data
 
Header header # timestamp in the header is the acquisition time of
 # the first ray in the scan.
 #
 # in frame frame_id, angles are measured around
 # the positive Z axis (counterclockwise, if Z is up)
 # with zero angle being forward along the x axis
  
float32 angle_min # start angle of the scan [rad]
float32 angle_max # end angle of the scan [rad]
float32 angle_increment # angular distance between measurements [rad]
 
float32 time_increment # time between measurements [seconds] - if your scanner
 # is moving, this will be used in interpolating position
 # of 3d points
float32 scan_time # time between scans [seconds]
 
float32 range_min # minimum range value [m]
float32 range_max # maximum range value [m]
 
float32[] ranges # range data [m] (Note: values < range_min or > range_max should be discarded)
float32[] intensities # intensity data [device-specific units]. If your
 # device does not provide intensities, please leave
 # the array empty.
```
### Статус зарядки charge: 
Топик выводит информацию статусе, типе зарядки. Через топик можно запустить приложение отправки на зарядную станцию.

Данные с топика:
```python
rostopic echo /charge/cur
#полученные данные
data: x #ток заряда (float)
---
 ```
```python
rostopic echo /charge/state
#полученные данные
data: True #робот заряжается
---
data: False #робот не на зарядке
---
 ```

```python
rostopic echo /charge/type
#полученные данные
data: 0 #не заряжается
---
data: 1 #заряжается по кабелю
---
data: 2 #заряжается через контакты зарядной станции
---
```

### Датчики прикосновений sens: 
Топик выводит информацию а срабатывании емкостного датчика в голове и ладонях робота. Через топик можно сымитировать прикосновение к роботу.

**Данные с топика:**
```python
rostopic echo /sens
#полученные данные
left_hand: False #емкостной датчик в левой ладони
right_hand: False #емкостной датчик в правой ладони
head_left: False #емкостной датчик в левом ухе
head_right: False #емкостной датчик в правом ухе
head_center: False #емкостной датчик в центре головы
```

_При срабатывании right_hand, left_hand в ладонях, робот начнет сгибать пальцы правой или левой руки соответственно_

_При срабатывании head_left, head_right, head_center в голове, уши робота загорятся желтым цветом_

**Публикация данных в топик:**
```python
rostopic pub /sens promobot_msgs/TouchSens "{left_hand: false, right_hand: false, head_left: false, head_right: false, head_center: false}" -1
```

#передача любому ключу значение true сымитирует прикосновение к датчику

## Распознавание речи asr: 
Топик выводит информацию о готовности робота распознавать, процесс распознавания и что распознал робот. Через топик можно отправить реплику роботу на распознавание.

**Данные с топика:**
```python
rostopic echo /asr
#полученные данные
data: True #если робот сейчас не произносит текст и готов слушать собеседника
---
data: False #если робот сейчас произносит текст и не может услышать собеседника
---

```
 
```python
rostopic echo /asr/result
#полученные данные
header:
  seq: 127 #кол-во итераций распознавания с момента запуска
  stamp: #время публикации в милисекундах
    secs: 1617172367
    nsecs: 814594122
  frame_id: "asr" #индентификатор asr
source: 0 #источник звука
uuid: "7d607d83-a98d-42cf-8e83-f0bcce857c91" #уникальный идентификатор
text: "hello" #распознанный текст
final: 1 #статус распознавания (1 - завершен, 0 - в процессе)
conf: 0.899999976158 #данные с google, коэфициент уверенности в распознавании
---
```

**Публикация данных в топик:**

```python
rostopic pub /asr std_msgs/Bool "data: true" -1 #включить распознавание речи
```
 
```python
rostopic pub /asr std_msgs/Bool "data: false" -1 #выключить распознавание речи
```
 
```python

rostopic pub /asr/result promobot_msgs/ASRResult "header:
  seq: 0
  stamp: {secs: 0, nsecs: 0}
  frame_id: ''
source: 0
uuid: 'cb2726de-91f2-11eb-a8b3-0242ac130003' #можно сгенерировать на https://www.uuidgenerator.net/version1
text: 'test' #что отправляем на распознавание
final: 1  #сообщаем сервису, что реплика завершена
conf: 1.0" #указываем коэфициент

```

### Произношение текста tts: 
Топик выводит информацию о реплике, которую робот произносит. Через топик можно отправить роботу реплику на произношение.

**Данные с топика:**
```python
rostopic echo /tts/process
#полученные данные
status: True #реплика сейчас произносится
uuid: "{460467e7-bdee-4b28-804b-fe35dbf296a1}" #уникальный идентификатор реплики
---
status: False #произношение реплики завершено
uuid: "{460467e7-bdee-4b28-804b-fe35dbf296a1}" #уникальный идентификатор реплики
---
 ```
```python
rostopic echo /tts/start
#полученные данные
text: "My name is Promobot" #текст, который робот произносит
terminate: True #может ли реплика быть прервана
uuid: "{9597cd61-8eb5-4dfc-a5c9-994492f5355a}" #уникальный идентификатор реплики
ignore_saving: False #данная логика используется в микрофонном массиве

```

**Публикация данных в топик:**
```python
rostopic pub /tts/cancel std_msgs/Empty "{}" -1 #отменяет произношение реплики
```
 
```python
rostopic pub /tts/start promobot_msgs/TTSCommand "text: 'test phrase' #отправка реплики на произношение
terminate: false
uuid: ''
ignore_saving: false"

```


### Уровень громкости volume: 
Топик выводит информацию об уровне громкости динамиков. Через топик можно выставить значение уровня громкости.

**Данные с топика:**

```python
rostopic echo /volume
#полученные данные
data: 81 #уровень громкости
---
```

**Публикация данных в топик:**
```python
rostopic pub /volume std_msgs/UInt16 "data: 30" -1 #установить уровень громкости 30
```

### Чувствительность микрофона mic: 
Топик выводит информацию о чувствительности микрофона. Через топик можно выставить значение чувствительности микрофона.

**Данные с топика:**
```python
rostopic echo /mic
#полученные данные
data: 81 #уровень чувствительности микрофона
---
```

**Публикация данных в топик:**
```python
pactl set-source-volume $PROMOBOT_SOURCE_DEFAULT 30%  #установить уровень чувствительности микрофона в 30%
```

### Публикация эмоций animation
**Публикация данных в топик:**
```python
rostopic pub /animation/file std_msgs/String "data: 'X'" # X - название gif файлов. Доступные gif файлы находятся в /opt/promobot/share/promobot_face_manager/images
```


### Проверка состояния красной кнопки
Красная кнопка находится в положении отключения серв и колес при выполнении двух условий:

```python
rostopic echo /main_board/voltages
#полученные данные
values:
  -
    name: "PC_win"
    value: 15.7399997711
  -
    name: "PC_linux"
    value: 15.7259998322
  -
    name: "router"
    value: 28.202999115
  -
    name: "printer_photo"
    value: 24.1870002747
  -
    name: "display"
    value: 11.9259996414
  -
    name: "printer_cheque"
    value: 24.1149997711
  -
    name: "servos"
    value: 0.0 #значение напряжение равно нулю
---
 
rostopic echo /wheel/left/sensors/core #в топики колес ничего не публикуется
```

### Статусы и ошибки чекового принтера

Топик выводит информацию о статусах и ошибках чекового принтера
```python

rostopic echo /printer_thermal/status
#полученные данные
data: X
---
X - статусы:
0 - Ожидание печати
1 - Находится в процессе печати
2 - Ошибка принтера
3 - Принтер не подключен
 
rostopic echo /printer_thermal/error
#полученные данные
code: X
description: "X"
---
X - код ошибки + описание:
NOT_ERROR = 0,
NO_PAPER = 1,
LOW_PAPER = 2,
PAPER_JAM = 3,
HEAD_OVERHEATED = 4,
POWER_SUPPLY = 5,
CUTTER_ERROR = 6,
RAM_ERROR = 7,
NOT_CONNECTED = 100

```