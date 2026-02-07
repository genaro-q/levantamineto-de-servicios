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
1. Instalamos y configuramos DNS (BIND)
     **Instalamos**
   "sudo dns install bind bind-utils -y"
     **Editar configuración principal**
   Ingresamos en "sudo nano /etc/named.conf"
   Cambiamos por:
   listen-on port 53 { any; };
   allow-query     { any; };
    **Creamos zona directa**
   "sudo nano /etc/named.rfc1912.zones"
   Añadimos al final
   zone "matute.local" IN {
    type master;
    file "matute.local.db";
};

   **Creamos archivo de zona**
   Ingresamos en "sudo nano /var/named/matute.local.db"
    **Damos permisos y arranque**
   "sudo chown root:named /var/named/matute.local.db"
   "sudo chmod 640 /var/named/matute.local.db"
   "sudo systemctl enable --now named"
    **Abrir puerto DNS (sin desactivar firewall)**
   "sudo firewall-cmd --add-service-dns --permanent"
   "dig www.matute.local

### INSTALACIÓN DEL SERVIDOR - SSH
1. Empezamos ejecutando el comando “sudo dnf install -y openssh-server” para instalar el servicio de ssh.
   
`sudo dnf install -y openssh-server`

2. Seguido de la instalación agregamos el servicio de ssh al firewall.

`sudo firewall-cmd --permanent --add-service=ssh`

`sudo firewall-cmd --reload`
   
3. Continuamos agregando el puerto “2222” a la configuración del nano

`PORT 2222`

4. Para terminar agregamos el puerto “2222” a la configuración del firewall para evitar problemas de conectividad con el funcionamiento del servicio

`sudo firewall-cmd --permanent --add-port=2222/tcp`

`sudo firewall-cmd --reload`

5. Reiniciamos el servicio ssh para actualizar los cambios y que empiece su funcionamiento

`sudo systemctl restart sshd`
    
6. Conectamos el servicio

`ssh localhost -p 2222`

 7. Conexión remota con mobaxterm

### INSTALACIÓN DEL SERVIDOR - APACHE
1. Para que pueda empezar con la instalacion de apache hay que hacer un update.

   `sudo dnf update`

2. Utilice el siguiente comando para instalar apache

   "sudo dnf install httpd -y"
   **Creamos un Virtualhost**

   **Creamos un sitio web**
   "sudo mkdir /var/www/matute
   **Le damos permisos y arranque**
   "sudo chown -R apache:apache /var/www/matute"
   "sudo systemctl enable httpd"
   **Abrimos puerto web**
   "sudo firewall-cmd --add-service=http --permanent
   **Prueba en la web**

3. Cree un directorio usando el siguiente comando

   `mkdr ~/CARPETA`
   
5. Abra el archivo nano de samba y agregamos lo siguiente al final del archivo
   
`sudo nano /etc/samba/smb.conf`

5. Configure los permisos de firewall para que no haya errores al abrir

   `sudo systemctl stop firewalld`
`sestatus`



`sudo restorecon -Rv “/home/usuario/DIRECTORIO"`

`sudo systemctl restart smb`

6. Asigne contraseña al usuario de samba con los siguientes comandos

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
   
3. Empiece con la configración

      `sudo nano /etc/postfix/main.cf`
      
4. Configure el firewall
   
`sudo firewall-cmd --permanent --add-service=smtp`

`sudo firewall-cmd --permanent --add-service=smtps`

`sudo firewall-cmd --reload`

5. Reinicie Postfix

   `sudo systemctl restart postfix`

6. Verifique el estado
   
   `sudo systemctl status postfix.service`
   
7. Pruebe el servicio (Instalar paquete si es necesario)

   `echo "Prueba de Postfix en CentOS 9" | mail -s "Correo de prueba" tuemail@dominio.com`

8. Revise cola de correos

      `sudo mailq`


### INSTALACIÓN DEL SERVIDOR - DNS

1. Actualice
   1. Instalamos y configuramos DNS (BIND)
     **Instalamos**
   "sudo dns install bind bind-utils -y"
     **Editar configuración principal**
   Ingresamos en "sudo nano /etc/named.conf"
   Cambiamos por:
   listen-on port 53 { any; };
   allow-query     { any; };
    **Creamos zona directa**
   "sudo nano /etc/named.rfc1912.zones"
   Añadimos al final
   zone "matute.local" IN {
    type master;
    file "matute.local.db";
};

   **Creamos archivo de zona**
   Ingresamos en "sudo nano /var/named/matute.local.db"
    **Damos permisos y arranque**
   "sudo chown root:named /var/named/matute.local.db"
   "sudo chmod 640 /var/named/matute.local.db"
   "sudo systemctl enable --now named"
    **Abrir puerto DNS (sin desactivar firewall)**
   "sudo firewall-cmd --add-service-dns --permanent"
   "dig www.matute.local
   
