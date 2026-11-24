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
SERVER
```
import socket

# Create TCP socket
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Bind server to IP and port
server.bind(('localhost', 8002))
server.listen(1)

print("Waiting for client connection...")

conn, addr = server.accept()
print("Client connected:", addr)

while True:
    frame = input("Enter frame data (exit to stop): ")

    if frame.lower() == "exit":
        break

    # Send one frame
    conn.sendall(frame.encode())

    print("Frame sent:", frame)

    # Wait for acknowledgement
    ack = conn.recv(1024).decode()

    print("Received ACK:", ack)

conn.close()
server.close()

print("Server closed.")
```
CLIENT
```
import socket

# Create TCP socket
client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Connect to server
client.connect(('localhost', 8002))

print("Connected to server.")
print("Waiting for frames...")

while True:
    # Receive frame from server
    frame = client.recv(1024).decode()

    if not frame:
        break

    print("Received frame:", frame)

    # Send acknowledgement
    client.sendall("ACK: Frame received successfully".encode())

    print("Acknowledgement sent.")

client.close()

print("Client disconnected.")
```
## OUTPUT
SERVER
<img width="1910" height="1007" alt="image" src="https://github.com/user-attachments/assets/f65cf696-c12d-46ee-af2e-d610958bee27" />

CLIENT

<img width="1917" height="1018" alt="image" src="https://github.com/user-attachments/assets/c29a8181-95f8-4afd-8d42-c5f0e6b7e8eb" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
