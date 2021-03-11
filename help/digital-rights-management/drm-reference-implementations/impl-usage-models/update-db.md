---
title: Actualizar la base de datos de implementación de referencia
description: Actualizar la base de datos de implementación de referencia
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Actualizar la implementación de referencia DB{#update-the-reference-implementation-db}

Para controlar los modelos de uso en los que se emite una licencia a un usuario designado, agregue entradas a la base de datos de implementación de referencia.

1. Agregue entradas a la tabla `Customer`.

   La tabla `Customer` incluye nombres de usuario y contraseñas para autenticar usuarios. También indica si un usuario tiene una suscripción (una licencia emitida bajo el modelo de uso *Subscription* ).

1. Conceda acceso a un usuario en los modelos de uso Descargar para ser propietario o Vídeo bajo demanda .

       Agregue entradas a la tabla &quot;CustomerAuthorization&quot; para especificar:
   
   * El modelo de uso
   * Cada segmento de contenido al que puede acceder un usuario

Para obtener más información sobre cómo rellenar cada tabla, consulte el script [!DNL PopulateSampleDB.sql] (incluido en el DVD de Primetime DRM en el directorio [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/]).
