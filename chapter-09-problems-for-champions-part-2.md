# Chapter 9.2. Problems for Champions – Part II

In this chapter we will review three additional problems that belong to the category "**For Champions**", i.e. they are more complex than the rest of the problems in this book.


## More Complex Problems on the Studied Material

Before we move on to particular tasks, we must clarify that these can be solved in an easier way with **additional knowledge in programming with Java** (methods, arrays, collections, recursion, etc.), but each solution that will be provided now only uses the material covered in this book. The goal is to learn how to construct **more complex algorithms** based on your knowledge collected up to the present moment.


## Problem: Passion Shopping Days

Lina has a real shopping passion. When she has some money, she immediately goes to the closest shopping center (mall) and tries to spend as much as she can on clothes, bags and shoes. But her favorite thing are winter sales. Our task is to analyze her strange behavior and  **calculate the purchases** that Lina does when she enters the mall, as well as the **money she has left** when the shopping is over. All prices and money are in BGN (Bulgarian levs, **lv**).

The **first line** of the input will pass the **amount** that Lina has **before** she starts shopping. After that, upon reading the "**`mall.Enter`**" command, Lina enters the mall and starts shopping until the "**`mall.Exit`**" command is given. When Lina starts shopping, **on each line** of the input you will be given strings that are **actions performed by Lina**. Each **symbol** in the string is a **purchase or another action**. String commands contain only symbols of the **ASCII table**. The ASCII code of each sign is **related to what Lina must pay** for each of the goods. You need to interpret the symbols in the following way:

- If the symbol is a **capital letter**, Lina gets a **50% discount**, which means that you must decrease the money she has by 50% of the numeric representation of the symbol from the ASCII table.
- If the symbol is a **small letter**, Lina gets a **70% discount**, which means that you must decrease the money she has by 30% of the numeric representation of the symbol from  the ASCII table.
- If the symbol is **"`%`"**, Lina makes a **purchase** that decreases her money in half.
- If the symbol is **"`*`"**, Lina **withdraws money from her debit card** and adds 10 lv. to her available funds.
- If the symbol is **different from all of the aforementioned**, Lina just makes a purchase without discount, and in this case you should simply subtract the value of the symbol from the ASCII table from her available funds.

If a certain value of her purchases is **higher** than her current available funds, Lina **DOES NOT** make the purchase. Lina's funds **cannot be less than 0**.

The shopping ends when the "**`mall.Exit`**" command is given. When this happens, you need to **print the number of purchases made and the money** that Lina has left.

### Input Data

The input data must be read from the console. The **first line** of the input will indicate the **amount that Lina has before starting to purchase**. On each of the following lines there will be a particular command. After you read the command "**`mall.Enter`**", on each of the following lines you will be given strings holding **information regarding the purchases / actions** that Lina wants to perform. These strings will keep being passed, until the "**`mall.Exit`**" command is given.

Always only one "**`mall.Enter`**" command will be given, as well as only one "**`mall.Exit`**" command.

### Output Data

The output data must be **printed on the console**.
When shopping is over, you must print on the console a particular output depending on what purchases have been made.
- If **no purchases have been made** – "**No purchases. Money left: {remaining funds} lv.**"
- If **at least one purchase** is made – "**{number of purchases} purchases. Money left: {remaining funds} lv.**"

**The funds** must be printed with **accuracy of up to 2 symbols after the decimal point**.

### Constraints

- Money is a **float** number within the range: [**0 - 7.9 x 10<sup>28</sup>**].
- The number of strings between "**`mall.Enter`**" and "**`mall.Exit`**" will be within the range: [**1-20**].
- The number of symbols in each string that represents a command will be within the range: [**1-20**].
- Allowed execution time: **0.1 seconds**.
- Allowed memory: **16 MB**.

### Sample Input and Output

| Input | Output | Comment |
|------|-------|----------|
| 110<br>mall.Enter<br>d<br>mall.Exit | 1 purchases. Money left: 80.00 lv. | ‘d’ has an ASCII code of 100. ‘d’ is a small letter, this is why Lina gets a 70% discount. She spends 30% of 100, which is 30 lv. After this purchase, she has: 110 - 30 = 80 lv. |

