###Regular Expression

##các kí tự đặc biệt

- '.' trong chế độ mặc định , kí tự này match với tất cả các kí tự ngoại trừ newline. nếu cờ DOTALL được set. kí tự này sẽ match tất cả các kí tự bao gồm 1 newline

- '^' : match với sự bắt đầu của chuỗi. và trong mode MULTILINE cũng match lập tức sau mỗi newline

- '$' : match với kết thúc của string hoặc chỉ trước dòng mới của 1 string. trong mode MULTILINE cũng match trước 1 dòng. Ví dụ: 'foo' match với 'foobar' trong khi 'foo$' chỉ match với 'foo'. Ví dụ 2: tìm kiếm 'foo.$' trong 'foo1\nfoo2\n' bình thường match với 'foo2' nhưng trong chế độ MULTILINE match với 'foo1'. Tìm kiếm '$' trong 'foo\n' sẽ tìm thấy 2 empty match 1 là trước 1 newline và 1 cuối của 1 string

- '*': ví dụ 'ab*' sẽ match với 'a','ab','a'. theo sau bởi số các kí tự 'b'

- '+': ví dụ 'ab+' sẽ mới với 'a' theo sau bởi số các kí tự b khác 0. -> ko match với 'a'. Sẽ match với 'ab' 'abb'

- '?': gây ra kết quả match với cả số lần lặp 0 và 1. Ví dụ: 'ab?' sẽ match với cả 'a' và 'ab'

- '*?' , '+?','??': Match với nhiều text. Ví dụ
<.*> sẽ match với <h1>title</h1>. <.*?> sẽ chỉ match với <h1> và </h1>

- '{m}' : Chỉ định rằng chính xác m bản RE trước đó nên được match. Ví dụ a{6} sẽ match chính xác 6 kí tự 'a' ko phải 5

- '{m,n}' : Gây ra kết quả RE match từ m tới n lần lặp. Ví dụ a{3,5} sẽ match với các kí tự 'a' từ 3 đến 5.
- '{m,n}?' : match từ m tới n lần lặp nhưng cố gắng match với ít nhất số lần lặp có thể. ví dụ có 6 kí tự a là 'aaaaaa' trong khi 'a{3,5}' sẽ match với 5 kí tự 'a' thì 'a{3,5}?' sẽ match với 3 kí tự a

- '\' : sử dụng để match với các kí tự đặc biệt. hoặc tín hiệu 1 sequence đặc biệt

- [] : sử dụng để biểu thị 1 tập của các kí tự. Trong 1 tập:

+ các kí tự có thể được list. ví dụ [amk] sẽ match với 'a', 'm' hoặc 'k'

+ Phạm vi của các kí tự có thể được biểu thị bằng cách đưa ra 2 kí tự và chia bằng '-'. Ví dụ [a-z] sẽ match với các kí tự thường. [0-5][0-9] sẽ chỉ match với số có 2 chữ số từ 00-59 và [0-9A-Fa-f] sẽ match với các kí hiệu mã hexa. 

+ Kí tự đặc biệt mất đi ý nghĩa đặc biệt của chúng trong 1 bộ. Ví dụ [(+*)] sẽ match với các kí tự '(' ,'+' ,'*',')'

+ Các kí tự lớp như \w hay \s cũng được chấp nhận trong 1 set. mặc dù những kí tự này match phụ thuộc vào chế độ LOCALE hay UNICODE đang có hiệu lực

+ Các kí tự không ở trong phạm vi có thể được match bằng cách bổ sung cho tập. Nếu kí tự đầu tiên của 1 tập là '^' thì tất cả các kí tự không ở trong tập sẽ được match. Ví dụ [^5] sẽ mới các tất cả các kí tự ngoại trừ '5' và [^^] sẽ match với tất cả các kí tự ngaọi trừ '^'. 

+ Để match với kí tự ']' bên trong 1 tập. sử dụng '\' hoặc đặt nó tại nơi bắt đầu của 1 tập. Ví dụ: cả [()[\]{}] và []()[{}] sẽ match với dấu ngoặc


- '|' : A|B nơi mà A và B có thể được RE tùy ý. 1 RE sẽ match với cả A và B. để match kí tự '|' sử dụng '\' hoặc đặt cuối 1 tập ví dụ: [a|]

(...) : Match RE bên trong dấu ngoặc. chỉ bắt đầu và kết thúc của 1 nhóm. Nội dung của nhóm có thể 
được lấy ra sau khi match đc thực hiện. 

(?P<name>...): thuơng tự biểu thức ngoặc. nhưng substring match bởi group được truy cập thông qua biểu tượng tên group name. Group name phải được khai báo. và mỗi group phải được định nghĩa chỉ 1 lần với 1 RE.

Xét ví dụ sau

```

list = ['saphi 129123','sa 149129412','manh 12421']

pattern = re.compile('(?P<name>.*) (?P<number>.*)')

for i in list:
match = pattern.search(i)
print "Name: "+match.group('name')
print "Number: "+match.group('number')

```

Kết quả chạy chuơng trình

```

Name: saphi

Number: 129123

Name: sa

Number: 149129412

Name: manh

Number: 12421


```

- (?P=name) : match với các text được kết hợp bởi nhóm có tên là name


- (?#...) là 1 comment

- (?=...) match nếu ... match tiếp theo. ví dụ 'saphi (?=pham)' sẽ match với 'saphi' nếu theo sau nó là 'pham' ('saphi pham')

- (?!...) ko match nếu ... match tiếp. ví dụ 'saphi (?!pham)' sẽ ko match với 'saphi' nếu theo sau nó là 'pham'

- (?<=...) match nếu vị trí hiện tại trong string đứng trước bởi 1 match cho ... mà kết thúc ở ví trí hiện tại. Ví dụ '(<=abc)dk' sẽ match với 'dk' trong chuỗi 'abcdk'

## Trình tự đặc biệt bao gồm '\' và 1 kí tự trong danh sách dưới đây.

- \number: match nội dung cuả nhóm của cùng số. Nhóm được đánh số từ 1. Ví dụ. '(.+) \1' sẽ match với 'the the' hoặc '55 55' ko match với 'thethe'.

- \A Chỉ match tại bắt đầu của 1 chuỗi. Ví dụ có RE '\Aa' sẽ chỉ match với 'a' khi 'a' là bắt đầu của 1 string ('absb' )

- \b match với empty string nhưng chỉ tại nơi bắt đầu hoặc kết thúc của 1 từ. Ví dụ r'\bfoo\b' match với 'foo', 'foo.' ,'(foo)' , 'bar foo bar' ko match với 'foo3' hoặc 'foob'

- \B. match với empty string nhưng chỉ khi nó ko là bắt đầu hay kết thúc của từ. có nghĩa rằng r'py\B' match với 'python' , 'pya' ko match với 'py','py.','py!'

- \d khi cờ UNICODE ko được khai báo, match tất cả các chữ số hệ 10. tuơng đuơng với [0-9]. với cờ UNICODE được khai báo sẽ match với bất cứ điều gì được phân loại như là một chữ số thập phân trong UNICODE charactor properties database

- \D khi cờ UNICODE ko dc khai báo. match với các các kí tự ko là số. tuơng đg [^0-9]

- \s khi cờ UNICODE ko được khai báo. nó match với các kí tự khoảng trắng.

- \w khi cờ LOCALE và UNICODE ko được khai báo. match các kí tự chữ và số dấu gạch dưới . tuơng đuơng [a-zA-Z_0-9]

- \W ngược lại \w

- \Z chỉ match khi kết thúc của string
