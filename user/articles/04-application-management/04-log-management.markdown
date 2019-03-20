# Log Management

One of the most efficient ways of debugging your application is checking its
logs. On DXP Cloud, you can access your environment's logs via the Web Console,
CLI, or downloading the log file.

## Accessing Logs from Web Console

The easiest way of accessing an environment's logs is via the Web Console. To do
that, you can select which environment you want to access and click on the
*Logs* tab on the left-side menu. To access logs of a specific service, select 
the service from the selector menu in the toolbar. To download the logs, click 
the *Download Logs* button in the toolbar. 

![Figure 1: The web console also lets you view your logs.](../../images/logs-web-console.png)

## Accessing Logs from the CLI

Another way of accessing logs is via your CLI. You can access it by running the
following command on your terminal:

    we log

It will list all your services so that you can choose the one you want to access
the logs. If you want to access logs from a specific environment you can type
its id or run the command containing the ID of your environment:

    we log -p myenvironmentid

The same is for specifying a service:

    we log -p myenvironmentid -s myserviceid 
