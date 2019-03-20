# Application Metrics Overview

Our built-in monitoring allows you to keep track of the CPU, Memory, Transfer,
and Health of your services for the past 30 days.

You can view the monitor metrics of your services by going to the Monitoring tab
of your environment. Then you can select the service, metric and time period you
would like to review.

![Figure 1: You can use DXP Cloud to monitor your services.](../../images/monitoring.png)

## Understanding Service Health

The service status can be none, healthy, and unhealthy. Each status represents a
state of your service. During your build process, its status will be `none`. We
will run the 
[health check](https://help.liferay.com/hc/en-us/articles/360013442951/preview/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpZCI6MzYwMDEzNDQyOTUxLCJleHAiOjE1Mzc4OTgyMDF9.ZuY-2KAq0EF5yDN5XN1emXJRq_UvbB1nlFTQBezGDkU)
until receiving a `200` status code and then your service health will be 
`healthy`. If any other code is returned, your service health will be 
`unhealthy`.

**Tip:** Sometimes your application might have peaks of usage that can reach the
*limit of your resources and make your service unhealthy. When this happens,
*check your services logs and its metrics based on the period when it occurred.

## Advanced Application Metrics

To conduct deeper and more advanced monitoring, you can go to the *Advanced* tab
which will lead you to your Dynatrace dashboard. There you can check things like
log trails and create custom dashboards. 
