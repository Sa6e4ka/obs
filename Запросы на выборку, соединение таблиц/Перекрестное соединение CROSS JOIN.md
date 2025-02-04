Оператор перекрёстного соединения, или декартова произведения `CROSS JOIN` (в запросе вместо ключевых слов можно поставить запятую между таблицами) соединяет две таблицы. Порядок таблиц для оператора неважен, поскольку оператор является симметричным. Его структура:

```sql
SELECT
 ...
FROM
    таблица_1 CROSS JOIN  таблица_2
...
```

или

```sql
SELECT
 ...
FROM
    таблица_1, таблица_2
...
```

Результат запроса формируется так: каждая строка одной таблицы соединяется с каждой строкой другой таблицы, формируя  в результате все возможные сочетания строк двух таблиц.

Например, запрос:

```sql
SELECT name_author, name_genre
FROM 
    author, genre;
```

каждому автору из таблицы `**author**` поставит в соответствие все возможные жанры из таблицы `**genre**`