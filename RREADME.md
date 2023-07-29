Flask tutor

Элементарное приложение в `Flask`.

```python
# app.py
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "<p>Hello, World!</p>"
```
1. Мы импортируем класс `Flask`.
2. Создаем инстанс `app` от класса `Flask`
3. Затем мы используем декоратор `rout()`, чтобы сообщить, какой URL должен вызвать нашу функцию.
4. Функция возвращает нам то, что мы можем увидеть в браузере.

*Примечение:* При создании инстанца `Flask` в своем параметре должен принять название модуля, это необходимо, чтобы Flask знал где искать ресурсы, такие как шаблоны и статические файлы.

Запуск приложения:
```shell
flask --app <app_name> run
```
*Примечание:* Если файл имеет название `app.py` или `wsgi.py`, то мы можем просто ввести команду:
```shell
flask run
```

Вы можете сделать сервер общедоступным:
```shell
flask run --host=0.0.0.0
```

Чтобы запустить в режиме отладки:
```shell
flask --app <app_name> run debug
```

При возврате HTML, все значения должны быть экранированы:
```python
from markupsafe import escape

@app.route('/<name>')
def index(name):
    return f'hello, {escape(name)}'
```

Типы преобразователей:
<table class="docutils align-default">
<tbody>
<tr class="row-odd"><td><p><code class="docutils literal notranslate"><span class="pre">string</span></code></p></td>
<td><p>(по умолчанию) принимает любой текст без косой черты</p></td>
</tr>
<tr class="row-even"><td><p><code class="docutils literal notranslate"><span class="pre">int</span></code></p></td>
<td><p>принимает целые положительные числа</p></td>
</tr>
<tr class="row-odd"><td><p><code class="docutils literal notranslate"><span class="pre">float</span></code></p></td>
<td><p>принимает положительные значения с плавающей точкой</p></td>
</tr>
<tr class="row-even"><td><p><code class="docutils literal notranslate"><span class="pre">path</span></code></p></td>
<td><p>как <code class="docutils literal notranslate"><span class="pre">string</span></code>, но также принимает косые черты</p></td>
</tr>
<tr class="row-odd"><td><p><code class="docutils literal notranslate"><span class="pre">uuid</span></code></p></td>
<td><p>принимает строки UUID</p></td>
</tr>
</tbody>
</table>

Методы HTTP:
```python
from flask import request

@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        return do_the_login()
    return show_the_login_form()
```
В примере выше все методы для маршрута находятся в одной функции, но мы можем разбить:
```python
@app.get('/login')
def login_get():
    return show_the_login_form()

@app.post('/login')
def login_post():
    return do_the_login()
```
