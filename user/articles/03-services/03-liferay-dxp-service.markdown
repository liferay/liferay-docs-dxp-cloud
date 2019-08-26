---
header-id: liferay-dxp-service
---

# Liferay DXP Service

The Liferay DXP service is the heartbeat of your project. It runs your 
application's Liferay DXP instance and interacts with other services like the 
web server, Elasticsearch, and MySQL database. 

![Figure 1: The Liferay DXP service is one of several services available in DXP Cloud.](../../images/services-dxp.png)

## Deployment

To install themes, portlets, or OSGi modules, you can include a WAR or JAR file 
in the `/deploy/common` folder. For example, to deploy a custom JAR file, your 
Liferay DXP source code directory could look like this: 

    liferay
    ├── deploy
    │ └── common
    │   └── com.liferay.apio.samples.portlet-1.0.0.jar
    └── LCP.json

Under the hood, such files are copied to the `$LIFERAY_HOME/deploy` folder and
deployed on startup. 

## Licenses

It's possible to add your own license by creating a license folder for the 
license: 

    liferay
    ├── license
    │ └── license.xml
    │ └── license.aatf
    └── LCP.json

XML licenses are copied to `$LIFERAY_HOME/deploy` and AATF licenses are copied 
to `$LIFERAY_HOME/data`. 

## Hot Deploy

Using hot deploy in DXP Cloud isn't recommended. If you still want to use hot 
deploy, you can do so via the Liferay DXP UI. 

## Configurations

To launch new property or OSGI configurations, you can use the `config` folder 
as an extension point. This extension point supports `.cfg`, `.properties`, and 
`.config` files. 

For example, to deploy a configuration for the Elasticsearch OSGi bundle, your 
folder structure could look like this: 

    liferay
    ├── config
    │ └── com.liferay.portal.search.elasticsearch6.configuration.ElasticsearchConfiguration.config
    └── LCP.json

Under the hood, all files are copied to the `$LIFERAY_HOME` folder and 
automatically applied on startup. 

## Portal Properties

There's also a set of files you can use to configure the environment. The portal 
reads these files in the following order: 

`portal-all.properties`: Contains the properties that change Liferay DXP across 
environments. 

`portal-env.properties`: Contains the properties that only affect the current 
environment (e.g., credentials and URL endpoints for external services that 
differ from environment to environment). 

`portal-clu.properties`: Contains the preconfigured properties for clustering 
Liferay DXP on DXP Cloud. You typically don't need to change these. See the 
[Clustering section](#clustering) 
for more information. 

`portal-ext.properties`: Contains the final changes to your Liferay DXP 
configuration. Since you should set most of your properties in 
`portal-all.properties` and `portal-env.properties`, this file is typically 
empty or missing altogether. For testing, however, you may find it useful. 

## Clustering

### Enabling Clustering

Clustering Liferay DXP on DXP Cloud is straightforward. First, set the 
environment variable `LCP_PROJECT_LIFERAY_CLUSTER_ENABLED` to `true`. This 
instructs the image startup process to add the clustering configuration to 
Liferay DXP. Second, increase the scale in `LCP.json` to the desired number of 
nodes. 

Behind the scenes, the image startup process copies the files 
`portal-clu.properties` and `unicast.xml` to the Liferay Home folder. These 
files contain the configuration needed to run a Liferay DXP cluster on DXP 
Cloud. 

### Verifying Clustering is Working

To check if clustering is working correctly, examine the Liferay logs of 
the different running instances to find the lines with the `Accepted View` 
message from the `JGroupsReceiver` class. Below are some sample logs: 

```shell
Aug 26 09:42:22.778 build-90 [liferay-68b8f6b48d-hdj9t] [dxp] INFO  [Incoming-2,liferay-channel-transport-0,liferay-68b8f6b48d-hdj9t-23003][JGroupsReceiver:91] Accepted view [liferay-68b8f6b48d-r8r5f-1292|8] (3) [liferay-68b8f6b48d-r8r5f-1292, liferay-68b8f6b48d-gzsg4-15389, liferay-68b8f6b48d-hdj9t-23003]
Aug 26 09:42:22.779 build-90 [liferay-68b8f6b48d-hdj9t] [dxp] INFO  [Incoming-1,liferay-channel-control,liferay-68b8f6b48d-hdj9t-17435][JGroupsReceiver:91] Accepted view [liferay-68b8f6b48d-r8r5f-29669|8] (3) [liferay-68b8f6b48d-r8r5f-29669, liferay-68b8f6b48d-gzsg4-48301, liferay-68b8f6b48d-hdj9t-17435]
```

`Accepted view [liferay-68b8f6b48d-r8r5f-1292|8]` tells us that 
`liferay-68b8f6b48d-r8r5f-1292` is master and 
`(3) [liferay-68b8f6b48d-r8r5f-29669, liferay-68b8f6b48d-gzsg4-48301, liferay-68b8f6b48d-hdj9t-17435]` 
tells us that `(3)` nodes are part of the cluster as well as the ids of the 
nodes. This list includes the master node in addition to the slave nodes. 

### Clustering and Auto-scaling

The `scale` attribute of `LCP.json` and auto-scaling features work together. By 
specifying `scale` the initial number of instances is set. If auto-scaling is 
enabled the number of instances will increase according to demand. 

## Hotfixes

To apply hotfixes, add the hotfix ZIP file to the `hotfix` folder. When you 
deploy this change, the hotfix is applied to your application. 

    liferay
    ├── hotfix
    │ └── liferay-hotfix-2-7110.zip
    └── LCP.json

## Scripts

You can use scripts for more extensive customizations. However, use caution when 
doing so. This is the most powerful way to customize Liferay DXP and can cause 
undesired side effects. 

Any `.sh` files found in the `script` folder are run prior to starting your 
service. For example, to include a script that removes all log files, you could 
place it in the following directory structure: 

    liferay
    ├── script
    │ └── remove-log-files.sh
    └── LCP.json

## Advanced Monitoring with Dynatrace

To enable advanced monitoring with Dynatrace on Liferay DXP in production, you 
must set two environment variables: 

```json
"environments": {
  "prd": {
    "env": {
      "LCP_PROJECT_MONITOR_DYNATRACE_TENANT": "tot02934",
      "LCP_PROJECT_MONITOR_DYNATRACE_TOKEN": "dDKSowkdID8dKDkCkepW"
    }
  }
}
```

`LCP_PROJECT_MONITOR_DYNATRACE_TENANT`: The tenant value is a string with eight 
characters. It's part of the URL (prefix) of your Dynatrace SaaS product. 

`LCP_PROJECT_MONITOR_DYNATRACE_TOKEN`: The token is another string with 22 
characters that you can find in your Dynatrace account at *Deploy Dynatrace* 
&rarr; *Start installation* &rarr; *Set up PaaS monitoring* &rarr; 
*Installer Download*. 
