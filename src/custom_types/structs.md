# Структуры

Существует три типа структур, которые можно создать с помощью ключевого слова `struct`:

* Кортежная структура, которая, в общем, является именованным кортежем.
* Классическую [C структуру][c_struct]
* Единичную структуру, которая не имеет полей, но может быть полезна для обобщённых типов.

```rust,editable
#[derive(Debug)]
struct Person<'a> {
    name: &'a str,
    age: u8
}

// Единичная структура
struct Nil;

// Кортежная структура
struct Pair(i32, f64);

// Структура с двумя полями
struct Point {
    x: f64,
    y: f64,
}

// Структуры могут быть использованы как поля другой структуры
#[allow(dead_code)]
struct Rectangle {
    p1: Point,
    p2: Point,
}

fn main() {
    // Создаём структуру с помощью короткой инициализации полей
    let name = "Петя";
    let age = 27;
    let peter = Person { name, age };
    
    // Дебаг вывод структуры
    println!("{:?}", peter);
    
    
    // Создаём структуру `Point`
    let point: Point = Point { x: 0.3, y: 0.4 };

    // Получаем доступ к полям структуры `Point`
    println!("Координаты точки: ({}, {})", point.x, point.y);

    // Деструктурируем `Point` создавая связь с помощью `let`
    let Point { x: my_x, y: my_y } = point;

    let _rectangle = Rectangle {
        // инициализация структуры так же является выражением
        p1: Point { x: my_y, y: my_x },
        p2: point,
    };

    // Создаём связь с единичной структурой
    let _nil = Nil;

    // Создаём связь с кортежной структурой
    let pair = Pair(1, 0.1);

    // Деструктурируем кортежную структуру
    let Pair(integer, decimal) = pair;

    println!("Pair хранит в себе {:?} и {:?}", integer, decimal);
}
```

### Задание

1. Добавьте функцию `rect_area`, которая рассчитывает площадь прямоугольника.
(попробуйте использовать "деструктуризацию" (разбор на части) ).
2. Добавьте функцию `square`, которая принимает в качестве аргументов `Point` и `f32`,
а возвращает `Rectangle`, левый нижний угол которого соответствует `Point`,
а ширина и высота соответствуют `f32`.

### Смотрите также:

[`атрибуты`][attributes] и [деструктуризация][destructuring]

[attributes]: attribute.html
[c_struct]: https://ru.wikipedia.org/wiki/Структура_(язык_Си)
[destructuring]: flow_control/match/destructuring.html
