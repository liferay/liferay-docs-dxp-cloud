# Using the DB Upgrade Tool to Upgrade a DXP Cloud Project

Upgrading the Liferay DXP instance (from 7.0 to a newer version) in DXP Cloud requires careful planning, testing and execution in order to be successful. However, Liferay DXP and DXP Cloud teams have introduced several features that make this upgrade process easier and seamless as possible. This article documents how to use the Liferay DXP Upgrade Tool that can be used to upgrade a DXP Cloud instance.

Regardless of whether the upgrade is performed in the cloud on or on site, developers should still make multiple backups at each phase of the project.

Important Note: The process documented below is documented as a workaround and temporary upgrade solution.


## Roadmap

1. [Obtain the Upgrade Environment](#obtain-the-upgrade-environment)
1. [Obtain the required files.](#obtain-the-required-files)
1. [Prepare the Upgrade Environment.](#prepare-the-upgrade-environment)
1. [Running the Upgrade](#running-the-upgrade)

## Obtain the Upgrade Environment

Before upgrading the production instance, it is best practices to perform an upgrade simulation in a lower environment. Administrators should take a backup of their production instance before beginning the upgrade process. Normally, only the DXP Cloud `prd` environment has the Backup and Restore functions. DXP Cloud customers can request that a specific lower environment to be flagged as a `prd` type; in this way, customers are able to use the Backup and Restore functions during the upgrade simulation.

Open a [Help Center](https://liferay-support.zendesk.com/agent/) ticket to request the environment.

## Obtain the required files

The following files are required:

* `app-server.properties`
* `portal-upgrade-database.properties`
* `portal-upgrade-ext.properties`
* `db_upgrade.sh`
* `com.liferay.portal.tools.db.upgrade.client.jar`

These files can be obtained from a Liferay DXP DB Upgrade Client which are available on the [Help Center](https://customer.liferay.com/download) Downloads Page.

1. Select the Product version for the upgrade environment (DXP 7.1 or 7.2).
1. Select _Product/Service Packs_ from the **File Type** drop down menu.
1. Click _Download_ for the corresponding Liferay DXP DB Upgrade Client.
1. Unzip the zip file.

## Prepare the Upgrade Environment

1. Navigate to the project's `/lcp/liferay/script` folder.
1. By default, the folders `common`, `dev`, `uat`, and `prd` are present. Administrators can either create the new folder where the upgrade is performed for testing purposes or use an existing one. If the administrator is creating the new folder, this should match the same environment requested.
1. In the folder where the upgrade is performed, place the files listed above.

### Update the `app-server.properties`

```properties
dir=/opt/liferay/tomcat
extra.lib.dirs=/bin
global.lib.dir=/lib
portal.dir=/webapps/ROOT
server.detector.server.id=tomcat
```

### Update the `portal-upgrade-database.properties`

Enter the following:

```properties
jdbc.default.driverClassName=com.mysql.cj.jdbc.Driver
jdbc.default.url=jdbc:mysql://database/lportal?dontTrackOpenResources=true&holdResultsOpenOverStatementClose=true&useFastDateParsing=false
jdbc.default.username=dxpcloud
jdbc.default.password=PASSWORD_HERE
```

Note: The database password can be found inside the `portal-all.properties` file found within `/lcp/liferay/config/common/`.

### Update the `portal-upgrade-ext.properties`

Enter the following: `liferay.home=/opt/liferay`

### Update Permissions (If Necessary)

It might be necessary to update permissions for the `db_upgrade.sh` and `com.liferay.portal.tools.db.upgrade.client.jar` files in a \*Nix environment. Administrators should be aware of the risks when granting permissions.

### Submit the Changes

Once the configuration files have been modified and the `jar` and shell script placed in the `/lcp/liferay/script` folder:

1. Commit the changes to the branch.
1. Open a pull request.

## Running the Upgrade

Once the pull request has been submitted, the DXP DB Upgrade Tool will execute the upgrade process:

1. A new build is created.
1. The new build will be tested on the Jenkins services.
1. Deploy the build on the upgrade environment; this could be a test environment or the production environment.
1. The upgrade process begins.

If the upgrade fails, restore the environment to a previous, stable build. Resolve whatever issues are in the database that caused the failure.

In order to locate and resolve any database issues during the upgrade process, the platform uses the `verify` process that runs on startup to detect any integrity problems found within the database. This check is done _once_ automatically by default. Change the frequency of the integrity check if necessary.

```properties
# Specify the frequency for verifying the integrity of the database.
    #
    # Constants in VerifyProcess:
    #     public static final int ALWAYS = -1;
    #     public static final int NEVER = 0;
    #     public static final int ONCE = 1;
    #
    # Env: LIFERAY_VERIFY_PERIOD_FREQUENCY
    #
    verify.frequency=1
```

## Additional Informaton

* [Running the Upgrade Tool](https://help.liferay.com/hc/en-us/articles/360018176751-Running-the-Upgrade-Tool)
* [Liferay Digital Experience Platform Upgrade Benchmark](https://www.liferay.com/documents/10182/3292406/Liferay+DXP+Upgrade+Performance+Benchmark.pdf/141a48f7-276b-4422-701b-3cc2f6a4c91b?t=1556636360679)
