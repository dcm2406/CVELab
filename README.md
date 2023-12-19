
# CVE-2023-46604 Lab
This lab guides on exploiting vulnerabilities of CVE-2023-46604
## Acknowledgements
 - [Apache ActiveMQ](https://activemq.apache.org/code-overview)
 - [CVE-2023-46604](https://nvd.nist.gov/vuln/detail/CVE-2023-46604)
## Requires
This lab requires the installation of 2 virtual machines. One Kali Linux machine version 2023.4 and one Ubuntu machine version 22.04.3 LTS. You can download them here:
- [Kali Linux 2023.4](https://kali.download/base-images/kali-2023.4/kali-linux-2023.4-vmware-amd64.7z)
- [Ubuntu 22.04.3 LTS](https://releases.ubuntu.com/22.04.3/ubuntu-22.04.3-desktop-amd64.iso)
- [VMware-workstation-17.5.0 for windows](https://download3.vmware.com/software/WKST-1750-WIN/VMware-workstation-full-17.5.0-22583795.exe)
- [VMware-workstation-17.5.0 for linux](https://download3.vmware.com/software/WKST-1750-LX/VMware-Workstation-Full-17.5.0-22583795.x86_64.bundle)
- [Key active VMWare 17 pro](https://gist.github.com/PurpleVibe32/30a802c3c8ec902e1487024cdea26251)
## Documentation

[Documentation](https://linktodocumentation)


## CVE-2023-46604 Exploiting

Model and system requirements
![](https://github.com/dcm2406/CVELab/blob/master/Model%20CVE-2023-46604.png)

On Kali Linux machine:
- Installed git
```command
sudo apt install git
```
- Installed gedit
```command
sudo apt install gedit
```
- Installed python (already available on kali linux)
- Installed Netcat (already available on kali linux)

On Ubuntu machine:
- Installed git
```command
sudo apt install git
```
- Installed openjdk 18
```command
sudo apt install opẹndk-18-jdk
```
- Installed ActiveMQ 5.18.2 package
```command
sudo su
git clone https://github.com/dcm2406/ApacheActiveMQ
cd ApacheActiveMQ/
tar -xf apache-activemq-5.18.2-bin.tar.gz
```
## Support

For support, email dcm240602@gmail.com or txc3000@gmail.com


## Authors

- [@dcm2406](https://github.com/dcm2406)
- [@txc3000](https://github.com/txc3000)

