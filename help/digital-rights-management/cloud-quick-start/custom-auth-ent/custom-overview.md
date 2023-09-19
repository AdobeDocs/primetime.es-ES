---
title: Autenticación personalizada/información general de asignación de derechos (opcional)
description: Autenticación personalizada/información general de asignación de derechos (opcional)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Autenticación personalizada/información general de asignación de derechos (opcional){#custom-authentication-entitlement-overview-optional}

Primetime Cloud DRM se puede configurar para que se ponga en contacto con su propio servicio de autenticación/derecho back-end y determine:

* ¿Este usuario puede adquirir una licencia?
* ¿Qué derechos/restricciones deben incluirse en la licencia?

Primetime Cloud DRM incluye una implementación de referencia de un servicio de autenticación/asignación de derechos del back-end. Para fines de demostración, este servidor emite respuestas de &quot;permiso&quot; a solicitudes de BEES. Consulte [!DNL BEESServlet.java] para modificar el comportamiento del servidor.

>[!NOTE]
>
>Anteriormente, este era un producto independiente denominado *Servidor de derechos back-end* (BEES), por lo tanto las referencias a BEES a lo largo de este documento y en los archivos fuente.
