<h1>HaProxy</h1>


<h2>Description</h2>
In this lab we used HaProxy to facilitate load balancing and failover for a simple web server scenario. For this lab I used three VM's one to act as the the Haproxy host and the others running a simple LAMP web server.


<h2>Languages and Utilities Used</h2>

- <b>HaProxy</b>

<h2>Environments Used </h2>

- <b>Ubuntu Server</b> (22.04.1)

<h2>Process:</h2>

<br /><p align="left">
<br/>
<img src="https://i.imgur.com/rWYU9v9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
*Default landing page the Apache server.*<br/>

Installing HaProxy:  <br/>
  - apt-get install haproxy
  - enable HaProxy by default by modifying the /etc/default/haproxy file
  - sudo nano /etc/default/haproxy
  - add “ENABLED=1” to the end of the file
  - confirm that haproxy is running with service haproxy
<br />
<img src="https://i.imgur.com/ErrzWs3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br/>

 Configure HaProxy: <br/>
  -	copy the current configuration file as a backup <br/>
    o	sudo cp /etc/haproxy/haproxy.cfg haproxy.cfg.bak<br/>
  -	modify the config file<br/>
    o	sudo nano /etc/haproxy/haproxy.cfg<br/>
  -	add the following to the end of the files<br/><br/>
frontend http_front<br/> <br/>
     bind *:80<br/>
     stats uri /haproxy?stats<br/>
     default_backend http_back<br/><br/>
backend http_back<br/><br/>
      balance roundrobin<br/>
      server lamp1 10.59.5.32:80 check<br/>

Start haproxy service: <br/>
   -  Service haproxy start
<br />


Open a internet browser and connect to HaProxy server IP address.  <br/>
<img src="https://i.imgur.com/G1BFJrM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br/>

*Default apache web page reached through the HaProxy server.*

<br/>
<img src="https://i.imgur.com/NuOzSAM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br/>

*HaProxy stats page.* 

<br/><br/>

<img src="https://i.imgur.com/rM3fElQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br/>


*HaProxy config file.*

<br/><br/>
 Add a second server to HaProxy: <br/>
   -  Edit HaProxy config and add: <br/>
     - server lamp2 10.59.5.60:80 check <br/>
  -  Restart HaProxy <br/>
    - service haproxy restart <br/> <br/>
    
Shut down server 1. Open a web browser and connect to the IP address of the HaProxy server. <br/>

<img src="https://i.imgur.com/prHekh9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br/>


*Default webpage of web server 2 accessed when server 1 is unavailable.*

<br/><br/>

<img src="https://i.imgur.com/53MwuYS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br/>


*HaProxy stats page*

<br/><br/>

<img src="https://i.imgur.com/ApJyYka.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br/>


*Final HaProxy Config File*
<br/>
<br/>
That's how you use HaProxy to implement load balancing and failover in a Linux environment.



</p>


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
