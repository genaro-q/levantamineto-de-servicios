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
1. Abrir el software de virtualizacion: Inicie VirtualBox y haga click en "Nueva Maquina Virtual"

     **Asignamos Recursos**
      
     **Nombre:** Asignamos un nombre descriptivo, como "Servidor Centos" en este caso

     **Tipo:** Selccionamos "Linux"

     **Version:** Elegimos "Red Hat (64-bit)"

     **Memoria RAM:** Asignamos al menos 2GB (2048 MB)

     **Disco Duro:** Crea un disco virtual de al menos 20GB

     Montar la Imagen ISO: En la configuracion de la maquina virtual, seleccionamos la imagen ISO de CentOS descargada 
     previamente como medio de arranque

   <p align="center">
   <img src="https://github.com/user-attachments/assets/da30f6e1-60d7-45b0-aca5-7a9caa5ae063" alt="Imagen de instalación" width="80%">
</p>

### INSTALACIÓN DE SISTEMA OPERATIVO - CentOS 9 Stream
1. **Proceso de Instalación de CentOS**
   
      Una vez configurada la máquina virtual, iniciamos y seguimos estos pasos:
   
      Iniciar la Instalación:
      1. **Al arrancar la máquina virtual, aparecerá el menú de instalación de CentOS. Seleccionamos "Install CentOS " y 
      presionamos Enter.**

      2. **Selección de Idioma:**
      Elegimos el idioma preferido para la instalación y continuamos.

<p align="center">
   <img src="https://github.com/user-attachments/assets/571c1337-5e7a-4e4b-b44f-56620b45729d" alt="Imagen de instalación" width="80%">
</p>

  4. **Configuración de la Fecha y Hora:**
  Seleccionamos la zona horaria correspondiente.

  5. **Selección del Software:**
  Elegimos el entorno de software que deseamos instalar. Para un servidor básico, seleccionamos "Minimal Install". En 
  este caso necesitamos una interfaz gráfica por lo que elegimos "Server with GUI".

<p align="center">
   <img src="https://github.com/user-attachments/assets/acabcfbe-cf6b-4eb4-af98-6da15c4388b5" alt="Imagen de instalación" width="80%">
</p>

<p align="center">
   <img src="https://github.com/user-attachments/assets/8b32fff2-d910-4413-bd7e-0236a696cc3d" alt="Imagen de instalación" width="80%">
</p>

  6. **Configuración del Disco:**
  Seleccionamos el disco virtual creado y hacemos click en "Done". CentOS configurará automáticamente las particiones.

  7. **Configuración de Red:**
  Activamos la conexión de red para que la máquina virtual tenga acceso a Internet.

  8. **Creación de Usuario:**
  Establece una contraseña para el usuario root y crea un usuario adicional para uso diario.

<p align="center">
   <img src="https://github.com/user-attachments/assets/9267e8d5-f595-4d24-a801-e411f5f445a0" alt="Imagen de instalación" width="80%">
</p>

  9. **Iniciar la Instalación:**
  Haz clic en "Begin Installation" y espera a que el proceso termine. Esto 
  puede tardar varios minutos.

  10. **Post-Instalación**
  Una vez completada la instalación, reiniciamos la máquina virtual y 
  seguimos estos pasos:
  Iniciar Sesión: Ingresamos con el usuario creado durante la instalación.
  Actualizar el Sistema: Ejecutamos el comando sudo yum update para 
  asegurarnos de que el sistema esté actualizado.

<p align="center">
   <img src="https://github.com/user-attachments/assets/eaa34836-5abf-4276-a891-ee667fc8a1e2" alt="Imagen de instalación" width="80%">
</p>

### INSTALACIÓN DEL SERVIDOR - SSH
1. Empezamos ejecutando el comando “sudo dnf install -y openssh-server” para instalar el servicio de ssh.
   
`sudo dnf install -y openssh-server`

<p align="center">
  <img src="https://github.com/user-attachments/assets/713117f6-4b29-4253-aefe-6f64cf2d3994" alt="Imagen de instalación" width="80%">
