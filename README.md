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
SERVER.PY:
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
CLIENT.PY:
```
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
OUTPUT:

<img width="1110" height="352" alt="image" src="https://github.com/user-attachments/assets/f75173bd-aaf9-4053-9442-c0916e15286e" />

<img width="1053" height="356" alt="image" src="https://github.com/user-attachments/assets/11c8ccb8-9286-4194-a635-8c261e5f2b17" />

1.UPLOAD OUTPUT:

<img width="1113" height="612" alt="image" src="https://github.com/user-attachments/assets/814d4c8b-7234-450e-a887-f1f2a838c387" />

2.DOWNLOAD OUTPUT:




  
## Result
Thus the socket for HTTP for web page upload and download created and Executed
