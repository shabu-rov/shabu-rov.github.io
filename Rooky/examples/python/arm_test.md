
# Пример прямой работы с Rooky.

<!-- <details style="font-size: 20px; margin-bottom:10px;">
	<summary style="font-size: 20px; color: #2030FF;">Запуск примера</summary>
	Текс спойлера
</details> -->

```python
# Импортируем необходимые библиотеки
# Библиотека для работы с Rooky
import Rooky

# Библиотека для работы с временными задержками
import time

# Создадим объект Rooky в соответствии с его типом: левая или правая
# '/dev/RS_485' - последовательный порт, для ubuntu по умолчанию - '/dev/RS_485'.
# 'right' - тип Rooky (left или right)
arm = Rooky.Rooky('/dev/RS_485','right')

while True:
	# Повернем сустав 1 на 30 градусов, максимальная скорость сервоприводов - 5 об/мин
	arm.move_joint('joint_1',5,30)

	# Получим данные от сервопривода
	print(arm.read_servos())

	# Задержка на 2 секунды
	time.sleep(2)

	# Вернем сустав в нулевое положение
	arm.move_joint('joint_1',5,0)

	# Задержка на 2 секунды
	time.sleep(2)
```