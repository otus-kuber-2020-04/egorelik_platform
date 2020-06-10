# Pull base image.
FROM library/ubuntu

# Install Nginx.
RUN \
  apt-get -y update && \
  apt-get -y install software-properties-common && \ 
  #add-apt-repository -y ppa:nginx/stable && \
  #apt-get update && \
  apt-get install -y nginx && \
  rm -rf /var/lib/apt/lists/* && \
  useradd -u 1001 nginx-user && \
  sed -i -e 's/80 default_server/8000 default_server/g' /etc/nginx/sites-enabled/default && \
  sed -i -e 's/user www-data/user nginx-user/g' /etc/nginx/nginx.conf && \
  echo "\ndaemon off;" >> /etc/nginx/nginx.conf && \
  chown -R nginx-user:nginx-user /var/lib/nginx

# Define mountable directories.
VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www/html"]

# Define working directory.
WORKDIR /etc/nginx

# Define default command.
CMD ["nginx"]

# Expose ports.
EXPOSE 8000
EXPOSE 443