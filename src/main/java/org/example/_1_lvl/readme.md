SQL - Structured query language

## 3 grade

1) Что такое DDL (Data Definition Language)?
   DDL (Data Definition Language, язык определения данных) — это часть языка SQL, используемая для определения и
   управления структурами базы данных. Команды DDL позволяют создавать, изменять и удалять базы данных и их объекты,
   такие как таблицы, индексы, представления и т. д.

CREATE, DROP, ALTER, RENAME, TRUNCATE

2) Что такое DML (Data Manipulation Language)? — это часть языка SQL, используемая для выполнения операций с данными в
   базе данных

INSERT, DELETE, UPDATE, SELECT

3) Что такое первичный ключ (Primary Key)? Уникальность, Не допускает NULL значений и Один на таблицу, составной
   первичный ключ.

```
CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT
);
```

```
CREATE TABLE orders (
    order_id INT,
    product_id INT,
    quantity INT,
    PRIMARY KEY (order_id, product_id)
);
```

5) Что такое внешний ключ (Foreign Key)? Связь между таблицами, Целостность данных, Может содержать NULL значения и
   Каскадные действия

```
CREATE TABLE enrollments (
    enrollment_id SERIAL PRIMARY KEY,
    student_id INT,
    course_id INT,
    FOREIGN KEY (student_id) REFERENCES students(student_id)
);
```

6) Как настроить автогенерацию первичного ключа?

SERIAL, BIGSERIAL

```
CREATE SEQUENCE student_id_seq;

CREATE TABLE students (
    student_id INT PRIMARY KEY DEFAULT nextval('student_id_seq'),
    name VARCHAR(100),
    age INT
);
```

```
CREATE EXTENSION IF NOT EXISTS "pgcrypto";

CREATE TABLE students (
    student_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(100),
    age INT
);
```

7) Какие существуют ограничения (constraints) и как они используются?

PRIMARY KEY, UNIQUE, FOREIGN KEY, CHECK и NOT NULL

8) Как обновить ограничения столбца (constraints) в SQL?

```
ALTER TABLE employees
DROP CONSTRAINT salary_positive;

ALTER TABLE employees
ADD CONSTRAINT salary_non_negative CHECK (salary >= 0);
```

9) Как создать и удалить базу данных в PostgreSQL?

```
CREATE DATABASE my_database;

DROP DATABASE IF EXISTS my_database;
```

10) Как создать и удалить схему в PostgreSQL?

```
CREATE SCHEMA my_schema;

DROP SCHEMA IF EXISTS my_schema CASCADE;
```

11) Как создать и удалить таблицу в PostgreSQL?

```
CREATE TABLE employees (
    employee_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    salary DECIMAL(10, 2)
);

DROP TABLE IF EXISTS employees;
```

12) Как добавить новый столбец в таблицу в SQL?

```
ALTER TABLE employees
ADD email VARCHAR(100);
```

13) Как вставить данные в таблицу в PostgreSQL?

```
INSERT INTO employees
VALUES (1, 'John', 'Doe', 50000.00);
```

14) Как удалить данные из таблицы?

```
DELETE FROM employees
WHERE employee_id = 1;
```

15) Как обновить данные в таблице?

```
UPDATE employees
SET salary = 55000.00
WHERE employee_id = 1;
```

16) Как получать данные при обновлении и удалении записей?

RETURNING

17) Как извлечь нужные данные из таблицы?

```
SELECT department_id, SUM(salary) AS total_salary
FROM employees
GROUP BY department_id;
```

18) Как изменить имена столбцов в результирующей выборке с помощью алиасов (aliases)?

```
SELECT first_name AS "Имя", last_name AS "Фамилия"
FROM employees;
```

19) Как получить уникальные значения из таблицы?

```
SELECT DISTINCT first_name, last_name
FROM employees;
```

20) Как ограничить количество строк в выборке?

```
SELECT * 
FROM employees
LIMIT 10;
```

21) Как пропускать строки в выборке?

