---
title: Acerca de los archivos de configuración de herramientas de línea de comandos
description: Acerca de los archivos de configuración de herramientas de línea de comandos
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Acerca de los archivos de configuración de herramientas de línea de comandos{#about-command-line-tools-configuration-files}

Las herramientas de la línea de comandos buscan [!DNL flashaccesstools.properties] en el directorio en el que se ejecutan las herramientas. Sin embargo, puede utilizar el complemento `-c` opción cuando se ejecuta una herramienta de línea de comandos para especificar una ubicación diferente para el valor predeterminado [!DNL flashaccesstools.properties]. También puede utilizar `-c` para especificar un archivo de configuración diferente.

Los archivos de configuración de las herramientas de la línea de comandos utilizan el *Archivo de propiedad Java* , para el cual se aplican las siguientes reglas:

* Salga de las barras invertidas con una barra invertida adicional.

  Por ejemplo, en un equipo con Windows, para especificar la variable [!DNL C:\credentials.pfx] , debe introducirlo como. [!DNL C:\\credentials.pfx] o `C:/credentials.pfx`. Para especificar un archivo en un servidor de red de Windows, debe escribir `\\\\server\\folder\\filename.pfx`
* Incluir solo *Latin-1* caracteres.

  Para utilizar recursos que no sean *Latin-1* caracteres, debe utilizar la secuencia de escape Unicode adecuada. Si lo desea, puede aplicar el [!DNL native2ascii] (incluida con Java) a las entradas del archivo de configuración.
