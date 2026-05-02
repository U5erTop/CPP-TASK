# Экзамен по системному программированию
## Тема: язык C++ и принципы объектно-ориентированного программирования

---

## Билет 1
1. История языка C++ и его место среди языков системного программирования.
2. Этапы компиляции программы: препроцессор, компиляция, линковка.
3. Структура простой программы на C++.
4. Понятия переменной, типа данных и области видимости.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 10;
    cout << A << endl;
    return 0;
}
```

---

## Билет 2
1. Основные типы данных в C++: целые, вещественные, символьные, логические.
2. Константы и литералы.
3. Операции ввода и вывода через `cin` и `cout`.
4. Арифметические и логические операторы.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

int main() {
    int x;
    cin >> x
    cout << x << endl;
    return 0;
}
```

---

## Билет 3
1. Условный оператор `if` и полная форма `if-else`.
2. Вложенные условные операторы.
3. Оператор выбора `switch`.
4. Тернарный оператор.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

int main() {
    int n = 2;
    if (n = 5)
        cout << "five";
    return 0;
}
```

---

## Билет 4
1. Цикл `while`.
2. Цикл `do-while`.
3. Цикл `for`.
4. Операторы `break` и `continue`.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

int main() {
    for (int i = 0; i <= 5; i--)
        cout << i << " ";
    return 0;
}
```

---

## Билет 5
1. Одномерные массивы в C++.
2. Инициализация и обработка массива.
3. Двумерные массивы.
4. Строки как массивы символов и тип `string`.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

int main() {
    int a[3] = {1, 2, 3};
    cout << a[3] << endl;
    return 0;
}
```

---

## Билет 6
1. Понятие функции в C++.
2. Объявление, определение и вызов функции.
3. Формальные и фактические параметры.
4. Возврат значения из функции.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

int sum(int a, int b) {
    a + b;
}

int main() {
    cout << sum(2, 3);
    return 0;
}
```

---

## Билет 7
1. Передача параметров по значению.
2. Передача параметров по ссылке.
3. Передача указателей в функции.
4. Перегрузка функций.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

void change(int x) {
    x = 100;
}

int main() {
    int a = 5;
    change(a);
    cout << a;
    return 0;
}
```

---

## Билет 8
1. Указатели: объявление и инициализация.
2. Операции `*` и `&`.
3. Нулевой указатель.
4. Связь указателей и массивов.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

int main() {
    int *p;
    *p = 10;
    cout << *p;
    return 0;
}
```

---

## Билет 9
1. Ссылки в C++.
2. Отличия ссылки от указателя.
3. Константные ссылки.
4. Использование ссылок для оптимизации передачи параметров.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

int main() {
    int &r;
    int a = 10;
    r = a;
    cout << r;
    return 0;
}
```

---

## Билет 10
1. Динамическая память в C++.
2. Операторы `new` и `delete`.
3. Выделение памяти под массив.
4. Утечки памяти и способы их предотвращения.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

int main() {
    int *a = new int[5];
    delete a;
    return 0;
}
```

---

## Билет 11
1. Понятие структуры `struct`.
2. Описание и использование структур.
3. Массивы структур.
4. Передача структур в функции.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

struct Point {
    int x;
    int y;
};

int main() {
    Point p;
    cout << p.x << " " << p.y;
    return 0;
}
```

---

## Билет 12
1. Перечисления `enum`.
2. Пространства имен.
3. Директива `using namespace`.
4. Файлы заголовков и подключение `#include`.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>

int main() {
    cout << "Hello" << std::endl;
    return 0;
}
```

---

## Билет 13
1. Понятие класса в C++.
2. Отличия `class` и `struct`.
3. Поля и методы класса.
4. Спецификаторы доступа `private`, `public`, `protected`.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

class Test {
    int x;
};

int main() {
    Test t;
    t.x = 5;
    return 0;
}
```

---

## Билет 14
1. Конструкторы класса.
2. Конструктор по умолчанию.
3. Конструктор с параметрами.
4. Список инициализации конструктора.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

class Test {
public:
    int x;
    Test(int a) { x = a; }
};

int main() {
    Test t;
    return 0;
}
```

---

## Билет 15
1. Деструктор класса.
2. Назначение деструктора.
3. Порядок вызова конструкторов и деструкторов.
4. Управление ресурсами в классе.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

class Test {
public:
    ~Test(int x) {}
};

int main() {
    Test t;
    return 0;
}
```

---

## Билет 16
1. Инкапсуляция как принцип ООП.
2. Сокрытие данных в классе.
3. Методы доступа `get` и `set`.
4. Преимущества инкапсуляции.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

class BankAccount {
private:
    double balance;
public:
    void setBalance(double b) {
        balance = b;
    }
};