```
SELECT * 
FROM employees
ORDER BY employee_id
LIMIT 5 OFFSET 5;
```

22) Как сортировать данные при выборке?

```
SELECT * 
FROM employees
ORDER BY last_name ASC, first_name ASC;
```

23) Как фильтровать данные в выборке?

```
SELECT * 
FROM employees
WHERE department_id IN (1, 2, 3);
```

24) Что такое агрегирующие функции и как они используются?

Агрегирующие функции в SQL - это функции, которые применяются к группе строк и возвращают одно значение для всей группы.
Эти функции используются для выполнения вычислений на множестве строк и возвращения одного значения, например, суммы,
среднего значения, минимального или максимального значения и т. д.

Вот некоторые из наиболее распространенных агрегирующих функций:

COUNT: Возвращает количество строк в группе.
SUM: Возвращает сумму значений в группе.
AVG: Возвращает среднее значение значений в группе.
MIN: Возвращает минимальное значение в группе.
MAX: Возвращает максимальное значение в группе.

```
SELECT department_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id;
```

25) Что такое встроенные функции в PostgreSQL?

В PostgreSQL встроенные функции представляют собой функции, которые встроены непосредственно в систему управления базами
данных (СУБД) и доступны для использования в SQL-запросах и хранимых процедурах. Эти функции включают в себя широкий
спектр операций, начиная от строковых и числовых функций и заканчивая функциями для работы с датами, геометрическими
данными и многими другими.

Вот некоторые из типов встроенных функций в PostgreSQL:

Строковые функции: Например, функции для работы со строками, такие как UPPER, LOWER, SUBSTRING, CONCAT, LENGTH и т. д.

Числовые функции: Включают арифметические функции (+, -, *, /), функции округления (ROUND, CEIL, FLOOR), функции
модуля (ABS) и т. д.

Функции для работы с датами и временем: Например, функции CURRENT_DATE, CURRENT_TIME, DATE_TRUNC, EXTRACT и многие
другие.

Геометрические функции: Включают функции для работы с геометрическими данными, такие как ST_AREA, ST_DISTANCE,
ST_INTERSECTS и т. д.

Логические функции: Например, функции для работы с логическими значениями, такие как AND, OR, NOT, TRUE, FALSE.

Массивные функции: Функции для работы с массивами, такие как ARRAY_LENGTH, ARRAY_APPEND, ARRAY_REMOVE и т. д.

JSON-функции: Функции для работы с JSON-данными, такие как JSON_BUILD_OBJECT, JSONB_SET, JSON_ARRAY_ELEMENTS и другие.

26) Как объединять запросы выборки?

В PostgreSQL для объединения результатов нескольких запросов выборки вы можете использовать операторы объединения UNION,
UNION ALL, INTERSECT и EXCEPT. Вот как они работают:

27) Как объядинять запросы исключив повтораяющися значения?

28) Что такое подзапросы и как они работают?

Подзапросы (также известные как вложенные запросы или вложенные подзапросы) в SQL - это запросы, вложенные внутри других
SQL-запросов. Они позволяют вам выполнить один запрос (внутренний запрос) и использовать его результаты в другом
запросе (внешний запрос).

29) Какие существуют примеры использования подзапросов?

```
SELECT column1, (SELECT MAX(column2) FROM table2) AS max_column2
FROM table1;
```

```
SELECT column1, column2
FROM table1
WHERE column3 = (SELECT MAX(column3) FROM table1);
```

```
SELECT column1, column2
FROM (SELECT column1, column2 FROM table1 WHERE condition) AS subquery;
```

```
DELETE FROM table1
WHERE column1 IN (SELECT column1 FROM table2 WHERE condition);
```

```
INSERT INTO table1 (column1, column2)
SELECT column1, column2
FROM table2
WHERE condition;
```

30) Какие типы связей существуют между таблицами в базе данных?

Один к одному (One-to-One)
Один ко многим (One-to-Many)
Многие к одному (Many-to-One)
Многие ко многим (Many-to-Many)

31) Что такое соединение (JOIN) таблиц?