</p>


2. Seguido de la instalación agregamos el servicio de ssh al firewall.

`sudo firewall-cmd --permanent --add-service=ssh`

`sudo firewall-cmd --reload`
   
<p align="center">
   <img src="https://github.com/user-attachments/assets/89db1527-5dfd-4685-b9a4-a1cab7be229e" alt="Imagen de instalación" width="80%">
</p>


3. Continuamos agregando el puerto “54321” a la configuración del nano

`PORT 54321`

<p align="center">
   <img src="https://github.com/user-attachments/assets/d39b6840-63a5-4353-b1f8-09cf82e780d8" alt="Imagen de instalación" width="80%">
</p>


4. Para terminar agregamos el puerto “54321” a la configuración del firewall para evitar problemas de conectividad con el funcionamiento del servicio

`sudo firewall-cmd --permanent --add-port=54321/tcp`

`sudo firewall-cmd --reload`

<p align="center">
   <img src="https://github.com/user-attachments/assets/9f1496a9-d567-4b7e-af44-928bc3acd3be" alt="Imagen de instalación" width="80%">
</p>


5. Reiniciamos el servicio ssh para actualizar los cambios y que empiece su funcionamiento

`sudo systemctl restart sshd`

  <p align="center">
    <img src="https://github.com/user-attachments/assets/c1c57d55-e1e9-42c1-a475-c93a4debd205" alt="Imagen de instalación" width="80%">
    </p>

    
6. Conectamos el servicio

`ssh localhost -p 54321`

   <p align="center">
   <img src="https://github.com/user-attachments/assets/96a17632-e6e8-4b8e-9397-48c2c9ed4bf7" alt="Imagen de instalación" width="80%">
   </p>


   7. Conexión remota con mobaxterm

   <p align="center">
<img src="https://github.com/user-attachments/assets/482a467e-ea29-4aff-bb31-11241c05710d" alt="Imagen de instalación" width="80%">
</p>



### INSTALACIÓN DEL SERVIDOR - SAMBA
1. Para que pueda empezar con la instalacion de samba hay que hacer un update.

   `sudo dnf update`

2. Utilice el siguiente comando para instalar samba

   `sudo dnf install samba samaba-cammon samba-client`

<p align="center">
<img src="https://github.com/user-attachments/assets/0067acde-1200-4b4e-b272-41cd39c200cb" alt="Imagen de instalación" width="80%">
</p>

3. Cree un directorio usando el siguiente comando

   `mkdr ~/CARPETA`

<p align="center">
<img src="https://github.com/user-attachments/assets/1ef6dc5b-7d4a-4cc1-acd3-d9728ed71f5e" alt="Imagen de instalación" width="80%">
</p>

4. Abra el archivo nano de samba y agregamos lo siguiente al final del archivo
   
`sudo nano /etc/samba/smb.conf`

<p align="center">
<img src="https://github.com/user-attachments/assets/9a5115e6-eefc-4f6d-b871-92cd8d13ce55" alt="Imagen de instalación" width="80%">
</p>

5. Configure los permisos de firewall para que no haya errores al abrir

   `sudo systemctl stop firewalld`

 <p align="center">
<img src="https://github.com/user-attachments/assets/695d5291-84fc-4878-9f86-a8dff2e7da4c" alt="Imagen de instalación" width="80%">
</p>  

`sestatus`

 <p align="center">
<img src="https://github.com/user-attachments/assets/c39b9253-05d2-46a7-ab75-bc9806e95f70" alt="Imagen de instalación" width="80%">
</p> 

`sudo restorecon -Rv “/home/usuario/DIRECTORIO"`

`sudo systemctl restart smb`

6. Asigne contraseña al usuario de samba con los siguientes comandos

`sudo smbpasswd -a USUARIO` Luego de este comando asigne la contraseña

`sudo smbpasswd -e USUARIO`






### INSTALACIÓN DEL SERVIDOR - POSTFIX

