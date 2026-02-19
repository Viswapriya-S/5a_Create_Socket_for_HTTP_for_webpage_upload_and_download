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
```
import socket

def download_file(host, port, filename):
    req = f"GET /{filename} HTTP/1.1\r\nHost: {host}\r\nConnection: close\r\n\r\n"
    
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.connect((host, port))
        s.sendall(req.encode())
        response = b""
        while (data := s.recv(4096)):
            response += data

    body = response.split(b"\r\n\r\n", 1)[1]
    out = f"downloaded_{filename}"
    with open(out, "wb") as f:
        f.write(body)

    print(f"Downloaded as {out}")

if __name__ == "__main__":
    download_file("127.0.0.1", 8080, "example.txt")

```
## OUTPUT
<img width="818" height="320" alt="Screenshot 2026-02-19 104343" src="https://github.com/user-attachments/assets/1cc47f12-17d0-45fe-9b5c-73e9ef96916b" />

<img width="778" height="332" alt="Screenshot 2026-02-19 104405" src="https://github.com/user-attachments/assets/622e493c-5e29-4983-bca5-56baff4dca22" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
