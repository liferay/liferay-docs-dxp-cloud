---
header-id: backup-service
---

# Backup Service

The backup service creates regular backups of your Liferay DXP database and 
Document Library. Here, you'll learn how to configure the backup service to your 
needs. 

![Figure 1: The backup service is one of several services available in DXP Cloud.](../../images/services-backups.png)

## Environment Variables

Use the following environment variables in your `LCP.json` file to achieve your 
data redundancy goals. 

Name                          | Default Value              | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
----------------------------- | -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
`LCP_BACKUP_CREATE_SCHEDULE`  | `[5-55][0-1] \* \* \*`     | Cron schedule for creating a backup. If no value is specified in versions `3.2.1` and above a random default will be created.                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
`LCP_BACKUP_FOLDER`           | `/opt/liferay/data`        | The Liferay folder to back up.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
`LCP_BACKUP_RESTORE_SCHEDULE` |                            | Cron schedule for restoring a backup from the production environment, so that the restore process does not need to be done manually in a disaster recovery scenario. This cron value should only be set on an environment intended for disaster recovery that is also of type `production`. Specifying a value for this variable will disable backup creation scheduling for this environment. Ideally this should be set to run every hour to match the backup creation scheduler, perhaps 30 minutes after the backup creation schedule of the actual production environment. |
`LCP_BACKUP_RETENTION_PERIOD` | `30`                       | Number of days to retain your backups. The maximum retention period is 30 days, even if you set this to a longer period of time.                                                                                                                                                                                                                                                                                                                                                                                                                                                |
`LCP_DATABASE_SERVICE`        | `database`                 | ID of the RDS database service.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
`LCP_DBNAME`                  | `lportal`                  | Database name.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
`LCP_MASTER_USER_NAME`        | `dxpcloud`                 | Master username.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
`LCP_MASTER_USER_PASSWORD`    | `LCP_PROJECT_MASTER_TOKEN` | Master password.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |

## Scheduling

You can customize the backup service's scheduling via 
[Cron scheduling syntax](https://crontab.guru/). 
Scheduling can be used for these variables: 

-   `LCP_BACKUP_CREATE_SCHEDULE`
-   `LCP_BACKUP_CLEANUP_SCHEDULE`

### Customizing Scheduling

Use this syntax to create a customized schedule: 

    * * * * *
    ┬ ┬ ┬ ┬ ┬
    │ │ │ │ │
    │ │ │ │ └ day of week (0 - 7) (0 or 7 is Sun)
    │ │ │ └───── month (1 - 12)
    │ │ └────────── day of month (1 - 31)
    │ └─────────────── hour (0 - 23)
    └──────────────────── minute (0 - 59)

For example, the following runs a backup every 12 hours (12AM and 12PM): 

    0 0,12 * * *

### Scheduling Syntax Shorthand

Use the following shorthand syntax for common use cases: 

`@yearly`: Run at the start of every year. 

`@monthly`: Run at the start of every month. 

`@weekly`: Run at the start of every week. 

`@daily`: Run at the start of every day. 

`@hourly`: Run at the start of every hour. 

## Backup APIs

### Invoking the APIs

You can invoke the APIs using a command line tool such as `curl`. 

You can determine the host name of the backup service by finding it on the 
services page. The host name of any service endpoint is constructed using three 
pieces of information: the service name, the project name, and the environment 
name. So for the service `backup`, project `project`, and environment `prd`, the 
host name would be `backup-project-prd.lfr.cloud`. 

### Authentication

You can authenticate using basic authentication; the curl examples to follow all 
use basic authentication. A user access token can also be used, which would be 
necessary if SSO is enabled. This token can be retrieved from the cookie 
`access_token`. The user token is used with the `dxpcloud-authorization` header; 
below is an example for the upload API. 

```bash
curl -X POST /
  http://<HOST-NAME>/backup/upload /
  -H 'Content-Type: multipart/form-data' /
  -H 'dxpcloud-authorization: Bearer <USER_TOKEN>' /
  -F 'database=@/my-folder/database.tgz' /
  -F 'volume=@/my-folder/volume.tgz'
```

| **Note:** Passing the user token in the header `dxpcloud-authorization` only 
| works for versions `3.2.0` or greater of the backup service. Previous versions 
| should be upgraded to at least `3.2.0`. Requests to earlier versions must use 
| the header `Authorization: Bearer <PROJECT_MASTER_TOKEN>`. You can find the 
| project master token by running the command 
| `env | grep LCP_PROJECT_MASTER_TOKEN` in any shell in the Liferay DXP Cloud 
| console. 

### Download Database API

This endpoint returns a compressed file of type ".tgz". 

#### Parameters

Name | Type     | Required |
---- | -------- | -------- |
`id` | `String` | Yes      |

#### curl Example

```bash
curl -X POST /
  https://<HOST-NAME>/backup/download/database/:id /
  -H 'Content-Type: application/json' /
  -u user@domain.com:password /
  --output database.tgz
```

### Download Volume API

This endpoint returns a compressed file of type ".tgz". 

#### Parameters

Name | Type     | Required |
---- | -------- | -------- |
`id` | `String` | Yes      |

#### curl Example

```bash
curl -X POST \
  https://<HOST-NAME>/backup/download/volume/:id /
  -H 'Content-Type: application/json' /
  -u user@domain.com:password /
   --output volume.tgz
```

### Upload Backup API

#### Parameters

Name       | Type   | Required |
---------- | ------ | -------- |
`database` | `File` | Yes      |
`volume`   | `File` | Yes      |

#### curl Example

```bash
curl -X POST /
  http://<HOST-NAME>/backup/upload /
  -H 'Content-Type: multipart/form-data' /
  -F 'database=@/my-folder/database.tgz' /
  -F 'volume=@/my-folder/volume.tgz' /
  -u user@domain.com:password
```

## Creating Files to Upload

### Creating the Database File

To create a MySQL dump file, run this command: 

```bash
mysqldump -uroot -ppassword --databases --add-drop-database lportal | tar -czvf database.tgz
```

The `databases` and `add-drop-database` options are necessary for backup 
restoration to work correctly (you can also use the `/backup/download` API to 
see how the backup service creates its MySQL dump file). With these options, the 
resulting dump file contains the following code just before the create table 
statements. 

```sql
--
-- Current Database: `lportal`
--

/*!40000 DROP DATABASE IF EXISTS `lportal`*/;

CREATE DATABASE /*!32312 IF NOT EXISTS*/ `lportal` /*!40100 DEFAULT CHARACTER SET utf8 */;

USE `lportal`;
```

### Creating the Volume File

To create a volume run this command: 

```bash
cd $LIFERAY_HOME/data && tar -czvf volume.tgz document_library
```