# UAS-SISTER

# Ansible

# Create lxc 

 ![lxc1](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/LXC%20PADA%20ANSIBLE.jpeg)
 ![lxc2](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/LXC%20PADA%20ANSIBLE%202.jpeg)
# mariadb.yml ini untuk menginstall database mysql pada lxc server ``kelompok15.local/phpmyadmin``
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
```
### hasil mariadb 
![db1](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/db1.png)
![db2](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/db2.png)
## ini file sites.conf.j2
```
server {
    listen 80;

      server_name {{ domain }};

      root /usr/share/phpMyAdmin;

      index index.php;

      location / {

           try_files $uri $uri/ @phpmyadmin;

      }
      location @phpmyadmin {
              fastcgi_pass unix:/run/php/php7.2-fpm.sock;   #Sesuaikan dengan versi PHP

              fastcgi_param SCRIPT_FILENAME /usr/share/phpMyAdmin/index.php;

              include /etc/nginx/fastcgi_params;

              fastcgi_param SCRIPT_NAME /index.php;
      }
      location ~ \.php$ {

              fastcgi_pass unix:/run/php/php7.2-fpm.sock;  #Sesuaikan dengan versi PHP

              fastcgi_index index.php;

              fastcgi_param SCRIPT_FILENAME /usr/share/phpMyAdmin$fastcgi_script_name;

              include fastcgi_params;

      }
  }
```

  ## membuat hosts di mana agar ansible bisa mengakses lxc untuk penginstalan otomatis
  ![host1](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/membuat%20host%20di%20ansible.jpeg)
# Penginstalan CI ``kelompok15.local/app``
## app.yml
  ![ci1](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/Install%20code%20igniters%20dan%20dependencies%201.jpeg)
  ![ci2](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/Install%20code%20igniters%20dan%20dependencies%202.jpeg)
## app.conf.j2 untuk konfigurasi nginx code ingniter
  ![app.conf.j2](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/app.confi.j2.jpeg)

### hasil code ingniter
  ![ci](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/cii.png)

# penginstallan wordprees `news.kelompok15.local`

## file `nano wp.yml`
 ```
---
- hosts: lxc_php7_1W
  vars:
    username: 'admin'
    password: 'admin'
    domain: 'lxc_php7_1W.dev'
  roles:
    - wp

- hosts: lxc_php7_2W
  vars:
    username: 'admin'
    password: 'admin'
    domain: 'lxc_php7_2W.dev'
  roles:
    - wp

- hosts: lxc_php7_4W
  vars:
    username: 'admin'
    password: 'admin'
    domain: 'lxc_php7_4W.dev'
  roles:
    - wp

