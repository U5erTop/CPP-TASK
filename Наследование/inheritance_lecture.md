# Наследование в C++

---

## 1. Введение в наследование

**Наследование** — фундаментальный механизм объектно-ориентированного программирования, позволяющий создавать новый класс на основе существующего. Новый класс (**производный**, derived) получает все поля и методы **базового** (base) класса и может добавлять собственные или переопределять унаследованные.

```
Базовый класс (Animal)
        │
        ├── Производный класс (Dog)
        ├── Производный класс (Cat)
        └── Производный класс (Bird)
```

### Зачем нужно наследование?

- **Повторное использование кода** — не переписывать общую логику снова
- **Расширяемость** — добавлять функциональность без изменения базового класса
- **Полиморфизм** — обрабатывать разные типы через единый интерфейс
- **Моделирование реального мира** — "Собака — это Животное" (is-a relationship)

### Отличие "is-a" от "has-a"

| Отношение            | Реализация   | Пример                        |
| -------------------- | ------------ | ----------------------------- |
| **is-a** (является)  | Наследование | Собака — это Животное         |
| **has-a** (содержит) | Композиция   | Автомобиль содержит Двигатель |

---

## 2. Синтаксис наследования

```cpp
class Производный : спецификатор Базовый {
    // дополнительные поля и методы
};
```

Пример:

```cpp
class Animal {
public:
    std::string name;
    int age;

    Animal(std::string n, int a) : name(n), age(a) {}

    void breathe() {
        std::cout << name << " дышит\n";
    }
};

class Dog : public Animal {        // Dog наследует Animal
    std::string breed;
public:
    Dog(std::string n, int a, std::string b)
        : Animal(n, a), breed(b) {}   // вызов конструктора базового класса

    void bark() {
        std::cout << name << " лает: Гав!\n";   // name унаследован
    }
};

int main() {
    Dog d("Рекс", 3, "Овчарка");
    d.breathe();   // унаследованный метод
    d.bark();      // собственный метод
}
```

---

## 3. Спецификаторы доступа при наследовании

Спецификатор доступа при наследовании определяет, как члены базового класса становятся доступны в производном.

### Таблица доступа

| Член базового класса | `public` наследование | `protected` наследование | `private` наследование |
| -------------------- | --------------------- | ------------------------ | ---------------------- |
| `public`             | `public`              | `protected`              | `private`              |
| `protected`          | `protected`           | `protected`              | `private`              |
| `private`            | недоступен            | недоступен               | недоступен             |

```cpp
class Base {
public:
    int pub;       // доступен всем
protected:
    int prot;      // доступен Base и производным
private:
    int priv;      // доступен только Base
};

class PublicDerived : public Base {
    void f() {
        pub  = 1;   // OK — остаётся public
        prot = 2;   // OK — остаётся protected
        // priv = 3; — ОШИБКА
    }
};

class PrivateDerived : private Base {
    void f() {
        pub  = 1;   // OK — становится private
        prot = 2;   // OK — становится private
    }
};
```

> **Правило Шилдта:** почти всегда используйте `public` наследование. `private` и `protected` наследование — особые случаи ограничения интерфейса.

---

## 4. Конструкторы и деструкторы при наследовании

### Порядок вызова конструкторов

Конструкторы вызываются **от базового к производному** (сначала базовый, затем производный):

```cpp
class A {
public:
    A() { std::cout << "Конструктор A\n"; }
    ~A() { std::cout << "Деструктор A\n"; }
};

class B : public A {
public:
    B() { std::cout << "Конструктор B\n"; }
    ~B() { std::cout << "Деструктор B\n"; }
};

class C : public B {
public:
    C() { std::cout << "Конструктор C\n"; }
    ~C() { std::cout << "Деструктор C\n"; }
};

int main() {
    C obj;
}
```

Вывод:

```
Конструктор A
Конструктор B
Конструктор C
Деструктор C
Деструктор B
Деструктор A
```

Деструкторы вызываются в **обратном порядке** — от производного к базовому.

### Передача аргументов базовому конструктору

```cpp
class Shape {
    std::string color;
public:
    Shape(std::string c) : color(c) {
        std::cout << "Создана фигура цвета " << color << "\n";
    }
    std::string getColor() const { return color; }
};

class Circle : public Shape {
    double radius;
public:
    Circle(double r, std::string c)
        : Shape(c),       // явный вызов конструктора базового класса
          radius(r)
    {
        std::cout << "Создан круг с радиусом " << radius << "\n";
    }
};
```

> **Важно:** базовый конструктор вызывается в **списке инициализации**, а не в теле конструктора производного класса.

---

## 5. Переопределение методов (Overriding)

Производный класс может **переопределить** (override) метод базового класса, объявив метод с тем же именем и сигнатурой:

```cpp
class Animal {
public:
    void speak() {
        std::cout << "Животное издаёт звук\n";
    }
};

class Dog : public Animal {
public:
    void speak() {          // переопределение
        std::cout << "Гав!\n";
    }
};

int main() {
    Dog d;
    d.speak();              // выводит "Гав!"
    d.Animal::speak();      // явный вызов базового: "Животное издаёт звук"
}
```

### Скрытие vs. Переопределение

```cpp
class Base {
public:
    void f(int x) { std::cout << "Base::f(int)\n"; }
};

class Derived : public Base {
public:
    void f(double x) { std::cout << "Derived::f(double)\n"; }
    // ВНИМАНИЕ: Base::f(int) теперь СКРЫТ, а не перегружен!
};

int main() {
    Derived d;
    d.f(1.0);    // Derived::f(double)
    d.f(1);      // Derived::f(double) — скрыт Base::f(int)!
    // Чтобы восстановить: using Base::f;
}
```

---

## 6. Виртуальные функции и полиморфизм

**Виртуальная функция** — функция базового класса, которую производный класс может переопределить, и это переопределение будет вызвано **через указатель/ссылку на базовый класс** во время выполнения.

