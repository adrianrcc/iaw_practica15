# Implantación de Aplicaciones Web - Práctica 15

Adrián Ramírez-Cruzado Carmona

2º CFGS Admón. de Sistemas Informáticos en Red

IES Celia Viñas (Almería) - 2020/2021

# Repositorio del proyecto

- [https://github.com/adrianrcc/iaw_practica15](https://github.com/adrianrcc/iaw_practica15)

# Práctica 15: Instalación de WordPress usando contenedores Docker y Docker Compose

## Descripción del proceso:

En esta práctica tendremos que realizar la implantación de un sitio WordPress en Amazon Web Services (AWS) haciendo uso de contenedores Docker y la herramienta Docker Compose.

### 1. Tareas a realizar

A continuación se describen muy brevemente algunas de las tareas que tendrá que realizar.

- Crear una máquina virtual Amazon EC2.

- Instalar y configurar Docker y Docker compose en la máquina virtual.

- Crear un archivo docker-compose.yml para poder desplegar los servicios de WordPress, MySQL y phpMyAdmin. Deberá utilizar las imágenes oficiales de Docker Hub.

- Buscar cuál es la dirección IP pública de su instancia en AWS y comprobar que puede acceder a los servicios de WordPress y phpMyAdmin desde una navegador web.

### 2 Requisitos del archivo docker-compose.yml
#### 2.1 Networks

Los servicios definidos en el archivo docker-compose.yml deberán usar dos redes:

- frontend-network
- backend-network

En la red frontend-network estarán los servicios:

- WordPress
- phpMyAdmin

Y en la red backend-network sólo estará el servicio:

- MySQL

Sólo los servicios que están en la red frontend-network expondrán sus puertos en el host. Por lo tanto, el servicio de MySQL no deberá estar accesible desde el host.

#### 2.2 Docker restart policies

Deberá utilizar alguna política de reinicio para que los contenedores se reinicien cada vez que se detengan de forma inesperada.

#### 2.3 Variables de entorno

Deberá hacer uso de un archivo .env para almacenar todas las variables de entorno que necesite en el archivo docker-compose.yml.

#### 2.4 Orden en el que se inician los servicios

Deberá indicar el orden en el que se deben iniciar los servicios con la opción depends_on.