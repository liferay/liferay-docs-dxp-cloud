# Auto Scaling

Whether you are experiencing a traffic spike or a memory leak, sometimes your
services need to have more resources to perform well. Our Auto Scaling feature
allows your services to automatically allocate more resources when needed. This
way, you do not need to worry about fitting exactly the required resources for
each service or reacting soon enough to events. Just enable Auto Scaling and we
do everything for you.

## Enabling Auto Scaling

You can easily enable auto scaling via your service's *Scale* tab. When Auto
Scaling is enabled, we will monitor your service in real-time and scale it
automatically when it reaches pre-defined thresholds. 

![Figure 1: Enable auto scaling from the Scale tab.](../../images/auto-scaling-enable.png)

## Downscaling Services

If you want to downscale a service, you can scroll down on the same page and
click on *Manual Downscale*. You will be redirected to a page for you to choose 
how many scales you want to remove. Then, once you have chosen it, you can click 
*Downscale Service* and it will be downscaled to use fewer resources. 

![Figure 2: You can also downscale your service.](../../images/auto-scaling-downscale.png)