- hosts: lxc_php7_6W
  vars:
    username: 'admin'
    password: 'admin'
    domain: 'lxc_php7_6W.dev'
  roles:
    - wp
 ```

## ansible untuk wordpress  
```
sudo mkdir -p wordpress /tasks
sudo mkdir -p wordpress /handlers
sudo mkdir -p wordpress /templates
```
## folder task/main.yml
```
---
- name: delete apt chache
  become: yes
  become_user: root
  become_method: su
  command: rm -vf /var/lib/apt/lists/*

- name: install requirement
  become: yes
  become_user: root
  become_method: su
  apt: name={{ item }} state=latest update_cache=true
  with_items:
    - nginx
    - nginx-extras
    - curl
    - wget
    - php7.4
    - php7.4-fpm
    - php7.4-curl
    - php7.4-xml
    - php7.4-gd
    - php7.4-opcache
    - php7.4-mbstring
    - php7.4-zip
    - php7.4-json
    - php7.4-cli
    - php7.4-mysqlnd
    - php7.4-xmlrpc
    - php7.4-curl

- name: wget wordpress
  shell: wget -c http://wordpress.org/latest.tar.gz

- name: tar latest.tar.gz
  shell: tar -xvzf latest.tar.gz

- name: copy folder wordpress
  shell: cp -R wordpress /var/www/html/blog

- name: chmod
  become: yes
  become_user: root
  become_method: su
  command: chmod 775 -R /var/www/html/blog/

- name: copy .wp-config.conf
  template:
    src=templates/wp.conf.j2
    dest=/var/www/html/blog/wp-config.php

- name: copy wordpress.conf.j2
  template:
    src=templates/wordpress.conf.j2
    dest=/etc/nginx/sites-available/{{ domain }}
  vars:
    servername: '{{ domain }}'

- name: Symlink wordpress.conf
  command: ln -sfn /etc/nginx/sites-available/{{ domain }} /etc/nginx/sites-enabled/{{ domain }}
  notify:
    - restart nginx

- name: Write {{ domain }} to /etc/hosts
  lineinfile:
    dest: /etc/hosts
    regexp: '.*{{ domain }}$'
    line: "127.0.0.1 {{ domain }}"
    state: present

- name: enable module php mbstring
  command: phpenmod mbstring
  notify:
    - restart php
  ```
## folder handlers/main.yml

      
      ---
      - name: restart nginx
        become: yes
        become_user: root
        become_method: su
        action: service name=nginx state=restarted
      
      - name: restart php
        become: yes
        become_user: root
        become_method: su
        action: service name=php7.4-fpm state=restarted
      

  # Folder templates

  ## php7.conf.j2

  ```  
        ; Start a new pool named 'www'.
        ; the variable $pool can we used in any directive and will be replaced by the
        ; pool name ('www' here)
        [www]
        
        ; Per pool prefix
        ; It only applies on the following directives:
        ; - 'slowlog'
        ; - 'listen' (unixsocket)
        ; - 'chroot'
        ; - 'chdir'
        ; - 'php_values'
        ; - 'php_admin_values'
        ; When not set, the global prefix (or /usr) applies instead.
        ; Note: This directive can also be relative to the global prefix.
        ; Default Value: none
        ;prefix = /path/to/pools/$pool
        
        ; Unix user/group of processes
        ; Note: The user is mandatory. If the group is not set, the default user's group
        ;       will be used.
        user = www-data
        group = www-data
        
        ; The address on which to accept FastCGI requests.
        ; Valid syntaxes are:
        ;   'ip.add.re.ss:port'    - to listen on a TCP socket to a specific address on
        ;                            a specific port;
        ;   'port'                 - to listen on a TCP socket to all addresses on a
        ;                            specific port;
        ;   '/path/to/unix/socket' - to listen on a unix socket.
        ; Note: This value is mandatory.
        listen = 127.0.0.1:9001
        
        ; Set listen(2) backlog. A value of '-1' means unlimited.
        ; Default Value: 128 (-1 on FreeBSD and OpenBSD)
        ;listen.backlog = -1
        
        ; Set permissions for unix socket, if one is used. In Linux, read/write
        ; permissions must be set in order to allow connections from a web server. Many
        ; BSD-derived systems allow connections regardless of permissions.
        ; Default Values: user and group are set as the running user
        ;                 mode is set to 0666
        listen.owner = www-data
        listen.group = www-data
        listen.mode = 0666
        
        ; List of ipv4 addresses of FastCGI clients which are allowed to connect.
        ; Equivalent to the FCGI_WEB_SERVER_ADDRS environment variable in the original
        ; PHP FCGI (5.2.2+). Makes sense only with a tcp listening socket. Each address
        ; must be separated by a comma. If this value is left blank, connections will be
        ; accepted from any ip address.
        ; Default Value: any
        ;listen.allowed_clients = 127.0.0.1
        
        ; Choose how the process manager will control the number of child processes.
        ; Possible Values:
        ;   static  - a fixed number (pm.max_children) of child processes;
        ;   dynamic - the number of child processes are set dynamically based on the
        ;             following directives. With this process management, there will be
        ;             always at least 1 children.
        ;             pm.max_children      - the maximum number of children that can
        ;                                    be alive at the same time.
        ;             pm.start_servers     - the number of children created on startup.
        ;             pm.min_spare_servers - the minimum number of children in 'idle'
        ;                                    state (waiting to process). If the number
        ;                                    of 'idle' processes is less than this
        ;                                    number then some children will be created.
        ;             pm.max_spare_servers - the maximum number of children in 'idle'
        ;                                    state (waiting to process). If the number
        ;                                    of 'idle' processes is greater than this
        ;                                    number then some children will be killed.
        ;  ondemand - no children are created at startup. Children will be forked when
        ;             new requests will connect. The following parameter are used:
        ;             pm.max_children           - the maximum number of children that
        ;                                         can be alive at the same time.
        ;             pm.process_idle_timeout   - The number of seconds after which
        ;                                         an idle process will be killed.
        ; Note: This value is mandatory.
        pm = dynamic
        
        ; The number of child processes to be created when pm is set to 'static' and the
        ; maximum number of child processes when pm is set to 'dynamic' or 'ondemand'.
        ; This value sets the limit on the number of simultaneous requests that will be
        ; served. Equivalent to the ApacheMaxClients directive with mpm_prefork.
        ; Equivalent to the PHP_FCGI_CHILDREN environment variable in the original PHP
        ; CGI. The below defaults are based on a server without much resources. Don't
        ; forget to tweak pm.* to fit your needs.
        ; Note: Used when pm is set to 'static', 'dynamic' or 'ondemand'
        ; Note: This value is mandatory.
        pm.max_children = 5
        
        ; The number of child processes created on startup.
        ; Note: Used only when pm is set to 'dynamic'
        ; Default Value: min_spare_servers + (max_spare_servers - min_spare_servers) / 2
        pm.start_servers = 2
        
        ; The desired minimum number of idle server processes.
        ; Note: Used only when pm is set to 'dynamic'
        ; Note: Mandatory when pm is set to 'dynamic'
        pm.min_spare_servers = 1
        
        ; The desired maximum number of idle server processes.
        ; Note: Used only when pm is set to 'dynamic'
        ; Note: Mandatory when pm is set to 'dynamic'
        pm.max_spare_servers = 3
        
        ; The number of seconds after which an idle process will be killed.
        ; Note: Used only when pm is set to 'ondemand'
        ; Default Value: 10s
        ;pm.process_idle_timeout = 10s;
        
        ; The number of requests each child process should execute before respawning.
        ; This can be useful to work around memory leaks in 3rd party libraries. For
        ; endless request processing specify '0'. Equivalent to PHP_FCGI_MAX_REQUESTS.
        ; Default Value: 0
        pm.max_requests = 100
        
        ; The URI to view the FPM status page. If this value is not set, no URI will be
        ; recognized as a status page. It shows the following informations:
        ;   pool                 - the name of the pool;
        ;   process manager      - static, dynamic or ondemand;
        ;   start time           - the date and time FPM has started;
        ;   start since          - number of seconds since FPM has started;
        ;   accepted conn        - the number of request accepted by the pool;
        ;   listen queue         - the number of request in the queue of pending
        ;                          connections (see backlog in listen(2));
        ;   max listen queue     - the maximum number of requests in the queue
        ;                          of pending connections since FPM has started;
        ;   listen queue len     - the size of the socket queue of pending connections;
        ;   idle processes       - the number of idle processes;
        ;   active processes     - the number of active processes;
        ;   total processes      - the number of idle + active processes;
        ;   max active processes - the maximum number of active processes since FPM
        ;                          has started;
        ;   max children reached - number of times, the process limit has been reached,
        ;                          when pm tries to start more children (works only for
        ;                          pm 'dynamic' and 'ondemand');
        ; Value are updated in real time.
        ; Example output:
        ;   pool:                 www
        ;   process manager:      static
        ;   start time:           01/Jul/2011:17:53:49 +0200
        ;   start since:          62636
        ;   accepted conn:        190460
        ;   listen queue:         0
        ;   max listen queue:     1
        ;   listen queue len:     42
        ;   idle processes:       4
        ;   active processes:     11
        ;   total processes:      15
        ;   max active processes: 12
        ;   max children reached: 0
        ;
        ; By default the status page output is formatted as text/plain. Passing either
        ; 'html', 'xml' or 'json' in the query string will return the corresponding
        ; output syntax. Example:
        ;   http://www.foo.bar/status
        ;   http://www.foo.bar/status?json
        ;   http://www.foo.bar/status?html
        ;   http://www.foo.bar/status?xml
        ;
        ; By default the status page only outputs short status. Passing 'full' in the
        ; query string will also return status for each pool process.
        ; Example:
        ;   http://www.foo.bar/status?full
        ;   http://www.foo.bar/status?json&full
        ;   http://www.foo.bar/status?html&full
        ;   http://www.foo.bar/status?xml&full
        ; The Full status returns for each process:
        ;   pid                  - the PID of the process;
        ;   state                - the state of the process (Idle, Running, ...);
        ;   start time           - the date and time the process has started;
        ;   start since          - the number of seconds since the process has started;
        ;   requests             - the number of requests the process has served;
        ;   request duration     - the duration in µs of the requests;
        ;   request method       - the request method (GET, POST, ...);
        ;   request URI          - the request URI with the query string;
        ;   content length       - the content length of the request (only with POST);
        ;   user                 - the user (PHP_AUTH_USER) (or '-' if not set);
        ;   script               - the main script called (or '-' if not set);
        ;   last request cpu     - the %cpu the last request consumed
        ;                          it's always 0 if the process is not in Idle state
        ;                          because CPU calculation is done when the request
        ;                          processing has terminated;
        ;   last request memory  - the max amount of memory the last request consumed
        ;                          it's always 0 if the process is not in Idle state
        ;                          because memory calculation is done when the request
        ;                          processing has terminated;
        ; If the process is in Idle state, then informations are related to the
        ; last request the process has served. Otherwise informations are related to
        ; the current request being served.
        ; Example output:
        ;   ************************
        ;   pid:                  31330
        ;   state:                Running
        ;   start time:           01/Jul/2011:17:53:49 +0200
        ;   start since:          63087
        ;   requests:             12808
        ;   request duration:     1250261
        ;   request method:       GET
        ;   request URI:          /test_mem.php?N=10000
        ;   content length:       0
        ;   user:                 -
        ;   script:               /home/fat/web/docs/php/test_mem.php
        ;   last request cpu:     0.00
        ;   last request memory:  0
        ;
        ; Note: There is a real-time FPM status monitoring sample web page available
        ;       It's available in: ${prefix}/share/fpm/status.html
        ;
        ; Note: The value must start with a leading slash (/). The value can be
        ;       anything, but it may not be a good idea to use the .php extension or it
        ;       may conflict with a real PHP file.
        ; Default Value: not set
        pm.status_path = /php-status
        
        ; The ping URI to call the monitoring page of FPM. If this value is not set, no
        ; URI will be recognized as a ping page. This could be used to test from outside
        ; that FPM is alive and responding, or to
        ; - create a graph of FPM availability (rrd or such);
        ; - remove a server from a group if it is not responding (load balancing);
        ; - trigger alerts for the operating team (24/7).
        ; Note: The value must start with a leading slash (/). The value can be
        ;       anything, but it may not be a good idea to use the .php extension or it
        ;       may conflict with a real PHP file.
        ; Default Value: not set
        ;ping.path = /ping
        
        ; This directive may be used to customize the response of a ping request. The
        ; response is formatted as text/plain with a 200 response code.
        ; Default Value: pong
        ;ping.response = pong
        
        ; The access log file
        ; Default: not set
        ;access.log = log/$pool.access.log
        
        ; The access log format.
        ; The following syntax is allowed
        ;  %%: the '%' character
        ;  %C: %CPU used by the request
        ;      it can accept the following format:
        ;      - %{user}C for user CPU only
        ;      - %{system}C for system CPU only
        ;      - %{total}C  for user + system CPU (default)
        ;  %d: time taken to serve the request
        ;      it can accept the following format:
        ;      - %{seconds}d (default)
        ;      - %{miliseconds}d
        ;      - %{mili}d
        ;      - %{microseconds}d
        ;      - %{micro}d
        ;  %e: an environment variable (same as $_ENV or $_SERVER)
        ;      it must be associated with embraces to specify the name of the env
        ;      variable. Some exemples:
        ;      - server specifics like: %{REQUEST_METHOD}e or %{SERVER_PROTOCOL}e
        ;      - HTTP headers like: %{HTTP_HOST}e or %{HTTP_USER_AGENT}e
        ;  %f: script filename
        ;  %l: content-length of the request (for POST request only)
        ;  %m: request method
        ;  %M: peak of memory allocated by PHP
        ;      it can accept the following format:
        ;      - %{bytes}M (default)
        ;      - %{kilobytes}M
        ;      - %{kilo}M
        ;      - %{megabytes}M
        ;      - %{mega}M
        ;  %n: pool name
        ;  %o: ouput header
        ;      it must be associated with embraces to specify the name of the header:
        ;      - %{Content-Type}o
        ;      - %{X-Powered-By}o
        ;      - %{Transfert-Encoding}o
        ;      - ....
        ;  %p: PID of the child that serviced the request
        ;  %P: PID of the parent of the child that serviced the request
        ;  %q: the query string
        ;  %Q: the '?' character if query string exists
        ;  %r: the request URI (without the query string, see %q and %Q)
        ;  %R: remote IP address
        ;  %s: status (response code)
        ;  %t: server time the request was received
        ;      it can accept a strftime(3) format:
        ;      %d/%b/%Y:%H:%M:%S %z (default)
        ;  %T: time the log has been written (the request has finished)
        ;      it can accept a strftime(3) format:
        ;      %d/%b/%Y:%H:%M:%S %z (default)
        ;  %u: remote user
        ;
        ; Default: "%R - %u %t \"%m %r\" %s"
        ;access.format = %R - %u %t "%m %r%Q%q" %s %f %{mili}d %{kilo}M %C%%
        
        ; The log file for slow requests
        ; Default Value: not set
        ; Note: slowlog is mandatory if request_slowlog_timeout is set
        ;slowlog = log/$pool.log.slow
        
        ; The timeout for serving a single request after which a PHP backtrace will be
        ; dumped to the 'slowlog' file. A value of '0s' means 'off'.
        ; Available units: s(econds)(default), m(inutes), h(ours), or d(ays)
        ; Default Value: 0
        ;request_slowlog_timeout = 0
        
        ; The timeout for serving a single request after which the worker process will
        ; be killed. This option should be used when the 'max_execution_time' ini option
        ; does not stop script execution for some reason. A value of '0' means 'off'.
        ; Available units: s(econds)(default), m(inutes), h(ours), or d(ays)
        ; Default Value: 0
        ;request_terminate_timeout = 0
        
        ; Set open file descriptor rlimit.
        ; Default Value: system defined value
        ;rlimit_files = 1024
        
        ; Set max core size rlimit.
        ; Possible Values: 'unlimited' or an integer greater or equal to 0
        ; Default Value: system defined value
        ;rlimit_core = 0
        
        ; Chroot to this directory at the start. This value must be defined as an
        ; absolute path. When this value is not set, chroot is not used.
        ; Note: you can prefix with '$prefix' to chroot to the pool prefix or one
        ; of its subdirectories. If the pool prefix is not set, the global prefix
        ; will be used instead.
        ; Note: chrooting is a great security feature and should be used whenever
        ;       possible. However, all PHP paths will be relative to the chroot
        ;       (error_log, sessions.save_path, ...).
        ; Default Value: not set
        ;chroot =
        
        ; Chdir to this directory at the start.
        ; Note: relative path can be used.
        ; Default Value: current directory or / when chroot
        chdir = /
        
        ; Redirect worker stdout and stderr into main error log. If not set, stdout and
        ; stderr will be redirected to /dev/null according to FastCGI specs.
        ; Note: on highloaded environement, this can cause some delay in the page
        ; process time (several ms).
        ; Default Value: no
        catch_workers_output = yes
        
        ; Limits the extensions of the main script FPM will allow to parse. This can
        ; prevent configuration mistakes on the web server side. You should only limit
        ; FPM to .php extensions to prevent malicious users to use other extensions to
        ; exectute php code.
        ; Note: set an empty value to allow all extensions.
        ; Default Value: .php
        ;security.limit_extensions = .php .php3 .php4 .php5 .php7
        
        ; Pass environment variables like LD_LIBRARY_PATH. All $VARIABLEs are taken from
        ; the current environment.
        ; Default Value: clean env
        ;env[HOSTNAME] = $HOSTNAME
        env[PATH] = /srv/www/phpcs/scripts/:/usr/local/bin:/usr/bin:/bin
        ;env[TMP] = /tmp
        ;env[TMPDIR] = /tmp
        ;env[TEMP] = /tmp
        
        ; Additional php.ini defines, specific to this pool of workers. These settings
        ; overwrite the values previously defined in the php.ini. The directives are the
        ; same as the PHP SAPI:
        ;   php_value/php_flag             - you can set classic ini defines which can
        ;                                    be overwritten from PHP call 'ini_set'.
        ;   php_admin_value/php_admin_flag - these directives won't be overwritten by
        ;                                     PHP call 'ini_set'
        ; For php_*flag, valid values are on, off, 1, 0, true, false, yes or no.
        
        ; Defining 'extension' will load the corresponding shared extension from
        ; extension_dir. Defining 'disable_functions' or 'disable_classes' will not
        ; overwrite previously defined php.ini values, but will append the new value
        ; instead.
        
        ; Note: path INI options can be relative and will be expanded with the prefix
        ; (pool, global or /usr)
        
        ; Default Value: nothing is defined by default except the values in php.ini and
        ;                specified at startup with the -d argument
        ;php_admin_value[sendmail_path] = /usr/sbin/sendmail -t -i -f www@my.domain.com
        ;php_flag[display_errors] = off
        ;php_admin_value[error_log] = /var/log/fpm-php.www.log
        ;php_admin_flag[log_errors] = on
        ;php_admin_value[memory_limit] = 32M
        
```
  ## wordpress.conf.j2

        ```
        server {
             listen 80;
             listen [::]:80;
        
             # Log files for Debugging
             access_log /var/log/nginx/wordpress-access.log;
             error_log /var/log/nginx/wordpress-error.log;
        
             # Webroot Directory for Laravel project
             root /var/www/html/wordpress;
             index index.php index.html index.htm;
        
             # Your Domain Name
             server_name {{ domain }};
        
             location / {
                     try_files $uri $uri/ /index.php?$query_string;
             }
        
             # PHP-FPM Configuration Nginx
             location ~ \.php$ {
                     try_files $uri =404;
                     fastcgi_split_path_info ^(.+\.php)(/.+)$;
                     fastcgi_pass 127.0.0.1:9001;
                     fastcgi_index index.php;
                     fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
                     include fastcgi_params;
             }
        }
        

  ### wp.conf.j2

      ```  
        <?php
        /**
         * The base configuration for WordPress
         *
         * The wp-config.php creation script uses this file during the installation.
         * You don't have to use the web site, you can copy this file to "wp-config.php"
         * and fill in the values.
         *
         * This file contains the following configurations:
         *
         * * MySQL settings
         * * Secret keys
         * * Database table prefix
         * * ABSPATH
         *
         * @link https://wordpress.org/support/article/editing-wp-config-php/
         *
         * @package WordPress
         */
        
        define( 'WP_HOME', 'http://news.kelompok12.fpsas' );
        define( 'WP_SITEURL', 'http://news.kelompok12.fpsas' );
        
        // ** MySQL settings - You can get this info from your web host ** //
        /** The name of the database for WordPress */
        define( 'DB_NAME', 'blog' );
        
        /** MySQL database username */
        define( 'DB_USER', 'admin' );
        
        /** MySQL database password */
        define( 'DB_PASSWORD', '10.0.3.46' );
        
        /** MySQL hostname */
        define( 'DB_HOST', '10.0.3.46' );
        /** Database charset to use in creating database tables. */
        define( 'DB_CHARSET', 'utf8' );
        
        /** The database collate type. Don't change this if in doubt. */
        define( 'DB_COLLATE', '' );
        
        /**#@+
         * Authentication unique keys and salts.
         *
         * Change these to different unique phrases! You can generate these using
         * the {@link https://api.wordpress.org/secret-key/1.1/salt/ WordPress.org secret-key service}.
         *
         * You can change these at any point in time to invalidate all existing cookies.
         * This will force all users to have to log in again.
         *
         * @since 2.6.0
         */
        define( 'AUTH_KEY',         'put your unique phrase here' );
        define( 'SECURE_AUTH_KEY',  'put your unique phrase here' );
        define( 'LOGGED_IN_KEY',    'put your unique phrase here' );
        define( 'NONCE_KEY',        'put your unique phrase here' );
        define( 'AUTH_SALT',        'put your unique phrase here' );
        define( 'SECURE_AUTH_SALT', 'put your unique phrase here' );
        define( 'LOGGED_IN_SALT',   'put your unique phrase here' );
        define( 'NONCE_SALT',       'put your unique phrase here' );
        
        /**#@-*/
        
        /**
         * WordPress database table prefix.
         *
         * You can have multiple installations in one database if you give each
         * a unique prefix. Only numbers, letters, and underscores please!
         */
        $table_prefix = 'wp_';
        /**
         * For developers: WordPress debugging mode.
         *
         * Change this to true to enable the display of notices during development.
         * It is strongly recommended that plugin and theme developers use WP_DEBUG
         * in their development environments.
         *
         * For information on other constants that can be used for debugging,
         * visit the documentation.
         *
         * @link https://wordpress.org/support/article/debugging-in-wordpress/
         */
        define( 'WP_DEBUG', false );
        
        /* Add any custom values between this line and the "stop editing" line. */
        
        
        
        /* That's all, stop editing! Happy publishing. */
        
        /** Absolute path to the WordPress directory. */
        if ( ! defined( 'ABSPATH' ) ) {
                define( 'ABSPATH', __DIR__ . '/' );
        }
        
        /** Sets up WordPress vars and included files. */
        require_once ABSPATH . 'wp-settings.php';
        ```

### hasil wordprees
  ![wp1](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/wp1.png)
  ![wp2](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/wp2.png)

# Penginstalan Laravel `kelompok15.local`

## file penginstalan nano laravel.yml 

    
    ---
    - hosts: lxc_php7_2L
        vars:
            username: 'admin'
            password: 'admin'
            domain: 'lxc_php7_2L.dev'
        roles:
            - php
            - laravel

        - hosts: lxc_php7_3L
        vars:
            username: 'admin'
            password: 'admin'
            domain: 'lxc_php7_3L.dev'
        roles:
            - php
            - laravel

        - hosts: lxc_php7_4L
        vars:
            username: 'admin'
            password: 'admin'
            domain: 'lxc_php7_4L.dev'
        roles:
            - php
            - laravel

        - hosts: lxc_php7_5L
        vars:
            username: 'admin'
            password: 'admin'
            domain: 'lxc_php7_5L.dev'
        roles:
            - php
            - laravel
    
## folder laravel

      
      sudo mkdir -p laravel/tasks
      sudo mkdir -p laravel/handlers
      sudo mkdir -p laravel/templates
      

## tasks/main.yml

      
        ---
          - name: delete apt chache
            become: yes
            become_user: root
            become_method: su
            command: rm -vf /var/lib/apt/lists/*
  
          - name: Download and install Composer
            shell: curl -sS https://getcomposer.org/installer | php
            args:
                chdir: /usr/src/
                creates: /usr/local/bin/composer
            become: yes
  
          - name: Add Composer to global path
            copy:
                dest: /usr/local/bin/composer
                group: root
                mode: '0755'
                owner: root
                src: /usr/src/composer.phar
                remote_src: yes
            become: yes
  
          - name: Ansible delete file create-project
            file:
                path: /var/www/html/laravel
                state: absent
  
          - name: composer create-project
            shell: /usr/local/bin/composer create-project laravel/laravel /var/www/html/laravel --prefer-dist --no-interaction
    
          - name: Copy .env.template
            template:
                src=templates/env.templates
                dest=/var/www/html/laravel/.env
    
          - name: composer
            shell: cd /var/www/html/laravel; /usr/local/bin/composer install  --no-interaction
  
          - name: key
            shell: /usr/bin/php7.4 /var/www/html/laravel/artisan key:generate
  
          - name: chmod
            become: yes
            become_user: root
            become_method: su
            command: chmod 777 -R /var/www/html/laravel/storage
    
          - name: Copy lv.conf
            template:
                src=templates/lv.conf.j2
                dest=/etc/nginx/sites-available/{{ domain }}
            vars:
                servername: '{{ domain }}'
  
          - name: copy php7.conf
            template:
                src=templates/php7.conf.j2
                dest=/etc/php/7.4/fpm/pool.d/www.conf
  
          - name: Symlink lv.conf
            command: ln -sfn /etc/nginx/sites-available/{{ domain }} /etc/nginx/sites-enabled/{{ domain }}
            notify:
                - restart nginx
  
          - name: Write {{ domain }} to /etc/hosts
            lineinfile:
                dest: /etc/hosts
                regexp: '.*{{ domain }}$'
                line: "127.0.0.1 {{ domain }}"
                state: present

      

## handler/main.yml

      
      ---
      - name: restart php
        become: yes
        become_user: root
        become_method: su
        action: service name=php7.4-fpm state=restarted
      
      - name: restart nginx
        become: yes
        become_user: root
        become_method: su
        action: service name=nginx state=restarted
      

## templates/

### env.templates

        
        APP_NAME=Landing
        APP_ENV=local
        APP_KEY=
        APP_DEBUG=true
        APP_URL=http://kelompok12.fpsas
        
        LOG_CHANNEL=stack
        LOG_DEPRECATIONS_CHANNEL=null
        LOG_LEVEL=debug
        
        DB_CONNECTION=mysql
        DB_HOST=10.0.3.46
        DB_PORT=3306
        DB_DATABASE=landing
        DB_USERNAME=admin
        DB_PASSWORD=admin
        
        BROADCAST_DRIVER=log
        CACHE_DRIVER=file
        FILESYSTEM_DRIVER=local
        QUEUE_CONNECTION=sync
        SESSION_DRIVER=file
        SESSION_LIFETIME=120
        
        MEMCACHED_HOST=127.0.0.1
        
        REDIS_HOST=127.0.0.1
        REDIS_PASSWORD=null
        REDIS_PORT=6379
        
        MAIL_MAILER=smtp
        MAIL_HOST=mailhog
        MAIL_PORT=1025
        MAIL_USERNAME=null
        MAIL_PASSWORD=null
        MAIL_ENCRYPTION=null
        MAIL_FROM_ADDRESS=null
        MAIL_FROM_NAME="${APP_NAME}"
        
        AWS_ACCESS_KEY_ID=
        AWS_SECRET_ACCESS_KEY=
        AWS_DEFAULT_REGION=us-east-1
        AWS_BUCKET=
        AWS_USE_PATH_STYLE_ENDPOINT=false
        
        PUSHER_APP_ID=
        PUSHER_APP_KEY=
        PUSHER_APP_SECRET=
        PUSHER_APP_CLUSTER=mt1
        
        MIX_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
        MIX_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"
        

### lv.conf.j2

        
        server {
             listen 80;
             listen [::]:80;
        
             # Log files for Debugging
             access_log /var/log/nginx/laravel-access.log;
             error_log /var/log/nginx/laravel-error.log;
        
             # Webroot Directory for Laravel project
             root /var/www/html/laravel/public;
             index index.php index.html index.htm;
        
             # Your Domain Name
             server_name {{ domain }};
        
             location / {
                     try_files $uri $uri/ /index.php?$query_string;
             }
        
             # PHP-FPM Configuration Nginx
             location ~ \.php$ {
                     try_files $uri =404;
                     fastcgi_split_path_info ^(.+\.php)(/.+)$;
                     fastcgi_pass 127.0.0.1:9001;
                     fastcgi_index index.php;
                     fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
                     include fastcgi_params;
             }
        }
        

### php7.conf.j2

        
        ; Start a new pool named 'www'.
        ; the variable $pool can we used in any directive and will be replaced by the
        ; pool name ('www' here)
        [www]
        
        ; Per pool prefix
        ; It only applies on the following directives:
        ; - 'slowlog'
        ; - 'listen' (unixsocket)
        ; - 'chroot'
        ; - 'chdir'
        ; - 'php_values'
        ; - 'php_admin_values'
        ; When not set, the global prefix (or /usr) applies instead.
        ; Note: This directive can also be relative to the global prefix.
        ; Default Value: none
        ;prefix = /path/to/pools/$pool
        
        ; Unix user/group of processes
        ; Note: The user is mandatory. If the group is not set, the default user's group
        ;       will be used.
        user = www-data
        group = www-data
        
        ; The address on which to accept FastCGI requests.
        ; Valid syntaxes are:
        ;   'ip.add.re.ss:port'    - to listen on a TCP socket to a specific address on
        ;                            a specific port;
        ;   'port'                 - to listen on a TCP socket to all addresses on a
        ;                            specific port;
        ;   '/path/to/unix/socket' - to listen on a unix socket.
        ; Note: This value is mandatory.
        listen = 127.0.0.1:9001
        
        ; Set listen(2) backlog. A value of '-1' means unlimited.
        ; Default Value: 128 (-1 on FreeBSD and OpenBSD)
        ;listen.backlog = -1
        
        ; Set permissions for unix socket, if one is used. In Linux, read/write
        ; permissions must be set in order to allow connections from a web server. Many
        ; BSD-derived systems allow connections regardless of permissions.
        ; Default Values: user and group are set as the running user
        ;                 mode is set to 0666
        listen.owner = www-data
        listen.group = www-data
        listen.mode = 0666
        
        ; List of ipv4 addresses of FastCGI clients which are allowed to connect.
        ; Equivalent to the FCGI_WEB_SERVER_ADDRS environment variable in the original
        ; PHP FCGI (5.2.2+). Makes sense only with a tcp listening socket. Each address
        ; must be separated by a comma. If this value is left blank, connections will be
        ; accepted from any ip address.
        ; Default Value: any
        ;listen.allowed_clients = 127.0.0.1
        
        ; Choose how the process manager will control the number of child processes.
        ; Possible Values:
        ;   static  - a fixed number (pm.max_children) of child processes;
        ;   dynamic - the number of child processes are set dynamically based on the
        ;             following directives. With this process management, there will be
        ;             always at least 1 children.
        ;             pm.max_children      - the maximum number of children that can
        ;                                    be alive at the same time.
        ;             pm.start_servers     - the number of children created on startup.
        ;             pm.min_spare_servers - the minimum number of children in 'idle'
        ;                                    state (waiting to process). If the number
        ;                                    of 'idle' processes is less than this
        ;                                    number then some children will be created.
        ;             pm.max_spare_servers - the maximum number of children in 'idle'
        ;                                    state (waiting to process). If the number
        ;                                    of 'idle' processes is greater than this
        ;                                    number then some children will be killed.
        ;  ondemand - no children are created at startup. Children will be forked when
        ;             new requests will connect. The following parameter are used:
        ;             pm.max_children           - the maximum number of children that
        ;                                         can be alive at the same time.
        ;             pm.process_idle_timeout   - The number of seconds after which
        ;                                         an idle process will be killed.
        ; Note: This value is mandatory.
        pm = dynamic
        
        ; The number of child processes to be created when pm is set to 'static' and the
        ; maximum number of child processes when pm is set to 'dynamic' or 'ondemand'.
        ; This value sets the limit on the number of simultaneous requests that will be
        ; served. Equivalent to the ApacheMaxClients directive with mpm_prefork.
        ; Equivalent to the PHP_FCGI_CHILDREN environment variable in the original PHP
        ; CGI. The below defaults are based on a server without much resources. Don't
        ; forget to tweak pm.* to fit your needs.
        ; Note: Used when pm is set to 'static', 'dynamic' or 'ondemand'
        ; Note: This value is mandatory.
        pm.max_children = 5
        
        ; The number of child processes created on startup.
        ; Note: Used only when pm is set to 'dynamic'
        ; Default Value: min_spare_servers + (max_spare_servers - min_spare_servers) / 2
        pm.start_servers = 2
        
        ; The desired minimum number of idle server processes.
        ; Note: Used only when pm is set to 'dynamic'
        ; Note: Mandatory when pm is set to 'dynamic'
        pm.min_spare_servers = 1
        
        ; The desired maximum number of idle server processes.
        ; Note: Used only when pm is set to 'dynamic'
        ; Note: Mandatory when pm is set to 'dynamic'
        pm.max_spare_servers = 3
        
        ; The number of seconds after which an idle process will be killed.
        ; Note: Used only when pm is set to 'ondemand'
        ; Default Value: 10s
        ;pm.process_idle_timeout = 10s;
        
        ; The number of requests each child process should execute before respawning.
        ; This can be useful to work around memory leaks in 3rd party libraries. For
        ; endless request processing specify '0'. Equivalent to PHP_FCGI_MAX_REQUESTS.
        ; Default Value: 0
        pm.max_requests = 100
        
        ; The URI to view the FPM status page. If this value is not set, no URI will be
        ; recognized as a status page. It shows the following informations:
        ;   pool                 - the name of the pool;
        ;   process manager      - static, dynamic or ondemand;
        ;   start time           - the date and time FPM has started;
        ;   start since          - number of seconds since FPM has started;
        ;   accepted conn        - the number of request accepted by the pool;
        ;   listen queue         - the number of request in the queue of pending
        ;                          connections (see backlog in listen(2));
        ;   max listen queue     - the maximum number of requests in the queue
        ;                          of pending connections since FPM has started;
        ;   listen queue len     - the size of the socket queue of pending connections;
        ;   idle processes       - the number of idle processes;
        ;   active processes     - the number of active processes;
        ;   total processes      - the number of idle + active processes;
        ;   max active processes - the maximum number of active processes since FPM
        ;                          has started;
        ;   max children reached - number of times, the process limit has been reached,
        ;                          when pm tries to start more children (works only for
        ;                          pm 'dynamic' and 'ondemand');
        ; Value are updated in real time.
        ; Example output:
        ;   pool:                 www
        ;   process manager:      static
        ;   start time:           01/Jul/2011:17:53:49 +0200
        ;   start since:          62636
        ;   accepted conn:        190460
        ;   listen queue:         0
        ;   max listen queue:     1
        ;   listen queue len:     42
        ;   idle processes:       4
        ;   active processes:     11
        ;   total processes:      15
        ;   max active processes: 12
        ;   max children reached: 0
        ;
        ; By default the status page output is formatted as text/plain. Passing either
        ; 'html', 'xml' or 'json' in the query string will return the corresponding
        ; output syntax. Example:
        ;   http://www.foo.bar/status
        ;   http://www.foo.bar/status?json
        ;   http://www.foo.bar/status?html
        ;   http://www.foo.bar/status?xml
        ;
        ; By default the status page only outputs short status. Passing 'full' in the
        ; query string will also return status for each pool process.
        ; Example:
        ;   http://www.foo.bar/status?full
        ;   http://www.foo.bar/status?json&full
        ;   http://www.foo.bar/status?html&full
        ;   http://www.foo.bar/status?xml&full
        ; The Full status returns for each process:
        ;   pid                  - the PID of the process;
        ;   state                - the state of the process (Idle, Running, ...);
        ;   start time           - the date and time the process has started;
        ;   start since          - the number of seconds since the process has started;
        ;   requests             - the number of requests the process has served;
        ;   request duration     - the duration in µs of the requests;
        ;   request method       - the request method (GET, POST, ...);
        ;   request URI          - the request URI with the query string;
        ;   content length       - the content length of the request (only with POST);
        ;   user                 - the user (PHP_AUTH_USER) (or '-' if not set);
        ;   script               - the main script called (or '-' if not set);
        ;   last request cpu     - the %cpu the last request consumed
        ;                          it's always 0 if the process is not in Idle state
        ;                          because CPU calculation is done when the request
        ;                          processing has terminated;
        ;   last request memory  - the max amount of memory the last request consumed
        ;                          it's always 0 if the process is not in Idle state
        ;                          because memory calculation is done when the request
        ;                          processing has terminated;
        ; If the process is in Idle state, then informations are related to the
        ; last request the process has served. Otherwise informations are related to
        ; the current request being served.
        ; Example output:
        ;   ************************
        ;   pid:                  31330
        ;   state:                Running
        ;   start time:           01/Jul/2011:17:53:49 +0200
        ;   start since:          63087
        ;   requests:             12808
        ;   request duration:     1250261
        ;   request method:       GET
        ;   request URI:          /test_mem.php?N=10000
        ;   content length:       0
        ;   user:                 -
        ;   script:               /home/fat/web/docs/php/test_mem.php
        ;   last request cpu:     0.00
        ;   last request memory:  0
        ;
        ; Note: There is a real-time FPM status monitoring sample web page available
        ;       It's available in: ${prefix}/share/fpm/status.html
        ;
        ; Note: The value must start with a leading slash (/). The value can be
        ;       anything, but it may not be a good idea to use the .php extension or it
        ;       may conflict with a real PHP file.
        ; Default Value: not set
        pm.status_path = /php-status
        
        ; The ping URI to call the monitoring page of FPM. If this value is not set, no
        ; URI will be recognized as a ping page. This could be used to test from outside
        ; that FPM is alive and responding, or to
        ; - create a graph of FPM availability (rrd or such);
        ; - remove a server from a group if it is not responding (load balancing);
        ; - trigger alerts for the operating team (24/7).
        ; Note: The value must start with a leading slash (/). The value can be
        ;       anything, but it may not be a good idea to use the .php extension or it
        ;       may conflict with a real PHP file.
        ; Default Value: not set
        ;ping.path = /ping
        
        ; This directive may be used to customize the response of a ping request. The
        ; response is formatted as text/plain with a 200 response code.
        ; Default Value: pong
        ;ping.response = pong
        
        ; The access log file
        ; Default: not set
        ;access.log = log/$pool.access.log
        
        ; The access log format.
        ; The following syntax is allowed
        ;  %%: the '%' character
        ;  %C: %CPU used by the request
        ;      it can accept the following format:
        ;      - %{user}C for user CPU only
        ;      - %{system}C for system CPU only
        ;      - %{total}C  for user + system CPU (default)
        ;  %d: time taken to serve the request
        ;      it can accept the following format:
        ;      - %{seconds}d (default)
        ;      - %{miliseconds}d
        ;      - %{mili}d
        ;      - %{microseconds}d
        ;      - %{micro}d
        ;  %e: an environment variable (same as $_ENV or $_SERVER)
        ;      it must be associated with embraces to specify the name of the env
        ;      variable. Some exemples:
        ;      - server specifics like: %{REQUEST_METHOD}e or %{SERVER_PROTOCOL}e
        ;      - HTTP headers like: %{HTTP_HOST}e or %{HTTP_USER_AGENT}e
        ;  %f: script filename
        ;  %l: content-length of the request (for POST request only)
        ;  %m: request method
        ;  %M: peak of memory allocated by PHP
        ;      it can accept the following format:
        ;      - %{bytes}M (default)
        ;      - %{kilobytes}M
        ;      - %{kilo}M
        ;      - %{megabytes}M
        ;      - %{mega}M
        ;  %n: pool name
        ;  %o: ouput header
        ;      it must be associated with embraces to specify the name of the header:
        ;      - %{Content-Type}o
        ;      - %{X-Powered-By}o
        ;      - %{Transfert-Encoding}o
        ;      - ....
        ;  %p: PID of the child that serviced the request
        ;  %P: PID of the parent of the child that serviced the request
        ;  %q: the query string
        ;  %Q: the '?' character if query string exists
        ;  %r: the request URI (without the query string, see %q and %Q)
        ;  %R: remote IP address
        ;  %s: status (response code)
        ;  %t: server time the request was received
        ;      it can accept a strftime(3) format:
        ;      %d/%b/%Y:%H:%M:%S %z (default)
        ;  %T: time the log has been written (the request has finished)
        ;      it can accept a strftime(3) format:
        ;      %d/%b/%Y:%H:%M:%S %z (default)
        ;  %u: remote user
        ;
        ; Default: "%R - %u %t \"%m %r\" %s"
        ;access.format = %R - %u %t "%m %r%Q%q" %s %f %{mili}d %{kilo}M %C%%
        
        ; The log file for slow requests
        ; Default Value: not set
        ; Note: slowlog is mandatory if request_slowlog_timeout is set
        ;slowlog = log/$pool.log.slow
        
        ; The timeout for serving a single request after which a PHP backtrace will be
        ; dumped to the 'slowlog' file. A value of '0s' means 'off'.
        ; Available units: s(econds)(default), m(inutes), h(ours), or d(ays)
        ; Default Value: 0
        ;request_slowlog_timeout = 0
        
        ; The timeout for serving a single request after which the worker process will
        ; be killed. This option should be used when the 'max_execution_time' ini option
        ; does not stop script execution for some reason. A value of '0' means 'off'.
        ; Available units: s(econds)(default), m(inutes), h(ours), or d(ays)
        ; Default Value: 0
        ;request_terminate_timeout = 0
        
        ; Set open file descriptor rlimit.
        ; Default Value: system defined value
        ;rlimit_files = 1024
        
        ; Set max core size rlimit.
        ; Possible Values: 'unlimited' or an integer greater or equal to 0
        ; Default Value: system defined value
        ;rlimit_core = 0
        
        ; Chroot to this directory at the start. This value must be defined as an
        ; absolute path. When this value is not set, chroot is not used.
        ; Note: you can prefix with '$prefix' to chroot to the pool prefix or one
        ; of its subdirectories. If the pool prefix is not set, the global prefix
        ; will be used instead.
        ; Note: chrooting is a great security feature and should be used whenever
        ;       possible. However, all PHP paths will be relative to the chroot
        ;       (error_log, sessions.save_path, ...).
        ; Default Value: not set
        ;chroot =
        
        ; Chdir to this directory at the start.
        ; Note: relative path can be used.
        ; Default Value: current directory or / when chroot
        chdir = /
        
        ; Redirect worker stdout and stderr into main error log. If not set, stdout and
        ; stderr will be redirected to /dev/null according to FastCGI specs.
        ; Note: on highloaded environement, this can cause some delay in the page
        ; process time (several ms).
        ; Default Value: no
        catch_workers_output = yes
        
        ; Limits the extensions of the main script FPM will allow to parse. This can
        ; prevent configuration mistakes on the web server side. You should only limit
        ; FPM to .php extensions to prevent malicious users to use other extensions to
        ; exectute php code.
        ; Note: set an empty value to allow all extensions.
        ; Default Value: .php
        ;security.limit_extensions = .php .php3 .php4 .php5 .php7
        
        ; Pass environment variables like LD_LIBRARY_PATH. All $VARIABLEs are taken from
        ; the current environment.
        ; Default Value: clean env
        ;env[HOSTNAME] = $HOSTNAME
        env[PATH] = /srv/www/phpcs/scripts/:/usr/local/bin:/usr/bin:/bin
        ;env[TMP] = /tmp
        ;env[TMPDIR] = /tmp
        ;env[TEMP] = /tmp
        
        ; Additional php.ini defines, specific to this pool of workers. These settings
        ; overwrite the values previously defined in the php.ini. The directives are the
        ; same as the PHP SAPI:
        ;   php_value/php_flag             - you can set classic ini defines which can
        ;                                    be overwritten from PHP call 'ini_set'.
        ;   php_admin_value/php_admin_flag - these directives won't be overwritten by
        ;                                     PHP call 'ini_set'
        ; For php_*flag, valid values are on, off, 1, 0, true, false, yes or no.
        
        ; Defining 'extension' will load the corresponding shared extension from
        ; extension_dir. Defining 'disable_functions' or 'disable_classes' will not
        ; overwrite previously defined php.ini values, but will append the new value
        ; instead.
        
        ; Note: path INI options can be relative and will be expanded with the prefix
        ; (pool, global or /usr)
        
        ; Default Value: nothing is defined by default except the values in php.ini and
        ;                specified at startup with the -d argument
        ;php_admin_value[sendmail_path] = /usr/sbin/sendmail -t -i -f www@my.domain.com
        ;php_flag[display_errors] = off
        ;php_admin_value[error_log] = /var/log/fpm-php.www.log
        ;php_admin_flag[log_errors] = on
        ;php_admin_value[memory_limit] = 32M
        

## Buat 2 folder di dalam folder PHP

### tasks/main.yml

        
        ---
        - name: delete apt chache
          become: yes
          become_user: root
          become_method: su
          command: rm -vf /var/lib/apt/lists/*
        
        - name: install php
          become: yes
          become_user: root
          become_method: su
          apt: name={{ item }} state=latest update_cache=true
          with_items:
            - gtkhash
            - crack-md5
            - git
            - curl
            - nginx
            - nginx-extras
            - php7.4
            - php7.4-fpm
            - php7.4-curl
            - php7.4-xml
            - php7.4-gd
            - php7.4-opcache
            - php7.4-mbstring
            - php7.4-zip
            - php7.4-json
            - php7.4-cli
        
        - name: enable module php mbstring
          command: phpenmod mbstring
          notify:
            - restart php
        

### handlers/main.yml

        
        ---
        - name: restart php
          become: yes
          become_user: root
          become_method: su
          action: service name=php7.4-fpm state=restarted
        
        - name: restart nginx
          become: yes
          become_user: root
          become_method: su
          action: service name=nginx state=restarted
          
 ### hasil laravel 
 ![laravel](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/laravel.jpeg)


# Penginstalan YII ``kelompok15.local/product``

## file penginstalan 'nano yii.yml' 
  ---
    - hosts: lxc_php7_1Y
      vars:
        username: 'admin'
        password: 'admin'
        domain: 'lxc_php7_1Y.dev'
      roles:
        - yii
    
    - hosts: lxc_php7_2Y
      vars:
        username: 'admin'
        password: 'admin'
        domain: 'lxc_php7_2Y.dev'
      roles:
        - yii
    
    - hosts: lxc_php7_4Y
      vars:
        username: 'admin'
        password: 'admin'
        domain: 'lxc_php7_4Y.dev'
      roles:
        - yii
    
    - hosts: lxc_php7_5Y
      vars:
        username: 'admin'
        password: 'admin'
        domain: 'lxc_php7_5Y.dev'
      roles:
        - yii
    
    - hosts: lxc_php7_6Y
      vars:
        username: 'admin'
        password: 'admin'
        domain: 'lxc_php7_6Y.dev'
      roles:
        - yii
    ```
    
