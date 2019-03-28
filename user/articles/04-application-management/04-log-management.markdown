# Log Management [](id=log-management)

Checking logs is crucial for debugging. On DXP Cloud, you can access your 
environment's logs via the web console or terminal. You can also download the 
log file. 

## Accessing Logs from the Web Console [](id=accessing-logs-from-the-web-console)

The easiest way to access an environment's logs is via the Web Console. To do 
so, select the environment and click the *Logs* tab in the left menu. To access 
a specific service's logs, select the service from the *All Services* menu in 
the toolbar. To download the logs, click the *Download Logs* button. 

![Figure 1: The web console also lets you view your logs.](../../images/logs-web-console.png)

## Accessing Logs from the Terminal [](id=accessing-logs-from-the-terminal)

You can also access logs from your terminal by running this command: 

    we log

This lists all your services so that you can choose the one whose logs to 
access. To access logs from a specific environment you can enter its ID or run 
the command with that ID:

    we log -p myenvironmentid

You can also specify the service as part of the command: 

    we log -p myenvironmentid -s myserviceid 
