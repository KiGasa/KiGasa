# Лабораторная работа 4
## Функции
Цель этой лабораторной работы — изучить понятие функции в C++ и научиться объявлять,
определять и вызывать функции, а также научиться хорошо тестировать свои собственные
программы!

(!) Обязательно скачиваете папку с cpp-файлами из Яндекс-диска курса! Там уже лежат
мои тесты для задач, а также места для ваших собственных тестов.  
(!!) Когда делаете свои unit-тесты, вы должны придумать их независимо от своей програм-
мы. Нельзя генерировать программой тесты для проверки самой же программы!  

### **Задания A**

1. Напишите функцию возведения целого числа в целую неотрицательную степень
long long power(long long x, unsigned k), которая вычисляет x<sup>k</sup>.
Надо unit-тестировать функцию power.
```
#include<iostream>
// #define NDEBUG
using namespace std;
#include<cassert>

long long power(long long x, int k) {
    long long res = 1;
    for (int i = 0; i < k; ++i)
        res = res * x;
    return res;
}
int main() {
     long long x,k; 
     cin >> x >> k;
     cout << power(x, k) << endl;
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
x - число которое надо возвесьти в степень *k* раз. сделан с помощью цикла где каждый до *k* раз res *= x.

2. C помощью написанной в предыдущей задаче функции power (ее надо скопировать в вашу
программу), напишите функцию
long long sum_p(int p, int n), которая вычисляет сумму *p*-х степеней чисел 1, 2, ..., *n*,
т.е. вычисляет 1<sup>*p*</sup> + 2<sup>*p*</sup> + ...+ *n*<sup>*p*</sup>.
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
Числа идут от 1<sup>*p*</sup> + 2 <sup>*p*</sup> до + n<sup>*p*</sup>, где p - степень. Расположил функцию power выше т.к. она задействована в функции sum_p, где с помощью цикла передовал числа в power, возвращал, суммировал и по циклу. В конце цикла ретурнул ответ.

3. Напишите функцию
double dist(double x1, double y1, double x2, double y2),
которая принимает вещественные декартовы координаты двух точек на плоскости и воз-
вращает расстояние между ними.
Напишите с ее помощью программу, которая вводит вещественные координаты x<sub>1</sub>, y<sub>1</sub>, x<sub>2</sub>, y<sub>2</sub>, x<sub>3</sub>, y<sub>3</sub> трех точек на плоскости и выводит длину самой длинной стороны треугольника
с вершинами в этих точках, или –1, если такого треугольника не существует.
*Пример*.  
Ввод: 0 0 6 0 3 2 Вывод: 6  
Сделайте функцию solve, которая принимает шесть аргументов (координаты) и возвра-
щает одно вещественное число — ответ на задачу. Функция main отвечает только за ввод-
вывод и вызов функции solve.  
Надо unit-тестировать обе функции dist и solve.

4. Напишите функцию void sort_by_last(int &a, int &b, int &c), которая сортирует
три натуральных числа по их последним цифрам.
Надо unit-тестировать только функцию sort_by_last.  
*Пример*.  
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
Сначала резал до последней цифры каждого числа, а затем решал жестким перебором.

5. Напишите функцию bool perfect(int n), которая принимает целое число n и проверяет,
является ли оно *совершенным числом*. Совершенное число — число, равное сумме всех
своих делителей.
Напишите с ее помощью программу, которая вводит целые числа 0 < *M* ⩽ *N* и выводит
все совершенные числа на диапазоне [*M*,*N* ] в порядке возрастания.
*Пример*.
Ввод: 3500 Вывод: 6 28 496
Надо unit-тестировать только функцию perfect.
```
//#define NDEBUG
#include<cassert>
#include<iostream>
using namespace std;

