# 4.Execution_of_NetworkCommands
## AIM :Use of Network commands in Real Time environment
## Software : Command Prompt And Network Protocol Analyzer
## Procedure: To do this EXPERIMENT- follows these steps:
<BR>
In this EXPERIMENT- students have to understand basic networking commands e.g cpdump, netstat, ifconfig, nslookup ,traceroute and also Capture ping and traceroute PDUs using a network protocol analyzer 
<BR>
All commands related to Network configuration which includes how to switch to privilege mode
<BR>
and normal mode and how to configure router interface and how to save this configuration to
<BR>
flash memory or permanent memory.
<BR>
This commands includes
<BR>
• Configuring the Router commands
<BR>
• General Commands to configure network
<BR>
• Privileged Mode commands of a router 
<BR>
• Router Processes & Statistics
<BR>
• IP Commands
<BR>
• Other IP Commands e.g. show ip route etc.
<BR>

## Program:
client
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

print("Connected. Type any network command (ipconfig, ping, etc.) or 'exit'.")

while True:
    cmd = input("Enter command: ").strip()
    if not cmd:
        continue

    s.send(cmd.encode('utf-8'))
    
    if cmd.lower() == "exit":
        print("Exiting...")
        break

    output = s.recv(65536).decode()
    print("\n----- RESULT -----")
    print(output)
    print("------------------\n")

s.close()
```
server
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
    command = c.recv(1024).decode().strip()
    if not command or command.lower() == 'exit':
        print("Client disconnected.")
        break

    try:
        # Run ANY command the client sends
        completed = subprocess.run(
            command, 
            capture_output=True, 
            text=True, 
            shell=True
        )
        output = completed.stdout + (completed.stderr or "")
    except Exception as e:
        output = f"Command failed: {e}"

    c.sendall(output.encode('utf-8'))

c.close()
s.close()
```
## Output

### netstat

<img width="1445" height="910" alt="image" src="https://github.com/user-attachments/assets/d7e471f2-fa90-4d07-b4d0-90f9999c91de" />


### ipconfig

<img width="876" height="752" alt="image" src="https://github.com/user-attachments/assets/0bb14401-422e-46a3-a83c-30a16231f95c" />


### ping

<img width="755" height="346" alt="image" src="https://github.com/user-attachments/assets/93dfe675-2b24-4183-83cb-86e2a9e18565" />


### tracert

<img width="707" height="301" alt="image" src="https://github.com/user-attachments/assets/341b3a5c-95f1-48b1-9493-146fdcab06c2" />


### nslookup

<img width="591" height="293" alt="image" src="https://github.com/user-attachments/assets/f0bc661c-12a1-4895-89e0-6e803dae1af1" />


### getmac

<img width="788" height="246" alt="image" src="https://github.com/user-attachments/assets/51951111-e051-4a1c-8d8d-051c4e6ad6c3" />


### hostname

<img width="365" height="157" alt="image" src="https://github.com/user-attachments/assets/da2053dc-ffba-4d60-a167-851a84491bed" />


### nbtstat

<img width="848" height="618" alt="image" src="https://github.com/user-attachments/assets/b6bbbd4d-5675-4f6c-a7ae-223b181ecb36" />


### arp

<img width="795" height="820" alt="image" src="https://github.com/user-attachments/assets/dcadab57-2c70-45aa-9426-b182c47d7f61" />


### systeminfo

<img width="968" height="942" alt="image" src="https://github.com/user-attachments/assets/6da396cd-f50c-488b-a624-5705a23d4c61" />


## Result
Thus Execution of Network commands Performed.
