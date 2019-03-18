# Shell Access

Command-line tools are fundamental for developer experience and productivity
because they deliver speed, control, traceability, scripting and automation
capabilities to the developer’s workflow.

In many cases, it’s challenging to get full visibility and control in your
service. Shell access makes it easy to see what's going on inside your
application, look for side effects that would not be easily spotted in the logs
or even call functions like data population or report generation that are just
meant to be performed once.

## Accessing Shell via Web Console

You can access your shell via DXP Cloud Web Console. Go to your environment
page, click on *Services* tab on the left side menu, select which service you
want to have shell access, and click on the *Shell* tab of your service.

![Figure 1: The Backup service is one of several services available in DXP Cloud.](../../images/shell-web-console.png)

## Accessing Shell via CLI

The other way you can access your service's shell is via the CLI. To do that,
you have to run the command `we shell` and select which service you want to have
shell access. Once you select it, you can run any command that you want.

![Figure 2: You can also access the shell via the command line.](../../images/shell-cli.png)

If you already know which service and project you want to access, you can run
this command instead:

    we shell -p projectID -s serviceID

## Shell Limitations

The Shell is a great tool to troubleshoot or perform one-time actions on your
service but not intended for permanent changes. This is because when you deploy
or restart your service, all files that are not inside of a persistent Volume
will be replaced by the new build.

For the Shell, this means every command you run on your service is temporary and
will reset when you redeploy or restart your service unless you make the changes
within a Volume.
