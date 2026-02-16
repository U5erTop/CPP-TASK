# 100 задач по темам: перегрузка функций, аргументы по умолчанию, конструктор копирования

---

## Задачи 1–35: перегрузка функций

1. Написать перегруженные функции `max` для типов `int`, `double` и `char`, возвращающие максимальное из двух значений.
2. Реализовать перегрузку функции `abs` для `int` и `double`.
3. Реализовать три перегруженных функции `print`: вывод строки, целого числа и числа с плавающей запятой.
4. Написать две перегруженные функции `sum`: одна принимает два `int`, другая — массив `int` и его размер.
5. Создать перегрузку функции `distance`: по двум точкам на оси (`double`), по двум точкам в 2D (`struct { double x, y; }`).
6. Реализовать функции `area` для круга (по радиусу), прямоугольника (по ширине и высоте) и треугольника (по основанию и высоте).
7. Написать перегруженные функции `swap` для `int`, `double` и структур `Point { int x, y; }`.
8. Написать перегруженные функции `read`: чтение `int` из `std::cin` и чтение `std::string` из `std::cin`.
9. Написать функции `toString`, которые преобразуют `int`, `double` и `bool` к `std::string`.
10. Реализовать перегруженные функции `pow`: возведение `int` в `int`‑степень и `double` в `int`‑степень (целая степень).

11. Создать класс `Vector2D` и перегрузить свободную функцию `length` для `Vector2D` и `Vector3D`.
12. Написать две функции `clamp`: одна ограничивает `int` в диапазоне `[min, max]`, другая ограничивает `double`.
13. Реализовать перегруженные функции `equal`: сравнение двух `int`, двух `double` с эпсилон‑погрешностью и двух `std::string`.
14. Написать перегруженные функции `fillArray`, заполняющие массив `int` и массив `double` заданным значением.
15. Создать перегруженные функции `factorial`: одна принимает `int`, другая — `unsigned long long`.
16. Написать перегруженные функции `logMessage`: принимают `const char*`, `std::string` и `int` (код).
17. Реализовать перегрузку функции `min` для трёх `int` и для трёх `double`.
18. Написать перегрузку функции `sort`: сортировка массива `int` и массива `double` простым обменом.
19. Реализовать перегруженные функции `find`: поиск элемента в массиве `int` и поиск символа в `const char*`.
20. Написать две функции `average`: среднее арифметическое массива `int` и массива `double`.

21. Создать перегрузки функции `printArray` для `int[]`, `double[]` и `std::string[]`.
22. Реализовать перегруженную функцию `distance` между двумя точками: по `Point` и по координатам `(x1, y1, x2, y2)`.
23. Написать перегрузку функции `scale`: умножение `Point` на скаляр `int` и на скаляр `double`.
24. Реализовать перегруженную функцию `readFromFile`: чтение всего файла в `std::string` и чтение целого числа из файла.
25. Написать перегруженную функцию `roundTo`, округляющую `double` до `int` и `float` до `int`.
26. Создать перегрузку функции `max` для трёх и четырёх аргументов типа `int`.
27. Реализовать перегруженную функцию `concat`: конкатенация двух `std::string` и конкатенация `std::string` и `int` (переводя число в строку).
28. Написать перегрузку `printBinary` для `unsigned int` и `unsigned long long`.
29. Реализовать перегрузку функции `countDigits` для `int` и `long long`.
30. Написать перегрузку функции `isPositive` для `int`, `double` и `long long`.

31. Создать класс `Complex` и перегрузить свободную функцию `abs` для `Complex` и `double`.
32. Реализовать перегруженные функции `readPoint`: из `std::cin` и из строки формата `"x y"`.
33. Написать перегрузку функции `triangleType`: по трём сторонам `int` и `double`.
34. Реализовать перегруженные функции `printMatrix` для матрицы `int` и матрицы `double`.
35. Написать перегрузку функции `distance` для одномерных точек (`int`) и двумерных точек (`Point`), используя перегрузку по типу.

---

## Задачи 36–70: аргументы по умолчанию

