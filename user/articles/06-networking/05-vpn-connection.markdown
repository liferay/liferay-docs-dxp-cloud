---
header-id: vpn-connection
---

# VPN Connection

You can use DXP Cloud's VPN feature to connect your DXP Cloud services to 
external services on private networks. For example, you may need to connect your 
DXP Cloud services to directories or applications that are only accessible on a 
company VPN. You'll learn how to do this here. 

## Connecting to a VPN

Follow these steps to connect your environment to a VPN: 

1.  Go to your environment's *Settings* tab. 

2.  Choose the type of VPN connection. Here are the supported types: 

    -   OpenVPN
    -   IPSec

3.  Fill in the VPN's required fields. 

4.  Click *Connect VPN*. 

To disconnect your service from a VPN after it's connected, click the 
*Disconnect* button. 

![Figure 1: You can connect to a VPN from the Settings tab.](../../images/vpn-connection.png)

## Port Configuration

Once connected to a VPN, you can choose which ports to forward requests to. 
Follow these steps to do so: 

1.  On the same page, click *Add VPN Port*. 

2.  Enter the local hostname and port for DXP Cloud. 

3.  Enter the forwarding hostname and port for the VPN. 

4.  Click *Add Port* when you're finished. 

To remove a port, click its *Actions* button 
(![Actions](../../images/icon-actions.png)) 
and select *Remove*. 

![Figure 2: You can also configure port forwarding.](../../images/vpn-ports.png)