```cpp
class Shape {
public:
    virtual double area() const {     // виртуальная функция
        return 0.0;
    }

    virtual void print() const {
        std::cout << "Фигура, площадь = " << area() << "\n";
    }

    virtual ~Shape() {}               // ВАЖНО: виртуальный деструктор!
};

class Circle : public Shape {
    double r;
public:
    Circle(double r) : r(r) {}
    double area() const override {    // override — проверка компилятором
        return 3.14159 * r * r;
    }
};

class Rectangle : public Shape {
    double w, h;
public:
    Rectangle(double w, double h) : w(w), h(h) {}
    double area() const override {
        return w * h;
    }
};

int main() {
    Shape* shapes[] = {
        new Circle(5),
        new Rectangle(4, 6),
        new Circle(3)
    };

    for (auto* s : shapes) {
        s->print();        // вызывается нужная area() — полиморфизм!
        delete s;
    }
}
```

### Механизм виртуальных функций: vtable

Каждый класс с виртуальными функциями имеет **таблицу виртуальных функций (vtable)**:

```
Объект Circle:
  [vptr] ──────→ vtable Circle
  [r]              [area()]  ──→ Circle::area
                   [print()] ──→ Shape::print
                   [~Shape()] ──→ Circle::~Circle
```

- `vptr` — скрытый указатель в каждом объекте на vtable своего класса
- При вызове `s->area()` идёт **разыменование через vptr** → небольшой overhead
- Статическое связывание (без `virtual`) не требует vtable → быстрее

---

## 7. Ключевые слова override и final (C++11)

```cpp
class Base {
public:
    virtual void foo(int x) {}
    virtual void bar() {}
};

class Derived : public Base {
public:
    void foo(int x) override {}   // OK — компилятор проверит совпадение сигнатуры
    // void foo(double x) override {}  — ОШИБКА компиляции: сигнатура не совпадает

    void bar() final {}           // final — нельзя переопределить дальше
};

class Further : public Derived {
    // void bar() override {}     — ОШИБКА: bar() объявлен final
};

class SealedClass final : public Base {  // final на классе — нельзя наследоваться
};
```

> **Совет от Шилдта:** всегда пишите `override` при переопределении. Это защитит от опечаток в сигнатуре.

---

## 8. Чисто виртуальные функции и абстрактные классы

**Чисто виртуальная функция** — виртуальная функция без реализации в базовом классе:

```cpp
virtual тип имя(параметры) = 0;
```

Класс с хотя бы одной чисто виртуальной функцией становится **абстрактным**:

```cpp
class AbstractAnimal {      // абстрактный класс
public:
    virtual void speak() = 0;    // чисто виртуальная
    virtual void move() = 0;     // чисто виртуальная

    void breathe() {             // обычная функция — реализована
        std::cout << "Дышит\n";
    }

    virtual ~AbstractAnimal() {}
};

// AbstractAnimal a;  — ОШИБКА: нельзя создать объект абстрактного класса

class Dog : public AbstractAnimal {
public:
    void speak() override { std::cout << "Гав!\n"; }
    void move() override  { std::cout << "Бежит\n"; }
};
```

### Абстрактный класс как интерфейс

```cpp
class IDrawable {           // "интерфейс" — только чисто виртуальные функции
public:
    virtual void draw() = 0;
    virtual void resize(double factor) = 0;
    virtual ~IDrawable() {}
};

class ISerializable {
public:
    virtual std::string serialize() const = 0;
    virtual void deserialize(const std::string& data) = 0;
    virtual ~ISerializable() {}
};

// Множественное наследование интерфейсов:
class Widget : public IDrawable, public ISerializable {
public:
    void draw() override { /* ... */ }
    void resize(double f) override { /* ... */ }
    std::string serialize() const override { return "widget_data"; }
    void deserialize(const std::string& d) override { /* ... */ }
};
```

---

## 9. Виртуальный деструктор

**Проблема:** если уничтожать объект производного класса через указатель на базовый без виртуального деструктора — произойдёт **утечка памяти**:

```cpp
class Base {
public:
    ~Base() { std::cout << "~Base\n"; }        // НЕ виртуальный — ОШИБКА
};

class Derived : public Base {
    int* data;
public:
    Derived() : data(new int[100]) {}
    ~Derived() { delete[] data; std::cout << "~Derived\n"; }
};

int main() {
    Base* p = new Derived();
    delete p;   // вызовет только ~Base — утечка памяти из data!
}
```

**Решение:** всегда объявляйте деструктор базового класса виртуальным:

```cpp
class Base {
public:
    virtual ~Base() { std::cout << "~Base\n"; }  // виртуальный
};
// Теперь delete p вызовет ~Derived, затем ~Base — правильно
```

> **Правило Шилдта:** если в классе есть хотя бы одна виртуальная функция — деструктор тоже должен быть виртуальным.

---

## 10. Множественное наследование

C++ позволяет классу наследовать от **нескольких базовых классов**:

```cpp
class Flyable {
public:
    virtual void fly() { std::cout << "Летит\n"; }
};

class Swimmable {
public:
    virtual void swim() { std::cout << "Плывёт\n"; }
};

class Duck : public Flyable, public Swimmable {
public:
    void fly()  override { std::cout << "Утка летит\n"; }
    void swim() override { std::cout << "Утка плывёт\n"; }
    void quack() { std::cout << "Кря!\n"; }
};
```

### Проблема ромбовидного наследования

```
       Animal
      /       \
    Dog        Cat
      \       /
       DogCat (?)
```

```cpp
class Animal {
public:
    int id = 0;
    void breathe() { std::cout << "Дышит\n"; }
};

class Dog : public Animal {};
class Cat : public Animal {};

class DogCat : public Dog, public Cat {
    // Конфликт: два экземпляра Animal!
    // DogCat::Dog::Animal и DogCat::Cat::Animal
};

DogCat dc;
// dc.id = 1;         — ОШИБКА: неоднозначность
dc.Dog::id = 1;       // OK — явное разрешение
dc.Cat::id = 2;       // OK — другой экземпляр!
```

---

## 11. Виртуальное наследование

**Виртуальное наследование** решает проблему ромба — гарантирует **один общий экземпляр** базового класса:

