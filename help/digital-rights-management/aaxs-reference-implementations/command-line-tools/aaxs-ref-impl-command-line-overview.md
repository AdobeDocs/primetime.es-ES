---
title: 'Herramientas de la línea de comandos para empaquetar contenido y crear listas de revocaciones '
description: 'Herramientas de la línea de comandos para empaquetar contenido y crear listas de revocaciones '
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# Herramientas de línea de comandos para empaquetar contenido y crear listas de revocaciones {#command-line-tools-for-packaging-content-revocation-lists}

La implementación de referencia incluye las siguientes herramientas de línea de comandos:

* Administrador de políticas: Herramienta para crear y administrar políticas
* Administrador de listas de actualización de directivas: Herramienta para crear y ver listas de actualización de directivas
* Administrador de la lista de revocación: Herramienta para crear y ver listas de revocación
* Paquete de medios: Herramienta para crear archivos FLV y F4V cifrados
* AIR Publisher ID
* Generador de licencias de utilidad
* Incrustador de licencias

## Requisitos {#requirements}

Los requisitos para utilizar las herramientas de línea de comandos disponibles en las implementaciones de referencia son los siguientes:

* Todas las herramientas de la línea de comandos requieren Java 1.5 o superior.
* Credenciales del paquete y del servidor de licencias (certificado y contraseña) que se emiten mediante Adobe. Necesita credenciales para cifrar y firmar archivos de vídeo, para firmar listas de revocación y actualización de directivas y para generar licencias previamente.

>[!NOTE]
>
>Debido a un error de Java, los argumentos que se utilizan en la línea de comandos (como nombres de archivo, nombres de directiva o descripciones) solo deben utilizar caracteres del conjunto de caracteres predeterminado del sistema operativo.

## Archivo de configuración {#configuration-file}

Varias de las herramientas de la línea de comandos requieren un archivo de configuración que contenga información para las herramientas que se utilizarán para aplicar políticas y cifrar archivos.

El archivo de configuración predeterminado es [!DNL flashaccesstools.properties]. Se encuentra en el directorio de trabajo; es decir, el directorio desde el que ejecuta las herramientas (consulte Instalación de las herramientas de la línea de comandos). Cada herramienta también contiene una opción ( `-c`) que le permite señalar al archivo de configuración que desea utilizar si prefiere no utilizar el valor predeterminado.

El archivo de configuración utiliza el formato de archivo de propiedad Java. Si los valores de cualquiera de las propiedades contienen caracteres especiales, tenga en cuenta las restricciones siguientes:

* Escape las barras invertidas con una barra invertida adicional. Por ejemplo, para especificar el archivo [!DNL C:\credentials.pfx], especifíquelo como [!DNL C:\\credentials.pfx] o `C:/credentials.pfx`. Para especificar un archivo en un servidor de red, especifique `\\\\server\\folder\\filename.pfx`.
* El archivo de configuración solo puede contener caracteres Latin-1. Si debe utilizar caracteres que no sean Latin-1, utilice la secuencia de escape Unicode apropiada (con la herramienta [!DNL native2ascii] que viene con Java).

Establezca los valores de las propiedades en el archivo de configuración antes de ejecutar las herramientas. Para algunas herramientas de la línea de comandos, puede establecer los valores de algunas opciones a través de la línea de comandos o el archivo de configuración. En esos casos, los valores configurados a través de la línea de comandos tienen prioridad sobre cualquier valor del archivo de configuración.

## Instalación de las herramientas de la línea de comandos {#installing-the-command-line-tools}

Puede copiar los archivos que necesita del directorio [!DNL \Reference Implementation\Command Line Tools] del DVD, que contiene el archivo de configuración predeterminado [!DNL flashaccesstools.properties], y un directorio [!DNL libs], que contiene los archivos JAR para las herramientas.

El directorio [!DNL samples] contiene varios archivos de origen Java de muestra que demuestran el uso de las API del SDK de acceso al Adobe. Para crear y ejecutar los ejemplos, utilice el script [!DNL build-samples.xml] Ant.