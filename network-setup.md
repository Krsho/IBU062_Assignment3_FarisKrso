# Network Setup

## Devices and IP Addresses

### Subnet 1: `168.90.0.0/24`
- **Switch0**: `2960-24TT`
- **PC0**: `168.90.0.2`
- **PC1**: `168.90.0.3`
- **PC3**: `168.90.0.6` 
- **Laptop0**: `168.90.0.4`
- **Server0**: `168.90.0.5`

### Subnet 2: `210.3.14.0/24`
- **Switch1**: `2960-24TT`
- **PC2**: `210.3.14.4`
- **PC4**: `210.3.14.5` 
- **Server1**: `210.3.14.3`
- **Server2**: `210.3.14.2`

## Router
- **Router1**: `SR4331`

# DHCP Configuration on Router

1. **Enter privileged EXEC mode:**
   enable

2. **Enter global configuration mode:**
   configure terminal

3. **Configure the first interface (GigabitEthernet0/0/0) for Subnet 1:**
   interface GigabitEthernet0/0/0
   ip address 168.90.0.1 255.255.0.0
   no shutdown
   exit

4. **Configure the second interface (GigabitEthernet0/0/1) for Subnet 2:**
   interface GigabitEthernet0/0/1
   ip address 210.3.14.1 255.255.255.0
   no shutdown
   exit

5. **Configure DHCP for Subnet 1 (168.90.0.0/24):**
   ip dhcp excluded-address 168.90.0.1
   ip dhcp pool FIRST_NETWORK
   network 168.90.0.0 255.255.0.0
   default-router 168.90.0.1
   exit

6. **Configure DHCP for Subnet 2 (210.3.14.0/24):**
   ip dhcp excluded-address 210.3.14.1
   ip dhcp pool SECOND_NETWORK
   network 210.3.14.0 255.255.255.0
   default-router 210.3.14.1
   exit

7. **Save the configuration:**
   write memory
