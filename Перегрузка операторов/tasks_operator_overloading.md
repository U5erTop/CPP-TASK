# 100 задач по теме “Перегрузка операторов в C++”

---

## Задачи 1–25: арифметика и сравнения

1. `Fraction`: перегрузить `+`, `-`, `*`, `/`, сократить дробь.
2. `Fraction`: перегрузить `+=`, реализовать `+` через `+=`.
3. `Fraction`: перегрузить `==` и `!=`.
4. `Complex`: перегрузить `+`, `-`, `*`.
5. `Complex`: перегрузить `==`.
6. `Vector2D`: перегрузить `+`, `-`, унарный `-`.
7. `Vector2D`: перегрузить `v*k` и `k*v`.
8. `Money` (руб/коп): перегрузить `+`, `-`, `<`, `==`.
9. `Angle` (градусы): `+`, `-` с нормализацией 0..360.
10. `BigInt` (неотриц.): перегрузить `+`.
11. `BigInt`: перегрузить `==` и `<`.
12. `ModInt`: `+,-,*,==` по модулю `MOD`.
13. `Point`: `==` и `<` (лексикографически).
14. `RGB`: `+` с насыщением 0..255.
15. `Matrix2x2`: умножение матриц `*`.
16. `Matrix2x2`: умножение матрицы на вектор.
17. `Seconds`: `+` и `-` (обёртка над `int`).
18. `Meters` и `Kilometers`: сложение и конверсия.
19. `Probability` (0..1): определить безопасное сложение.
20. `Polynomial`: `+` (по коэффициентам).
21. `Polynomial`: `*`.
22. `Fraction`: поддержать `int + Fraction` и `Fraction + int`.
23. `Fraction`: сделать конструктор из `int` и проверить влияние `explicit`.
24. `Temperature`: запретить `+` (обосновать).
25. `SafeInt`: `+` с проверкой переполнения.

---

## Задачи 26–45: инкремент, присваивание, побитовые

26. `Counter`: префиксный `++`.
27. `Counter`: постфиксный `++`.
28. `IteratorLike`: перегрузить `++` и `*` для обхода массива.
29. `Vector2D`: `+=` и `+` через `+=`.
30. `Vector2D`: `-=` и `-` через `-=`.
31. `Bitset8`: `|=`, `&=`, `^=`.
32. `Bitset8`: `~`.
33. `Flags`: `|` через `|=`.
34. `Fraction`: унарный `+`.
35. `Fraction`: унарный `-`.
36. `ModuloCounter`: циклический `++`.
37. `StringBuilder`: `+=` для добавления строки.
38. `SmallVector`: корректный `operator=` (правило 3/5).
39. `MoveOnly`: запретить копирование (`operator=` delete), разрешить перемещение.
40. `SharedPtr`: `operator=` с refcount.
41. `UniqueHandle`: запретить копирующее присваивание.
42. `Matrix`: `*=` на число.
43. `Matrix`: `*` на число через `*=`.
44. `ClampInt`: `+=` с ограничением диапазона.
45. `LoggerValue`: `operator=` логирует присваивание.

---

## Задачи 46–65: [], (), указательные операторы

46. `IntArray`: перегрузить `operator[]` (const и non-const).
47. `IntArray`: добавить проверку границ в `operator[]`.
48. `Matrix`: реализовать `operator()(row, col)` (const и non-const).
49. `Tensor3`: реализовать `operator()(i,j,k)`.
50. `Image`: `operator()(x,y)` для пикселя.
51. `Span`: `operator[]` без владения памятью.
52. `SmartPtr<T>`: перегрузить `*` и `->`.
53. `SmartPtr<T>`: добавить const-корректность `->`.
54. `Optional<T>`: `operator*`, `operator->`, `operator bool`.
55. `StringView`: `operator[]` и объяснить почему нельзя `char&`.
56. `Polynomial`: `operator[](degree)` для коэффициента.
57. `RingBuffer`: `operator[]` с циклической индексацией.
58. `Grid`: `operator()` и метод `at()`.
59. `MatrixView`: `operator()(r,c)` для подматрицы.
60. `Config`: `operator[]` доступ по ключу.
61. `Utf8String`: обсудить `operator[]` (опасность по кодпоинтам).
62. `DequeLike`: `operator[]`.
63. `Handle`: `operator!` как `!isValid()`.
64. `Socket`: `explicit operator bool()` как `isConnected()`.
65. `File`: `explicit operator bool()` как `isOpen()`.

