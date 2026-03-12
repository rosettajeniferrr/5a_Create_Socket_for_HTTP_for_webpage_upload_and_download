# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download

## Algorithm

1. Start the program.
2. Create a socket connection between the client and the server using localhost and port number.
3. Get the user choice to either download the webpage (GET request) or upload data (POST request).
4. Client sends the request to the server based on the user selection.
5. Server processes the request – sends the webpage for download or stores the uploaded data in a file and sends a response to the client.
6. Close the connection and stop the program.
## Program 
## Server.py
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
## Client.py
```
import socket

s = socket.socket()
s.connect(("localhost",8080))

ch = input("1.Download 2.Upload : ")

# Download webpage
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

# Upload file
else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())

s.close()
```
## index.html
```
<title>
    <head>
        <title>index html server</title>
        
    </head>
    <body>
        <h1>hello from python socket server</h1>
    </body>
</title>
```
## upload.text
<img width="1053" height="240" alt="image" src="https://github.com/user-attachments/assets/cc7e6a09-b1e6-4485-b094-d58101e01fa5" />

## OUTPUT
<img width="1282" height="320" alt="image" src="https://github.com/user-attachments/assets/0cbb99f7-1743-490a-9df2-a726d38fb779" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
