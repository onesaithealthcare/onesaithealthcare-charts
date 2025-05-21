# Onesait Healthcare Chart: onesaithealthcare-mdm-chart

Este Chart instala los módulos core de la solución.

## Prerrequisitos

- Se requiere un repositorio docker con las imágenes de los módulos.
- Se deberá crear un secret con el nombre "*oh-docker-creds*" que contenga las credenciales para el repositorio que se vaya a usar.

- Entre los parámetros del chart se deberá indicar el protocolo y dominio con el que se expondrán públicamente los módulos.

- Se debe crear previamente el gateway "*oh-modules-gateway*" según la infraesctructura disponible en el cluster k8s (istio o k8s-gateway,
  se deberá consultar y seguir la guía apropiada según el caso).  
  
## Módulos

- ohcommons: configuraciónes comunes
- OHSSO
- OHCON
- OHAUT
- OHONT
- OHMPI
- OHATN
- OHDSK

## WebComponent genéricos

- OHWCFORM
- OHWCVIEWER

## Instalación

1. Agregar el repositorio Helm (si no se tenía ya agregado):
   ```sh
   helm repo add onesaithealthcare https://github.com/onesaithealthcare/onesaithealthcare-charts
   helm repo update
   ```

2. Instalar el chart:
   ```sh
   helm install mi-release onesaithealthcare/onesaithealthcare-mdm-chart --namespace oh-modules
   ```

## Operaciones post instalación

- Una vez arrancado ohsso se deberá crear el realm oh-base importando el archivo: 
[Descargar realm-export-oh-base.json](https://onesaithealthcare.github.io/onesaithealthcare-charts/extras/onesaithealthcare-mdm/realm-export-oh-base.json)
Acceder al client hnrole y añadir la redirect uri correspondiente al dominio del entorno donde se está desplegando.
Reiniciar ohsso y los despliegues de backend.


