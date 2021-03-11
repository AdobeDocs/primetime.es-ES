---
title: Licencias fuera de banda
description: Licencias fuera de banda
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# Licencias fuera de banda {#out-of-band-licenses}

Con Primetime DRM, puede implementar un flujo de trabajo en el que los clientes obtengan licencias pregeneradas fuera de banda y, por lo tanto, no tengan que implementar un servidor de licencias. Para admitir este flujo de trabajo, se debe especificar una opción que indique que no hay ningún servidor de licencias disponible en el momento del empaquetado. Esto evita que el cliente intente solicitar una licencia para este contenido desde un servidor de licencias.

El contenido que indica la no disponibilidad de un servidor de licencias solo se puede reproducir en clientes de Primetime DRM versión 3.0 o posterior. Los clientes más antiguos deben actualizar para reproducir este contenido.
