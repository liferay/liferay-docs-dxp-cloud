# Liferay DXP Service

The Liferay DXP service is the heartbeat of your entire project. It runs the DXP
instance of your application and interacts with the other services like the
Proxy, Elasticsearch, and RDS database.

![Figure 1: The Liferay DXP service is one of several services available in DXP Cloud.](../../images/services-dxp.png)

## Deployment

To install themes, portlets, or OSGi modules, you can include a WAR or JAR file
in the `/deploy/common` folder and then push it to DXP Cloud.

For example, if you wanted to deploy a custom JAR file, you would include it in
this is how your DXP source code directory could look like:

    liferay
    ├── deploy
    │ └── common
    │   └── com.liferay.apio.samples.portlet-1.0.0.jar
    └── wedeploy.json

Under the hood, those files will be copied into the `$LIFERAY_HOME/deploy`
folder and deployed on startup.

## Licenses

It is possible to add your own license by creating a directory called `license` 
and dropping it there.

    liferay
    ├── license
    │ └── license.xml
    │ └── license.aatf
    └── wedeploy.json

The license will be copied into either the deploy folder or into data folder of
the Liferay home. If the license is a .xml file, it will be copied to the deploy
folder. Otherwise, if it is a .aatf file, it goes to the data folder.

## Hot Deployment

In order to promote best practices, we do not recommend using the hot deployment
approach. If you still want to use this method for development purposes, you can
do it with the Liferay application UI.

## Configurations

To launch new property or OSGI configurations, you can use the config directory
as an extension point. This extension point supports `.cfg`, `.properties`, and
`.config` files.

For example, if you wanted to deploy a configuration for the Elasticsearch OSGi
bundle, this is how your directory could look like:

    liferay
    ├── config
    │ └── com.liferay.portal.search.elasticsearch6.configuration.ElasticsearchConfiguration.config
    └── wedeploy.json

Under the hood, all files will be copied into the `$LIFERAY_HOME` folder and
automatically applied on startup.

## Portal Properties

There is also a set of files that can be used to configure the environment
properly. These files are read by the portal in the order that they are
presented below:

`portal-all.properties`: contains the properties that change Liferay across 
environments.

`portal-env.properties`: contains the properties that will only affect the
current environment like credentials and URL endpoints for external services
that differ from environment to environment.

`portal-clu.properties`: contains the pre-configured properties for clustering
Liferay on DXP Cloud. Most of the time you don't need to make any change to it.
More information is available on the Configuring Cluster section.

`portal-ext.properties`: contains the final changes to your Liferay
configuration. Most of the time you are going to use portal-all.properties and
portal-env.properties to set the properties. As a best practice, this file
should be empty or nonexistent, but for testing purposes, it works well.

## Cluster

You can cluster Liferay on DXP Cloud very easily by just setting the environment
variable `WEDEPLOY_PROJECT_LIFERAY_CLUSTER_ENABLED` to `true`. That will
instruct the image startup process to add the configuration to Liferay for
establishing a cluster.

Behind the scenes, the image startup process copies the file
`portal-clu.properties` and `unicast.xml` to the Liferay home. These files
contain the configuration needed to run a Liferay cluster on the DXP Cloud
infrastructure.

## Hotfixes

To apply hot fixes, you can just add your .zip file to the `hotfix` folder. When
you deploy this change, we will apply the hotfix to your application.

    liferay
    ├── hotfix
    │ └── liferay-hotfix-2-7110.zip
    └── wedeploy.json

## Scripts

For full customization, you can use the scripts extension points. This is the
most powerful and customizable functionality so be careful of what you are
running to avoid causing undesired side effects.

Any `.sh` files found in the `script` directory will be run prior to starting
your service. For example, if you wanted to include a script that removed all
log files, you could include something like this:

    liferay
    ├── script
    │ └── remove-log-files.sh
    └── wedeploy.json

## Advanced Monitoring with Dynatrace

To enable advanced monitoring with Dynatrace on your DXP, you must set two
environment variables:

`WEDEPLOY_PROJECT_MONITOR_DYNATRACE_TENANT`: The tenant value is a string with 8
characters. It is part (prefix) of the URL of your Dynatrace SaaS product.

`WEDEPLOY_PROJECT_MONITOR_DYNATRACE_TOKEN`: The token is another string with 22
characters that can be found at you Dynatrace account in the following menu
path: Deploy Dynatrace &rarr; Start installation &rarr; Set up PaaS monitoring
&rarr; InstallerDownload.
