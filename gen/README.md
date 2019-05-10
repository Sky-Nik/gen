{% include mathjax %}

## Опис алгоритму

Нехай є певна фітнес-функція $$f: \mathbb{R}^m \to \mathbb{R}$$ і ставиться оптимцізаційна задача

$$
f(x) \xrightarrow[x \in \mathcal{C}]{} \min,
$$

де $$\mathcal{C} \subset \mathbb{R}^m$$ &mdash; опукла і замкнена допустима множина, наприклад $$\mathcal{C} = [x_{\text{min}}, x_{\text{max}}]^m$$.

Розглянемо популяцію з $$n$$ особин які протягом $$M$$ поколінь розв'язують цю оптимізаційну задачу (пристосовуються під задану фітнес-функцію). Кожну особину будемо описувати двійковим вектором достатньо довгим для того щоб кодувати десяткові значення аргументів функції $$x_i$$ з потрібною точністю $$\varepsilon$$.

Перше покоління не має &laquo;досвіду предків&raquo; і генерується випадковим чином, рівномірно на $$\mathcal{C}$$.

Далі з кожним поколінням відбуваються наступні речі:

- воно кодується з десяткового представлення у двійкове;

- у ньому із заданою ймовірністю $$p$$ відбувають бітові мутації;

- покоління розбивається на пари, між якими відбувається кроссовер (обмін генами);

- на основі покоління генерується нове таким чином що найкращі особини мають більшу ймовірність мати нащадка.

## Псевдокод

_Точніше не псевдокод а програма-драйвер на python._

```python
g_dec = generation_dec(n, x_min, x_max)
nn, dd, NN = bin_dec_param(x_min, x_max, eps)

for _ in range(M):
	g_bin = a_cod_binary(g_dec, x_min, nn, dd)
	g_bin, mutation_count = mutation(g_bin, p)
	m, f = parents(n >> 1)
	g_bin = crossover(g_bin, m, f)
	g_dec = a_cod_decimal(g_bin, x_min, NN, dd)
	f_vals = np.array([f(g_dec[i]) for i in range(n)]).reshape((n, 1))
	g_dec = np.hstack([g_dec, f_vals])
	b, w = best(g_dec), worst(g_dec)
	g_best = np.asarray(g_dec[b, :-1]).flatten()
	g_dec = np.delete(g_dec, w, axis=0)
	num = adapt(np.asarray(g_dec[:, -1]).flatten())
	g_dec = np.vstack([new_generation(g_dec[:, :-1], num), g_best])
``` 

## Реалізація

_Для зручності реалізації і оцінювання специфікація всіх необхідних процедур вже визначена, але від неї можна несуттєво відходити якщо так буде зручніше програмувати на вибраній Вами мові програмування._

_Також присутні вказівки для Maple і приклади реалізації на python._

Резюмуючи, Вам необхідно написати наступні процедури:

1. GenerationDec: [документація](generation_dec.md), [приклад реалізації](generation_dec.py);

2. Mutation: [документація](mutation.md), [приклад реалізації](mutation.py);

3. Crossover: [документація](crossover.md), [приклад реалізації](crossover.py);

4. Parents: [документація](parents.md), [приклад реалізації](parents.py);

5. BinDecParam: [документація](bin_dec_param.md), [приклад реалізації](bin_dec_param.py);

6. CodBinary: [документація](cod_binary.md), [приклад реалізації](cod_binary.py);

7. CodDecimal: [документація](cod_decimal.md), [приклад реалізації](cod_decimal.py);

8. ACodBinary: [документація](a_cod_binary.md), [приклад реалізації](cod_binary.py);

9. ACodDecimal: [документація](a_cod_decimal.md), [приклад реалізації](cod_decimal.py);

10. Adapt: [документація](adapt.md), [приклад реалізації](adapt.py);

11. Best і Worst: [документація](best_worst.md), [приклад реалізації](best_worst.py);

12. NewGeneration: [документація](new_generation.md), [приклад реалізації](new_generation.py);

І, нарешті. написати програму-драйвер, яка буде поєднувати усі вищезгадані процедури.

[Назад на головну](../README.md)