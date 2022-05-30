#ICINGA
## Tutorial - Icinga2 Ubuntu Linux

Para instalar los paquetes necesarios utilice apt-get
```bash
apt-obtener actualización
apt-get install apt-transport-https wget gnupg
```
Después de descargar e instalar la clave del repositorio de Icinga2
```bash
wget -O - https://packages.icinga.com/icinga.key | apt-key agregar -
```
A continuación use el comando que voy a poner ahora para descubrir su nombre de código de Ubuntu Linux
```bash
. /etc/os-release; si [ ! -z ${UBUNTU_CODIGO+x} ]; luego DIST="${UBUNTU_CODENAME}"; else DIST="$(lsb_release -c| awk '{imprimir $2}')"; fi;
conjunto | grep DISTR.
```

Ahora agregue la base de datos APT al repositorio oficial de Icinga2
```bash
echo "deb https://packages.icinga.com/ubuntu icinga-${DIST} principal" > /etc/apt/sources.list.d/${DIST}-icinga.list
echo "deb-src https://packages.icinga.com/ubuntu icinga-${DIST} principal" >> /etc/apt/sources.list.d/${DIST}-icinga.list
```
Actualice la base de datos APT e instale el paquete Icinga2
```bash
apt-obtener actualización
apt-get install icinga2
```
Instale los complementos de monitoreo estándar del Icinga2
```bash
apt-get install monitoreo-complementos
```
Lista Icinga2 características instaladas
```bash
lista de características de icinga2
​
Funciones deshabilitadas: comando api compatlog debuglog elasticsearch gelf graphite influxdb livestatus opentsdb perfdata statusdata syslog
Funciones habilitadas: notificación de registro principal del verificador
```
Habilite el servicio Icinga2 para que se inicie automáticamente durante el tiempo de arranque
```bash
systemctl habilitar icinga2
```
Y ya terminarí la instalación de Icinga2

# Tutorial - Icinga2 MySQL

Instale el paquete icinga2-ido-mysql
Esto permitirá al servidor Icinga2 almacenar la configuración en Mysql
```bash
apt-obtener actualización
apt-get install icinga2-ido-mysql
```
Habilite la función ido-mysql del Icinga 2
![SQL](https://github.com/Ruyman18/HelloMarckdown/blob/main/idp1.PNG?raw=true)
![SQL](https://github.com/Ruyman18/HelloMarckdown/blob/main/idp2.PNG?raw=true)
Habilite la característica ido-mysql
```bash
icinga2 feature enable command  ido-mysql
```
Reiniciar Icinga2
```bash
service icinga2 restart
```
Instale el servicio de base de datos MySQL
```bash
apt-get install mysql-server mysql-client
```
Acceda al servidor de bases de datos MySQL
```bash
mysql -u root -p
```
Establezca una contraseña para el usuario raíz de MySQL
```bash
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'kamisama123';
```
Cree una base de datos denominada icinga2
```bash
CREATE DATABASE icinga2 CHARACTER SET UTF8 COLLATE UTF8_BIN;
```
Cree un usuario mysql denominado icinga2
```bash
CREATE USER 'icinga2'@'%' IDENTIFIED BY 'onmulalumno123?`#';
```
Conceda al usuario de MySQL permiso denominado icinga2 sobre la base de datos denominada icinga2
```bash
GRANT ALL PRIVILEGES ON icinga2.* TO 'icinga2'@'%';
quit;
```
Ahora importe la plantilla de base de datos Icinga2 dentro del MySQL
El sistema solicitará la contraseña del usuario de icinga2 MysQL para poder importar la plantilla
```bash
mysql -u icinga2 -p icinga2 < /usr/share/icinga2-ido-mysql/schema/mysql.sql
```
Edite el archivo de configuración ido-mysql.conf para habilitar la comunicación con el servicio MySQL
```bash
vi /etc/icinga2/features-enabled/ido-mysql.conf
```
Aquí está nuestra configuración
```bash
/**
 * The db_ido_mysql library implements IDO functionality
 * for MySQL.
 */

library "db_ido_mysql"

object IdoMysqlConnection "ido-mysql" {
  user = "icinga2",
  password = "kamisama123",
  host = "localhost",
  database = "icinga2"
}
```
A continuacion hay reiniciar el Icinga2
```bash
service icinga2 restart
```
Y ya habría terminado la instalación de la base de datos
Y también habría importado la plantilla de la base de datos del MySQL Server

## Tutorial - Icinga2 instalacion interaz web

A continuación, necesitamos instalar el servidor web Apache y todo el software necesario
En la consola Linux, utilice los siguientes comandos para instalar los paquetes necesarios
```bash
apt-get -y install apache2 php libapache2-mod-php php-cli php-opcache php-gd
apt-get -y install php-mysql php-mbstring php-xml php-gd php-json php-curl
apt-get -y install php-bcmath php-ldap php-intl php-readline 
```
Edite el archivo de configuración PHP y establezca la zona horaria correcta
```bash

```

```bash

```
