###Regular Expression

##các kí tự đặc biệt

- '.' trong chế độ mặc định , kí tự này match với tất cả các kí tự ngoại trừ newline. nếu cờ DOTALL được set. kí tự này sẽ match tất cả các kí tự bao gồm 1 newline

```
>>> import re
>>> obj = re.compile('.')
>>> obj.findall('aaa')
['a', 'a', 'a']

```

- '^' : match với sự bắt đầu của chuỗi. và trong mode MULTILINE cũng match lập tức sau mỗi newline

```
>>> obj = re.compile('^a')
>>> obj.findall('aaa')

```

- '$' : match với kết thúc của string hoặc chỉ trước dòng mới của 1 string. trong mode MULTILINE cũng match trước 1 dòng. Ví dụ: 'foo' match với 'foobar' trong khi 'foo$' chỉ match với 'foo'. Ví dụ 2: tìm kiếm 'foo.$' trong 'foo1\nfoo2\n' bình thường match với 'foo2' nhưng trong chế độ MULTILINE match với 'foo1'. Tìm kiếm '$' trong 'foo\n' sẽ tìm thấy 2 empty match 1 là trước 1 newline và 1 cuối của 1 string

```
>>> obj = re.compile('ab$')
>>> obj.findall('aaa')
[]
>>> obj.findall('aaab')
['ab']

```

- '*': ví dụ 'ab*' sẽ match với 'a','ab','a'. theo sau bởi số các kí tự 'b'
```
>>> obj = re.compile('ab*')
>>> obj.findall('aaab')
['a', 'a', 'ab']
```

- '+': ví dụ 'ab+' sẽ mới với 'a' theo sau bởi số các kí tự b khác 0. -> ko match với 'a'. Sẽ match với 'ab' 'abb'

```
>>> obj = re.compile('ab+')
>>> obj.findall('aaab')
['ab']
```
- '?': gây ra kết quả match với cả số lần lặp 0 và 1. Ví dụ: 'ab?' sẽ match với cả 'a' và 'ab'
```
>>> obj = re.compile('ab?')
>>> obj.findall('aaab')
['a', 'a', 'ab']

```

- '*?' , '+?' , '??': Match với nhiều text. Ví dụ
```
>>> obj = re.compile('<.*>')
>>> obj.findall('<h1>title</h1>')
['<h1>title</h1>']
>>> obj = re.compile('<.*?>')
>>> obj.findall('<h1>title</h1>')
['<h1>', '</h1>']

```

- '{m}' : Chỉ định rằng chính xác m bản RE trước đó nên được match. Ví dụ a{6} sẽ match chính xác 6 kí tự 'a' ko phải 5

```
>>> obj = re.compile('a{3}')
>>> obj.findall('aaababaaaa')
['aaa', 'aaa']

```

- '{m,n}' : Gây ra kết quả RE match từ m tới n lần lặp. Ví dụ a{3,5} sẽ match với các kí tự 'a' từ 3 đến 5.

```
>>> obj = re.compile('a{3,5}')
>>> obj.findall('aaababaaaa')
['aaa', 'aaaa']

```
- '{m,n}?' : match từ m tới n lần lặp nhưng cố gắng match với ít nhất số lần lặp có thể. ví dụ có 6 kí tự a là 'aaaaaa' trong khi 'a{3,5}' sẽ match với 5 kí tự 'a' thì 'a{3,5}?' sẽ match với 3 kí tự a
```
>>> obj = re.compile('a{3,5}?')
>>> obj.findall('aaababaaaa')
['aaa', 'aaa']
```


- '\' : sử dụng để match với các kí tự đặc biệt. hoặc tín hiệu 1 sequence đặc biệt

