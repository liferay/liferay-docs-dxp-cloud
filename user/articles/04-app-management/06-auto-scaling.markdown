# Auto Scaling

Whether due to a traffic spike, memory leak, or some other issue, sometimes your
services must be upscaled or downscaled to perform well. DXP Cloud's
auto-scaling feature automatically creates and destroys instances of your
service as needed to optimize performance. You therefore don't need to worry
about doing so manually. 

## Enabling Auto Scaling

You can enable auto scaling via your service's *Scale* tab. Navigate to 
*Services* &rarr; *Scale*, and click *Enable Auto Scaling*. With auto-scaling 
enabled, DXP Cloud monitors your service and scales it automatically according 
to predefined thresholds. 

![Figure 1: Enable auto-scaling from the Scale tab.](../../images/auto-scaling.png)

## Downscaling Services

To downscale a service, scroll down the Scale tab and click *Manual Downscale*.
This redirects you to a page for you to choose how many service instances you
want to remove. Make your selection and click *Downscale Service*. 

![Figure 2: You can downscale your service manually.](../../images/downscale-manual.png)
