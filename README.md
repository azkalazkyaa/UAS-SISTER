# UAS-SISTER

## Ansible

  ## Create lxc 

 ![lxc1](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/LXC%20PADA%20ANSIBLE.jpeg)
 ![lxc2](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/LXC%20PADA%20ANSIBLE%202.jpeg)
## mariadb.yml ini untuk menginstall database mysql pada lxc server
 ![db1](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/DB%201.jpeg)
 ![db2](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/DB%202.jpeg)
  ![db3](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/DB%203.jpeg)

```
 These groups are read by MariaDB server.
 Use it for options that only the server (but not clients) should see

 See the examples of server my.cnf files in /usr/share/mysql/


# this is read by the standalone daemon and embedded servers
[server]

# this is only for the mysqld standalone daemon
[mysqld]


# Basic Settings

user            = mysql
pid-file        = /var/run/mysqld/mysqld.pid
socket          = /var/run/mysqld/mysqld.sock
port            = 3306
basedir         = /usr
datadir         = /var/lib/mysql
tmpdir          = /tmp
lc-messages-dir = /usr/share/mysql
skip-external-locking
Instead of skip-networking the default is now to listen only on
localhost which is more compatible and is not less secure.
bind-address            = 0.0.0.0

Fine Tuning

key_buffer_size         = 16M
max_allowed_packet      = 16M
thread_stack            = 192K
thread_cache_size       = 8
This replaces the startup script and checks MyISAM tables if needed
the first time they are touched
myisam_recover_options  = BACKUP
#max_connections        = 100
#table_cache            = 64
#thread_concurrency     = 10


 * Query Cache Configuration

query_cache_limit       = 1M
query_cache_size        = 16M


 * Logging and Replication
 Both location gets rotated by the cronjob.
 Be aware that this log type is a performance killer.
 As of 5.1 you can enable the log at runtime!
#general_log_file        = /var/log/mysql/mysql.log
#general_log             = 1
#
# Error log - should be very few entries.
#
log_error = /var/log/mysql/error.log
#
# Enable the slow query log to see queries with especially long duration
#slow_query_log_file    = /var/log/mysql/mariadb-slow.log
#long_query_time = 10
#log_slow_rate_limit    = 1000
#log_slow_verbosity     = query_plan
#log-queries-not-using-indexes
#
# The following can be used as easy to replay backup logs or for replication.
# note: if you are setting up a replication slave, see README.Debian about
#       other settings you may need to change.
#server-id              = 1
#log_bin                        = /var/log/mysql/mysql-bin.log
expire_logs_days        = 10
max_binlog_size   = 100M
#binlog_do_db           = include_database_name
#binlog_ignore_db       = exclude_database_name

#
# * InnoDB
#
# InnoDB is enabled by default with a 10MB datafile in /var/lib/mysql/.
# Read the manual for more InnoDB related options. There are many!

#
# * Security Features
#
# Read the manual, too, if you want chroot!
# chroot = /var/lib/mysql/
#
# For generating SSL certificates you can use for example the GUI tool "tinyca".
#
# ssl-ca=/etc/mysql/cacert.pem
# ssl-cert=/etc/mysql/server-cert.pem
# ssl-key=/etc/mysql/server-key.pem
#
# Accept only connections using the latest and most secure TLS protocol version.
# ..when MariaDB is compiled with OpenSSL:
# ssl-cipher=TLSv1.2
# ..when MariaDB is compiled with YaSSL (default in Debian):
# ssl=on

#
# * Character sets
#
# MySQL/MariaDB default is Latin1, but in Debian we rather default to the full
# utf8 4-byte character set. See also client.cnf
#
character-set-server  = utf8mb4
collation-server      = utf8mb4_general_ci

#
# * Unix socket authentication plugin is built-in since 10.0.22-6
#
# Needed so the root database user can authenticate without a password but
# only when running as the unix root user.
#
# Also available for other users if required.
# See https://mariadb.com/kb/en/unix_socket-authentication-plugin/

# this is only for embedded server
[embedded]

# This group is only read by MariaDB servers, not by MySQL.
# If you use the same .cnf file for MySQL and MariaDB,
# you can put MariaDB-only options here
[mariadb]
  ## membuat hosts di mana agar ansible bisa mengakses lxc untuk penginstalan otomatis
  ![host1](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/membuat%20host%20di%20ansible.jpeg)
  ## app.yml di mana ini menginstal Code Igniter
  ![ci1](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/Install%20code%20igniters%20dan%20dependencies%201.jpeg)
  ![ci2](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/Install%20code%20igniters%20dan%20dependencies%202.jpeg)
## app.conf.j2 untuk konfigurasi nginx code ingniter
  ![app.conf.j2](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/app.confi.j2.jpeg)
```



 
