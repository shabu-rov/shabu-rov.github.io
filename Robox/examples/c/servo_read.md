# Пример работы с сервоприводом. Цикличный опрос.
```c++
#include "Servo.h"
#include "bus_handler.h"

// Структура для записи данных с сервопривода
// struct servo_data {
//    int16_t ID;
//    bool torque;
//    int16_t setpoint;
//    int16_t position;
//    int16_t speed;
//    int16_t command;
//    int16_t current;
//    float   pos_PID_P;
//    float   pos_PID_I;
//    float   pos_PID_D;
//    float   speed_PID_P;
//    float   speed_PID_I;
//    float   speed_PID_D;   
//    char    *errors[9];    
// };
struct servo_data data;

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

  while (1) 
  {  
    // Чтение данных с сервопривода
    data = get_servo_data(servo_addr);

    // Вывод некоторых данных с сервопривода
    printf("Data from servo: \n");  
    printf("Position: %i\n",data.position);
    printf("Setpoint: %i\n",data.setpoint);
    printf("Motor current: %i mA \n\n",data.current);
    usleep(10000);
  }   
  return 0; 
}
```