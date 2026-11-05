# Домашнее задание к работе 9

## Условие задачи

Создать программу с вложенными циклами и обработкой чисел: вывод таблиц умножения и геометрических узоров, всесторонний анализ 6-значного числа (подсчет цифр, суммирование, поиск произведений по условиям), а также построение «золотого» прямоугольника.

## Алгоритм и блок-схема

### Алгоритм

1. Начало
2. Функция `task_one_two_three`: использование вложенных циклов для вывода таблицы умножения 9х9, треугольной таблицы умножения и треугольной фигуры из единиц.
3. Функция `task_two`:
   - Ввод 6-значного числа с проверкой.
   - Разделение числа на отдельные цифры (`number1` — `number6`).
   - Выполнение серии расчетов по 12 подзадачам (подсчет цифр '3', четных цифр, суммы нечетных цифр, произведений, сравнение сумм половин числа и т.д.).
4. Функция `task_three`:
   - Ввод символа отрисовки и стороны `a`.
   - Вычисление второй стороны прямоугольника на основе коэффициента «золотого сечения» ($1.618$).
   - Отрисовка контура прямоугольника с помощью вложенных циклов.
5. Функция `main`: бесконечный цикл с возможностью выхода по клавише `n`.
6. Конец

### Блок-схема

```
[ Начало ]
    │
    ▼
[ Внешний цикл (строки) ]
    │
    ▼
[ Внутренний цикл (столбцы / разбор цифр числа) ]
    │
    ▼
[ Условия и вычисления (подсчет, суммы, отрисовка) ]
    │
    ▼
[ Вывод результатов ]
    │
    ▼
[ Конец ]
```

## Реализация программы

