# Вопросы и ответы на собеседовании iOS разработчика.

### Бинарный поиск
Бинарный поиск производится в упорядоченном массиве. При бинарном поиске искомый ключ сравнивается с ключом среднего элемента в массиве. Если они равны, то поиск успешен. В противном случае поиск осуществляется аналогично в левой или правой частях массива.
```swift
func binarySearch<T: Comparable>(_ a: [T], key: T, range: Range<Int>) -> Int? {
    if range.lowerBound >= range.upperBound {
        return nil
    } else {
        let midIndex = range.lowerBound + (range.upperBound - range.lowerBound) / 2
        if a[midIndex] > key {
            return binarySearch(a, key: key, range: range.lowerBound ..< midIndex)

        } else if a[midIndex] < key {
            return binarySearch(a, key: key, range: midIndex + 1 ..< range.upperBound)

        } else {
            return midIndex
        }
    }
}
```


### Как называется файловая система используемая на iOS?
До марта 2017 года использовалась HFS+, после Apple внедрила новую файловую систему под названием APFS. 


### Какие объекты можно добавлять в качестве ключей к NSDictionary
Вы можете использовать пользовательские объекты в качестве ключей в словаре, но есть два момента: 
- Ключи должны соответствовать NSCopying протоколу.
- Ключи должны реализовать hash и isEqual: методы, потому что словарь использует хэш-таблицу, чтобы организовать его хранение и быстрый доступ к содержащимся объектам.


### Какие типы хранилищ core data доступны "из коробки" для ios
- XML
- In-Memory
- SQLite
- Binary


### По умолчанию @property объявляются со следующим атрибутом атомарности
Дефолтное значение атомарности atomic


### Что выведется в лог
```objective-c
- (void)viewDidLoad {
    [super viewDidLoad];
    
    __block int count = 0;
    void (^countBlock)() = ^() {
        NSLog(@"%d", count);
    };
    
    count++;
    NSLog(@"%d", count);
    countBlock();
}
```
В лог выведется 1, 1


### Что выведется в лог
```objective-c
- (void)viewDidLoad {
    [super viewDidLoad];
    
    dispatch_async(dispatch_get_main_queue(), ^
    {
        NSLog(@"A");
        dispatch_async(dispatch_get_main_queue(), ^
        {
            NSLog(@"B");
        });
        NSLog(@"C");
    });
    NSLog(@"D");
}
```
В лог выведется D A C B












