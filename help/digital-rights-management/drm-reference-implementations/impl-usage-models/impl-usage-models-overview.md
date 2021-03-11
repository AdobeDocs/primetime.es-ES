---
title: Información general
description: Información general
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---


# Información general{#overview}

La implementación de referencia incluye una opción de modo de demostración que muestra cómo implementar diferentes modelos de uso para un segmento de contenido empaquetado. El modo de demostración incluye lógica empresarial para estos modelos de uso:

* **Descargar para su propiedad (DTO)** : Los usuarios pueden descargar el contenido en línea o sin conexión y se les otorga una licencia permanente para el contenido.
* **Alquiler/Vídeo bajo demanda (VOD)** : el contenido disponible viene con restricciones basadas en el tiempo. Por ejemplo, los usuarios pueden reproducir contenido durante un período de 30 días. Una vez que comienza la reproducción, el usuario tiene hasta 48 horas para finalizar la visualización del contenido. El contenido debe visualizarse en 30 días.
* **Suscripción (todo lo que se puede comer)** : algunos servicios ofrecen suscripciones de pago que proporcionan a los usuarios acceso ilimitado a una gran biblioteca de contenido siempre y cuando sigan pagando una tarifa mensual. El servidor de licencias emite una licencia única para cada segmento de contenido y también emite una licencia raíz que caduca al final del periodo de suscripción. Cada mes, cuando los usuarios renuevan su suscripción, también se debe renovar la licencia raíz.

   >[!NOTE]
   >
   >Para los modelos de uso anteriores, después de adquirir una licencia, los usuarios deben introducir sus credenciales para que el servidor pueda verificar que los usuarios tengan una cuenta de alquiler.

* **Con financiación de publicidad** : el contenido se monetiza al incluir la publicidad como parte de la experiencia. Con este modelo, el contenido se puede distribuir y no requiere autenticación del usuario.

En el modo de demostración del modelo de uso, la lógica empresarial del servidor controla los atributos de las licencias generadas. En el momento del empaquetado, la directiva DRM solo tiene que indicar si se requiere o no autenticación.

Para habilitar los cuatro modelos de uso, solo necesita incluir dos directivas DRM:

* Una política de DRM que permite el acceso anónimo al modelo financiado por AdHoc
* Una directiva DRM que requiere autenticación de nombre de usuario/contraseña para los otros tres modelos de uso.

Cuando un usuario solicita una licencia, una aplicación cliente puede determinar si desea solicitar al usuario la autenticación en función de la información de autenticación de las políticas de DRM.
