Backup Restoration Guide
------------------------

MySQL Data Restoration
----------------------
This guide describes the process of restoring the MySQL database from a backup.

Prerequisites:
- Access to the MySQL server with root privileges.
- The backup files available on the server.

Restoration Steps:
1. Download the Backup:

Log in as the `backup` user and download the backup from the backup server:

sudo -i -u backup

duplicity --no-encryption restore rsync://bagi0@backup.rabagh.io/mysql /home/backup/restore/mysql

Check if the file is actually restored:

ls -la /home/backup/restore/mysql

If the file is missing clear duplicity cache and run the duplicity restore command again:

sudo rm -rf /home/backup/.cache/duplicity

2. Prepare MySQL database:

Switch back to ubuntu/root user.
Before restoring, ensure the agama database is clean or does not exist to prevent conflicts:

sudo mysql -e "DROP DATABASE IF EXISTS agama; CREATE DATABASE agama;"

3. Restore MySQL Data:
Execute the following command as the `root` user:

mysql agama < /home/backup/restore/mysql/agama.sql

4. Verification:
Verify the integrity and completeness of the restored data by accessing agama via pubic url and checking table records.


InfluxDB Data Restoration
-------------------------
This section details the steps to restore the InfluxDB `telegraf` database from the backup.

Prerequisites:
- Access to the InfluxDB server.
- The backup files must be available on the server.

Restoration Steps:
1. Stop Telegraf Service:
Prevent data writes during the restoration process.

sudo service telegraf stop

2. Download the Backup:
Log in as the `backup` user and download the InfluxDB backup.

sudo -i -u backup

duplicity --no-encryption restore rsync://bagi0@backup.rabagh.io/influxdb /home/backup/restore/influxdb

3. Restore the Database:
- Drop the existing `telegraf` database.

  influx -execute 'DROP DATABASE telegraf'

- Restore the `telegraf` database from the backup.

  influxd restore -portable -database telegraf /home/backup/restore/influxdb


4. Restart the Telegraf Service:
After verifying the restoration, login back to root/ubuntu and restart the Telegraf service.

sudo service telegraf start

Verification:
Ensure that the `telegraf` database has been restored correctly.

sudo systemctl status telegraf
