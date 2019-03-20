# Health Checks and Zero-downtime Deployments

Health Checks are primarily useful for two things: validating deployment success 
and enabling accurate service self-healing. 

## Validating Deployment Success

When deploying a service, our default behavior is to make sure the container in
the background of your service is up and running. At that point, we will say
your deployment was successful. In many cases, this is not enough to truly
validate if the deployment was complete and ready.

To add custom checks, you can use our Health Check feature to specify a custom
URL or command to check before declaring your service is healthy.

## Accurate Service Self Healing

Once your service has successfully deployed, it is important that you always
know it's health status. We are always running a health check on your service
and if we notice the health check fail then we will replace your service with a
new one.

This is a powerful self-healing feature, but unless you have accurate Health
Checks, we may not know that your service needs to be replaced.

To add custom checks, you can use our Health Check feature to specify a custom
URL or command to check before declaring your service is healthy.

## Custom health Checks

### Checking with URL

If you provide a URL, we will ping that address until we get a `200` response.

Here is an example of the URL approach:

    {
     "id": "dxp",
     "healthCheck": {
      "url": "localhost"
     }
    }

By putting `localhost` as the health check URL, we will ping the IP of your
service. You could also specify a specific path like `localhostcompany.com/blog`
or a certain port like `localhost:4000`.

### Checking With Command

For more complex health checks, you can add commands to check the uptime of your
service.

    {
     "id": "db",
     "healthCheck": {
      "command": "curl -X GET --silent --fail 'localhost'"
     }
    }

With both of these approaches, we provide you with other customizable
configurations:

-   `interval`: How many seconds should pass between health check tries. The 
    default value is `30`.
-   `timeout`: How long we will wait for your service to answer. The default 
    value is `30`.
-   `startPeriod`: How many seconds the `healthCheck` should wait before 
    testing. The default value is `0`. 
-   `retries`: How many times the `healthCheck` will retry before declaring your 
    service as `unhealthy`. The default value is `3`.

Usage example:

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

## Zero Downtime Deployments

Configuring a service to have zero downtime means that it will have 100%
of uptime during new deployments. By default, all services have this
configuration as `true`. If you want to turn it off, you can set it to
`false` in your `wedeploy.json`.

    {
      "id": "dxp",
      "zeroDowntime": false
    }

## Using Health Checks with Zero Downtime Deployments

We saw that when adding a `healthCheck` to your service, it means that we are
going to check your service until we receive a 200 response code. This is used
to define the health of a service. 

When you set `zeroDowntime` as `true` (default), it means that any time you
redeploy your service, a new instance is deployed and your current service keeps
running. When the new instance is determined to be `healthy` by the health
check, we replace the older service instance with the newer one. 

On the other hand, when we configure `zeroDowntime` to `false`, it means that
your current instance will be down during the deployment process. Once the new
instance is determined to be `healthy`, the service will be up again. 
