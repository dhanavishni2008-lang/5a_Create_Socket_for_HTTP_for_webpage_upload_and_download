# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## Program 

CLIENT:

```
#DEVELOPED BY: DHANAVISHNI M
#REGISTER NO: 212225040064

import socket
s = socket.socket()
s.connect(("localhost",8080))
ch = input("1.Download 2.Upload : ")
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())
    data = s.recv(4096)
    print(data.decode())
else:
    msg = input("Enter data to upload: ")
    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())
    data = s.recv(1024)
    print(data.decode())
s.close()
```
SERVER:
```
import socket
s = socket.socket()
s.bind(("localhost",8080))
s.listen(1)
print("Server running...")
while True:
    c,addr = s.accept()
    request = c.recv(1024).decode()
    print("Request received")
    if "GET" in request:
        f = open("index.html","r")
        data = f.read()
        f.close()
        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())
    elif "POST" in request:
        data = request.split("\n\n")[1]
        f = open("upload.txt","w")
        f.write(data)
        f.close()
        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())
    c.close()
```
INDEX.html:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome Page</title>
</head>
<body>
    <h1>Welcome to the Python HTTP Server!</h1>
    <p>This is the default page served by the server.</p>

</body>
</html>
```
## OUTPUT
CLIENT(download):

<img width="892" height="507" alt="image" src="https://github.com/user-attachments/assets/9077d2d3-1779-4911-b1d3-50c6823887e5" />

SERVER(download):

<img width="849" height="270" alt="image" src="https://github.com/user-attachments/assets/9d3842d8-2b82-4695-918b-747efaef6d7c" />

client(upload):

<img width="818" height="294" alt="image" src="https://github.com/user-attachments/assets/d2313124-1a80-4826-94e9-3b5fecd2420a" />

SERVER(upload):

<img width="849" height="270" alt="image" src="https://github.com/user-attachments/assets/a3ae7380-7609-4e22-ba23-d20114527bc6" />
<img width="1377" height="464" alt="WhatsApp Image 2026-05-28 at 10 18 35 PM" src="https://github.com/user-attachments/assets/a608d064-0c52-4801-8a6b-2c4d75d1aab4" />


## Result
Thus the socket for HTTP for web page upload and download created and Executed
