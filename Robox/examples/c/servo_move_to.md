# Пример работы с сервоприводом. Перемещение в требуемую позицию.
```c++
// Включение библиотек для работы с сервоприводом
// Библиотека для работы с сервоприводом
#include "Servo.h"

// Модуль для инициализации шины передачи данных
#include "bus_handler.h"

// Адрес сервопривода. По умолчанию 10.
int servo_addr = 10;

int main()
{
  // Инициализация последовательного порта для работы с сервоприводом. 
  // По умолчанию для ubuntu - /dev/RS_485
  if (init_port("/dev/RS_485",false) < 0)
  {
    return -1;
  }

  // Инициализация сервопривода
  init_servo(servo_addr);

  // Стандартный режим работы сервопривода
  set_PID_mode(servo_addr,NORMAL);

  // Включение питания обмоток двигателя
  set_torque(servo_addr,true);
  while (1) 
  {  
    // Перемещение на позицию 4000
    set_point(servo_addr,4000);
    sleep(4);

    set_point(servo_addr,0);
    sleep(4);

    set_point(servo_addr,-4000);
    sleep(4);   
  }   
  return 0; 
}
```