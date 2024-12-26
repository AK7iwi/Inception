FROM	debian:bullseye

# Update and install necessary packages
RUN	apt-get update -y && apt-get upgrade -y
RUN	apt-get install -y wget \
	php7.4 php-fpm php-mysql php-common php-cgi php-cli mariadb-client

# Create /run/php directory to fix the PID file issue
RUN mkdir -p /run/php && chown -R www-data:www-data /run/php

# Download and extract WordPress
RUN	wget https://fr.wordpress.org/wordpress-6.2.2-fr_FR.tar.gz -P /var/www
RUN	tar -xzf /var/www/wordpress-6.2.2-fr_FR.tar.gz -C /var/www/.
RUN	cp -r /var/www/wordpress/. /var/www/html
RUN	rm /var/www/wordpress-6.2.2-fr_FR.tar.gz

# Install WP-CLI
RUN	wget https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN 	chmod +x wp-cli.phar

# Expose PHP-FPM port
EXPOSE	9000

# Copy configuration files and tools
COPY	conf/www.conf /etc/php/7.4/fpm/pool.d/www.conf
COPY 	tools/config_wp.sh config_wp.sh

# Ensure the script is executable
RUN	chmod +x config_wp.sh

# Run the configuration script
CMD ["./config_wp.sh"]