1. Proceda a instalar el paquete de postfix

   `sudo dnf install postfix -y`

<p align="center">
   <img src="https://github.com/user-attachments/assets/2da7e2b7-4123-4366-a62e-6380704f90b5" alt="Imagen de instalación" width="80%">
</p>


2. Habilite como servicio predeterminado

   `sudo systemctl enable postfix`

   `sudo systemctl start postfix`

<p align="center">
   <img src="https://github.com/user-attachments/assets/97180813-f0c1-4300-af88-7ad805b6c8d5" alt="Imagen de instalación" width="80%">
   </p>


3. Empiece con la configración

      `sudo nano /etc/postfix/main.cf`

   <p align="center">
      <img src="https://github.com/user-attachments/assets/306b3aee-f751-48a1-aa8d-2f32e1796e29" alt="Imagen de instalación" width="80%">
      </p>
      
      <p align="center">
      <img src="https://github.com/user-attachments/assets/97a4ed85-9c8d-49a7-8c44-efda69ac599e" alt="Imagen de instalación" width="80%">
      </p>


4. Configure el firewall
   
`sudo firewall-cmd --permanent --add-service=smtp`

`sudo firewall-cmd --permanent --add-service=smtps`

`sudo firewall-cmd --reload`

<p align="center">
<img src="https://github.com/user-attachments/assets/80efab2b-8998-4b82-9258-2a526c6c36d3" alt="Imagen de instalación" width="80%">
</p>


5. Reinicie Postfix

   `sudo systemctl restart postfix`

   <p align="center">
   <img src="https://github.com/user-attachments/assets/6c9daa4f-ff68-4746-90a9-b5710fbd4269" alt="Imagen de instalación" width="80%">
</p>


6. Verifique el estado
   
   `sudo systemctl status postfix.service`
   
<p align="center">
<img src="https://github.com/user-attachments/assets/c3cdcc4b-96cd-4cef-bf8a-8c080da97560" alt="Imagen de instalación" width="80%">
</p>


7. Pruebe el servicio (Instalar paquete si es necesario)

   `echo "Prueba de Postfix en CentOS 9" | mail -s "Correo de prueba" tuemail@dominio.com`

   <p align="center">
   <img src="https://github.com/user-attachments/assets/70d140c9-3b6a-4c94-98d8-6ddbc1b56e05" alt="Imagen de instalación" width="80%">
   </p>


8. Revise cola de correos

      `sudo mailq`

      <p align="center">
      <img src="https://github.com/user-attachments/assets/cf7bdf73-56fc-462a-b887-4c72e7af00e2" alt="Imagen de instalación" width="80%">
      </p>


### INSTALACIÓN DEL SERVIDOR - PLEX
1. Descargue el plex, descargar el que esta subrayado

   <p align="center">
    <img src="https://github.com/user-attachments/assets/77a10fc6-f27b-4f2a-bd30-77c0c2e9fc39" alt="Imagen de instalación" width="80%">
    </p>

2. Abra la carpeta descargada e instalamos

   <p align="center">
     <img src="https://github.com/user-attachments/assets/dd2f660f-2a1a-4db5-9b94-655d564c90d5" alt="Imagen de instalación" width="80%">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/8aff06dc-709f-4ab1-9b58-ff5fb6bcf148" alt="Imagen de instalación" width="80%">
</p>

3. Active e inicie plex

   `sudo systemctl enable plexmediaserver.service`

   `sudo systemctl start plexmediaserver.service`

   <p align="center">
   <img src="https://github.com/user-attachments/assets/74811c50-78b4-40c5-8317-f615fcecf96d" alt="Imagen de instalación" width="80%">
   </p>
   
4. Configure el firewall añadiendo el puerto "32400"

   `sudo firewall-cmd --add-port=32400/tcp --permanent`

   `sudo firewall-cmd -reload`

<p align="center">
<img src="https://github.com/user-attachments/assets/40a37ad1-0c3b-47c0-a4f6-409b4eace939" alt="Imagen de instalación" width="80%">
</p>

