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
server.py
import socket
s = socket.socket()
s.bind(("localhost", 3024))
s.listen(1)
print("Server running...")

while True:
    c, addr = s.accept()
    request = c.recv(4096).decode()
    print(f"Request received ")

    if "GET" in request:
        try:
            with open("index.html", "r") as f:
                data = f.read()
            response = "HTTP/1.1 200 OK\n\n" + data
        except FileNotFoundError:
            response = "HTTP/1.1 404 Not Found\n\nFile not found"
    elif "POST" in request:
        body = request.split("\n\n", 1)[-1]
        with open("upload.txt", "w") as f:
            f.write(body)
        response = "HTTP/1.1 200 OK\n\nFile Uploaded"
    else:
        response = "HTTP/1.1 400 Bad Request\n\nUnknown method"

    c.send(response.encode())
    c.close()

  client.py:
  import socket
s = socket.socket()
s.connect(("localhost", 3024))
ch = input("1.Download  2.Upload : ")
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

index.html:
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <p>hello world</p>
</body>
</html>
## OUTPUT
server.py
<img width="713" height="537" alt="image" src="https://github.com/user-attachments/assets/6097caf8-7b0e-437a-908f-9b0189d4c056" />
client.py
<img width="707" height="666" alt="image" src="https://github.com/user-attachments/assets/4e71d729-b316-4063-b960-304a3c921c44" />
<img width="716" height="177" alt="image" src="https://github.com/user-attachments/assets/520447be-cb05-453e-aaff-e63e60868049" />

upload.txt
<img width="715" height="310" alt="image" src="https://github.com/user-attachments/assets/f30be400-1e07-4414-897b-dfdfca659e04" />





## Result
Thus the socket for HTTP for web page upload and download created and Executed
