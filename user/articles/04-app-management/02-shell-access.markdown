# Shell Access

The command-line tools in DXP Cloud contribute to the developer's workflow by
delivering speed, control, traceability, scripting, and automation capabilities.
Shell access makes it simpler to see what's going on inside your application.
For example, you can use shell access to look for side effects not easily
spotted in the logs. You can also call functions for data population or report
generation that are meant to be performed once.

## Accessing the Shell via the Web Console

You can access the shell via the DXP Cloud web console. Go to your environment
page, click Services in the menu on the left, select the service you want to
access, and click the Shell tab.

![Figure 1: You can access the shell via DXP Cloud's web console.](../../images/shell-web-console.png)

## Accessing the Shell via a Terminal

You can also access your service's shell via a terminal. After 
[installing the Liferay Cloud command line tool](https://help.liferay.com/hc/en-us/articles/360028252951), 
run the command `lcp shell` and select the service to access. Once you select 
it, you can run any command that you want. 

![Figure 2: You can also access the shell via the command line..](../../images/lcp-shell.png)

If you already know which service and project you want to access, you can run
this command instead:

```shell
lcp shell -p projectID -s serviceID
```

## Shell Limitations

The shell is a great tool to troubleshoot or perform one-time actions on your
service, but it's not intended for permanent changes. This is because when you
deploy or restart your service, all files not in a persistent volume are
replaced by the new build. For the shell, this means every command you run on
your service is temporary and will reset when you redeploy or restart your
service, unless you make the changes within a volume. 
