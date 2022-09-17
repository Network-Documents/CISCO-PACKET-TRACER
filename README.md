# cisco
1. first set the topology 
2. in the karaj's switch CLI:

```
  enable
  configure terminal
  hostname sw-karaj
```

	
3. do the same for the router
4. connect the devices by straight through cable
5. set the rw-krj interface g0/0/0 ip to the last usable address :
```
	enable 
	conf t
	int g0/0/0
	ip address 192.168.10.254 255.255.255.0
	no shutdown
```
6.configure dhcp on router:
```
	enable
	conf t
	ip dhcp pool lan1
	network 192.168.10.0 255.255.255.0
	default-router 192.168.10.254
```	
7.on every pc's config set ipv4 to DHCP    
then you can see that every pc has an ip and a default gateway
![image](https://user-images.githubusercontent.com/98854412/190874470-815e17bb-108d-452b-95f8-887eb07039a5.png)

8.on the switch configs:
```
	spanning-tree vlan 1
	spanning-tree portfast default
```	
note:  vlan1 includes all interfaces

9.go to pc3 config and change dhcp to static:
	ip : 192.168.10.4
	def gateway : 192.168.10.254

10.on the global configuration of the switch and the router:
```	
	access-list 1 permit 192.168.10.4
	line vty 0 15
	access-class 1 in
```
read about it : https://www.certificationkits.com/cisco-certification/ccna-articles/cisco-ccna-access-lists/configuring-telnet-a-ssh-via-an-acces-list/  
&  
https://learningnetwork.cisco.com/s/question/0D53i00000Kt5qICAR/what-is-the-difference-between-line-vty-0-4-line-vty-0-15

11. setting the terminal time out:
```	
	enable
	conf t
	line console 0
	exec-timeout 1
```  
![image](https://user-images.githubusercontent.com/98854412/190874504-ef40fd3f-3520-4b94-abec-bfcfa44a63af.png)

 or  
 
```
	line vty 0 15
 	exec-timeout 1
```

more terminal conf:    https://www.cisco.com/c/en/us/td/docs/switches/datacenter/nexus1000/sw/4_2_1_s_v_1_4_a/getting_started/configuration/guide/n1000v_gsg/n1000v_gsg_7terminal.pdf


13.	connect karaj and zanjan routers by straight through cable , then on the karaj's router CLI :
```	
	en
	conf t
	int g0/0/1
	ip address 192.168.12.1 255.255.255.252
	no shut
```	
on zanjan's router CLI :
```	
	en
	conf t
	int g0/0
	ip address 192.168.12.2 255.255.255.252
	no shut
```
14. on karaj's router CLI:
```	
	en 
	conf t
	ip route 192.168.11.0 255.255.255.0 192.168.12.2
```	
15. on zanjan's router CLI :
```	
	en 
	conf t
	ip route 192.168.10.0 255.255.255.0 192.168.12.1
```	
16.repeat the same things on the zanjan LAN

17. ping pc4 from pc1 to check   
the first few tries might say timeout because of ARP

* * *
