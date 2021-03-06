Общие сведения о языке FBD
==========================

.. contents:: Содержание

**FBD (Function Block Diagram)** – это графический язык программирования
высокого уровня, обеспечивающий управление потока данных всех типов.
Позволяет использовать мощные алгоритмы простым вызовом функций и
функциональных блоков. Удовлетворяет непрерывным динамическим процессам.
Замечательно подходит для небольших приложений и удобен для реализации
сложных вещей подобно ПИД регуляторам, массивам и т. д. Данный язык
может использовать большую библиотеку блоков, описание которых приведено
в приложении 2. FBD заимствует символику булевой алгебры и, так как
булевы символы имеют входы и выходы, которые могут быть соединены между
собой, FBD является более эффективным для представления структурной
информации, чем язык релейно-контактных схем.

Основные понятия и конструкции языка
------------------------------------

Согласно IEC 61131­3, основными элементами языка FBD являются:
переменные, функции, функциональные блоки и соединения.

Переменные бывают входные, выходные и входные/выходные. На рис. 1
показаны: входная переменная – «in\_var», выходная переменная –
«out\_var» и входная/выходная переменная – «in\_out\_var».

|image1|

Рис. 1 – Изображение переменной в языке FBD

Графическое изображение функции приведено на рис. 2. С левой стороны
располагаются вхо­ды (IN1 и IN2), с правой стороны выходы (OUT).

|image2|

Рис. 2 – Изображение функции в языке FBD

Аналогично, изображение функционального блока, приведённое на рис. 3,
имеет с левой стороны вхо­ды (S1 и R), с правой стороны выход (Q1).

|image3|

Рис. 3 – Изображение функционального блока в языке FBD

Соответственно, переменные соединяются с входными и выходными
параметрами функций и функциональных блоков. Входные переменные могут
быть соединены только с входными параметрами функции или функционального
блока, выходные переменные – только с выходными параметрами функции или
функционального блока, входные/выходные переменные – как входами, так и
с выходами функции или функционального блока. Также выходной параметр
одной функции или функционального блока может быть напрямую соединён с
входным параметром другого.

|image4|

Рис. 4 – Пример соединения переменных, функций и функциональных блоков

Все функциональные блоки могут быть вызваны с дополнительными
(необязатель­ными) формальными параметрами: EN (входом) и ENO (выходом).
Пример такого функционального блока приведен на рис. 5.

|image5|

Рис. 5 – Изображение элементарного функционального блока с параметрами
EN/ENO

Если функциональный блок вызывается с параметрами EN/ENO и при этом
значе­ние EN равно нулю, то алгоритмы, определяемые в функциональном
блоке, не будут вы­полняться. В этом случае значение ENO автоматически
устанавлива­ется равным 0. Если же значение EN равно 1, то алгоритмы,
опреде­ляемые функциональным блоком, будут выполнены. После выполнения
этих алгоритмов без ошибок значение ENO автоматически устанавливается
равным 1. Если же возникает ошибка во время выполнения этих алгоритмов,
то значение ENO будет установлено равным 0. Поведение функционального
блока одинаково как в случае вызова функционального блока с EN = 1, так
и при вызове без параметров EN/ENO.

Для более компактного соединения входов и выходов различных функций и
функциональных блоков используются элементы «Соединение», показанные на
рис. 6:

|image6|

Рис. 6 – Изображение соединений в языке FBD

Они бывают двух видов: входное соединение и выходное выходные
соединение. Основная задача соединений – передать значение из одного
выхода на другой вход без прямого соединения выхода и входа. На рис. 5.7
показан пример, в котором выходное значение OUT функции BOOL\_TO\_INT
передаётся на вход IN2 функции ADD:

|image7|

Рис. 7 – Пример использования соединения на FBD диаграмме

Пример программы на языке FBD
-----------------------------

На рис. 8 приведена FBD диаграмма, состоящая из следующих
функциональных блоков: SR0, AND, TP0.

|image8|

Рис. 8 – пример FBD диаграммы

Функциональный блок SR0 представляет собой Бистабильный SR-триггер. У
него имеются входы S1, R1 и выход Q1, а так же дополнительный вход EN и
выход ENO, позволяющие включать и выключать выполнение SR0. Выход Q1 с
помощью соединён с входом IN1 блока AND, представляющий собой
«Логическое И». Вход IN2 типа BOOL соединён с литералом «BOOL#1»,
который всегда положительный. Выход OUT блока AND соединён с входом IN
функционального блока TP0, представляющий собой повторитель импульсов.
Вход PT типа TIME, соединён с литералом «T#5s», который задаёт значение
5 секунд.

Если после запуска выполнения данного функционального блока enabled
равно True и переменная S1\_IN тоже True, функциональный блок SR0
начинает выполняться. На выходе OUT функционального блока AND будет
значение True как только Q1 у SR0 будет равен True. Следовательно, как
только OUT становится True вход IN функционального блока TP0 принимает
тоже True и начинается отсчёт таймера ET (см. рис. 9).

|image9|

Рис. 9 – Выполнение FBD диаграммы

Пока данный таймер не достигнет значения PT выход Q у функционального
блока TP0 будет равен True. При достижении таймером ET значения PT, т.е.
через 5 секунд выход Q становится False (см. рис. 10).

|image10|

Рис. 10 – Выполнение FBD диаграммы

Как только вход IN функционального блока TP0 становится значения FALSE,
счётчик ET сбрасывается в T#0s.

.. |image1| image:: ./media/fbd/image1.png
   :width: 1.14722in
   :height: 1.10764in
.. |image2| image:: ./media/fbd/image2.png
   :width: 1.13056in
   :height: 0.84028in
.. |image3| image:: ./media/fbd/image3.png
   :width: 1.26875in
   :height: 1.05556in
.. |image4| image:: ./media/fbd/image4.png
   :width: 4.27847in
   :height: 1.11667in
.. |image5| image:: ./media/fbd/image5.png
   :width: 1.18264in
   :height: 0.95972in
.. |image6| image:: ./media/fbd/image6.png
   :width: 1.02500in
   :height: 0.77083in
.. |image7| image:: ./media/fbd/image7.png
   :width: 2.59097in
   :height: 1.86875in
.. |image8| image:: ./media/fbd/image8.png
   :width: 6.73194in
   :height: 1.61736in
.. |image9| image:: ./media/fbd/image9.png
   :width: 6.56458in
   :height: 1.59583in
.. |image10| image:: ./media/fbd/image10.png
   :width: 6.62083in
   :height: 1.62569in

