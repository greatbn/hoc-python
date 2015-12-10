##poplib

Thu vien cho phep su dung cac giao thuc POP3 va IMAP dung voi email

vi du dang nhap vao yahoo mail
```
import poplib
username= 'youruser@yahoo.com'
password = 'yourpassword'
p = poplib.POP3_SSL('pop.mail.yahoo.com')
p.user(username)
p.pass_(password)

```

```
Server mail google: pop.googlemail.com:995
```


poplib ho tro cac method sau

- `apop`
- `buffer`
- `certfile`
- `dele`
- `file`
- `getwelcome`
- `host`
- `keyfile`
- `list`
- `noop`
- `pass_`
- `port`
- `quit`
- `retr`
- `rpop`
- `rset`
- `set_debuglevel`
- `sock`
- `sslobj`
- `stat`
- `timestamp`
- `top`
- `uidl`
- `user`
- `welcome`
