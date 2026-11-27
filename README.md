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


##program:

```

import socket
import subprocess
import re

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)

print("Server is waiting for connection...")

c, addr = s.accept()
print("Connected to:", addr)

while True:
    hostname = c.recv(1024).decode()

    if not hostname:
        break

    if hostname.lower() == "exit":
        break

    result = subprocess.run(
        ["ping", "-n", "4", hostname],
        capture_output=True,
        text=True
    )

    match = re.search(
        r"Minimum\s*=\s*(\d+)ms.*Maximum\s*=\s*(\d+)ms.*Average\s*=\s*(\d+)ms",
        result.stdout
    )

    if match:
        min_time, max_time, avg_time = match.groups()
        response = (
            f"Minimum: {min_time} ms\n"
            f"Average: {avg_time} ms\n"
            f"Maximum: {max_time} ms"
        )
    else:
        response = "Host Not Found or Ping Failed"

    c.send(response.encode())

c.close()
s.close()

```

client:

```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    ip = input("Enter the website you want to ping: ")

    if ip.lower() == 'exit':
        break

    s.send(ip.encode())

    result = s.recv(4096).decode()
    print("\nPing Statistics:")
    print(result)

s.close()

```




## Output



server:


<img width="636" height="380" alt="Screenshot 2026-11-27 091446" src="https://github.com/user-attachments/assets/fe6f8090-6b08-48ff-ab5e-fa7fb9bc079b" />


client:

<img width="666" height="487" alt="Screenshot 2026-11-27 091454" src="https://github.com/user-attachments/assets/3aa13703-6fbb-41c2-bde8-21c7ed5315d6" />






## Result
Thus Execution of Network commands Performed 
