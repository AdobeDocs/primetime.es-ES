---
title: Ventana de reproducción
description: Ventana de reproducción
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Ventana de reproducción{#playback-window}

La ventana de reproducción especifica la duración de la validez de una licencia tras la primera vez que se utiliza para reproducir contenido protegido.

Ejemplo de caso de uso: Algunos modelos comerciales permiten un periodo de alquiler de 30 días, pero, una vez iniciada la reproducción, esta debe completarse en 48 horas. En este caso, la duración de la licencia de 48 horas es la ventana de reproducción.

**A partir de la versión 5.3** : La ventana de reproducción también admite la opción de habilitar o deshabilitar la detención completa, lo que indica si el contexto de descifrado para la reproducción debe detenerse al expirar la ventana de reproducción (habilitada) o continuar a pesar de la caducidad (deshabilitada).

>[!NOTE]
>
>La opción de parada forzada no funciona correctamente con la ventana de reproducción si se utiliza junto con ella (la ventana de reproducción no se respetará). La reproducción de contenido con la ventana de reproducción sin parada segura respeta la restricción de la ventana de reproducción.

