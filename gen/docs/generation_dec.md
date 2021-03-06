{% include mathjax %}

## GenerationDec
	
### Призначення

Ця процедура заповнює матрицю із заданою кількістю рядків і стовпчиків випадковими десятковими числами із заданого діапазону. 

Діапазон значень фіксований для усіх елементів кожного стовпчика матриці. 

Елементи останнього стовпчика матриці не заповнюються випадковими числами і призначені для обчислення значень фітнес-функції, аргументами якої є всі попередні елементи рядка матриці.

### Вхідні параметри

- $$N, M$$ &mdash; цілі невід'ємні числа

- $$X_{\text{min}}(1..M), X_{\text{max}}(1..M)$$ &mdash; масиви дійсних чисел, $$X_{\text{min}}[i] < X_{\text{max}}[i]$$, $$i = \overline{1..M}$$;

### Вихідні параметри

- $$G(1..N, 1..M+1)$$ &mdash; матриця випадкових значень.

### Обчислення

Заповнює елементи матриці $$G[i,j]$$, $$i = \overline{1..N}$$, $$j = \overline{1..M}$$, $$X_{\text{min}}[j] \le G[i, j] \le X_{\text{max}}[j]$$.

### Вказівки

Для генерування випадкових чисел з заданого діапазону використовувати функцію Generate пакета Random Tools.

[Назад до лаби](../README.md)

[Назад на головну](../../README.md)