## folder yii   
    ```
      sudo mkdir -p yii /tasks
      sudo mkdir -p yii /handlers
      sudo mkdir -p yii /templates
    ```
### tasks/main.yml
    ```
          ---
    - name: delete apt cache
      become: yes
      become_user: root
      become_method: su
      command: rm -vf /var/lib/apt/lists/*
    
    - name: Download and install Composer
      shell: curl -sS https://getcomposer.org/installer | php
      args:
        chdir: /usr/src/
        creates: /usr/local/bin/composer
      become: yes
      register: composer_install_result
      changed_when: composer_install_result.rc != 0
    
    - name: Add Composer to global path if installed
      copy:
        dest: /usr/local/bin/composer
        group: root
        mode: '0755'
        owner: root
        src: /usr/src/composer.phar
        remote_src: yes
      become: yes
      when: composer_install_result.changed
    
    - name: Ensure /var/www/html/basic directory is absent
      file:
        path: /var/www/html/basic
        state: absent
      become: yes
      ignore_errors: yes
    
    - name: Create directory /var/www/html/basic
      file:
        path: /var/www/html/basic
        state: directory
        owner: root
        mode: '0755'
      become: yes
    
    - name: Composer create-project Yii2 basic app
      shell: >
        COMPOSER_ALLOW_SUPERUSER=1 /usr/local/bin/composer create-project yiisoft/yii2-app-basic /var/www/html/basic --prefer-dist --no-interaction
      become: yes
      retries: 3
      delay: 10
    
    - name: Set permissions for Composer
      become: yes
      become_user: root
      become_method: su
      command: chmod +x /usr/local/bin/composer
    
    - name: Install Composer dependencies
      shell: >
        cd /var/www/html/basic && COMPOSER_ALLOW_SUPERUSER=1 /usr/local/bin/composer install --no-interaction
      become: yes
    
    - name: Copy yii.conf.j2
      template:
        src: templates/yii.conf.j2
        dest: /etc/nginx/sites-available/{{ domain }}
      vars:
        servername: '{{ domain }}'
    
    - name: Install required packages
      apt:
        name:
            - nginx-extras
            - php7.4
            - php7.4-fpm
            - php7.4-mbstring
            - php7.4-xml
            - php7.4-mysql
            - php7.4-curl
            - curl
            - zip
            - unzip
            - git
        state: present
    
    - name: Symlink yii.conf
      command: ln -sfn /etc/nginx/sites-available/{{ domain }} /etc/nginx/sites-enabled/{{ domain }}
      notify:
        - restart nginx
    
    - name: Write {{ domain }} to /etc/hosts
      lineinfile:
        dest: /etc/hosts
        regexp: '.*{{ domain }}$'
        line: "127.0.0.1 {{ domain }}"
        state: present
    ```

      

