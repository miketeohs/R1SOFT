AGENT INSTALLATION:
yum install r1soft_cdp_enterprise_agent
yum -y --disablerepo=\* --enablerepo=r1soft install serverbackup-enterprise-agent

systemctl enable cdp-agent.service
systemctl start cdp-agent.service
systemctl status cdp-agent.service
systemctl list-units


r1soft-setup --test-connection
r1soft-setup --get-key
r1soft-setup --list-keys

r1soft-setup --test-connection
r1soft-setup --list-keys
r1soft-setup --get-keys http://10.11.53.206:8080

AGENT WITH MYSQL DB

grant all on mysql.* to 'softlayerbackup'@'10.111.53.206' identified by '';
grant all on psa_fish.* to 'softlayerbackup'@'10.111.53.206' identified by '';
grant all on dbpsamarine.* to 'softlayerbackup'@'10.111.53.206' identified by '';
grant all on dbpsausity.* to 'softlayerbackup'@'10.111.53.206' identified by '';
grant all on dbunboxed.* to 'softlayerbackup'@'10.111.53.206' identified by '';
grant all on dbglobalpsa.* to 'softlayerbackup'@'10.111.53.206' identified by '';
grant all on mysql.* to 'softlayerbackup'@'10.111.53.206' identified by '';

1. grant all on *.* to 'softlayerbackup'@'%' identified by ''
grant shutdown on *.* to 'softlayerbackup'

show grants for 'softlayerbackup'@'localhost'
select user(), currentuser();

SELECT table_schema                                        "DB Name",
   Round(Sum(data_length + index_length) / 1024 / 1024, 1) "DB Size in MB"
FROM   information_schema.tables
where table_schema='psa_fish'
GROUP  BY table_schema;

http://wiki.r1soft.com/display/kb3/CDP+for+Databases
http://wiki.r1soft.com/display/kb3/Error+-+Backups+of+MS+SQL+Server+and+Databases+using+MS+SQL+Addon+not+Working
http://wiki.r1soft.com/display/kb3/Restoring+MySQL+Using+Bare-Metal+Restore

Restoration Steps

Settings - Disk Safe - choose/tick the desired Disk Safe - Actions column - Open Recovery Points

Action column of DS - 1. Open Recovery Point 2. Edit DS 3. Vacuum DS 4. Compact DS 5. Detach DS 6. Close 7. Delete DS

Settings - Policies - tick Policy - Actions - 1. Edit Policy - 2. Run Now 3. On Demand Retention 4. Verify DS Now 5. Disable 6. Delete Policy

Perform a Compact DS on Protected Machine : UAT. During the execution, another directory is created in backup01:/data/Backups/VOL_UAT001/abef0b26-c3be-4bfe-ab1f-dd0395d44324_compaction_in_progres
started at 10:04. altogether 51 min

/usr/sbin/r1soft/bin/r1soft-mysql-util --wait-ping --hostname 'localhost' --port 3307 --user 'softlayerbackup' --pass ''

mysql    32335 32227  0 19:13 pts/1    00:00:00 /usr/libexec/mysqld ' --basedir=/usr '
--datadir=/var/lib/mysql '
--user=mysql '
--log-error=/var/log/mysqld.log '
--pid-file=/var/run/mysqld/mysqld.pid '
--socket=/var/lib/mysql/mysql.sock
root     32227     1  0 19:13 pts/1    00:00:00 /bin/sh /usr/bin/mysqld_safe '
--datadir=/var/lib/mysql '
--socket=/var/lib/mysql/mysql.sock '
--pid-file=/var/run/mysqld/mysqld.pid '
--basedir=/usr '
--user=mysql

/usr/libexec/mysqld ' --no-defaults --big-tables '
--innodb_data_home_dir=./ '
--innodb_log_group_home_dir=./ '
--innodb_log_file_size=5242880 '
--innodb_log_files_in_group=2 '
--innodb_data_file_path=ibdata1:10M:autoextend '
--user=root '
--basedir=/usr/ '
--datadir=/var/lib/r1soft/tmp/r1soft-mysql-restore-tmp-47e045bb-37a6-4852-94fb-050b85b4f850 '
--socket=/var/lib/r1soft/tmp/r1soft-mysql-restore-tmp-47e045bb-37a6-4852-94fb-050b85b4f850/mysqld.sock '
--pid-file=/var/lib/r1soft/tmp/r1soft-mysql-restore-tmp-47e045bb-37a6-4852-94fb-050b85b4f850/mysqld.pid '
--tmpdir=/var/lib/r1soft/tmp/r1soft-mysql-restore-tmp-47e045bb-37a6-4852-94fb-050b85b4f850 '
--log-error '
--port=3307

