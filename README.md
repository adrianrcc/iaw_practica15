# Implantación de Aplicaciones Web - Práctica 15

Adrián Ramírez-Cruzado Carmona

2º CFGS Admón. de Sistemas Informáticos en Red

IES Celia Viñas (Almería) - 2020/2021

# Repositorio del proyecto

- [https://github.com/adrianrcc/iaw_practica15](https://github.com/adrianrcc/iaw_practica15)

# Práctica 15: Instalación de WordPress usando contenedores Docker y Docker Compose

## Descripción del proceso:

En esta práctica realizaremos la implantación de un sitio WordPress en Amazon Web Services (AWS) haciendo uso de contenedores Docker y la herramienta Docker Compose.

### 1. Tareas a realizar

A continuación se describen muy brevemente algunas de las tareas que llevaremos a cabo:

- Crear una máquina virtual Amazon EC2.

- Instalar y configurar Docker y Docker compose en la máquina virtual.

- Crear un archivo docker-compose.yml para poder desplegar los servicios de WordPress, MySQL y phpMyAdmin utilizando las imágenes oficiales de Docker Hub.

- Buscar cuál es la dirección IP pública de su instancia en AWS y comprobar que puede acceder a los servicios de WordPress y phpMyAdmin desde una navegador web.

### 2 Requisitos del archivo docker-compose.yml
#### 2.1 Networks

Los servicios definidos en el archivo docker-compose.yml usan dos redes:

- frontend-network
- backend-network

En la red frontend-network están los servicios:

- WordPress
- phpMyAdmin

Y en la red backend-network sólo está el servicio:

- MySQL

Sólo los servicios que están en la red frontend-network expondrán sus puertos en el host. Por lo tanto, el servicio de MySQL no deberá estar accesible desde el host: nosotros nos conectamos al puerto 80 y 8080 de la instancia de AWS, MySQL trabaja con la base de datos por detrás.

Como usamos la última versión de MySQL, para evitar que se use la contraseña de root en vez de la de mysql usamos el comando:
~~~
command: --default-authentication-plugin=mysql_native_password
~~~

#### 2.2 Docker restart policies

Usamos una política de reinicio para que los contenedores se reinicien cada vez que se detengan de forma inesperada.

~~~
restart: always
~~~

#### 2.3 Orden en el que se inician los servicios

"depends_on" expresa la dependencia entre los servicios, es decir, "docker-compose up" iniciará los servicios en orden de dependencia. 

~~~
depends_on: 
      - mysql
~~~

Nota: depends_on no esperará a que mysql esté "listo" antes de iniciar phpmyadmin y wordpress, sólo hasta que se hayan iniciado. 