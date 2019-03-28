# VPN Connection

DXP Cloud's VPN feature is an advanced way to connect your DXP Cloud services to
external services that have their own private network. This is especially useful 
when you need to connect your DXP Cloud services to things like databases or 
applications that are only accessible inside a company VPN. 

## Connecting to a VPN

To connect your environment to a VPN, first go to your environment's *Settings* 
tab. Then fill in the required fields for the VPN and click *Connect VPN*. To 
disconnect your service from a VPN, click the *Disconnect* button. 

![Figure 1: You can connect to a VPN from the Settings tab.](../../images/vpn.png)

## Adding Port Configuration

Once you have connected to a VPN, you can also choose which ports to forward 
requests to. On the same page, click *Add VPN Port*, then enter the local 
hostname and port for DXP Cloud, and the forwarding hostname and port for the 
VPN. Click *Add Port* when you're finished. To remove a port, click its 
*Actions* button and select *Remove*. 

![Figure 1: You can also configure port forwarding.](../../images/vpn-port-config.png)

![Figure 1: Remove a port via the Actions button.](../../images/vpn-port-remove.png)
