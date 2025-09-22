# 2a_Stop_and_Wait_Protocol
## AIM 
To write a python program to perform stop and wait protocol
## ALGORITHM
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
### Server
```
import socket
import time


server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_socket.bind(('localhost', 9999))
server_socket.listen(1)

print("Server: Waiting for client connection...")
conn, addr = server_socket.accept()
print(f"Server: Connected to {addr}\n")

while True:
    
    frame = conn.recv(1024).decode()
    if not frame or frame == "END":
        print("Server: Transmission completed.")
        break

    print(f"Server: Received Frame {frame}")

    
    time.sleep(1)

    
    ack = f"ACK{frame}"
    conn.send(ack.encode())
    print(f"Server: Sent {ack}\n")

conn.close()
server_socket.close()
```

### Client
```
import socket
import time


client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client_socket.connect(('localhost', 9999))

frames = int(input("Enter number of frames to send: "))

for i in range(frames):
    frame = str(i)
    print(f"Client: Sending Frame {frame}")
    client_socket.send(frame.encode())

    
    ack = client_socket.recv(1024).decode()
    print(f"Client: Received {ack}\n")
    time.sleep(1)  # Simulate delay


client_socket.send("END".encode())
print("Client: Transmission completed.")

client_socket.close()

```


## OUTPUT

## Server

<img width="388" height="841" alt="image" src="https://github.com/user-attachments/assets/049fb6b8-0062-46d5-babe-10da555a0992" />

## Client

<img width="493" height="795" alt="image" src="https://github.com/user-attachments/assets/8a6900aa-ab2f-4322-8de5-d1dee3bf21c8" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