## handler/main.yml

    ```
      ---
      - name: restart php
        become: yes
        become_user: root
        become_method: su
        action: service name=php7.4-fpm state=restarted
      
      - name: restart nginx
        become: yes
        become_user: root
        become_method: su
        action: service name=nginx state=restarted
     ```

## templates/yii.conf.j2

      
        server {
            set $host_path "/var/www/html/basic";

            server_name  {{ domain }};
            root   $host_path/web;
            set $yii_bootstrap "index.php";

            # Access log configuration
            #access_log /var/log/nginx/{{ domain }}_access.log main;


            charset utf-8;

            location / {
                index  index.html $yii_bootstrap;
                try_files $uri $uri/ /$yii_bootstrap?$args;
            }

            location ~ ^/(protected|framework|themes/\w+/views) {
                deny  all;
            }

            #avoid processing of calls to unexisting static files by yii
            location ~ \.(js|css|png|jpg|gif|swf|ico|pdf|mov|fla|zip|rar)$ {
                try_files $uri =404;
            }

            # pass the PHP scripts to FastCGI server listening on UNIX socket
            location ~ \.php {
                fastcgi_split_path_info  ^(.+\.php)(.*)$;

                #let yii catch the calls to unexising PHP files
                set $fsn /$yii_bootstrap;
                if (-f $document_root$fastcgi_script_name){
                    set $fsn $fastcgi_script_name;
                }
            fastcgi_pass   unix:/run/php/php7.4-fpm.sock;
                include fastcgi_params;
                fastcgi_param  SCRIPT_FILENAME  $document_root$fsn;

            #PATH_INFO and PATH_TRANSLATED can be omitted, but RFC 3875 specifies them for CGI
                fastcgi_param  PATH_INFO        $fastcgi_path_info;
                fastcgi_param  PATH_TRANSLATED  $document_root$fsn;
            }

            # prevent nginx from serving dotfiles (.htaccess, .svn, .git, etc.)
            location ~ /\. {
                deny all;
                access_log off;
                log_not_found off;
            }
        }
      
  ### Hasil dari YII
  ![yii](https://github.com/azkalazkyaa/UAS-SISTER/blob/main/ASSETS/yiii.jpeg)


  # Host utama setting nginx cd /etc/nginx/sites-available dan file nama sudo nano kelompok12.local
```
  upstream ci {
    server 10.0.3.144;
      server 10.0.3.41;
  }

  upstream laravel {
      least_conn;
      server 10.0.3.137;
      server 10.0.3.200;
      server 10.0.3.104;
      server 10.0.3.176;
  }

  upstream mariadb {
      server 10.0.3.46;

  }

  upstream yii {
      server 10.0.3.251 weight=3;
      server 10.0.3.137 weight=2;
      server 10.0.3.104 weight=4;
      server 10.0.3.176 weight=1;
  }

  upstream wp{
      ip_hash;
      server 10.0.3.251;
      server 10.0.3.137;
      server 10.0.3.104;
      server 10.0.3.202;
  }

  
  server {
    listen 80;
    listen [::]:80;

    server_name kelompok15.local;

    root /var/www/html;
    index index.html;

    location /product {
        # Jika ada aplikasi web di balik proxy_pass
        rewrite /product/?(.*)$ /$1 break;
        proxy_pass http://yii;
    }

    location /app {
        rewrite /app/?(.*)$ /$1 break;
        proxy_pass http://ci;
    }

    location /phpmyadmin {
        rewrite /phpmyadmin/?(.*)$ /$1 break;
        proxy_pass http://mariadb;
    }

    location / {
        rewrite /?(.*)$ /$1 break;
        proxy_pass http://laravel;
    }
  }
  server {
          listen 80;
          listen [::]:80;
  
          server_name news.kelompok15.local;
  
          root /var/www/html;
          index index.html;
  
          location / {
                  rewrite /?(.*)$ /$1 break;
                  proxy_pass http://wp;
          }
  }
  ```
  
# Jmeter

otw
 
