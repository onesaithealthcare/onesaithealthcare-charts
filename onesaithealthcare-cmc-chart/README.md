# Onesait Healthcare Chart: onesaithealthcare-cmc-chart

Este Chart instala los módulos de Command Center.

## Prerrequisitos

- Se debe haber instalado y configurado previamente el chart MDM (onesaithealthcare-mdm-chart).  

- Se debe disponer del siguiente software base instalado así como sus datos de conexión:
* BD MongoDB con al menos 3 nodos configurados en modo ReplicaSet (con una BD con nombre: cmc).
* BD PostgreSQL (con usuario un us_rule_engine con permiso para el esquema del módulo)
* Cluster Kafka
  
## Módulos

- alertmodule: configuraciónes comunes
- cmc-front
- cmc-front-ruleengine
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



