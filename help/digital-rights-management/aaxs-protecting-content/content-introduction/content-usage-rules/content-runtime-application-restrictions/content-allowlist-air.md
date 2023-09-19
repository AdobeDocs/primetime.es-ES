---
title: Lista de permitidos para aplicaciones de Adobe ® Primetime permitidas para reproducir contenido protegido
description: Lista de permitidos para aplicaciones de Adobe ® Primetime permitidas para reproducir contenido protegido
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
