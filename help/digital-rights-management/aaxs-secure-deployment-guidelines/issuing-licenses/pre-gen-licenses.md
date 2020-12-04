---
seo-title: Licencias de pregeneración
title: Licencias de pregeneración
uuid: 0207abdf-52bb-4bd0-a4f2-fe740b89fa83
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# Licencias de pregeneración{#pre-generating-licenses}

Si está generando licencias previamente que contienen reglas de uso basadas en el tiempo, se recomienda encarecidamente que la licencia incluya requisitos de sincronización (consulte *Uso de la guía SDK de Adobe Access para la protección de contenido*), para que la caducidad de la licencia se pueda aplicar de forma segura. Se recomienda implementar un mecanismo de latidos entre el cliente y el servidor si tiene alguna restricción basada en el tiempo en la licencia, ya que el latido del corazón sincronizará el tiempo del cliente con el tiempo del servidor.
