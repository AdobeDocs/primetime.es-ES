---
title: Actualizar la base de datos de implementación de referencia
description: Actualizar la base de datos de implementación de referencia
copied-description: true
exl-id: b337bf9c-7add-47b8-9576-db7fa067c51d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Actualizar la base de datos de implementación de referencia{#update-the-reference-implementation-db}

Para controlar los modelos de uso en los que se emite una licencia a un usuario designado, añada entradas a la base de datos de implementación de referencia.

1. Agregar entradas a `Customer` tabla.

   El `Customer` La tabla incluye los nombres de usuario y contraseñas para autenticar a los usuarios. También indica si un usuario tiene una suscripción (una licencia emitida bajo el *Suscripción* modelo de uso).

1. Conceder acceso al usuario en los modelos de uso de Descargar para uso propio o Vídeo bajo demanda.

       Agregue entradas a la tabla CustomerAuthorization para especificar:
   
   * El modelo de uso
   * Cada segmento de contenido al que puede acceder un usuario

Para obtener más información sobre cómo rellenar cada tabla, consulte la [!DNL PopulateSampleDB.sql] (incluido en el DVD de DRM de Primetime en el [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] directorio).
