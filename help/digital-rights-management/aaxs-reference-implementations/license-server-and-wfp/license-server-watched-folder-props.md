---
title: Propiedades de carpeta inspeccionada
description: Propiedades de carpeta inspeccionada
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Propiedades de carpeta inspeccionada {#watched-folder-properties}

Cada carpeta inspeccionada contiene un archivo llamado [!DNL properties/watchfolder.properties]. Este archivo contiene las opciones de empaquetado del contenido colocado en esta carpeta, incluido lo que se debe cifrar y las directivas que se deben aplicar. Cualquier cambio realizado en los valores del archivo de propiedades surtirá efecto la próxima vez que se ejecute el empaquetador de carpetas vigiladas (no es necesario reiniciar el servidor).

Si hay un error de configuración en el archivo de propiedades del empaquetador, se detiene el subproceso del empaquetador. Para reanudar el empaquetador de carpetas vigiladas, reinicie el servidor. Si hay un error de configuración en un archivo de propiedades de carpeta inspeccionada, la carpeta inspeccionada se elimina temporalmente de la lista de carpetas que procesa el empaquetador. Para volver a agregar la carpeta vigilada a la lista, reinicie el servidor o modifique el archivo de propiedades del empaquetador. Si se produce un error durante el empaquetado de un archivo concreto (por ejemplo, porque el archivo está dañado), el archivo se omite y se procesan los archivos restantes de la carpeta.
