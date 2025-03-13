# Onesait Healthcare Chart: onesaithealthcare-cmc-chart

Este Chart instala los módulos de Command Center.

## Prerrequisitos

- Se debe haber instalado y configurado previamente el chart MDM (onesaithealthcare-mdm-chart), la instalación de CMC
  debe realizarse en el mismo namespace donde se encuentre desplegado MDM.

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

## Operaciones pre instalación

1. Crear un Secret oh-docker-creds (si no se encuentra ya creado) con las credenciales del repositorio de imágenes docker.

2. Crear el esquema y modelo de datos sobre la BD PostgreSQL usando los scripts proporcionados (ejecutar el lanzador .sh desde una máquina con el cliente psql).

3. Crear un usuario Kafka (si no se dispone ya del mismo) para rule_engine con los permisos necesarios para toods los topics del cluster.

4. Crear la BD mongo:
   - conectar a mongo
   - use <nombre_db_mongo>
   - db.test.insertOne({"test":"test"})
   
5. Acceder a la consola de administración de OHSSO y realizar los siguientes pasos:
- Importar el client ruleengine-client.json.
- Una vez importado acceder a la configuración del mismo y revisar las redirectUris.
- Acceder a User Federation -> hn-provider, y en included clients añadir "ruleengine".

6. Importar las propiedades de HNCONF del fichero: OHCON_OHCMC_properties.csv

7. Importar los catálogs de HNCAT: cmc-alert-type.json, cmc-alert-priority.json, cmc-alert-status.json, cmc-alert-owner.json




## Instalación

1. Agregar el repositorio Helm (si no se tenía ya agregado):
   ```sh
   helm repo add onesaithealthcare https://github.com/onesaithealthcare/onesaithealthcare-charts
   helm repo update
   ```

2. Instalar el chart con el siguiente comando (o usando los formularios si la plataforma kubernetes usada tiene dicha posibilidad):
   ```sh
   helm install mi-release onesaithealthcare/onesaithealthcare-cmc-chart --namespace oh-modules
   ```

## Operaciones post instalación

1. Lanzar la siguiente petición (sustituir host_entorno por el valor correspondiente para el entorno):
   ```sh
curl --location --request PUT 'https://<host_entorno>/restheart/cmc_alerts_alert_module' \
--header 'Content-Type: application/json' \
--data '{
      "streams": [
        {
          "stages": [
            { "_$ifvar": [ "typeCode", { "_$match": { "fullDocument.type.code": { "$var": "typeCode" } } } ] },
            { "_$ifvar": [ "categoryCode", { "_$match": { "fullDocument.category.code": { "$var": "categoryCode" } } } ] },
            { "_$ifvar": [ "entityId", { "_$match": { "fullDocument.entityReference._id": { "$var": "entityId" } } } ] },
            {
              "_$ifvar": [
                "priorityCode",
                { "_$match": { "fullDocument.priority.code": { "$in": { "$var": "priorityCode" } } } }
              ]
            },
            {
              "_$ifvar": [
                "priorityDisplay",
                { "_$match": { "fullDocument.priority.display": { "$in": { "$var": "priorityDisplay" } } } }
              ]
            },
            { "_$ifvar": [ "text", { "_$match": { "fullDocument.text": { "$var": "text" } } } ] },
            { "_$ifvar": [ "trend", { "_$match": { "fullDocument.trendIndication": { "$var": "trend" } } } ] },
            {
              "_$ifvar": [
                "status",
                { "_$match": { "fullDocument.status": { "$in": { "$var": "status" } } } }
              ]
            },
            {
              "_$ifvar": [
                "startDate",
                { "_$match": { "fullDocument.created": { "$gte": { "$var": "startDate" } } } }
              ]
            },
            {
              "_$ifvar": [
                "endDate",
                { "_$match": { "fullDocument.created": { "$lte": { "$var": "endDate" } } } }
              ]
            }
          ],
          "uri": "filter"
        },
        {
          "stages": [
            {
              "_$match": {
                "_$or": [
                  { "operationType": "insert" },
                  { "operationType": "update" },
                  { "operationType": "replace" }
                ]
              }
            }
          ],
          "uri": "all"
        }
      ]
    }'
   ```

2. Una vez hayan arrancado correctamente todos los Pods, verificar la instalación accediendo a la url:
https://<dominio_entorno>/ohcmc







