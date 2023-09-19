---
title: Información general
description: Información general
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Información general{#overview}

La Implementación de referencia incluye una opción de modo de demostración que muestra cómo implementar diferentes modelos de uso para un segmento de contenido empaquetado. El modo de demostración incluye lógica empresarial para estos modelos de uso:

* **Descarga por cuenta propia (DTO)** - Los usuarios pueden descargar el contenido en línea o sin conexión, y se les emite una licencia permanente para el contenido.
* **Alquiler/vídeo bajo demanda (VOD)** : el contenido disponible viene con restricciones basadas en el tiempo. Por ejemplo, los usuarios pueden reproducir contenido durante un periodo de 30 días. Una vez que comienza la reproducción, el usuario tiene hasta 48 horas para terminar de ver el contenido. El contenido debe verse en 30 días.
* **Suscripción (todo lo que puedas comer)** - Algunos servicios ofrecen suscripciones de pago que dan a los usuarios acceso ilimitado a una gran biblioteca de contenido siempre y cuando sigan pagando una tarifa mensual. El servidor de licencias emite una licencia única para cada segmento de contenido y también una licencia raíz que caduca al final del período de suscripción. Cada mes, cuando los usuarios renuevan su suscripción, también se debe renovar la licencia raíz.

  >[!NOTE]
  >
  >Para los modelos de uso anteriores, después de adquirir una licencia, los usuarios deben introducir sus credenciales para que el servidor pueda comprobar que los usuarios tienen una cuenta de alquiler.

* **Financiado por publicidad** - El contenido se monetiza incluyendo publicidad como parte de la experiencia. Con este modelo, el contenido se puede distribuir y no requiere autenticación del usuario.

En el modo de demostración del modelo de uso, la lógica empresarial del servidor controla los atributos de las licencias generadas. En el momento del empaquetado, la política de DRM solo debe indicar si se requiere o no autenticación.

Para activar los cuatro modelos de uso, solo es necesario incluir dos políticas de DRM:

* Una política de DRM que permite el acceso anónimo para el modelo financiado con publicidad
* Una directiva DRM que requiere autenticación de nombre de usuario y contraseña para los otros tres modelos de uso.

Cuando un usuario solicita una licencia, una aplicación cliente puede determinar si se debe solicitar al usuario la autenticación en función de la información de autenticación contenida en las directivas de DRM.