```cpp
class Animal {
public:
    int id;
    Animal(int i) : id(i) {}
    virtual void breathe() { std::cout << "Дышит\n"; }
};

class Dog : virtual public Animal {    // virtual!
public:
    Dog() : Animal(0) {}
};

class Cat : virtual public Animal {    // virtual!
public:
    Cat() : Animal(0) {}
};

class DogCat : public Dog, public Cat {
public:
    DogCat() : Animal(42), Dog(), Cat() {}  // Animal инициализируется ОДИН раз
};

int main() {
    DogCat dc;
    dc.id = 1;      // OK — только один экземпляр Animal
    dc.breathe();   // OK — нет неоднозначности
}
```

### Порядок инициализации при виртуальном наследовании

При виртуальном наследовании конструктор **самого производного класса** напрямую инициализирует виртуальную базу:

```
Порядок: Animal → Dog → Cat → DogCat
```

---

## 12. Приведение типов при наследовании

### Upcasting (к базовому) — безопасно, неявно

```cpp
Dog* dog = new Dog("Рекс", 3, "Овчарка");
Animal* animal = dog;      // upcasting — всегда безопасно
animal->breathe();         // OK
```

### Downcasting (к производному) — опасно, явно

```cpp
Animal* animal = new Dog("Рекс", 3, "Овчарка");

// Небезопасно:
Dog* dog = static_cast<Dog*>(animal);  // OK, если уверены в типе

// Безопасно — с проверкой типа:
Dog* dog2 = dynamic_cast<Dog*>(animal);
if (dog2) {
    dog2->bark();    // OK
} else {
    std::cout << "Не Dog!\n";
}
```

### Четыре вида приведений

| Приведение            | Назначение                           | Безопасность |
| --------------------- | ------------------------------------ | ------------ |
| `static_cast<T>`      | Upcasting / downcasting без проверки | Среднее      |
| `dynamic_cast<T>`     | Downcasting с проверкой типа (RTTI)  | Высокое      |
| `const_cast<T>`       | Снятие/добавление `const`            | Специальное  |
| `reinterpret_cast<T>` | Побитовое переинтерпретирование      | Низкое       |

---

## 13. RTTI — информация о типах во время выполнения

```cpp
#include <typeinfo>

class Animal { virtual ~Animal(){} };
class Dog : public Animal {};
class Cat : public Animal {};

int main() {
    Animal* a = new Dog();

    // typeid — возвращает информацию о типе
    std::cout << typeid(*a).name() << "\n";    // Dog (зависит от компилятора)

    // dynamic_cast — безопасное приведение
    if (Dog* d = dynamic_cast<Dog*>(a)) {
        std::cout << "Это Dog!\n";
    }

    // Проверка типа
    if (typeid(*a) == typeid(Dog)) {
        std::cout << "Тип совпадает\n";
    }

    delete a;
}
```

> **RTTI работает только** для классов с хотя бы одной виртуальной функцией (полиморфных классов).

---

## 14. Полиморфизм: статический и динамический

### Статический полиморфизм (время компиляции)

```cpp
// Шаблоны (compile-time polymorphism)
template<typename T>
void printArea(const T& shape) {
    std::cout << "Площадь: " << shape.area() << "\n";
}
```

### Динамический полиморфизм (время выполнения)

```cpp
void printArea(const Shape* shape) {
    std::cout << "Площадь: " << shape->area() << "\n";  // virtual dispatch
}
```

### Пример: система фигур

```cpp
class Shape {
public:
    virtual double area() const = 0;
    virtual double perimeter() const = 0;
    virtual std::string name() const = 0;
    virtual ~Shape() {}

    void printInfo() const {
        std::cout << name() << ": площадь=" << area()
                  << ", периметр=" << perimeter() << "\n";
    }
};

class Circle : public Shape {
    double r;
public:
    Circle(double r) : r(r) {}
    double area() const override { return 3.14159 * r * r; }
    double perimeter() const override { return 2 * 3.14159 * r; }
    std::string name() const override { return "Круг"; }
};

class Rectangle : public Shape {
    double w, h;
public:
    Rectangle(double w, double h) : w(w), h(h) {}
    double area() const override { return w * h; }
    double perimeter() const override { return 2 * (w + h); }
    std::string name() const override { return "Прямоугольник"; }
};

class Triangle : public Shape {
    double a, b, c;
public:
    Triangle(double a, double b, double c) : a(a), b(b), c(c) {}
    double perimeter() const override { return a + b + c; }
    double area() const override {
        double s = perimeter() / 2;
        return sqrt(s*(s-a)*(s-b)*(s-c));
    }
    std::string name() const override { return "Треугольник"; }
};

int main() {
    std::vector<Shape*> shapes = {
        new Circle(5),
        new Rectangle(4, 6),
        new Triangle(3, 4, 5)
    };

    for (auto* s : shapes) {
        s->printInfo();
        delete s;
    }
}
```

---

## 15. Наследование и конструктор копирования

```cpp
class Base {
    int x;
public:
    Base(int x) : x(x) {}
    Base(const Base& other) : x(other.x) {
        std::cout << "Копирование Base\n";
    }
    Base& operator=(const Base& other) {
        x = other.x;
        return *this;
    }
};

class Derived : public Base {
    int y;
public:
    Derived(int x, int y) : Base(x), y(y) {}

    // Конструктор копирования — ЯВНО вызывает базовый
    Derived(const Derived& other) : Base(other), y(other.y) {
        std::cout << "Копирование Derived\n";
    }

    // Оператор присваивания
    Derived& operator=(const Derived& other) {
        if (this != &other) {
            Base::operator=(other);   // копируем базовую часть
            y = other.y;
        }
        return *this;
    }
};
```

> **Внимание:** если не вызвать `Base(other)` в конструкторе копирования — базовая часть будет инициализирована конструктором по умолчанию, а не скопирована!

---

## 16. Делегирующие конструкторы и наследование конструкторов (C++11)

### Наследование конструкторов через using

```cpp
class Base {
public:
    Base(int x) { std::cout << "Base(" << x << ")\n"; }
    Base(int x, int y) { std::cout << "Base(" << x << "," << y << ")\n"; }
};

class Derived : public Base {
public:
    using Base::Base;   // наследуем ВСЕ конструкторы Base

    // Теперь можно:
    // Derived(int x)       — автоматически делегирует Base(x)
    // Derived(int x, int y) — автоматически делегирует Base(x, y)
};

int main() {
    Derived d1(5);       // вызовет Base(5)
    Derived d2(3, 4);    // вызовет Base(3, 4)
}
```

