De gui email ta dung thu vien smtplib
code

```
#!/usr/bin/env python
import smtplib
import sys
from email.mime.text import MIMEText
username = sys.argv[1] 
password = sys.argv[2]
from_addr = username
to_addr = sys.argv[3]

mail_server = 'smtp.gmail.com'
mail_server_port = 587

body = 'python send email through gmail'
msg = MIMEText(body)
msg['Subject'] = "Test Email"
msg['From'] = from_addr 
msg['To'] = to_addr

def send():
	try:
		s = smtplib.SMTP(mail_server,mail_server_port)
		s.starttls() #Xac thuc SSL
		s.login(username,password) # login
		print "Login success"
		s.sendmail(from_addr,to_addr,msg.as_string()) #sent
		print "Sent"
		s.quit()
	except Exception,R:
		print "Error: check again"
if __name__=="__main__":
	send()

```
