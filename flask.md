# Flask

### Введение

> **Flask** - микрофреймворк[^1] для создания сайтов.

Для дальнейшей работы нужно понять принцип взаимодействия
между **клиентом** (браузером) и **сервером** (нашим фреймворком).

Когда пользователь вводит желанный сайт, браузер отправляет
запрос на **DNS-сервер**[^2], чтобы получить **IP-адрес**[^3] нашего сайта.
Затем по полученному IP отправляется запрос, который возвращает
ответ в виде какого-то документа.

```text
User -[url]-> DNS -[ip]-> User -[ip]-> Server -[Document]-> User.
```

Наш фреймворк установлен на сервере, которому веб-сервер[^4] отдает
запрос на обработку. Между Python-программой и сервером находиться
прослойка в виде **WSGI-приложением** [_Web Server Gateway Interface_], 
предоставляющим удобный интерфейс для взаимодействия с сервером.

При поступлении нового запроса активизируется WSGI-приложение, 
выполняется определенный обработчик, который называется "**Представление**".
При нескольких запросах обработчики работают в многопоточном режиме.

**Установка** микрофреймворка происходит через пакетный менеджер в 
CLI командой: `pip install Flask`.

Создадим простое WSGI-приложение, которое по url "/" будет возвращать
заголовок "Some Text".

```python
from flask import Flask

app = Flask(__name__)


@app.route("/")
def index():
    return "<h1>Some Text</h1>"


if __name__ == "__main__":
    app.run(debug=True)
```

[^1]: Фреймворк - программная платформа (набор библиотек),
призванная облегчить разработку продукта путём предоставления
всего необходимого инструментария. Микрофреймворк - ограничен
по функциям, но он легковеснее и, как правило, хорошо защищён.

[^2]: DNS (Domain Name Server) - специализированный компьютер, который
хранит IP-адреса сайтов.

[^3]: IP (Internet Protocol) - уникальный числовой идентификатор устройства
в компьютерной сети.

[^4]: Веб-сервер - сервер, принимающий HTTP-запросы от клиентов.