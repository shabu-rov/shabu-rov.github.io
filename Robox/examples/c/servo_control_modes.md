# Пример работы с сервоприводом. Работа в различных режимах управления двигателем.
```c++
// Включение библиотек для работы с сервоприводом
// Библиотека для работы с сервоприводом
#include "Servo.h"

// Библиотека для взаимодействия с последовательным портом
#include "bus_handler.h"

// Адрес сервопривода. По умолчанию 10.
int servo_addr = 10;

int main()
{
  // Инициализация последовательного порта для работы с сервоприводом.
  // Вывод отладочной информации отключен.
  // По умолчанию для ubuntu - /dev/RS_485
  if (init_port("/dev/RS_485",false) < 0)
  {
    return -1;
  }

  // Инициализация сервопривода
  init_servo(servo_addr);

  // Стандартный режим работы сервопривода
  // enum PID_mode {
  //   NORMAL,
  //   PWM,
  //   SPEED
  // };
  printf("Normal mode: \n");  
  set_PID_mode(servo_addr,NORMAL);

  // Включение питания обмоток двигателя
  set_torque(servo_addr,true);

  // Перемещение на позицию 4000
  set_point(servo_addr,4000);

  sleep(4);

  // Выключение питания обмоток двигателя
  set_torque(servo_addr,false);



  printf("Only speed PID mode: \n");  
  // Режим ПИД по скорости
  set_PID_mode(servo_addr,SPEED);

  set_torque(servo_addr,true);

  // Скорость вращения вала 10 об/сек
  set_point(servo_addr,10);

  sleep(4);  

  set_torque(servo_addr,false);

  printf("PWM mode: \n"); 
  // Прямой режим работы. Без ПИД-регуляторов
  set_PID_mode(servo_addr,PWM);
  set_torque(servo_addr,true);

  // Высталение ШИМ 750 из 1000. Скважность 75%
  set_point(servo_addr,750);
  sleep(4);  
  set_torque(servo_addr,false);

  // Включение стадартного режима работы
  set_PID_mode(servo_addr,NORMAL);
 
  return 0;
}
```