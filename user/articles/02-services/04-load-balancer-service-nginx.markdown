# Load Balancer Service (Nginx)

The Nginx load balancer sits in front as a gateway from the open
internet to your services. It handles all traffic from your users and
acts as a high-performance load balancer and web server.

![Figure 1: The load balancer service is one of several services available in DXP Cloud.](../../images/services-nginx.png)

## Configurations

Even though we have fine-tuned the entire stack of services to work well out of
the box, you may need to configure your Nginx further. To do this, you can
include any `.conf` file inside the config folder. When you deploy your changes,
the config file will be automatically injected into your service and overwrite
the default configuration.

    loadbalancer
    ├── config
    │ └── nginx.conf
    └── wedeploy.json

## Scripts

For full customization, you can use the scripts extension points. This is the
most powerful and customizable functionality so be careful of what you are
running to avoid causing undesired side effects.

Any `.sh` files found in the `script` directory will be run prior to starting
your service. For example, if you wanted to include a script that removed all
log files, you could include something like this:

    loadbalancer
    ├── script
    │ └── remove-log-files.sh
    └── wedeploy.json
