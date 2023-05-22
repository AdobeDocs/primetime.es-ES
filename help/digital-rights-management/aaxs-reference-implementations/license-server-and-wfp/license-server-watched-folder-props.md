---
title: Propiedades de carpeta inspeccionada
description: Propiedades de carpeta inspeccionada
copied-description: true
exl-id: e86518d4-2a16-45c7-aa96-189f677c3ee6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Propiedades de carpeta inspeccionada {#watched-folder-properties}

Cada carpeta inspeccionada contiene un archivo llamado [!DNL properties/watchfolder.properties]. Este archivo contiene las opciones de empaquetado del contenido colocado en esta carpeta, incluido lo que se debe cifrar y las directivas que se deben aplicar. Cualquier cambio realizado en los valores del archivo de propiedades surtirá efecto la próxima vez que se ejecute el empaquetador de carpetas vigiladas (no es necesario reiniciar el servidor).

Si hay un error de configuración en el archivo de propiedades del empaquetador, se detiene el subproceso del empaquetador. Para reanudar el empaquetador de carpetas vigiladas, reinicie el servidor. Si hay un error de configuración en un archivo de propiedades de carpeta inspeccionada, la carpeta inspeccionada se elimina temporalmente de la lista de carpetas que procesa el empaquetador. Para volver a agregar la carpeta vigilada a la lista, reinicie el servidor o modifique el archivo de propiedades del empaquetador. Si se produce un error durante el empaquetado de un archivo concreto (por ejemplo, porque el archivo está dañado), el archivo se omite y se procesan los archivos restantes de la carpeta.
