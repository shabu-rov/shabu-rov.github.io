# Библиотека для работы с сервоприводами Rooky.

```cpp
/**
 * Режим работы сервопривода
 */
enum PID_mode
{
	NORMAL,	 /**< Нормальный - включены PID по скорости и положению */
	PWM, 	 /**< ШИМ режим - все PID выключены*/
	SPEED 	 /**< Режим по скорости. Включен только PID по скорости */
};

extern const char *errors_list[9];

/**
 * Разрешение движения сервопривода
 * @param addr - адрес modbus устройства
 * @param state - флаг включения/отключения движения
 * @return true - успешно
 *         false - ошибка связи
 */
bool set_torque(int addr, bool state);

/**
 * Задача цели в зависимости от режима может быть как:
 * - тики магнитного энкодера
 * - скорость, об/мин
 * - скважность ШИМ сигнала 0-1000
 * @param addr - адрес modbus устройства
 * @param setpoint - цель
 * @return true - успешно
 *         false - ошибка связи
 */
bool set_point(int addr, int16_t setpoint);

/**
 * Установить желаемый угол сервоприводу второго типа
 * @param addr - адрес modbus устройства
 * @param servoNum - номер сервопривода для управляющей платы (1 или 2)
 * @param angle - желаемый угол от -90 до 90
 * @return true - успешно
 *         false - ошибка связи
 */
bool set_ppm_angle(int addr, int servoNum, int16_t angle);

/**
 * Отправить команду в сервопривод
 * @param addr - адрес modbus устройства
 * @param command - команда hex
 * @return true - успешно
 *         false - ошибка связи
 */
bool set_command(int addr, int16_t command);

/**
 * Инициализация сервопривода первого типа
 * @param addr - адрес modbus устройства
 * @return true - успешно
 *         false - ошибка связи
 */
bool initServo(int addr);

/**
 * Инициализация сервопривода второго типа
 * @param addr - адрес modbus устройства
 * @param angle_1 - угол для сервопривода 1
 * @param angle_2 - угол для сервопривода 2
 * @return true - успешно
 *         false - ошибка связи
 */
bool initServoPpm(int addr, int angle_1, int angle_2);

/**
 * Установить режим работы PID
 * @param addr - адрес modbus устройства
 * @param mode - режим работы
 *               0 - Нормальный
 *               1 - ШИМ
 *               2 - Скорость
 * @return true - успешно
 *         false - ошибка связи
 */
bool set_PID_mode(int addr, int mode);

/**
 * Установить коэффициенты для PID контроллера по позиции
 * @param addr - адрес modbus устройства
 * @param value - коээфициент
 * @return true - успешно
 *         false - ошибка связи
 */
bool set_Pos_PID_P(int addr, float value);
bool set_Pos_PID_I(int addr, float value);
bool set_Pos_PID_D(int addr, float value);

/**
 * Установить коэффициенты для PID контроллера по скорости
 * @param addr - адрес modbus устройства
 * @param value - коэффициент
 * @return true - успешно
 *         false - ошибка связи
 */
bool set_Speed_PID_P(int addr, float value);
bool set_Speed_PID_I(int addr, float value);
bool set_Speed_PID_D(int addr, float value);

/**
 * Установить предельное значение скорости вращения сервопривода об/мин
 * @param addr - адрес modbus устройства
 * @param value - предельная скорость
 * @return true - успешно
 *         false - ошибка связи
 */
bool set_speed_limit(int addr, float value);

/**
 * Считать данные с сервопривода первого типа
 * @param addr - адрес modbus устройства
 * @param data - структура для заполнения данными
 * @return true - успешно
 *         false - ошибка связи
 */
bool get_servo_data(int addr, ServoData &data);

/**
 * Считать данные с сервопривода второго типа
 * @param addr - адрес modbus устройства
 * @param data - структура для заполнения данными
 * @return true - успешно
 *         false - ошибка связи
 */
bool get_ppm_servo_data(int addr, PpmServoData &data);

/**
 * Получить безразмерное значение от датчиков касания
 * @param addr - адрес modbus устройства
 * @param data - вектор с данными, который в случае успеха будет заполнен
 * @return true - успешно
 *         false - ошибка связи
 */
bool read_touch(int addr, std::vector<int> &data);
```