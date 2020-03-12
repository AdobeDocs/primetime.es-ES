---
description: 'null'
seo-description: 'null'
seo-title: Información general
title: Información general
uuid: 5f82f603-6e2d-4c9d-a49f-7b07f30a29e4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Información general{#overview}

La implementación de referencia incluye una opción de modo de demostración que muestra cómo implementar distintos modelos de uso para un segmento de contenido empaquetado. El modo de demostración incluye lógica empresarial para estos modelos de uso:

* **Descargar en propiedad (DTO)** : los usuarios pueden descargar el contenido en línea o sin conexión y se les concede una licencia permanente para el contenido.
* **Alquiler/Video-On-Demand (VOD)** : el contenido disponible incluye restricciones basadas en el tiempo. Por ejemplo, los usuarios pueden reproducir contenido durante un período de 30 días. Una vez que comienza la reproducción, el usuario tiene hasta 48 horas para finalizar la visualización del contenido. El contenido debe verse en 30 días.
* **Suscripción (todo lo que pueda comer)** : algunos servicios ofrecen suscripciones de pago que proporcionan a los usuarios acceso ilimitado a una gran biblioteca de contenido, siempre y cuando sigan pagando una tarifa mensual. El servidor de licencias emite una licencia única para cada segmento de contenido y también emite una licencia raíz que caduca al final del período de suscripción. Cada mes, cuando los usuarios renueven su suscripción, también se debe renovar la licencia raíz.

   >[!NOTE]
   >
   >Para los modelos de uso anteriores, después de adquirir una licencia, los usuarios deben introducir sus credenciales para que el servidor pueda comprobar que los usuarios tienen una cuenta de alquiler.

* **Financiado** por publicidad: el contenido se monetiza incluyendo la publicidad como parte de la experiencia. Con este modelo, el contenido se puede distribuir y no requiere autenticación del usuario.

En el modo de demostración del modelo de uso, la lógica empresarial del servidor controla los atributos de las licencias generadas. En el momento del empaquetado, la directiva DRM solo tiene que indicar si se requiere o no autenticación.

Para habilitar los cuatro modelos de uso, solo necesita incluir dos directivas DRM:

* Una política de DRM que permite el acceso anónimo al modelo financiado con publicidad
* Una directiva DRM que requiere autenticación de nombre de usuario/contraseña para los otros tres modelos de uso.

Cuando un usuario solicita una licencia, una aplicación cliente puede determinar si solicita al usuario la autenticación según la información de autenticación de las directivas de DRM.
