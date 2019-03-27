# Command Line Tool

DXP Cloud's command line interface (CLI) is a tool that helps you use and manage 
DXP Cloud. For example, you can use the CLI to create, manage, and scale 
applications. Here, you'll learn how to install and use the CLI: 

-   [Installing the DXP Cloud CLI](#installing-the-dxp-cloud-cli)
-   [Changing the CLI Remote](#changing-the-cli-remote)
-   [Showing the Service Logs](#showing-the-service-logs)
-   [Manage Custom Domains](#manage-custom-domains)
-   [Manage Environment Variables](#manage-environment-variables)
-   [List Projects or Services](#list-projects-or-services)
-   [Execute Commands in a Service Container](#execute-commands-in-a-service-container)
-   [Access a Service's Shell](#access-a-services-shell)

## Installing the DXP Cloud CLI

If you use a Unix-like system such as macOS or Linux, open a terminal and run 
this command: 

    curl https://cdn.wedeploy.com/cli/latest/wedeploy.sh -fsSL | bash

If you get a permissions error, try running the same command with `sudo`. 

If you use Windows, download the latest version of the CLI installer 
[here](https://cdn.wedeploy.com/cli/latest/we-installer-windows-amd64.msi). 
For other systems, see the list of 
[available builds](https://dl.equinox.io/wedeploy/we/stable). 

**Note**: To deploy services on DXP Cloud, you must have 
[Git](https://git-scm.com/) 
installed. 

## Changing the CLI Remote

To access DXP Cloud services via the CLI, you must change the default remote to 
the DXP Cloud servers. The remote URL is `us-west-1.liferay.cloud`. To list the 
CLI's remotes, run this command: 

    we remote

Follow these steps to change the default remote:

1.  Add a new remote, if needed. Note that if the remote you want to set as 
    default already exists, then you don't need to do this step: 

        we remote add <remote-alias> <remote-url>

2.  Run this command to set the default remote: 

        we remote default <remote-alias>

Alternatively, you can specify the remote inline via this command:

    we shell -p <project-id> -s <service-id> --remote <remote-alias>

## Showing the Service Logs

You can use the CLI to display the logs of the services in your DXP Cloud 
project. You do this with the `we log` command. Here are some common examples. 

Check the logs of an entire project: 

    we log --project <projectID>

View the logs of a specific service in a project: 

    we log --project <projectID> --service <serviceID>

Alternatively, you can view a service's logs by passing the service's full URL 
to `we log`: 

    we log --url <serviceID>-<projectID>.wedeploy.io

## Manage Custom Domains

You can use the CLI to manage custom domains in your DXP Cloud project. You do 
this with the `we domain` command. Here are some common examples. 

Get the list of custom domains for a particular service:

    we domain --project <projectID> --service <serviceID>

Add a custom domain to a service:

    we domain add example.com --project <projectID> --service <serviceID>

Remove a custom domain from a service:

    we domain rm example.com --project <projectID> --service <serviceID>

Alternatively, you can run the same commands by passing the service's full URL 
to `we domain`: 

    we domain --url <serviceID>-<projectID>.wedeploy.io

## Manage Environment Variables

To manage environment variables with the CLI, you should use the `we env` 
command. Here are some common examples. 

Get the list of environment variables for a particular service:

    we env --project <projectID> --service <serviceID>

Add an environment variable to a service:

    we env set SOME_KEY somevalue --project <projectID> --service <serviceID>

Remove an environment variable from a service:

    we env rm SOME_KEY --project <projectID> --service <serviceID>

Alternatively, you can pass a service's full URL to `we env`: 

    we env --url <serviceID>-<projectID>.wedeploy.io

## List Projects or Services

You can use the CLI's `we list` command to list projects and services. Here are 
some common examples. 

See the full list of projects and services you own or collaborate on: 

    we list

List a project's services: 

    we list --project <projectID>

Check a specific service in a project: 

    we list --project <projectID> --service <serviceID>

Alternatively, you can check a service by passing its full URL to `we list`: 

    we list --url <serviceID>-<projectID>.wedeploy.io

## Execute Commands in a Service Container

You can also use the CLI to run commands in a service container. For example, 
this runs a command in a specific service instance: 

    we exec --project <projectID> --service <serviceID> --instance <abc123> -- mkdir foo

You can also run the command in any instance of your service: 

    we delete --project <projectID> --service <serviceID> --instance any -- mkdir foo

## Access a Service's Shell

To access a service container's shell, run this command: 

    we shell

This lists all the services in the container and lets you choose which one to 
access. 

Alternatively, you can access the shell of a specific service's container by 
adding the service's project ID and service ID to the `we shell` command: 

    we shell -p <projectID> -s <serviceID>
