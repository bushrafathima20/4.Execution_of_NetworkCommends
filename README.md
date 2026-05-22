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

## Program
## Client.py:
```
import socket
s = socket.socket()
try:
    s.connect(('localhost', 8000))
    print("Connected to server.")
    print("Type commands or 'exit' to quit.\n")
    while True:
        cmd = input("Enter command: ").strip()
        if not cmd:
            continue
        s.send(cmd.encode())
        if cmd.lower() == 'exit':
            print("Closing connection...")
            break
        data = b""
        while True:
            part = s.recv(4096)
            data += part
            if len(part) < 4096:
                break
        print("\n----- RESULT -----")
        print(data.decode())
        print("------------------\n")
except ConnectionRefusedError:
    print("Server is not running!")
finally:
    s.close()
```
## Server.py:
```
import socket
import subprocess
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
        completed = subprocess.run(
            command,
            capture_output=True,
            text=True,
            shell=True
        )
        output = completed.stdout + completed.stderr
        if not output:
            output = "Command executed successfully."
    except Exception as e:
        output = f"Command failed: {e}"
    c.sendall(output.encode())
c.close()
s.close()
```
## Output
## Client.py:
<img width="828" height="1085" alt="image" src="https://github.com/user-attachments/assets/b67c884a-01c1-4513-b175-7718dcb94040" />
<img width="1401" height="188" alt="image" src="https://github.com/user-attachments/assets/084ce060-ccf0-4629-816b-ebb2fe553c32" />
## Server.py:
<img width="754" height="1039" alt="image" src="https://github.com/user-attachments/assets/5b0facb6-2dab-4825-872e-ad3638aba141" />
<img width="1381" height="168" alt="WhatsApp Image 2026-05-22 at 1 28 40 PM" src="https://github.com/user-attachments/assets/b7754ff1-0040-4ef7-b9aa-f424bc3719b8" />
## Developed By: BUSHRA FATHIMA I
## Register Number: 212225040051
## Result
Thus Execution of Network commands Performed 
