# Pasos para configurar ssh en la máquina host:

## Generar clase ssh
Vamos a necesitar una clave ssh para conectarnos con los entornos remotos.
**Comando a ejecutar:** `ssh-keygen`
Esto genera 2 ficheros:
- ~/.ssh/id_rsa
- ~/.ssh/id_rsa.pub

Mostramos el contenido del segundo con el comando `cat ~/.ssh/id_rsa.pub`
El contanido será similar a:
> ubuntu:~/environment $ cat /home/ubuntu/.ssh/id_rsa.pub 
> ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC2k8seRSiNsv14w5DQkld1E3mTUs/zzeBW2S5zg7i1IDlfPvSAh4JWjvWjxgDYiFzWoL6KsQryeYvTmet2Pni6cnw6NYtyVdxtb1VkYwXH4RDtHXj81cNT7xS3l6c9aBPWiK8Y4dggJQhlmAbfFDZyx7W/frjDWSeq1CGnxr1Xih0f35h3vNn1CaDVIGyR4YzQO+fzzqp8uIZhQrbRmlSEmm9eoYb7wSlnIDtX3AZDGcYWsOlo6zAV7aT1nxntLK5g+HNY69RS52o1m7rDa7JN+0Z7hEqP9bct2niIw0iYIn0IBONaXuscMH5R2fRA6i8tfS/2kvEdq3RGyqtwC2oB ubuntu@ip-172-31-30-186

## Crear un fichero de configuración
En este fichero, que se situará en ~/.ssh/config, daremos de alta los distintos servidores a los que acederemos vía ssh.
Para cada fichero tendremos un bloque como el siguiente:
>Host ubuntu01
>  Hostname 172.17.0.2
>  User root
>  PubKeyAuthentication yes
>  IdentityFile ~/.ssh/id_rsa

Para copiar el fichero config suministrado se ejecuta: 

## Copiar la clave en el entorno al que nos vayamos a conectar por ssh
Será necesario dar de alta la clave que hemos mostrado arriba (id_rsa.pub), dentro del entorno al que se vaya a acceder.
Para ello, dentro del entorno, debe existir un fichero ~/.ssh/authorized_keys. 
En ese fichero se dan de alta las claves de los entornos a los que se autoriza a acceder a este.
Dentro de ese fichero se copia el contenido de id_rsa.pub.
Para ello puede utilizarse:
> echo 'CONTENIDO DE id_rsa.pub' >> ~/.ssh/authorized_keys

## Realizar un primer acceso
Mediante el comando `ssh root@<IP_O_HOSTNAME>`
Cuando solicite permiso para dar de alta al entorno remoto, aceptarlo tecleando `yes`

## Comprobar de nuevo el acceso
Esta vez ya debe ser silencioso: debe entrar sin solicitar ningún tipo de información ni confirmación.
Ejecutar de nuevo el comando `ssh root@<IP_O_HOSTNAME>`
