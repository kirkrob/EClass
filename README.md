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

# supuestos 
los datos se encuentran almacenados en una base de datos 
