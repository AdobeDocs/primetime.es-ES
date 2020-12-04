---
description: El servidor DRM de Adobe Primetime para flujo protegido es una implementación de servidor de licencias basada en el SDK de DRM de Primetime. Este servidor emite licencias para contenido protegido a clientes de DRM de Primetime.
seo-description: El servidor DRM de Adobe Primetime para flujo protegido es una implementación de servidor de licencias basada en el SDK de DRM de Primetime. Este servidor emite licencias para contenido protegido a clientes de DRM de Primetime.
seo-title: Acerca del servidor DRM de Adobe Primetime para flujo protegido
title: Acerca del servidor DRM de Adobe Primetime para flujo protegido
uuid: 775bef19-6071-428f-80f5-57cae472753c
translation-type: tm+mt
source-git-commit: 68f1318db89cf9422f5969f669c11f3784560db6
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# Acerca del servidor DRM de Adobe Primetime para flujo protegido{#about-adobe-primetime-drm-server-for-protected-streaming}

El servidor DRM de Adobe Primetime para flujo protegido es una implementación de servidor de licencias basada en el SDK de DRM de Primetime. Este servidor emite licencias para contenido protegido a clientes de DRM de Primetime.

El servidor Primetime DRM para flujo protegido admite varios inquilinos. Puede alojar un solo servidor en nombre de varios editores de contenido, cada uno con sus propios ajustes de configuración. Además, el servidor admite componentes de autorización personalizados, por lo que puede ejecutar la lógica personalizada antes de que se emita una licencia.

Este servidor está diseñado para utilizarse con flujo HTTP. Como resultado, esta implementación de servidor no admite todas las capacidades disponibles en Primetime DRM. Por ejemplo, no admite solicitudes de autenticación de usuarios, varias políticas, licencias enlazadas a dominios, encadenamiento de licencias o mensajes de sincronización.

>[!NOTE]
>
>Adobe Primetime DRM se llamaba anteriormente Adobe Access y antes de eso, Flash Access.

