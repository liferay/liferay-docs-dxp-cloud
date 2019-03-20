# Command Line Tool

The DXP Cloud command line interface is a tool for helping you to use the DXP
Cloud platform by providing support for things like creating, managing, and
scaling applications.

## Installing DXP Cloud CLI

If you use a Unix-like system such as macOS or Linux, open your terminal and
run:

    curl https://cdn.wedeploy.com/cli/latest/wedeploy.sh -fsSL | bash

In case of error regarding permissions, try to run the same command with `sudo`
the the beginning.

If you use Windows, download the latest version of our installer
[here](https://cdn.wedeploy.com/cli/latest/we-installer-windows-amd64.msi).
For other systems, take a look at the list of 
[available builds](https://dl.equinox.io/wedeploy/we/stable).

**Note**: It is required to have Git installed for deploying services. If you do
not have 
[Git](https://git-scm.com/) 
installed, you can download it 
[here](https://git-scm.com/download/).

## Change the CLI Remote

To access DXP Cloud services via CLI you have to change the default
remote to the DXP Cloud servers. The remote URL is `us-west-1.liferay.cloud`. To 
list all remotes of the CLI, just run the following command:

    we remote

To change the default remote from CLI, you must add a new remote first:

    we remote add <remote-alias> <remote-url>

To select a remote as the default one, you have to choose one among the
ones shown by the command `we remote`:

    we remote default <remote-alias>

Alternatively, you can run every CLI command and specify the remote inline:

    we shell -p <project-id> -s <service-id> --remote <remote-alias>

## Show Logs of the Services

You can check the logs of an entire project:

    we log --project <projectID>

Or you can see the logs of a specific service inside of a project:

    we log --project <projectID> --service <serviceID>

Alternatively, you can see the logs of a service by passing the full URL:

    we log --url <serviceID>-<projectID>.wedeploy.io

## Manage Custom Domains

Get the list of custom domains for a particular service:

    we domain --project <projectID> --service <serviceID>

Add a custom domain to a service:

    we domain add example.com --project <projectID> --service <serviceID>

Remove custom domain from a service:

    we domain rm example.com --project <projectID> --service <serviceID>

Alternatively, you can run those same commands by passing the full URL:

    we domain --url <serviceID>-<projectID>.wedeploy.io

## Manage Environment Variables

Get the list of environment variables for a particular service:

    we env --project <projectID> --service <serviceID>

Add an environment variable to a service:

    we env set SOME_KEY somevalue --project <projectID> --service <serviceID>

Remove environment variable from a service:

    we env rm SOME_KEY --project <projectID> --service <serviceID>

Alternatively, you can run those same commands by passing the full URL:

    we env --url <serviceID>-<projectID>.wedeploy.io

## List Projects or Services

See the full list of projects and services you own or collaborator with:

    we list

List the services that are contained on a project:

    we list --project <projectID>

Check a specific service inside of a project:

    we list --project <projectID> --service <serviceID>

Alternatively, check a specific service by passing the full URL:

    we list --url <serviceID>-<projectID>.wedeploy.io

## Execute Commands Into a Service Container

You can run a command in a specific instance of your service:

    we exec --project <projectID> --service <serviceID> --instance <abc123> -- mkdir foo

Or you can run the command in any instance of your service:

    we delete --project <projectID> --service <serviceID> --instance any -- mkdir foo

## Access Shell of a Service

You can access the shell of a service's container by running the command below. 
It will list all your services for you to choose which one you want to access: 

    we shell

Or you can access the shell of a specific service’s container by adding its 
`projectId` and `serviceId`: 

    we shell -p <projectID> -s <projectID>
