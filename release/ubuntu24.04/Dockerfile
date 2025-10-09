FROM ubuntu:24.04
#MAINTAINER Greg Cockburn

# Update base packages
RUN apt update \
    && apt upgrade --assume-yes

# Install pre-reqs
RUN DEBIAN_FRONTEND=noninteractive apt install --assume-yes software-properties-common file

# Configure Zoneminder PPA
RUN add-apt-repository -y ppa:iconnor/zoneminder-1.36

# Install MariaDB
RUN DEBIAN_FRONTEND=noninteractive apt install --assume-yes mariadb-server
# Install zoneminder
RUN DEBIAN_FRONTEND=noninteractive apt install --assume-yes zoneminder \
    && a2enconf zoneminder \
    && a2enmod rewrite headers cgi

# Setup Volumes
VOLUME /var/cache/zoneminder/events /var/cache/zoneminder/images /var/lib/mysql /var/log/zm

# Expose http port
EXPOSE 80

# Configure entrypoint
COPY utils/entrypoint.sh /usr/local/bin/
RUN chmod 755 /usr/local/bin/entrypoint.sh
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
