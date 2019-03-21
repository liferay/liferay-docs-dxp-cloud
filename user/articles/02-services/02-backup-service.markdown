# Backup Service

The backup service creates regular backups of your Liferay DXP database and
Document Library. Here, you'll find all the details you'll need to configure the 
backup service to suit your needs. 

![Figure 1: The backup service is one of several services available in DXP Cloud.](../../images/services-backups.png)

## Environment Variables

Use the following environment variables in your `wedeploy.json` file to achieve 
your data redundancy goals.
<!-- Explain wedeploy.json... e.g., where do you put it? -->

Name | Default Value | Description |
---- | ------------- | ----------- |
`WEDEPLOY_BACKUP_CREATE_SCHEDULE` |  | Create backup schedule. |
`WEDEPLOY_BACKUP_FOLDER` | `/opt/liferay/data` | The Liferay folder to be backed up. |
`WEDEPLOY_BACKUP_RDS` | `database` | ID of the RDS database service. |
`WEDEPLOY_BACKUP_RETENTION_PERIOD` | `30` | Number of days to retain your backups. Note that the maximum retention period for backups is 30 days, even if you set this to a longer period of time. |
`WEDEPLOY_BACKUP_CLEANUP_SCHEDULE` | `0 1 * * *` | The cleanup schedule for backups outside the retention period. |

## Scheduling

You can customize the backup service's scheduling via 
[Cron scheduling syntax](https://crontab.guru/). 
This scheduling can be used for the following variables: 

-   `WEDEPLOY_BACKUP_CREATE_SCHEDULE`
-   `WEDEPLOY_BACKUP_CLEANUP_SCHEDULE`

### Customizing Scheduling

    * * * * *
    ┬ ┬ ┬ ┬ ┬
    │ │ │ │ │ 
    │ │ │ │ └ day of week (0 - 7) (0 or 7 is Sun)
    │ │ │ └───── month (1 - 12)
    │ │ └────────── day of month (1 - 31)
    │ └─────────────── hour (0 - 23)
    └──────────────────── minute (0 - 59)

Use this syntax to create a customized schedule. For example, the following runs 
a backup every 12 hours (12AM and 12PM): 

    0 0,12 * * *

### Scheduling Syntax Shorthand

Use the following shorthand syntax for common use cases: 

`@yearly`: Run at the start of every year.

`@monthly`: Run at the start of every month.

`@weekly`: Run at the start of every week.

`@daily`: Run at the start of every day.

`@hourly`: Run at the start of every hour.
