

# If Using systemd init Linux system
## Ensure MariaDB Server is Running Using Systemctl:
~~~console
sudo systemctl start mariadb.service
~~~

## Check if MariaDB Service Is Running
~~~console
systemctl | grep "maria"
~~~

## Check The Status Of The MariaDB Service
~~~console
systemctl status mariadb.service
~~~