5. Acceda a plex desde el navegador usando "https://<ip-servidor-centos>:32400/web" (si no funciona con la ip del servidor) pruebe con esto "https://localhost:32400/web"

   <p align="center">
   <img src="https://github.com/user-attachments/assets/e0883ae8-c91f-4b83-8d29-436da4e1a0a3" alt="Imagen de instalación" width="80%">
   </p>

6. Configure plex, cree una cuenta

   <p align="center">
   <img src="https://github.com/user-attachments/assets/f0ae263d-c91e-41da-8c6b-8706e42fd936" alt="Imagen de instalación" width="80%">
      </p>

7. Una vez creada la cuenta proceda a darle un nombre a la empresa

   <p align="center">
   <img src="https://github.com/user-attachments/assets/fb3c3ff5-581e-4a41-a80c-1b69ac40f2ba" alt="Imagen de instalación" width="80%">
      </p>

8. Posteriormente de click en el nombre de la emprea para poder agregar bibliotecas

<p align="center">
   <img src="https://github.com/user-attachments/assets/d83ddc72-bae5-4fb8-aab8-10c0d92e7018"
 alt="Imagen de instalación" width="80%">
      </p>

9. Añada a la biblioteca

    <p align="center">
   <img src="https://github.com/user-attachments/assets/e990b19a-9353-4e52-ad46-f6e679dcdb80" alt="Imagen de instalación" width="80%">
      </p>

10. De un nombre a la carpeta y siguiente

  <p align="center">
   <img src="https://github.com/user-attachments/assets/52ae1835-e673-428f-9ba5-226715cd8ccb" alt="Imagen de instalación" width="80%">
      </p>

### INSTALACIÓN DEL SERVIDOR - DNS

1. Actualice
   
`sudo yum update -y`

2. Instale paquete bind

  `sudo yum install -y bind bind-utils`

3. Habilite DNS

`sudo systemctl enable named`

4. Configure firewall

   `sduo firewall-cmd --permanent --xone=public --add-service=dns`

5. Configure servidor DNS

   `sudo nano /etc/named.conf`

   <p align="center">
   <img src="https://github.com/user-attachments/assets/e5e64f72-e7e1-4583-8e28-12644b0e8c3b"
 alt="Imagen de instalación" width="80%">
      </p>

6. Desactive las líenas "listen on" y "listen on v6" usando #

   <p align="center">
   <img src="https://github.com/user-attachments/assets/84f20caf-fd3b-446d-8db4-453e98f93c42" alt="Imagen de instalación" width="80%">
      </p>

7. Busque la líena "allow-query" y sustituye "localhost" por "any"

   <p align="center">
   <img src="https://github.com/user-attachments/assets/ecae5d1e-422b-478a-9471-71ab3c18d5e4" alt="Imagen de instalación" width="80%">
      </p>

8. Guarde los cambios y compruebe que no hay errores en la configuración

   `sudo named-checkconf`

   <p align="center">
   <img src="https://github.com/user-attachments/assets/5836e06b-d657-4315-ab90-183a008d608f" alt="Imagen de instalación" width="80%">
      </p>

   si no se produce ninguna salida significa que todo esta correcto

9. Inicie el servidor

    `sudo systemctl start named`

     <p align="center">
   <img src="https://github.com/user-attachments/assets/565cfd6a-5b3e-4b0b-8192-b03f5dedbaee" alt="Imagen de instalación" width="80%">
      </p>

10. Verifique el estado
    
`sudo systemctl status named`
    
<p align="center">
   <img src="https://github.com/user-attachments/assets/b62a011d-1d62-4f00-8a87-3880d8fa7822"
 alt="Imagen de instalación" width="80%">
      </p>

11. Creamos un archivo de configuración adicionales

    `sudo nano /etc/NetworkManager/conf.d/10-dns.conf`

<p align="center">
   <img src="https://github.com/user-attachments/assets/8a8f8ae9-146f-4a17-be7f-f893efb62186"