36. Написать функцию `printLine(const std::string& s, char sep = '\n')`, которая печатает строку и символ‑разделитель.
37. Реализовать функцию `repeat(const std::string& s, int times = 1)`, повторяющую строку указанное количество раз.
38. Написать функцию `log(const std::string& msg, int level = 1, std::ostream& out = std::cout)`.
39. Создать функцию `drawRectangle(int width, int height, char ch = '#')`, рисующую прямоугольник в консоли.
40. Реализовать функцию `openFile(const std::string& name, bool createIfMissing = true)`, которая открывает файл, создавая его при необходимости.

41. Написать функцию `randomInt(int min = 0, int max = 100)`.
42. Создать функцию `connect(const std::string& host = "localhost", int port = 80)`.
43. Реализовать функцию `formatNumber(int value, int width = 5, char fill = '0')`.
44. Написать функцию `printVector(const std::vector<int>& v, const std::string& sep = " ")`.
45. Реализовать функцию `saveSettings(const std::string& path = "config.ini", bool overwrite = false)`.

46. Написать функцию `drawLine(int length, char ch = '-', bool newline = true)`.
47. Создать функцию `power(double base, int exp = 2)`, возводящую число в степень.
48. Реализовать функцию `greet(const std::string& name = "Guest", const std::string& prefix = "Hello")`.
49. Написать функцию `resizeArray(int*& arr, int& size, int newSize, int defaultValue = 0)`.
50. Реализовать функцию `findChar(const std::string& s, char c, size_t startPos = 0)`.

51. Написать функцию `replaceAll(std::string& s, char from, char to, bool ignoreCase = false)`.
52. Создать функцию `sortArray(int* arr, int size, bool ascending = true)`.
53. Реализовать функцию `readInt(int defaultValue = 0)`, которая возвращает введённое число или значение по умолчанию при ошибке ввода.
54. Написать функцию `download(const std::string& url, int timeoutMs = 5000, bool verbose = false)` (реализацию можно оставить заглушкой).
55. Реализовать функцию `merge(std::vector<int>& a, const std::vector<int>& b, bool unique = false)`.

56. Написать функцию `printTable(int rows, int cols, char fill = '*', bool border = true)`.
57. Создать функцию `clip(double value, double minVal = 0.0, double maxVal = 1.0)`.
58. Реализовать функцию `encode(const std::string& s, char key = 13)`, выполняющую простейшее шифрование сдвигом.
59. Написать функцию `createUser(const std::string& name, int age = 18, bool active = true)`.
60. Реализовать функцию `scheduleTask(const std::string& name, int delayMs = 0, int repeatCount = 1)`.

61. Написать функцию `formatTime(int hours, int minutes = 0, int seconds = 0)`.
62. Создать функцию `initializeArray(int* arr, int size, int value = 0)`.
63. Реализовать функцию `loadTexture(const std::string& path, bool mipmaps = true, bool repeat = false)`.
64. Написать функцию `printProgress(int current, int total, int width = 50, char fill = '#')`.
65. Реализовать функцию `configureLogger(const std::string& file = "", int level = 1, bool console = true)`.

66. Написать функцию `drawCircle(int radius, char ch = '*', bool filled = true)`.
67. Создать функцию `connectDB(const std::string& connStr = "localhost", int timeout = 1000)`.
68. Реализовать функцию `copyFile(const std::string& from, const std::string& to, bool overwrite = false)`.
69. Написать функцию `generateReport(const std::string& title = "Report", bool withDate = true, bool withSummary = true)`.
70. Реализовать функцию `sleepMs(int ms = 1000)` (можно использовать `std::this_thread::sleep_for`).

---

## Задачи 71–100: конструктор копирования и перегрузка конструкторов

