---
title: Lista de permitidos para aplicaciones DRM de Primetime permitidas para reproducir contenido protegido
description: Lista de permitidos para aplicaciones DRM de Primetime permitidas para reproducir contenido protegido
copied-description: true
exl-id: c5aced0f-2c38-4ae7-9a33-44877e57a993
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Lista de permitidos para aplicaciones DRM de Primetime permitidas para reproducir contenido protegido {#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

Una lista de permitidos especifica las aplicaciones de AIR, iOS y Android permitidas para reproducir contenido. También especifica los ID de aplicación de AIR y iOS, la versión mínima, la versión máxima y el ID de editor.

Ejemplo de caso de uso: Utilice esta regla para limitar la reproducción a una aplicación concreta o para controlar la versión de la aplicación que puede acceder al contenido.

>[!NOTE]
>
>Si utiliza el Flash Builder de Adobe para generar aplicaciones protegidas, debe asegurarse de no implementar la aplicación en modo de depuración. Cuando se implementa una aplicación en modo de depuración, el Flash Builder anexa `.debug` a la ID de aplicación de AIR, lo que provoca que la funcionalidad de lista de permitidos de Primetime DRM se comporte de forma inesperada.
