---
header-id: command-line-tool
---

# Command-line Tool

Liferay Cloud's command-line interface (CLI) is a tool that helps you use and 
manage DXP Cloud. For example, you can use the CLI to create, manage, and scale 
applications. 

## Installing the Liferay Cloud CLI

If you use a Unix-like system such as macOS or Linux, open a terminal and run 
this command: 

```bash
curl https://cdn.liferay.cloud/cli/latest/lcp.sh -fsSL | bash
```

If you get a permissions error, try running the same command with `sudo`. 

If you use Windows, download the latest version of the 
[CLI installer](https://cdn.wedeploy.com/cli/latest/we-installer-windows-amd64.msi). 
For other systems, see the list of 
[available builds](https://dl.equinox.io/wedeploy/we/stable). 

| **Note:** To deploy services on DXP Cloud, you must have 
| [Git](https://git-scm.com/) 
| installed. 

## Changing the CLI Remote

To access DXP Cloud services via the CLI, your CLI must be pointed to the right 
DXP Cloud. The remote URL for DXP Cloud is `liferay.cloud`. To list the CLI's 
remotes, run this command: 

```shell
lcp remote
```

Follow these steps to change the default remote: 

1.  Add a new remote, if needed (if the remote you want to set as default 
    already exists, then you don't need to do this step): 

    ```shell
    lcp remote add <remote-alias> <remote-url>
    ```

2.  Run this command to set the default remote: 

    ```shell
    lcp remote default <remote-alias>
    ```

Alternatively, you can specify the remote inline via this command: 

```shell
lcp shell -p <project-id> -s <service-id> --remote <remote-alias>
```

## Showing the Service Logs

You can use the `lcp log` command to display your DXP Cloud project's service 
logs. Here are some common examples. 

Check the logs of an entire project: 

```shell
lcp log --project <projectID>
```

View the logs of a specific service in a project: 

```shell
lcp log --project <projectID> --service <serviceID>
```

Alternatively, you can view a service's logs by passing the service's full URL 
to `lcp log`: 

```shell
lcp log --url <serviceID>-<projectID>.lfr.cloud
```

## Manage Custom Domains

You can use the `lcp domain` command to manage custom domains in your DXP Cloud 
project. Here are some common examples. 

Get the list of custom domains for a particular service: 

```shell
lcp domain --project <projectID> --service <serviceID>
```

Add a custom domain to a service:

```shell
lcp domain add example.com --project <projectID> --service <serviceID>
```

Remove a custom domain from a service:

```shell
lcp domain rm example.com --project <projectID> --service <serviceID>
```

Alternatively, you can run the same commands by passing the service's full URL 
to `lcp domain`: 

```shell
lcp domain --url <serviceID>-<projectID>.lfr.cloud
```

## Manage Environment Variables

You can use the `lcp env` command to manage environment variables. Here are some 
common examples. 

Get the list of environment variables for a particular service: 

```shell
lcp env --project <projectID> --service <serviceID>
```

Add an environment variable to a service: 

```shell
lcp env set SOME_KEY somevalue --project <projectID> --service <serviceID>
```

Remove an environment variable from a service: 

```shell
lcp env rm SOME_KEY --project <projectID> --service <serviceID>
```

Alternatively, you can pass a service's full URL to `lcp env`: 

```shell
lcp env --url <serviceID>-<projectID>.lfr.cloud
```

## List Projects or Services

You can use the `lcp list` command to list projects and services. Here are some 
common examples. 

See the full list of projects and services you own or collaborate on: 

```shell
lcp list
```

List a project's services: 

```shell
lcp list --project <projectID>
```

Check a specific service in a project: 

```shell
lcp list --project <projectID> --service <serviceID>
```

Alternatively, you can check a service by passing its full URL to `lcp list`: 

```shell
lcp list --url <serviceID>-<projectID>.lfr.cloud
```

## Execute Commands in a Service Container

You can also use the CLI to run commands in a service container. For example, 
this runs a command in a specific service instance: 

```shell
lcp exec --project <projectID> --service <serviceID> --instance <abc123> -- mkdir foo
```

You can also run the command in any instance of your service: 

```shell
lcp delete --project <projectID> --service <serviceID> --instance any -- mkdir foo
```

## Access a Service's Shell

To access a service container's shell, run this command: 

```shell
lcp shell
```

This lists all the services in the container and lets you choose which one to 
access. 

Alternatively, you can access the shell of a specific service's container by 
adding the service's project ID and service ID to the `lcp shell` command: 

```shell
lcp shell -p <projectID> -s <serviceID>
```
