# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
## Server
```

import socket

# Table that stores IP address and the corresponding MAC address
arp_table = {
    "192.168.1.1": "00:1A:2B:3C:4D:5E",
    "192.168.1.2": "00:1A:2B:3C:4D:5F",
    "192.168.1.3": "00:1A:2B:3C:4D:60",
    "192.168.1.4": "00:1A:2B:3C:4D:61",
}

# Create a TCP socket and wait for the client
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(("localhost", 8000))
server.listen(1)
print("ARP Server started. Waiting for client...")

# Accept the socket created by the client
conn, addr = server.accept()
print("Connected to client:", addr)

# Read the IP address sent by the client
ip = conn.recv(1024).decode().strip()
print("Received IP address:", ip)

# Map the IP address to its MAC address and return it
mac = arp_table.get(ip, "MAC address not found")
conn.send(mac.encode())
print("Sent MAC address:", mac)

conn.close()
server.close()
```
## Client
```
import socket

# Establish a socket connection between client and server
client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect(("localhost", 8000))
print("Connected to ARP server")

# Get the IP address to be converted into a MAC address
ip = input("Enter the IP address: ")

# Send this IP address to the server
client.send(ip.encode())

# Receive the MAC address returned by the server
mac = client.recv(1024).decode()
print("MAC address of", ip, "is:", mac)

client.close()
```
## OUPUT - ARP
<img width="940" height="323" alt="image" src="https://github.com/user-attachments/assets/7a4bbf52-5ce4-4e1c-b61a-e8edb18eb5ee" />

## PROGRAM - RARP
## Server
```
import socket

# Table that stores MAC address and the corresponding IP address
rarp_table = {
    "00:1A:2B:3C:4D:5E": "192.168.1.1",
    "00:1A:2B:3C:4D:5F": "192.168.1.2",
    "00:1A:2B:3C:4D:60": "192.168.1.3",
    "00:1A:2B:3C:4D:61": "192.168.1.4",
}

# Create a TCP socket and wait for the client
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(("localhost", 8000))
server.listen(1)
print("RARP Server started. Waiting for client...")

# Accept the socket created by the client
conn, addr = server.accept()
print("Connected to client:", addr)

# Read the MAC address sent by the client
mac = conn.recv(1024).decode().strip().upper()
print("Received MAC address:", mac)

# Map the MAC address to its IP address and return it
ip = rarp_table.get(mac, "IP address not found")
conn.send(ip.encode())
print("Sent IP address:", ip)

conn.close()
server.close()
```
## Client
```
import socket

# Establish a socket connection between client and server
client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect(("localhost", 8000))
print("Connected to RARP server")

# Get the MAC address to be converted into an IP address
mac = input("Enter the MAC address: ")

# Send this MAC address to the server
client.send(mac.encode())

# Receive the IP address returned by the server
ip = client.recv(1024).decode()
print("IP address of", mac, "is:", ip)

client.close()
```
## OUPUT -RARP
<img width="941" height="320" alt="image" src="https://github.com/user-attachments/assets/374a04e2-47aa-4ddf-aedf-bde6fbbbe974" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
