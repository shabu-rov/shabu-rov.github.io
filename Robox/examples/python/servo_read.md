# Пример подключения к сервоприводу и чтения с него данных.

```python
# Импорт необходимых модулей
# Модуль для работы с сервоприводом
import Servo

# Модуль для паузы между запросами информации от сервопривода
import time

# Модуль для работы с шиной передачи данных
import bus_handler


# Определение последовательного порта интерфейсного блока. 
# По умолчпнию для ubuntu - /dev/RS_485
port        = '/dev/RS_485'

# Адрес сервопривода. По умолчанию 10
servo_id    = 10

# Инициализация шины передачи данных
master = bus_handler.Bus(port = port, baudrate = 460800, debug = False, timeout = 1.0)

# Инициализация сервопривода. Создание объекта - сервопривода.
servo = Servo.Servo(servo_id, master.bus)

time.sleep(2)

if __name__ == '__main__':

    while(True):
        # Чтение данных с сервопривода. Функция возвращает словарь c ключами: 
        # - "ID"
        # - "Torque", 
        # - "Setpoint" 
        # - "Position" 
        # - "Speed" 
        # - "Command" 
        # - "Current" 
        # - "Pos_PID_P" 
        # - "Pos_PID_I" 
        # - "Pos_PID_D" 
        # - "Speed_PID_P" 
        # - "Speed_PID_I" 
        # - "Speed_PID_D" 
        # - "Errors"
        vals = servo.get_data()

        # Если есть данные, то делаим их вывод на экран
        if vals:
            # Вывод полученных данных
            print('Data from servo: {0}'.format(servo_id))
            print('------------')
            for i in vals:
                print('{0} : {1}'.format(i, vals[i]))
            time.sleep(0.05)
            print('\n' * 3)
```