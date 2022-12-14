## Поиск по Википедии. В консольной программе

### Задача:
Напишите программу, которая с консоли считывает поисковый запрос, и выводит результат поиска по Википедии. Задача разбивается на 4 этапа:

### Функционал программы
1. Считать запрос
2. Сделать запрос к серверу
3. Распарсить ответ
4. Вывести результат

Первый и четвертый пункт не сильно нуждаются в пояснении, остановимся на запросе к серверу.
<br><br>
Эту задачу тоже можно разбить на несколько этапов:
1. Генерация запроса
2. Запрос к серверу
3. Подготовка к обработке ответа
4. Обработка ответа

Рассмотрим это подробнее:

### Генерация запроса
API предоставляет возможность делать поисковые запросы, без ключей. Вот таким, примерно, образом:
```
https://ru.wikipedia.org/w/api.php?action=query&list=search&utf8=&format=json&srsearch="Java"
```
Вы можете открыть эту ссылку в браузере, и посмотреть на результат запроса.
Однако, чтобы запрос прошел удачно, следует убрать из ссылки недопустимые символы, то есть сделать [Percent-encoding](https://en.wikipedia.org/wiki/Percent-encoding "Percent-encoding"), он же URL Encoding.
Для этого в Java можно воспользоваться статическим методом encode в классе URLEncoder, вот так:
```
street = URLEncoder.encode(street, "UTF-8");  
```
Вот и всё, URL готов! Осталось теперь сделать запрос к серверу…
### Запрос к серверу
Для GET и POST запросов можно воспользоваться классом [HttpURLConnection](https://docs.oracle.com/javase/10/docs/api/java/net/HttpURLConnection.htmlHttpURLConnection "HttpURLConnection"). Это самое простое. Просто создать, открыть соединение и получить InputStream. Нам его даже не надо читать, за нас это сделает [Gson](https://github.com/google/gson "Gson").
Ещё можно использовать [retrofit](https://square.github.io/retrofit/ "retrofit"), или что-то подобное.
### Подготовка к обработке ответа
Сервер возвращает данные в формате [JSON](https://en.wikipedia.org/wiki/JSONJSON "JSON").
Но нам его не надо парсить вручную, для этого есть библиотека [Gson](https://github.com/google/gson "Gson") от Google.

Примеры есть тут:

https://github.com/google/gson <br>
https://habrahabr.ru/company/naumen/blog/228279/

Если остаётся время, можно написать получение статьи, выбранной при поиске и так далее.
