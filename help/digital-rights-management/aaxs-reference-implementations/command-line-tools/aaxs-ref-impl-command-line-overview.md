---
seo-title: 'Herramientas de la línea de comandos para empaquetar contenido y crear listas de revocación '
title: 'Herramientas de la línea de comandos para empaquetar contenido y crear listas de revocación '
uuid: 2c740521-2004-4320-88e1-118b84e80e31
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# Herramientas de la línea de comandos para empaquetar contenido y crear listas de revocación {#command-line-tools-for-packaging-content-revocation-lists}

La implementación de referencia incluye las siguientes herramientas de línea de comandos:

* Administrador de directivas: Una herramienta para crear y administrar políticas
* Administrador de Listas de actualización de directivas: Herramienta para crear y ver listas de actualización de directivas
* Administrador de Listas de revocación: Herramienta para crear y ver listas de revocación
* Media Packager: Herramienta para crear archivos FLV y F4V cifrados
* ID de editor de AIR
* Generador de licencias de utilidad
* Incrustación de licencias

## Requisitos {#requirements}

Los requisitos para utilizar las herramientas de línea de comandos disponibles en las implementaciones de referencia son los siguientes:

* Todas las herramientas de la línea de comandos requieren Java 1.5 o superior.
* Credenciales de Packager y del servidor de licencias (certificado y contraseña) que se emiten mediante Adobe. Necesita credenciales para cifrar y firmar archivos de vídeo, para firmar listas de revocación y actualización de directivas y para generar licencias previamente.

>[!NOTE]
>
>Debido a un error de Java, los argumentos que se utilizan en la línea de comandos (como nombres de archivo, nombres de política o descripciones) deben utilizar sólo caracteres del conjunto de caracteres predeterminado del sistema operativo.

## Archivo de configuración {#configuration-file}

Varias de las herramientas de la línea de comandos requieren un archivo de configuración que contenga información para las herramientas que se utilizarán para aplicar políticas y cifrar archivos.

El archivo de configuración predeterminado es [!DNL flashaccesstools.properties]. Se encuentra en el directorio de trabajo; es decir, el directorio desde el cual se ejecutan las herramientas (consulte Instalación de las herramientas de la línea de comandos). Cada herramienta también contiene una opción ( `-c`) que le permite apuntar al archivo de configuración que desee utilizar si prefiere no utilizar el predeterminado.

El archivo de configuración utiliza el formato de archivo de propiedad Java. Si los valores de cualquiera de las propiedades contienen caracteres especiales, tenga en cuenta las siguientes restricciones:

* Escapar las barras invertidas con una barra invertida adicional. Por ejemplo, para especificar el archivo [!DNL C:\credentials.pfx], especifíquelo como [!DNL C:\\credentials.pfx] o `C:/credentials.pfx`. Para especificar un archivo en un servidor de red, especifique `\\\\server\\folder\\filename.pfx`.
* El archivo de configuración sólo puede contener caracteres Latin-1. Si debe utilizar caracteres que no sean Latin-1, utilice la secuencia de escape Unicode adecuada (si lo desea, utilice la herramienta [!DNL native2ascii] que viene con Java).

Defina los valores de las propiedades en el archivo de configuración antes de ejecutar las herramientas. Para algunas de las herramientas de la línea de comandos, puede establecer los valores de algunas opciones a través de la línea de comandos o del archivo de configuración. En esos casos, los valores que se establecen a través de la línea de comandos tienen prioridad sobre cualquier valor del archivo de configuración.

## Instalación de las herramientas de la línea de comandos {#installing-the-command-line-tools}

Puede copiar los archivos que necesita del directorio [!DNL \Reference Implementation\Command Line Tools] del DVD, que contiene el archivo de configuración predeterminado [!DNL flashaccesstools.properties], y un directorio [!DNL libs], que contiene los archivos JAR para las herramientas.

El directorio [!DNL samples] contiene varios archivos de origen Java de muestra que demuestran el uso de las API del SDK de Adobe Access. Para generar y ejecutar los ejemplos, utilice la secuencia de comandos [!DNL build-samples.xml] Ant.