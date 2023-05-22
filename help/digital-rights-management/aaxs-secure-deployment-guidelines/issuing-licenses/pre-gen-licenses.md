---
title: Generación previa de licencias
description: Generación previa de licencias
copied-description: true
exl-id: d0bdd722-fd0e-4f34-87e7-28a564daf82b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# Generación previa de licencias{#pre-generating-licenses}

Si está pregenerando licencias que contienen reglas de uso basadas en el tiempo, es muy recomendable que la licencia incluya requisitos de sincronización (consulte *Uso del SDK de acceso a Adobe para proteger el contenido* guía), para que la caducidad de la licencia se pueda aplicar de forma segura. La implementación de un mecanismo de &quot;latido&quot; entre el cliente y el servidor es muy recomendable si tiene restricciones basadas en el tiempo en la licencia, ya que el latido sincronizará la hora del cliente con la hora del servidor.
