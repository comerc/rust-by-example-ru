# Вложенность и метки

Можно прерывать выполнение внешних циклов с помощью `break` или `continue`,
когда речь заходит о вложенных циклах.
Для этого циклы должны быть обозначены метками вроде `'label`,
а метки должны быть переданы операторам `break` или `continue`.

```rust,editable
#![allow(unreachable_code)]

fn main() {
    'outer: loop {
        println!("Вошли во внешний цикл");

        'inner: loop {
            println!("Вошли во внутренний цикл");

            // Это прервёт лишь внутренний цикл
            //break;

            // Это прервёт внешний цикл
            break 'outer;
        }

        println!("Эта точка не будет достигнута");
    }

    println!("Вышли из внешнего цикла");
}
```