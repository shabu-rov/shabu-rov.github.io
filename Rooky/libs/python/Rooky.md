# Библиотека для прмяой работы с Rooky.

```python
class Rooky():
	""" Класс для работы с манипулятором.

	Args:
		* port (str): имя посдеовательного порта манипулятора.
		* side (str): Типа манипулятора. Левый или правый.
		* debug (bool): Вывод отладочной информации в консоль.
	
	"""


	def __init__(self, port, side = "left", debug = False)


	def move_joint(self, joint_name, speed = 10, position = 0):
		""" Перемещение сустава в желаемую позицию.

		Args:
			* joint_name (str):имя сустава.
			* speed (int): Скорость перемещения сустава.
			* position (int): Желаемая позиция сустава в градусах.
		
		"""


	def relax(self, state):
		""" Полностью отключить питание двигателей всех суставов (включая тормоз).

		Args:
			* state (bool):True - отключить питание. False - включить питание.
		
		"""


	def read_servos(self):
		""" Получить данные с сервоприводов

		Args:
			* None
		
		"""

	def read_touch(self):
		"""Чтение данных с датчиков касания

        Args:
            None
        Returns:
            * Словарь с ключами:
                | "Touch_1"
                | "Touch_2"

        Raises:
            None

        """


	def is_touched(self):
		"""Есть ли факт касания датчика касания

        Args:
            None
        Returns: True - есть касание датчика
				 False - нет касания датчика

        """
```