- это операция, которая объединяет строки из двух или более таблиц в один результат на основе совпадения значений в
  указанных столбцах.

INNER JOIN, LEFT JOIN (или LEFT OUTER JOIN), RIGHT JOIN (или RIGHT OUTER JOIN), FULL JOIN (или FULL OUTER JOIN)

32) Что такое INNER JOIN?

Возвращает строки, которые имеют совпадающие значения в обеих таблицах.

34) Что такое CROSS JOIN?

каждая строка из первой таблицы будет объединена со всеми строками из второй таблицы.

35) Что такое LEFT JOIN?

Возвращает все строки из левой таблицы (первой указанной в запросе), а также совпадающие строки из правой таблицы

36) Что такое RIGHT JOIN?

Возвращает все строки из правой таблицы (второй указанной в запросе), а также совпадающие строки из левой таблицы.

37) Что такое FULL JOIN?

Возвращает все строки из обеих таблиц.

38) Как группировать данные в SQL?

```
SELECT department_id, job_title, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id, job_title;
```

38) Как фильтровать сгруппированные данные (условие HAVING)?

```
SELECT department_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 50000;
```

## 4 grade

1) Что такое оконные функции в SQL? это функции, которые выполняются над набором строк, связанных с текущей строкой, и
   возвращают значение для каждой строки в результирующем наборе.

Множество оконных функций можно разделять на 3 класса:

* Агрегирующие (Aggregate)
* Ранжирующие (Ranking)
* Функции смещения (Value)

2) Какие оконные функции вы знаете?

![img_19.png](assets/img_19.png)

В ранжирующих функция под ключевым словом OVER обязательным идет указание условия ORDER BY, по которому будет
происходить сортировка ранжирования.

* ROW_NUMBER() - функция вычисляет последовательность ранг (порядковый номер) строк внутри партиции, НЕЗАВИСИМО от того,
  есть ли в строках повторяющиеся значения или нет.
* RANK() - функция вычисляет ранг каждой строки внутри партиции. Если есть повторяющиеся значения, функция возвращает
  одинаковый ранг для таких строчек, пропуская при этом следующий числовой ранг.
* DENSE_RANK() - то же самое что и RANK, только в случае одинаковых значений DENSE_RANK не пропускает следующий числовой
  ранг, а идет последовательно.
* Ntile - 1, 1, 2, 2
* cuma_dist - 8% ... 100%
* percent_rank - 0% ... 100%

Это функции, которые позволяют перемещаясь по выделенной партиции таблицы обращаться к предыдущему значению строки или
крайним значениям строк в партиции.

* LAG() - функция, возвращающая предыдущее значение столбца по порядку сортировки.
* LEAD() - функция, возвращающая следующее значение столбца по порядку сортировки.

3) Что такое представление (VIEW) в базе данных?

это виртуальная таблица, основанная на результатах запроса SQL.
Представления не содержат данных самостоятельно; они представляют собой динамические наборы данных, которые
генерируются в реальном времени на основе базовых таблиц.

```
CREATE VIEW sales_department AS
SELECT employee_id, employee_name, salary
FROM employees
WHERE department_id = 10;
```

4) Что такое материализованное представление (MATERIALIZED VIEW)?

Материализованное представление (MATERIALIZED VIEW) — это объект базы данных, который хранит результат запроса, в
отличие от обычного представления (VIEW), которое является виртуальным и динамически генерирует данные при каждом
запросе. Материализованные представления используются для улучшения производительности запросов, так как они содержат
предварительно вычисленные результаты.

