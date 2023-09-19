---
title: Parte inicial del contenido en la zona de borrado
description: Parte inicial del contenido en la zona de borrado
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Parte inicial del contenido en la zona de borrado{#initial-portion-of-content-in-the-clear}

Este parámetro opcional especifica la cantidad de tiempo (en segundos) desde el principio del contenido que permanecerá sin cifrar.

Ejemplo de caso de uso: Esto permite un tiempo de inicio de reproducción más rápido mientras el cliente DRM de Primetime descarga la licencia en segundo plano. La parte no encriptada del vídeo comienza a reproducirse inmediatamente mientras la inicialización y la adquisición de la licencia se producen en segundo plano. Cuando esta función está desactivada, es posible que los usuarios observen un retraso en la reproducción, ya que el equipo cliente realiza todos los pasos de licencia antes de que se produzca cualquier reproducción de vídeo.