/usr/libexec/mysqld '
--no-defaults '
--big-tables '
--innodb_data_home_dir=./ '
--innodb_log_group_home_dir=./ '
--innodb_log_file_size=5242880 '
--innodb_log_files_in_group=2 '
--innodb_data_file_path=ibdata1:10M:autoextend '
--user=root '
--basedir=/usr/ '
--datadir=/var/lib/r1soft/tmp/r1soft-mysql-restore-tmp-a275cfcf-04e7-4599-aa75-b754b7f8cb42 '
--socket=/var/lib/r1soft/tmp/r1soft-mysql-restore-tmp-a275cfcf-04e7-4599-aa75-b754b7f8cb42/mysqld.sock '
--pid-file=/var/lib/r1soft/tmp/r1soft-mysql-restore-tmp-a275cfcf-04e7-4599-aa75-b754b7f8cb42/mysqld.pid '
--tmpdir=/var/lib/r1soft/tmp/r1soft-mysql-restore-tmp-a275cfcf-04e7-4599-aa75-b754b7f8cb42 '
--log-error '
--port=3307

restore to alt agent
agent uat001
db host 10.66.177.83
db port 3306

authentication
spec alt authentication
username root
password 

temp instance
db host 10.66.177.83
db port 3306

/usr/sbin/r1soft/bin/r1soft-mysql-util --wait-ping --hostname 'localhost' --port 3306 --user 'softlayerbackup' --pass ''
/usr/sbin/r1soft/bin/r1soft-mysql-util --wait-ping --hostname 'localhost' --port 3306 --user 'root' --pass 'vTaRuy1L257d'

Task Status
----------------------------------------
Type            Database Restore
State           Error
Start Time      September 29, 2017 5:36:24 PM SGT
End Time        September 29, 2017 6:31:50 PM SGT
Run Time        55m 25s

Alerts
----------------------------------------
Alert Time      September 29, 2017 6:31:50 PM SGT
essage         Socket timed out
Associated Log Messages
        Message Time            Level   Source                  Message^M
        9/29/17 6:31:50 PM      Error   Manager                 Socket timed out after waiting for more than 1,800 seconds to read/write

Logs
----------------------------------------
essage Time            Level   Source                  Message
9/29/17 5:36:24 PM      Info    Manager Attempting to connect to agent 10.66.177.83 at port 1167
9/29/17 5:36:24 PM      Info    Manager Connected to agent 10.66.177.83 at port 1167 successfully
9/29/17 5:36:25 PM      Info    Protected Machine       Agent Version 6.4.1.120
9/29/17 5:36:25 PM      Info    Protected Machine       Connection authenticated; Waiting for command.
9/29/17 5:36:25 PM      Info    Protected Machine       Executing get_mysql_instance_configuration_request request...
9/29/17 5:36:25 PM      Info    Manager Restoring files to Agent required for selected databases
9/29/17 5:36:25 PM      Info    Manager Calculating restore size
9/29/17 5:36:25 PM      Info    Manager Calculation complete
9/29/17 5:36:25 PM      Info    Manager Calculated 0.0 bytes to restore (0 files)
9/29/17 5:36:25 PM      Info    Manager Calculating restore size
9/29/17 5:36:25 PM      Info    Manager Calculation complete
9/29/17 5:36:25 PM      Info    Manager Calculated 250.0 MB to restore (1 files)
9/29/17 5:36:25 PM      Info    Manager Calculating restore size
9/29/17 5:36:25 PM      Info    Manager Calculation complete
9/29/17 5:36:25 PM      Info    Manager Calculated 10.0 MB to restore (2 files)
9/29/17 5:36:25 PM      Info    Manager Restoring MySQL database files to '/var/lib/r1soft/tmp/r1soft-mysql-restore-tmp-47e045bb-37a6-4852-94fb-050b85b4f850'
9/29/17 5:36:25 PM      Info    Protected Machine       Command completed; Waiting for next command.
9/29/17 5:36:25 PM      Info    Protected Machine       Executing file restore request...
9/29/17 5:36:49 PM      Info    Manager File restore complete
9/29/17 5:36:49 PM      Info    Manager Setting up temporary MySQL instance
9/29/17 5:36:49 PM      Info    Protected Machine       Command completed; Waiting for next command.
9/29/17 5:36:49 PM      Info    Protected Machine       Executing mysql_start_restore request...
9/29/17 6:01:49 PM      Info    Protected Machine       Nonzero exit status 255 for '"/usr/sbin/r1soft/bin/r1soft-mysql-util" --wait-ping --hostname 'localhost' --port 3307 --user 'softlayerbackup'; error: Failed to connect to database: Access denied for user 'softlayerbackup'@'localhost' (using password: YES)
9/29/17 6:01:49 PM      Warn    Protected Machine       Nonzero exit status 255 for '"/usr/sbin/r1soft/bin/r1soft-mysql-util" --shutdown --hostname 'localhost' --port 3307 --user 'softlayerbackup'; error: Failed to connect to database: Access denied for user 'softlayerbackup'@'localhost' (using password: YES)
9/29/17 6:01:49 PM      Warn    Protected Machine       Secondary MySQL instance could not be shutdown; you must do so manually!
9/29/17 6:31:50 PM      Error   Manager Socket timed out after waiting for more than 1,800 seconds to read/write
9/29/17 6:31:50 PM      Info    Manager Task Finished


