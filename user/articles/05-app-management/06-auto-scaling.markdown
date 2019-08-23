---
header-id: auto-scaling
---

# Auto Scaling

Currently, this feature is only available for the Liferay service. Furthermore, 
the feature is only enabled for production type environments. Whether due to a 
traffic spike, memory leak, or some other issue, sometimes Liferay must be 
upscaled or downscaled to perform well. DXP Cloud's auto-scaling feature 
automatically creates and destroys instances of Liferay as needed to optimize 
performance. You therefore don't need to worry about doing so manually. 

## Enabling Auto Scaling

You can enable auto scaling via Liferay's _Scale_ tab. To do so, navigate to
_Services_ &rarr; _Liferay_ &rarr; _Scale_ and click _Enable Auto Scaling_. If
auto-scaling is enabled, you can click _Disable Auto Scaling_ to disable it.
With auto-scaling enabled, DXP Cloud monitors your service and scales it
automatically according to predefined thresholds.

![Figure 1: Enable or disable auto-scaling from your service's Scale tab.](../../images/auto-scaling.png)

## Downscaling Liferay

To downscale Liferay, scroll down on the Scale tab and click _Manual Downscale_.
This redirects you to a page where you can choose how many instances to remove.
Make your selection and click _Downscale Service_.

![Figure 2: You can downscale your service manually.](../../images/downscale-manual.png)
