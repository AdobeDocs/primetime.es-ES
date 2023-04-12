---
title: Notas de la versión de la autenticación de Adobe Primetime 2.6.3
description: Notas de la versión de la autenticación de Adobe Primetime 2.6.3
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Notas de la versión Adobe Primetime Authentication 2.63 {#pt-authn-263-rn}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

Esta página describe nuevas funciones, cambios y problemas conocidos con esta versión:

## Clientes web y del lado del servidor {#server-side-web-clients-263}

* [Número de compilación](#build-number)
* [Nuevas funciones](#new-features)

### Número de compilación {#build-number-263}

Autenticación de Adobe Primetime: adobe-pass-**2,63**
Fecha de versión: **20/9/2022 - 22/09/2022**

### Nuevas funciones {#new-features-263}

#### Mejorar el mecanismo de identificación de la plataforma {#pf-identification-mech}

* A partir de esta versión, hemos mejorado el mecanismo utilizado para identificar un dispositivo y ya no dependeremos de la implementación del lado del cliente. Esto proporcionará una granularidad más precisa al aplicar reglas comerciales a nivel de plataforma y una mejor comprensión de los valores de tráfico en los informes de ESM.

* Próximamente se publicará una nueva versión de ESM, con informes nuevos y mejorados que expondrán los campos relacionados con la plataforma.

* Para obtener más información sobre los cambios planificados, póngase en contacto con su TAM.

#### Autodegradación de MVPD {#mvpd-self-degradation}

Esta función proporciona a los MVPD la capacidad de evitar temporalmente sus propios extremos de autenticación y autorización para escenarios de alto tráfico cuando la carga en esos puntos finales respectivos se vuelve demasiado alta.


#### Añadir ID proxy en el encabezado de las llamadas de autorización {#add-proxied-id}

Esta función añade el id de un MVPD proxy Synacor en el encabezado de la llamada de autorización. Esto permite a Synacor configurar reglas comerciales para cada proxy individual (por ejemplo, enrutamiento a diferentes dominios por MVPD proxy).


#### TVE {#tve-dashboard}

En esta versión hemos solucionado un problema en el que authN o authZ TTL establecidos a nivel de MVPD no se calculaban correctamente en los informes de configuración.


#### SDK de JavaScript 4.6.0 {#js-sdk}

* Se ha eliminado el uso de `eval` , lo que hace que el SDK sea compatible con la Política de seguridad de contenido.
* Se ha corregido un problema que impedía que el flujo de autenticación finalizara correctamente cuando una aplicación de socio borraba explícitamente el almacenamiento local del explorador.



