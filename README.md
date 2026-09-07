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
SERVER:
```import socket
s = socket. socket()
s.bind(("localhost",8081))
s.listen(1)
print("Server running ... ")
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
CLIENT:
```
import socket
s = socket. socket()
s.connect(("localhost", 8081))
ch = input("1.Download 2.Upload : ")
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())
    data = s.recv(4096)
    print(data.decode())
else:
    msg = input("Enter data to upload: ")
    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s. send(req.encode())
    data = s.recv(1024)
    print(data.decode())
s.close()
```

## OUTPUT
<img width="1797" height="670" alt="Screenshot 2026-09-07 130317" src="https://github.com/user-attachments/assets/5087d7c6-60ce-4c1e-941c-4a7d965660dd" />
<img width="1835" height="100" alt="Screenshot 2026-09-07 130332" src="https://github.com/user-attachments/assets/4dcce67a-d263-45b7-9bfb-25bdc7bdd3da" />
<img width="1915" height="732" alt="Screenshot 2026-09-07 130349" src="https://github.com/user-attachments/assets/2ca2b2e5-b395-4a71-9309-e37e16cd7e1f" />
<img width="1832" height="137" alt="Screenshot 2026-09-07 130411" src="https://github.com/user-attachments/assets/16ea24aa-1878-448b-a525-45ca07fc3370" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