```
CREATE MATERIALIZED VIEW mv_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

5) Как обновить материализованное представление в базе данных?

```
REFRESH MATERIALIZED VIEW mv_name;
```

6) Что такое нормализация базы данных?

Нормализация - это метод проектирование базы данных, который позволяет привести базы данных к
минимальной избыточности.

Избыточность - это когда данные одни и те же данные хранятся в базе данных в нескольких таблицах.

7) Сколько существует нормальных форм и каковы их названия?

![img.png](assets/img.png)

8) Что такое первая нормальная форма (1NF)?

![img_1.png](assets/img_1.png)

9) Что такое вторая нормальная форма (2NF)?

![img.png](assets/img_2.png)

10) Что такое третья нормальная форма (3NF)?

![img.png](assets/img_3.png)

11) Что такое множество?

В SQL множество представляет собой набор данных, обычно таблицу, в которой хранятся строки данных.

12) Как найти пересечение двух множеств?

INTERSECT

13) Как исключить элементы одного множества из другого?

EXCEPT

14) Что такое индексы в базе данных?

это специальные структуры данных, которые используются для повышения скорости выполнения запросов.

Быстрый поиск, Упорядочивание данных, Уменьшение производительности операций записи, Потребление памяти
Первичный ключ (Primary Key), Уникальный индекс (Unique Index), Обычный индекс (Non-Unique Index), Составной индекс (
Composite Index), Кластеризованный индекс (Clustered Index), Некластеризованный индекс (Non-Clustered Index)

15) Что такое B-Tree индекс?

B-Tree (сокращение от "Balanced Tree") индекс — это тип индекса, который широко используется в системах управления
базами данных (СУБД) для повышения производительности запросов. B-Tree индексы позволяют эффективно искать, вставлять,
удалять и обновлять записи в базе данных.

16) Как создать индекс в базе данных?

```
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

```
CREATE UNIQUE INDEX idx_unique_name ON employees(name);
```

```
CREATE INDEX idx_name ON employees(name);
```

```
CREATE INDEX idx_name_department ON employees(name, department_id);
```

```
CREATE CLUSTERED INDEX idx_id ON employees(id);
```

```
CREATE CLUSTERED INDEX idx_id ON employees(id);
```

```
CREATE NONCLUSTERED INDEX idx_name ON employees(name);
```

17) Какие особенности есть у составных индексов?

Они используются для улучшения производительности запросов, которые фильтруют или сортируют данные по нескольким
критериям одновременно.

Многостолбцовая структура: Составной индекс включает в себя два и более столбца, что позволяет ускорять запросы,
использующие несколько условий фильтрации или сортировки.
Лексикографический порядок: Составной индекс упорядочивает данные сначала по первому столбцу, затем по второму, и так
далее.
Использование начального набора столбцов: Запросы, которые фильтруются по первому столбцу (или первому и второму, и так
далее) в составе индекса, могут использовать этот индекс. Однако запросы, которые не включают в себя начальный столбец
индекса, не будут использовать составной индекс эффективно.
Сортировка: Составные индексы могут ускорить сортировку данных, если порядок сортировки соответствует порядку столбцов в
индексе.
Диапазонные запросы: Составные индексы поддерживают диапазонные запросы, если они используют начальный набор столбцов
индекса.

18) Как посмотреть структуру таблицы?

`\d table_name`

```
SELECT column_name, data_type, character_maximum_length
FROM information_schema.columns
WHERE table_name = 'table_name';
```

19) Как переключиться на другую базу данных?

`\c test;`

20) Что такое транзакция в базе данных?

![img.png](assets/transaction/img.png)

21) Какие свойства имеет транзакция?

![img_1.png](assets/transaction/img_1.png)

22) Что такое атомарность транзакции?

![img_2.png](assets/transaction/img_2.png)

23) Что такое согласованность транзакции?

![img_3.png](assets/transaction/img_3.png)

24) Что такое изолированность транзакции?

![img_4.png](assets/transaction/img_4.png)

25) Что такое долговечность транзакции?

![img_5.png](assets/transaction/img_5.png)

26) Какие существуют уровни изоляции транзакций?

![img_6.png](assets/transaction/img_6.png)
![img_12.png](assets/transaction/img_12.png)
![img_13.png](assets/transaction/img_13.png)

27) Что такое потерянное обновление?

![img_7.png](assets/transaction/img_7.png)
![img_15.png](assets/transaction/img_15.png)

28) Что такое грязное чтение?

![img_8.png](assets/transaction/img_8.png)
![img_14.png](assets/transaction/img_14.png)

