Тесты «Объектный Фибоначчи» для разных языков.
==============================================

Подробнее об истории теста и старых результатах см. на
[Форумах Balancer'а](http://www.balancer.ru/tech/forum/2008/08/t63003--proizvoditelnost-yazykov-obektnyj-fibonachchi.html)

Что это такое
-------------

Большинство синтетических тестов различных языков, их реализаций и сред
исполнения ориентируются на «числодробительные» возможности. В то время, как
сегодня, при программировании широкого спектра задач, чаще требуется
высокая скорость работы с объектами и быстрое выделение и освобождение
памяти.

Для оценки языков по этим критериям и был в своё время сделан этот набор
тестов. Первой и весьма простой задачей, реализуемой на объектном представлении
мне в голову пришла такой своеобразный вариант вычисления чисел Фибоначчи.

```
class Fib:
	_value as uint

	def constructor(n as uint):
		_value = n

	def value() as uint:
		if(_value <= 2):
			return 1

		return Fib(_value - 1).value() + Fib(_value - 2).value()

print "Result = ", Fib(40).value()

```

Каждый объект содержит в себе свойство номера числа, которое записывается
при вызове конструктора. И метод, возвращающий значение. Который рекурсивно
создаёт ещё два объекта для предыдущих номеров и затем возвращает сумму
полученных значений. Получается множество итераций с созданием новых объектов,
доступом к свойствам, вызов методов… То, что и актуально в наше время для
весьма многих задач.

Предупреждаю сразу — эти тесты созданы ***не для того, чтобы считать Фибоначчи***.
Постоянно появляется очередной Кэп О., глубокомысленно заявляющий, что это
неоптимальный метод для вычисления чисел Фибоначчи. При чём, что характерно,
в качестве решения чаще предлагают рекурсивный же алгоритм, но без объектов.
Господа-товарищи, тест служит не для этого. А если уж хотите менять алгоритм,
то используйте не рекурсивный, а итеративный. Или с локальными переменными :)

В настоящее время тест переживает третью реинкарнацию. Первый вариант был
написан в 2008г. и результаты выкладывались на форуме. Второй, так толком
и не стартовал в 2009-м там же. И, вот, теперь набор тестов лежит в GitHub,
включая скрипты для запуска, с которыми проходило тестирование, а результаты
выкладываются в Wiki. Пока там — [только мои](https://github.com/Balancer/benchmarks-fib-obj/wiki/Результат-теста:-i3-2.2ГГц).

Тест будет понемногу пополняться, даже старые данные воспроизведены ещё не все.
И, конечно же, присоединяйтесь все желающие. Со своими тестама и результатами.

В будущем надо подумать над новой версией теста, включающей также наследование
и, опциональное, параллелизацию вычислений.
