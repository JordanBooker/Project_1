Domain: Cloud Security

Question 1: Cloud Access Control

How would you control access to a cloud network?
1. Restate the Problem

- How would I regulate whats interacts with the cloud network?

2. Provide a Concrete Example Scenario
 - In Project 1, did you deploy an on-premises or cloud network? 

_I deployed a cloud network_
 
- Did you have to configure access controls to this network?
_Yes_

 - What kinds of access controls did you configure, and why were they necessary?

_I created a security group and assigned an inbound security rule allowing ssh to port 22 from the Red Team virtual network. It was necessary for the DVWA VMs needs to gain access to ELK through port 22._

- How do these details relate to the interview question?
 
_They relate to the question because they show how access controls will protect the cloud by making sure that only authorized users can access critical files._

3. Explain the Solution Requirements
 - In Project 1, what kinds of access controls did you have to implement? Consider:
 
 - What did each access control achieve, and why was this restriction necessary for the project?

_I used the NSG’s for the ELK VNet and VMs. The firewalls were made in the NSG for the VNet. The NSGs created rules that allow or deny inbound network traffic. It was necessary for the project because it helped to connect to the correct port. Other firewalls were made in the NSGs helped to eliminate the unwanted network communications and this allowed the communication for the project._

4. Explain the Solution Details
 - Which rules do you set for each NSG in the network?

_I allowed inbound traffic to the load balancers by setting the source IP address to 10.1.0.4 and the destination to the virtual Network. The port was 80 and protocol, TCP. I allowed ssh from my personal IP to the virtual networks by setting the source IP address to 107.142.242.51 and the destination to virtual networks. The port was set to 22 and protocol set to any. I allowed internal ssh from the jumpbox by setting the source IP address to 10.1.0.4 and the destination to the virtual Network. The port was 22 and protocol set to any. I allowed Elk to be accessible by my PC by setting the source IP address to 107.142.242.51, the destination to the virtual network._

5. Identify Advantages/Disadvantages of the Solution
 - Does your solution scale?
 - How does access to the jump box work?

_I accessd the jump box by using ssh azadmin@10.1.0.4 and a private key_

 - How does access from the jump box to the web servers work?

_It works by using ssh and a private key with the webserver’s private address._

 - Is there a better solution than a jump box?
_Jump box is pretty good but it has its risks. If breached by a hacker could traverse organization’s networks and resources will be in danger. Switching to more dynamic methods such as zero trust security, in which all network traffic is untrusted by default can be a better solution._


 - What are the disadvantages of implementing a VPN that kept you from doing it this time?

_VPNs can slow your connection speed. You could be blocked from using certain services or websites. VPNs are illegal or tightly controlled in certain countries._

- What are the advantages of a VPN?

_Your traffic is encrypted and others cant see what you do online, nor interfere. VPNs require accommodation of protocols other than IPs_


- When is it appropriate to use a VPN?

_Employers may require the use of a VPN to access company services remotely, for security reasons. A VPN that connects to your server can give you access to internal company networks and resources when you're not in the office. It can do the same for your home network while you're gone_