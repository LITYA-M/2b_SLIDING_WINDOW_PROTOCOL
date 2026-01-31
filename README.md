# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM

client.py

```
import socket
server_socket = socket.socket()
server_socket.bind(('localhost', 8000))
server_socket.listen(1)

print("Waiting for connection from server...")
connection, addr = server_socket.accept()
print(f"Connected to: {addr}")

total_frames = int(input("Enter number of frames to send: "))
frames = list(range(total_frames))
window_size = int(input("Enter Window Size: "))

start = 0  
while start < len(frames):
    end = start + window_size
    frame_batch = frames[start:end] 
    connection.send(str(frame_batch).encode())  
    ack = connection.recv(1024).decode()
    if ack:
        print(ack)
        start = end
```

server.py

```
import socket

client_socket = socket.socket()
client_socket.connect(('localhost', 8000))

while True:
    data = client_socket.recv(1024).decode()
    if not data:
        break
    print(data)
    client_socket.send("Acknowledgement received from the server".encode())
```
## OUPUT

client.py

<img width="634" height="199" alt="Screenshot 2026-01-31 142657" src="https://github.com/user-attachments/assets/1c63b99c-6e41-4479-b091-0a647d566659" />

server.py

<img width="647" height="101" alt="Screenshot 2026-01-31 142712" src="https://github.com/user-attachments/assets/ee513ca8-c779-4d53-b9fc-87186d7b9d68" />
## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