bool perfect(int n)
{
    int sum = 0;
    for (int i = 1; i < n; i++)
    {
        if (n % i == 0) { sum = sum + i;}
    }
    if (n == sum) return true;
    else return false;
}
int main()
{
    int m, n;
    cin >> m >> n;
    for (int i = m; i <= n; i++)
    {
        if (perfect(i)) {cout << i << ' ';}
    }
    //Dulustan's tests
    {
        assert(perfect(6));
        assert(perfect(28));
        assert(perfect(496));
        assert(perfect(8128));
        assert(!perfect(36));
        assert(!perfect(490));
        assert(!perfect(812));
        assert(!perfect(6458));
#ifndef NDEBUG
        cout << "SUCCESS!" << endl;
#endif
    }
    //Тут свои тесты можно не делать, ура!
}
```
Диапазон идет по циклу, проверяется на совершенство (путем проверки от 1 до n, где каждыое n % i == 0 суммируется в sum = sum + i и если sum == n выводится на экран).

### **Задания B**

1. Напишите функцию bool hamming(int n), которая принимает целое число *n* и проверяет,
является ли оно *числом Хэмминга*. Число Хэмминга — число, не имеющее других простых
делителей, кроме 2, 3 или 5
Напишите с ее помощью программу, которая вводит целые числа 0 < M ⩽ N и выводит
все числа Хэмминга на диапазоне [*M*,*N*] в порядке возрастания.
*Пример*.
Ввод: 9 20 Вывод: 9 10 12 15 16 18 20
Надо unit-тестировать только функцию hamming.
```
//#define NDEBUG
#include<cassert>
#include<iostream>
using namespace std;

bool hamming(int n)
{
    while (n % 2 == 0) {
        n /= 2;
    }
    while (n % 3 == 0) {
        n /= 3;
    }
    while (n % 5 == 0) {
        n /= 5;
    }
    if (n == 1) return true;
    return false;
}


