---
description: 'null'
seo-description: 'null'
seo-title: Acerca de los archivos de configuración de las herramientas de la línea de comandos
title: Acerca de los archivos de configuración de las herramientas de la línea de comandos
uuid: 8220921f-1fe9-439c-8134-dc16c2e3601b
translation-type: tm+mt
source-git-commit: 0143d98185b9a63ef978aba18e2f3c8728333155
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# Acerca de los archivos de configuración de las herramientas de la línea de comandos{#about-command-line-tools-configuration-files}

Las herramientas de la línea de comandos buscan [!DNL flashaccesstools.properties] en el directorio en el que se ejecutan las herramientas. Sin embargo, puede utilizar la opción `-c` cuando ejecute una herramienta de línea de comandos para especificar una ubicación diferente para el [!DNL flashaccesstools.properties] predeterminado. También puede utilizar `-c` para especificar un archivo de configuración diferente.

Los archivos de configuración de las herramientas de la línea de comandos utilizan el formato *archivo de propiedades Java*, para el cual se aplican las siguientes reglas:

* Escapar las barras invertidas con una barra invertida adicional.

   Por ejemplo, en un equipo Windows, para especificar el archivo [!DNL C:\credentials.pfx], debe escribirlo como [!DNL C:\\credentials.pfx] o `C:/credentials.pfx`. Para especificar un archivo en un servidor de red de Windows, debe especificar `\\\\server\\folder\\filename.pfx`
* Incluir sólo *caracteres Latin-1*.

   Para utilizar caracteres que no sean *Latin-1*, debe utilizar la secuencia de escape Unicode adecuada. Opcionalmente, puede aplicar la herramienta [!DNL native2ascii] (incluida con Java) a las entradas de archivo de configuración.
