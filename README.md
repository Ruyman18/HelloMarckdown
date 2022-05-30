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
