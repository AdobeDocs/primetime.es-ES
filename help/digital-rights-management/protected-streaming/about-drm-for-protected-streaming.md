---
description: El servidor Adobe Primetime DRM para transmisión protegida es una implementación de servidor de licencias basada en el SDK de DRM de Primetime. Este servidor emite licencias para contenido protegido a clientes de DRM de Primetime.
title: Acerca del servidor Adobe Primetime DRM para flujo continuo protegido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# Acerca del servidor Adobe Primetime DRM para transmisión protegida{#about-adobe-primetime-drm-server-for-protected-streaming}

El servidor Adobe Primetime DRM para transmisión protegida es una implementación de servidor de licencias basada en el SDK de DRM de Primetime. Este servidor emite licencias para contenido protegido a clientes de DRM de Primetime.

El servidor Primetime DRM para transmisión protegida admite varios inquilinos. Puede alojar un solo servidor en nombre de varios editores de contenido, cada uno con sus propios ajustes de configuración. Además, el servidor admite componentes de autorización personalizados, por lo que puede ejecutar la lógica personalizada antes de expedir una licencia.

Este servidor está diseñado para utilizarse con la transmisión HTTP. Como resultado, esta implementación de servidor no admite todas las capacidades disponibles en Primetime DRM. Por ejemplo, no admite solicitudes de autenticación de usuarios, políticas múltiples, licencias enlazadas a dominios, encadenamientos de licencias o mensajes de sincronización.

>[!NOTE]
>
>Adobe Primetime DRM antes se llamaba Acceso a Adobe y antes de eso, Flash Access.

