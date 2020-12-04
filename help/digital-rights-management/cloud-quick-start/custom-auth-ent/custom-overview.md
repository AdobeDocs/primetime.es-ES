---
seo-title: Autenticación personalizada/información general de asignación de derechos (opcional)
title: Autenticación personalizada/información general de asignación de derechos (opcional)
uuid: 8b5e38a5-562c-4781-ac40-4b3d6cdd97fe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# Autenticación personalizada/información general de asignación de derechos (opcional){#custom-authentication-entitlement-overview-optional}

El DRM de Primetime Cloud se puede configurar para conectarse a su propio servicio de autenticación/asignación de derechos de back-end para determinar:

* ¿Puede este usuario adquirir una licencia?
* ¿Qué derechos/restricciones deben incluirse en la licencia?

Primetime Cloud DRM incluye una implementación de referencia de un servicio de autenticación/asignación de derechos back-end. Para fines de demostración, este servidor está emitiendo respuestas &quot;allow&quot; a las solicitudes BEES. Consulte [!DNL BEESServlet.java] para modificar el comportamiento del servidor.

>[!NOTE]
>
>Anteriormente, se trataba de un producto independiente llamado *Back End Entitlement Server* (BEES), por lo que las referencias a BEES en todo este documento y en los archivos de origen.