int main()
{
    int m, n;
    cin >> m >> n;
    for (int i = m; i <= n; i++)
    {
        if (hamming(i))
        {
            cout << i << ' ';
        }
    }
    //Dulustan's tests
    {
        assert(hamming(1));
        assert(hamming(8));
        assert(hamming(12));
        assert(hamming(24));
        assert(hamming(45));
        assert(hamming(384));
        assert(!hamming(14));
        assert(!hamming(26));
        assert(!hamming(44));
        assert(!hamming(365));
#ifndef NDEBUG
        cout << endl <<"SUCCESS 1!" << endl;
#endif   
    }

    //Придумайте 3 положительных и 3 отрицательных теста.
    //Student's tests
    {
        assert(hamming(128));
        assert(hamming(12));
        assert(hamming(800));
        assert(!hamming(114));
        assert(!hamming(17));
        assert(!hamming(101));
#ifndef NDEBUG
        cout << "SUCCESS 2!" << endl;
#endif     
    }
}
```
Перебор диапазона с помощю цикла, где каждое число проверяется на число Хэмингтона. Если число хэмингтонова то выводится. 

2. Возьмем любое натуральное число. Если оно четное — разделим его пополам, если нечетное — умножим на 3, прибавим 1 и разделим пополам. Повторим эти действия с вновь
полученным числом. Гипотеза Сиракуз гласит, что независимо от выбора первого числа рано или поздно мы получим 1.  
Напишите функцию int Syracuse(int n), которая проверяет, за сколько шагов число n
превратится в единичку вышеуказанным алгоритмом (одним шагом считайте одно пол-
ное преврашение числа: разделение пополам ИЛИ (умножение на 3 + прибавление 1 + разделение пополам).    
Напишите с ее помощью программу, которая вводит целые числа 0 < *M* ⩽ *N* и выводит
количество шагов Гипотезы Сиракуз для каждого числа на диапазоне [*M*,*N* ].
Надо unit-тестировать только функцию Syracuse.
```
//#define NDEBUG
#include<cassert>
#include<iostream>
using namespace std;
int Syracuse(int n)
{
    int x = 0;
    while (n != 1)
    {
        if (n % 2 == 0) {
            n = n / 2; 
        }
        else
        {
            n *= 3;
            n++;
            n = n / 2;
        }
        ++x;
    }
    return x;
}
int main()
{
    int m, n;
    cin >> m >> n;
    for (int i = m; i <= n; ++i)
    {
        cout << i << ' ' << Syracuse(i) << endl;
    }

    //Dulustan's tests
    {
        assert(Syracuse(1) == 0);
        assert(Syracuse(2) == 1);
#ifndef NDEBUG
        cout << "SUCCESS 1!" << endl;
#endif    
    }
    //Тут я поленился вычислять тесты, оставляю это дело за вами.
    //Придумайте 8 тестов.
    //Student's tests
    {
        assert(Syracuse(200) == 19);
        assert(Syracuse(4) == 2);
        assert(Syracuse(8) == 3);
        assert(Syracuse(9) == 13);
        assert(Syracuse(115) == 23);
        assert(Syracuse(32) == 5);
        assert(Syracuse(72) == 16);
        assert(Syracuse(920) == 26);
#ifndef NDEBUG
        cout << "SUCCESS 2!" << endl;
#endif    
    }
}
```
Опять по диапазону циклом for пробежались. Для каждого числа диапозона воспользовались *Гипотезой Сиркауза* и считали сколько раз нужно воспользоваться гипотезой, чтобы в конце концов получилась 1 и в выводе выводилось кол-во шагов.

3. *Цифровой корень* натурального числа получается следующим образом: cкладываем все
цифры данного числа — получаем новое число. Повторяем процесс, пока в результате не
будет получено однозначное число, которое и называется цифровым корнем числа.  
Напишите функцию void digit_root(long long &n), которое превращает *n* в свой цифровой корень.  
Надо unit-тестировать функцию digit_root.
```
//#define NDEBUG
#include<cassert>
#include<iostream>
using namespace std;
int len(long long x)
{
    int len = 0;
    if (x == 0) { return 1; }
    while (x != 0)
    {
        len++;
        x = x / 10;
        
    }
    return len;
}
long long sum(long long x)
{
    long long sum = 0;
    while (x != 0)
    {
        sum = sum + (x % 10);
        x = x / 10;
    }
    return sum;
}
void digit_root(long long& n)
{
    while (len(n) != 1)
    {
        n = sum(n);
    }
}
int main()
{
    long long n; 
    cin >> n;
    digit_root(n);
    cout << n << endl;
    //Dulustan's tests
//    {
//        {
//            long long x = 8; digit_root(x);
//            assert(x == 8);
//        }
//        {
//            long long x = 25; digit_root(x);
//            assert(x == 7);
//        }
//        {
//            long long x = 99; digit_root(x);
//            assert(x == 9);
//        }
//        {
//            long long x = 987; digit_root(x);
//            assert(x == 6);
//        }
//        {
//            long long x = 777'777'777'777; digit_root(x);
//            assert(x == 3);
//        }
//
//#ifndef NDEBUG
//        cout << "SUCCESS 1!" << endl;
//#endif 
//    }
//
//    ////Придумайте 5 тестов.
//    ////Student's tests
//    {
//        {
//            long long x = 231'123'111; digit_root(x);
//            assert(x == 6);
//        }
//        {
//            long long x = 111'222'333; digit_root(x);
//            assert(x == 9);
//        }
//        {
//            long long x = 7479; digit_root(x);
//            assert(x == 9);
//        }
//        {
//            long long x = 21; digit_root(x);
//            assert(x == 3);
//        }
//        {
//            long long x = 0; digit_root(x);
//            assert(x == 0);
//        }
//#ifndef NDEBUG
//        cout << "SUCCESS 2!" << endl;
//#endif  
//    }
}
```
Вводится число n, n принимает функция void digit_root, где проверяется в функции len на длину числа (если осталась одна цифра, то она прекращает работу). Если len успешно проверен в функции sum отрезаются и суммируется все цифры. ДОПУСТИМ вышло не однозначное число после sum, если такое произошло то все начинается опять с проверки на len.

4. Напишите функцию int my_gcd(int a, int b), которая находит НОД (наибольший об-
щий делитель) чисел a и b. Используйте реализацию алгоритма Евклида через цикл while.
Напишите функцию void simplify(int &num, int &denom), которая сокращает дробь
num/denom , используя написанную вами функцию my_gcd. Также напишите функцию main,
чтобы она делала ввод числителя и знаменателя, и выводила числитель и знаменатель
сокращенной дроби. А само сокращение должно делаться через вашу функцию.
Надо unit-тестировать обе функции my_gcd и simplify.
```
//#define NDEBUG
#include<cassert>
#include<iostream>
using namespace std;