```c
#include <stdio.h>
#include <stdlib.h>
#include <locale.h>
#include <math.h>
#define ROW 9
#define COL 9
task_one_two_three();
task_two();
task_three();
void main() {
	while (1) {
		char a;
		setlocale(LC_ALL, "RUS");
		task_one_two_three();
		task_two();
		task_three();
		printf("Продолжить? (y/n): ");
		scanf_s(" %c", &a, 1);
		if (a == 'n') break;
	}
}
int task_one_two_three() {
	puts("TASK ONE1----------------------------------------------------------------------------------------------------------------");
	int row, col;
	printf("\n");
	for (row = 1; row <= ROW; ++row) {
		for (col = 1; col <= COL; col++) {
			printf("%5d", row * col);
		}
		printf("\n");
	}
	puts("TASK ONE2----------------------------------------------------------------------------------------------------------------");
	printf("\n");
	for (row = 1; row <= ROW; ++row) {
		for (col = 1; col <= row; col++) {
			printf("%5d", row * col);
		}
		printf("\n");
	}
	puts("TASK ONE3----------------------------------------------------------------------------------------------------------------");
	printf("\n");
	for (row = 1; row <= 5; row++) {
		for (col = row; col <= 5; col++) {
			printf("%5d", 1);
		}
		printf("\n");
	}
}
int task_two() {
	puts("TASK TWO----------------------------------------------------------------------------------------------------------------");
	int number, count = 0;
	int number1, number2, number3, number4, number5, number6;
	printf("Введите шестизначаное число:\n ");
	scanf_s("%d", &number);
	if (number < 100000 || number > 999999) {
		printf("Ошибка! Введите шестизначаное число:\n ");
		scanf_s("%d", &number);
	}
	puts("TASK TWO_1------");
	number1 = number / 100000;
	number2 = (number / 10000) % 10;
	number3 = (number / 1000) % 10;
	number4 = (number / 100) % 10;
	number5 = (number / 10) % 10;
	number6 = number % 10;
	if (number1 == 3) count++;
	if (number2 == 3) count++;
	if (number3 == 3) count++;
	if (number4 == 3) count++;
	if (number5 == 3) count++;
	if (number6 == 3) count++;
	printf("Количество цифр 3 в числе %d: %d\n", number, count);
	
	puts("TASK TWO_2------");
	count = 0;
	if (number6 == number1) count++;
	if (number6 == number2) count++;
	if (number6 == number3) count++;
	if (number6 == number4) count++;
	if (number6 == number5) count++;
	if (number6 == number6) count++;
	printf("Количество повторений последней цифры %d в числе %d: %d\n", number6, number, count);
	
	puts("TASK TWO_3------");
	count = 0;
	if (number1 % 2 == 0) count++;
	if (number2 % 2 == 0) count++;
	if (number3 % 2 == 0) count++;
	if (number4 % 2 == 0) count++;
	if (number5 % 2 == 0) count++;
	if (number6 % 2 == 0) count++;
	printf("Количество четных цифр в числе %d: %d\n", number, count);
	
	puts("TASK TWO_4------");
	count = 0;
	if (number1 > 5) count++;
	if (number2 > 5) count++;
	if (number3 > 5) count++;
	if (number4 > 5) count++;
	if (number5 > 5) count++;
	if (number6 > 5) count++;
	printf("Количество цифр больше 5 в числе %d: %d\n", number, count);
	
	puts("TASK TWO_5------");
	int sum = 0;
	if (number1 % 2 != 0) sum += number1;
	if (number2 % 2 != 0) sum += number2;
	if (number3 % 2 != 0) sum += number3;
	if (number4 % 2 != 0) sum += number4;
	if (number5 % 2 != 0) sum += number5;
	if (number6 % 2 != 0) sum += number6;
	printf("Сумма нечетных цифр в числе %d: %d\n", number, sum);
	
	puts("TASK TWO_6------");
	sum = 0;
	if (number1 >= 7) sum += number1;
	if (number2 >= 7) sum += number2;
	if (number3 >= 7) sum += number3;
	if (number4 >= 7) sum += number4;
	if (number5 >= 7) sum += number5;
	if (number6 >= 7) sum += number6;
	printf("Сумма цифр больше или равных 7 в числе %d: %d\n", number, sum);
	
	puts("TASK TWO_7------");
	int product = 1;
	if (number1 != 0) product *= number1;
	if (number2 != 0) product *= number2;
	if (number3 != 0) product *= number3;
	if (number4 != 0) product *= number4;
	if (number5 != 0) product *= number5;
	if (number6 != 0) product *= number6;
	printf("Произведение цифр числа %d, не равных нулю: %d\n", number, product);
	
	puts("TASK TWO_8------");
	product = number5 * number2;
	printf("Произведение второй и пятой цифры числа %d: %d\n", number, product);
	
	puts("TASK TWO_9------");
	sum = 0;
	if (number1 % 2 == 0) sum += number1;
	if (number2 % 2 == 0) sum += number2;
	if (number3 % 2 == 0) sum += number3;
	if (number4 % 2 == 0) sum += number4;
	if (number5 % 2 == 0) sum += number5;
	printf("Сумма четных цифр в числе %d исключая последнюю: %d\n", number, sum);
	
	puts("TASK TWO_10------");
	if (number1 == number2) printf("Цифры %d и %d расположены рядом и одинаковы\n", number1, number2);
	if (number2 == number3) printf("Цифры %d и %d расположены рядом и одинаковы\n", number2, number3);
	if (number3 == number4) printf("Цифры %d и %d расположены рядом и одинаковы\n", number3, number4);
	if (number4 == number5) printf("Цифры %d и %d расположены рядом и одинаковы\n", number4, number5);
	if (number5 == number6) printf("Цифры %d и %d расположены рядом и одинаковы\n", number5, number6);
	
	puts("TASK TWO_11------");
	int number123 = number1 + number2 + number3;
	int number456 = number4 + number5 + number6;
	if (number123 == number456) printf("Сумма первых трех цифр числа %d равна сумме последних трех\n", number);
	else printf("Сумма первых трех цифр числа %d не равна сумме последних трех\n", number);
	
	puts("TASK TWO_12------");
	int sum_odd = 0, sum_even = 0;
	if (number1 % 2 == 0) sum_even += number1; else sum_odd += number1;
	if (number2 % 2 == 0) sum_even += number2; else sum_odd += number2;
	if (number3 % 2 == 0) sum_even += number3; else sum_odd += number3;
	if (number4 % 2 == 0) sum_even += number4; else sum_odd += number4;
	if (number5 % 2 == 0) sum_even += number5; else sum_odd += number5;
	if (number6 % 2 == 0) sum_even += number6; else sum_odd += number6;
	int product1 = sum_odd * sum_even;
	printf("Произведение суммы четных и суммы нечетных цифр: %d\n", product1);
}
int task_three() {
	char symbol;
	int a, b;
	printf("Введите символ из которого будет строиться фигура:\n");
	scanf_s(" %c", &symbol);
	printf("Введите сторону:\n");
	scanf_s("%d", &a);
	b = (int)round(a * 1.618);
	puts("«Золотой» прямоугольник:");
	for (int i = 1; i <= a; i++) {
		for (int j = 1; j <= b; j++) {
			if (i == 1 || i == a || j == 1 || j == b) {
				printf("%c", symbol);
			}
			else {
				printf(" ");
			}
		}
		printf("\n");
	}
	return 0;
}
```

## Результаты работы программы

```text
TASK ONE1----------------------------------------------------------------------------------------------------------------
    1    2    3    4    5    6    7    8    9
    2    4    6    8   10   12   14   16   18
    3    6    9   12   15   18   21   24   27
    ...
TASK TWO----------------------------------------------------------------------------------------------------------------
Введите шестизначаное число:
 123456
Количество цифр 3 в числе 123456: 1
Сумма нечетных цифр в числе 123456: 9
```

## Информация о разработчике

Панарин Егор БИД-261
