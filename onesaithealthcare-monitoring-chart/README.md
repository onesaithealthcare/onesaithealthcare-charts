# Onesait Healthcare Chart: onesaithealthcare-monitoring-chart

Este Chart instala los módulos de Onesait Healthcare Monitoring.

## Prerrequisitos

- Se debe haber instalado y configurado previamente el chart MDM (onesaithealthcare-mdm-chart).  

- Se debe disponer de un Storage Class con provisión dinámica.
  
## Módulos

- Prometheus
- Grafana

## Operaciones pre instalación

1. ???



## Instalación

1. Agregar el repositorio Helm (si no se tenía ya agregado):
   ```sh
   helm repo add onesaithealthcare https://github.com/onesaithealthcare/onesaithealthcare-charts
   helm repo update
   ```

2. Instalar el chart con el siguiente comando (o usando los formularios si la plataforma kubernetes usada tiene dicha posibilidad):
   ```sh
   helm install mi-release onesaithealthcare/onesaithealthcare-monitoring-chart --namespace oh-modules
   ```

## Operaciones post instalación

1. ¿Configuración prometheus?

2. ¿Configuración grafana?








