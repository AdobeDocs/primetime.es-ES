---
title: Lista de permitidos para aplicaciones de Adobe ® Primetime permitidas para reproducir contenido protegido
description: Lista de permitidos para aplicaciones de Adobe ® Primetime permitidas para reproducir contenido protegido
copied-description: true
exl-id: 56004a0f-118c-42f3-869b-2cc1c91ee544
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Lista de permitidos para aplicaciones de Adobe ® Primetime permitidas para reproducir contenido protegido {#allowlist-for-adobe-primetime-applications-allowed-to-play-protected-content}

Especifica las aplicaciones de AIR/iOS que pueden reproducir contenido. Especifique el ID de la aplicación de AIR/iOS, la versión mínima, la versión máxima y el ID del editor.

Ejemplo de caso de uso: Utilice esta regla para limitar la reproducción a una aplicación de AIR/iOS concreta o para controlar qué versión puede acceder al contenido.

>[!NOTE]
>
>Si utiliza el Flash Builder de Adobe para crear aplicaciones protegidas, asegúrese de no implementar la aplicación en el modo &quot;Depurar&quot;. Al implementar una aplicación en modo &quot;Depuración&quot;, el Flash Builder anexará &quot;.debug&quot; al ID de aplicación de AIR. Esto provocará que la funcionalidad de lista de permitidos de Acceso a Adobe se comporte de forma inesperada.
