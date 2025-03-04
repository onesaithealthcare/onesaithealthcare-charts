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

## Operaciones pre instalación

1. Si se va a usar un docker registry distinto al de Onesait Healthcare se debe crear un Secret oh-docker-creds (si no se encuentra ya creado) con las credenciales del repositorio de imágenes docker.  Si se va a usar el repositorio de Onesait Healthcare no es necesario crearlo ya que en este caso lo creará la instalación.

2. Crear el esquema y modelo de datos sobre la BD PostgreSQL usando los scripts proporcionados.

3. Crear un usuario Kafka (si no se dispone ya del mismo) para rule_engine con los permisos necesarios para toods los topics del cluster.


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

1. Acceder a la consola de administración de OHSSO y realizar los siguientes pasos:
- Importar el client ruleengine-client.json.
- Una vez importado acceder a la configuración del mismo y revisar las redirectUris.
- Acceder a User Federation -> hn-provider, y en included clients añadir "ruleengine".

2. Lanzar la siguiente petición (sustituir host_entorno por el valor correspondiente para el entorno):
   ```sh
curl --location --request PUT 'https://<host_entorno>/restheart/cmc_alerts_alert_module' \
--header 'Content-Type: application/json' \
--data '{
    "streams" : [
      { "stages" : [
          { "_$ifvar" : [ "typeCode" , { "_$match" :{ "fullDocument.type.code" : { "$var" : "typeCode" } } } ] },
          { "_$ifvar" : [ "categoryCode" , { "_$match" :{ "fullDocument.category.code" : { "$var" :"categoryCode" } } } ] },
          { "_$ifvar" : [ "entityType" , { "_$match" :{ "fullDocument.entity.type.code" : { "$var" : "entityType" } } } ] },
          { "_$ifvar" : [ "entityId" , { "_$match" :{ "fullDocument.entityId" : { "$var" : "entityId" } } } ] },
          { "_$ifvar" : [ "value" , { "_$match" :{ "fullDocument.value" : { "$var" : "value" } } } ] },
          { "_$ifvar" : [ "text" , { "_$match" :{ "fullDocument.text" : { "$var" : "text" } } } ] },
          { "_$ifvar" : [ "priority" , { "_$match" :{ "fullDocument.priority" : { "$var" : "priority" } } } ] },
          { "_$ifvar" : [ "status" , { "_$match" :{ "fullDocument.status" : { "$var" : "status" } } } ] },
          { "_$ifvar" : [ "trend" , { "_$match" :{ "fullDocument.trendIndication" : { "$var" : "trendIndication" } } } ] },
          { "_$ifvar" : [ "count" , { "_$match" :{ "fullDocument.count" : { "$var" : "count" } } } ] },
          { "_$ifvar" : [ "eventId" , { "_$match" :{ "fullDocument.event.id" : { "$var" :"eventId" } } } ] },
          { "_$ifvar" : [ "eventTypeCode" , { "_$match" :{ "fullDocument.event.type.code" : { "$var" :"eventTypeCode" } } } ] },
          { "_$ifvar" : [ "eventCategoryCode" , { "_$match" :{ "fullDocument.event.category.code" : { "$var" :"eventCategoryCode" } } } ] },
          { "_$ifvar" : [ "ruleId" , { "_$match" :{ "fullDocument.rule.id" : { "$var" :"ruleId" } } } ] },
          { "_$ifvar" : [ "ruleName" , { "_$match" :{ "fullDocument.rule.name" : { "$var" :"ruleName" } } } ] }
        ],
        "uri" : "filter"
      },
	  {
        "stages": [
          {
            "_$match": {
              "_$or": [
                {
                  "operationType": "insert"
                },
                {
                  "operationType": "update"
                },
                {
                  "operationType": "replace"
                }
              ]
            }
          }
        ],
        "uri": "all"
      }
    ]
}'
   ```

3. Importar las propiedades de HNCONF del fichero: OHCON_OHCMC_properties.csv

4. Importar los catálogs de HNCAT: cmc-alert-type.json, cmc-alert-priority.json, cmc-alert-status.json, cmc-alert-owner.json








