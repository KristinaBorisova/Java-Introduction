# Lecture 6
#java course#

## String & OOP Exercises

### Какво е `String`?

`String` е **class**, който репрезентира текст. За разлика от другите типове данни, 
които изучавахме, той не е примитивен, а е съставен от примитивни типове.

`String` се характеризира с това че има `n` на брой символи `char`. Или с други думи
масив от символи `char[n]`.

В Java можем да различим `char` от `String`, поглеждайки броя на кавичките.  
`char` се създава с единични кавички `char a ='A';`, а `String` с двойни кавички
`String a = "A";`

> типът `char` репрезентира само 1 символ

###### Дължина на `String`

Дължината може да бъде достъпена чрез методът `length()`.

- Пример

    ```java
    String foo = "foo";
    
    System.out.println(foo.length()); // принтира 3
    ```

    > Начина по който достъпваме дължината на текста се различава от начина,
     по който достъпваме дължината на масив. В първия случай ползваме **method** `length()`,
     а във втория **property** `length`.


###### Събиране на `String`

Един `String` може да бъде събиран с друг `String`, като резултата е трети `String` 

- Пример

    ```java
    String firstName = "John";
    String lastName = "Doe";
    
    String name = firstName + lastName;
    
    System.out.println(name); // Принтира John Doe
  
    int age = 30;
    String nameAndNumber = name + age;
  
    System.out.println(nameAndNumber); // Принтира John Doe30
    ```
    
    > Текстът може да бъде само събиран с други типове данни и не може да бъде изваждан, умножаван и тнт...

###### Има разлика м/у символ (`char`), масив от символи (`char[]`) и текст (`String`)

Общото м/у трите типа е символът `char`, но те се различават с това,
че всеки следващ тип надгражда над предеходния.

```java
char char1 = 'J';
char char2 = 'o';
char char3 = 'h';
char char4 = 'n';

char[] chars = {'J', 'o', 'h', 'n'}

String myString = "John";
```

###### Създаване на `String`

`String` се създава с двойни кавички.

```java
String firstString = "John";

String secondString = new String("John");
```
> Втория начин за създаване на `String` не е за предпочитане.


###### Как да проверяваме за еднаквост (equality)?
`String` е сложен тип или също така референтен тип.
Това означава,цче ако използваме оператор за сравнение `==`, 
ние ще сръвним адреси в паметта. За да сравним текста,
който е репрезентиран от конкретния `String`, може да 
ползваме **method** `equals()`

- Пример
    ```java
    String firstString = "John";
    
    String secondString = new String("John");
    
    String firstPart = "Jo";
    String secondPart = "hn";
    
    String thirdString = firstPart + secondPart;
    
    System.out.println(firstString == secondString);   // false
    System.out.println(firstString == thirdString);    // false
    
    System.out.println(firstString.equals(secondString));  // true
    System.out.println(firstString.equals(thirdString));   // true
    ```
    > Методът `equals` има 1 аргумент (параметър)

---

### Exercises

#### Task 1

```
Моделирайте животното хамелион. Един хамелион се характеризира с:
• цвят (color
• тегло (weight)
• способността да сменя цветът си (change color)

Хамелионът може да приема всякакъв цвят освен сив (gray)
```
> смяната на цвят  ще е **method**, който има 1 параметър, новият цвят 🦎