int my_gcd(int a, int b)
{
    int c, d, S;
    if (a % b == 0) return b;
    if (b % a == 0) return a;
    if (a > b)
    {
        c = a % b;
        if (b % c == 0) return c;
        d = b % c;
        while (c % d != 0)
        {
            S = c % d;
            c = d;
            d = S;
        }
        return d;
    }
    else
    {
        c = b % a;
        if (a % c == 0) return c;
        d = a % c;
        while (c % d != 0)
        {
            S = c % d;
            c = d;
            d = S;
        }
        return d;
    }
}
void simplify(int& num, int& denom)
{
    int A = my_gcd(num, denom);
    num = num / A;
    denom = denom / A;
}
int main()
{
    /*int num, denom;
    cin >> num >> denom;
    simplify(num, denom);
    cout << num << '/' << denom<<endl;*/


    //Dulustan's tests GCD
    {
        assert(my_gcd(12, 20) == 4);
        assert(my_gcd(35, 56) == 7);
        assert(my_gcd(100, 9900) == 100);
        assert(my_gcd(999, 2775) == 111);
#ifndef NDEBUG
        cout << "SUCCESS 1!" << endl;
#endif 
    }

    //Придумайте 4 теста.
    //Student's tests GCD
    {
        assert(my_gcd(84, 90) == 6);
        assert(my_gcd(15, 28) == 1);
        assert(my_gcd(140, 96) == 4);
        assert(my_gcd(24, 8) == 8);
#ifndef NDEBUG
        cout << "SUCCESS 2!" << endl;
#endif 
    }

    //Dulustan's tests simplify
    {
        int a = 15, b = 20;
        simplify(a, b);
        assert(a == 3); assert(b == 4);

        a = 48, b = 120;
        simplify(a, b);
        assert(a == 2); assert(b == 5);

        a = 1680, b = 4620;
        simplify(a, b);
        assert(a == 4); assert(b == 11);
#ifndef NDEBUG
        cout << "SUCCESS 3!" << endl;
#endif 
    }

    //Придумайте 4 теста.
    //Student's tests simplify
    {
        {
            int a = 1000, b = 30;
            simplify(a, b);
            assert(a == 100); assert(b == 3);
        }
        {
            int a = 30564, b = 11232;
            simplify(a, b);
            assert(a == 283); assert(b = 104);
        }
        {
            int a = 312312, b = 66666666;
            simplify(a, b);
            assert(a == 4732); assert(b == 1010101);
        }
        {
            int a = 1111, b = 2222;
            simplify(a, b);
            assert(a == 1); assert(b == 2);
        }
#ifndef NDEBUG
        cout << "SUCCESS 4!" << endl;
#endif 
    }
}
```
Находим НОД с помощью *алгоритма Евклида* (my_gcd), а simplify т.е упрощения путём деления числа с НОД.

5. Напишите функцию void intersect(int a, int b, int c, int d, int &l, int &r), ко-
торая находит пересечение [*l, r*] отрезков [*a, b*] и [*c, d*]. Если эти отрезки не пересекаются,
то ответом сделайте *l* = 0, *r* = −1. Гарантируется, что *a* ≤ *b* и *c* ≤ *d*.
Надо unit-тестировать функцию intersect. Все случаи взаимного расположения отрезков
[*a, b*] и [*c, d*] надо тщательно тестировать!

