# Описание библиотек и примеров работы с Robox
В данном разделе дано описание для файлов с примерами кода, который использует прилагаемые библиотеки на языках C и Python.

ℹ️ [Описание библиотеки сервопривода на Python](/Robox/libs/python/servo_py)

ℹ️ [Описание библиотеки сервопривода на C](/Robox/libs/c/servo_c)

ℹ️ [Описание библиотеки датчика расстояния на языке "Python"](/Robox/libs/python/ranger_py)

ℹ️ [Описание библиотеки датчика расстояния на языке "C"](/Robox/libs/c/ranger_c)

## Примеры на языке Python
#### Датчик расстояния
* [ranger_read](/Robox/examples/python/ranger_read) - Цикличный опрос датчика расстояния.

#### Сервопривод
* [servo_read](/Robox/examples/python/servo_read) - Цикличное считывание данных с сервопривода.
* [servo_move_to](/Robox/examples/python/servo_move_to) - Цикличное движение сервоприводом в указанное положение.
* [servo_control_modes](/Robox/examples/python/servo_control_modes) - Переключение режимов сервопривода:
  * нормальный (движение в заданную позицию)
  * угловая скорость
  * ШИМ
* [distance_to_servo_pos](/Robox/examples/python/distance_to_servo_pos) - Передвижение сервоприводом в зависимости от значений с датчика расстояния.
* [servo_plot](/Robox/examples/python/servo_plot) - Построение графика желаемой позиции и реальной позиции вала во времени.

## Примеры на языке C
#### Датчик расстояния
* [ranger_read](/Robox/examples/c/ranger_read) - Цикличный опрос датчика расстояния.

#### Сервопривод
* [servo_move_to](/Robox/examples/c/servo_move_to) - Цикличное движение сервоприводом в указанное положение.
* [servo_read](/Robox/examples/c/servo_read) - Цикличное считывание данных с сервопривода.
* [servo_control_modes](/Robox/examples/c/servo_control_modes) - Переключение режимов сервопривода:
  * нормальный (движение в заданную позицию)
  * угловая скорость
  * ШИМ