29) Что такое неповторяющееся чтение?

![img_9.png](assets/transaction/img_9.png)
![img_16.png](assets/transaction/img_16.png)

![img_10.png](assets/transaction/img_10.png)
![img_17.png](assets/transaction/img_17.png)

30) Что такое фантомное чтение?

![img_11.png](assets/transaction/img_11.png)
![img_18.png](assets/transaction/img_18.png)

31) Что такое чтение незафиксированных данных (Read uncommitted)?

32) Что такое чтение зафиксированных данных (Read committed)?

33) Что такое повторяемое чтение (Repeatable read)?

34) Что такое сериализуемость (Serializable)?

35) begin transaction isolation level repeatable read;

`begin transaction isolation level repeatable read;`

36) Что такое теорема CAP?

![img.png](assets/cap/img.png)

## 5 grade

1) Что такое план выполнения запроса?

План выполнения запроса — это набор шагов, которые СУБД выполняет для обработки SQL-запроса. План показывает, какие
операции будут выполнены и в каком порядке, чтобы получить требуемый результат.

2) Что такое оптимизатор запросов на основе стоимости (cost-based optimizer)?

Оптимизатор запросов на основе стоимости (CBO) — это компонент СУБД, который выбирает наиболее эффективный план
выполнения запроса, оценивая различные возможные планы на основе их предполагаемой стоимости выполнения.

old - rule-based

![img.png](assets/cost_based_optimizer/img.png)
![img_1.png](assets/cost_based_optimizer/img_1.png)

3) Что такое стоимость (cost) в контексте оптимизации запросов?

Стоимость (cost) — это числовая оценка ресурсов, необходимых для выполнения запроса (например, время процессора,
количество операций ввода-вывода), которую оптимизатор использует для выбора наилучшего плана выполнения.

4) Что такое page_cost?

Page_cost — это параметр, который определяет стоимость чтения одной страницы данных из диска в память. В PostgreSQL этот
параметр обычно называют seq_page_cost или random_page_cost.

5) Что такое cpu_cost?

CPU_cost — это параметр, который определяет стоимость выполнения операций процессора, таких как вычисления и сравнения,
в процессе выполнения запроса.

6) Как обновить статистику по таблице в базе данных?

`ANALYZE table_name;`

7) Что делает функция byte_length?

нет такой функции, bit_length возвращает количество битов которые занимает место в базе

8) Что такое index only scan?

Возвращает данные индекса

9) Что такое index scan?

Также должен сходить в бд где лежат данные по страницам

10) Что такое bitmap scan?

![img_2.png](assets/cost_based_optimizer/img_2.png)

![img_3.png](assets/cost_based_optimizer/img_3.png)

-- dop info

nested loop - используется если данных мало
hash join - использует hashtable для 2 таблицы в join
merge join - быстрее hash join но чтобы его использовать ключи должны быть отсортированы

## 6 grade

1) Что хранит в себе класс pg_catalog.pg_class?

Класс pg_catalog.pg_class в PostgreSQL хранит информацию обо всех таблицах, индексах, представлениях и других объектах,
которые имеют строки. Это системная таблица, содержащая метаданные, такие как имя объекта, его тип, владелец и другая
важная информация.

2) Что такое репликация базы данных?

Репликация базы данных — это процесс копирования и поддержания синхронизации данных между несколькими серверами баз
данных. Это обеспечивает высокую доступность, отказоустойчивость и распределение нагрузки.

3) Что такое сегментация (sharding) базы данных?

Сегментация (sharding) — это метод распределения данных по нескольким базам данных или серверам, называемым шардов.
Каждый шард хранит подмножество данных, что позволяет масштабировать систему горизонтально, улучшая производительность и
управляемость больших объемов данных.

4) Что такое распределенная база данных?

Распределённая база данных — это база данных, данные которой хранятся на нескольких узлах (серверах) и управляются как
единая система. Она обеспечивает масштабируемость, отказоустойчивость и возможность параллельной обработки запросов.
