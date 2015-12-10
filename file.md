###FILE in Python

####Readfile
```
f = open(filename,'r'[,buffer])
f.read()
f.read(bytes)
f.readlines()
f.readline()
```
####Writefile
```

f = open(filename,'w')
f = open(filename,'a')
f.write(str)
f.writelines(object)

```
note: writelines() khong tao new line

##StringIO

from StringIO import StringIO
