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

You can enable auto-scaling for Liferay DXP via its *Scale* tab. Navigate to 
*Services* &rarr; *Liferay* &rarr; *Scale* and click *Enable Auto Scaling*. If 
auto-scaling is enabled, you can click *Disable Auto Scaling* to disable it. 
With auto-scaling enabled, DXP Cloud monitors your service and scales it 
automatically according to predefined thresholds. 

![Figure 1: Enable or disable auto-scaling from your service's Scale tab.](../../images/auto-scaling.png)

## Specifying Target Average Utilization

To specify the target average utilization, add the following to `LCP.json`: 

```json
"autoscale": {
    "cpu": 80,
    "memory": 90
}
```

If the `autoscale` property is not used, the target average utilization defaults 
to 80 for both CPU and memory utilization. 

So what does target average utilization mean? Here is a brief explanation: 

*Target average utilization* represents a *percentage average*. So for 3 
instances of a service with memory utilization at 70%, 90%, and 95%, the average 
memory utilization would be 85%. Since 85 is below 90, no upscaling is needed. 
Remember that the total available memory is specified by the `memory` property 
in `LCP.json`, as referenced in 
[Configuration via LCP.json](/docs/-/knowledge_base/dxp-cloud/configuration-via-lcp-json). 

For a more in-depth look at the algorithm used to dynamically upscale and 
downscale, please refer to 
[Kubernetes auto-scaling algorithm](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/#algorithm-details). 
