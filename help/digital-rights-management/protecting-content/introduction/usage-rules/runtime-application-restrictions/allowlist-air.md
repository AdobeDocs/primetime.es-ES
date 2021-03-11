---
title: Lista de permitidos para aplicaciones DRM de Primetime permitidas para reproducir contenido protegido
description: Lista de permitidos para aplicaciones DRM de Primetime permitidas para reproducir contenido protegido
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Lista de permitidos para aplicaciones DRM de Primetime permitidas para reproducir contenido protegido {#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

Una lista de permitidos especifica las aplicaciones de AIR, iOS y Android a las que se permite reproducir contenido. También especifica los ID de aplicación de AIR e iOS, la versión mínima, la versión máxima y el ID de editor.

Ejemplo de caso de uso: Utilice esta regla para limitar la reproducción a una aplicación concreta o para controlar la versión de la aplicación que puede acceder al contenido.

>[!NOTE]
>
>Si utiliza el Flash Builder de Adobe para crear aplicaciones protegidas, debe asegurarse de no implementar la aplicación en modo de depuración. Al implementar una aplicación en modo de depuración, el Flash Builder añade `.debug` al ID de la aplicación de AIR, lo que hace que la funcionalidad de lista de permitidos en Primetime DRM se comporte de forma inesperada.
