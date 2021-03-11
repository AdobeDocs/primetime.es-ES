---
title: Acerca de los archivos de configuración de las herramientas de la línea de comandos
description: Acerca de los archivos de configuración de las herramientas de la línea de comandos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Acerca de los archivos de configuración de las herramientas de línea de comandos{#about-command-line-tools-configuration-files}

Las herramientas de línea de comandos buscan [!DNL flashaccesstools.properties] en el directorio en el que ejecuta las herramientas. Sin embargo, puede utilizar la opción `-c` cuando ejecuta una herramienta de línea de comandos para especificar una ubicación diferente para el [!DNL flashaccesstools.properties] predeterminado. También puede utilizar `-c` para especificar un archivo de configuración diferente.

Los archivos de configuración de las herramientas de línea de comandos utilizan el formato *Java property file*, para el que se aplican las siguientes reglas:

* Escape las barras invertidas con una barra invertida adicional.

   Por ejemplo, en un equipo Windows, para especificar el archivo [!DNL C:\credentials.pfx], debe introducirlo como [!DNL C:\\credentials.pfx] o `C:/credentials.pfx`. Para especificar un archivo en un servidor de red de Windows, debe introducir `\\\\server\\folder\\filename.pfx`
* Incluir solo caracteres *Latin-1*.

   Para utilizar caracteres que no sean *Latin-1*, debe utilizar la secuencia de escape Unicode adecuada. Si lo desea, puede aplicar la herramienta [!DNL native2ascii] (incluida con Java) a las entradas del archivo de configuración.
