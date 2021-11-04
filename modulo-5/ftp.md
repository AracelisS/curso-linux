# Instalación de  FTP
![LOGO FTP](https://global-uploads.webflow.com/5f3ab2f9e5c5f12c86880cf1/60e308e8a48029768bf8a9a1_07f7327b_e49f-4c05-ab0a-fcd3d2414474.png)
 1. Desde nuestra terminal primero comprobamos si hay actualizaciones.
 2. Instalamos **vsftpd**. 
 3. Creamos una copia de seguridad del archivo original.
 4. Le modificamos las opciones que se adapten a nuestro gusto.
 5. Habilitar la directiva.
 6. Reiniciamos **vsftpd**.
 7. comprobamos el *estado* del servidor. 
 8. Habilitamos el **firewall**.


 ```bash
1. sudo apt update
2. sudo apt-get install vsftpd -y
3. sudo cp /etc/vsftpd.conf /etc/vsftpd conf.backup
4. sudo nano /etc/vsftpd.conf
5. write_enoble = yes   Anonymous_enable = yes
6. sudo systemctl restart vsftpd
7. sudo systemctl status vsftpd 
8. sudo ufw allow ftp
9. sudo ufw allow ftp-data
 ```
