# Onesait Healthcare Chart: onesaithealthcare-mdm-chart

Este Chart instala los módulos core de la solución.

## Prerrequisitos

- Se requiere un repositorio docker con las imágenes de los módulos.  En caso de no usar el repositorio de 
  Onesait Healthcare (docksdtr.indra.es) se deberá crear un secret con el nombre oh-docker-creds que contenga
  las credenciales para el repositorio que se vaya a usar.

- Entre los parámetros del chart se debe indicar el protocolo y dominio con el que se expondrán los módulos, por
  tanto se debe crear previamente el ingress o gateway de los módulos y para tener definidos dichos valores antes 
  de la instalación del chart.  
  
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



