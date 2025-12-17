# Network-Segmentation-VLAN-Configuration

## Objective
Configure pfSense with VLANs, set up firewall rules for controlled inter-VLAN communication, and provide internet access for isolated subnets while allowing selective traffic flow between VMs.

## Skills Learned
- Configuring VLANs and managing subnets in pfSense
- Creating and testing firewall rules for inter-VLAN communication
- Troubleshooting network connectivity and NAT issues
- Understanding DHCP assignment per VLAN and IP management
- Enhancing hands-on experience with Linux (Ubuntu, Kali) networking and security testing

## Tools Used
- Proxmox VE for virtualization
- pfSense for firewall and VLAN management
- Ubuntu for network testing and connectivity verification
- Kali Linux for security testing and VLAN isolation verification

## Steps

1. **Set Up Virtual Machines**
   - Created three VMs: Ubuntu (VLAN 20), Kali Linux (VLAN 40), and pfSense (firewall/router)
   - ![VM Setup](./screenshots/vm-setup.png)  
     *Ref 1: Virtual Machines created in Proxmox*

2. **Configure Network Interfaces on pfSense**
   - Assigned LAN and WAN interfaces
   - Created VLAN 20 (Ubuntu) and VLAN 40 (Kali) on LAN interface
   - ![pfSense VLAN Setup](./screenshots/pfsense-vlans.png)  
     *Ref 2: VLANs configured in pfSense*

3. **Configure DHCP for VLANs**
   - VLAN 20: 192.168.20.10–192.168.20.150
   - VLAN 40: 192.168.40.10–192.168.40.150
   - *Third octet identifies VLAN for easy management*
   - ![DHCP Configuration](./screenshots/dhcp-setup.png)  
     *Ref 3: DHCP ranges assigned per VLAN*

4. **Assign VLANs to Interfaces**
   - Ubuntu VM → VLAN 20
   - Kali VM → VLAN 40

5. **Set Up Firewall Rules**
   - Allowed VLAN 20 → VLAN 40 (Ubuntu can access Kali)
   - Blocked VLAN 40 → VLAN 20 (Kali cannot access Ubuntu)
   - ![Firewall Rules](./screenshots/firewall-rules.png)  
     *Ref 4: pfSense firewall rules applied*

6. **Test Connectivity**
   - Ubuntu VM can ping Kali VM 
   - Kali VM cannot ping Ubuntu VM 
   - Verified internet access for both VLANs
   - ![Ping Test](./screenshots/ping-test.png)  
     *Ref 5: Connectivity tests*

7. **Refinement**
   - Adjusted rules for proper routing and NAT
   - Verified isolation and selective access

## Outcome
- VLANs configured successfully with proper isolation and internet access
- Traffic flows as expected: Ubuntu → Kali allowed, Kali → Ubuntu blocked

## Challenges
- Intially forgot to enable routing between VLANs, routing, and firewall rule creation in pfSense.
- Encountered issues with pfSense's default rules blocking traffic that needed to be manually adjusted.
