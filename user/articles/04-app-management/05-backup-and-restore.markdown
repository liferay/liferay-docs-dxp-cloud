---
header-id: backup-and-restore
---

# Backup and Restore

It's important for the data of production applications to be safe. You can use 
DXP Cloud to backup and restore data. All backups save a dump of the database, 
environment volumes, and the Documents and Media folder. 

## Creating a Backup

To create a manual backup, go to your production environment's page, select the 
*Backups* tab in the left menu, and click *Backup Now*. You can also set an 
interval for automated backups via environment variables. See 
[Backup Service](https://help.liferay.com/hc/en-us/articles/360027968772) 
to learn more about configuring this service. 

![Figure 1: You can create backups in DXP Cloud.](../../images/backups.png)

## Restoring from a Backup 

The Backups tab contains a table that shows each backup in the environment. The 
table displays each backup's name, size, and creation date and time. To restore 
from a backup, click the backup's *Actions* button in the table and select 
*Restore*. 

![Figure 2: You can restore from a backup in DXP Cloud.](../../images/backup-restore.png)
