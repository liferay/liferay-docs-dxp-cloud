# Backup Service

The Backup service creates regular backups of your Liferay DXP database and
Document Library. Below, you'll find all the details you'll need to configure
your Backup service to suit your needs.

![Figure 1: The Backup service is one of several services available in DXP Cloud.](../../images/services-backups.png)

## Environment Variables

We've included environment variables for your `wedeploy.json` file to help you
achieve your data redundancy goals.

Name | Default Value | Description |
---- | ------------- | ----------- |
`WEDEPLOY_BACKUP_CREATE_SCHEDULE` |  | Create backup schedule. |
`WEDEPLOY_BACKUP_FOLDER` | `/opt/liferay/data` | The Liferay folder to be backed up. |
`WEDEPLOY_BACKUP_RDS` | `database` | ID of the RDS database service. |
`WEDEPLOY_BACKUP_RETENTION_PERIOD` | `30` | Number of days to retain your backups. |
`WEDEPLOY_BACKUP_CLEANUP_SCHEDULE` | `0 1 * * *` | The cleanup schedule for backups outside the retention period. |

**Note**: The maximum retention period for backups is 30 days ,even if you set 
`WEDEPLOY_BACKUP_RETENTION_PERIOD` for a longer period of time.

## Scheduling

All the scheduling on the backup service can be customized using 
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

You can use this syntax to create a customized schedule. For example, the 
following runs a backup every 12 hours (12AM and 12PM): 

    0 0,12 * * *

### Scheduling Syntax Shorthand

You can use the following shorthand syntax for common use cases: 

`@yearly`: Run at the start of every year.

`@monthly`: Run at the start of every month.

`@weekly`: Run at the start of every week.

`@daily`: Run at the start of every day.

`@hourly`: Run at the start of every hour.
