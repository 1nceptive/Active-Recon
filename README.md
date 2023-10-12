<h1>Active Reconnisance</h1>


<h2>Key Outcomes Required</h2>

- <b>Identify Open Ports on target systems</b>
- <b>Analyse internal infrastructure of a organisation/network</b>
  

<h2>Websites & Tools used</h2>
<b>Mentioned in Order</b>

- <b>netcraft.com</b> 
- <b>dnsdumpster.com</b>
- <b>wafw00f</b>
- <b>sublist3r</b>
- <b>theHarvester</b>
- <b>haveibeenpwned.com</b>

<h2>Environments Used </h2>

- <b>Kali Linux</b> 

<h2>Cheatsheet Walkthrough</h2>


 We will find some more subdomains, DNS info but this time with active recon tools.
1. ***TERMINAL***
   **Automatic Zone Transfer to enumerate DNS records and subdomains:**
   - Using `dnsenum`: dnsenum runs everything without control/ performs automatic zonetransfer.
     ```
     dnsenum zonetransfer.me
     ```
   - Alternatively using `dig`: more controlled unlike dnsenum/ axfr is tag for zonetransfer/ @nsztm1.digi.ninja is a DNS Server
     ```
     dig axfr @nsztm1.digi.ninja zonetransfer.me
     ```

2. ***TERMINAL***
   **Bruteforce DNS:**
   - Using `fierce`:
     ```
     fierce -dns zonetransfer.me
     ```

ASSUMING YOU HAVE GAINED ACCESS TO INTERNAL NETWORK

3. ***TERMINAL***
   **Discover all devices on the network (host discovery):**
   - Find your current eth0 IP address:
     ```
     ip a s
     ```
   - Using `nmap` for host discovery:
     ```
     sudo nmap -sn 192.168.2.0/24
     ```
   - Alternatively, using `netdiscover`:
     ```
     sudo apt-get install netdiscover -y
     sudo netdiscover -i eth0 -r 192.168.2.0/24
     ```

4. ***TERMINAL***
   **Find open ports with nmap:**
   - Scan most common 1000 ports:
     ```
     nmap 10.4.19.218
     ```
   - Scan all 60,000 ports:
     ```
     nmap -p- 10.4.19.218
     ```
   - UDP PORT SCAN:
     ```
     nmap -Pn -sU 10.4.19.218
     ```

5. ***TERMINAL***
   **Find Services Running on open ports:**
   - Scan open ports for service information:
     ```
     nmap -Pn -F -sV -O -sC 10.4.19.218 -v
     ```
     - `-F`: Fast scan
     - `-sV`: Service version
     - `-Pn`: Windows targets blocking
     - `-O`: Operating system
     - `-sC`: Scripts run on ports for more info
     - `-v`: Shows output while scanning

   **Output Nmap scan results into a file:**




<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
