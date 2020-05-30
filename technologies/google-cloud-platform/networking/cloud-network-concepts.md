# Network Core Concepts

## Global Private Network:
- Regions, Zones, Edge Points of Presence (Edge POP)    
    - Edge POP: connection points between Google's network and the internet.
    - Regions and Zones are connected to the same network. 
        - All traffic between nodes in different regions don't go through the internet

## Virtual Private Cloud
- Projects separate users, VPCs separate systems.
- A software defined network (SDN)
- Egress traffic costs, Ingress traffic is free
- Doesn't come with a CIDR range attached to it

## Subnets
- Define a CIDR range per subnet
- Can choose any ranges of subnets as long as they don't overlap
- Individual subnets are confined to a single region, but can be in different zones
- Subnet Modes:
    - Default: 
        - Auto Mode network with pre-made firewall rules
    - Auto Mode Network: 
        - Automatically creates a subnet for each region
        - Predefined IP ranges
    - Custom Mode Network
- Reserved IP Addresses:
    - First two and last two IP addresses in range reserved (e.g. 10.1.2.0/24)
        - 10.1.2.0 -> Network
        - 10.1.2.1 -> Default Gateway
        - 10.1.2.254 -> Future Use
        - 10.1.2.255 -> Broadcast
- Network class
    - Class A: 10.0.0.0/8, Class B: 172.16.0.0/12, Class C: 192.168.0.0/16 
- Address Ranges
    - Primary CIDR range
        - for instances
    - Secondary CIDR range
        - for alias IPs, e.g. containers

## IP Addresses
- Every instance has a private IP allocated by a DHCP server from the CIDR range
- It also has a DNS entry: `<instance-name>.c.<project-name>.internal`