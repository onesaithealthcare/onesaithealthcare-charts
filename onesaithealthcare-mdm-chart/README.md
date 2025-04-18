# Onesait Healthcare Chart: onesaithealthcare-mdm-chart

Este Chart instala los módulos core de la solución.

## Prerrequisitos

- Se requiere un repositorio docker con las imágenes de los módulos.  Se deberá crear un secret con el nombre 
  oh-docker-creds que contenga las credenciales para el repositorio que se vaya a usar.

- Entre los parámetros del chart se deberá indicar el protocolo y dominio con el que se expondrán los públicamente los módulos.

- Se debe crear previamente el gateway oh-modules-gateway según la infraesctructura disponible en el cluster k8s (istio o k8s-gateway,
  se deberá consultar y seguir la guía apropiada según el caso).  
  
## Módulos

- ohcommons: configuraciónes comunes
- OHSSO
- OHCON
- OHAUT
- OHONT
- OHMPI
- OHATN

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



