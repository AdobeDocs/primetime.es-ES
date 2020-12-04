---
description: 'null'
seo-description: 'null'
seo-title: Lista de permitidos para aplicaciones DRM Primetime con permiso para reproducir contenido protegido
title: Lista de permitidos para aplicaciones DRM Primetime con permiso para reproducir contenido protegido
uuid: 23dd4faf-7992-4ee9-97ce-c6004ee995c2
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Lista de permitidos para aplicaciones DRM Primetime con permiso para reproducir contenido protegido {#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

Una lista de permitidos especifica las aplicaciones de AIR, iOS y Android a las que se permite reproducir contenido. También especifica los ID de aplicaciones de AIR e iOS, la versión mínima, la versión máxima y el ID de editor.

Ejemplo de caso de uso: Utilice esta regla para limitar la reproducción a una aplicación concreta o para controlar la versión de la aplicación que puede acceder al contenido.

>[!NOTE]
>
>Si utiliza Adobe Flash Builder para crear aplicaciones protegidas, debe asegurarse de no implementar la aplicación en modo de depuración. Cuando implementa una aplicación en modo de depuración, el Flash Builder anexa `.debug` al ID de aplicación de AIR, lo que hace que la funcionalidad de lista de permitidos en Primetime DRM se comporte de forma inesperada.
