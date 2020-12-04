---
description: Para configurar el uso de Adobe® Access™, copie los archivos del DVD. Estos archivos incluyen archivos JAR que contienen código, certificados y clases de terceros. Además, solicite un certificado de Adobe Systems Incorporated. Se le expedirán varias credenciales utilizadas para proteger la integridad del contenido empaquetado, las licencias y la comunicación entre el cliente y el servidor.
seo-description: Para configurar el uso de Adobe® Access™, copie los archivos del DVD. Estos archivos incluyen archivos JAR que contienen código, certificados y clases de terceros. Además, solicite un certificado de Adobe Systems Incorporated. Se le expedirán varias credenciales utilizadas para proteger la integridad del contenido empaquetado, las licencias y la comunicación entre el cliente y el servidor.
seo-title: Configuración del entorno de desarrollo
title: Configuración del entorno de desarrollo
uuid: 1f192783-9c9a-4342-909a-4881248a85ad
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Configuración del SDK {#setting-up-the-sdk}

Para configurar el uso de Adobe® Access™, copie los archivos del DVD. Estos archivos incluyen archivos JAR que contienen código, certificados y clases de terceros. Además, solicite un certificado de Adobe Systems Incorporated. Se le expedirán varias credenciales utilizadas para proteger la integridad del contenido empaquetado, las licencias y la comunicación entre el cliente y el servidor.

El SDK de Adobe Access está disponible en dos tipos:
* SDK de Adobe Access Core
* SDK de Adobe Access Professional

La siguiente tabla muestra una comparación básica de los SDK de Adobe Access:

| Función | SDK de Adobe Access Core | SDK de Adobe Access Professional |
|---|---|---|
| Funciones de Flash Access 2.0 | Disponible | Disponible |
| Rotación de clave | - | Disponible |
| Compatibilidad con dominios | Disponible | Disponible |
| Encadenamiento de licencias mejorado | Disponible | Disponible |
| Mensajes de sincronización | Disponible | Disponible |
| Licencia de pregeneración | Disponible | Disponible |
| Licencias incrustadas | Disponible | Disponible |

## Configuración del entorno de desarrollo {#setting-up-the-development-environment}

Desde el DVD, copie los siguientes archivos SDK para utilizarlos en el entorno de desarrollo y en la ruta de clases de Java:

* adobe-flashaccess-certs.jar (contiene certificados raíz de Adobe)
* adobe-flashaccess-sdk.jar (contiene clases de SDK de Adobe Access Core)
* adobe-flashaccess-sdk-pro.jar (contiene clases de SDK de Adobe Access Professional, solo necesarias para funciones Professional)

Los siguientes archivos JAR de terceros también se encuentran en el DVD, en la carpeta de terceros del SDK:

* bcmail-jdk15-141.jar
* bcprov-jdk15-141.jar
* commons-discover-0.4.jar
* commons-logging-1.1.1.jar
* cryptoj.jar
* jaxb-api.jar
* jaxb-impl.jar
* jaxb-libs.jar
* relaxngDatatype.jar
* rm-pdrl.jar
* xsdlib.jar

Para mejorar el rendimiento, si lo desea, puede activar la compatibilidad nativa con operaciones criptográficas mediante la implementación de las bibliotecas específicas de la plataforma situadas en la carpeta &quot;thirdparty/cryptoj&quot; del SDK. Para habilitar la compatibilidad nativa, agregue la biblioteca para su plataforma (jsafe.dll para Windows o libjsafe.so para Linux) a la ruta. Se proporcionan las versiones de 32 y 64 bits de estas bibliotecas. (Tenga en cuenta que la versión de 64 bits solo debe utilizarse si tiene un SO de 64 bits y está ejecutando la versión de 64 bits de Java).

Además, una parte opcional del SDK es adobe-flashaccess-lcrm.jar. Este archivo solo es necesario para la funcionalidad relacionada con la compatibilidad con Adobe Flash Media Rights Management Server (FMRMS) 1.x. Si ya ha implementado FMRMS 1.x y no desea volver a empaquetar el contenido protegido por FMRMS, debe agregar soporte al servidor de licencias para que pueda gestionar el contenido y los clientes antiguos.