---

## 17. Скрытие имён и ключевое слово using

```cpp
class Base {
public:
    void f(int x)    { std::cout << "Base::f(int)\n"; }
    void f(double x) { std::cout << "Base::f(double)\n"; }
};

class Derived : public Base {
public:
    using Base::f;     // открываем все перегрузки f из Base

    void f(std::string s) { std::cout << "Derived::f(string)\n"; }
    // Теперь все три версии доступны
};

int main() {
    Derived d;
    d.f(1);        // Base::f(int)
    d.f(3.14);     // Base::f(double)
    d.f("hello");  // Derived::f(string)
}
```

---

## 18. Невиртуальный интерфейс (NVI — Non-Virtual Interface)

Идиома, рекомендуемая Шилдтом и современными практиками:

```cpp
class Base {
public:
    // Публичный невиртуальный метод — "шаблонный метод"
    void process() {
        preProcess();    // hook — может переопределить производный
        doProcess();     // чисто виртуальный — ОБЯЗАН переопределить
        postProcess();   // hook
    }

private:
    virtual void preProcess()  { std::cout << "Предобработка\n"; }
    virtual void doProcess() = 0;
    virtual void postProcess() { std::cout << "Постобработка\n"; }
};

class ConcreteA : public Base {
    void doProcess() override { std::cout << "Обработка A\n"; }
};

class ConcreteB : public Base {
    void preProcess() override { std::cout << "Особая предобработка B\n"; }
    void doProcess() override  { std::cout << "Обработка B\n"; }
};
```

---

## 19. Итоговая таблица: ключевые понятия наследования

| Понятие                  | Ключевое слово   | Описание                                    |
| ------------------------ | ---------------- | ------------------------------------------- |
| Публичное наследование   | `public`         | is-a, интерфейс базового сохраняется        |
| Защищённое наследование  | `protected`      | Интерфейс скрыт извне                       |
| Приватное наследование   | `private`        | Реализация через базовый класс              |
| Виртуальная функция      | `virtual`        | Динамическое связывание                     |
| Чисто виртуальная        | `= 0`            | Абстрактный класс                           |
| Переопределение          | `override`       | Явная проверка компилятором                 |
| Запрет переопределения   | `final`          | Заморозка метода или класса                 |
| Виртуальный деструктор   | `virtual ~T()`   | Корректное удаление через базовый указатель |
| Виртуальное наследование | `virtual public` | Один экземпляр базового при ромбе           |
| Безопасное приведение    | `dynamic_cast`   | Проверка типа во время выполнения           |

---

---

# 200 Практических задач по наследованию в C++

---

## Блок 1: Базовое наследование (задачи 1–25)

**1.** Создайте класс `Animal` с полями `name` и `age`, методом `speak()`. Создайте класс `Dog : public Animal` с методом `bark()`.

**2.** Для задачи 1 добавьте класс `Cat : public Animal` с методом `purr()`.

**3.** Создайте иерархию: `Vehicle → Car → ElectricCar`. Каждый уровень добавляет одно поле и один метод.

**4.** Создайте класс `Person` (имя, возраст). Наследуйте от него `Student` (добавьте номер зачётки и GPA).

**5.** От `Student` наследуйте `GraduateStudent` (добавьте тему диссертации).

**6.** Создайте `Shape` (цвет). Наследуйте `Circle` (радиус) и `Rectangle` (ширина, высота).

**7.** Для задачи 6 добавьте `Triangle` (три стороны).

**8.** Создайте `BankAccount` (баланс, номер счёта). Наследуйте `SavingsAccount` (процентная ставка).

**9.** Наследуйте от `BankAccount` класс `CreditAccount` (кредитный лимит).

**10.** Создайте иерархию `Employee → Manager → Director`. Каждый уровень добавляет уровень зарплаты.

**11.** Создайте `Fruit` с методом `taste()`. Наследуйте `Apple`, `Orange`, `Banana` с переопределением `taste()`.

**12.** Создайте `Furniture` (материал, вес). Наследуйте `Chair` (количество ног) и `Table` (площадь поверхности).

**13.** Создайте `Device` (производитель, мощность). Наследуйте `Phone`, `Laptop`, `Tablet`.

**14.** Создайте `Weapon` (урон). Наследуйте `Sword`, `Bow`, `Staff` с переопределением метода `attack()`.

**15.** Создайте класс `Game` с методами `start()`, `pause()`, `stop()`. Наследуйте `RPGGame` с добавлением инвентаря.

**16.** Создайте иерархию `Polygon → Quadrilateral → Parallelogram → Rhombus`.

**17.** Создайте `LivingThing → Plant → Tree → OakTree`. Каждый уровень добавляет поведение.

**18.** Создайте `Media → Audio → Song`. У `Song` — название, исполнитель, длительность.

**19.** Создайте `Vehicle → Boat → Yacht`. `Yacht` имеет тип паруса и длину.

**20.** Создайте класс `Container` (объём). Наследуйте `Box`, `Sphere`, `Cylinder`.

**21.** Для задачи 20 добавьте метод `volume()` в каждый класс, вычисляющий объём по формуле.

**22.** Создайте класс `Animal` с виртуальным методом `describe()`. В `Dog` и `Cat` переопределите его.

**23.** Создайте `Sensor → TemperatureSensor → ThermostatSensor`. Добавьте методы чтения и установки порога.

**24.** Создайте `File` (имя, размер). Наследуйте `TextFile` (кодировка) и `BinaryFile` (тип).

**25.** Создайте иерархию `Exception → NetworkException → TimeoutException`. Добавьте метод `getMessage()`.

---

## Блок 2: Конструкторы и деструкторы (задачи 26–50)

**26.** Продемонстрируйте порядок вызова конструкторов и деструкторов в цепочке `A → B → C`.

**27.** Создайте `Base` с конструктором, принимающим `int`. Создайте `Derived`, передающий значение через список инициализации.

**28.** Создайте класс `Resource` с динамическим массивом. Наследуйте `ManagedResource` и корректно реализуйте деструкторы.

