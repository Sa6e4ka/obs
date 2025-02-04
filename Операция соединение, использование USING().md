
При описании соединения таблиц с помощью `**JOIN**` в некоторых случаях вместо **`ON`** и следующего за ним условия можно использовать оператор **`USING()`**.

`**USING**` позволяет указать набор столбцов, которые есть в обеих объединяемых таблицах. Если база данных хорошо спроектирована, а каждый внешний ключ имеет такое же имя, как и соответствующий первичный ключ (например, `**genre.genre_id = book.genre_id**`), тогда можно использовать предложение **`USING`** для реализации операции `**JOIN**`. 

При этом после **`SELECT`**, при использовании столбцов из `**USING()**`, необязательно указывать, из какой именно таблицы берется столбец.

**Пример**

Вывести название книг, фамилии и `**id**` их авторов.

_Запрос:_

Вариант с `**ON**`

```sql
SELECT title, name_author, author.author_id /* явно указать таблицу - обязательно */
FROM 
    author INNER JOIN book
    ON author.author_id = book.author_id;
```

Вариант с `**USING**`

```sql
SELECT title, name_author, author_id /* имя таблицы, из которой берется author_id, указывать не обязательно*/
FROM 
    author INNER JOIN book
    USING(author_id);
```

_Результат (одинаковый для обоих запросов):_

```sql
+-----------------------+------------------+-----------+
| title                 | name_author      | author_id |
+-----------------------+------------------+-----------+
| Мастер и Маргарита    | Булгаков М.А.    | 1         |
| Белая гвардия         | Булгаков М.А.    | 1         |
| Идиот                 | Достоевский Ф.М. | 2         |
| Братья Карамазовы     | Достоевский Ф.М. | 2         |
| Игрок                 | Достоевский Ф.М. | 2         |
| Стихотворения и поэмы | Есенин С.А.      | 3         |
| Черный человек        | Есенин С.А.      | 3         |
| Лирика                | Пастернак Б.Л.   | 4         |
+-----------------------+------------------+-----------+
```

Запись условия соединения с **`ON`** является более общим случаем, так как

- позволяет задавать соединение не только по одноименным полям;
- позволяет использовать произвольное условие на соединение таблиц, при этом в условие может включаться произвольное выражение, например, можно указать связь двух таблиц по двум и более столбцам.