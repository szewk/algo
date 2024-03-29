---
layout: default
---

<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

<script>
  MathJax = {
    tex: {
      inlineMath: [['$', '$']]
    }
  };
</script>

# **Метод двух указателей**

*Метод двух указателей* помогает решать целый класс задач, в который в отсортированном массиве требуется найти два элемента, удовлетворяющие некоторому условию. Рассмотрим одну из них на примере: дан отсортированный массив $A$ и некоторое число $X$. Требуется найти такие индексы $i$ и $j$, что $A_i + A_j = X$.

## **Очевидное решение**

Несомненно, эту задачу можно решить простым перебором всех пар $i$ и $j$. Это делается вложенным циклом:

```cpp
    vector<int> findPair(vector<int> A, int X) {
        // перебираем все возможные пары
        int N = A.size();
        for (int i = 0; i < N; ++i) {
            for (int j = 0; j < N; ++j) {
                if (A[i] + A[j] == X)
                    return {i, j};
            }
        }
  return {-1, -1}; // возвращаем {-1, -1}, если искомой пары нет
}
```

Понятно, что асимптотика данного решения составляет $O(N^2)$. Но эту задачу можно решить линейно!

## **Линейное решение (метод двух указателей)**

Вспомним, что наш массив отсортирован, это важно. Тогда мы сперва выберем первый и последний элементы, на них будут распологаться наши "указатели" $R_0$ и $L_0$. Если их сумма слишком велика, то мы уменьшим ее. Как? У нас отсортированный массив, значит можно сдвинуть правый указатель $R$ на один элемент влево, и он будет меньше, значит и сумма тоже будет меньше ($R_1 = R_0 - 1 \Rightarrow A_{L_0} + A_{R_1} \leq A_{L_0} + A_{R_0}$). Если сумма оказывается слишком мала, то мы поступаем ровно также: двигаем левый указатель на один элемент вправо, увеличивая сумму.

<img src="assets/two_pointers.png" alt="Two pointers" width="500"/>

Тогда перепишем функцию:

```cpp
vector<int> findPair(vector<int> A, int X) {
    int N = A.size();
    // индексы L и R– изначальное положение указателей
    int L = 0, R = N - 1;
    while (L < R) {
        if (A[L] + A[R] == X) { // если удовлетворяет условию
            return {L, R};
        } else if (A[L] + A[R] < X) { // если сумма меньше x
            ++L; // двигаем левый указатель на один элемент вправо
        } else {
            // двигаем правый на один элемент влево
            --R;
        }
    }
    return {-1, -1};
}
```

В итоге, в худшем случае каждый элемент будет посещен единожды, и асимптотическая сложность такого решения – $O(N)$.
