##URLLIB

Duoc su dung de doc 1 file tu web server

vi du

```
In [1]: import urllib

In [2]: url_file = urllib.urlopen('https://google.com') #Open file

In [3]: url_docs = url_file.read() #read file and save 

In [4]: url_file.close()

In [5]: len(url_docs)
Out[5]: 154147

In [6]: url_docs[:10]
Out[6]: '<!doctype '

In [7]: url_docs[-10:]
Out[7]: 'dy></html>'

```


#####method

urllib co cac phuong thuc sau

- read()

- close()

- readline()
```
In [23]: line = url_file.readline()

In [24]: line
Out[24]: 'function _gjh(){!_gjuc()&&window.google&&google.x&&google.x({id:"GJH"},function(){google.nav&&google.nav.gjh&&google.nav.gjh()})};window._gjh&&_gjh();</script><style>#gbar,#guser{font-size:13px;padding-top:1px !important;}#gbar{height:22px}#guser{padding-bottom:7px !important;text-align:right}.gbh,.gbd{border-top:1px solid #c9d7f1;font-size:1px}.gbh{height:0;position:absolute;top:24px;width:100%}@media all{.gb1{height:22px;margin-right:.5em;vertical-align:top}#gbar{float:left}}a.gb1,a.gb4{text-decoration:underline !important}a.gb1,a.gb4{color:#00c !important}.gbi .gb4{color:#dd8e27 !important}.gbf .gb4{color:#900 !important}\n'
```
- readlines()

```

In [19]: list = url_file.readlines()

In [20]: list[1]
Out[20]: 'function _gjh(){!_gjuc()&&window.google&&google.x&&google.x({id:"GJH"},function(){google.nav&&google.nav.gjh&&google.nav.gjh()})};window._gjh&&_gjh();</script><style>#gbar,#guser{font-size:13px;padding-top:1px !important;}#gbar{height:22px}#guser{padding-bottom:7px !important;text-align:right}.gbh,.gbd{border-top:1px solid #c9d7f1;font-size:1px}.gbh{height:0;position:absolute;top:24px;width:100%}@media all{.gb1{height:22px;margin-right:.5em;vertical-align:top}#gbar{float:left}}a.gb1,a.gb4{text-decoration:underline !important}a.gb1,a.gb4{color:#00c !important}.gbi .gb4{color:#dd8e27 !important}.gbf .gb4{color:#900 !important}\n'


```
- fineno()

```

In [12]: url_file.fileno()
Out[12]: 5


```
- info()
```
In [13]: url_file.info()
Out[13]: <httplib.HTTPMessage instance at 0x7f669e764368>

```
- geturl()

```
In [14]: url_file.geturl()
Out[14]: 'https://www.google.com/'

```
