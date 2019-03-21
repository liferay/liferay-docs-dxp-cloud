# Load Balancer Service (Nginx)

The Nginx load balancer functions as a gateway from the open Internet to your 
DXP Cloud services. It handles all traffic from your users and acts as a 
high-performance load balancer and web server. 

![Figure 1: The load balancer service is one of several services available in DXP Cloud.](../../images/services-nginx.png)

## Configurations

Although the stack of DXP Cloud services are fine-tuned to work well by default, 
you may need to configure Nginx further. To do this, you can include any CONF 
file inside the `config` folder. When you deploy your changes, the config file 
is automatically injected into your service and overwrites the default 
configuration. Here's an example folder structure of such a file inside the 
`config` folder: 

    loadbalancer
    ├── config
    │ └── nginx.conf
    └── wedeploy.json

## Scripts

You can use scripts for more extensive customizations. However, use caution when 
doing so. This is the most powerful way to customize the load balancer service 
and can cause undesired side effects. 

Any `.sh` files found in the `script` folder are run prior to starting your 
service. For example, to include a script that removes all log files, you could 
place it in the following directory structure: 

    loadbalancer
    ├── script
    │ └── remove-log-files.sh
    └── wedeploy.json