**29.** Докажите утечку памяти при невиртуальном деструкторе: добавьте вывод в деструкторы и удаляйте через базовый указатель.

**30.** Исправьте задачу 29: сделайте деструктор базового класса виртуальным.

**31.** Создайте `Sensor(std::string name)` и наследуйте `GPS(std::string name, double lat, double lon)` с передачей `name` базовому.

**32.** В иерархии `A → B → C` у каждого конструктора разные параметры — передайте нужные значения вниз по цепочке.

**33.** Используйте `using Base::Base` для наследования конструктора.

**34.** Создайте `Logger` с конструктором, открывающим файл. Наследуйте `TimestampLogger`. Проверьте, что файл закрывается в деструкторе.

**35.** Создайте `Widget` и `Button : public Widget`. Реализуйте конструктор копирования в `Button`, явно копирующий часть `Widget`.

**36.** Реализуйте оператор присваивания в `Button`, вызывая `Widget::operator=`.

**37.** Создайте `Base` с `Base(const Base&) = delete`. Попробуйте создать копию `Derived` — объясните ошибку.

**38.** Создайте `Base` с `protected` конструктором. Убедитесь, что `Derived` может его вызвать, а внешний код — нет.

**39.** Реализуйте иерархию с `= default` конструктором копирования на каждом уровне и проверьте корректность.

**40.** Создайте `abstract Factory` с виртуальным деструктором. Наследуйте `ConcreteFactory`. Убедитесь, что удаление через `Factory*` корректно.

**41.** В классе `Derived` добавьте статическое поле `count`. Инкрементируйте в конструкторе, декрементируйте в деструкторе. Выводите количество живых объектов.

**42.** Создайте `Base` и `Derived` с `noexcept` деструкторами. Объясните, зачем `noexcept` в деструкторах.

**43.** Реализуйте move-конструктор и move-оператор присваивания в `Derived`, делегируя `Base`.

**44.** Реализуйте иерархию `Socket → TcpSocket → HttpSocket`. В конструкторе симулируйте открытие соединения, в деструкторе — закрытие.

**45.** Напишите класс `Derived` с конструктором делегирования: `Derived(int x) : Derived(x, 0) {}`.

**46.** Создайте `Vehicle(int speed, int fuel)`. Наследуйте `Car(int speed, int fuel, int doors)`. Передавайте `speed` и `fuel` базовому.

**47.** Создайте иерархию из 4 уровней. В каждом конструкторе выводите `"Создан уровень N"`. Создайте объект самого глубокого типа и убедитесь в правильном порядке.

**48.** Реализуйте `Singleton` через наследование: `BaseSingleton` с методом `getInstance()`, `DerivedSingleton` расширяет функциональность.

**49.** Создайте `ICloneable` с чисто виртуальным методом `clone()`. Реализуйте в `Circle` и `Rectangle`, возвращающих копию через `new`.

**50.** Для задачи 49 напишите функцию `copyShapes(vector<Shape*>)`, создающую глубокую копию массива через `clone()`.

---

## Блок 3: Виртуальные функции и полиморфизм (задачи 51–80)

**51.** Создайте `Shape` с виртуальным `area()`. Реализуйте в `Circle` и `Rectangle`. Вызовите через `Shape*`.

**52.** Добавьте в задачу 51 `Triangle`. Поместите все три в `vector<Shape*>` и посчитайте суммарную площадь.

**53.** Создайте `Animal` с виртуальным `speak()`. В цикле через `vector<Animal*>` заставьте каждое животное говорить.

**54.** Продемонстрируйте разницу: вызов `virtual` через указатель vs. через объект (статическое связывание).

**55.** Создайте `Printer` с виртуальным `print(Document)`. Наследуйте `ColorPrinter` и `LaserPrinter` с разным поведением.

**56.** Создайте `Logger` с виртуальным `log(string)`. Наследуйте `FileLogger`, `ConsoleLogger`, `NetworkLogger`.

**57.** Создайте `UIElement` с виртуальными `draw()` и `handleClick()`. Наследуйте `Button`, `Checkbox`, `TextField`.

**58.** Добавьте невиртуальный метод `render()` в `UIElement`, вызывающий `draw()`. Продемонстрируйте NVI-идиому.

**59.** Создайте `Sorter` с виртуальным `sort(vector<int>&)`. Наследуйте `BubbleSorter`, `QuickSorter`, `MergeSorter`.

**60.** Используйте `Sorter*` в функции `benchmark(Sorter*, vector<int>)` для замера времени разных алгоритмов.

**61.** Создайте `Compressor` с виртуальным `compress(string)`. Наследуйте `RLECompressor` и `ZlibCompressor`.

**62.** Создайте иерархию `Event → MouseEvent → ClickEvent`. Виртуальный метод `handle()`.

**63.** Создайте `Validator` с виртуальным `validate(string)`. Наследуйте `EmailValidator`, `PhoneValidator`, `PasswordValidator`.

**64.** Создайте `Game` с виртуальными `update()` и `render()`. Наследуйте `PlatformerGame` и `PuzzleGame`.

**65.** Создайте базовый класс `Expression` с виртуальным `evaluate()`. Наследуйте `Number`, `Add`, `Multiply` — AST-дерево.

**66.** Создайте `Protocol` с виртуальными `encode(string)` и `decode(string)`. Наследуйте `JsonProtocol` и `XmlProtocol`.

**67.** Создайте `Strategy` с виртуальным `execute()`. Реализуйте паттерн Strategy через наследование.

**68.** Создайте `Observer` с виртуальным `update(Event)`. Реализуйте паттерн Observer: `Subject` хранит `vector<Observer*>`.

**69.** Создайте `Command` с виртуальными `execute()` и `undo()`. Реализуйте `HistoryManager` с `vector<Command*>`.

**70.** Создайте `Iterator<T>` с виртуальными `hasNext()` и `next()`. Наследуйте `VectorIterator<T>`.

**71.** Продемонстрируйте срезку объекта (slicing): что происходит при копировании `Dog` в переменную типа `Animal`.

**72.** Исправьте проблему срезки через использование `Animal*` вместо `Animal`.

