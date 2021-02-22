# Ch.11 Managing Network Connections
 - commands with network interface cards(NICs) such as *ethtool, mii-tool, ifconfig*
 - configuring wired and wireless Ethernet connections
 - *netstat, dig, ip, ping* for getting information about my network

 ## Configuring Networks from the GUI
 - DHCP server can assign IP address to computer's network inteface
 - assign a default gateway, DNS server, and a hostname
 - NetworkManager app manages network interfaces

 ## Managing Network Interface Cards
 - Steps to go to troubleshoot internet problem
	> 1. veryfiy NIC is properly installed and the cable is connected to your network
    > 2. after cable is connected, check if you have a link with no speed or duplex mismatches
	> 3. make sure that cable is firmly seated in the NIC
 *mii-tool , ethtool*: can check my link, and set speed and duplex
 ![image.png](attachment:image.png)
 ![image-2.png](attachment:image-2.png)
 
 - can change NIC with **sudo ethtool -s eth0 speed 100 duplex full autoneg off**
 - but change will be lost when you reboot
 - following are steps to not loose the setting
     > 1. create a script in the */etc/init.d* directory
     > 2. Insert the following textD
     > ![image-3.png](attachment:image-3.png)
     > 3. insert specific settings at *ETHTOOL_OPTS*
     > 4. Set up the script as an executable file
     > 5. Set up the symbolic links to run new script under different runlevels
     > 6. run **sudo /etc/init.d/eth_options start**
 - for older NICs use **mii-tool**
 > ![image-4.png](attachment:image-4.png)]
 - *netstat* command provides network interface statistics
 > ![image-5.png](attachment:image-5.png)
 
 ## Managing Network Connections
 ### Starting and Stopping Ethernet Connections
 - restart network manger : **sudo service network-manager restart**
 - **ifconfig**: check network interface status
 > ![image-6.png](attachment:image-6.png)
 ### Viewing Ethernet Connection Information
 > ![image-7.png](attachment:image-7.png)
 > ![image-8.png](attachment:image-8.png)
 > ![image-9.png](attachment:image-9.png)
 

## Using Wireless Connections
- get help determining exactly what wireless card you have
 > **dmesg | grep -i wireless**
 ![image-13.png](attachment:image-13.png)
- no wireless card in my case
- wireless interfaces may be named wlanX or ethX
- can get more information with following commands
>  **ip link set eth1 up** or
>  **iwconfig eth1**

## Checking Name Resolution
- Ubuntu provides several tools for looking up information related to DNS name resolution
- */etc/resolv.conf* file stores DNS server information
> ![image-14.png](attachment:image-14.png)
- *dig* command can be used to look up information from a DNS server
- *host* : used to look up address information for a hostname or domain name
> ![image-15.png](attachment:image-15.png)
> ![image-16.png](attachment:image-16.png)
> ![image-17.png](attachment:image-17.png)
> ![image-18.png](attachment:image-18.png)
- can do a reverse lookup to find DNS information based on an IP address

## Troubleshooting Network Problems
### Checking Connectivity to a Host
- **ip route** : check my default gateway in the actual routing table
>![image-19.png](attachment:image-19.png)
- other options for ping
> ![image-20.png](attachment:image-20.png)
### Checking Address Resolution Protocol
- if not able to ping, there may be an issue at the Ethernet MAC layer
- Address Resolution Protocol(ARP) shows MAC layer information
> ![image-21.png](attachment:image-21.png)
- *arping* : to query a subnet to see if an IP is already in use
- arping continuously queries for the address until ctrl+c
### Tracing Routes to Hosts
- use *traceroute*to find the bottleneck or point of failure
> ![image-22.png](attachment:image-22.png)
- lines with * are caused by firewalls that block traffic to the target
> **traceroute -I boost.turbosphere.com**: Use ICMP packets to trace a route
> **traceroute -p 25 boost.turbosphere.com**: Connect to port 25 in trace
> **traceroute -n boost.turbosphere.com**: Disable name resolution in trace
> **tracepath boost.turbosphere.com**: Use UDP to trace the route
- *route* to view and manipulate the kernel's routing table (or *ip route*)
> ![image-23.png](attachment:image-23.png)

### Displaying netstat Connections and Statistics
- *netstat* to display information about packets sent between transport-layer protocols and ICMP
> ![image-24.png](attachment:image-24.png)


### Other Useful Network Tools
- *tcpdump*: to see header information about packets
- *wireshark* : to dig deeper into packet-level traffic
- *nmap* : to explore networks and remote machines and see what services they offer


```python

```
