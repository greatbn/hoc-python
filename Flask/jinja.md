- biến có thể được modified với filters, được thêm vào sau tên biến với kí tự '|'. ví dụ template sau show tên biến capitalize
	Hello {{ name|capitalize }}
- Danh sách các filter thường sử dụng với jinja2

+ safe : render value without apply escaping
+ capitalize : convert first character of value to uppercase và the rest to lowercase
+ lower : convert the value to lowercase characters
+ upper : convert the value to uppercase characters
+ title : capitalize mỗi word in the value
+ trim : remove leading and trailing whitespace from the value
+ striptags : remove any HTML tags from value before rendering

- Cấu trúc điều khiển

{% if user %}
Hello {{ user }}
{% else %}
Hello World!
{% endif %}

- Cấu trúc lặp.

{% for comment in comments %}
<li> {{ comment }}</li>
{% endfor %}

- jinja2 cũng hỗ trợ macro tương tự như python

Ví dụ

{% macro render_comment(comment) %}
<li> {{ comment }}</li>
{% endmacro %}

<ul>
{% for comment in comments %}
{{ render_comment(comment) }}
{% endfor %}
</ul>

- Để macro được sử dụng lại nhiều lần. ta có thể lưu nó vào 1 file sau đó import từ template cần chúng

{% import 'macros.html' as macros %}
<ul>
{% for comment in comments %}
{{ marcos.render_comment(comment) }}
{% endfor %}
</ul>

- Một phần code của template sử dụng nhiều lần cũng được lưu vào file và sau đó include từ các template cần nó 
{% include 'common.html' %} 

- Vẫn còn một cách để sử dụng lại là thông qua template kế thừa 
Ví dụ ta có base.html

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

Và file show.html extends từ file base.html

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

- flask-bootstrap

