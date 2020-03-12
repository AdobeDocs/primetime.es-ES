---
seo-title: Actualizar la base de datos de implementación de referencia
title: Actualizar la base de datos de implementación de referencia
uuid: 2883045e-ad62-466d-94a2-fc45ded2a4f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Actualizar la base de datos de implementación de referencia{#update-the-reference-implementation-db}

Para controlar los modelos de uso en los que se emite una licencia a un usuario designado, agregue entradas a la base de datos de implementación de referencia.

1. Agregue entradas a la `Customer` tabla.

   La `Customer` tabla incluye nombres de usuario y contraseñas para autenticar usuarios. También indica si un usuario tiene una suscripción (una licencia emitida según el modelo de uso de *suscripción* ).

1. Otorgue acceso al usuario en los modelos de uso Descargar para poseer o Vídeo bajo demanda.

       Agregue entradas a la tabla &quot;CustomerAuthorization&quot; para especificar:
   
   * El modelo de uso
   * Cada segmento de contenido al que un usuario puede acceder

Para obtener más información sobre cómo rellenar cada tabla, consulte la [!DNL PopulateSampleDB.sql] secuencia de comandos (incluida en el DVD de Primetime DRM en el [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] directorio).
