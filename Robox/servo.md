# Сервопривод

![servo](/Robox/res/servo.png)

Сервопривод является высокопроизводительным исполнительным механизмом, разработанным специально для нужд робототехники. Данный сервопривод может использоваться для создания подвижных механизмов повышенной сложности, например, роботов-манипуляторов, pan-tilt модулей и т.п.

| Основные характеристики сервопривода:                                 	| 
|:------------- 						|----------------:					|
| Микроконтроллер           			| ARM CORTEX-M3 (72 [MHz], 32Bit)   | 
| Датчик положения     					| 14 бит AS5047       				| 
| Алгоритм контроля    					| 2-х контурное подчиненное ПИД-регулирование  | 
| Обратная связь    					| Положение, скорость, ток  | 
| Напряжение питания 					| 12 В       				    	| 
| Ном. потребление (без нагрузки) 		| 125 мА       				    	| 
| Ном. потребление (удержание) 			| 2.5 А       				    	| 
| Крутящий момент удержания (12 В) 		| 30.21 кг/см       				    | 
| Передаточное соотношение 				| 1:32       				   		| 
| Скорость холостого хода (12 В)		| 40 об./мин.       				| 


**Структура типового взаимодействия с сервоприводом:**

![motor_struct](/Robox/res/motor_struct.png)


**Структура регулятора сервопривода:**

![motor_control](/Robox/res/motor_control.png)


ℹ️ [Пример работы с сервоприводом (Python/C)](/Robox/servo_code)

## Описание регистров сервопривода

<div class="table-wrap">
    <table class="relative-table confluenceTable tablesorter tablesorter-default stickyTableHeaders"
        style="width: 100%; padding: 0px;" role="grid" resolved="">
        <colgroup>
            <col style="width: 6%;">
            <col style="width: 21%;">
            <col style="width: 60%;">
            <col style="width: 7%;">
            <col style="width: 6%;">
        </colgroup>
        <thead class="tableHeader">
            <tr role="row" class="headerRow">
                <th>
                    <div class="header">Номер</div>
                </th>
                <th>
                    <div class="header" style="text-align: center;">Название</div>
                </th>
                <th>
                    <div class="header">Описание</div>
                </th>
                <th >
                    <div class="header">Формат</div>
                </th>
                <th>
                    <div class="header">Чтение/запись</div>
                </th>
            </tr>
        </thead>
        <tbody aria-live="polite" aria-relevant="all">
            <tr role="row">
                <td colspan="1" style="text-align: center;">0</td>
                <td colspan="1" style="text-align: center;">Адрес modbus</td>
                <td colspan="1" style="text-align: center;"><br></td>
                <td colspan="1" style="text-align: center;">int</td>
                <td colspan="1" style="text-align: center;">R/W</td>
            </tr>
            <tr role="row">
                <td colspan="1" style="text-align: center;">1</td>
                <td colspan="1" style="text-align: center;">Скорость modbus</td>
                <td colspan="1">Табличная скорость порта делённая на 600</td>
                <td colspan="1" style="text-align: center;"><span>int</span></td>
                <td colspan="1" style="text-align: center;"><span>R/W</span></td>
            </tr>
            <tr role="row">
                <td colspan="1" style="text-align: center;">3</td>
                <td colspan="1" style="text-align: center;">Настроечный регистр</td>
                <td colspan="1"><a href="#описание-настроек-через-настроечный-регистр">Регистр отвечающий за настройки сервопривода</a></td>
                <td colspan="1" style="text-align: center;"><span>int</span></td>
                <td colspan="1" style="text-align: center;"><span>R/W</span></td>
            </tr>
            <tr role="row">
                <td colspan="1" style="text-align: center;">10</td>
                <td colspan="1" style="text-align: center;">Регистр PID Speed P</td>
                <td colspan="1">Настройка коэффициента P PID регулятора скорости</td>
                <td colspan="1" style="text-align: center;"><span>float</span></td>
                <td colspan="1" style="text-align: center;"><span>R/W</span></td>
            </tr>
            <tr role="row">
                <td colspan="1" style="text-align: center;">12</td>
                <td colspan="1" style="text-align: center;">Регистр PID Speed I</td>
                <td colspan="1">Настройка коэффициента I PID регулятора скорости</td>
                <td colspan="1" style="text-align: center;"><span>float</span></td>
                <td colspan="1" style="text-align: center;"><span>R/W</span></td>
            </tr>
            <tr role="row">
                <td colspan="1" style="text-align: center;">14</td>
                <td colspan="1" style="text-align: center;">Регистр PID Speed D</td>
                <td colspan="1">Настройка коэффициента D PID регулятора скорости</td>
                <td colspan="1" style="text-align: center;"><span>float</span></td>
                <td colspan="1" style="text-align: center;"><span>R/W</span></td>
            </tr>
            <tr role="row">
                <td colspan="1" style="text-align: center;">16</td>
                <td colspan="1" style="text-align: center;">Регистр PID Pos P</td>
                <td colspan="1">Настройка коэффициента P PID регулятора позиции</td>
                <td colspan="1" style="text-align: center;"><span>float</span></td>
                <td colspan="1" style="text-align: center;"><span>R/W</span></td>
            </tr>
            <tr role="row">
                <td colspan="1" style="text-align: center;">18</td>
                <td colspan="1" style="text-align: center;">Регистр PID Pos I</td>
                <td colspan="1">Настройка коэффициента I PID регулятора позиции</td>
                <td colspan="1" style="text-align: center;"><span>float</span></td>
                <td colspan="1" style="text-align: center;"><span>R/W</span></td>
            </tr>
            <tr role="row">
                <td colspan="1" style="text-align: center;">20</td>
                <td colspan="1" style="text-align: center;">Регистр PID Pos D</td>
                <td colspan="1">Настройка коэффициента D PID регулятора позиции</td>
                <td colspan="1" style="text-align: center;"><span>float</span></td>
                <td colspan="1" style="text-align: center;"><span>R/W</span></td>
            </tr>
            <tr role="row">
                <td colspan="1" style="text-align: center;">22</td>
                <td colspan="1" style="text-align: center;">Speed limit</td>
                <td colspan="1">Предельное значение скорости вращения вала в об/мин</td>
                <td colspan="1" style="text-align: center;"><span>float</span></td>
                <td colspan="1" style="text-align: center;"><span>R/W</span></td>
            </tr>
            <tr role="row">
                <td colspan="1" style="text-align: center;">40</td>
                <td colspan="1" style="text-align: center;">Регистр команд</td>
                <td colspan="1"><a href="#описание-команд-управления-сервоприводом">Команды управления сервоприводом</a></td>
                <td colspan="1" style="text-align: center;"><span>int (</span>hex)</td>
                <td colspan="1" style="text-align: center;"><span>R/W</span></td>
            </tr>
            <tr role="row">
                <td colspan="1" style="text-align: center;">41</td>
                <td colspan="1" style="text-align: center;">Включение питания (torque)</td>
                <td colspan="1">Включения питания сервовприводов</td>
                <td colspan="1" style="text-align: center;"><span>int</span></td>
                <td colspan="1" style="text-align: center;"><span>R/W</span></td>
            </tr>
            <tr role="row">
                <td colspan="1" style="text-align: center;">42</td>
                <td colspan="1" style="text-align: center;">"Установка задачи"</td>
                <td colspan="1">В зависимости от настройки ПИД регуляторов пишется задача для регулятора или просто ШИМ (0-1000)</td>
                <td colspan="1" style="text-align: center;"><span>int</span></td>
                <td colspan="1" style="text-align: center;"><span>R/W</span></td>
            </tr>
            <tr role="row">
                <td colspan="1" style="text-align: center;">45</td>
                <td colspan="1" style="text-align: center;">Регистр ошибок</td>
                <td colspan="1"><a href="#описание-ошибок">Текущий статус сервопривода (ошибки)</a></td>
                <td colspan="1" style="text-align: center;"><span>int</span></td>
                <td colspan="1" style="text-align: center;">R</td>
            </tr>
            <tr role="row">
                <td colspan="1" style="text-align: center;">47</td>
                <td colspan="1" style="text-align: center;">Позиция сервопривода</td>
                <td colspan="1">Текущее положение сервопривода, ticks</td>
                <td colspan="1" style="text-align: center;"><span>int</span></td>
                <td colspan="1" style="text-align: center;">R</td>
            </tr>
            <tr role="row">
                <td colspan="1" style="text-align: center;">48</td>
                <td colspan="1" style="text-align: center;">Скорость сервопривода</td>
                <td colspan="1">Скорость вращения вала сервопривода, об/мин</td>
                <td colspan="1" style="text-align: center;"><span>int</span></td>
                <td colspan="1" style="text-align: center;">R</td>
            </tr>
            <tr role="row">
                <td colspan="1" style="text-align: center;">49</td>
                <td colspan="1" style="text-align: center;">Ток сервопривода</td>
                <td colspan="1">Текущий потребляемый сервоприводом ток, мА</td>
                <td colspan="1" style="text-align: center;"><span>int</span></td>
                <td colspan="1" style="text-align: center;">R</td>
            </tr>
        </tbody>
    </table>
