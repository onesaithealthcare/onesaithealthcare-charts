# Onesait Healthcare Chart: onesaithealthcare-monitoring-chart

Este Chart instala los módulos de Onesait Healthcare Monitoring.

## Módulos

- Prometheus (incluyendo la configuración para recolectar las métricas de los módulos OH, OHSSO y Kafka).
- Grafana (incluyendo los dashboards de monitorización de las métricas de los módulos OH, OHSSO y Kafka).


## Prerrequisitos

- Se debe haber instalado y configurado previamente el chart MDM (onesaithealthcare-mdm-chart).  

- Se debe disponer de un Storage Class con provisión dinámica.

- Acceder a OHSSO, si se tiene instalado el client oh-monitoring apuntar las credenciales del mismo ya que se utilizarán en la instalación del Chart.
  Si no se tiene instalado, acceder a Client Scopes y añadir los scopes (de tipo openid-connect): openid, groups.
  Importar el client oh-monitoring con el json proporcionado.
  Revisar que las redirectUris se corresponden con las del entorno entorno (añadir las redirect uris que se vayan a asignar a prometheus y grafana).
  Acceder a User Federation y en hn-provider en la lista de Included clients añadir: oh-monitoring.

- En openshift editar el SecurityContextConstraint anyuid y en la lista de users añadirle: 
  system:serviceaccount:<namespace-donde-se-instalara_el_chart>:oh-prometheus
  system:serviceaccount:<namespace-donde-se-instalara_el_chart>:oh-grafana
  Por ejemplo:
  system:serviceaccount:oh-modules:oh-prometheus
  system:serviceaccount:oh-modules:oh-grafana

- Comprobar que la NetworkPolicy cluster-network-policy-<namespace_instalacion> contiene los puertos: 9090, 9091 y 3000.
  

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

## Operaciones pre instalación

1. Verificar el acceso a prometheus con la URL configurada y que en la sección Status -> Target se están alcanzando los endpoints de métricas de kafka, OH Modules y OHSSO.
2. Verificar el acceso a grafana y que en la sección dashboards aparecen los paneles correspondientes a los targets de prometheus y se visualizan correctamente.









