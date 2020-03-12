---
seo-title: Ventana de reproducción
title: Ventana de reproducción
uuid: a06a1e28-8f14-4231-bb88-61aa7e33cace
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Ventana de reproducción{#playback-window}

La ventana de reproducción especifica la duración durante la que una licencia es válida la primera vez que se utiliza para reproducir contenido protegido.

Ejemplo de caso de uso: Algunos modelos empresariales permiten un período de alquiler de 30 días, pero, una vez que comienza la reproducción, la reproducción debe completarse en 48 horas. En este caso, la duración de 48 horas de la licencia es la ventana de reproducción.

**A partir de la versión 5.3 hacia adelante** : la ventana de reproducción también admite la opción de activar o desactivar la opción Parada dura, que indica si el contexto de descifrado para la reproducción debe detenerse al finalizar la ventana de reproducción (activado) o continuar a pesar de la caducidad (deshabilitado).

>[!NOTE]
>
>La opción de parada dura no funciona correctamente con la ventana de reproducción si se utiliza junto con ella (no se respetará la ventana de reproducción). La reproducción de contenido con la ventana de reproducción sin parada segura respeta la restricción de la ventana de reproducción.