71. Создать класс `IntArray`, владеющий динамическим массивом `int`. Реализовать конструктор по размеру и конструктор копирования с глубоким копированием.
72. Написать класс `String`, который хранит `char*`. Реализовать конструктор из `const char*` и конструктор копирования (глубокое копирование).
73. Создать класс `FileHandle`, владеющий файловым дескриптором. Реализовать конструктор копирования, запрещающий копирование (например, сделав его `delete`).
74. Написать класс `Point`, перегрузить конструкторы: по умолчанию `(0,0)`, по `int x`, по `int x, int y`, и конструктор копирования.
75. Создать класс `Matrix`, владеющий динамическим двумерным массивом. Реализовать конструктор с размерами и конструктор копирования.

76. Написать класс `Person` с полями `name` и `age`. Реализовать конструктор с аргументами по умолчанию и конструктор копирования.
77. Создать класс `Buffer`, хранящий размер и указатель на байты. Реализовать конструктор копирования и убедиться, что копия не делит память с оригиналом.
78. Написать класс `Timer`, в котором копирование запрещено (скрытый или удалённый конструктор копирования).
79. Создать класс `Image`, владеющий пиксельными данными. Реализовать конструкторы: по размерам, из файла (пока заглушка), копирующий конструктор.
80. Написать класс `ArrayWrapper`, который владеет `int*`. Реализовать конструктор копирования и продемонстрировать, чем он лучше поверхностного копирования.

81. Создать класс `Resource`, в котором конструктор копирования принимает дополнительный параметр с аргументом по умолчанию (например, режим копирования).
82. Написать класс `Logger`, у которого есть конструктор по умолчанию и конструктор копирования, выводящий сообщение о копировании.
83. Создать класс `Counter` с полем `id` и статическим счётчиком созданных объектов. Реализовать конструктор копирования, чтобы было видно, когда происходит копирование.
84. Написать класс `Vector2D` с конструктором по умолчанию, конструктором по двум координатам и конструктором копирования.
85. Создать класс `Book` с полями `title`, `author`, `pages`. Реализовать перегруженные конструкторы (с разными наборами параметров) и конструктор копирования.

86. Написать класс `SmartPtr`, который ведёт счётчик ссылок (упрощённый `shared_ptr`). Реализовать конструктор копирования, увеличивающий счётчик.
87. Создать класс `Node` (элемент списка) и реализовать копирующий конструктор, который копирует только сам узел без хвоста списка.
88. Написать класс `DynamicStringArray`, владеющий массивом `std::string`, с корректным конструктором копирования.
89. Создать класс `BigNumber`, который хранит число в виде динамического массива цифр. Реализовать конструктор копирования.
90. Написать класс `Rectangle` с перегруженными конструкторами (по умолчанию, по ширине и высоте, по двум точкам) и конструктором копирования.

91. Создать класс `Polynomial`, хранящий коэффициенты в динамическом массиве. Реализовать конструктор копирования.
92. Написать класс `Settings`, который можно копировать, но при копировании некоторые поля сбрасываются (например, временные).
93. Создать класс `Socket`, в котором копирование запрещено, но есть перемещающий конструктор (копирующий конструктор удалить).
94. Написать класс `Path`, хранящий динамический массив точек, с конструктором копирования.
95. Создать класс `Label`, содержащий текст и цвет. Реализовать конструктор с аргументами по умолчанию и конструктор копирования.

96. Написать класс `Database`, запрещающий копирование и имеющий только один глобальный экземпляр (синглтон с закрытым конструктором копирования).
97. Создать класс `AudioBuffer`, хранящий динамический массив сэмплов, с корректным конструктором копирования.
98. Написать класс `Grid`, реализующий двумерную сетку, с конструктором копирования и перегрузкой конструктора по умолчанию и по размерам.
99. Создать класс `Texture`, владеющий ресурсом, с конструктором копирования, выполняющим глубокое копирование.
100.  Написать класс `History`, хранящий динамический массив строк (записей истории), с корректным конструктором копирования и несколькими перегруженными конструкторами.

---

### Задача 3

> Реализовать три перегруженных функции `print`: вывод строки, целого числа и числа с плавающей запятой.

```cpp
#include <iostream>
#include <string>

void print(const std::string& s) {
    std::cout << s << '\n';
}

void print(int x) {
    std::cout << x << '\n';
}

void print(double x) {
    std::cout << x << '\n';
}

int main() {
    print("Hello");
    print(42);
    print(3.14);
}
```

