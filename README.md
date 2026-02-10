<p align="center">
  <img src="https://github.com/user-attachments/assets/8d94fa85-31f0-4fe0-90d4-9afad8a5b7ca" width="20%" style="margin-right: 10px;" />
  <img src="https://github.com/user-attachments/assets/7f068076-91e3-4775-aa04-8256db3fa184" width="20%" />
</p>

<h1 align="center">Documentación de Servidores</h1>

> 🌟 *Integrantes:*  
> * Steven Matute  
> steven.matute@ucuenca.edu.ec    
> * Genaro Quezada  
> genaro.quezada@ucuenca.edu.ec  



INTRODUCCIÓN


### LEVANTAMIENTO DE SERVIDORES BÀSICOS
En este github presentaremos nuestros servicios, **Correo, servidores web, multimedia, voz, dominio, conexion remota** A continuacion se mostrarà todos los servidores funcionando


### SERVIDOR - WORDPRESS
1. Para que pueda empezar con la instalacion de apache hay que hacer un update.

   `sudo dnf update`

2. Utilice el siguiente comando para instalar apache

   "sudo dnf install httpd -y"
3. Creamos un Virtualhost

4. Creamos un sitio web
   "sudo mkdir /var/www/matute
5. Le damos permisos y arranque**
   "sudo chown -R apache:apache /var/www/matute"
   "sudo systemctl enable httpd"
6. Abrimos puerto web**
   "sudo firewall-cmd --add-service=http --permanent
7. Prueba en la web**

8. Cree un directorio usando el siguiente comando

   `mkdr ~/CARPETA`
   
9. Abra el archivo nano de samba y agregamos lo siguiente al final del archivo
   
`sudo nano /etc/samba/smb.conf`

10. Configure los permisos de firewall para que no haya errores al abrir

   `sudo systemctl stop firewalld`
`sestatus`



`sudo restorecon -Rv “/home/usuario/DIRECTORIO"`

`sudo systemctl restart smb`

11. Asigne contraseña al usuario de samba con los siguientes comandos

`sudo smbpasswd -a USUARIO` Luego de este comando asigne la contraseña

`sudo smbpasswd -e USUARIO`


### INSTALACIÓN DEL SERVIDOR - POSTFIX

1. Proceda a instalar el paquete de postfix

   `sudo dnf install postfix devecot -y`

2. Configurar postfix
    Utilizamos `sudo nano /etc/postfix/main.cf`

   `sudo systemctl enable postfix`

   `sudo systemctl start postfix`
3. Configurar Dovevecot (IMAP)
    `sudo nano /etc/devecot/devecot.conf`
    agregamos la palabra "imap"
4. Creamos usuarios de correo
   `sudo useradd usuario1`
   `sudo passwd usuario1`
   `sudo useradd usuario2`
   `sudo passwd usuario2`

5. Iniciamos servicios
     `sudo systemctl enable --now postfix`
     `sudo systemctl enable --now devecot`
6. Abrimos los puertos de correo
     `sudo firewall-cmd --add-service=smtp --permanent`
     `sudo firewall-cmd --add-service=imap --permanent`
7. Reiniciamos el firewall
     `sudo firewall-cmd --reload`
   
8. Empiece con la configración

      `sudo nano /etc/postfix/main.cf`
      
9. Configure el firewall
   
`sudo firewall-cmd --permanent --add-service=smtp`

`sudo firewall-cmd --permanent --add-service=smtps`

`sudo firewall-cmd --reload`

10. Reinicie Postfix

   `sudo systemctl restart postfix`

11. Verifique el estado
   
   `sudo systemctl status postfix.service`
   
12. Pruebe el servicio (Instalar paquete si es necesario)

   `echo "Prueba de Postfix en CentOS 9" | mail -s "Correo de prueba" tuemail@dominio.com`

13. Revise cola de correos

      `sudo mailq`


### INSTALACIÓN DEL SERVIDOR - DNS

1. Actualice
   1. Instalamos y configuramos DNS (BIND)
     **Instalamos**
   "sudo dns install bind bind-utils -y"
   2. Editar configuración principal
   Ingresamos en "sudo nano /etc/named.conf"
   Cambiamos por:
   listen-on port 53 { any; };
   allow-query     { any; };
   3. Creamos zona directa
   "sudo nano /etc/named.rfc1912.zones"
   Añadimos al final
   zone "matute.local" IN {
    type master;
    file "matute.local.db";
};

   4. Creamos archivo de zona
   Ingresamos en "sudo nano /var/named/matute.local.db"
   5. Damos permisos y arranque
   "sudo chown root:named /var/named/matute.local.db"
   "sudo chmod 640 /var/named/matute.local.db"
   "sudo systemctl enable --now named"
   6. Abrir puerto DNS (sin desactivar firewall)
   "sudo firewall-cmd --add-service-dns --permanent"
   "dig www.matute.local
   