**73.** Создайте виртуальный метод `toString()` в `Animal`. Переопределите в `Dog` и `Cat`. Используйте в `operator<<`.

**74.** Перегрузите `operator<<` для базового класса `Shape`, используя виртуальный метод `print()`.

**75.** Создайте `Decorator` (паттерн): `Coffee → MilkDecorator → SugarDecorator`. Каждый добавляет к стоимости.

**76.** Создайте `FileReader` с виртуальным `read()`. Наследуйте `CachedFileReader`, переопределив `read()` с кэшированием.

**77.** Реализуйте паттерн `Template Method`: `DataProcessor` с виртуальными хуками `readData()`, `processData()`, `writeData()`.

**78.** Создайте `Renderer` с виртуальным `render()`. Наследуйте `OpenGLRenderer` и `VulkanRenderer`.

**79.** Реализуйте метод `clone()` через виртуальные функции (паттерн `Prototype`) для иерархии `Shape`.

**80.** Создайте `AbstractFactory` с виртуальными `createButton()` и `createTextBox()`. Наследуйте `WindowsFactory` и `LinuxFactory`.

---

## Блок 4: Абстрактные классы и интерфейсы (задачи 81–105)

**81.** Создайте абстрактный `Shape` с чисто виртуальными `area()` и `perimeter()`. Реализуйте в `Circle`, `Rectangle`, `Triangle`.

**82.** Попробуйте создать объект абстрактного класса — объясните ошибку компиляции.

**83.** Создайте `IComparable<T>` с чисто виртуальным `compareTo(T)`. Реализуйте для `Student`.

**84.** Создайте `ISerializable` с `serialize()` и `deserialize()`. Реализуйте для `Point` и `Circle`.

**85.** Создайте `IDrawable` с `draw()`. Создайте `IResizable` с `resize()`. Реализуйте `Widget : IDrawable, IResizable`.

**86.** Создайте `ILogger` с `log(string, Level)`. Реализуйте `ConsoleLogger` и `FileLogger`.

**87.** Создайте `IContainer<T>` с `add(T)`, `remove(T)`, `contains(T)`. Реализуйте `ListContainer<T>`.

**88.** Создайте `IPlugin` с `getName()`, `execute()`, `shutdown()`. Реализуйте два разных плагина.

**89.** Создайте `IAnimal` с `speak()`, `move()`, `eat()`. Реализуйте `Dog`, `Fish`, `Eagle`.

**90.** Создайте частично абстрактный класс: `Shape` реализует `toString()`, но `area()` чисто виртуальная. Убедитесь, что `toString()` использует `area()` корректно.

**91.** Создайте `AbstractList<T>` с `add`, `get`, `size` как чисто виртуальными. Реализуйте `ArrayList<T>` и `LinkedList<T>`.

**92.** Создайте `Codec` с `encode` и `decode` как чисто виртуальными. Наследуйте `Base64Codec` и `HexCodec`.

**93.** Создайте `AbstractGame` с методами `initialize()`, `update()`, `render()`, `cleanup()`. Реализуйте `SnakeGame`.

**94.** Реализуйте паттерн `Chain of Responsibility`: `Handler` с чисто виртуальным `handle(Request)` и полем `Handler* next`.

**95.** Реализуйте паттерн `State`: абстрактный `State` с `handle(Context&)`. Конкретные: `IdleState`, `RunningState`.

**96.** Создайте `AbstractBuilder` с методами `buildWalls()`, `buildRoof()`, `buildDoor()`. Наследуйте `WoodenHouseBuilder`, `BrickHouseBuilder`.

**97.** Создайте интерфейс `IEventHandler` с `onEvent(Event)`. Реализуйте несколько обработчиков и зарегистрируйте их.

**98.** Создайте `AbstractRepository<T>` с `findById`, `save`, `delete`. Реализуйте `InMemoryRepository<T>`.

**99.** Создайте `AbstractParser` с `parse(string)`. Реализуйте `CsvParser` и `JsonParser` с разным поведением.

**100.** Создайте иерархию с двумя уровнями абстракции: `IShape → AbstractShape → Circle`, где `AbstractShape` реализует `toString()`, а `Circle` — `area()`.

**101.** Создайте `IDisposable` с чисто виртуальным `dispose()`. Создайте `RAII`-класс `AutoDispose`, вызывающий `dispose()` в деструкторе.

**102.** Создайте `AbstractVisitor` (паттерн Visitor) с `visit(Circle)`, `visit(Rectangle)`. Наследуйте `AreaCalculator`.

**103.** Создайте `AbstractAlgorithm<T>` с чисто виртуальными `run(T)` и `benchmark(T)`. Реализуйте `SortAlgorithm`.

**104.** Создайте абстрактный `Formatter` с `format(string)`. Наследуйте `UpperCaseFormatter`, `TrimFormatter`, `HtmlEscapeFormatter`.

**105.** Реализуйте цепочку форматтеров из задачи 104: `FormatterChain`, принимающий `vector<Formatter*>`.

---

## Блок 5: Множественное наследование (задачи 106–130)

**106.** Создайте `Flyable` и `Swimmable`. Наследуйте `Duck : public Flyable, public Swimmable`.

**107.** Добавьте `Runnable` к задаче 106. Создайте `SuperDuck : public Flyable, public Swimmable, public Runnable`.

**108.** Создайте `Worker` (метод `work()`) и `Student` (метод `study()`). Наследуйте `WorkingStudent`.

**109.** Продемонстрируйте конфликт имён при множественном наследовании: два базовых класса с методом `greet()`.

**110.** Разрешите конфликт задачи 109 через явное указание: `obj.A::greet()`.

**111.** Разрешите конфликт задачи 109 через переопределение `greet()` в производном классе.

**112.** Реализуйте класс `Amphibian : public LandAnimal, public WaterAnimal`. Оба базовых имеют `move()`.

**113.** Продемонстрируйте ромбовидное наследование: `A → B, A → C, B+C → D`. Покажите два экземпляра `A`.

**114.** Исправьте задачу 113 с помощью виртуального наследования.

**115.** При виртуальном наследовании покажите, что конструктор виртуальной базы вызывается только один раз.

