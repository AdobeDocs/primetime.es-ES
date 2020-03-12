---
seo-title: Licencias fuera de banda
title: Licencias fuera de banda
uuid: 43397ce5-6c52-429d-b7fa-fa8c91cf9742
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Licencias fuera de banda {#out-of-band-licenses}

Con Primetime DRM, puede implementar un flujo de trabajo en el que los clientes obtienen licencias pregeneradas fuera de banda y, por lo tanto, eliminar la necesidad de implementar un servidor de licencias. Para admitir este flujo de trabajo, se debe especificar una opción que indique que no hay ningún servidor de licencias disponible en el momento del empaquetado. Esto evita que el cliente intente solicitar una licencia para este contenido desde un servidor de licencias.

El contenido que indica la no disponibilidad de un servidor de licencias solo se puede reproducir en los clientes Primetime DRM versión 3.0 o posterior. Los clientes más antiguos necesitan actualizar para reproducir este contenido.