int main() {
    BankAccount acc;
    acc.balance = 1000;
    return 0;
}
```

---

## Билет 17
1. Наследование в C++.
2. Базовый и производный класс.
3. Виды наследования: public, private, protected.
4. Доступ к членам базового класса.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

class Base {
private:
    int x;
};

class Derived : public Base {
public:
    void show() {
        x = 10;
    }
};
```

---

## Билет 18
1. Полиморфизм как принцип ООП.
2. Раннее и позднее связывание.
3. Виртуальные функции.
4. Ключевое слово `virtual`.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

class Base {
public:
    void show() { cout << "Base"; }
};

class Derived : public Base {
public:
    void show() { cout << "Derived"; }
};

int main() {
    Base *p = new Derived();
    p->show();
    return 0;
}
```

---

## Билет 19
1. Абстракция как принцип ООП.
2. Абстрактные классы.
3. Чисто виртуальные функции.
4. Интерфейсный подход в C++.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

class Shape {
public:
    virtual void draw() = 0;
};

int main() {
    Shape s;
    return 0;
}
```

---

## Билет 20
1. Дружественные функции и классы.
2. Статические поля класса.
3. Статические методы класса.
4. Ключевое слово `this`.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

class Test {
public:
    static int count;
};

int main() {
    cout << Test::count;
    return 0;
}
```

---

## Билет 21
1. Перегрузка операторов.
2. Правила перегрузки операторов.
3. Перегрузка бинарных и унарных операторов.
4. Ограничения при перегрузке операторов.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

class Number {
public:
    int x;
    Number(int a) : x(a) {}
    void operator+(Number n) {
        x += n.x;
    }
};

int main() {
    Number a(2), b(3);
    Number c = a + b;
    return 0;
}
```

---

## Билет 22
1. Конструктор копирования.
2. Оператор присваивания.
3. Поверхностное и глубокое копирование.
4. Правило трех.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

class Array {
    int *data;
public:
    Array() { data = new int[5]; }
    ~Array() { delete[] data; }
};

int main() {
    Array a;
    Array b = a;
    return 0;
}
```

---

## Билет 23
1. Шаблоны функций.
2. Шаблоны классов.
3. Параметры шаблонов.
4. Преимущества обобщенного программирования.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

template <class T>
T sum(T a, T b) {
    return a + b;
}

int main() {
    cout << sum(2, 3.5);
    return 0;
}
```

---

## Билет 24
1. Исключения в C++.
2. Блоки `try`, `catch`, `throw`.
3. Обработка стандартных исключений.
4. Преимущества механизма исключений.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

int main() {
    try {
        throw 5;
    }
    catch (double x) {
        cout << x;
    }
    return 0;
}
```

---

## Билет 25
1. Файловый ввод-вывод в C++.
2. Классы `ifstream`, `ofstream`, `fstream`.
3. Открытие и закрытие файлов.
4. Проверка успешности открытия файла.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    ofstream fout;
    fout << "Hello";
    fout.close();
    return 0;
}
```
Ошибка: файл не открыт перед записью.

---

## Билет 26
1. Стандартная библиотека шаблонов STL.
2. Контейнер `vector`.
3. Итераторы.
4. Алгоритмы STL.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    cout << v[0];
    return 0;
}
```

---

## Билет 27
1. Модификаторы доступа и их влияние на проектирование класса.
2. Ключевое слово `const` для методов.
3. Константные объекты.
4. Перегрузка методов по `const`.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

class Test {
public:
    void show() {
        cout << "Hello";
    }
};

int main() {
    const Test t;
    t.show();
    return 0;
}
```

---

## Билет 28
1. Пространство памяти программы: стек, куча, статическая память.
2. Локальные и глобальные переменные.
3. Время жизни объектов.
4. RAII как подход к управлению ресурсами.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

int* getPtr() {
    int x = 10;
    return &x;
}

int main() {
    int *p = getPtr();
    cout << *p;
    return 0;
}
```

---

## Билет 29
1. Множественное наследование.
2. Проблема ромбовидного наследования.
3. Виртуальное наследование.
4. Особенности конструирования при множественном наследовании.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

class A {
public:
    void show() { cout << "A"; }
};

class B : public A {};
class C : public A {};
class D : public B, public C {};

int main() {
    D d;
    d.show();
    return 0;
}
```

---

## Билет 30
1. Современный стиль программирования на C++.
2. Отличия C и C++ в системном программировании.
3. Основные принципы хорошего объектно-ориентированного дизайна.
4. Связь ООП с практической разработкой программных систем.

**Практическая задача — найти ошибку:**
```cpp
#include <iostream>
using namespace std;

class Base {
public:
    ~Base() {}
};

class Derived : public Base {
public:
    ~Derived() { cout << "Deleted"; }
};

int main() {
    Base *p = new Derived();
    delete p;
    return 0;
}
```

---
