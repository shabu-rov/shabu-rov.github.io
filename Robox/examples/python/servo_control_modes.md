# Пример работы сервопривода в разных режимах.

* С каскадом ПИД регуляторов по сокрости и положению.

* Только с ПИД регулятором по скорости.

* Без регуляторов отпрвка ШИМ сигнала напрямую.

```python
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


if __name__ == '__main__':
    # С каскадом ПИД регуляторов по сокрости и положение.
    print("NORMAL mode")

    servo.set_PID_Mode("NORMAL")

    # Включение питания обмоток мотора
    servo.set_torque(1)

    # Движение в позицию 4000        
    servo.set_point(4000)
     
    time.sleep(4)


    # Только с ПИД регулятором по скорости.
    print("SPEED mode")
    servo.set_torque(0)                

    servo.set_PID_Mode("SPEED")

    servo.set_torque(1)

    # Установка оборотов вала в минуту
    servo.set_point(10)

    time.sleep(4)

    servo.set_torque(0)    


    # Без регуляторов, отправка ШИМ сигнала напрямую.
    print("PWM mode")
    servo.set_torque(0)                

    servo.set_PID_Mode("PWM")

    servo.set_torque(1)

    # Установка скважности ШИМ сигнала. (0-1000)
    servo.set_point(750)

    time.sleep(4)

    servo.set_torque(0)      


    # Выставление обычного режима работы           
    servo.set_PID_Mode("NORMAL")
```