| Input | Output |Input | Output |
|------|-------|------|-------|
| 110<br>mall.Enter<br>%<br>mall.Exit|1 purchases. Money left: 55.00 lv.| 100<br>mall.Enter<br>Ab<br>\*\*<br>mall.Exit|2 purchases. Money left: 58.10 lv.|

### Hints and Guidelines

We will separate the solution of the problem into three main parts:
- Processing of the **input**.
- **Algorithm** for solving the problem. 
- Formatting the **output**.

Let's examine each of the parts in details.

#### Processing the Input Data

The input of our task consists of a few components:
- On the **first line we have all the money** that Lina has for shopping.
- On **each of the following lines** we will have some kind of a **command**.

The first part from the reading is trivial. We should keep in mind that we will be using the **`BigDecimal`** type, because we are working with money and we need precise accuracy:

![](assets/chapter-9-2-images/01.Passion-days-01.png)

The second one contains a detail that we need to take into consideration. The requirements state the following:

> On each of the following lines there will be a particular command. After you read the command "**`mall.Enter`**", on each of the following lines you will be given strings containing information regarding the purchases / actions that Lina wants to perform.

This is where we need to take into consideration the fact that from the **second input line on, we need to start reading commands**, but **only after we read** the command **"mall.Enter"**, we must start processing them. How can we do this? Using a **`while`** or a **`do-while`** loop is a good option. Here is an exemplary solution of how **to skip** all commands before processing the command "**`mall.Enter`**":

![](assets/chapter-9-2-images/01.Passion-days-02.png)

Here is the place to point out that calling  **`scanner.nextLine()`** after the end of the loop is used for **moving to the first command** for processing.

#### Algorithm for Solving the Problem

The algorithm for solving the problem is a direct one – we continue **reading commands** from the console, **until the command "mall.Exit" is passed**. In the meantime, we **process** each symbol (**`char`**) of each one of the commands according to the rules specified in the task requirements, and in parallel, we **modify the amount** that Lina has, and **store the number of purchases**.

Let's examine the first two problems for our algorithm. The first problem concerns the way we read the commands until we reach the **"mall.Exit"** command. The solution that we previously saw uses a **`while-loop`**. The second problem for the task is to **access each symbol** of the command passed. Keeping in mind that the input data with the commands is **`String`** type, the easiest way to access each symbol inside the strings is via a **`foreach` loop**. 

This is how the code will look like when using those two type of loops:

![](assets/chapter-9-2-images/01.Passion-days-03.png)

The next part of the algorithm is to **process the symbols from the commands**, according to the following rules in the requirements:

> * If the symbol is a **capital letter**, Lina gets a 50% discount, which means that you must decrease the money she has by 50% of the numeric representation of the symbol from the ASCII table.
> * If the symbol is a **small letter**, Lina gets a 70% discount, which means that you must decrease the money she has by 30% of the numeric representation of the symbol from the ASCII table.
> * If the symbol is **"%"**,  Lina makes a purchase that decreases her money in half.
> * If the symbol is **"\*"**, Lina withdraws money from her debit card and adds 10 lv. to her available funds.
> * If the symbol is **different from all of the aforementioned**, Lina just makes a purchase without discount, and in this case you should simply subtract the value of the symbol from the ASCII table from her available funds.

Let's examine the problems that we will be facing in the first condition. The first one is how to distinguish if a particular **symbol is a capital letter**. We can use one of the following ways:
* Keeping in mind the fact that the letters in the alphabet have a particular order, we can use the following condition **`action >= 'A' && action <= 'Z'`**, in order to check if our symbol is within the capital letters range.
* We can use the **`char.IsUpper(..)`** function.

The other problem is how **to skip a particular symbol**, if it is not an operation that requires more money that Lina has. This is doable using the **`continue`** construction.

An exemplary condition for the first part of the requirements looks like this:

![](assets/chapter-9-2-images/01.Passion-days-04.png)

