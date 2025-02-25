# Onesait Healthcare Chart: onesaithealthcare-cmc-chart

Este Chart instala los módulos de Command Center.

## Prerrequisitos

- Se debe haber instalado y configurado previamente el chart MDM (onesaithealthcare-mdm-chart).  

- Se debe disponer del los siguientes recursos instalados así como sus datos de conexión:
* BD MongoDB con al menos 3 nodos configurados en modo ReplicaSet.
* BD PostgreSQL.
* Cluster Kafka.
  
## Módulos

- alertmodule
- cmc-front
- cmc-front-ruleengine
- api rest mongobd
- rule_engine

## Instalación

1. Agregar el repositorio Helm (si no se tenía ya agregado):
   ```sh
   helm repo add onesaithealthcare https://github.com/onesaithealthcare/onesaithealthcare-charts
   helm repo update
   ```

2. Instalar el chart:
   ```sh
   helm install mi-release onesaithealthcare/onesaithealthcare-cmc-chart --namespace oh-modules
   ```

## Operaciones post instalación

1. Acceder a la consola de administración de OHSSO y realizar los siguientes pasos:
- Importar el client ruleengine.
- Una vez importado acceder a la configuración del mismo y revisar las redirectUris.
- Acceder a User Federation -> hn-provider, y en included clients añadir "ruleengine".

2. ¿Propiedades HNCONF?

3. ¿Catálogos HNCAT?

4. ¿Permisos HNAUT?






