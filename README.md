# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM

Developed By: Gokul C
Register Number: 212223240040

### SERVER:
```
import socket

def send_file(filename, client_socket):
    with open(filename, 'rb') as file:
        for data in file:
            client_socket.sendall(data)

def start_server():
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server_socket.bind(('127.0.0.1', 5555))
    server_socket.listen(5)
    print("Server started, listening on port 5555")

    while True:
        client_socket, addr = server_socket.accept()
        print(f"Accepted connection from {addr}")

        filename = input("Enter filename to send: ")
        try:
            send_file(filename, client_socket)
            print(f"File '{filename}' sent successfully")
        except FileNotFoundError:
            print(f"File '{filename}' not found")

        client_socket.close()

start_server()
```

### CLIENT:

```
import socket

def receive_file(filename, server_socket):
    with open(filename, 'wb') as file:
        while True:
            data = server_socket.recv(1024)
            if not data:
                break
            file.write(data)

def start_client():
    client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    client_socket.connect(('127.0.0.1', 5555))

    filename = input("Enter filename to save: ")
    client_socket.sendall(filename.encode())

    receive_file(filename, client_socket)
    print(f"File '{filename}' received successfully")

    client_socket.close()

start_client()

```

## OUPUT 

### SERVER:

![311163404-33a75331-236c-4923-8bc1-aa71ee41eea9](https://github.com/Gokul1410/3c.FILE_TRANSFER_USING_TCP_SOCKETS/assets/153058321/d0c49c75-f618-48f7-ab77-7e909fa0fa0e)

### CLIENT:
![311163464-4a07734d-29c4-4507-9880-df467a2794f5](https://github.com/Gokul1410/3c.FILE_TRANSFER_USING_TCP_SOCKETS/assets/153058321/c5d84de9-d33d-4d5b-b779-06f282ae43d3)


## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
