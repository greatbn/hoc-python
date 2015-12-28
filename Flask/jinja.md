##Jinja2

### variable
- biến có thể được modified với filters, được thêm vào sau tên biến với kí tự '|'. ví dụ template sau show tên biến capitalize
```
Hello {{ name|capitalize }}
```
- Danh sách các filter thường sử dụng với jinja2

	+ safe : render value without apply escaping
	+ capitalize : convert first character of value to uppercase và the rest to lowercase
	+ lower : convert the value to lowercase characters
	+ upper : convert the value to uppercase characters
	+ title : capitalize mỗi word in the value
	+ trim : remove leading and trailing whitespace from the value
	+ striptags : remove any HTML tags from value before rendering

###Cấu trúc điều khiển

```
{% if user %}
Hello {{ user }}
{% else %}
Hello World!
{% endif %}
```
###Cấu trúc lặp.

```
{% for comment in comments %}
<li> {{ comment }}</li>
{% endfor %}
```

###macro
- jinja2 cũng hỗ trợ macro tương tự như python

Ví dụ

```
{% macro render_comment(comment) %}
<li> {{ comment }}</li>
{% endmacro %}

<ul>
{% for comment in comments %}
{{ render_comment(comment) }}
{% endfor %}
</ul>
```
- Để macro được sử dụng lại nhiều lần. ta có thể lưu nó vào 1 file sau đó import từ template cần chúng

```
{% import 'macros.html' as macros %}
<ul>
{% for comment in comments %}
{{ marcos.render_comment(comment) }}
{% endfor %}
</ul>
```

###Template 

- Một phần code của template sử dụng nhiều lần cũng được lưu vào file và sau đó include từ các template cần nó 

```
{% include 'common.html' %} 
```


- Vẫn còn một cách để sử dụng lại là thông qua template kế thừa 
Ví dụ ta có base.html

```
<html>
<head>
{% block head %}
<title>{% block title %}{% endblock %} </title>
{% endblock %}
</head>
<body>
{% block body %}
{% endblock %}
</body>
</html>

```

Và file show.html extends từ file base.html

```
{% extends "base.html" %}
{% block title %} hello {% endblock%}
{% block head %}
{{ super() }}
<style>
</style>
{% endblock %}
{% block body %}
<h1> hello world </h1>
{% endblock %}

```
###flask-bootstrap

- Bootstrap là một extension cho flask. Để dễ dàng tạo một giao diện đẹp kết hợp với jinja2
- Cài đặt `pip install flask-bootstrap`
- Để sử dụng bootstrap với flask ta thực hiện import bootstrap

```
from flask.ext.bootstrap import Bootstrap
from flask import Flask

app = Flask(__name__)

Bootstrap(app)


```

-Từ đây các file template có thể kế thừa base của bootstrap bằng cách

```
{% extends "bootstrap/base.html" %}
```

- Ví dụ về cách sử dụng bootstrap
- ứng dụng đơn giản hiển thị user-agent của trình duyệt
- Thư mục

```
--user-agent/
------------app.py
------------templates/
---------------------base.html
---------------------index.html

```

####Code

- app.py
```
from flask import Flask,request,make_response,redirect,render_template,url_for
from flask.ext.bootstrap import Bootstrap

app = Flask(__name__)
Bootstrap(app)
@app.route("/")
def index():
	user_agent= request.headers.get('User-Agent')
	return render_template("index.html",user_agent = user_agent)
if __name__ == '__main__':
	app.run(debug=True)

```

- base.html
```

{% extends "bootstrap/base.html" %}
{% block title %} Hello Flask {% endblock %}
{% block navbar %}
<div class="navbar navbar-inverse" role="navigation">
<div class="container">
<div class="navbar-header">
<button type="button" class="navbar-toggle"
data-toggle="collapse" data-target=".navbar-collapse">
<span class="sr-only">Toggle navigation</span>
<span class="icon-bar"></span>
<span class="icon-bar"></span>
<span class="icon-bar"></span>
</button>
<a class="navbar-brand" href="/">Flasky</a>
</div>
<div class="navbar-collapse collapse">
<ul class="nav navbar-nav">
<li><a href="/">Home</a></li>
</ul>
</div>
</div>
</div>
{% endblock %}
{% block content %}
<div class="container">
{% block page_content %}{% endblock %}
</div>
{% endblock %}

```

- index.html

```
{% extends "base.html" %}
{% block title %} Hello {% endblock %}
{% block page_content %}
<h1> Hello </h1>
<h4> Your browser is {{ user_agent }}</h4>
{% endblock %}

```

- Chạy ứng dụng mở trình duyệt tại địa chỉ  http://localhost:5000

<img src="http://i.imgur.com/q2ZQ0IJ.png">
