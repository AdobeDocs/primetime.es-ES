---
title: Resumen de autenticación/asignación de derechos personalizado (opcional)
description: Resumen de autenticación/asignación de derechos personalizado (opcional)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# Resumen de autenticación/asignación de derechos personalizado (opcional){#custom-authentication-entitlement-overview-optional}

El DRM de Primetime Cloud se puede configurar para que llegue a su propio servicio de autenticación/derechos back-end para determinar:

* ¿Puede este usuario adquirir una licencia?
* ¿Qué derechos/restricciones deben incluirse en la licencia?

Primetime Cloud DRM incluye una implementación de referencia de un servicio de autenticación/asignación de derechos de back-end. Para fines de demostración, este servidor está emitiendo respuestas &quot;permitidas&quot; a las solicitudes BEES. Consulte [!DNL BEESServlet.java] para modificar el comportamiento del servidor.

>[!NOTE]
>
>Anteriormente, este era un producto separado llamado *Back End Entitlement Server* (BEES), por lo que las referencias a BEES en este documento y en los archivos de origen.

