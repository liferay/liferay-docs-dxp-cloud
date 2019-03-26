# Health Checks and Zero-downtime Deployments

Health Checks are primarily useful for validating deployment success and 
enabling accurate service self-healing. 

## Validating Deployment Success

When deploying a service, DXP Cloud's default behavior is to make sure the 
container in your service's background is up and running. At that point, DXP 
Cloud considers your deployment successful. In many cases, however, this isn't 
enough to truly determine if the deployment is complete and ready. To add custom 
checks, use DXP Cloud's Health Check feature to specify a custom URL or command 
to check before declaring your service is healthy. For more information, see 
[Custom Health Checks](#custom-health-checks). 

## Accurate Service Self Healing

Once your service is successfully deployed, it's important that you always know 
its health status. DXP Cloud constantly checks your service's health. If a 
health check fails, DXP Cloud replaces your service with a new one. This 
self-healing feature also works with custom health checks, which are discussed 
next. 

## Custom Health Checks

To perform a custom health check, you must specify it via the `healthCheck` 
property in `wedeploy.json`. The following sections show you how to do this for 
a URL and a command.

### Checking with a URL

To perform a custom health check with a URL, set the `url` property to the URL. 
To perform the check, DXP Cloud pings that address until receiving a `200` 
response.

This example sets `url` to `localhost`:

    {
      "id": "dxp",
      "healthCheck": {
        "url": "localhost"
      }
    }

With `localhost` as the health check's URL, DXP Cloud pings your service's IP 
address. Note, however, that you can use any URL here. For example, you could 
specify a path like `localhostcompany.com/blog` or a specific port like 
`localhost:4000`. 

### Checking with a Command

For more complex health checks, you can add commands via the `command` property. 
Here's an example:

    {
      "id": "db",
      "healthCheck": {
        "command": "curl -X GET --silent --fail 'localhost'"
      }
    }

### Additional Properties

You can use additional properties to customize both the `url` and `command` 
health checks. Here's a list of these properties: 

-   `interval`: The number of seconds that pass between health checks. The 
    default value is `30`.
-   `timeout`: The number of seconds DXP Cloud waits for your service to answer. 
    The default value is `30`. 
-   `startPeriod`: The number of seconds the `healthCheck` should wait before 
    testing. The default value is `0`. 
-   `retries`: The number times the `healthCheck` will retry before declaring 
    your service unhealthy. The default value is `3`. 

For example: 

    {
      "id": "db",
      "healthCheck": {
        "command": "curl -X GET --silent --fail 'localhost'",
        "interval": 5,
        "timeout": 5,
        "startPeriod": 1,
        "retries": 10
      }
    }

## Zero-downtime Deployments

Configuring a service to have zero downtime means that it will have 100% uptime 
during new deployments. Zero-downtime deployments are enabled by default. If you 
want to turn this off, set the `zeroDowntime` property in your `wedeploy.json` 
to `false`: 

    {
      "id": "dxp",
      "zeroDowntime": false
    }

## Using Health Checks with Zero-downtime Deployments

When you combine health checks with zero-downtime deployments, a health check 
first determines if the new service is healthy. If it is, then the new service 
instance is deployed and replaces the old one. 

If zero-downtime deployments are off, the current service instance is down 
while a health check ensures that the new service instance is healthy. If the 
new service is healthy, deployment completes and the service is up again. 
