---
seo-title: Propiedades de la carpeta de inspección
title: Propiedades de la carpeta de inspección
uuid: fc204bb4-033a-46fe-8642-737f6a4cd1f1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Propiedades de carpeta observadas {#watched-folder-properties}

Cada carpeta vigilada contiene un archivo llamado [!DNL properties/watchfolder.properties]. Este archivo contiene las opciones de empaquetado para el contenido colocado en esta carpeta, incluyendo qué codificar y qué políticas aplicar. Los cambios realizados en los valores del archivo de propiedades tendrán efecto la próxima vez que se ejecute el empaquetador de carpetas vigilado (no es necesario reiniciar el servidor).

Si hay un error de configuración en el archivo de propiedades del empaquetador, el subproceso del empaquetador se detiene. Para reanudar el empaquetador de carpetas observado, reinicie el servidor. Si hay un error de configuración en un archivo de propiedades de carpeta vigilada, la carpeta vigilada se elimina temporalmente de la lista de las carpetas que procesa el empaquetador. Para volver a agregar la carpeta vigilada a la lista, reinicie el servidor o modifique el archivo de propiedades del empaquetador. Si se produce un error durante el empaquetado de un archivo determinado (por ejemplo, porque el archivo está dañado), se omite el archivo y se procesan los archivos restantes de la carpeta.