- [] : sử dụng để biểu thị 1 tập của các kí tự. Trong 1 tập:

       + các kí tự có thể được list. ví dụ [amk] sẽ match với 'a', 'm' hoặc 'k'
       ```
        >>> obj = re.compile('[amk]')
        >>> obj.findall('aimdk')
        ['a', 'm', 'k']

       ```

       + Phạm vi của các kí tự có thể được biểu thị bằng cách đưa ra 2 kí tự và chia bằng '-'. Ví dụ [a-z] sẽ match với các kí tự thường. [0-5][0-9] sẽ chỉ match với số có 2 chữ số từ 00-59 và [0-9A-Fa-f] sẽ match với các kí hiệu mã hexa. 
       ```
       >>> obj = re.compile('[a-g]')
        >>> obj.findall('aimdkz98')
        ['a', 'd']
       ```

       + Kí tự đặc biệt mất đi ý nghĩa đặc biệt của chúng trong 1 bộ. Ví dụ [(+*)] sẽ match với các kí tự '(' ,'+' ,'*',')'
       
       ```
        >>> obj = re.compile('[(+*)]')
        >>> obj.findall('a+i*(mdkz98)')
        ['+', '*', '(', ')']

       ```

       + Các kí tự lớp như \w hay \s cũng được chấp nhận trong 1 set. mặc dù những kí tự này match phụ thuộc vào chế độ LOCALE hay UNICODE đang có hiệu lực

       + Các kí tự không ở trong phạm vi có thể được match bằng cách bổ sung cho tập. Nếu kí tự đầu tiên của 1 tập là '^' thì tất cả các kí tự không ở trong tập sẽ được match. Ví dụ [^5] sẽ mới các tất cả các kí tự ngoại trừ '5' và [^^] sẽ match với tất cả các kí tự ngoai trừ '^'.
       
       ```
        >>> obj = re.compile('[^o]')
        >>> obj.findall('heLLo')
        ['h', 'e', 'L', 'L']

       ```

      + Để match với kí tự ']' bên trong 1 tập. sử dụng '\' hoặc đặt nó tại nơi bắt đầu của 1 tập. Ví dụ: cả [()[\]{}] và []()[{}] sẽ match với dấu ngoặc
        
        ```
        >>> obj = re.compile('[[\]]')
        >>> obj.findall('[heLLo]')
        ['[', ']']
        ```

- '|' : A|B nơi mà A và B có thể được RE tùy ý. 1 RE sẽ match với cả A và B. để match kí tự '|' sử dụng '\' hoặc đặt cuối 1 tập ví dụ: [a|]
```
>>> obj = re.compile('slow|fast')
>>> obj.findall('this is slow car')
['slow']
>>> obj.findall('this is fast car')
['fast']

```

- (...) : Match RE bên trong dấu ngoặc. chỉ bắt đầu và kết thúc của 1 nhóm. Nội dung của nhóm có thể 
được lấy ra sau khi match đc thực hiện. 

```
>>> obj = re.compile('{([a-zA-Z]*?)}')
>>> obj.findall('this is fast {car}')
['car']

```

- (?P<name>...): thuơng tự biểu thức ngoặc. nhưng substring match bởi group được truy cập thông qua biểu tượng tên group name. Group name phải được khai báo. và mỗi group phải được định nghĩa chỉ 1 lần với 1 RE.

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

```
>>> obj = re.compile('saphi (?=pham)')
>>> obj.findall('saphi')
[]
>>> obj.findall('saphi pham')
['saphi ']

```
- (?!...) ko match nếu ... match tiếp. ví dụ 'saphi (?!pham)' sẽ ko match với 'saphi' nếu theo sau nó là 'pham'

```
>>> obj = re.compile('saphi (?!pham)')
>>> obj.findall('saphi')
[]
>>> obj.findall('saphi pham')
[]
>>> obj.findall('saphi phi')
['saphi ']

```
- (?<=...) match nếu vị trí hiện tại trong string đứng trước bởi 1 match cho ... mà kết thúc ở ví trí hiện tại. Ví dụ '(?<=abc)dk' sẽ match với 'dk' trong chuỗi 'abcdk'

```
>> obj = re.compile('(?<=sa)phi')
>>> obj.findall('sa phi')
[]
>>> obj.findall('saphi')
['phi']

```
## Trình tự đặc biệt bao gồm '\' và 1 kí tự trong danh sách dưới đây.

- \number: match nội dung cuả nhóm của cùng số. Nhóm được đánh số từ 1. Ví dụ. '(.+) \1' sẽ match với 'the the' hoặc '55 55' ko match với 'thethe'.

- \A Chỉ match tại bắt đầu của 1 chuỗi. Ví dụ có RE '\Aa' sẽ chỉ match với 'a' khi 'a' là bắt đầu của 1 string ('absb' )

```
>>> obj = re.compile('\APhi')
>>> obj.findall('saphi')
[]
>>> obj.findall('Phi Sa')
['Phi']

```

- \b match với empty string nhưng chỉ tại nơi bắt đầu hoặc kết thúc của 1 từ. Ví dụ r'\bfoo\b' match với 'foo', 'foo.' ,'(foo)' , 'bar foo bar' ko match với 'foo3' hoặc 'foob'

```
>>> obj = re.compile(r'\bPhi')
>>> obj.findall('Phi Sa')
['Phi']
>>> obj.findall('PhiSa')
['Phi']
>>> obj = re.compile(r'\bPhi\b')
>>> obj.findall('PhiSa')
[]
>>> obj.findall('Phi Sa')
['Phi']

```

