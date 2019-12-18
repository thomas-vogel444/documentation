# Networking Cheatsheet

- iptables
- dns server
- Which process is listening on which port?
- testing connectivity

From Prints https://itsfoss.com/basic-linux-networking-commands/

## Connectivity

- `ping <host>`
    Sends a ICMP echo message to a host

- `telnet host <port>`
    Talk to hosts at the given port number, by default port 23

## Arp

Translates IP addresses into Ethernet aaddresses. Entries are cached and deleted every 20 minutes.
- `arp -a`
    Prints the arp table 
- `arp -s <ip_address> <mac_address> [pub]` 
    Adds an entry in the table
- `arp -a -d`
    Deletes all the entry  in the ARP table

## Routing

- `netstat -r`
    Prints routing table 
- `netstat -rnf inet`
    Prints routing table for IPV4
- `traceroute`
    Traces the route of an IP address

## Others

- `nslookup <domain_name>`
    Makes queries to the DNS server to translate IP to a name

## Important Files

- `/etc/hosts`
    Names to ip addresses
- `/etc/networks`
    Network names to ip addresses
- `/etc/protocols`
    Protocol names to protocol numbers
- `/etc/services`
    tcp/udp service names to port numbers

## Tools and network performance analysis

- `tcpdump -i -vvv`
    Tool to capture and analyze packets

## Switching

## VLAN

## UDP/TCP

## NAT/Firewall
