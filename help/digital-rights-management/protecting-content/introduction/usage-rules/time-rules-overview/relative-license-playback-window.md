---
title: Ventana de reproducción
description: Ventana de reproducción
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Ventana de reproducción{#playback-window}

La ventana de reproducción especifica la duración de una licencia válida después de la primera vez que se utiliza para reproducir contenido protegido.

Ejemplo de caso de uso: Algunos modelos de negocio permiten un periodo de alquiler de 30 días, pero una vez que comienza la reproducción, la reproducción debe completarse en 48 horas. En este caso, la duración de 48 horas de la licencia es la ventana de reproducción.

**A partir de la versión 5.3 adelante** : la ventana de reproducción también admite la opción de habilitar o deshabilitar la Parada dura, que indica si el contexto de descifrado para la reproducción debe detenerse al expirar la ventana de reproducción (habilitada) o continuar a pesar de la caducidad (deshabilitada).

>[!NOTE]
>
>La opción de parada dura no funciona correctamente con la ventana de reproducción si se utiliza junto con ella (no se respetará la ventana de reproducción). Al reproducir contenido con la ventana de reproducción sin parada segura, se respeta la restricción de la ventana de reproducción.

