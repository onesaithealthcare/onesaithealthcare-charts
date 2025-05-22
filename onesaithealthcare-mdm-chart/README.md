# Onesait Healthcare Chart: onesaithealthcare-mdm-chart

Este Chart instala los módulos core de la solución.

## Prerrequisitos

- Antes de instalar el chart se deben cumplir los prerrequisitos especificados en la guía de instalación de MDM.

- Se deberá tener disponible la siguiente información: 
	- tipo de base de datos, ip o host y puerto
	- usarios y passwords de los esquemas de base de datos de los módulos
	- protocolo y dominio en el que se expondrán los módulos
  
## Módulos

- ohcommons: configuraciones comunes
- OHSSO (v4.10.0)
- OHCON (v4.7.0)
- OHAUT (v4.8.0)
- OHONT (v4.6.0)
- OHMPI (v4.10.0)
- OHATN (v4.3.0)
- OHDSK (v3.23.0)

## WebComponent genéricos

- OHWCFORM (v4.9.0)
- OHWCVIEWER (4.6.0)

## Instalación

Consultar la guía general de prerrequisitos donde se indican varias alternativas para registrar el repositorio helm e instalar el chart.
El repositorio se encuentra en:
https://nexus.devops.onesait.com/repository/onesait-healthcare-helm-charts
Se deberá disponer de credenciales para poder acceder al mismo, dichas credenciales serán proporcionadas por el equipo de Onesait Healthcare.
   

## Operaciones post instalación

Tras instanciar el chart, una vez todos los pods se encuentran en estado Running se deberán ejecutar las tareas post instalación indicadas en la guía de MDM.


