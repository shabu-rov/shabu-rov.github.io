# Библиотека для работы с суставами Rooky.

```cpp
/**
 * Тип Rooky
 */
enum RookySide
{
	LEFT,    /**< Левая */
	RIGHT,   /**< Правая */
	NONE     /**< Не определено */
};

/**
 * Ининциализация и предварительные настройки перед работой с Rooky
 * @param port - строка с портом для подключения
 * @param side - тип Rooky (левая или правая)
 * @param debug - флаг на вывод отладочной информации
 * @return true - всё хорошо
 *         false - ошибка связи
 */
bool initRooky(std::string port, RookySide side = RookySide::NONE, bool debug =
false);

/**
 * Сдвинуть сустав на определнный угол с определенной скоростью
 * @param name - строка с именем сустава
 * @param speed - скорость сервоприводов об/мин.
 * @param position - угол в радианах, на который необходимо повернуть сустав.
 */
void moveJoint(const std::string &name, float speed = 10, float position = 0);

/**
 * Расслабить Rooky, отключает торможение сервоприводов,
 * кисть и пальцы ставит в изначальное положение.
 * Если была подана команда с флагом - true,
 * для работы необходимо послать команду с флагом - false.
 * @param flag
 */
void relax(bool flag);

/**
 * Считать состояние сервоприводов первого типа
 * @param servo_datas - вектор структур который будет заполнен данными,
 * 						или очищен при ошибке связи
 * @return true - все удачно
 *         false - ошибка связи
 */
bool readServos(std::vector<ServoData> &servo_datas);

/**
 * Считать состояние сервоприводов второго типа
 * @param data структура для заполнения
 * @return true - все удачно
 *         false - ошибка связи
 */
bool readPpmServo(PpmServoData &data);

/**
 * Получение данных о регистрации касания
 * @return true - есть касание датчика
 *         false - нет касания датчика
 */
bool isTouched();
```