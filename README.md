# 4.Execution_of_NetworkCommands
## AIM :
Use of Network commands in Real Time environment
## Software Required : 
* Command Prompt 

* Network Protocol Analyzer
## Procedure: 


To do this experiment, follow these steps:

Students have to understand basic networking commands such as:

- `tcpdump`
- `netstat`
- `ifconfig`
- `nslookup`
- `traceroute`

Additionally, capture **ping** and **traceroute** PDUs using a **network protocol analyzer**.

This includes all commands related to **network configuration**, such as:

- Switching to **privileged mode** and **normal mode**
- Configuring **router interfaces**
- Saving the configuration to **flash memory** or **permanent memory**

### This includes the following commands:

- Configuring the router commands  
- General commands to configure network  
- Privileged mode commands of a router  
- Router processes & statistics  
- IP commands  
- Other IP commands (e.g., `show ip route`)

---

## Program:

### `Client`

```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    host = input("Enter website to ping (or 'exit'): ").strip()
    if not host:
        continue
    s.send(host.encode('utf-8'))
    if host.lower() == 'exit':
        print("Exiting...")
        break
    print(s.recv(8192).decode('utf-8'))

s.close()

```

### `server.py`

```
import socket
import subprocess
import platform

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)
print("Server listening on port 8000...")
c, addr = s.accept()
print("Connected:", addr)

while True:
    hostname = c.recv(1024).decode().strip()
    if not hostname or hostname.lower() == 'exit':
        print("Client disconnected.")
        break

    # use correct flag for platform
    flag = '-n' if platform.system().lower() == 'windows' else '-c'
    try:
        completed = subprocess.run(['ping', flag, '2', hostname],
                                   capture_output=True, text=True, timeout=10)
        output = completed.stdout + (completed.stderr or '')
    except Exception as e:
        output = f"Ping failed: {e}"
    c.sendall(output.encode('utf-8'))

c.close()
s.close()

```

## Output:

#### `Client`
<img width="737" height="362" alt="image" src="https://github.com/user-attachments/assets/66a3d33c-1620-4437-a192-f2aba2607869" />

#### `Server`
<img width="679" height="112" alt="image" src="https://github.com/user-attachments/assets/c9abaa9d-f47f-41a3-9572-d84f191e0e72" />


## Result
Thus Execution of Network commands Performed.
