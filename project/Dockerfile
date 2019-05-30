FROM amazonlinux:1
MAINTAINER Thoz <huynhductho96@gmail.com>

RUN yum clean all
RUN yum update -y
RUN yum install -y nano
RUN yum install -y vim

#install php
RUN yum install -y php72 php72-cli php72-common php72-json php72-mbstring php72-mysqlnd php72-pdo php72-process php72-xml openssl zip unzip php72-zip git php72-gmp php72-gd

#install httpd
RUN yum install httpd24 httpd24-tools -y

# Install Composer
RUN  curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

# Install nodejs
RUN yum -y update
RUN yum install -y gcc gcc-c++ make openssl-devel
RUN curl --silent --location https://rpm.nodesource.com/setup_8.x | bash -
RUN yum -y install nodejs

# Install yarn
RUN curl -sL https://dl.yarnpkg.com/rpm/yarn.repo | tee /etc/yum.repos.d/yarn.repo
RUN yum -y install yarn
RUN yum install -y ghc-glib-devel ghc-glib autoconf autogen intltool libtool libpng-devel

# Clear yum cache
RUN yum clean all

RUN mkdir -p /var/www/html/project_laravel
RUN chmod -R 755 /var/www/html/project_laravel

# config virtual host
ADD project.conf /etc/httpd/conf.d

RUN echo -e "127.0.0.1 localhost" | tee -a /etc/hosts
RUN echo -e "127.0.0.1 project.test" | tee -a /etc/hosts

# workspace
WORKDIR /var/www/html/project_laravel/
# for web
EXPOSE 80
EXPOSE 443

CMD /usr/sbin/httpd -DFOREGROUND