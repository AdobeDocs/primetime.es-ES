---
title: Generación previa de licencias
description: Generación previa de licencias
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# Generación previa de licencias{#pre-generating-licenses}

Si está pregenerando licencias que contienen reglas de uso basadas en el tiempo, es muy recomendable que la licencia incluya requisitos de sincronización (consulte *Uso del SDK de acceso a Adobe para proteger el contenido* guía), para que la caducidad de la licencia se pueda aplicar de forma segura. La implementación de un mecanismo de &quot;latido&quot; entre el cliente y el servidor es muy recomendable si tiene restricciones basadas en el tiempo en la licencia, ya que el latido sincronizará la hora del cliente con la hora del servidor.
