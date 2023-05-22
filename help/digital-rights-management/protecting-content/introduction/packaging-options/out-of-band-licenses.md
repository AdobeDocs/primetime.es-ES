---
title: Licencias fuera de banda
description: Licencias fuera de banda
copied-description: true
exl-id: d9e54c8f-ff82-4834-a62e-20e67c4343dd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Licencias fuera de banda {#out-of-band-licenses}

Con Primetime DRM, se puede implementar un flujo de trabajo en el que los clientes obtienen licencias generadas previamente fuera de banda y, por lo tanto, se elimina la necesidad de implementar un servidor de licencias. Para admitir este flujo de trabajo, se debe especificar en el momento del empaquetado una opción que indique que no hay ningún servidor de licencias disponible. Esto evita que el cliente intente solicitar una licencia para este contenido desde un servidor de licencias.

El contenido que indica la no disponibilidad de un servidor de licencias solo se puede reproducir en clientes DRM de Primetime versión 3.0 o posterior. Los clientes más antiguos deben actualizar para reproducir este contenido.
