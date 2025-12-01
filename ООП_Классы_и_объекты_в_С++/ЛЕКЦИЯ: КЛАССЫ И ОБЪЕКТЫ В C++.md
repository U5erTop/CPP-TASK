# ЛЕКЦИЯ: КЛАССЫ И ОБЪЕКТЫ В C++

## ОГЛАВЛЕНИЕ

1. [Введение в объектно-ориентированное программирование](#введение)
2. [Понятие класса и объекта](#понятие-класса)
3. [Объявление и определение класса](#объявление-класса)
4. [Инкапсуляция и модификаторы доступа](#инкапсуляция)
5. [Конструкторы](#конструкторы)
6. [Деструкторы](#деструкторы)
7. [Методы класса](#методы-класса)
8. [Указатель this](#указатель-this)
9. [Статические члены класса](#статические-члены)
10. [Перегрузка операторов](#перегрузка-операторов)
11. [Дружественные функции и классы](#дружественные-функции)
12. [Примеры практического применения](#практические-примеры)
13. [Заключение](#заключение)

---

## 1. ВВЕДЕНИЕ В ОБЪЕКТНО-ОРИЕНТИРОВАННОЕ ПРОГРАММИРОВАНИЕ {#введение}

### 1.1 Что такое ООП?

**Объектно-ориентированное программирование (ООП)** — это парадигма программирования, основанная на концепции "объектов", которые объединяют данные и методы для работы с этими данными.

### 1.2 Основные принципы ООП

1. **Инкапсуляция** — сокрытие внутренней реализации и предоставление интерфейса для работы с объектом
2. **Наследование** — создание новых классов на основе существующих с расширением функциональности
3. **Полиморфизм** — возможность объектов с одинаковым интерфейсом иметь различное поведение
4. **Абстракция** — выделение существенных характеристик объекта и игнорирование несущественных

### 1.3 Преимущества ООП

- **Модульность** — код разбивается на независимые модули (классы)
- **Повторное использование** — классы можно использовать в разных проектах
- **Расширяемость** — легко добавлять новую функциональность через наследование
- **Maintainability** — проще поддерживать и модифицировать код
- **Безопасность** — инкапсуляция защищает данные от некорректного использования

---

## 2. ПОНЯТИЕ КЛАССА И ОБЪЕКТА {#понятие-класса}

### 2.1 Определения

**Класс** — это пользовательский тип данных, который описывает структуру и поведение объектов. Класс является шаблоном или чертежом для создания объектов.

**Объект** — это экземпляр (конкретный представитель) класса. Объект содержит реальные данные и может выполнять действия, определенные в классе.

### 2.2 Аналогия из жизни

- **Класс "Автомобиль"** — описание того, что такое автомобиль: имеет марку, модель, цвет, может ехать, тормозить
- **Объект** — конкретный автомобиль: Toyota Camry 2020 года, красного цвета

### 2.3 Различие между классом и структурой

В C++ классы (`class`) и структуры (`struct`) практически идентичны. Единственное различие:

- В `struct` члены по умолчанию **public**
- В `class` члены по умолчанию **private**

```cpp
struct Point1 {
    int x, y;  // По умолчанию public
};

class Point2 {
    int x, y;  // По умолчанию private
};
```

---

## 3. ОБЪЯВЛЕНИЕ И ОПРЕДЕЛЕНИЕ КЛАССА {#объявление-класса}

### 3.1 Синтаксис объявления класса

```cpp
class ИмяКласса {
    // Спецификаторы доступа и члены класса
private:
    // Приватные члены (по умолчанию)
    
public:
    // Публичные члены
    
protected:
    // Защищенные члены
};
```

### 3.2 Пример простого класса

```cpp
#include <iostream>
#include <string>

class Student {
private:
    std::string name;
    int age;
    double gpa;
    
public:
    // Конструктор
    Student(std::string n, int a, double g) {
        name = n;
        age = a;
        gpa = g;
    }
    
    // Методы
    void display() {
        std::cout << "Имя: " << name << std::endl;
        std::cout << "Возраст: " << age << std::endl;
        std::cout << "Средний балл: " << gpa << std::endl;
    }
    
    // Геттеры
    std::string getName() { return name; }
    int getAge() { return age; }
    double getGPA() { return gpa; }
    
    // Сеттеры
    void setName(std::string n) { name = n; }
    void setAge(int a) { 
        if (a > 0 && a < 120) {
            age = a;
        }
    }
    void setGPA(double g) {
        if (g >= 0.0 && g <= 5.0) {
            gpa = g;
        }
    }
};
```

### 3.3 Создание объектов класса

```cpp
int main() {
    // Создание объекта на стеке
    Student student1("Иван Иванов", 20, 4.5);
    student1.display();
    
    // Создание объекта в динамической памяти (куче)
    Student* student2 = new Student("Мария Петрова", 19, 4.8);
    student2->display();
    
    // Массив объектов
    Student students[3] = {
        Student("Петр", 21, 4.2),
        Student("Анна", 20, 4.9),
        Student("Олег", 22, 4.0)
    };
    
    // Не забываем освободить память
    delete student2;
    
    return 0;
}
```

### 3.4 Разделение объявления и определения

**Заголовочный файл (Student.h):**
```cpp
#ifndef STUDENT_H
#define STUDENT_H

#include <string>

class Student {
private:
    std::string name;
    int age;
    double gpa;
    
public:
    Student(std::string n, int a, double g);
    void display();
    std::string getName();
    void setAge(int a);
};

#endif
```

**Файл реализации (Student.cpp):**
```cpp
#include "Student.h"
#include <iostream>

Student::Student(std::string n, int a, double g) 
    : name(n), age(a), gpa(g) {
}

void Student::display() {
    std::cout << "Имя: " << name << ", Возраст: " << age 
              << ", GPA: " << gpa << std::endl;
}

std::string Student::getName() {
    return name;
}

void Student::setAge(int a) {
    if (a > 0 && a < 120) {
        age = a;
    }
}
```

---

## 4. ИНКАПСУЛЯЦИЯ И МОДИФИКАТОРЫ ДОСТУПА {#инкапсуляция}

### 4.1 Понятие инкапсуляции

**Инкапсуляция** — это механизм, который объединяет данные и методы, работающие с этими данными, в единое целое (класс) и скрывает детали реализации от пользователя.

### 4.2 Модификаторы доступа

#### **private** (приватный)
- Члены доступны **только внутри класса**
- Недоступны извне, даже в производных классах (наследниках)
- Используется для скрытия внутренней реализации

```cpp
class BankAccount {
private:
    double balance;  // Скрыт от внешнего доступа
    
public:
    void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }
    
    double getBalance() {
        return balance;
    }
};
```

#### **public** (публичный)
- Члены доступны **отовсюду**
- Формируют интерфейс класса
- Обычно это методы для работы с объектом

```cpp
class Point {
public:
    int x, y;  // Публичные поля (не рекомендуется)
    
    void print() {  // Публичный метод
        std::cout << "(" << x << ", " << y << ")" << std::endl;
    }
};
```

#### **protected** (защищенный)
- Члены доступны **внутри класса и в производных классах**
- Недоступны извне
- Используется при наследовании

```cpp
class Shape {
protected:
    std::string color;  // Доступен в наследниках
    
public:
    void setColor(std::string c) {
        color = c;
    }
};

class Circle : public Shape {
public:
    void display() {
        std::cout << "Цвет круга: " << color << std::endl;  // OK
    }
};
```

### 4.3 Геттеры и сеттеры

Геттеры и сеттеры обеспечивают контролируемый доступ к приватным полям:

```cpp
class Temperature {
private:
    double celsius;
    
public:
    // Геттер
    double getCelsius() const {
        return celsius;
    }
    
    // Сеттер с валидацией
    void setCelsius(double c) {
        if (c >= -273.15) {  // Абсолютный ноль
            celsius = c;
        } else {
            std::cout << "Ошибка: температура ниже абсолютного нуля!" << std::endl;
        }
    }
    
    // Вычисляемое свойство
    double getFahrenheit() const {
        return celsius * 9.0 / 5.0 + 32.0;
    }
    
    void setFahrenheit(double f) {
        celsius = (f - 32.0) * 5.0 / 9.0;
    }
};
```

### 4.4 Преимущества инкапсуляции

1. **Контроль данных** — можно проверять корректность значений
2. **Гибкость** — можно изменить внутреннюю реализацию без изменения интерфейса
3. **Безопасность** — нельзя случайно испортить состояние объекта
4. **Документирование** — интерфейс явно показывает, что можно делать с объектом

---

## 5. КОНСТРУКТОРЫ {#конструкторы}

### 5.1 Понятие конструктора

**Конструктор** — специальный метод класса, который автоматически вызывается при создании объекта. Служит для инициализации объекта.

**Особенности конструктора:**
- Имеет то же имя, что и класс
- Не имеет типа возвращаемого значения (даже `void`)
- Может быть перегружен (несколько конструкторов с разными параметрами)

### 5.2 Конструктор по умолчанию

Конструктор без параметров или с параметрами по умолчанию:

```cpp
class Point {
private:
    int x, y;
    
public:
    // Конструктор по умолчанию
    Point() {
        x = 0;
        y = 0;
        std::cout << "Конструктор по умолчанию\n";
    }
    
    void print() {
        std::cout << "(" << x << ", " << y << ")" << std::endl;
    }
};

int main() {
    Point p1;      // Вызов конструктора по умолчанию
    Point p2();    // ВНИМАНИЕ! Это объявление функции, а не создание объекта!
    Point p3{};    // C++11: uniform initialization
}
```

### 5.3 Конструктор с параметрами

```cpp
class Rectangle {
private:
    double width, height;
    
public:
    // Конструктор с параметрами
    Rectangle(double w, double h) {
        width = w;
        height = h;
    }
    
    double area() {
        return width * height;
    }
};

int main() {
    Rectangle rect1(5.0, 3.0);        // Вызов конструктора
    Rectangle rect2 = Rectangle(4, 6); // Тоже вызов конструктора
    Rectangle rect3{7.5, 2.5};        // C++11 стиль
}
```

### 5.4 Список инициализации

**Предпочтительный способ инициализации** членов класса:

```cpp
class Circle {
private:
    double radius;
    const double PI;  // Константу можно инициализировать только в списке
    
public:
    // Список инициализации (после :)
    Circle(double r) : radius(r), PI(3.14159) {
        // Тело конструктора
        std::cout << "Создан круг радиусом " << radius << std::endl;
    }
};
```

**Преимущества списка инициализации:**
- Эффективнее (избегает двойной инициализации)
- Единственный способ инициализировать константы и ссылки
- Единственный способ вызвать конструктор базового класса

```cpp
class Complex {
private:
    double real, imag;
    
public:
    // С списком инициализации (эффективно)
    Complex(double r, double i) : real(r), imag(i) { }
    
    // Без списка (менее эффективно)
    Complex(double r, double i) {
        real = r;  // Сначала инициализация по умолчанию, потом присваивание
        imag = i;
    }
};
```

### 5.5 Перегрузка конструкторов

Можно создать несколько конструкторов с разными параметрами:

```cpp
class Time {
private:
    int hours, minutes, seconds;
    
public:
    // Конструктор по умолчанию
    Time() : hours(0), minutes(0), seconds(0) { }
    
    // Только часы
    Time(int h) : hours(h), minutes(0), seconds(0) { }
    
    // Часы и минуты
    Time(int h, int m) : hours(h), minutes(m), seconds(0) { }
    
    // Полное время
    Time(int h, int m, int s) : hours(h), minutes(m), seconds(s) { }
};

int main() {
    Time t1;              // 00:00:00
    Time t2(14);          // 14:00:00
    Time t3(10, 30);      // 10:30:00
    Time t4(15, 45, 30);  // 15:45:30
}
```

### 5.6 Делегирующие конструкторы (C++11)

Конструктор может вызывать другой конструктор:

```cpp
class Point {
private:
    int x, y;
    
public:
    Point(int x, int y) : x(x), y(y) {
        std::cout << "Основной конструктор\n";
    }
    
    // Делегирующий конструктор
    Point() : Point(0, 0) {
        std::cout << "Делегирующий конструктор\n";
    }
    
    Point(int x) : Point(x, x) { }
};
```

### 5.7 Конструктор копирования

Создает новый объект как копию существующего:

```cpp
class String {
private:
    char* str;
    int length;
    
public:
    // Обычный конструктор
    String(const char* s) {
        length = strlen(s);
        str = new char[length + 1];
        strcpy(str, s);
    }
    
    // Конструктор копирования (ГЛУБОКОЕ КОПИРОВАНИЕ!)
    String(const String& other) {
        length = other.length;
        str = new char[length + 1];
        strcpy(str, other.str);
        std::cout << "Конструктор копирования\n";
    }
    
    ~String() {
        delete[] str;
    }
};

int main() {
    String s1("Привет");
    String s2 = s1;     // Вызов конструктора копирования
    String s3(s1);      // Тоже вызов конструктора копирования
}
```

### 5.8 Конструктор перемещения (C++11)

Перемещает ресурсы из временного объекта:

```cpp
class Array {
private:
    int* data;
    int size;
    
public:
    Array(int s) : size(s) {
        data = new int[size];
    }
    
    // Конструктор копирования
    Array(const Array& other) : size(other.size) {
        data = new int[size];
        std::copy(other.data, other.data + size, data);
        std::cout << "Копирование\n";
    }
    
    // Конструктор перемещения
    Array(Array&& other) noexcept : data(other.data), size(other.size) {
        other.data = nullptr;
        other.size = 0;
        std::cout << "Перемещение\n";
    }
    
    ~Array() {
        delete[] data;
    }
};
```

### 5.9 Explicit конструкторы

Предотвращают неявные преобразования типов:

```cpp
class Integer {
private:
    int value;
    
public:
    // Без explicit - неявное преобразование разрешено
    Integer(int v) : value(v) { }
};

void func(Integer i) { }

int main() {
    func(42);  // OK: int неявно преобразуется в Integer
}
```

```cpp
class Integer {
private:
    int value;
    
public:
    // С explicit - только явное преобразование
    explicit Integer(int v) : value(v) { }
};

void func(Integer i) { }

int main() {
    // func(42);           // ОШИБКА!
    func(Integer(42));     // OK: явное преобразование
}
```

### 5.10 Default и Delete (C++11)

```cpp
class Example {
public:
    // Явно сгенерировать конструктор по умолчанию
    Example() = default;
    
    // Запретить конструктор копирования
    Example(const Example&) = delete;
    
    // Запретить оператор присваивания
    Example& operator=(const Example&) = delete;
};
```

---

## 6. ДЕСТРУКТОРЫ {#деструкторы}

### 6.1 Понятие деструктора

**Деструктор** — специальный метод класса, который автоматически вызывается при уничтожении объекта. Служит для освобождения ресурсов.

**Особенности деструктора:**
- Имеет имя класса с символом `~` впереди
- Не имеет параметров и возвращаемого значения
- Не может быть перегружен (всегда только один)
- Вызывается автоматически при выходе из области видимости или delete

### 6.2 Синтаксис деструктора

```cpp
class Example {
public:
    Example() {
        std::cout << "Конструктор\n";
    }
    
    ~Example() {
        std::cout << "Деструктор\n";
    }
};

int main() {
    {
        Example obj;  // Создание объекта
        // ...
    }  // Здесь вызывается деструктор
    
    Example* ptr = new Example();  // Создание в куче
    delete ptr;  // Явный вызов деструктора
}
```

### 6.3 Деструктор для управления памятью

```cpp
class DynamicArray {
private:
    int* data;
    int size;
    
public:
    DynamicArray(int s) : size(s) {
        data = new int[size];
        std::cout << "Выделено " << size << " элементов\n";
    }
    
    ~DynamicArray() {
        delete[] data;
        std::cout << "Освобождена память для " << size << " элементов\n";
    }
};
```

### 6.4 Виртуальный деструктор

При работе с наследованием деструктор базового класса должен быть виртуальным:

```cpp
class Base {
public:
    virtual ~Base() {  // ВИРТУАЛЬНЫЙ деструктор
        std::cout << "Деструктор Base\n";
    }
};

class Derived : public Base {
private:
    int* data;
    
public:
    Derived() {
        data = new int[100];
    }
    
    ~Derived() override {
        delete[] data;
        std::cout << "Деструктор Derived\n";
    }
};

int main() {
    Base* ptr = new Derived();
    delete ptr;  // Вызовутся ОБА деструктора (Derived, потом Base)
}
```

**Без виртуального деструктора** вызовется только деструктор Base — утечка памяти!

### 6.5 Правило трех/пяти/нуля

**Правило трех (C++98):** Если класс определяет один из:
- Деструктор
- Конструктор копирования
- Оператор присваивания

то он должен определить все три.

**Правило пяти (C++11):** Добавляются:
- Конструктор перемещения
- Оператор присваивания с перемещением

**Правило нуля:** Лучше не управлять ресурсами вручную, а использовать RAII-обертки (`std::unique_ptr`, `std::shared_ptr`, `std::vector`, etc.)

```cpp
class Resource {
private:
    int* data;
    
public:
    // Конструктор
    Resource() {
        data = new int;
    }
    
    // Деструктор
    ~Resource() {
        delete data;
    }
    
    // Конструктор копирования
    Resource(const Resource& other) {
        data = new int(*other.data);
    }
    
    // Оператор присваивания
    Resource& operator=(const Resource& other) {
        if (this != &other) {
            delete data;
            data = new int(*other.data);
        }
        return *this;
    }
    
    // Конструктор перемещения (C++11)
    Resource(Resource&& other) noexcept : data(other.data) {
        other.data = nullptr;
    }
    
    // Оператор присваивания с перемещением (C++11)
    Resource& operator=(Resource&& other) noexcept {
        if (this != &other) {
            delete data;
            data = other.data;
            other.data = nullptr;
        }
        return *this;
    }
};
```

---

## 7. МЕТОДЫ КЛАССА {#методы-класса}

### 7.1 Определение методов

Методы — это функции, определенные внутри класса.

**Способы определения методов:**

1. **Внутри класса (inline по умолчанию):**
```cpp
class Point {
private:
    int x, y;
    
public:
    void set(int newX, int newY) {  // inline метод
        x = newX;
        y = newY;
    }
};
```

2. **Вне класса:**
```cpp
class Point {
private:
    int x, y;
    
public:
    void set(int newX, int newY);  // Объявление
    int getX();
};

// Определение вне класса
void Point::set(int newX, int newY) {
    x = newX;
    y = newY;
}

int Point::getX() {
    return x;
}
```

### 7.2 Константные методы

Методы, которые не изменяют состояние объекта:

```cpp
class Circle {
private:
    double radius;
    
public:
    Circle(double r) : radius(r) { }
    
    // Константный метод - не может изменять поля
    double getArea() const {
        // radius = 10;  // ОШИБКА! Нельзя изменять поля
        return 3.14159 * radius * radius;
    }
    
    double getRadius() const {
        return radius;
    }
    
    // Неконстантный метод
    void setRadius(double r) {
        radius = r;
    }
};

int main() {
    const Circle c1(5.0);
    double area = c1.getArea();  // OK - метод константный
    // c1.setRadius(10);         // ОШИБКА! Объект константный
}
```

### 7.3 Перегрузка методов

Методы с одинаковым именем, но разными параметрами:

```cpp
class Printer {
public:
    void print(int value) {
        std::cout << "Integer: " << value << std::endl;
    }
    
    void print(double value) {
        std::cout << "Double: " << value << std::endl;
    }
    
    void print(const std::string& value) {
        std::cout << "String: " << value << std::endl;
    }
    
    void print(int value, int width) {
        std::cout << std::setw(width) << value << std::endl;
    }
};
```

### 7.4 Параметры по умолчанию

```cpp
class Logger {
public:
    void log(const std::string& message, int level = 1) {
        std::cout << "[Level " << level << "] " << message << std::endl;
    }
};

int main() {
    Logger logger;
    logger.log("Сообщение");      // level = 1 (по умолчанию)
    logger.log("Ошибка", 3);      // level = 3
}
```

### 7.5 Inline методы

Методы, код которых вставляется в место вызова (для оптимизации):

```cpp
class Point {
private:
    int x, y;
    
public:
    // Определение внутри класса - автоматически inline
    int getX() const { return x; }
    
    // Явное указание inline
    inline int getY() const;
};

inline int Point::getY() const {
    return y;
}
```

### 7.6 Цепочки вызовов (Method Chaining)

Возврат ссылки на `*this` позволяет вызывать методы цепочкой:

```cpp
class StringBuilder {
private:
    std::string str;
    
public:
    StringBuilder& append(const std::string& s) {
        str += s;
        return *this;  // Возврат ссылки на себя
    }
    
    StringBuilder& appendLine(const std::string& s) {
        str += s + "\n";
        return *this;
    }
    
    std::string toString() const {
        return str;
    }
};

int main() {
    StringBuilder sb;
    std::string result = sb.append("Hello ")
                           .append("World")
                           .appendLine("!")
                           .append("C++ is awesome")
                           .toString();
}
```

---

## 8. УКАЗАТЕЛЬ THIS {#указатель-this}

### 8.1 Понятие указателя this

`this` — это неявный указатель на текущий объект, доступный во всех нестатических методах класса.

### 8.2 Использование this

```cpp
class Person {
private:
    std::string name;
    int age;
    
public:
    // Разрешение конфликта имен
    void setName(std::string name) {
        this->name = name;  // this->name - поле класса, name - параметр
    }
    
    // Возврат ссылки на объект
    Person& setAge(int age) {
        this->age = age;
        return *this;
    }
    
    // Сравнение с другим объектом
    bool isOlderThan(const Person& other) const {
        return this->age > other.age;
    }
    
    // Копирование с проверкой самоприсваивания
    Person& operator=(const Person& other) {
        if (this != &other) {  // Проверка this != &other
            this->name = other.name;
            this->age = other.age;
        }
        return *this;
    }
};
```

### 8.3 Когда this особенно полезен

1. **Разрешение конфликта имен**
2. **Возврат текущего объекта** для цепочки вызовов
3. **Проверка самоприсваивания**
4. **Передача текущего объекта** в другие функции

```cpp
class Node {
private:
    int value;
    Node* next;
    
public:
    Node(int v) : value(v), next(nullptr) { }
    
    // Добавление узла в конец списка
    Node* addNext(int v) {
        Node* newNode = new Node(v);
        this->next = newNode;
        return this;  // Возврат указателя на текущий узел
    }
};
```

---

## 9. СТАТИЧЕСКИЕ ЧЛЕНЫ КЛАССА
### 9.1 Статические поля

Статические поля принадлежат **классу**, а не конкретному объекту. Существует только одна копия статического поля для всех объектов.

```cpp
class Counter {
private:
    static int count;  // Объявление статического поля
    int id;
    
public:
    Counter() {
        count++;
        id = count;
    }
    
    ~Counter() {
        count--;
    }
    
    static int getCount() {  // Статический метод
        return count;
    }
    
    int getID() const {
        return id;
    }
};

// ОБЯЗАТЕЛЬНАЯ инициализация статического поля вне класса
int Counter::count = 0;

int main() {
    std::cout << "Счетчик: " << Counter::getCount() << std::endl;  // 0
    
    Counter c1;
    std::cout << "Счетчик: " << Counter::getCount() << std::endl;  // 1
    
    Counter c2, c3;
    std::cout << "Счетчик: " << Counter::getCount() << std::endl;  // 3
    
    std::cout << "ID объектов: " << c1.getID() << ", " 
              << c2.getID() << ", " << c3.getID() << std::endl;  // 1, 2, 3
}
```

### 9.2 Статические методы

Статические методы могут работать только со статическими членами класса:

```cpp
class Math {
public:
    static double PI;  // Статическая константа
    
    static double square(double x) {
        return x * x;
    }
    
    static double circleArea(double radius) {
        return PI * square(radius);
    }
};

double Math::PI = 3.14159265359;

int main() {
    double area = Math::circleArea(5.0);  // Вызов без создания объекта
    std::cout << "Площадь: " << area << std::endl;
}
```

### 9.3 Статические константы (inline static)

В C++17 можно инициализировать статические константы внутри класса:

```cpp
class Config {
public:
    inline static const int MAX_SIZE = 100;  // C++17
    inline static const std::string APP_NAME = "MyApp";  // C++17
};
```

До C++17:
```cpp
class Config {
public:
    static const int MAX_SIZE = 100;  // OK для integral типов
    static const std::string APP_NAME;  // Только объявление
};

// Инициализация вне класса
const std::string Config::APP_NAME = "MyApp";
```

### 9.4 Паттерн Singleton

Использование статических членов для создания единственного экземпляра класса:

```cpp
class Singleton {
private:
    static Singleton* instance;
    
    // Приватный конструктор
    Singleton() {
        std::cout << "Singleton создан\n";
    }
    
    // Запрет копирования
    Singleton(const Singleton&) = delete;
    Singleton& operator=(const Singleton&) = delete;
    
public:
    static Singleton* getInstance() {
        if (instance == nullptr) {
            instance = new Singleton();
        }
        return instance;
    }
    
    void doSomething() {
        std::cout << "Doing something...\n";
    }
};

Singleton* Singleton::instance = nullptr;

int main() {
    Singleton* s1 = Singleton::getInstance();
    Singleton* s2 = Singleton::getInstance();
    
    std::cout << "s1 и s2 - один объект? " 
              << (s1 == s2 ? "Да" : "Нет") << std::endl;  // Да
}
```

---

## 10. ПЕРЕГРУЗКА ОПЕРАТОРОВ

### 10.1 Понятие перегрузки операторов

Перегрузка операторов позволяет использовать стандартные операторы C++ (+, -, *, ==, etc.) с пользовательскими типами.

### 10.2 Синтаксис перегрузки

```cpp
возвращаемый_тип operator символ_оператора (параметры)
```

### 10.3 Арифметические операторы

```cpp
class Complex {
private:
    double real, imag;
    
public:
    Complex(double r = 0, double i = 0) : real(r), imag(i) { }
    
    // Перегрузка оператора + (как метод класса)
    Complex operator+(const Complex& other) const {
        return Complex(real + other.real, imag + other.imag);
    }
    
    // Перегрузка оператора - 
    Complex operator-(const Complex& other) const {
        return Complex(real - other.real, imag - other.imag);
    }
    
    // Перегрузка унарного минуса
    Complex operator-() const {
        return Complex(-real, -imag);
    }
    
    void print() const {
        std::cout << real;
        if (imag >= 0) std::cout << "+";
        std::cout << imag << "i" << std::endl;
    }
};

int main() {
    Complex c1(3, 4);    // 3+4i
    Complex c2(1, 2);    // 1+2i
    
    Complex c3 = c1 + c2;  // 4+6i
    Complex c4 = c1 - c2;  // 2+2i
    Complex c5 = -c1;      // -3-4i
    
    c3.print();
    c4.print();
    c5.print();
}
```

### 10.4 Операторы сравнения

```cpp
class Point {
private:
    int x, y;
    
public:
    Point(int x = 0, int y = 0) : x(x), y(y) { }
    
    // Оператор равенства
    bool operator==(const Point& other) const {
        return x == other.x && y == other.y;
    }
    
    // Оператор неравенства
    bool operator!=(const Point& other) const {
        return !(*this == other);  // Используем уже определенный ==
    }
    
    // Оператор "меньше" (лексикографическое сравнение)
    bool operator<(const Point& other) const {
        if (x != other.x) return x < other.x;
        return y < other.y;
    }
    
    bool operator>(const Point& other) const {
        return other < *this;
    }
    
    bool operator<=(const Point& other) const {
        return !(other < *this);
    }
    
    bool operator>=(const Point& other) const {
        return !(*this < other);
    }
};
```

### 10.5 Операторы присваивания

```cpp
class String {
private:
    char* str;
    int length;
    
public:
    String(const char* s = "") {
        length = strlen(s);
        str = new char[length + 1];
        strcpy(str, s);
    }
    
    ~String() {
        delete[] str;
    }
    
    // Оператор присваивания
    String& operator=(const String& other) {
        // Проверка самоприсваивания
        if (this == &other) {
            return *this;
        }
        
        // Освобождаем старую память
        delete[] str;
        
        // Копируем данные
        length = other.length;
        str = new char[length + 1];
        strcpy(str, other.str);
        
        // Возвращаем ссылку на себя
        return *this;
    }
    
    // Оператор += 
    String& operator+=(const String& other) {
        int newLength = length + other.length;
        char* newStr = new char[newLength + 1];
        
        strcpy(newStr, str);
        strcat(newStr, other.str);
        
        delete[] str;
        str = newStr;
        length = newLength;
        
        return *this;
    }
    
    void print() const {
        std::cout << str << std::endl;
    }
};
```

### 10.6 Операторы инкремента и декремента

```cpp
class Counter {
private:
    int value;
    
public:
    Counter(int v = 0) : value(v) { }
    
    // Префиксный инкремент: ++obj
    Counter& operator++() {
        ++value;
        return *this;
    }
    
    // Постфиксный инкремент: obj++
    Counter operator++(int) {  // int - фиктивный параметр для различения
        Counter temp = *this;
        ++value;
        return temp;  // Возврат старого значения
    }
    
    // Префиксный декремент: --obj
    Counter& operator--() {
        --value;
        return *this;
    }
    
    // Постфиксный декремент: obj--
    Counter operator--(int) {
        Counter temp = *this;
        --value;
        return temp;
    }
    
    int getValue() const { return value; }
};

int main() {
    Counter c(5);
    
    ++c;  // c = 6 (префиксный)
    c++;  // c = 7 (постфиксный)
    
    std::cout << c.getValue() << std::endl;  // 7
}
```

### 10.7 Оператор индексации

```cpp
class Array {
private:
    int* data;
    int size;
    
public:
    Array(int s) : size(s) {
        data = new int[size]();
    }
    
    ~Array() {
        delete[] data;
    }
    
    // Оператор [] для чтения и записи
    int& operator[](int index) {
        if (index < 0 || index >= size) {
            throw std::out_of_range("Индекс за пределами массива");
        }
        return data[index];
    }
    
    // Константная версия оператора []
    const int& operator[](int index) const {
        if (index < 0 || index >= size) {
            throw std::out_of_range("Индекс за пределами массива");
        }
        return data[index];
    }
    
    int getSize() const { return size; }
};

int main() {
    Array arr(5);
    
    arr[0] = 10;
    arr[1] = 20;
    
    std::cout << arr[0] << std::endl;  // 10
}
```

### 10.8 Операторы ввода-вывода

Операторы `<<` и `>>` удобнее определять как **friend функции**:

```cpp
class Point {
private:
    int x, y;
    
public:
    Point(int x = 0, int y = 0) : x(x), y(y) { }
    
    // Дружественные функции для потокового ввода-вывода
    friend std::ostream& operator<<(std::ostream& os, const Point& p);
    friend std::istream& operator>>(std::istream& is, Point& p);
};

// Оператор вывода
std::ostream& operator<<(std::ostream& os, const Point& p) {
    os << "(" << p.x << ", " << p.y << ")";
    return os;
}

// Оператор ввода
std::istream& operator>>(std::istream& is, Point& p) {
    is >> p.x >> p.y;
    return is;
}

int main() {
    Point p1(3, 4);
    std::cout << "Точка: " << p1 << std::endl;  // Точка: (3, 4)
    
    Point p2;
    std::cout << "Введите координаты: ";
    std::cin >> p2;
    std::cout << "Вы ввели: " << p2 << std::endl;
}
```

### 10.9 Оператор преобразования типа

```cpp
class Fraction {
private:
    int numerator, denominator;
    
public:
    Fraction(int n = 0, int d = 1) : numerator(n), denominator(d) { }
    
    // Оператор преобразования к double
    operator double() const {
        return static_cast<double>(numerator) / denominator;
    }
    
    // Explicit оператор преобразования к bool
    explicit operator bool() const {
        return numerator != 0;
    }
};

int main() {
    Fraction f(3, 4);
    
    double d = f;  // Неявное преобразование к double
    std::cout << d << std::endl;  // 0.75
    
    if (f) {  // Явное преобразование к bool
        std::cout << "Дробь не нулевая\n";
    }
    
    // bool b = f;  // ОШИБКА из-за explicit
}
```

### 10.10 Операторы, которые нельзя перегружать

Следующие операторы **нельзя перегружать**:
- `.` (доступ к членам)
- `::` (разрешение области видимости)
- `.*` (доступ к члену через указатель на член)
- `?:` (тернарный оператор)
- `sizeof`
- `typeid`

---

## 11. ДРУЖЕСТВЕННЫЕ ФУНКЦИИ И КЛАССЫ

### 11.1 Дружественные функции (friend)

**Дружественная функция** — это функция, не являющаяся членом класса, но имеющая доступ к приватным и защищенным членам класса.

```cpp
class Box {
private:
    double width, height, depth;
    
public:
    Box(double w, double h, double d) : width(w), height(h), depth(d) { }
    
    // Объявление дружественной функции
    friend double getVolume(const Box& box);
    friend void printBox(const Box& box);
};

// Определение дружественной функции (без Box::)
double getVolume(const Box& box) {
    // Доступ к приватным членам
    return box.width * box.height * box.depth;
}

void printBox(const Box& box) {
    std::cout << "Box: " << box.width << " x " 
              << box.height << " x " << box.depth << std::endl;
}

int main() {
    Box box(2.0, 3.0, 4.0);
    
    std::cout << "Объем: " << getVolume(box) << std::endl;
    printBox(box);
}
```

### 11.2 Зачем нужны дружественные функции?

1. **Симметричные бинарные операторы**
```cpp
class Complex {
private:
    double real, imag;
    
public:
    Complex(double r = 0, double i = 0) : real(r), imag(i) { }
    
    // Дружественная функция для симметричной операции
    friend Complex operator+(const Complex& c1, const Complex& c2);
    friend Complex operator*(double scalar, const Complex& c);
    friend Complex operator*(const Complex& c, double scalar);
};

Complex operator+(const Complex& c1, const Complex& c2) {
    return Complex(c1.real + c2.real, c1.imag + c2.imag);
}

Complex operator*(double scalar, const Complex& c) {
    return Complex(scalar * c.real, scalar * c.imag);
}

Complex operator*(const Complex& c, double scalar) {
    return scalar * c;  // Используем уже определенный оператор
}

int main() {
    Complex c1(3, 4);
    Complex c2 = 2.0 * c1;  // Возможно благодаря friend
    Complex c3 = c1 * 2.0;  // Тоже работает
}
```

2. **Операторы ввода-вывода**
```cpp
friend std::ostream& operator<<(std::ostream& os, const MyClass& obj);
friend std::istream& operator>>(std::istream& is, MyClass& obj);
```

3. **Доступ к приватным данным нескольких классов**
```cpp
class Meter;  // Предварительное объявление

class Centimeter {
private:
    double value;
    
public:
    Centimeter(double v) : value(v) { }
    friend Meter operator+(const Centimeter& cm, const Meter& m);
};

class Meter {
private:
    double value;
    
public:
    Meter(double v) : value(v) { }
    friend Meter operator+(const Centimeter& cm, const Meter& m);
};

Meter operator+(const Centimeter& cm, const Meter& m) {
    return Meter(m.value + cm.value / 100.0);
}
```

### 11.3 Дружественные классы

Весь класс может быть объявлен дружественным:

```cpp
class Storage {
private:
    int data[100];
    int size;
    
public:
    Storage() : size(0) { }
    
    // Класс Iterator - дружественный
    friend class Iterator;
};

class Iterator {
private:
    Storage* storage;
    int index;
    
public:
    Iterator(Storage* s) : storage(s), index(0) { }
    
    int next() {
        if (index < storage->size) {  // Доступ к приватному size
            return storage->data[index++];  // Доступ к приватному data
        }
        return -1;
    }
};
```

### 11.4 Ограничения дружественности

- **Дружба не наследуется:** если класс A — друг класса B, это не означает, что наследники A также друзья B
- **Дружба не взаимна:** если A — друг B, это не означает, что B — друг A
- **Дружба не транзитивна:** если A — друг B, и B — друг C, это не означает, что A — друг C

---

## 12. ПРИМЕРЫ ПРАКТИЧЕСКОГО ПРИМЕНЕНИЯ

### 12.1 Класс для работы с дробями

```cpp
#include <iostream>
#include <numeric>  // для std::gcd

class Fraction {
private:
    int numerator;
    int denominator;
    
    // Приватный метод для сокращения дроби
    void reduce() {
        int gcd = std::gcd(numerator, denominator);
        numerator /= gcd;
        denominator /= gcd;
        
        // Знак только в числителе
        if (denominator < 0) {
            numerator = -numerator;
            denominator = -denominator;
        }
    }
    
public:
    Fraction(int n = 0, int d = 1) : numerator(n), denominator(d) {
        if (denominator == 0) {
            throw std::invalid_argument("Знаменатель не может быть нулем");
        }
        reduce();
    }
    
    // Арифметические операции
    Fraction operator+(const Fraction& other) const {
        return Fraction(
            numerator * other.denominator + other.numerator * denominator,
            denominator * other.denominator
        );
    }
    
    Fraction operator-(const Fraction& other) const {
        return Fraction(
            numerator * other.denominator - other.numerator * denominator,
            denominator * other.denominator
        );
    }
    
    Fraction operator*(const Fraction& other) const {
        return Fraction(
            numerator * other.numerator,
            denominator * other.denominator
        );
    }
    
    Fraction operator/(const Fraction& other) const {
        return Fraction(
            numerator * other.denominator,
            denominator * other.numerator
        );
    }
    
    // Операторы сравнения
    bool operator==(const Fraction& other) const {
        return numerator == other.numerator && 
               denominator == other.denominator;
    }
    
    bool operator<(const Fraction& other) const {
        return numerator * other.denominator < 
               other.numerator * denominator;
    }
    
    // Преобразование к double
    explicit operator double() const {
        return static_cast<double>(numerator) / denominator;
    }
    
    // Вывод
    friend std::ostream& operator<<(std::ostream& os, const Fraction& f) {
        os << f.numerator << "/" << f.denominator;
        return os;
    }
};

int main() {
    Fraction f1(1, 2);   // 1/2
    Fraction f2(1, 3);   // 1/3
    
    Fraction f3 = f1 + f2;  // 5/6
    std::cout << f1 << " + " << f2 << " = " << f3 << std::endl;
    
    Fraction f4 = f1 * f2;  // 1/6
    std::cout << f1 << " * " << f2 << " = " << f4 << std::endl;
}
```

### 12.2 Класс динамического массива

```cpp
template <typename T>
class DynamicArray {
private:
    T* data;
    size_t size;
    size_t capacity;
    
    void resize(size_t newCapacity) {
        T* newData = new T[newCapacity];
        for (size_t i = 0; i < size; i++) {
            newData[i] = data[i];
        }
        delete[] data;
        data = newData;
        capacity = newCapacity;
    }
    
public:
    DynamicArray() : data(nullptr), size(0), capacity(0) { }
    
    explicit DynamicArray(size_t initialCapacity) 
        : size(0), capacity(initialCapacity) {
        data = new T[capacity];
    }
    
    ~DynamicArray() {
        delete[] data;
    }
    
    // Конструктор копирования
    DynamicArray(const DynamicArray& other) 
        : size(other.size), capacity(other.capacity) {
        data = new T[capacity];
        for (size_t i = 0; i < size; i++) {
            data[i] = other.data[i];
        }
    }
    
    // Оператор присваивания
    DynamicArray& operator=(const DynamicArray& other) {
        if (this != &other) {
            delete[] data;
            size = other.size;
            capacity = other.capacity;
            data = new T[capacity];
            for (size_t i = 0; i < size; i++) {
                data[i] = other.data[i];
            }
        }
        return *this;
    }
    
    void push_back(const T& value) {
        if (size == capacity) {
            resize(capacity == 0 ? 1 : capacity * 2);
        }
        data[size++] = value;
    }
    
    void pop_back() {
        if (size > 0) {
            size--;
        }
    }
    
    T& operator[](size_t index) {
        return data[index];
    }
    
    const T& operator[](size_t index) const {
        return data[index];
    }
    
    size_t getSize() const { return size; }
    size_t getCapacity() const { return capacity; }
    bool isEmpty() const { return size == 0; }
    
    void clear() {
        size = 0;
    }
};
```

### 12.3 Класс для работы с комплексными числами

```cpp
class Complex {
private:
    double real, imag;
    
public:
    Complex(double r = 0, double i = 0) : real(r), imag(i) { }
    
    // Геттеры
    double getReal() const { return real; }
    double getImag() const { return imag; }
    
    // Модуль комплексного числа
    double abs() const {
        return std::sqrt(real * real + imag * imag);
    }
    
    // Аргумент (фаза)
    double arg() const {
        return std::atan2(imag, real);
    }
    
    // Сопряженное число
    Complex conjugate() const {
        return Complex(real, -imag);
    }
    
    // Арифметические операции
    Complex operator+(const Complex& other) const {
        return Complex(real + other.real, imag + other.imag);
    }
    
    Complex operator-(const Complex& other) const {
        return Complex(real - other.real, imag - other.imag);
    }
    
    Complex operator*(const Complex& other) const {
        return Complex(
            real * other.real - imag * other.imag,
            real * other.imag + imag * other.real
        );
    }
    
    Complex operator/(const Complex& other) const {
        double denominator = other.real * other.real + 
                           other.imag * other.imag;
        return Complex(
            (real * other.real + imag * other.imag) / denominator,
            (imag * other.real - real * other.imag) / denominator
        );
    }
    
    // Вывод
    friend std::ostream& operator<<(std::ostream& os, const Complex& c) {
        os << c.real;
        if (c.imag >= 0) os << "+";
        os << c.imag << "i";
        return os;
    }
};
```
