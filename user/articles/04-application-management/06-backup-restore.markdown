# Backup and Restore

It's important for all application in production to have its data safe. Allowing
backup and restore gives you the possibility of creating backups whenever you
want as well as restoring them.

All backups save a dump of the database, environments' volumes, and documents
and media folder.

## Creating a Backup

To create a backup, you have to go to your `prd` environment page, select the
*Backups* tab on the left menu, and click on *Backup Now*. Also, you can set an 
interval for automated backups via environment variables. 

![Figure 1: You can create backups in DXP Cloud.](../../images/backups.png)

## Restoring from a Backup

At the same page, you are able to see the backup history of your environment.
There, you can click on the *Actions* icon located on each row of the backup
history and select *Restore*. 

![Figure 2: You can create backups in DXP Cloud.](../../images/backup-restore.png)
