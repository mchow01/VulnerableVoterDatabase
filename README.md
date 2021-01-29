# Overview
The purpose of this system is to demonstrate what happens when a voter database, including web forms, are not developed well and have vulnerabilities.

# Audience
1. Govies, lawmakers, politicians
2. Developers

# DISCLAIMER
* Because this is a deliberately vulnerable system, DO NOT launch this on the real Internet!
* Please DO NOT attack your state's actual "Find my voter registration status" page.

# Installation and Running

### Docker

Using [Docker and `docker-compose`](https://github.com/docker/compose):

```console
cd docker
docker-compose build
docker-compose up
```

The Vulnerable Voter Database should now be running at http://localhost/.

When you are finished, be sure to run `docker-compose down` to top and remove containers, networks, images, and volumes.

### Manual

1. Install a web server (e.g., `nginx`), MySQL / MariaDB server, PHP, `php-mysql` extension, and Git.  On Debian:
```console
sudo apt install nginx php-fpm mariadb-server git php-mysql php-gd
```

2. Enable PHP on your web server.  See https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-20-04 how-to.

3. Set up database in `mysql`:
- Create database in MySQL: `CREATE DATABASE voterdb;`
- Create user for database in MySQL: `CREATE USER 'hacked'@localhost IDENTIFIED BY 'epicfail';`
- Grant database privileges to user in MySQL: `GRANT ALL ON voterdb.* TO 'hacked'@localhost;`

4. Import database and data: `mysql -u hacked -p voterdb < docker/database/data.sql;`

5. Copy files in `src` to web root (e.g., to `/var/www/html`)

# References
1. https://us-cert.cisa.gov/ncas/tips/ST16-001
2. "SQL Injection Attack is Tied to Election Commission Breach" https://threatpost.com/sql-injection-attack-is-tied-to-election-commission-breach/122571/
3. "How the Russians penetrated Illinois election computers" https://abc7chicago.com/politics/how-the-russians-penetrated-illinois-election-computers/3778816/
4. "US Alleges Iran Sent Threatening Emails to Democrats" https://www.bankinfosecurity.com/us-alleges-iran-sent-threatening-emails-to-democrats-a-15221
5. "Free tech tools for election officials" https://gcn.com/articles/2020/10/08/election-security-tools.aspx
6. "U.S. Voter Databases Offered for Free on Dark Web, Report" https://threatpost.com/u-s-voter-databases-offered-free-dark-web/158840/

# Acknowledgement
Many thanks to "A Docker-Compose PHP Environment From Scratch" https://x-team.com/blog/docker-compose-php-environment-from-scratch/ as it served as the guide to create this system via containers.