</div>

## Описание настроек через настроечный регистр
Каждый бит регистра «Управление настройками» (4) отвечает за определенный функционал платы:
Индекс бита(начиная с 0):

    0 - Не используется
    1 - Включение выключение пида по скорости
    2 - Включение выключение пида по положению


## Описание команд управления сервоприводом

Список возможных команд для записи в Регистр команд (41):

1 - «0xDEAD» команда перезагрузки платы.

2 - «0xAAAA» полностью размыкает обмотки от платы, по умолчанию, когда torque в нуле (регистр 41 = 0) обмотки замкнуты друг на друга для торможения.

3 - «0xACDC» разрешает запись в ЕЕПРОМ единично, после записи одного из регистров сбрасывается.

## Описание ошибок
Каждый бит регистра «Регистр ошибок» (45) отвечает за индикацию определенной ошибки:

    0 - Ошибка связи.
    1 - Отсутствие платы с датчиками холлов. Не подключена плата.

    2 - Ошибка полярности двигателя, если ШИМ положительный, а скорость отрицательная, то выводится ошибка. 
        ПИД регуляторы при неправильной полярности работают не корректно.

    3 - Ошибка по току. Появляется при превышении тока.

    4 - Ошибка магнита. Появляется при неправильном зазоре (положении) магнита относительно датчика положения.

    5 - Обрыв связи с датчиком AS5047 по SPI. 
        Может появляться при отсутствии платы внешнего датчика положения или при поломке платы.

    6 - Ошибка DRV8302 fault. Появляется когда на пине драйвера управления двигателем ошибка. Пин fault в 0.

    7 - Бит причины выключения регистра «Разрешения работы двигателя» (42). 
        При выключении через регистр остается в 0, при выключении двигателя по ошибке устанавливается в 1. 
        При разрешении работы двигателя устанавливается в 0.

    8 - Бит необходим для контроля самопроизвольной перезагрузки устройства. 
        При разрешении работы двигателя устанавливается в 1 и сбрасывается только перезагрузкой устройства.