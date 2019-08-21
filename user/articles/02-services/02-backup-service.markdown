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

Name                          | Default Value       | Description |
----------------------------- | ------------------- | ----------- |
`LCP_BACKUP_CREATE_SCHEDULE`  |                     | Create backup schedule. |
`LCP_BACKUP_FOLDER`           | `/opt/liferay/data` | The Liferay folder to back up. |
`LCP_BACKUP_RDS`              | `database`          | ID of the RDS database service. |
`LCP_BACKUP_RETENTION_PERIOD` | `30`                | Number of days to retain your backups. The maximum retention period is 30 days, even if you set this to a longer period of time. |
`LCP_BACKUP_CLEANUP_SCHEDULE` | `0 1 * * *`         | The cleanup schedule for backups outside the retention period. | 

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

## Uploading a Backup

### Creating the Database And Volume Files to Upload

#### Creating the Database File

To create a MySQL dump file run the command
`mysqldump -uroot -ppassword --databases --add-drop-database lportal | tar -czvf database.tgz`.
Using the `database` and `add-drop-database` options is necessary for backup
restores to work correctly. You can always use the `/backup/download` api to see
how the backup service creates its MySQL dump file. Using these options will
result in the dump file containing the follow code just before the create table
statements.

```sql
    --
    -- Current Database: `lportal`
    --

    /*!40000 DROP DATABASE IF EXISTS `lportal`*/;

    CREATE DATABASE /*!32312 IF NOT EXISTS*/ `lportal` /*!40100 DEFAULT CHARACTER SET utf8 */;

    USE `lportal`;
```

#### Creating the Volume File

To create a volume run the command
`cd $LIFERAY_HOME/data && tar -czvf volume.tgz document_library`.

### Invoking the Backup API

You can invoke the `/backup/upload` api using a command line tool such as
`curl`. For authentication, use either basic authentication or a user's access
token, which can be retrieved from the cookie `access_token`.

IMPORTANT NOTE:

Passing in the user token in the header `dxpcloud-authorization` will only work
for version `3.2.0` or greater of the backup service. Previous versions should
be upgraded to at least `3.2.0`; otherwise, requests to a previous version need
to use the header `Authorization: Bearer <PROJECT_MASTER_TOKEN>`. The project
master token can be found by running the command
`env | grep LCP_PROJECT_MASTER_TOKEN` in any shell in the Liferay DXP Cloud
console.

##### Parameters

| Name     | Type | Required |
| -------- | ---- | -------- |
| database | file | ✓        |
| volume   | file | ✓        |

##### Curl Examples

```bash
curl -X POST http://<HOST-NAME>/backup/upload /
  -H 'Content-Type: multipart/form-data' /
  -H 'dxpcloud-authorization: Bearer <USER_TOKEN>' /
  -F 'database=@/my-folder/database.tgz' /
  -F 'volume=@/my-folder/volume.tgz'
```

or

```bash
curl -X POST http://<HOST-NAME>/backup/upload /
  -H 'Content-Type: multipart/form-data' /
  -F 'database=@/my-folder/database.tgz' /
  -F 'volume=@/my-folder/volume.tgz' /
  -u user@domain.com:password
```