alt="Imagen de instalación" width="80%">
      </p>

12. Recargue la configuracion

    `sudo systemctl reload NetworkManager`

<p align="center">
   <img src="https://github.com/user-attachments/assets/cde19e15-ed0e-48ac-949f-212aff12d525"
alt="Imagen de instalación" width="80%">
      </p>

13. Edite el siguiente archivo

    `sudo nano /etc/resolv/conf`

<p align="center">
   <img src="https://github.com/user-attachments/assets/3bc78086-a5b7-420b-aa62-291f2e89b33c"
alt="Imagen de instalación" width="80%">
      </p>

14. En la primera líena de nameserver agregue un #, guarde y cierre

<p align="center">
   <img src="https://github.com/user-attachments/assets/dc1269f6-4118-47f1-8dbc-29a20a7b855a"
alt="Imagen de instalación" width="80%">
      </p>

15. Treas gurdar los cambio y cerrar el archivo, ya puede probar la resolucion de nombres en cualquier maquina de red, con el comando "nslookup" y el domino de internet que prefiera

`nslookup kernel.org`

<p align="center">
   <img src="https://github.com/user-attachments/assets/a064f8df-9d65-4efc-9963-4213c2e67ef0" alt="Imagen de instalación" width="80%">
      </p>
    
### INSTALACIÓN DEL SERVIDOR - ISSABEL
1. Cree una maquina cirtual con la iso previamente descara de su pagina oficial

  Omitimos la instalacion desatendida, y seleccionamos "OTHER LINUX (64- bit)"

  <p align="center">
   <img src="https://github.com/user-attachments/assets/79273cc1-5649-4d07-9753-cae54e665f70" alt="Imagen de instalación" width="80%">
      </p>

2. Deje las especificaciones dl hardware por defecto, luego, dentro de las configuraciones de red cambiamos la conexion a adaptador puente

