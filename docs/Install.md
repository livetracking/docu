# Installation

## Requirements

* [PHP 7](http://php.net/) and [Composer](https://getcomposer.org/)
* [Lighttpd](https://www.lighttpd.net/) or another web server
* [InfluxDB](https://www.influxdata.com/products/influxdb-overview/)
* [SQLite](https://www.sqlite.org/)

For many distributions, there are pre-packaged packages.

### Ubuntu

Install InfluxDB with the following commands:

```
wget https://dl.influxdata.com/influxdb/releases/influxdb_1.7.10_amd64.deb
sudo dpkg -i influxdb_1.7.10_amd64.deb
```

More help: <https://portal.influxdata.com/downloads/>

Install packages:

```
sudo apt update
sudo apt install git curl php-cli php-sqlite3 php-mbstring phpunit sqlite3 zip unzip
```

Install Composer:

```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
sudo php composer-setup.php --install-dir=/usr/bin --filename=composer
php -r "unlink('composer-setup.php');"
```

## Installation

```
# Clone this repository
git clone "https://github.com/livetracking/server.git"
cd server

# Install dependencies
composer install

# Create SQLite database
cat database/users.sql | sqlite3 database/users.sqlite

# Create default users
php database/default_users.php | sqlite3 database/users.sqlite

# Create InfluxDB default users and databases
bash database/influxdb.sh

# Edit setting, set InfluxDB username and password
vi src/settings.php

# Edit InfluxDB configuration
# Enable authentication by setting the 'auth-enabled' option to 'true'
sudo vi /etc/influxdb/influxdb.conf

# Restart InfluxDB
sudo systemctl restart influxdb
```

## Test

### Start the Application

You can then run it with PHP's built-in webserver:

	php -S 127.0.0.1:8080 -t public public/index.php
	# or run
	bash start.sh

Test your setup:

	# Adjust variables
	vi test/test.sh
	# Run
	bash test/test.sh

### Insert some data

Register new user:

	curl "http://127.0.0.1:8080/register" \
	--data "username=my_username" \
	--data "password=my_password"

Write data into InfluxDB:

	curl -u "my_username:my_password" "http://127.0.0.1:8086/write?db=my_username" \
	--data "test value=1"

### Query for the data

Show user:

	curl -u "my_username:my_password" "http://127.0.0.1:8080/user"

Query data from InfluxDB:

	curl -u "public:livetracking" "http://127.0.0.1:8086/query?db=my_username" \
	--data "q=SELECT * FROM test"

## Deploy

If you want to publish your setup on the internet you should use a proper web server.

A Lighttpd configuration (`lighttpd.conf`) can be found in the folder `server`.
Lighttpd is also used as a reverse proxy for InfluxDB.

Run Phing build script:

	vi build.xml
	sudo bash deploy.sh