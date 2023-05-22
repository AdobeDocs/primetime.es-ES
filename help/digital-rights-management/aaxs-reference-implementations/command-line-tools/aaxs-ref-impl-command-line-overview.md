---
title: Herramientas de línea de comandos para empaquetar contenido y crear listas de revocaciones
description: Herramientas de línea de comandos para empaquetar contenido y crear listas de revocaciones
copied-description: true
exl-id: 34305dab-a2f0-41c2-9a59-3261e8dea7e2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Herramientas de línea de comandos para empaquetar contenido y crear listas de revocaciones {#command-line-tools-for-packaging-content-revocation-lists}

La implementación de referencia incluye las siguientes herramientas de línea de comandos:

* Administrador de directivas: herramienta para crear y administrar directivas
* Administrador de listas de actualización de directivas: herramienta para crear y ver listas de actualización de directivas
* Administrador de listas de revocación: herramienta para crear y ver listas de revocación
* Media Packager: herramienta para crear archivos FLV y F4V cifrados
* ID de publicador de AIR
* Generador de licencias de utilidades
* Incrustador de licencia

## Requisitos {#requirements}

Los requisitos para utilizar las herramientas de línea de comandos disponibles en las implementaciones de referencia son los siguientes:

* Todas las herramientas de línea de comandos requieren Java 1.5 o superior.
* Credenciales del empaquetador y del servidor de licencias (certificado y contraseña) emitidas por el Adobe. Necesita credenciales para cifrar y firmar archivos de vídeo, para firmar listas de actualización y revocación de directivas y para generar previamente licencias.

>[!NOTE]
>
>Debido a un error de Java, los argumentos que se utilizan en la línea de comandos (como nombres de archivo, nombres de directivas o descripciones) sólo deben utilizar caracteres del conjunto de caracteres predeterminado del sistema operativo.

## Archivo de configuración {#configuration-file}

Varias de las herramientas de la línea de comandos requieren un archivo de configuración que contiene información para las herramientas que se van a utilizar para aplicar directivas y cifrar archivos.

El archivo de configuración predeterminado es [!DNL flashaccesstools.properties]. Se encuentra en el directorio de trabajo, es decir, el directorio desde el que se ejecutan las herramientas (consulte Instalación de las herramientas de la línea de comandos). Cada herramienta también contiene una opción ( `-c`), que le permite seleccionar el archivo de configuración que desea utilizar si prefiere no utilizar el predeterminado.

El archivo de configuración utiliza el formato de archivo de propiedad Java. Si los valores de cualquiera de las propiedades contienen caracteres especiales, tenga en cuenta las siguientes restricciones:

* Salga de las barras invertidas con una barra invertida adicional. Por ejemplo, para especificar la variable [!DNL C:\credentials.pfx] archivo, especifíquelo como [!DNL C:\\credentials.pfx] o `C:/credentials.pfx`. Para especificar un archivo en un servidor de red, especifique `\\\\server\\folder\\filename.pfx`.
* El archivo de configuración solo puede contener caracteres latinos-1. Si debe utilizar caracteres que no sean Latin-1, utilice la secuencia de escape Unicode adecuada (utilizando, opcionalmente, el método [!DNL native2ascii] que viene con Java).

Establezca valores para las propiedades del archivo de configuración antes de ejecutar las herramientas. Para algunas de las herramientas de línea de comandos, puede establecer los valores de algunas opciones a través de la línea de comandos o del archivo de configuración. En estos casos, los valores que se establecen a través de la línea de comandos tienen prioridad sobre cualquier valor del archivo de configuración.

## Instalación de las herramientas de línea de comandos  {#installing-the-command-line-tools}

Puede copiar los archivos que necesite desde el [!DNL \Reference Implementation\Command Line Tools] en el DVD, que contiene el directorio predeterminado [!DNL flashaccesstools.properties] y un archivo de configuración [!DNL libs] , que contiene los archivos JAR para las herramientas.

El [!DNL samples] contiene varios archivos de origen Java de ejemplo que muestran el uso de las API del SDK de acceso a Adobe. Para generar y ejecutar los ejemplos, utilice el [!DNL build-samples.xml] Guión hormiga.