**Note**: the variable “**`purchases`**” is of **`int`** type, in which we store the number of all purchases.

We believe the reader should not have difficulties implementing all the other conditions because they are very similar to the first one.

#### Formatting the Output

In the end of our task we must **print** a particular **output**, depending on the following condition:

> - If no purchases have been made – "**No purchases. Money left: {remaining funds} lv.**"
> - If at least one purchase is made – "**{number of purchases} purchases. Money left: {remaining funds} lv.**"

The printing operations are trivial, as the only thing we need to take into consideration is that **the amount has to be printed with accuracy of up to 2 symbols after the decimal point**.

How can we do that? We will leave the answer to this question to the reader.

### Testing in the Judge System

Test your solution here: [https://judge.softuni.bg/Contests/Practice/Index/664#0](https://judge.softuni.bg/Contests/Practice/Index/664#0).


## Задача: числен израз

Бони е изключително могъща вещица. Тъй като силата на природата не е достатъчна, за да се бори успешно с вампири и върколаци, тя започнала да усвоява силата на Изразите. Изразът е много труден за усвояване, тъй като заклинанието разчита на способността за **бързо решаване на математически изрази**.

За използване на "Израз заклинание", вещицата трябва да знае резултата от математическия израз предварително. **Израз заклинанието** се състои от няколко прости математически израза. Всеки математически израз може да съдържа оператори за **събиране**, **изваждане**, **умножение** и/или **деление**.

Изразът се решава без да се вземат под внимание математическите правила при пресмятане на числови изрази. Това означава, че приоритет има последователността на операторите, а не това какъв вид изчисление правят. Израза **може да съдържа скоби**, като **всичко в скобите се пресмята първо**. Всеки израз може да съдържа множество скоби, но не може да съдържа вложени скоби:
- Израз съдържащ **(…(…)…) е невалиден**.
- Израз съдържащ **(…)…(…) е валиден**.

### Пример

Изразът

![](assets/chapter-9-2-images/02.X-expression-01.png)

бива решен по следния начин:

![](assets/chapter-9-2-images/02.X-expression-02.png)

Бони е много красива, но не чак толкова съобразителна, затова тя има нужда от нашата помощ, за да усвои силата на Изразите.

### Входни данни

Входните данни се състоят от един ред, който бива подаван от конзолата. Той съдържа **математическият израз за пресмятане**. Редът **винаги завършва със символа "="**. Символът **"="** означава **край на математическия израз**.

Входните данни винаги са валидни и във формата, който е описан. Няма нужда да бъдат валидирани.

### Изходни данни

Изходните данни трябва да се принтират на конзолата. Изходът се състои от един ред – резултата от **пресметнатия математически израз**.

Резултатът трябва да бъде **закръглен до втората цифра след десетичния знак**.

### Ограничения

- Изразите ще състоят от **максимум 2500 символа**.
- Числата от всеки математически израз ще са в интервала [**1 … 9**].
- Операторите в математическите изрази винаги ще бъдат измежду **`+`** (събиране), **`-`** (изваждане), **`/`** (деление) или **`*`** (умножение).
- Резултатът от математическия израз ще е в интервала [**-100000.00 … 100000.00**].
- Позволено време за изпълнение: **0.1 секунди**.
- Позволена памет: **16 MB**.

### Примерен вход и изход

| Вход                           | Изход  |Вход                           | Изход  |
|--------------------------------|--------|-------------------------------|--------|
| 4+6/5+(4\*9–8)/7\*2=           | 8.57   |3+(6/5)+(2\*3/7)\*7/2\*(9/4+4\*1)= | 110.63 |

### Насоки и подсказки

Както обикновено, първо ще прочетем и обработим входа, след това ще решим задачата и накрая ще отпечатаме резултата, форматиран, както се изисква.

#### Обработване на входа

Входните данни се състоят от точно един ред от конзолата. Тук имаме **два начина**, по които можем да обработим входа. Първият е чрез **прочитането на целия ред с командата `bufferReader.readLine()`**(където **`bufferReader`** е променлива от тип **`BufferedReader`**) и достъпването на всеки един символ (**`char`**) от реда чрез **`foreach` цикъл**. Вторият е чрез **прочитане на входа символ по символ чрез командата `bufferReader.read()`** и обработване на всеки символ.

За решаване на задачата ще използваме втория вариант.

![](assets/chapter-9-2-images/02.X-expression-03.png)

#### Алгоритъм за решаване на задачата

За целите на нашата задача ще имаме нужда от две променливи:
* Една променлива, в която ще пазим **текущия резултат**.
* Още една променлива, в която ще пазим **текущия оператор** от нашия израз.

![](assets/chapter-9-2-images/02.X-expression-04.png)

Относно кода по-горе трябва да поясним следния детайл. Стойността по подразбиране на оператора е **`+`**, за да може още първото срещнато число да бъде събрано с резултата ни.

След като вече имаме началните си променливи, трябва да помислим върху това **каква ще е основната структура** на нашата програма. От условието разбираме, че **всеки израз завършва с `=`**, т.е. ще трябва да четем и обработваме символи, докато не срещнем **`=`**. Следва точното изписване на **`while` цикъл**.

![](assets/chapter-9-2-images/02.X-expression-05.png)

Следващата стъпка е обработването на нашата **`symbol`** променлива. За нея имаме 3 възможни случая:
* Ако символът е **начало на подизраз, заграден в скоби**, т.е. срещнатият символ е **`(`**.
* Ако символът е **цифра между 0 и 9**. Но как можем да проверим това? Как можем да проверим дали символът ни е цифра? Тук идва на помощ **ASCII кодът** на символа, чрез който можем да използваме следната формула: **`[ASCII кода на нашия символ] - [ASCII кода на символа 0] = [цифрата, която репрезентира символа]`**. Ако **резултатът от тази проверка е между 0 и 9**, то тогава нашият символ наистина е **число**.
* Ако символът е **оператор**, т.е. е **`+`**, **`-`**, **`*`** или **`/`**.

![](assets/chapter-9-2-images/02.X-expression-06.png)

Нека разгледаме действията, които трябва да извършим при съответните случаи, които дефинирахме:
* Ако нашият символ е **оператор**, то тогава единственото, което трябва да направим, е да **зададем нова стойност на променливата `expressionOperator`**.
*  Ако нашият символ е **цифра**, тогава трябва да **променим текущия резултат от израза в зависимост от текущия оператор**, т.е. ако **`expressionOperator`** е **`-`**, тогава трябва да **намалим резултата с цифровата репрезентация на текущия символ**. Можем да вземем цифровата репрезентация на текущия символ, чрез формулата, която използвахме при проверката на този случай (**`[ASCII кода на нашия символ] - [ASCII кода на символа `0`] = [цифрата, която репрезентира символа]`**).

![](assets/chapter-9-2-images/02.X-expression-07.png)

* Ако нашият символ е **`(`**, това индикира **началото на подизраз** (израз в скоби). По дефиниция **подизразът трябва да се калкулира преди да се модифицира резултата от целия израз** (действията в скобите се извършват първи). Това означава, че ще имаме локален резултат за подизраза ни и локален оператор.

![](assets/chapter-9-2-images/02.X-expression-08.png)

След това, за **пресмятане стойността на подизраза** използваме същите методи, които използвахме за пресмятане на главния израз - използваме **`while` цикъл**, за **да четем символи** (докато не срещнем символа **`)`**). В зависимост от това дали прочетения символ е цифра или оператор, модифицираме резултата на подизраза. Имплементацията на тези операции е аналогична на имплементацията за пресмятане на изрази, описана по-горе, затова смятаме, че читателят не би трябвало да има проблем с нея.

След като приключим калкулацията на резултата от подизраза ни, **модифицираме резултата на целия израз** в зависимост от стойността на **`expressionOperator`**.

![](assets/chapter-9-2-images/02.X-expression-09.png)

#### Форматиране на изхода

Единствения изход, който програмата трябва да принтира на конзолата, е **резултатът от решаването на израза, с точност два символа след десетичния знак**. Как можем да форматираме изхода по този начин? Отговора на този въпрос оставяме на читателя.

### Тестване в Judge системата

Тествайте решението си тук: [https://judge.softuni.bg/Contests/Practice/Index/664#1](https://judge.softuni.bg/Contests/Practice/Index/664#1).


## Задача: бикове и крави

Всички знаем играта „Бикове и крави“ ([http://en.wikipedia.org/wiki/Bulls_and_cows](http://en.wikipedia.org/wiki/Bulls_and_cows)). При дадено 4-цифрено **тайно число** и 4-цифрено **предполагаемо число**, използваме следните правила:
* Ако имаме цифра от предполагаемото число, която съвпада с цифра от тайното число и е на **същата позиция**, имаме ***бик***.
* Ако имаме цифра от предполагаемото число, която съвпада с цифра от тайното число, но е **на различна позиция**, имаме ***крава***.

| Тайно число         | 1 | 4 | 8 | 1 |Коментар|
|:-------------------:|:---:|:---:|:---:|:---:|:--------------------------:|
| Предполагаемо число | 8 | 8 | 1 | 1 | Бикове = 1<br>Крави = 2  |

| Тайно число         | 2 | 2 | 4 | 1 |Коментар|
|:-------------------:|:---:|:---:|:---:|:---:|:-------------------------:|
| Предполагаемо число | 9 | 9 | 2 | 4 | Бикове = 0<br>Крави = 2 |

При дадено тайно число и брой на бикове и крави, нашата задача е **да намерим всички възможни предполагаеми числа** в нарастващ ред.

Ако **не съществуват предполагаеми числа**, които да отговарят на зададените критерии на конзолата, трябва да се отпечата "**No**".

### Входни данни

Входните данни се четат от конзолата. Входът се състои от 3 реда:
* Първият ред съдържа **секретното число**.
* Вторият ред съдържа **броя бикове**.
* Третият ред съдържа **броя крави**.

Входните данни ще бъдат винаги валидни. Няма нужда да бъдат проверявани.

### Изходни данни

Изходните данни трябва да се принтират на конзолата.
Изходът трябва да се състои от **един единствен ред** – **всички предполагаеми числа**, разделени с единично празно място.
Aко **не съществуват предполагаеми числа**, които да отговарят на зададените критерии на конзолата, трябва **да се изпише “No”**.

### Ограничения

- Тайното число винаги ще се състои от **4 цифри в интервала** [**1..9**].
- Броят на **кравите и биковете** винаги ще е в интервала [**0..9**].
- Позволено време за изпълнение: **0.15 секунди**.
- Позволена памет: **16 MB**.

### Примерен вход и изход

| Вход           | Изход        |
|--------------|------------|
| 2228<br>2<br>1 | 1222 2122 2212 2232 2242 2252 2262 2272 2281 2283 2284 2285 2286 2287 2289 2292 2322 2422 2522 2622 2722 2821 2823 2824 2825 2826 2827 2829 2922 3222 4222 5222 6222 7222 8221 8223 8224 8225 8226 8227 8229 9222 |

| Вход           | Изход        |
|--------------|------------|
| 1234<br>3<br>0 | 1134 1214 1224 1231 1232 1233 1235 1236 1237 1238 1239 1244 1254 1264 1274 1284 1294 1334 1434 1534 1634 1734 1834 1934 2234 3234 4234 5234 6234 7234 8234 9234 |

| Вход           | Изход        |
|--------------|------------|
| 1234<br>3<br>1 | No           |

### Насоки и подсказки

Ще решим задачата на няколко стъпки:
 - Ще прочетем **входните данни**.
 - Ще генерираме всички възможни **четирицифрени комбинации** (кандидати за проверка).
 - За всяка генерирана комбинация ще изчислим **колко бика** и **колко крави** има в нея спрямо секретното число. При съвпадение с търсените бикове и крави, ще **отпечатаме комбинацията**.

#### Обработване на входа

За входа на нашата задача имаме 3 реда:
* **Секретното число**.
* **Броят** желани **бикове**.
* **Броят** желани **крави**.

Прочитането на тези входни данни е тривиално:

![](assets/chapter-9-2-images/03.Bulls-and-cows-03.png)

#### Алгоритъм за решаване на задачата

Преди да започнем писането на алгоритъма за решаване на нашия проблем, трябва да **декларираме флаг**, който да указва дали е намерено решение:

![](assets/chapter-9-2-images/03.Bulls-and-cows-04.png)

Ако след приключването на нашия алгоритъм, този флаг все още е **`false`**, тогава ще принтираме **`No`** на конзолата, както е указано в условието.

![](assets/chapter-9-2-images/03.Bulls-and-cows-05.png)

Нека започнем да размишляваме над нашия проблем. Това, което трябва да направим, е да **анализираме всички числа от `1111` до `9999`** без тези, които съдържат в себе си нули (напр. **`9011`**, **`3401`** и т.н. са невалидни). Какъв е най-лесният начин за **генериране** на всички тези **числа**? **С вложени цикли**. Тъй като имаме **4-цифрено число**, ще имаме **4 вложени цикъла**, като всеки един от тях ще генерира **отделна цифра от нашето число** за тестване.

![](assets/chapter-9-2-images/03.Bulls-and-cows-06.png)

Благодарение на тези цикли, **имаме достъп до всяка една цифра** на всички числа, които трябва да проверим. Следващата ни стъпка е да **разделим секретното число на цифри**. Това може да се постигне много лесно чрез **комбинация от целочислено и модулно деление**.

![](assets/chapter-9-2-images/03.Bulls-and-cows-07.png)

Остават ни последните две стъпки преди да започнем да анализираме колко крави и бикове има в дадено число. Съответно, първата е **декларацията на `counter` променливи** във вложените ни цикли, за да **броим кравите и биковете** за текущото число. Втората стъпка е да направим **копия на цифрите на текущото число**, което ще анализираме, за да предотвратим проблеми с работата на вложите цикли, ако правим промени по тях.

![](assets/chapter-9-2-images/03.Bulls-and-cows-08.png)

Вече сме готови да започнем анализирането на генерираните числа. Каква логика можем да използваме? Най-елементарният начин да проверим колко крави и бикове има в едно число е чрез **поредица от `if-else` проверки**. Да, не е най-оптималния начин, но с цел да не използваме знания извън пределите на тази книга, ще изберем този подход.

От какви проверки имаме нужда?

Проверката за бикове е елементарна - проверяваме дали **първата цифра** от генерираното число е еднаква със **същата цифра** от секретното число. Премахваме проверените цифри с цел да избегнем повторения на бикове и крави.

![](assets/chapter-9-2-images/03.Bulls-and-cows-09.png)

Повтаряме действието за втората, третата и четвърта цифра. 

Проверката за крави можем да направи по следния начин - първо проверяваме дали **първата цифра** от генерираното число **съвпада с втората**, **третата** или **четвъртата цифра** на секретното число. Примерна имплементация:

![](assets/chapter-9-2-images/03.Bulls-and-cows-10.png)

След това последователно проверяваме дали **втората цифра** от генерираното число **съвпада с първата**, **третата** или **четвъртата цифра** на секретното число, дали **третата цифра** от генерираното число съвпада с **първата**, **втората** или **четвъртата цифра** на секретното число и накрая проверяваме дали **четвъртата цифра** от генерираното число съвпада с **първата**, **втората** или **третата цифра** на секретното число.

#### Отпечатване на изхода

След като приключим всички проверки, ни остава единствено да **проверим дали биковете и кравите в текущото генерирано число съвпадат с желаните бикове и крави, прочетени от конзолата**. Ако това е така, принтираме текущото число на конзолата.

![](assets/chapter-9-2-images/03.Bulls-and-cows-11.png)

### Тестване в Judge системата

Тествайте решението си тук: [https://judge.softuni.bg/Contests/Practice/Index/664#2](https://judge.softuni.bg/Contests/Practice/Index/664#2).
