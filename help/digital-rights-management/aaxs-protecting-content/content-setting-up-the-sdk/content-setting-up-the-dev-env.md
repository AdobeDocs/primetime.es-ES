---
description: Para configurar el Adobe® Access™ para su uso, copie los archivos del DVD. Estos archivos incluyen archivos JAR que contienen código, certificados y clases de terceros. Además, solicite un certificado de Adobe Systems Incorporated. Se le otorgarán varias credenciales utilizadas para proteger la integridad del contenido empaquetado, las licencias y la comunicación entre el cliente y el servidor.
title: Configuración del entorno de desarrollo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# Configuración del SDK {#setting-up-the-sdk}

Para configurar el Adobe® Access™ para su uso, copie los archivos del DVD. Estos archivos incluyen archivos JAR que contienen código, certificados y clases de terceros. Además, solicite un certificado de Adobe Systems Incorporated. Se le otorgarán varias credenciales utilizadas para proteger la integridad del contenido empaquetado, las licencias y la comunicación entre el cliente y el servidor.

El SDK de acceso a Adobe está disponible en dos tipos:
* SDK de Adobe Access Core
* SDK de Adobe Access Professional

La siguiente tabla muestra una comparación básica de los SDK de acceso a Adobe:

| Función | SDK de Adobe Access Core | SDK de Adobe Access Professional |
|---|---|---|
| Funciones de Flash Access 2.0 | Disponible | Disponible |
| Rotación de clave | - | Disponible |
| Compatibilidad con dominios | Disponible | Disponible |
| Encadenado de licencias mejorado | Disponible | Disponible |
| Mensajes de sincronización | Disponible | Disponible |
| Pregeneración de licencias | Disponible | Disponible |
| Licencias incrustadas | Disponible | Disponible |

## Configuración del entorno de desarrollo {#setting-up-the-development-environment}

Desde el DVD, copie los siguientes archivos SDK para utilizarlos en su entorno de desarrollo y en la ruta de clase Java:

* adobe-flashaccess-certs.jar (contiene certificados raíz de Adobe)
* adobe-flashaccess-sdk.jar (contiene clases de SDK de Adobe Access Core)
* adobe-flashaccess-sdk-pro.jar (contiene clases de SDK de Adobe Access Professional, solo necesarias para funciones profesionales)

Necesita los siguientes archivos JAR de terceros también ubicados en el DVD de la carpeta &quot;de terceros&quot; del SDK:

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

Para mejorar el rendimiento, opcionalmente, puede habilitar la compatibilidad nativa con las operaciones criptográficas mediante la implementación de las bibliotecas específicas de la plataforma ubicadas en la carpeta &quot;thirdparty/cryptoj&quot; del SDK. Para habilitar el soporte nativo, agregue la biblioteca para su plataforma (jsafe.dll para Windows o libjsafe.so para Linux) a la ruta. Se proporcionan las versiones de 32 y 64 bits de estas bibliotecas. (Tenga en cuenta que la versión de 64 bits solo debe usarse si tiene un sistema operativo de 64 bits y ejecuta la versión de 64 bits de Java).

Además, una parte opcional del SDK es adobe-flashaccess-lcrm.jar. Este archivo solo es necesario para funciones relacionadas con la compatibilidad con el Servidor Media Rights Management de Flash de Adobe (FMRMS) 1.x. Si ha implementado anteriormente FMRMS 1.x y no desea volver a empaquetar el contenido protegido por FMRMS, debe añadir compatibilidad al servidor de licencias para que pueda gestionar el contenido antiguo y los clientes.