3. Proceda a iniciar con la instalacion como un sistema operativo normal. (Arranque con la opcion: test this media & install.

4. A continuacion configure diferentes aspectos como:
     - Seleccion  de Sfotware - Issabel con Aesterik 18
     - Idioma de Teclado
     - Destino de la Instalacion
     - Creacion de usuario y contraseña de root

<p align="center">
   <img src="https://github.com/user-attachments/assets/74e08369-d1be-43dd-a0ae-4670249b2a9c" alt="Imagen de instalación" width="80%">
      </p>

  En el destino de la isntalacion active la opcion personalizada

  <p align="center">
   <img src="https://github.com/user-attachments/assets/41247ff5-8dfc-4e3d-b0ca-e7f20f634568" alt="Imagen de instalación" width="80%">
      </p>

  A continuacion, haga la configuracion automatica

  <p align="center">
   <img src="https://github.com/user-attachments/assets/69b33f5c-fa7b-446d-b84d-896ef4a5577c" alt="Imagen de instalación" width="80%">
      </p>

  Sin cambiar nada, haga click en hecho, y acepte los cambios.

  En el apartado de red, cambie el nombre del equipo, y aplique los cambios

   <p align="center">
   <img src="https://github.com/user-attachments/assets/b2e1b73e-35a3-4616-9ae2-5ca6054f4033" alt="Imagen de instalación" width="80%">
      </p>

5. Empiece con la instalacion y espere que acabe la descarga, una vez cargado el sistema empezamos a configurar Issabel

   Empiece agregando una contraseña a la base de datos

   <p align="center">
   <img src="https://github.com/user-attachments/assets/51a93656-af3e-4cfa-8507-97c5ff4c15e8" alt="Imagen de instalación" width="80%">
      </p>

   Ingrese una contraseña para el usuario administrador
   
<p align="center">
   <img src="https://github.com/user-attachments/assets/e2e36d6a-3aab-42e3-8cdf-857b1599e0ca" alt="Imagen de instalación" width="80%">
      </p>

   Elija un idioma
   
<p align="center">
   <img src="https://github.com/user-attachments/assets/d4339f9f-3abd-4811-a64b-35f8d777a770" alt="Imagen de instalación" width="80%">
       </p>

  Elija la segunda opcion, ya que la primera ya no recibe mantenimiento en Aesterik
  
<p align="center">
   <img src="https://github.com/user-attachments/assets/4fda1496-99c6-4e3b-9255-2fbf67c9d5b0" alt="Imagen de instalación" width="80%">
       </p>

  Con la consola cargada, ingrese el usuario root y contraseña para poder ver las especificaciones de la instalaciones.
Como la ip “red local” con la que va a acceder desde el navegador.

<p align="center">
   <img src="https://github.com/user-attachments/assets/9a21822b-7882-49b5-ace2-917d25a50497" alt="Imagen de instalación" width="80%">
       </p>

6. Ingrese a Issabel desde el navegador como anteriormente mencionamos

   Al ingresar por primera vez, tendra que seleccionar la opción Avanzado → Continuar a IP (no seguro).
   
<p align="center">
   <img src="https://github.com/user-attachments/assets/bded0f62-351e-4427-b5fd-cbb31ba47813" alt="Imagen de instalación" width="80%">
       </p>

   Ahora ingrese el usuario y la contraseña asignada anteriormente, y con eso ya estaria funcionando el servidor

   <p align="center">
   <img src="https://github.com/user-attachments/assets/40466439-59f4-4fc5-8e76-67cd93bc18dd" alt="Imagen de instalación" width="80%">
       </p>

7. Primera extension

   PRIMERA - EXTENSIÓN
EXTENSIÓN PARA LLAMADAS : zoiper softphone “TELÉFONO”, descarguela en

`https://www.zoiper.com/en/voip-softphone/download/current`

Dentro del enlace, instale el archivo para windows con la opción gratuita.

Ejecute e  instale la aplicación telefónica como una aplicación común de Windows

8. Configuracion del servidor

   Agregaremos una extensión:
PBX - PBX Configuration - Aplications - Extensions

<p align="center">
   <img src="https://github.com/user-attachments/assets/f43ece4c-a21c-4e5c-ba4c-58c592a778d7" alt="Imagen de instalación" width="80%">
       </p>

Agregue la extensión, nombre.
Y elimine la contraseña del apartado Secret, para que quede en blanco

<p align="center">
   <img src="https://github.com/user-attachments/assets/286e4fdd-da73-4a65-b214-8ba2951cea1b" alt="Imagen de instalación" width="80%">
       </p>

suba la primera extensión

<p align="center">
   <img src="https://github.com/user-attachments/assets/7dfcc4cc-94d0-42e5-882d-6a2df08bc9df" alt="Imagen de instalación" width="80%">
       </p>
       
SEGUNDA - EXTENSIÓN
De igual manera agregue una nueva extensión, ingresando una extensión y nombre de usuario.

<p align="center">
   <img src="https://github.com/user-attachments/assets/d147e88e-0459-485a-9293-d97667f2d18d" alt="Imagen de instalación" width="80%">
       </p>
    
Elimine la contraseña, y guarde los cambios.
Ahora aplique los cambios

<p align="center">
   <img src="https://github.com/user-attachments/assets/f22031f5-18bc-4863-990b-4e6c9c59d25b" alt="Imagen de instalación" width="80%">
       </p>

ZOIPER
Dentro de la aplicación cree una cuenta gratis.
En el usuario, ingrese la extensión y la ip de Isabel
“EXTENSIÓN” @ “IP”
Y asignele una contraseña al usuario

<p align="center">
   <img src="https://github.com/user-attachments/assets/1ed72faa-5b6f-42b9-a7f8-ce8f0135b9c8" alt="Imagen de instalación" width="80%">
       </p>

Seguido de esto haga click en siguiente, y saltar

<p align="center">
   <img src="https://github.com/user-attachments/assets/afb974f5-4f4e-4777-9ea9-82601153b34c"
 alt="Imagen de instalación" width="80%">
       </p>


