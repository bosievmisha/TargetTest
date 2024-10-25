Тестовое задание
# Задачи
## Задание 1
Напишите функцию, которая в качестве аргумента принимает натуральное число n и возвращает сумму цифр этого числа. Если это значение имеет более одной цифры, продолжайте уменьшать его таким образом, пока не будет получено одноразрядное число. Это применимо только к натуральным числам. 
Пример: 	my_function(16)    1 + 6 = 7
   		my_function(942)    9 + 4 + 2 = 15    1 + 5 = 6

### Ответ
```csharp
static int sumOfDigits(int number)
{
    int temp = 0;
    while (number != 0)
    {
        temp += number % 10;
        number /= 10;
    }
    return temp;
}
```

## Задание 2
Напишите функцию, которая принимает количество американской валюты центы (cents) и возвращает словарь / хэш, который показывает наименьшее количество монет, используемых для создания этой суммы. Рассматриваются только номиналы монет: Pennies (1¢), Nickels (5¢), Dimes (10¢) and Quarters (25¢). Поэтому возвращаемый словарь должен содержать ровно 4 пары ключ / значение.

### Ответ
Поскольку данные монеты позволяют решить задачу жадным алгоритмом, так и поступим.
```csharp
static Dictionary<string, int> currency = new Dictionary<string, int>()
{
    { "Quarters", 25 },
    { "Dimes", 10 },
    { "Nickels", 5 },
    { "Pennies", 1 },
};
static Dictionary<string, int> Exchange(float number)
{
    var cents = new Dictionary<string, int>();
    foreach (var item in currency)
    {
        var temp = (int)(number / item.Value);
        cents.Add(item.Key, number > 0 ? temp : 0);
        number -= temp * item.Value;
    }
    return cents;
}
```

## Задание 3
Напишите функцию, которая может принимать любое неотрицательное целое число в качестве аргумента и возвращать его вместе с цифрами в порядке убывания. Переставьте цифры так, чтобы на выходе создать максимально возможное число.

### Ответ
```csharp
static int ArrangeDescending(int number)
{
    var digits = new int[10];
    while (number > 0)
    {
        digits[number % 10] += 1;
        number /= 10;
    }
    for (int i = 9; i > 0; i--)
    {
        for (int j = 0; j < digits[i]; j++)
        {
            number *= 10;
            number += i;
        }
    }
    return number;
}
```
## Задание 4
Дана пирамида чисел:

                    1
                3     5
            7     9    11
        13    15    17    19
    21    23    25    27    29
                ...
Напишите функцию, которая вычисляет сумму строки этого треугольника из переданного в функцию индекса строки (начиная с индекса 1).
Пример: 	my_function (2)  3 + 5  8

### Ответ
```csharp
static int calculateTriangle(int index)
{
    int firstNum = (index - 1) * index + 1;
    int sum = 0;

    for (int i = 0; i < index; i++)
    {
        sum += firstNum + i * 2;
    }

    return sum;
}
```

## Задание 5
Напишите функцию, которая не принимает аргументов и всегда возвращает 5. Звучит просто, не правда ли? Просто имейте в виду, что вы не можете использовать ни один из следующих символов: 
0 1 2 3 4 5 6 7 8 9 * + - /

## Ответ
```csharp
public static int getFive()
{
    string[] five = {"One", "Two", "Three", "Four", "Five" };
    return five.Length;
}
```
# SQL
1. Вывести список автомобилей, которые были созданы на базе авто той же марки (название авто)
```sql
SELECT a.Name
FROM Cars AS a
INNER JOIN Cars AS a2 ON a.BaseID = a2.ID
INNER JOIN Brands AS b ON a.BrandID = b.ID AND a2.BrandID = b.ID;
```
2. Вывести список марок, которые содержат больше 3 автомобилей в представленном списке (название марки)
```sql
SELECT Brands.Name 
FROM Cars 
JOIN Brands ON Cars.BrandID = Brands.id  
GROUP BY Brands.Name  
HAVING COUNT(Brands.Name) > 3
```
3. Вывести список марок с необходимой суммой на покупку всего модельного ряда (название марки + сумма)
```sql
SELECT b.Name, SUM(c.Price) AS TotalPrice
FROM Brands AS b
INNER JOIN Cars AS c ON b.ID = c.BrandID
GROUP BY b.Name;
```
4. Вывести список двух стран с максимальной средней мощностью автомобилей (название страны + средняя мощность)
```sql
SELECT TOP 2 co.Name, AVG(c.Pow) AS AvgPow
FROM Countries AS co
INNER JOIN Brands AS b ON co.ID = b.CountryID
INNER JOIN Cars AS c ON b.ID = c.BrandID
GROUP BY co.Name
ORDER BY AvgPow DESC;
```
5. Вывести список самых дешевых автомобилей каждой марки (название авто + название марки)
```sql
SELECT c.Name, b.Name
FROM Cars AS c
INNER JOIN Brands AS b ON c.BrandID = b.ID
WHERE c.Price = (SELECT MIN(Price) FROM Cars WHERE BrandID = c.BrandID);
```
