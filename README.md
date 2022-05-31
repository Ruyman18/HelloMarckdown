# ICINGA
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
icinga2 feature list

Disabled features: api command compatlog debuglog elasticsearch gelf graphite influxdb livestatus opentsdb perfdata statusdata syslog
Enabled features: checker mainlog notification
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
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'onmulalumno123?`#';
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
updatedb
locate php.ini
vi /etc/php/7.2/apache2/php.ini
```
Reinicie el servicio Apache
```bash
service apache2 restart
```
Acceda al servidor de bases de datos MySQL
```bash
mysql -u root -p
```
Cree una base de datos denominada icingaweb_db
```bash
CREATE DATABASE icingaweb_db CHARACTER SET UTF8 COLLATE UTF8_BIN;
```
Cree un usuario mysql denominado icingaweb_db
```bash
CREATE USER 'icingaweb_db'@'%' IDENTIFIED BY 'onmulalumno123?`#';
```
Conceda al usuario MySQL el nombre icingaweb_db permiso sobre la base de datos denominada icingaweb_db
```bash
GRANT ALL PRIVILEGES ON icingaweb_db.* TO 'icingaweb_db'@'%';
quit;
```
Instale el paquete de interfaz web de Icinga denominado icingaweb2
```bash
apt-get install icingaweb2
```
Reinicie el servicio Apache
```bash
service apache2 restart
```
Genere el token de instalación de Icinga
```bash
icingacli setup token create
The newly generated setup token is: 0637e471ff1a6cf9ef2
```
Abra su navegador e introduzca la dirección IP de su servidor web más /icingaweb2
En nuestro ejemplo, se introdujo la siguiente URL en el navegador:
• http://10.0.2.15/icingaweb2
Se debe presentar la interfaz de instalación web de Icinga2
Ingrese el token de configuración de Icinga web2

![SQL](https://github.com/Ruyman18/HelloMarckdown/blob/main/1.PNG?raw=true)

En la pantalla Módulos web de Icinga, haga clic en el botón Siguiente

![SQL](https://github.com/Ruyman18/HelloMarckdown/blob/main/2.PNG?raw=true)

En la pantalla Requisitos web de Icinga, haga clic en el botón Siguiente

![SQL](https://github.com/Ruyman18/HelloMarckdown/blob/main/3.PNG?raw=true)

En la pantalla Recurso de base de datos de Icinga, realice la siguiente configuración:

• Nombre del recurso - icingaweb_db
• Tipo de base de datos - MYSQL
• Anfitrión - localhost
• Puerto - 3306
• Nombre de la base de datos - icingaweb_db
• Nombre de usuario - icingaweb_db
• Contraseña - onmulalumno123?`#

Haga clic en el botón Siguiente

![SQL](https://github.com/Ruyman18/HelloMarckdown/blob/main/5.PNG?raw=true)

En esta pantalla, ingrese el inicio de sesión raíz de MySQL para importar la plantilla de base de datos Icingaweb2

![SQL](https://github.com/Ruyman18/HelloMarckdown/blob/main/6.PNG?raw=true)

Establezca el nombre de back-end icingaweb2 y haga clic en el botón Siguiente

![SQL](https://github.com/Ruyman18/HelloMarckdown/blob/main/7.PNG?raw=true)

Establezca una cuenta administrativa para acceder a la interfaz web de Icinga

![SQL](https://github.com/Ruyman18/HelloMarckdown/blob/main/8.PNG?raw=true)

Pantalla de configuración de la aplicación, realice la configuración de seguimiento:

• Mostrar Stacktraces - Habilitado
• Mostrar mensajes de estado de la aplicación - Habilitado
• Tipo de almacenamiento de preferencias de usuario - Base de datos
• Tipo de registro - Syslog
• Nivel de registro - Error
• Prefijo de aplicación - icingaweb2
• Facilidad - Usuario

Haga clic en el botón Siguiente

![SQL](https://github.com/Ruyman18/HelloMarckdown/blob/main/9.PNG?raw=true)

En la pantalla de resumen de instalación de Icinga, haga clic en el botón Siguiente
En la pantalla de bienvenida, haga clic en el botón Siguiente

![SQL](https://github.com/Ruyman18/HelloMarckdown/blob/main/11.PNG?raw=true)

En la pantalla Monitoring IDO Resource (Supervisión de recursos de IDO), realice la siguiente configuración:
• Nombre del recurso - icinga_ido
• Tipo de base de datos - MYSQL
• Anfitrión - localhost
• Puerto - 3306
• Nombre de la base de datos - icinga2
• Nombre de usuario - icinga2
• Contraseña - onmulalumno123?`#

Haga clic en el botón Siguiente

![SQL](https://github.com/Ruyman18/HelloMarckdown/blob/main/12.PNG?raw=true)

En la pantalla Transporte de comandos, realice la siguiente configuración:

• Nombre del transporte - icinga2
• Tipo de transporte - Archivo de comandación local
• Archivo De comunicación - /var/run/icinga2/cmd/icinga2.cmd

Haga clic en el botón Siguiente

![SQL](https://github.com/Ruyman18/HelloMarckdown/blob/main/13.PNG?raw=true)

En la pantalla Seguridad de supervisión, realice la siguiente configuración:

• Variables personalizadas protegidas - *pw*,*pass*,community

Haga clic en el botón Siguiente

![SQL](https://github.com/Ruyman18/HelloMarckdown/blob/main/14.PNG?raw=true)

En la última pantalla, haga clic en el botón Finalizar y espere a que finalice la instalación de Icinga2

![SQL](https://github.com/Ruyman18/HelloMarckdown/blob/main/16.PNG?raw=true)

Por último se debe mostrar la interfaz de inicio de sesión de Icinga2
Después de un inicio de sesión correcto, se le enviará al panel de Icinga2

![SQL](https://github.com/Ruyman18/HelloMarckdown/blob/main/17..png?raw=true)

Y ya estaría instalado la interfaz web Icinga2 en Ubuntu Linux
