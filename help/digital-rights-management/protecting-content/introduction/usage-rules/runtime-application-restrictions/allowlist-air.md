---
description: 'null'
seo-description: 'null'
seo-title: Lista de permitidos para aplicaciones DRM Primetime con permiso para reproducir contenido protegido
title: Lista de permitidos para aplicaciones DRM Primetime con permiso para reproducir contenido protegido
uuid: 23dd4faf-7992-4ee9-97ce-c6004ee995c2
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# Lista de permitidos para aplicaciones DRM Primetime con permiso para reproducir contenido protegido {#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

Una lista de permitidos especifica las aplicaciones de AIR, iOS y Android a las que se permite reproducir contenido. También especifica los ID de aplicaciones de AIR e iOS, la versión mínima, la versión máxima y el ID de editor.

Ejemplo de caso de uso: Utilice esta regla para limitar la reproducción a una aplicación concreta o para controlar la versión de la aplicación que puede acceder al contenido.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Si utiliza Adobe Flash Builder para crear aplicaciones protegidas, debe asegurarse de que no implementa la aplicación en modo de depuración. Al implementar una aplicación en modo de depuración, Flash Builder se añade `.debug` al ID de aplicación de AIR, lo que hace que la funcionalidad de lista de permitidos de Primetime DRM se comporte de forma inesperada.
