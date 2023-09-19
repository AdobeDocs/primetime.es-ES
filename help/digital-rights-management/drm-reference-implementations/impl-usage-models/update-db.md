---
title: Actualizar la base de datos de implementación de referencia
description: Actualizar la base de datos de implementación de referencia
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