TEST 1. from agent (aka protected machines) to backup server (Manager)

/usr/sbin/r1soft/bin/r1soft-mysql-util --show-variables --hostname <>  --port 3306 --user 'root'

actual ([root@DB01Clone ~]# to backup01 10.111.53.206)
/usr/sbin/r1soft/bin/r1soft-mysql-util --show-variables --hostname 10.111.53.206 --port 3306 --user 'softlayerbackup' --pass ''

TEST 2. from backup server to agent

/usr/sbin/r1soft/bin/r1soft-mysql-util --show-variables --hostname 10.111.53.223 --port 3306 --user 'softlayerbackup' --pass ''

TEST 3.
firewall /etc/apf/allow_hosts.rules
to allow backup01 to access protected machines
tcp:in:d=3306:s=10.111.53.206
tcp:in:d=3307:s=10.111.53.206
tcp:in:d=1167:s=10.111.53.206

tcp:in:d=3306:s=10.111.53.223
tcp:in:d=3307:s=10.111.53.223
tcp:in:d=1167:s=10.111.53.223

port 3306 3307 and 1167

use nmap to test 


check contents on /usr/sbin/r1soft/log/server.log


1. /var/log/mariadb/mariadblog
2. nmap -sS localhost on bacup01
3. backup01 apf/allow_hosts.rules

d=1167:s=10.66.177.115/24
74=app01, 89=?, 83=uat001
d=1167:s=10.66.177.74/24
d=1167:s=10.66.177.89/24
d=1167:s=10.66.177.83/24


LOCATION OF R1SOFT LOGS 
/usr/sbin/r1soft/log/server.log

/usr/sbin/r1soft/bin/r1soft-mysql-util --verbose --flush --flush-lock --unlock --user <user> --pass <pass> --new-pass <new-pass> [--sock <socketfile> | --port <portnumber> ]


http://wiki.r1soft.com/display/TP/MySQL+Backup+Technology
restore
http://wiki.r1soft.com/display/ServerBackupManager/Restore+a+MySQL+database+to+the+original+location^M

5. host - restore to alt agent
uat001
localhost
3306

authentication - spec alt authentication cred
softlayerbackup

temp instance - spec alter connection info
database host localhost
database port 3306 or 3307

https://www.lowendtalk.com/discussions/tagged/backup

9/20/17 1:13:11 PM ?Info Protected Machine Command completed; Waiting for next command. 
9/20/17 1:13:11 PM ?Info Protected Machine Executing mysql_start_restore request... 
9/20/17 1:38:12 PM ?Info Protected Machine Nonzero exit status 255 for '"/usr/sbin/r1soft/bin/r1soft-mysql-util" --wait-ping --hostname 'localhost' --port 3307 --user 'softlayerbackup'; error: Failed to connect to database: Access denied for user 'softlayerbackup'@'localhost' (using password: YES) 
9/20/17 1:38:12 PM ?Warn  Protected Machine Nonzero exit status 255 for '"/usr/sbin/r1soft/bin/r1soft-mysql-util" --shutdown --hostname 'localhost' --port 3307 --user 'softlayerbackup'; error: Failed to connect to database: Access denied for user 'softlayerbackup'@'localhost' (using password: YES) 
9/20/17 1:38:12 PM ?Warn Protected Machine  Secondary MySQL instance could not be shutdown; you must do so manually! 


To test from agent login to R1soft
"/usr/sbin/r1soft/bin/r1soft-mysql-util" --show-variables --hostname 'localhost' --port 3306 --user 'softlayerbackup' --pass ''

