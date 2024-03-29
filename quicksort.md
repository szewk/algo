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

# **Быстрая сортировка**

Алгоритм быстрой сортировки работает быстрее, чем сортировка пузырьком и сортировка вставками, а именно за $O(N \log N)$ операций в большинстве случаев. В отличие от алгоритмов, которые сравнивают соседние элементы и идут по массиву линейно (из-за чего такие алгоритмы часто работают за $O(N^2)$ в худшем случае), быстрая сортировка работает рекурсивно.

В массиве случайно выбирается опорный элемент (`pivot`), часто это первый или последний элемент. Затем массив делится на три группы: элементы, которые больше опорного элемента, меньше его и равны ему. Потом эта же функция рекуррентно обрабатывает массивы `less` и `greater`. Таким образом, когда обрабатываемый массив будет содержать только один элемент, функция вернет этот массив.

```py
    def quicksort(mas):
        less, equal, greater = [], [], []
        
        if len(mas) > 1:
            pivot = mas[0]
        
            for item in mas:
                if item < pivot:
                    less.append(item)
                elif item == pivot:
                    equal.append(item)
                elif item > pivot:
                    greater.append(item)
            return quicksort(less) + equal + quicksort(greater)
        
        else:
            return mas
```

Принцип работы быстрой сортировки можно представить в виде следующей схемы:

<img src="assets/quicksort.png" alt="Quicksort" width="500"/>

Мы видим, что массив "ветвится" на подмассивы и в конце полученные части соединяются в отсортированный массив благодаря тому, что функция возвращает `quicksort(less) + equal + quicksort(greater)` именно в таком порядке.
