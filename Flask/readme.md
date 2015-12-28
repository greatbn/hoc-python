##Flask

- Tự học flask. 
- Ghi chú những kiến thức căn bản


###Routing
- Mỗi một website sẽ có có đường dẫn. ta cần chỉ tới đường dẫn đó làm những công việc gì. Ở flask ta dùng app.route để dịnh nghĩa
- Mỗi function theo sau một route được gọi là view function

```
@app.route("/")
def index():
	return "Index Page"
@app.route("/hello")
def hello():
	return "Helo Page"
```

###Debug mode
- Khi enable debug mode ta có thể đang chạy code và sửa code sẽ được áp dụng mà không cần chạy lại.
- Để bật debug mode 

```
app.debug= True

```

hoặc 

```
app.run(debug = True)
```

###Variable

- Để thêm biến vào URL ta phải đặt tên biến vào cặp dấu < >
Ví dụ <username>

- Lựa chọn một converter có thể được sử dụng bởi khai báo 1 rule với <converter: variable_name>
```
@app.route("/user/<username>")
def show_user_profile(username):
	return 'User %s' %username
@app.route("/post/<int:post_id>")
def show_post(post_id):
	return "Post %d" %post_id
```
- Các kiểu converter
	- int
	- float
	- path

###HTTP Method

- Khai báo các http method tại route()
```
@app.route("/login",method=["GET","POST"])
def login():
	if request.method=="POST":
		do_the_login()
	else:
		show_the_profile()
```

###Rendering Template

- Để render một template bạn có thể sử dụng phương thức render_template(). Tất cả bạn phải làm là cung cấp tên của template và các biến để pass tới template engine. Các ví dụ.

```
from flask import Flask
from flask import render_template

app=Flask(__name__)
@app.route("/hello")
@app.route("/hello/<name>")
def hello(name=None):
	return render_template("hello.html",name=name)

```

- Flask sẽ tìm kiếm những template trong folder templates. Ví dụ nếu ứng dụng của bạn là một module nó sẽ ở bên cạnh module đó. còn nếu ứng dụng là một package thì nó sẽ nằm trong package đó.

TH1:  một module
```
/app.py
/templates
   /hello.html
```
TH2: một package
```
/app
   /__init__.py
   /templates
       /hello.py
```

- Ví dụ về một template
hello.html
```
<html>
<titel> Hello Flask </title>
{% if name %}
	<h1> Hello {{ name }}</h1>
{% elif %}
	<h1> Hello World </h1>
{% endif %}
```

### app and request context 
- current_app : ứng dụng thể hiện cho ứng dụng đang active
- g : một object được ứng dụng sử dụng cho việc lưu trữ tạm trong quá trình handling một request. biến này được reset sau mỗi request
- request: request object, đóng gói nội dung của http request gửi bởi client
- session: user sesion, là một dict mà ứng dụng có thể sử dụng để lưu trữ giá trị mà để nhớ giữa các request

### Custom error pages
- Khi truy cập vào không đúng đường dẫn tại browser bạn có thể bị lỗi 404. Trang hiển thị quá phức tạp và ko có tính tương tác. Flask cho phép một ứng dụng đinh nghĩa một error page. có thể dựa trên template. 

- Ví dụ custom error page 404 và 500

```

@app.errorhandler(404):
def page_not_found(e):
	return render_template("404.html") , 404
@app.errorhandler(500):
def internal_server_error(e):
	return render_template("500.html"),500

```


###Accessing request data

```
app.config.from_object(__name__)
app.config.from_envvar('FLASKR_SETTING',silent = True)
```
###Request Database connection

Flask cho phép chúng ta làm điều này với 
before_request() , after_request() và teardown_request()

```
@app.before_request
def before_request():
	g.db = connect_db()
@app.teardown_request
def teardown_request(exception):
	db = getattr(g,'db',None)
	if db is not None:
		db.close()
```


- Function before_request() được gọi trước một request không có tham số nào truyền vào. Function after_request() được gọi sau một request và có một response mà sẽ được gửi tới client. Chúng phải trả vè response object hoặc một cái khác. Tuy nhiên chúng không đảm bảo được thực thi khi có một ngoại lệ, và đó là nơi mà function teardown_request() đến. CHúng được gọi sau khi response được xây dựng. Chúng không được cho phép để sửa request và chúng trả về giá trị bị bỏ qua. Nếu một ngoại lệ xảy ra khi một request được xử lý, nó được pass tới mỗi function mặt khác None sẽ được pass. 

Chúng ta lưu kết nối database hiện thời trong object đặc biệt là 'g' nó đc Flask cung cấp cho chúng ta. Object này lưu trữ thông tin chỉ một request và sẵn có từ bên trong mỗi function. Không bao giờ lưu trữ những thứ như vậy trên các đối tượng khác vì điều này sẽ không làm việc với môi trường thread.

	