**116.** Создайте `Serializable` и `Printable` как интерфейсы (все методы чисто виртуальные). Наследуйте оба в `Config`.

**117.** Создайте `IComparable`, `IHashable`, `ICloneable`. Реализуйте класс `Key`, наследующий все три.

**118.** Создайте `IInputStream` и `IOutputStream`. Наследуйте `IStream : IInputStream, IOutputStream`. Реализуйте `MemoryStream`.

**119.** Создайте `Animal` с виртуальным `breathe()`. Наследуйте `Dog : virtual Animal` и `PoliceDog : Dog, WorkingAnimal`. Покажите корректную иерархию.

**120.** Реализуйте паттерн `Mixin`: `Loggable` (метод `log()`), `Configurable` (метод `configure()`). Применяйте к разным классам.

**121.** Создайте `EventEmitter` (emit, on) и `EventReceiver` (handle). Наследуйте оба в `NetworkNode`.

**122.** Реализуйте `Saveable` с `save()` и `Loadable` с `load()`. Наследуйте `Persistent` от обоих.

**123.** Создайте `Thread` и `Runnable`. Наследуйте `ActiveObject : Thread, Runnable` с реализацией рабочего потока.

**124.** Реализуйте иерархию `Instrument → StringInstrument, WindInstrument → Guitar, Violin` (StringInstrument), `Flute` (WindInstrument).

**125.** Создайте `PropertyMixin` и `EventMixin`. Наследуйте `Component : PropertyMixin, EventMixin` — основа UI-фреймворка.

**126.** Реализуйте `Hashable` с `hash()`. Примените множественное наследование в `HashMap` для ключей.

**127.** Создайте `Nameable` и `Describable` с соответствующими методами. Наследуйте `Product : Nameable, Describable`.

**128.** Создайте `Listenable` (подписка на события) и `Observable` (уведомление). Объедините в `ReactiveComponent`.

**129.** Продемонстрируйте порядок конструкторов при множественном наследовании с виртуальными базами.

**130.** Создайте `Plugin : public IPlugin, public IConfigurable, public ILoggable`. Реализуйте все три интерфейса.

---

## Блок 6: RTTI и приведение типов (задачи 131–150)

**131.** Используйте `dynamic_cast` для безопасного приведения `Animal*` к `Dog*`. Выведите сообщение при неудаче.

**132.** Используйте `typeid` для определения реального типа объекта через указатель на базовый класс.

**133.** Создайте функцию `describeAnimal(Animal* a)`, использующую `dynamic_cast` для специального поведения для `Dog` и `Cat`.

**134.** Реализуйте `dynamic_cast` с ссылкой: поймайте `std::bad_cast` при неудачном приведении.

**135.** Создайте фабрику, возвращающую `Shape*`. Используйте `dynamic_cast` для вызова специфичных методов.

**136.** Используйте `static_cast` для upcasting. Объясните, почему это безопасно.

**137.** Попробуйте некорректный `static_cast` вниз по иерархии. Объясните последствия.

**138.** Реализуйте функцию `printIfCircle(Shape* s)` с `dynamic_cast`. Вызовите с разными типами.

**139.** Создайте `Registry` — хранилище `Animal*`. Реализуйте метод `getAll<T>()`, возвращающий только объекты типа `T`.

**140.** Реализуйте паттерн `Visitor` с `dynamic_cast` для диспетчеризации по типу.

**141.** Сравните производительность `dynamic_cast` и виртуальных функций — объясните разницу.

**142.** Используйте `const_cast` для снятия `const` с базового указателя (объясните, когда это допустимо).

**143.** Создайте `type_switch` — аналог `switch` по типу через цепочку `dynamic_cast`.

**144.** Используйте `typeid` для реализации `operator==` двух объектов с проверкой типа.

**145.** Реализуйте `clone_cast<T>(Base* p)` — шаблонную функцию с `dynamic_cast` + `clone()`.

**146.** Создайте `ObjectFactory` с регистрацией типов по строковому ключу и созданием через `new`.

**147.** Реализуйте сериализацию с RTTI: `serialize(Base* obj)` выводит тип и данные.

**148.** Реализуйте десериализацию: читает строку с типом и создаёт нужный объект.

**149.** Создайте функцию `isA<T>(Base* p)`, возвращающую `true` если объект является `T`.

**150.** Реализуйте `safe_polymorphic_copy(Base* p)` — копирует объект через `dynamic_cast` + `clone()`.

---

## Блок 7: Продвинутые темы и паттерны (задачи 151–175)

**151.** Реализуйте паттерн `Strategy` через наследование: `Sorter` → `BubbleSort`, `QuickSort`.

**152.** Реализуйте паттерн `Decorator` через наследование: `TextWidget → BoldWidget → ItalicWidget`.

**153.** Реализуйте паттерн `Composite`: `Component → Leaf, Composite`. `Composite` хранит `vector<Component*>`.

**154.** Реализуйте паттерн `Template Method` с 3 уровнями иерархии.

**155.** Реализуйте паттерн `Factory Method`: `Creator → ConcreteCreatorA, ConcreteCreatorB`.

**156.** Реализуйте паттерн `Abstract Factory` для UI: кнопки и поля для Windows и Linux.

**157.** Реализуйте паттерн `Bridge`: `Abstraction` + `Implementor` — разделение иерархий.

**158.** Реализуйте `CRTP` (Curiously Recurring Template Pattern): `Base<Derived>` вызывает методы `Derived`.

**159.** Используйте CRTP для реализации статического полиморфизма без vtable.

**160.** Реализуйте `mixin` через CRTP: `Printable<T>` добавляет метод `print()` используя методы `T`.

**161.** Реализуйте `EBO` (Empty Base Optimization): наследуйте пустой базовый класс для уменьшения размера.

**162.** Создайте `Policy-based` класс через шаблонные параметры-политики вместо наследования.

**163.** Реализуйте паттерн `Prototype` с `clone()` для иерархии из 4 классов.

**164.** Реализуйте паттерн `Flyweight`: базовый `GlyphFactory`, разделяющий общее состояние.

**165.** Реализуйте `TypeList` через наследование шаблонных базовых классов.

**166.** Реализуйте `Visitor` с двойной диспетчеризацией через виртуальные функции.

