#Manejo de sistema operativo Linux

*Este curso en el Técnico en informática de INFOTEP - Noviembre 2021*

  

##### Módulos (... de GNU/Linux)

1. Instalación...

2. Configuración...

3. Manejo...

4. Instalación de servicios de Red...

5. Administración de Servicios de Red...

  

```html

<h1>Hola</h1>

```

  

![Logo de SAMBA](https://www.muylinux.com/wp-content/uploads/2014/04/samba.jpg)

  

# Manual de Instalación y Configuración de SAMBA

  

### THE ULTIMATE GUIDE

  

> Este manual esta dirigido a los vagos

  

***Creditos:***

  

A mi esfuerzo exhaustivo de búsqueda de Internet hehe.

  

*Este manual es incomparable y esto es un perro 🐕*

  

```bash

$ sudo xd

```

  

## Introduccion

### ¿Que es SAMBA?

Es un conjunto de aplicaciones Linux, basada en el protocolo SMB[^1], que permite compartir archivos en red.

  

### Orígenes

Fue creado por [Andrew Tridgell](https://es.wikipedia.org/wiki/Andrew_Tridgell  "https://es.wikipedia.org/wiki/Andrew_Tridgell").

El necesitaba montar un espacio en disco en su computadora para un servidor Unix.

Esa computadora utilizaba el sistema de archivos **NFS** (*Network File System*). Sin embargo, una aplicación necesitaba soporte para el protocolo **NetBIOS[^2]** (no soportado por el NFS).

Tridgell lo solucionó escribiendo un sniffer[^3] que permitía analizar el tráfico de datos generado por el protocolo NetBIOS. Hizo [ingeniería inversa](https://es.wikipedia.org/wiki/Ingenier%C3%ADa_inversa  "https://es.wikipedia.org/wiki/Ingeniería_inversa") en el protocolo SMB y lo implementó en el Unix.

  

Eso hizo que el servidor Unix apareciera como un servidor de archivos Windows en su PC con DOS

  

## Instalacion

 Antes instalar SAMBA usamos el siguiente comando para actualizar los paquetes que tenemos instalados:
```bash
sudo apt update
```
Ahora usamos el siguiente comando para instalar SAMBA en nuestro equipo:

```bash
sudo apt install samba
```
Por ultimo usamos el siguiente comando para verificar el status de SAMBA: 

```bash
sudo systemctl status nmbd
```
## Configuracion

Para iniciar la configuración tenemos que crear la carpeta SAMBA en nuestra raiz con el comando: 

```bash
sudo mkdir /samba
```
Ahora vamos a crear una copia de seguridad del archivo de configuracion de SAMBA antes de hacer modificaciones

```bash
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.original
```

Ahora vamos a modificar el archivo de configuracion de SAMBA original con el comando: 

```bash
sudo nano /etc/samba/smb.conf
```
y al final del archivo agregamos:

```bash
[samba-nuestro-nombre]
comment = Samba on Ubuntu
path = /samba
read only = no
browsable = yes
```
Ahora agregamos un usuario con el comando:

```bash
sudo useradd nombre
```
Y lo agregamos a SAMBA con el comando:

```bash
sudo smbpasswd -a nombre-usuario
```
Ahora vamos a crear una carpeta publica con el comando:

```bash
sudo mkdir /samba/nombre-de-carpeta
```

Ahora vamos a modificar los usuarios y permisos de la carpeta para que otros puedan conectarse con los siguientes tres comandos:

```bash
sudo chown -R nobody:nogroup /samba/nombre-de-carpeta
sudo chmod -R 0777 /samba/nombre-de-carpeta
sudo chgrp sambashare /samba/nombre-de-carpeta
```
Y reiniciamos el servicio con:

```bash
sudo systemctl restart smbd.service
```
*Tenemos que habilitar el firewall*
```bash
sudo ufw allow samba
```
Para conectarnos a la carpeta desde linux, abrimos un explorador de archivos y al final de la izquierda saldrá red, entramos y ya estaremos en la carpeta

Para entrar desde windows tendremos que presionar windows + r y poner: \\ip-servidor\nombre-de-usuario

Y para conectarnos desde MacOS damos click derecho a finder damos a conectar conectarse al servidor e introducimos: smb://ip-servidor

## Desinstalacion

  

[^1]: Server Message Block

[^2]: Network Basic Input/Output System

[^3]: Pequeño programa para captura de tráfico de datos en red




