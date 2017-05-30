# EClass
#preparacion del entorno

*una ves instaldo el sistema operativo (ubuntu-16.04.2-server-amd64.iso) instalar openssh-server para realizar todas la interacciones con el servidor mediante ssh

sudo apt-get -y openssh-server
sudo apt-get update && sudo apt-get -y upgrade 

*Instalar apache y php junto al modulo para apache y activar el modulo de escritura ultimo en modo escritura

sudo apt-get -y install apache2 php libapache2-mod-php7.0
sudo a2enmod rewrite

*instalar y configurar mysql

sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password eclass' && sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password eclass' && sudo apt-get -y install mysql-server

*instalar phalcon php

curl -s "https://packagecloud.io/install/repositories/phalcon/stable/script.deb.sh" | sudo bash && sudo apt-get -y install php7.0-phalcon && sudo service apache2 restart

*crear la base de dartos que contencdra la informacion 

mysql -u root --password=eclass -e "SET SQL_MODE = 'NO_AUTO_VALUE_ON_ZERO';SET time_zone = '+00:00';CREATE DATABASE IF NOT EXISTS eclass DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;USE eclass;CREATE TABLE atenciones ( id int(16) NOT NULL,fecha date NOT NULL,id_forma_ingreso int(16) NOT NULL,id_contacto_crm int(16) NOT NULL,id_coordinadora_crm int(16) NOT NULL,id_producto_agrupador int(16) NOT NULL,id_oficina_comercial_crm int(16) NOT NULL,deleted tinyint(1) NOT NULL) ENGINE=InnoDB DEFAULT CHARSET=utf8;ALTER TABLE atenciones ADD PRIMARY KEY (id);ALTER TABLE atenciones MODIFY id int(16) NOT NULL AUTO_INCREMENT;"

sudo apt-get update && sudo apt-get -y upgrade

todas las contraseñas son eclass y el usuario es eclass eceptuando el usuario de mysql que es root

cambiar los archivos de configuraicon de :

/etc/apache2/sites-enabled/000-default.conf 

<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html
        <Directory "/var/www/">
                  AllowOverride All
        </Directory>

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
</VirtualHost>

cambiar los siguientes elemtos /etc/php5/apache2/php.ini

file_uploads 		    = On
upload_max_filesize = 20M
post_max_size		    = 20M
max_file_uploads	  = 1

# supuestos 
los datos se encuentran almacenados en una base de datos 