---

## Задачи 66–85: потоки, вызов, сдвиги

66. `Fraction`: перегрузить `operator<<` для вывода `a/b`.
67. `Fraction`: перегрузить `operator>>` для ввода `a/b`.
68. `Point`: `operator<<` вывод `(x,y)`.
69. `Complex`: `operator<<` вывод `re+imi`.
70. `Logger`: перегрузить `operator()` чтобы писать `log("msg")`.
71. `Stopwatch`: `operator()` возвращает время.
72. `Validator`: `operator()` как предикат.
73. `FunctionWrapper`: хранить функцию и вызывать `operator()`.
74. `Bitset8`: перегрузить `<<` и `<<=` как сдвиг.
75. `Bitset8`: перегрузить `>>` и `>>=`.
76. `Flags`: перегрузить `&` и `|`.
77. `Path`: перегрузить `/` для склейки пути (обсудить).
78. `Range`: перегрузить `|` как pipe (обсудить риск).
79. `Matrix`: `operator==` сравнение размеров и элементов.
80. `Matrix`: `operator+` поэлементно.
81. `String`: `operator+` конкатенация.
82. `String`: `operator+=`.
83. `String`: `operator==`.
84. `BigInt`: `operator<<` как умножение на 10^k (обсудить спорность).
85. `Vector`: `operator*` как скалярное произведение (обсудить).

---

## Задачи 86–100: подводные камни и проектирование

86. Показать пример, почему перегружать `&&` опасно (нет short-circuit).
87. Показать пример, почему перегружать `||` опасно.
88. Показать пример, почему перегрузка `,` опасна.
89. `Matrix`: сравнить `m(i,j)` и `m[i][j]` (Row proxy).
90. `Fraction`: проверить неоднозначности из-за неявных преобразований.
91. `Complex`: сделать конструктор из `double` и поэкспериментировать с `explicit`.
92. `Unit`-типы: `Meters`, `Seconds`, `Mps`; разрешить только совместимые операции.
93. `UniquePtr<T>`: `*`, `->`, запретить копирование.
94. `SharedPtr<T>`: копирование и `operator=` с refcount.
95. `OptionalInt`: реализовать безопасные операторы.
96. `Matrix`: добавить `const` перегрузку `operator()` и тесты.
97. `IntArray`: сделать итератор с `operator*` и `operator++`.
98. `SortKey`: перегрузить `<` так, чтобы сортировка была стабильной по вторичному ключу.
99. `Version`: перегрузить сравнения `1.2.10 > 1.2.3`.
100.  Написать мини-гайд (10–15 строк): когда перегружать операторы, а когда методы.

---

### Решение задачи 1 — Fraction: + - \* /

```cpp
#include <iostream>
#include <numeric>
#include <stdexcept>

class Fraction {
    long long n = 0;
    long long d = 1;

    void normalize() {
        if (d == 0) throw std::invalid_argument("denominator is zero");
        if (d < 0) { d = -d; n = -n; }
        long long g = std::gcd(n, d);
        n /= g; d /= g;
    }

public:
    Fraction(long long num = 0, long long den = 1) : n(num), d(den) { normalize(); }

    friend Fraction operator+(const Fraction& a, const Fraction& b) {
        return Fraction(a.n * b.d + b.n * a.d, a.d * b.d);
    }
    friend Fraction operator-(const Fraction& a, const Fraction& b) {
        return Fraction(a.n * b.d - b.n * a.d, a.d * b.d);
    }
    friend Fraction operator*(const Fraction& a, const Fraction& b) {
        return Fraction(a.n * b.n, a.d * b.d);
    }
    friend Fraction operator/(const Fraction& a, const Fraction& b) {
        return Fraction(a.n * b.d, a.d * b.n);
    }

    friend std::ostream& operator<<(std::ostream& os, const Fraction& f) {
        return os << f.n << "/" << f.d;
    }
};

int main() {
    Fraction a(1, 2), b(1, 3);
    std::cout << (a + b) << "\n";
    std::cout << (a - b) << "\n";
    std::cout << (a * b) << "\n";
    std::cout << (a / b) << "\n";
}
```