**167.** Реализуйте иерархию исключений: `AppException → NetworkException, DatabaseException → ConnectionException`.

**168.** Поймайте исключения иерархии в порядке от конкретного к общему. Покажите важность порядка `catch`.

**169.** Реализуйте `Interpreter`: иерархия `Expression → Number, Add, Multiply, Negate` с `eval()`.

**170.** Реализуйте `Command` с `undo()`: `TextEditor` + `TypeCommand`, `DeleteCommand`.

**171.** Реализуйте шаблонный `Observable<T>` — при `virtual` ограничениях покажите альтернативу через шаблоны.

**172.** Реализуйте `Proxy`: `RealSubject` и `ProxySubject` с одним базовым `Subject`.

**173.** Реализуйте `Adapter`: адаптируйте старый `LegacyPrinter` к новому интерфейсу `IPrinter`.

**174.** Реализуйте `Façade` поверх сложной иерархии классов.

**175.** Реализуйте `Type Erasure` через наследование: `AnyDrawable` хранит любой drawable-объект.

---

## Блок 8: Практические мини-проекты (задачи 176–200)

**176.** Реализуйте иерархию `Shape` (Circle, Rectangle, Triangle, Ellipse) с `area()`, `perimeter()`, `draw()`, `clone()`, `operator<<`. Запишите их в `vector<unique_ptr<Shape>>` и обработайте полиморфно.

**177.** Реализуйте мини-банк: `Account → SavingsAccount, CreditAccount, DepositAccount`. У каждого — своя логика начисления процентов. Полиморфный отчёт через `vector<Account*>`.

**178.** Реализуйте иерархию виджетов: `Widget → Button, Label, TextInput, Checkbox`. Метод `render()` виртуальный. `Container : Widget` хранит дочерние виджеты.

**179.** Реализуйте систему существ для RPG: `Creature → Warrior, Mage, Archer`. Полиморфные методы `attack()`, `defend()`, `specialAbility()`. Симулируйте бой.

**180.** Реализуйте `FileSystem`: `FSNode → File, Directory`. `Directory` хранит `vector<FSNode*>`. Метод `print(int indent)` выводит дерево. Рекурсивный подсчёт размера.

**181.** Реализуйте простой интерпретатор выражений: `Expr → Num, Add, Sub, Mul, Div, Neg`. Метод `eval()` рекурсивно вычисляет значение.

**182.** Реализуйте систему плагинов: `IPlugin` с `getName()`, `execute(Args)`, `shutdown()`. `PluginManager` загружает и управляет плагинами через `vector<IPlugin*>`.

**183.** Реализуйте иерархию транспорта: `Vehicle → Car, Truck, Bus, Motorcycle`. Полиморфный расчёт расхода топлива и стоимости поездки.

**184.** Реализуйте `EventSystem`: `Event → MouseEvent, KeyEvent, NetworkEvent`. `EventDispatcher` хранит `map<type, vector<IHandler*>>` и диспетчеризует через `dynamic_cast`.

**185.** Реализуйте систему логирования: `Logger → ConsoleLogger, FileLogger, NetworkLogger, CompositeLogger`. `CompositeLogger` делегирует нескольким логгерам.

**186.** Реализуйте мини-ORM: `Model → UserModel, ProductModel`. Абстрактный `Repository<T>` с `findById`, `save`, `delete`. `InMemoryRepository<T>` как реализация.

**187.** Реализуйте `Serializer`: `ISerializer → JsonSerializer, XmlSerializer, BinarySerializer`. `Serialize(ISerializable&)` полиморфно.

**188.** Реализуйте паттерн MVC: `Model`, `View → ConsoleView, HtmlView`, `Controller`. Полиморфный рендеринг через `View*`.

**189.** Реализуйте иерархию коллекций: `Collection<T> → ArrayList<T>, LinkedList<T>, HashSet<T>`. Общий интерфейс `add`, `remove`, `contains`, `iterate`.

**190.** Реализуйте иерархию исключений для веб-приложения: `AppException → HttpException(code) → NotFoundException, ForbiddenException, ServerErrorException`. Обработайте полиморфно.

**191.** Реализуйте `Pipeline`: `Stage → FilterStage, TransformStage, AggregateStage`. `Pipeline` хранит цепочку `Stage*` и последовательно применяет к данным.

**192.** Реализуйте `AI` для игры: `AIStrategy → AggressiveAI, DefensiveAI, RandomAI`. Полиморфный выбор действия через `vector<AIStrategy*>`.

**193.** Реализуйте `ReportGenerator`: `ReportSection → HeaderSection, TableSection, ChartSection, FooterSection`. Метод `render()` полиморфный. Собирайте отчёт из секций.

**194.** Реализуйте граф полиморфных функций: `Node → InputNode, ProcessNode, OutputNode`. Метод `execute()` и `connect(Node*)` для построения потока данных.

**195.** Реализуйте иерархию `Sensor → TemperatureSensor, PressureSensor, HumiditySensor`. Абстрактный `SensorHub` агрегирует показания. Полиморфный мониторинг.

**196.** Реализуйте `TaskScheduler`: `Task → PeriodicTask, OneTimeTask, DelayedTask`. `Scheduler` управляет `vector<Task*>`, вызывает `execute()` по расписанию.

**197.** Реализуйте `Notification` систему: `Notification → EmailNotification, SMSNotification, PushNotification`. `NotificationService` полиморфно отправляет через `vector<Notification*>`.

**198.** Реализуйте `DataTransformer`: `Transformer<In, Out> → MapTransformer, FilterTransformer, ReduceTransformer`. Цепочка трансформаций через наследование.

**199.** Реализуйте полноценный `ShapeEditor`: `Shape`-иерархия с `move()`, `rotate()`, `scale()`, `clone()`, `serialize()`, `draw()`. `Canvas` хранит фигуры. Реализуйте `undo/redo` через `Command`.

**200.** Реализуйте мини-игровой движок: `GameObject → Player, Enemy, Projectile, Platform`. Каждый имеет `update(float dt)`, `render()`, `onCollision(GameObject&)`. `Scene` управляет объектами через `vector<unique_ptr<GameObject>>`. Реализуйте простой игровой цикл.
