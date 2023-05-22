---
description: Para configurar el Adobe ® Access™ para su uso, copie los archivos del DVD. Estos archivos incluyen archivos JAR que contienen código, certificados y clases de terceros. Además, solicite un certificado a Adobe Systems Incorporated. Se le emitirán varias credenciales utilizadas para proteger la integridad del contenido empaquetado, las licencias y la comunicación entre el cliente y el servidor.
title: Configuración del entorno de desarrollo
exl-id: 66310fc8-7513-4aab-81d6-1370ce216cbf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Configuración del SDK {#setting-up-the-sdk}

Para configurar el Adobe ® Access™ para su uso, copie los archivos del DVD. Estos archivos incluyen archivos JAR que contienen código, certificados y clases de terceros. Además, solicite un certificado a Adobe Systems Incorporated. Se le emitirán varias credenciales utilizadas para proteger la integridad del contenido empaquetado, las licencias y la comunicación entre el cliente y el servidor.

El SDK de acceso a Adobe está disponible en dos tipos:
* SDK de Adobe Access Core
* SDK de Adobe Access Professional

En la tabla siguiente se muestra una comparación básica de los SDK de acceso a Adobe:

| Función | SDK de Adobe Access Core | SDK de Adobe Access Professional |
|---|---|---|
| Funciones de Flash Access 2.0 | Disponible | Disponible |
| Rotación de clave | - | Disponible |
| Compatibilidad con dominios | Disponible | Disponible |
| Encadenamiento de licencias mejorado | Disponible | Disponible |
| Mensajes de sincronización | Disponible | Disponible |
| Generación previa de licencias | Disponible | Disponible |
| Licencias incrustadas | Disponible | Disponible |

## Configuración del entorno de desarrollo {#setting-up-the-development-environment}

Desde el DVD, copie los siguientes archivos SDK para utilizarlos en su entorno de desarrollo y en su ruta de clase Java:

* adobe-flashaccess-certs.jar (contiene certificados raíz de Adobe)
* adobe-flashaccess-sdk.jar (contiene clases de SDK de Adobe Access Core)
* adobe-flashaccess-sdk-pro.jar (contiene clases de SDK de Adobe Access Professional, necesarias solo para las funciones profesionales)

Necesita los siguientes archivos JAR de terceros también ubicados en el DVD en la carpeta &quot;third party&quot; del SDK:

* bcmail-jdk15-141.jar
* bcprov-jdk15-141.jar
* commons-discovery-0.4.jar
* commons-logging-1.1.1.jar
* cryptoj.jar
* jaxb-api.jar
* jaxb-impl.jar
* jaxb-libs.jar
* relaxngDatatype.jar
* rm-pdrl.jar
* xsdlib.jar

Para mejorar el rendimiento, puede habilitar opcionalmente la compatibilidad nativa con operaciones criptográficas implementando las bibliotecas específicas de la plataforma ubicadas en la carpeta &quot;third party/cryptoj&quot; del SDK. Para habilitar la compatibilidad nativa, agregue la biblioteca de su plataforma (jsafe.dll para Windows o libjsafe.so para Linux) a la ruta. Se proporcionan las versiones de 32 y 64 bits de estas bibliotecas. (Tenga en cuenta que la versión de 64 bits solo debe usarse si tiene un sistema operativo de 64 bits y ejecuta la versión de 64 bits de Java).

Además, una parte opcional del SDK es adobe-flashaccess-lcrm.jar. Este archivo solo es necesario para la funcionalidad relacionada con la compatibilidad con Adobe Flash Media Rights Management Server (FMRMS) 1.x. Si ha implementado anteriormente FMRMS 1.x y no desea volver a empaquetar el contenido protegido por FMRMS, debe agregar compatibilidad con el servidor de licencias para que pueda gestionar el contenido y los clientes antiguos.
