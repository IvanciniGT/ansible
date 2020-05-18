##############################################################################
# Ejemplo de imagen para un contenedor con Ubuntu instalado y acceso ssh
##############################################################################

# Partimos de la ultima versión de Ubuntu
FROM ubuntu:latest    
MAINTAINER Ivan Osuna

# Se actualizan dependencias y librerias
RUN apt-get update          

# Instalación del servidor de ssh
RUN apt-get install -y openssh-server   
# Cración del directorio de ejecución del demonio
RUN mkdir /var/run/sshd                 

# Asignación de la contraseña del usuario root
RUN echo 'root:root' |chpasswd          

# Acceso permitido por ssh para root
RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config 
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config 

# Creación de la carpeta .ssh para el usuario root
RUN mkdir -p /root/.ssh 

# Generamos el fichero que contendrá las claves cuyo acceso está autorizado
RUN touch ~/.ssh/authorized_keys            
# Permisos adecuados para los ficheros de configuración de .ssh
RUN chmod -R go= ~/.ssh                     

# Para disponer de ping
RUN apt-get install iputils-ping -y         
# Para disponer de netstat
RUN apt-get install net-tools -y             
# Para disponer de python
RUN apt-get install python -y            
# Permitir acceso por ssh sin contraseña, sólo con claves
RUN echo 'PasswordAuthentication no' >> /etc/ssh/sshd_config 

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
## Borramos para aligerar las librerias y dependencias de los repos

# Abrimos puertos
# Requerido para ssh
EXPOSE 22       
## Otros puertos que a lo mejor utilizamos en ejemplos
EXPOSE 10000
EXPOSE 80
EXPOSE 8080
EXPOSE 3306

# Ejecutar el demonio de ssh
CMD    ["/usr/sbin/sshd", "-D"]
