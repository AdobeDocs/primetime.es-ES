---
title: Propiedades de la carpeta vigilada
description: Propiedades de la carpeta vigilada
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Propiedades de carpeta vigiladas {#watched-folder-properties}

Cada carpeta vigilada contiene un archivo llamado [!DNL properties/watchfolder.properties]. Este archivo contiene las opciones de empaquetado para el contenido colocado en esta carpeta, lo que incluye qué cifrar y qué políticas aplicar. Cualquier cambio realizado en los valores del archivo de propiedad surtirá efecto la próxima vez que se ejecute el paquete de carpetas visto (no es necesario reiniciar el servidor).

Si hay un error de configuración en el archivo de propiedades del empaquetador, el subproceso del empaquetador se detiene. Para reanudar el empaquetador de carpetas visto, reinicie el servidor. Si hay un error de configuración en un archivo de propiedades de carpeta vigilada, la carpeta vigilada se elimina temporalmente de la lista de carpetas que procesa el empaquetador. Para volver a añadir la carpeta vigilada a la lista, reinicie el servidor o modifique el archivo de propiedades del empaquetador. Si se produce un error durante el empaquetado de un archivo concreto (por ejemplo, porque el archivo está dañado), el archivo se omite y se procesan los archivos restantes de la carpeta.
