#Let's receive it from Ubuntu.
FROM ubuntu:20.04

# Update.
RUN apt-get update

# Set argument for Mongodb.
ARG DEBIAN_FRONTEND=noninteractive

# Install necessary utilities.
RUN apt-get install -y net-tools curl git gnupg

# Install MongoDB (V4).
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
RUN echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-4.0.list
RUN apt-get update
RUN apt-get install -y mongodb-org

# Install NodeJS.
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install -y nodejs

# Install Supervisord.
RUN apt-get install -y supervisor

# Create user.
RUN groupadd site && useradd -m -d /var/pg/ -s /bin/bash -g site site

# Grant privileges.
RUN chown -R site:site /var/pg

# Copy over needed files.
COPY files/supervisord.conf /etc/supervisor/supervisord.conf
COPY files/mongodb.conf /etc/mongodb-pg.conf

# Copy startup file.
COPY files/startup.sh /startup.sh

# Expose port for NGINX reverse proxy.
EXPOSE 4568

# Startup script.
CMD ["./startup.sh"]
