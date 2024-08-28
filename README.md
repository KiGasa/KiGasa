# Лабораторная работа 4
## Функции
Цель этой лабораторной работы — изучить понятие функции в C++ и научиться объявлять,
определять и вызывать функции, а также научиться хорошо тестировать свои собственные
программы!

(!) Обязательно скачиваете папку с cpp-файлами из Яндекс-диска курса! Там уже лежат
мои тесты для задач, а также места для ваших собственных тестов.
(!!) Когда делаете свои unit-тесты, вы должны придумать их независимо от своей програм-
мы. Нельзя генерировать программой тесты для проверки самой же программы!

### Задания A

1. Напишите функцию возведения целого числа в целую неотрицательную степень
long long power(long long x, unsigned k), которая вычисляет xk.
Надо unit-тестировать функцию power.
```
#include<iostream>
// #define NDEBUG
using namespace std;
#include<cassert>

long long power(long long x, int p) {
    long long res = 1;
    for (int i = 0; i < p; ++i)
        res = res * x;
    return res;
}
int main() {
     long long x,p; 
     cin >> x >> p;
     cout << power(x, p) << endl;
    //Dulustan's tests
    {
        assert(power(1, 100) == 1);
        assert(power(2, 7) == 128);
        assert(power(2, 10) == 1024);
        assert(power(6, 5) == 7776);
        assert(power(7,13) == 96889010407);
#ifndef NDEBUG
        cout << "SUCCESS 1!" << endl;
#endif
    }
    //Придумайте 4 теста.
    //Student's tests
    {
        assert(power(2, 4) == 16);
        assert(power(3, 12) == 531441);
        assert(power(2, 20) == 1048576);
        assert(power(2, 11) == 2048);
#ifndef NDEBUG
        cout << "SUCCESS 2!" << endl;
#endif
    }
}
```
2. C помощью написанной в предыдущей задаче функции power (ее надо скопировать в вашу
программу), напишите функцию
long long sum_p(int p, int n), которая вычисляет сумму p-х степеней чисел 1, 2, ..., n,
т.е. вычисляет 1p + 2p + ...+ np.
Надо unit-тестировать функцию sum_p.
```
#include<iostream>
// #define NDEBUG
#include<cassert>
using namespace std;

long long power(long long x, int p) {
    long long res = 1;
    for (int i = 0; i < p; ++i)
        res = res * x;
    return res;
}
long long sum_p(int p, int n) {
    int r = 0;
    for (int i = 1; i <= n; ++i) {
        r = r + power(i, p);
    }
    return r;
}

int main() {
    int p, n;
    cin >> p >> n;
    cout << sum_p(p, n) << endl;
    //Dulustan's tests
    {
        assert(sum_p(1, 10) == 55);
        assert(sum_p(2, 10) == 385);
        assert(sum_p(3, 3) == 36);
        assert(sum_p(4, 5) == 979);
#ifndef NDEBUG
        cout << "SUCCESS 1!" << endl;
#endif
    }

    //Придумайте 4 теста.
    //Student's tests
    {
        assert(sum_p(1, 15) == 120);
        assert(sum_p(2, 9) == 285);
        assert(sum_p(5, 4) == 1300);
        assert(sum_p(8, 3) == 6818);
#ifndef NDEBUG
        cout << "SUCCESS 2!" << endl;
#endif
    }
}
```
3. Напишите функцию
double dist(double x1, double y1, double x2, double y2),
которая принимает вещественные декартовы координаты двух точек на плоскости и воз-
вращает расстояние между ними.
Напишите с ее помощью программу, которая вводит вещественные координаты x1, y1, x2,
y2, x3, y3 трех точек на плоскости и выводит длину самой длинной стороны треугольника
с вершинами в этих точках, или –1, если такого треугольника не существует.
Пример.
Ввод: 0 0 6 0 3 2 Вывод: 6
Сделайте функцию solve, которая принимает шесть аргументов (координаты) и возвра-
щает одно вещественное число — ответ на задачу. Функция main отвечает только за ввод-
вывод и вызов функции solve.
Надо unit-тестировать обе функции dist и solve.

5. Напишите функцию void sort_by_last(int &a, int &b, int &c), которая сортирует
три натуральных числа по их последним цифрам.
Надо unit-тестировать только функцию sort_by_last.
Пример.
Ввод: 138 2647 36971 Вывод: 36971 2647 138
```
//#define NDEBUG
#include<cassert>
#include<iostream>
using namespace std;

void sort_by_last(int& a, int& b, int& c)
{
    int A, B, C, AA = a, BB = b, CC = c;
    A = a % 10;
    B = b % 10;
    C = c % 10;
    if (A < B and B < C)//ABC
    {
        return;
    }
    else if (A < C and C < B)//ACB
    {
        a = AA;
        b = CC;
        c = BB;
        return;
    }
    else if (B < A and A < C)//BAC
    {
        a = BB;
        b = AA;
        c = CC;
        return;
    }
    else if (B < C and C < A)//BCA
    {
        a = BB;
        b = CC;
        c = AA;
        return;
    }
    else if (C < A and A < B)//CAB
    {
        a = CC;
        b = AA;
        c = BB;
        return;
    }
    else if (C < B and B < A)//CBA
    {
        a = CC;
        b = BB;
        c = AA;
        return;
    }
    else if (A == B and B < C)//ABC or BAC
    {
        a = AA;
        b = BB;
        c = CC;
        return;
    }
    else if (A == C and C < B)//ACB or CAB
    {
        a = AA;
        b = CC;
        c = BB;
        return;
    }
    else if (B == C and C < A)//BCA or CBA
    {
        a = BB;
        b = CC;
        c = AA;
        return;
    }
}

int main()
{
    int a, b, c;
    cin >> a >> b >> c;
    sort_by_last(a, b, c);
    cout << a << ' ' << b << ' ' << c << ' ' << endl;
    //Dulustan's tests
    {
        {
            int a = 138, b = 2647, c = 36971;
            sort_by_last(a, b, c);
            assert(a == 36971 && b == 2647 && c == 138);
        }
        {
            int a = 456, b = 123, c = 789;
            sort_by_last(a, b, c);
            assert(a == 123 && b == 456 && c == 789);
        }

#ifndef NDEBUG
        cout << "SUCCESS 1!" << endl;
#endif
    }

    //Минимум 4 теста 
    //Все возможные перестановки a,b,c должны быть протестированы!
    //Student's tests
    {
        {
            int a = 138, b = 2641, c = 36972;
            sort_by_last(a, b, c);
            assert(a == 2641 && b == 36972 && c == 138);
        }
        {
            int a = 1, b = 2, c = 1;
            sort_by_last(a, b, c);
            assert(a == 1 && b == 1 && c == 2);
        }
        {
            int a = 12338, b = 2649, c = 72;
            sort_by_last(a, b, c);
            assert(a == 72 && b == 12338 && c == 2649);
        }
        {
            int a = 13, b = 2641, c = 1;
            sort_by_last(a, b, c);
            assert(a == 2641 && b == 1 && c == 13);
        }
#ifndef NDEBUG
        cout << "SUCCESS 2!" << endl;
#endif
    }
}
```
7. Напишите функцию bool perfect(int n), которая принимает целое число n и проверяет,
является ли оно совершенным числом. Совершенное число — число, равное сумме всех
своих делителей.
Напишите с ее помощью программу, которая вводит целые числа 0 < M ⩽ N и выводит
все совершенные числа на диапазоне [M,N ] в порядке возрастания.
Пример.
Ввод: 3 500 Вывод: 6 28 496
Надо unit-тестировать только функцию perfect.
