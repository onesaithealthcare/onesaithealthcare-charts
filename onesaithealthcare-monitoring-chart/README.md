# Onesait Healthcare Chart: onesaithealthcare-monitoring-chart

Este Chart instala los módulos de Onesait Healthcare Monitoring.

## Prerrequisitos

- Se debe haber instalado y configurado previamente el chart MDM (onesaithealthcare-mdm-chart).  

- Se debe disponer de un Storage Class con provisión dinámica.

- Acceder a OHSSO, si se tiene instalado el client oh-monitoring apuntar las credenciales del mismo ya que se utilizarán en la instalación del Chart.
  Si no se tiene instalado, acceder a Client Scopes y añadir los scopes (de tipo openid-connect): openid, groups.
  Importar el client oh-monitoring con el json proporcionado.
  Revisar que las redirectUris y urls base se corresponden con el subdominio del entorno.

- En openshift editar el SecurityContextConstraint anyuid y en la lista de users añadirle: 
  system:serviceaccount:<namespace-donde-se-instalara_el_chart>:oh-prometheus
  Por ejemplo:
  system:serviceaccount:oh-modules:oh-prometheus

- En openshift editar el SecurityContextConstraint hostmount-anyuid y en la lista de users añadirle:
  system:serviceaccount:<namespace-donde-se-instalara_el_chart>:oh-grafana
  Por ejemplo:
  system:serviceaccount:oh-modules:oh-grafana

- Comprobar que la NetworkPolicy cluster-network-policy-<namespace_instalacion> contiene los puertos: 9090, 9091 y 3000.
  
## Módulos

- Prometheus (incluye la configuración para recolectar las métricas de los módulos OH, OHSSO y Kafka).
- Grafana (incluye los dashboards de monitorización de las métricas de los módulos OH, OHSSO y Kafka).

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








