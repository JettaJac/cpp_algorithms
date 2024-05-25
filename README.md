# Pathfinding algorithms
##
В данном проекте реализовано несколько основных алгоритмов на графах. В частности поиск в глубину и в ширину, алгоритм Дейстры, алгоритм Флойда-Уоршелл, алгоритм Прима, муравьиный алгоритм.

#
## Запуск проекта

- make (используя Makefile)

#
## Contents

1. [Требования к коду и графам](#chapter-i) \
2. [Part 1 - Обход графа в глубину и в ширину](#part-1-обход-графа-в-глубину-и-в-ширину)  
3. [Part 2 - Поиск кратчайших путей в графе](#part-2-поиск-кратчайших-путей-в-графе)  
4. [Part 3 - Поиск минимального остовного дерева](#part-3-поиск-минимального-остовного-дерева)  
5. [Part 4 - Задача коммивояжера](#part-4-задача-коммивояжера)  
6. [Part 5 - Консольный интерфейс](#part-5-консольный-интерфейс)  


#
## Требования к коду
- Библиотеки разработана на языке С++ стандарта C++17
- При написании кода придерживались Google Style
- Сборка программы настроена с помощью Makefile со стандартным набором целей для GNU-программ: _all, clean, test, s21_graph.a_б _s21_graph_algorithms.a_
- Библиотеки обеспечены полным покрытием unit-тестами методов класса `Graph`, `GraphAlgorithms`

#
## Требования к графам
- Веса ребер только натуральными числами
- Могут быть петли
- Веса могут отличаться на всех ребрах
- Только ненулевой связный граф

#
Реализована библиотеку _s21_graph.h_:
* Решение оформлено как статическая библиотека (с заголовочным файлом _s21_graph.h_)
* Библиотека представлена в виде класса `Graph`, который хранит в себе информацию о графе с помощью **матрицы смежности**. Размерность матрицы смежности задаватется динамически при инициализации графа (при его загрузке из файла)

* Класс `Graph` содержит в себе следующие публичные методы:
    + `LoadGraphFromFile(string filename)` - загрузка графа из файла в формате матрицы смежности
    + `ExportGraphToDot(string filename)` - выгрузка графа в файл в формате dot (см. материалы)

Реализована библиотеку _s21_graph_algorithms.h_
* Решение оформлено как статическая библиотека(с заголовочным файлом _s21_graph_algorithms.h_)
* Библиотека представлена в виде класса `GraphAlgorithms`, который содержит в себе реализацию алгоритмов на графах. При этом сам класс `GraphAlgorithms` ничего не знает о внутреннем представлении графа из класса `Graph`. 

#
## Part 1. Обход графа в глубину и в ширину

* Класс `GraphAlgorithms` содержит в себе по крайней мере следующие публичные методы:    
    + `DepthFirstSearch(Graph &graph, int start_vertex)` - *нерекурентный* поиск в глубину в графе от заданной вершины. Функция возвращает массив, содержащий в себе обойдённые вершины в порядке их обхода. При реализации этой функции использован *самописный* структуру данных **стек**
    + `BreadthFirstSearch(Graph &graph, int start_vertex)` - поиск в ширину в графе от заданной вершины. Функция возвращает массив, содержащий в себе обойдённые вершины в порядке их обхода. При реализации этой функции обязательно использована *самописная* структура данных **очередь**
    
*Номера вершин начинаются с 1*

## Part 2. Поиск кратчайших путей в графе

* :
    + `GetShortestPathBetweenVertices(Graph &graph, int vertex1, int vertex2)` - поиск кратчайшего пути между двумя вершинами в графе с использованием *алгоритма Дейкстры*. Функция принимает на вход номера двух вершин и возвращает численный результат, равный наименьшему расстоянию между ними
    + `GetShortestPathsBetweenAllVertices(Graph &graph)` - поиск кратчайших путей между всеми парами вершин в графе с использованием *алгоритма Флойда-Уоршелла*. В качестве результата функция возвращает матрицу кратчайших путей между всеми вершинами графа

## Part 3. Поиск минимального остовного дерева

* :
    + `GetLeastSpanningTree(Graph &graph)` - поиск наименьшего остовного дерева в графе с помощью *алгоритма Прима*. В качестве результата функция должна возвращать матрицу смежности для минимального остовного дерева

## Part 4. Задача коммивояжера

* :
    + `SolveTravelingSalesmanProblem(Graph &graph)` - решение задачи коммивояжера с помощью *муравьиного алгоритма*. Алгоритм ищет самый выгодный (короткий) маршрут, проходящий через все вершины графа хотя бы по одному разу с последующим возвратом в исходную вершину. В качестве результата функция возвращает структуру `TsmResult`, описанную ниже:
    ```cpp
    struct TsmResult {
        int* vertices;    // массив с искомым маршрутом (с порядком обхода вершин). Вместо int* можно использовать std::vector<int>
        double distance;  // длина этого маршрута
    }
    ``` 

*Если при заданном графе решение задачи невозможно, выводиться ошибка.*

## Part 5. Консольный интерфейс

* Основная программа, которая представляет из себя консольное приложение для проверки работоспособности реализованных библиотек s21_graph.h и s21_graph_algorithms.h
* Консольный интерфейс покрывает следующий функционал:
    1. загрузка исходного графа из файла
    2. обход графа в ширину с выводом результата обхода в консоль
    3. обход графа в глубину с выводом результата обхода в консоль
    4. поиск кратчайшего пути между произвольными двумя вершинами с выводом результата в консоль
    5. поиск кратчайших путей между всеми парами вершин в графе с выводом результирующей матрицы в консоль
    6. поиск минимального остовного дерева в графе с выводом результирующей матрицы смежности в консоль
    7. решение задачи комивояжера с выводом результирующего маршрута и его длины в консоль



