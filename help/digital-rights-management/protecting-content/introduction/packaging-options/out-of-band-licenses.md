---
title: Licencias fuera de banda
description: Licencias fuera de banda
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Licencias fuera de banda {#out-of-band-licenses}

Con Primetime DRM, se puede implementar un flujo de trabajo en el que los clientes obtienen licencias generadas previamente fuera de banda y, por lo tanto, se elimina la necesidad de implementar un servidor de licencias. Para admitir este flujo de trabajo, se debe especificar en el momento del empaquetado una opción que indique que no hay ningún servidor de licencias disponible. Esto evita que el cliente intente solicitar una licencia para este contenido desde un servidor de licencias.

El contenido que indica la no disponibilidad de un servidor de licencias solo se puede reproducir en clientes DRM de Primetime versión 3.0 o posterior. Los clientes más antiguos deben actualizar para reproducir este contenido.
