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
client
```
import socket
s=socket.socket()
s.bind(('localhost',8000))
s.listen(5)
c,addr=s.accept()
address={"fe80::8f5e:49c:a806:cb62%15":"A8:59:5F:F0:0F:C3","165.165.79.1":"8A:BC:E3:FA"};
while True:
    ip=c.recv(1024).decode()
    try:
       c.send(address[ip].encode())
    except KeyError:
       c.send("Not Found".encode())
```
server
```
import socket
s=socket.socket()
s.connect(('localhost',8000))
while True:
    ip=input("Enter logical Address : ")
    s.send(ip.encode())
    print("MAC Address",s.recv(1024).decode())
```

## OUPUT - ARP
<img width="1778" height="907" alt="Screenshot 2026-05-12 131349" src="https://github.com/user-attachments/assets/b44c4694-0cdd-4b90-962c-b5cb9972d499" />

## PROGRAM - RARP
client
```
import socket
s = socket.socket()
s.bind(('localhost', 8001))
s.listen(5)
print("RARP Server is listening on port 8001...")
c, addr = s.accept()

address = {
    "A8:59:5F:F0:0F:C3": "fe80::8f5e:49c:a806:cb62%15",
    "8A:BC:E3:FA": "165.165.79.1"
}

while True:
    mac = c.recv(1024).decode()
    print(f"Received MAC: {mac}")
    ip = address.get(mac, "Not Found")
    c.send(ip.encode())
```
server
```
import socket

s = socket.socket()
s.connect(('localhost', 8001))

while True:
    mac = input("Enter Physical Address (MAC): ")
    s.send(mac.encode())
    print("IP Address:", s.recv(1024).decode()
```
## OUPUT -RARP
<img width="1739" height="846" alt="Screenshot 2026-05-12 132313" src="https://github.com/user-attachments/assets/4ae625f3-7114-4fe0-95ec-15bc7e418fce" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
