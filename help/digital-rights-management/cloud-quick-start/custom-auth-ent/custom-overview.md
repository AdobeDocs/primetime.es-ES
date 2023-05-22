---
title: Autenticación personalizada/información general de asignación de derechos (opcional)
description: Autenticación personalizada/información general de asignación de derechos (opcional)
copied-description: true
exl-id: d92c4246-c772-44da-80b6-4086dfc30ff4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
