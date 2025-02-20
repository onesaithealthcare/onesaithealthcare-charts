# Helm Charts para Onesait Healthcare

Este repositorio contiene una colección de charts de Helm para desplegar Onesait Healthcare en Kubernetes.

## Contenido

- [Onesait Healthcare MDM](onesaithealthcare-mdm-chart/): Módulos core de Onesait Healthcare.
- [Onesait Healthcare Data](onesaithealthcare-data-chart/): Global Repository y visores.
- [Onesait Healthcare BPM](onesaithealthcare-bpm-chart/): Módulos relacionados con la gestión de procesos.
- [Onesait Healthcare Integration Engine](onesaithealthcare-iengine-chart/): Motor de integración.
- [Onesait Healthcare Analytics](onesaithealthcare-analytics-chart/): Módulos analíticos.


## Requisitos

- Helm 3.x
- Kubernetes 1.x
- Acceso a un clúster Kubernetes

## Instalación

1. Agregar el repositorio Helm:
   ```sh
   helm repo add onesaithealthcare https://github.com/onesaithealthcare/onesaithealthcare-charts
   helm repo update
   ```

2. Instalar un chart específico:
   ```sh
   helm install mi-release onesaithealthcare/chart-1--namespace mi-namespace
   ```

## Uso

Para listar los releases desplegados:
```sh
helm list -n mi-namespace
```

Para actualizar un chart:
```sh
helm upgrade mi-release onesaithealthcare/chart-1 --namespace mi-namespace
```

Para desinstalar un release:
```sh
helm uninstall mi-release --namespace mi-namespace
```


## Desarrollo

Es necesario tener instalado el cliente helm en la máquina local desde la que se esté trabajando.

Para añadir un chart se creará una nueva carpeta sobre el directorio raíz y en ella se añadirán los ficheros necesarios.

Para empaquetar un chart (nuevo o modificado) desde el directorio raíz se ejecuta el comando:
```sh
helm package <nombre_de_directorio>
```

Una vez se ha (re)generado el correspondiente .tgz se ejecuta el siguiente comando para actualizar el index:
```sh
helm repo index .
```

Finalmente se hará commit y push al repositorio de los cambios realizados.


