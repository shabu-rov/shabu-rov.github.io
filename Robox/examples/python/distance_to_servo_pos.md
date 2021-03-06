# Пример отправки на сервопривод команд для перемещения в требуемую позицию.

```python
# Импортирование необходимых модулей
# Модуль для работы с сервоприводом
import Servo

# Модуль для работы с датчиком расстояния
import Ranger 

# Модуль для работы с таймерами и задержками
import time

# Модуль для работы с интерфейсной платой
import bus_handler

# Порт шины данных. 
# По умолчанию для ubuntu - /dev/RS_485
port        = '/dev/RS_485'

# Адрес сервопривода. По умолчанию 10
servo_id    = 10

# Адрес датчика расстояния. По умолчанию 1
sensor_id   = 1

# Инициализация шины передачи данных
master = bus_handler.Bus(port = port, baudrate = 460800, debug = False, timeout = 1.0)


# Соотношение расстояния к перемещению сервопривода
distance_to_pos_scale = 100

# Инициализация сервопривода
servo = Servo.Servo(servo_id, master.bus)

# Инициализация датчика расстояния
sensor = Ranger.Sensor(sensor_id, master.bus)

# Включение питания обмоток мотора
servo.set_torque(1)

if __name__ == '__main__':
    while(True):  
        # Отправка команды для измерения раастояния
        sensor.trig_sensor()

        # Задержка перед получением данных о расстоянии. 
        # Ожидание прохождения звука от излучателя и обратно. 
        # Здесь установлено время с запасом. 
        # Расчет времени = (макс.дист. / скорость звука) * 2 таким образом (2.5 / 343)*2 = 0.014
        time.sleep(0.05)

        # Чтение полученных данных о расстоянии
        sensor_data = sensor.read_sensor()

        # Чтение данных с сервопривода
        vals = servo.get_data()

        # Вывод полученных данных
        print('Data from servo: {0}'.format(servo_id))
        print('------------')
        for i in vals:
            print('{0} : {1}'.format(i, vals[i]))    

        # Движение на позицию       
        servo.set_point(sensor_data["US_distance"] * distance_to_pos_scale) 
```