---
header-id: auto-scaling
---

# Auto-scaling

Whether due to a traffic spike, memory leak, or some other issue, sometimes a 
service must be upscaled or downscaled to perform well. DXP Cloud's auto-scaling 
feature automatically creates and destroys instances of a service as needed to 
optimize performance. You therefore don't need to worry about doing so manually. 

A service can automatically upscale to 10 instances maximum, and downscale to 
the number specified for the `scale` property in `LCP.json`. The `scale` 
property specifies the minimum number of instances that can run for a given 
service.

| **Note:** Currently, this feature is only available for the Liferay DXP 
| service in production environments. 

## Enabling Auto-scaling

Follow these steps to enable or disable auto-scaling: 

1.  Navigate to *Services* &rarr; *Liferay* &rarr; *Scale* and click 
    *Enable Auto Scaling*. 

2.  If auto-scaling is disabled, click *Enable Auto Scaling* to enable it. If 
    auto-scaling is already enabled, click *Disable Auto Scaling* to disable it. 

With auto-scaling enabled, DXP Cloud monitors your service and scales it 
automatically according to predefined thresholds. 

![Figure 1: Enable or disable auto-scaling from your service's Scale tab.](../../images/auto-scaling.png)

## Specifying Target Average Utilization

*Target average utilization* represents a *percentage average* of memory and/or 
CPU usage. For example, if three service instances utilize 70%, 90%, and 95% of 
memory, respectively, then the average memory utilization is 85%. If the target 
average utilization is set to 90, then no upscaling is needed; upscaling in this 
situation only occurs when the average memory utilization exceeds the target. 
Remember that the total available memory is specified by the `memory` property 
in `LCP.json`, as referenced in 
[Configuration via LCP.json](/docs/-/knowledge_base/dxp-cloud/configuration-via-lcp-json). 

Specify the target average utilization in the `autoscale` property of the 
service's `LCP.json`: 

```json
"autoscale": {
    "cpu": 80,
    "memory": 90
}
```

If the `autoscale` property isn't set, the target average utilization defaults 
to 80 for both CPU and memory utilization. 