- \B. match với empty string nhưng chỉ khi nó ko là bắt đầu hay kết thúc của từ. có nghĩa rằng r'py\B' match với 'python' , 'pya' ko match với 'py','py.','py!'

```
>>> obj = re.compile(r'Py\B')
>>> obj.findall(' Python')
['Py']
>>> obj.findall('Py')
[]
>>> obj.findall('Py!')
[]

```

- \d khi cờ UNICODE ko được khai báo, match tất cả các chữ số hệ 10. tuơng đuơng với [0-9]. với cờ UNICODE được khai báo sẽ match với bất cứ điều gì được phân loại như là một chữ số thập phân trong UNICODE charactor properties database

- \D khi cờ UNICODE ko dc khai báo. match với các các kí tự ko là số. tuơng đg [^0-9]

- \s khi cờ UNICODE ko được khai báo. nó match với các kí tự khoảng trắng.
```
>>> obj = re.compile(r'\sSa\s')
>>> obj.findall('SaPhi')
[]
>>> obj.findall('Sa Phi')
[]
>>> obj.findall(' Sa Phi')
[' Sa ']

```
- \w khi cờ LOCALE và UNICODE ko được khai báo. match các kí tự chữ và số dấu gạch dưới . tuơng đuơng [a-zA-Z_0-9]
```
>>> obj = re.compile(r'\w')
>>> obj.findall('SaPhi!$')
['S', 'a', 'P', 'h', 'i']
```
- \W ngược lại \w

```
>>> obj = re.compile(r'\W')
>>> obj.findall('SaPhi!$')
['!', '$']
```

- \Z chỉ match khi kết thúc của string

```

```

###Các hàm
###1.re.compile(pattern, flags=0)

```

prog = re.compile(pattern)
result = prog.match(string)


```
tuơng đương với 

```
result = re.match(pattern, string)
```


re.DEBUG

re.I
re.IGNORECASE

re.L
re.LOCALE

re.M
re.MULTILINE

re.S
re.DOTALL

re.X
re.VERBOSE

2 RE dưới dây giống nhau

```
a = re.compile(r"""\d +  # the integral part
                   \.    # the decimal point
                   \d *  # some fractional digits""", re.X)

b = re.compile(r"\d+\.\d*")
```

###2.re.search(pattern, string, flags=0)

###3.re.match(pattern, string, flags=0)


###4.re.split(pattern, string, maxsplit=0, flags=0)

Cắt string bằng sự xuất hiện của pattern. 

```
>>> re.split('\W+', 'Words, words, words.')
['Words', 'words', 'words', '']
>>> re.split('(\W+)', 'Words, words, words.')
['Words', ', ', 'words', ', ', 'words', '.', '']
>>> re.split('\W+', 'Words, words, words.', 1)
['Words', 'words, words.']
>>> re.split('[a-f]+', '0a3B9', flags=re.IGNORECASE)
['0', '3', '9']

```

###5.re.findall(pattern, string, flags=0)

###6.re.finditer(pattern, string, flags=0)¶

###7.re.sub(pattern, repl, string, count=0, flags=0)

###8.re.subn(pattern, repl, string, count=0, flags=0)

tuong tu re.sub() nhung tra ve 1 tuple

###9. re.escape(string)

###10. re.purge()
clear cache


Vi du 1: 

<img src="https://www.evernote.com/shard/s637/res/d203ab54-c17d-4f8c-94d3-4d7488ed8dbf">
- Dau tien ta can import thu vien re
-  Tiep theo khai bao re_string1 day la mau de tim kiem. bat dau bang '{{' va ket thuc boi '}}'
- 1 some_string chua cac chuoi co mau
- lap cac chuoi trong 1 string su dung ham findall() se tim kiem tu nao trung voi mau


Note: Su dung re_ob = re.recompile(pattern)
                        re_ob.search(pattern) cho toc do thuc thi nhanh hon

##Raw String and regular expression



- Cac method thuong su dung: findall(), finditer(), match(), search()

* findall

findall() match cac tu bat dau bang 't' va ket thuc bang 'e' chi thi '.*?' se match tat ca cac ki tu ke ca khoang trang do vay 'ttt eee' cung match
findall() tra ve list cua 1 tuple

de loai bo khoang trang ta dung 


finditer() khac voi findall() o ket qua tra ve la iterator

- search() va match() tuong doi giong nhau. search() tim ko theo tuan tu. con match() tim theo tuan tu



- Tham so pos va endpos: pos la gia tri index bat dau tim kiem mau tren string va endpos la gia tri index ket thuc tim kiem 


