---
header-id: log-management
---

# Log Management

Logs are crucial for debugging. On DXP Cloud, you can access your environment's 
logs via the web console or terminal. You can also download log files. 

## Accessing Logs from the Web Console

The easiest way to access an environment's logs is via the web console. To do 
so, select the environment and click the *Logs* tab in the left menu. To access 
a specific service's logs, select the service from the *All Services* menu in 
the toolbar. To download the logs, click *Download Logs*. 

![Figure 1: The web console also lets you view your logs.](../../images/logs-web-console.png)

## Accessing Logs from the Terminal

You can also access logs from your terminal by running this command: 

```shell
lcp log
```

This lists all your services so that you can choose the one whose logs to 
access. To access logs from a specific environment you can enter its ID or run 
the command with that ID: 

```shell
lcp log -p myenvironmentid
```

You can also specify the service as part of the command: 

```shell
lcp log -p myenvironmentid -s myserviceid
```
