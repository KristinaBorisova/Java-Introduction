# Lecture 9
#java course#

## Inheritance (Наследяване) 🏛️

Наследяването е вторият основен принцип на ООП след енкапсулация. Проблема, който цели да реши
е да направи по-лесно преизползването на логика написана в различни класове. Начина, по който се постига
това презизползване чрез ООП, е като се изгражда йерархична връзка м/у отделните класове.

- Например

![inheritance-illustration](https://developer.hyvor.com/tutorials/static/images/php-oop-inheritance-2.png)
> Имаме една абстракция за животно, като имаме два конкретни представителя на тази абстракция и те са Куче и Котка.  
Или с други думи казваме че Куче и Котка наследяват абстракцията Животно

![4-pillars-of-oop](https://media.licdn.com/dms/image/C5112AQEk0LRh73xNYA/article-cover_image-shrink_720_1280/0?e=1564012800&v=beta&t=19rrny8585V5xxamUmLGfQrmHV6tyqQIcD2-skgUre0)
> Четирите основни принципа на ООП

При наследяването имаме `super class`, който представлява по-високото ниво в йерархията и наследяващ клас `child class`,
който представлява по-ниското ниво в йерархията. Така `child` (дете) класът наследява `super` класът.

В примера по-горе `Animal` е `super class`, а `Dog` и `Cat` са `child` класове на `Animal`.

### Какво може да бъде преизползвано чрез наследяване?

Когато един клас наследява друг клас наследника получава достъп до:

- methods (методи)
- properties (свойства)
- constructors (конструктори)

По този начин общата логика м/у отделните наследници може да бъде написа в `super` класът, а всички наследници 
на този клас да я преизползват.

Наследяването се осъществява чрез ключовата дума `extends`, която се изписва на нивото на класът.

- Пример

    - Animal.java (`super class`)
    
    ```java
    public class Animal {
    
        public int age;
    
        public void eat() {
            System.out.println("Eating...");
        }
    }
    ```
    
    > `Animal` класът дефинира property `age` и method `eat()`, които ще бъдат достъпни
    в `child` класовете
    
    - Dog.java (`child class`)
    
    ```java
    public class Dog extends Animal {
    
        public String breed;
    
        public void bark() {
            System.out.println("Woff woff...");
        }
    
        public void printDetailsAndEat() {
            // age е дефинирано в супер класът
            System.out.println("Breed: " + breed + " " + "Age: " + age);
    
            eat(); // този метод е дефиниран в супер класът
        }
    }
    ```
    
    > `Dog` наследява `Animal`, като класът дефинира ново property `breed` (порода), method `bark()` (лая)
    и method `printDetailsAndEat()`, които са достъпни само в `Dog` класът. 
    `Dog` също така получава достъп до `age` и `eat()` от супер класът.
    
    - Cat.java (`child class`)
    
    ```java
    public class Cat extends Animal {
    
        public int numberOfLives;
    
        public void purr() {
            System.out.println("PurRrRr...");
        }
    
        public void printDetailsAndEat() {
            // age е дефинирано в супер класът
            System.out.println("Num of Lives: " + numberOfLives + " " + "Age: " + age);
    
            // този метод е дефиниран в супер класът
            eat();
        }
    }
    ```
    
    > `Cat` наследява `Animal`, като класът дефинира ново property `numberOfLives` (брой животи), method `purr()` (мърка)
    и method `printDetailsAndEat()`, които са достъпни само в `Cat` класът. 
    `Cat` също така получава достъп до `age` и `eat()` от супер класът.
    

### Method Overloading
В Java можем да създадем два метода с еднакво име, еднакви return типове, но различни на борй или тип входни параметри.
Като методът, който ще бъде извикан се определя от входните параметри, които биват подавани.

Това свойство на Java се нарича Method Overloading.

- Пример

    ```java
    class Foo {
        void doSomething(int a) {
            System.out.println(a);
        }
        
        void doSomething(String a) {
            System.out.println(a);
        }
        
        void doSomething(int a, String b) {
            System.out.println(a + " " + b);
        }
    }
    ```
    > В този случай казваме, че методът `doSomething` е overload-нат

### Constructors and chaining

Ще разгледаме в повече детайли как можем да обвържем няколко конструктора на един и същи клас.
Като примерите, които ще разгледаме ще са за клас, който не наследява нищо и клас, който наследява друг клас.

Логически **constructor chaining** може да се разглежда, като **method overloading**. 
Като задължително при извикването на първия конструктор се извиква и втория и третия ако има такъв и тнт...

#### Constructor chaining без наследяване

Ако един клас има 2 конструктора, то ние сме задължени, когато инстанцираме класът да използваме един от 2-та конструктора.
Така например единия конструктор може да приема 2 параметъра, а другия 3.  
Възможно е да навържим така първия конструктор, че той да предава 2-та параметъра на конструктора с 3 параметъра.  
Това става с помоща на ключовата дума `this`.

- Пример

    ```java
    class Person {
        
        final String firstName;
        final String middleName;
        final String lastName;
        
        Person(String firstName) {
            this(firstName, null); // конструкторът с 1 параметър извиква конструктора с 2 параметъра
        }
        
        Person(String firstName, String lastName) {
            this(firstName, null, lastName); // конструкторът с 2 параметъра извиква конструктора с 3 параметъра
        }
      
        Person(String firstName, String middleName, String lastName) {
            this.firstName = firstName;
            this.middleName = middleName;
            this.lastName = lastName;
        }
       
    }
    ```
    
В случаят използваме ключовата дума `this` в 2 от конструкорите като метод `this(param1, param2)`. 
В третия конструктор с три параметръра използваме ключовата дума `this` за да достъпим свойствата на класа.

#### Constructor chaining с наследяване

Ако имаме `super class`, който дефинира 1 конструктор всички наследници са длъжни да извикат този конструктор,
при тяхното инстанциране. Това става чрез ключовата дума `super` в конструктора на `child` класът.

- Пример

    ```java
    class Person {
      
        final String firstName;
        final String lastName;
        final boolean isMale;
    
        Person(String firstName, String lastName, boolean isMale) {
            this.firstName = firstName;
            this.lastName = lastName;
            this.isMale = isMale;
        }
    }  
  
    class Male extends Person {
            
        Male(String firstName, String lastName) {
            super(firstName, lastName, true); // извикваме конструктора на Person с ключовата дума super
        } 
    }
    ```
    
В случая ползваме ключовата дума като метод `super(param1, param2, param3)`, обаче тя може да бъде ползвана и
за достъпване на методи и променливи от super класът.
    
### Java Object class

В Java всичко наследява класът `Object`. Той е супер класът на всеки един клас.

От този клас получаваме няколко често използвани метода:

- toString
- equals
- hashCode

### toString

Сигнатурата на този метод е следната `String toString()`. Този метод се използва, когато искаме да получим
текстова репрезентация на даден обект. Имплементацията на `toString` идваща от `Object` класът, връща текстовата
репрезентация на адреса на обекта в паметта. За това когато принтираме със `System.out.println(myObject)`
се принтира адреса на обекта вместо неговото съдържание.

> Знаете ли че `System.out.println()` извиква `toString` метода на класът.

### equals

Сигнатурата на този метод е следната `boolean equals(Object otherObject)`. Този метод се използва, когато искаме
да проверим дали една инстанция на обект е равна на друга инстанция. Методът приема 1 параметър 
(обектът срещу който ще се сравнява) и връща `boolean` резултат. true ако са еднакви false в противен случай.
Имплементацията на `equals` идваща от `Object` класът сравнява адресите на променливите вместо да сравнява съдържанието
на променливите.

### hashCode

Сигнатурата на този мето е следната `int hashCode()`. Този метод се използва когато [хешираме][hash-function]
даден обект. Целта на това хеширане е да прекараме данните на един обект през математически функции и да получим
число. Това число може да бъде използвано като числова репрезентация на данните. Като задължително крайния резултат
от хеширането на една и съща променлива n на брой пъти трябва да е еднакъв.

> Ще разгледаме хеширащите функции в повече детайли следващите лекции

[hash-function]: https://bg.wikipedia.org/wiki/%D0%A5%D0%B5%D1%88-%D1%84%D1%83%D0%BD%D0%BA%D1%86%D0%B8%D1%8F

### Method Overriding (пренамисване на метод)

Когато един клас наследява друг клас, то първия има възможността да пренапише функционалността на някои от методите
на super класът. Това нещо се нарича Override (презаписване/пренаписване).
Като за четимост методите, които биват пренаписани се обозначават с `@Override` над сигнатурата им.

- Пример

    ```java
    class Animal {
        
        void speak() { // класът Animal дефинира метод speak
            System.out.println("Speaking...");
        }
    }
    
    class Dog extends Animal { // Dog наследява Animal
        
        @Override   // обозначаваме че методът е пренаписан и идва от super класът
        void speak() { // Класът Dog пренаписва (override) методът speak от класът Animal
            System.out.println("Woff woff...");
        }
    }
    ```
    
    > `new Animal().speak()` ще изпише `Speaking...`, а `new Dog().speak()` ще изпише `Woff woff...`

---


### Exercises

### Task 1
Създайте програма, която симулира работата на болница. 🏥  
В една болница има няколко участника:
- Доктори (Doctor)
- Пациенти (Patient)

И докторите и пациентите се характеризират с:
- име (name)
- възраст (age)
- дали е мъж или жена  (isFemale)

Един пациент се характеризира с:
- Диагноза (diagnose)
    - примерна диагноза може да е `кардиолог` (това означава че трябва да посети кардиолог)    
- Способността да му се поставя диагноза (setDiagnose)
- Способността да му се премахва диагноза (removeDiagnose)

Докторите се характеризират с:
- способността да лекуват пациенти (heal) (просто премахват диагнозата на пациента)

Докторите се делят на различни под типове:
- Кардиолог (Cardiologist)
    - лекува само диагнози тип `кардиолог`
- Дерматолог (Dermatologist)
    - лекува само диагнози тип `дерматолог`
- Педиатър (Pediatrician)
    - лекува само пациенти на възраст под 18 години


Болницата е това което навръзва докторите с пациентите. Тя се характеризира с:
- множество доктори
- способността да се добавя доктор
- способността да се лекува пациент
    - за целта болницата намира лекаря, който може да излекува пациента и го лекува
    
###### Примерна йерархия на програмата

- class Person
    - class Patient
        - class MalePatient 
        - class FemalePatient
    - class Doctor
        - class Cardiologist
        - class Dermatologist
        - class Pediatrician
    
<br/><details><summary><b>Solution</b> 👀</summary> 
<p>

- Person.java
```java
/**
 * Клас който представлява човек.
 * Този клас съдържа общите свойства м/у пациенти и лекари.
 */
class Person {

    final String name;
    final int age;
    final boolean isFemale;

    Person(String name, int age, boolean isFemale) {
        this.name = name;
        this.age = age;
        this.isFemale = isFemale;
    }

    @Override
    public String toString() {
        return "Person{ " + name + " " + age + " " + isFemale + " }";
    }
}
```

- Patient.java

```java
/**
 * Клас пациент, който наследява {@link Person}.
 * Така пациента има достъп до името, годините и пола на човека.
 * <p>
 * Този клас надгражда с това че добавя диагноза и няколко метода, които оперират с диагнозата.
 */
class Patient extends Person {

    private String diagnose;

    Patient(String name, int age, boolean isFemale) {
        super(name, age, isFemale);
    }

    public void setDiagnose(String diagnose) {
        this.diagnose = diagnose;
    }

    public String getDiagnose() {
        return diagnose;
    }

    public void removeDiagnose() {
        diagnose = null;
    }
}
```

- MalePatient.java

```java
/**
 * Клас МъжкиПациент, който наследява {@link Patient}.
 * Единственото, което прави този клас е да създава нов конструктор с един параметър по-малко и подава false,
 * като параметър за пол на super конструктора.
 */
class MalePatient extends Patient {

    MalePatient(String name, int age) {
        super(name, age, false);
    }
}
```

- FemalePatient.java

```java
/**
 * Клас ЖенскиПациент, който наследява {@link Patient}.
 * Единственото, което прави този клас е да създава нов конструктор с един параметър по-малко и подава true,
 * като параметър за пол на super конструктора.
 */
class FemalePatient extends Patient {

    FemalePatient(String name, int age) {
        super(name, age, true);
    }
}
```

- Doctor.java

```java
/**
 * Абстрактен клас доктор. Този клас наследява {@link Person}.
 * Класът дефинира метода heal за лекуване на пациенти, както и абстрактен метод canHeal, който ще бъде
 * дефиниран от всеки вид доктор. Този клас понеже е абстрактен не може да бъде инстанциран директно.
 * Необходимо е да има наследник на този клас за да може да бъде създаден.
 */
abstract class Doctor extends Person {

    public Doctor(String name, int age, boolean isFemale) {
        super(name, age, isFemale);
    }

    /**
     * Метод който лекува пациента, единствено ако пациента може да бъде излекуван от текущия лекар.
     * Този метод използва абстрактния метод {@link Doctor#canHeal(Patient)}
     *
     * @param patient пациента, който ще бъде излекуван.
     * @return true ако пациента е успешно излекуван, false в противен случай.
     */
    public boolean heal(Patient patient) {

        if (canHeal(patient)) {
            patient.removeDiagnose();
            return true;
        }

        return false;
    }

    @Override
    public String toString() {
        return "Doctor{ " + name + " " + age + " }";
    }

    /**
     * Абстрактен метод, който ще пъде задължителен за всеки наследник на този клас.
     * Наследникът е длъжен да имплементира този метод.
     *
     * @param patient пациента, който ще бъде лекуван.
     * @return true ако пациента може да бъде излекувам от този лекар, false в противен случай.
     */
    public abstract boolean canHeal(Patient patient);
}
```

- Cardiologist.java

```java
/**
 * Клас който представлява специализиран доктор кардиолог.
 * <p>
 * Този тип доктор мое да лекува пациенти само с диагноза "кардиолог".
 */
class Cardiologist extends Doctor {

    public Cardiologist(String name, int age, boolean isFemale) {
        super(name, age, isFemale);
    }

    @Override // класът Cardiologist имплементира абстрактния метод canHeal дефиниран в Doctor класът
    public boolean canHeal(Patient patient) {
        return "кардиолог".equals(patient.getDiagnose());
    }
}
```

- Dermatologist.java

```java
/**
 * Клас който представлява специализиран доктор дерматолог.
 * <p>
 * Този тип доктор мое да лекува пациенти само с диагноза "дерматолог".
 */
class Dermatologist extends Doctor {

    public Dermatologist(String name, int age, boolean isFemale) {
        super(name, age, isFemale);
    }

    @Override // класът Dermatologist имплементира абстрактния метод canHeal дефиниран в Doctor класът
    public boolean canHeal(Patient patient) {
        return "дерматолог".equals(patient.getDiagnose());
    }
}
```

- Pediatrician.java

```java
/**
 * Клас който представлява специализиран доктор педиатър.
 * <p>
 * Този тип доктор мое да лекува пациенти само под 18 години".
 */
class Pediatrician extends Doctor {

    public Pediatrician(String name, int age, boolean isFemale) {
        super(name, age, isFemale);
    }

    @Override // класът Pediatrician имплементира абстрактния метод canHeal дефиниран в Doctor класът
    public boolean canHeal(Patient patient) {
        return patient.age < 18;
    }
}
```

- Hospital.java

```java
/**
 * Репрезентация на болница, която свързва лекарите с пациентите.
 */
class Hospital {

    private Doctor[] doctors = new Doctor[10];

    /**
     * Метод добавяш лекари в болницата.
     *
     * @param doctor лекарят който ще бъде добавен в болницата.
     */
    public void addDoctor(Doctor doctor) {

        for (int i = 0; i < doctors.length; i++) {

            if (doctors[i] == null) {
                doctors[i] = doctor;
                return;
            }
        }
    }

    /**
     * Метод приемащ пациент, който да бъде излекуван.
     * Този метод се грижи за това да намери доктор от съществуващите в болницата
     * и да го използва за да излекува пациента
     *
     * @param patient пациента който трябва да бъде излекуван.
     */
    public void heal(Patient patient) {

        for (Doctor doctor : doctors) {
            if (doctor == null) {
                continue;
            }

            boolean healed = doctor.heal(patient);

            if (healed) {
                System.out.printf("Доктор %s излекува пациент %s\n", doctor, patient);
                return;
            }
        }

        System.out.printf("Не беше намерен лекар, който да излекува %s\n", patient);

    }
}
```    

- HospitalDemo.java

```java
public class HospitalDemo {

    public static void main(String[] args) {

        // Създаване на различните видове доктори
        Cardiologist cardiolog = new Cardiologist("Ivan", 40, false);
        Dermatologist dermatholog = new Dermatologist("Joana", 40, true);
        Pediatrician pediater = new Pediatrician("Georgi", 40, false);

        // Създаване на болницата
        Hospital hospital = new Hospital();

        // Добавяне на докторите в болницата
        hospital.addDoctor(cardiolog);
        hospital.addDoctor(dermatholog);
        hospital.addDoctor(pediater);

        // Създаване на малолетен пациент
        Patient goshko = new MalePatient("Goshko", 15);

        // Създаване на пациент с диагноза 'дерматолог'
        Patient lyudmila = new FemalePatient("Lyudmila", 30);
        lyudmila.setDiagnose("дерматолог");

        // Създаване на пациент с диагноза 'кардиолог'
        Patient parvan = new MalePatient("Parvan", 30);
        parvan.setDiagnose("кардиолог");

        // Излекуване на пациентите
        hospital.heal(goshko);
        hospital.heal(lyudmila);
        hospital.heal(parvan);
    }
}
```
</p>
</details>