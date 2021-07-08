# Пример отправки в сервопривод команд для перемещения в требуемую позицию.

```python
# Импортирование необходимых библиотек
# Библиотека для работы с сервоприводом
import Servo

# Библиотека для работы с таймерами и задержками
import time

# Библиотека для работы с интерфейсной платы
import bus_handler

# Порт шины данных. 
# По умолчпнию для ubuntu - /dev/RS_485
port        = '/dev/RS_485'

# Адрес сервопривода. По умолчанию 10
servo_id    = 10

# Инициализация шины передачи данных
master = bus_handler.Bus(port = port, baudrate = 460800, debug = False, timeout = 1.0)

# Инициализация сервопривода
servo = Servo.Servo(servo_id, master.bus)

# Включение питания обмоток мотора
servo.set_torque(1)

if __name__ == '__main__':
    while(True):
        # Движение в позицию 4000        
        servo.set_point(4000)

        # Ожидание перемещения мотора до требуемой позиции
        time.sleep(4)

        servo.set_point(0)
        time.sleep(4)

        servo.set_point(-4000)
        time.sleep(4)

        servo.set_point(0)
        time.sleep(4)   
```