---

### Задача 7

> Написать перегруженные функции `swap` для `int`, `double` и структур `Point { int x, y; }`.

```cpp
#include <iostream>

struct Point {
    int x;
    int y;
};

void swap(int& a, int& b) {
    int tmp = a;
    a = b;
    b = tmp;
}

void swap(double& a, double& b) {
    double tmp = a;
    a = b;
    b = tmp;
}

void swap(Point& a, Point& b) {
    Point tmp = a;
    a = b;
    b = tmp;
}

int main() {
    int a = 1, b = 2;
    swap(a, b);

    double x = 1.5, y = 2.5;
    swap(x, y);

    Point p1{1, 2}, p2{3, 4};
    swap(p1, p2);
}
```

---

### Задача 15

> Создать перегруженные функции `factorial`: одна принимает `int`, другая — `unsigned long long`.

```cpp
#include <iostream>

unsigned long long factorial(int n) {
    if (n < 0) return 0;      // грубая защита
    unsigned long long res = 1;
    for (int i = 1; i <= n; ++i)
        res *= i;
    return res;
}

unsigned long long factorial(unsigned long long n) {
    unsigned long long res = 1;
    for (unsigned long long i = 1; i <= n; ++i)
        res *= i;
    return res;
}

int main() {
    std::cout << factorial(5) << '\n';
    std::cout << factorial(10ULL) << '\n';
}
```

---

### Задача 22

> Реализовать перегруженную функцию `distance` между двумя точками: по `Point` и по координатам `(x1, y1, x2, y2)`.

```cpp
#include <iostream>
#include <cmath>

struct Point {
    double x;
    double y;
};

double distance(const Point& a, const Point& b) {
    double dx = a.x - b.x;
    double dy = a.y - b.y;
    return std::sqrt(dx * dx + dy * dy);
}

double distance(double x1, double y1, double x2, double y2) {
    double dx = x1 - x2;
    double dy = y1 - y2;
    return std::sqrt(dx * dx + dy * dy);
}

int main() {
    Point p1{0, 0}, p2{3, 4};
    std::cout << distance(p1, p2) << '\n';          // 5
    std::cout << distance(0, 0, 3, 4) << '\n';      // 5
}
```

---

### Задача 30

> Написать перегрузку функции `isPositive` для `int`, `double` и `long long`.

```cpp
#include <iostream>

bool isPositive(int x) {
    return x > 0;
}

bool isPositive(double x) {
    return x > 0.0;
}

bool isPositive(long long x) {
    return x > 0;
}

int main() {
    std::cout << std::boolalpha;
    std::cout << isPositive(5) << '\n';
    std::cout << isPositive(-3.14) << '\n';
    std::cout << isPositive(0LL) << '\n';
}
```

---

### Задача 45

> Реализовать функцию `saveSettings(const std::string& path = "config.ini", bool overwrite = false)`.

```cpp
#include <iostream>
#include <fstream>
#include <string>

bool saveSettings(const std::string& path = "config.ini", bool overwrite = false) {
    std::ios_base::openmode mode = std::ios::out;
    if (!overwrite) {
        // Если нельзя перезаписывать, открываем с флагом app,
        // чтобы дописывать в конец
        mode |= std::ios::app;
    }

    std::ofstream file(path, mode);
    if (!file) {
        return false;
    }

    file << "# sample settings\n";
    file << "volume=80\n";
    file << "brightness=50\n";
    return true;
}

int main() {
    if (!saveSettings()) {
        std::cerr << "Cannot save settings\n";
    }
}
```

---

### Задача 52

> Создать функцию `sortArray(int* arr, int size, bool ascending = true)`.

