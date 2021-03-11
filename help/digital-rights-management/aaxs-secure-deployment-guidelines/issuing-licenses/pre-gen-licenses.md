---
title: Licencias de pregeneración
description: Licencias de pregeneración
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# Licencias de pregeneración{#pre-generating-licenses}

Si está generando licencias previamente que contienen reglas de uso basadas en el tiempo, es muy recomendable que la licencia incluya requisitos de sincronización (consulte la guía *Uso del SDK de acceso al Adobe para la protección de contenido* ), de modo que la caducidad de la licencia se pueda aplicar de forma segura. Se recomienda implementar un mecanismo de &quot;latido&quot; entre el cliente y el servidor si tiene alguna restricción basada en el tiempo en la licencia, ya que el latido del corazón sincronizará la hora del cliente con la hora del servidor.
