---
description: Adobe Primetime DRM Server for Protected Streaming es una implementación de servidor de licencias basada en el SDK de DRM de Primetime. Este servidor emite licencias para contenido protegido a clientes de DRM de Primetime.
title: Acerca del servidor DRM de Adobe Primetime para flujo protegido
exl-id: 911acd61-8b27-4ac7-a420-2faeb46e8087
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Acerca del servidor DRM de Adobe Primetime para flujo protegido{#about-adobe-primetime-drm-server-for-protected-streaming}

Adobe Primetime DRM Server for Protected Streaming es una implementación de servidor de licencias basada en el SDK de DRM de Primetime. Este servidor emite licencias para contenido protegido a clientes de DRM de Primetime.

El servidor DRM de Primetime para flujo protegido admite varios inquilinos. Puede alojar un único servidor en nombre de varios editores de contenido, cada uno con su propia configuración. Además, el servidor admite componentes de autorización personalizados, por lo que puede ejecutar la lógica personalizada antes de emitir una licencia.

Este servidor está diseñado para utilizarse con flujo HTTP. Como resultado, esta implementación del servidor no admite todas las funciones disponibles en Primetime DRM. Por ejemplo, no admite solicitudes de autenticación de usuarios, varias directivas, licencias enlazadas a dominios, encadenamiento de licencias o mensajes de sincronización.

>[!NOTE]
>
>Adobe Primetime DRM se llamaba anteriormente Acceso de Adobe y, antes de eso, Flash Access.
