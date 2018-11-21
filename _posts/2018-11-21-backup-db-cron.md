---
published: true
---
## Взято отсюда [BASH BACKUP ROTATION SCRIPT](https://nicaw.wordpress.com/2013/04/18/bash-backup-rotation-script/ "BASH BACKUP ROTATION SCRIPT")

Создаем следующую фаловую структуру:
```
drwxr-xr-x 15 root root 4096 Apr 23 06:44 backup.daily
drwxr-xr-x  4 root root 4096 Apr  1 06:29 backup.monthly
-rwxr-x---  1 root root 1386 Feb 21 11:53 backup.sh
drwxr-xr-x 10 root root 4096 Apr 20 06:38 backup.weekly
drwxr-xr-x  2 root root 4096 Apr 23 06:44 incoming
drwxr-xr-x  2 root root 4096 Apr 23 06:44 cron_daily.sh
```

### Далее создаем в этой же директории файл backup.sh:
```
#!/bin/bash
# Julius Zaromskis
# Backup rotation

# Storage folder where to move backup files
# Must contain backup.monthly backup.weekly backup.daily folders
storage=/backup/path

# Source folder where files are backed
source=$storage/incoming

# Destination file names
date_daily=`date +"%d-%m-%Y"`
#date_weekly=`date +"%V sav. %m-%Y"`
#date_monthly=`date +"%m-%Y"`

# Get current month and week day number
month_day=`date +"%d"`
week_day=`date +"%u"`

# Optional check if source files exist. Email if failed.
if [ ! -f $source/archive.tgz ]; then
ls -l $source/ | mail user@mail.com -s "[backup script] Daily backup failed! Please check for missing files."
fi

# It is logical to run this script daily. We take files from source folder and move them to
# appropriate destination folder

# On first month day do
if [ "$month_day" -eq 1 ] ; then
  destination=backup.monthly/$date_daily
else
  # On saturdays do
  if [ "$week_day" -eq 6 ] ; then
    destination=backup.weekly/$date_daily
  else
    # On any regular day do
    destination=backup.daily/$date_daily
  fi
fi

# Move the files
mkdir $storage/$destination
mv -v $source/* $storage/$destination

# daily - keep for 14 days
find $storage/backup.daily/ -maxdepth 1 -mtime +14 -type d -exec rm -rv {} \;

# weekly - keep for 60 days
find $storage/backup.weekly/ -maxdepth 1 -mtime +60 -type d -exec rm -rv {} \;

# monthly - keep for 300 days
find $storage/backup.monthly/ -maxdepth 1 -mtime +300 -type d -exec rm -rv {} \;
```
### Далее создаем в этой же директории файл cron_daily.sh:
```
#!/bin/bash
#@author kwhy
#@description Backup script for your website

BACKUP_DIR=/backup/dir

# Dump MySQL tables
mysqldump -u user -pPass dbname | gzip -3 -c > $BACKUP_DIR/incoming/dbname.sql.gz

# Run backup rotate
cd $BACKUP_DIR
bash backup.sh

# Cleanup
#rm $BACKUP_DIR/incoming/dbname.sql.gz
```

### Далее запускаем по крону shell скрипт:
```
20 17 * * * /CONTENT/hdd/backups/picfind/cron_daily.sh
```
