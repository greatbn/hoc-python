###socket

```
import socket
buffer = 1000
s  = socket.socket() # tao 1 object socket
s.connect ((IP,port)) # ket noi toi dia chi ip hoac domain tren port
recv = s.recv(buffer) # nhan ve buffer byte
print recv
```


check status web server 

```
import socket
import sys
import re
def check_webserver(addr,port,resource):
	#build up HTTP request string
	if not resource.startswith('/'):
		resource = '/' + resource
	request_string ='GET %s HTTP/1.1\r\nHost: %s\r\n\r\n' %(resource,addr)
	print 'HTTP request'
	print '|||\n%s|||' %request_string
	#create a socket
	s = socket.socket()
	print 'Attempting to connect to %s on port %s' %(addr,port)
	try:
		s.connect((addr,port))
		s.send(request_string)

		response = s.recv(100)

		print 'Receive 100 byte from HTTP Server'
	except socket.error, e:
		print 'Connection to %s on port %s failed: %s' %(addr.port,e)
		return False
	finally:
		print 'Close Connection'
		s.close()
	lines = response.splitlines()
	print 'First line in response \n %s' %lines[0]
	try:
		version , status, message = re.split(r'\s+',lines[0],2)
		print 'Version %s status %s message %s' %(version,status,message)
	except ValueError:
		print 'failed to split line'
		return False
	if status in ['200','301']:
		print 'Success. Status code: %s' %status
		return True
	else:
		print 'Status %s'%status
		return False
if __name__=='__main__':
	from optparse import OptionParser
	parser = OptionParser()
	parser.add_option('-a','--address',dest='address',default='localhost',help='Address for destination',metavar='ADDRESS')
	parser.add_option('-p','--port',dest='port',default='80',help='Port for destination',metavar='PORT')
	parser.add_option('-r','--resource',dest='resource',default='index.php',help='Resource for destination',metavar='RESOURCE')

	(options,args) = parser.parse_args()
	check = check_webserver(options.address,int(options.port),str(options.resource))
	print 'Check web server return %s' %check
	sys.exit(not check)	
```