### Решение задачи 2 — Fraction: += и + через +=

```cpp
#include <numeric>
#include <stdexcept>

class Fraction {
    long long n = 0;
    long long d = 1;

    void normalize() {
        if (d == 0) throw std::invalid_argument("denominator is zero");
        if (d < 0) { d = -d; n = -n; }
        long long g = std::gcd(n, d);
        n /= g; d /= g;
    }

public:
    Fraction(long long num = 0, long long den = 1) : n(num), d(den) { normalize(); }

    Fraction& operator+=(const Fraction& r) {
        n = n * r.d + r.n * d;
        d = d * r.d;
        normalize();
        return *this;
    }

    friend Fraction operator+(Fraction l, const Fraction& r) {
        l += r;
        return l;
    }
};
```

### Решение задачи 7 — Vector2D: v*k и k*v

```cpp
class Vector2D {
    double x, y;
public:
    Vector2D(double x = 0, double y = 0) : x(x), y(y) {}

    friend Vector2D operator*(const Vector2D& v, double k) {
        return Vector2D(v.x * k, v.y * k);
    }

    friend Vector2D operator*(double k, const Vector2D& v) {
        return v * k;
    }
};
```

### Решение задачи 26 — Counter: префиксный ++

```cpp
class Counter {
    int value = 0;
public:
    explicit Counter(int v = 0) : value(v) {}

    Counter& operator++() {
        ++value;
        return *this;
    }
};
```

### Решение задачи 27 — Counter: постфиксный ++

```cpp
class Counter {
    int value = 0;
public:
    explicit Counter(int v = 0) : value(v) {}

    Counter& operator++() {
        ++value;
        return *this;
    }

    Counter operator++(int) {
        Counter old = *this;
        ++(*this);
        return old;
    }
};
```

### Решение задачи 46 — IntArray: operator[] const/non-const

```cpp
#include <cstddef>
#include <stdexcept>

class IntArray {
    int* data = nullptr;
    std::size_t n = 0;

public:
    explicit IntArray(std::size_t size) : data(new int[size]{}), n(size) {}
    ~IntArray() { delete[] data; }

    int& operator[](std::size_t i) {
        if (i >= n) throw std::out_of_range("index");
        return data[i];
    }

    const int& operator[](std::size_t i) const {
        if (i >= n) throw std::out_of_range("index");
        return data[i];
    }
};
```

### Решение задачи 48 — Matrix: operator()(row,col)

```cpp
#include <vector>
#include <cstddef>
#include <stdexcept>

class Matrix {
    std::size_t rows, cols;
    std::vector<double> a;

    std::size_t idx(std::size_t r, std::size_t c) const { return r * cols + c; }

public:
    Matrix(std::size_t r, std::size_t c) : rows(r), cols(c), a(r*c, 0.0) {}

    double& operator()(std::size_t r, std::size_t c) {
        if (r >= rows || c >= cols) throw std::out_of_range("index");
        return a[idx(r,c)];
    }

    double operator()(std::size_t r, std::size_t c) const {
        if (r >= rows || c >= cols) throw std::out_of_range("index");
        return a[idx(r,c)];
    }
};
```

### Решение задачи 52 — SmartPtr<T>: \* и ->

```cpp
#include <stdexcept>

template <class T>
class SmartPtr {
    T* p = nullptr;
public:
    explicit SmartPtr(T* ptr = nullptr) : p(ptr) {}

    T& operator*() const {
        if (!p) throw std::runtime_error("null");
        return *p;
    }

    T* operator->() const {
        if (!p) throw std::runtime_error("null");
        return p;
    }
};
```

### Решение задачи 66 — Fraction: operator<<

```cpp
#include <iostream>

class Fraction {
    long long n, d;
public:
    Fraction(long long n = 0, long long d = 1) : n(n), d(d) {}

    friend std::ostream& operator<<(std::ostream& os, const Fraction& f) {
        return os << f.n << "/" << f.d;
    }
};
```

### Решение задачи 70 — Logger: operator()

```cpp
#include <iostream>
#include <string>

class Logger {
public:
    void operator()(const std::string& msg) const {
        std::cout << "[LOG] " << msg << "\n";
    }
};

int main() {
    Logger log;
    log("hello");
}
```
