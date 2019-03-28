# Application Metrics

With DXP Cloud's built-in monitoring, you can track the following information 
about your service: 

-   CPU usage
-   Memory usage
-   Transfer data
-   Health

To view this information, select your environment's *Monitoring* tab. Data is 
displayed for the past 30 days. You can also select the service, metric, and 
time period to display data for. 

![Figure 1: You can use DXP Cloud to monitor your services.](../../images/monitoring.png)

## Understanding Service Health

Your service's status can be listed as any of the following: 

**None:** This is the status during the build process.

**Healthy:** The service has passed a 
[health check](https://help.liferay.com/hc/en-us/articles/360013442951-Health-Checks-and-Zero-Downtime-Deployments). 

**Unhealthy:** The service has failed a health check. 

Note that sometimes your application might have usage peaks that can hit 
resource limits and make your service unhealthy. If this occurs, check your 
service's logs and metrics for the time period in question. 

## Advanced Application Metrics

To conduct deeper and more advanced monitoring, click the *Advanced* tab to 
access your Dynatrace dashboard. There you can check things like log trails, and 
create custom dashboards. 