```cpp
#include <iostream>

void sortArray(int* arr, int size, bool ascending = true) {
    for (int i = 0; i < size - 1; ++i) {
        for (int j = 0; j < size - 1 - i; ++j) {
            bool needSwap = ascending
                ? (arr[j] > arr[j + 1])
                : (arr[j] < arr[j + 1]);
            if (needSwap) {
                int tmp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = tmp;
            }
        }
    }
}

int main() {
    int a[] = {5, 1, 4, 2, 8};
    int n = sizeof(a) / sizeof(a[0]);

    sortArray(a, n); // по возрастанию

    for (int x : a) std::cout << x << ' ';
    std::cout << '\n';

    sortArray(a, n, false); // по убыванию
    for (int x : a) std::cout << x << ' ';
}
```

---

### Задача 68

> Реализовать функцию `copyFile(const std::string& from, const std::string& to, bool overwrite = false)`.

```cpp
#include <iostream>
#include <fstream>
#include <string>

bool copyFile(const std::string& from, const std::string& to, bool overwrite = false) {
    // Если не разрешено перезаписывать, проверим существование файла назначения
    if (!overwrite) {
        std::ifstream test(to, std::ios::binary);
        if (test.good()) {
            return false; // файл уже существует
        }
    }

    std::ifstream src(from, std::ios::binary);
    if (!src) return false;

    std::ofstream dst(to, std::ios::binary | std::ios::trunc);
    if (!dst) return false;

    dst << src.rdbuf();
    return true;
}

int main() {
    if (!copyFile("input.txt", "output.txt")) {
        std::cerr << "Copy failed\n";
    }
}
```

---

### Задача 79

> Создать класс `Image`, владеющий пиксельными данными. Реализовать конструкторы: по размерам, из файла (пока заглушка), копирующий конструктор.

```cpp
#include <iostream>
#include <cstring>

class Image {
    int width;
    int height;
    unsigned char* data;
public:
    // Конструктор по размерам
    Image(int w, int h)
        : width(w), height(h), data(nullptr) {
        if (width > 0 && height > 0) {
            data = new unsigned char[width * height * 4]; // RGBA
            std::memset(data, 0, width * height * 4);
        }
    }

    // Конструктор из "файла" (заглушка)
    explicit Image(const char* filename)
        : width(0), height(0), data(nullptr) {
        // Для примера создадим 1×1 белую картинку
        width = 1;
        height = 1;
        data = new unsigned char[4];
        data[0] = data[1] = data[2] = 255; // RGB
        data[3] = 255;                     // A
        std::cout << "Loaded image from " << filename << " (stub)\n";
    }

    // Конструктор копирования (глубокое копирование)
    Image(const Image& other)
        : width(other.width), height(other.height), data(nullptr) {
        if (width > 0 && height > 0 && other.data) {
            data = new unsigned char[width * height * 4];
            std::memcpy(data, other.data, width * height * 4);
        }
    }

    ~Image() {
        delete[] data;
    }
};

int main() {
    Image img1(100, 100);
    Image img2("file.png");
    Image img3 = img2; // вызов конструктора копирования
}
```

---

### Задача 94

> Написать класс `Path`, хранящий динамический массив точек, с конструктором копирования.

```cpp
#include <iostream>

struct Point {
    double x;
    double y;
};

class Path {
    Point* points;
    int size;
public:
    Path(int n = 0)
        : points(nullptr), size(n) {
        if (size > 0) {
            points = new Point[size];
            for (int i = 0; i < size; ++i) {
                points[i].x = 0.0;
                points[i].y = 0.0;
            }
        }
    }

    // Конструктор копирования: глубокое копирование
    Path(const Path& other)
        : points(nullptr), size(other.size) {
        if (size > 0) {
            points = new Point[size];
            for (int i = 0; i < size; ++i) {
                points[i] = other.points[i];
            }
        }
    }

    ~Path() {
        delete[] points;
    }

    int getSize() const { return size; }

    Point& operator[](int index) { return points[index]; }
    const Point& operator[](int index) const { return points[index]; }
};

int main() {
    Path p1(3);
    p1[0] = {0, 0};
    p1[1] = {1, 1};
    p1[2] = {2, 2};

    Path p2 = p1; // копирующий конструктор

    std::cout << p2.getSize() << '\n';
}
```
