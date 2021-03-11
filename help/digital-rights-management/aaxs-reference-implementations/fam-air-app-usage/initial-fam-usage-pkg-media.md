---
title: Medios de paquetes
description: Medios de paquetes
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Medios de paquete {#package-media}

Utilice la pestaña Package Media para empaquetar contenido. La sección Propiedades del empaquetador muestra la configuración del empaquetador que se introdujo en la ficha Preferencias. Para modificar esta configuración, vaya a la pestaña Preferencias, cambie la configuración y guarde.

Si desea empaquetar un solo archivo FLV o F4V, elija la opción **[!UICONTROL Select Single File]** e introduzca la ruta completa al archivo de origen y la ruta completa donde debe guardarse el archivo cifrado.

Si desea empaquetar todos los archivos de una carpeta, seleccione la opción **[!UICONTROL Select Single Folder]**. Especifique la carpeta que contiene los archivos de origen. Solo se empaquetarán los archivos de la carpeta de entrada que coincidan con los criterios **[!UICONTROL Input Media File Selection]** (los archivos de las subcarpetas no están empaquetados). Elija cifrar archivos [!DNL .flv], [!DNL .f4v] o introducir una expresión regular personalizada (por ejemplo, &quot;.*&quot; cifra todos los archivos de la carpeta). Los archivos cifrados se guardarán en la carpeta de salida especificada, utilizando el mismo nombre de archivo que el archivo original.

>[!NOTE]
>
>Las rutas de archivo deben hacer referencia a los archivos disponibles para el servidor de empaquetado. Si está ejecutando el Administrador de Flashes Access en un equipo diferente al servidor de paquetes, debe especificar una ruta a la que sea accesible para el servidor (ya sea en una unidad de red o en el propio servidor).

En la tabla siguiente se describen las preferencias de medios de paquete:

| Preferencia | Descripción |
|---|---|
| Nombres de archivos de directivas | Seleccione una o varias políticas de la lista desplegable para aplicarlas al contenido. Para seleccionar varias directivas, mantenga pulsada la tecla CTRL mientras selecciona las directivas. |
| Segundos sin cifrar | Especifica el número de segundos de contenido que se dejarán sin cifrar al principio del archivo. Para cifrar a partir del principio, escriba &quot;0&quot;. |
| Codificar vídeo | Seleccione esta casilla de verificación para cifrar datos de vídeo |
| Nivel de cifrado | Si el cifrado de vídeo está habilitado, seleccione el nivel de codificación para los datos de vídeo. Alta cifra todos los datos de vídeo. Las partes del vídeo se cifran de forma selectiva en medias y bajas. (Solo para F4V con vídeo H.264) |
| Codificar audio | Seleccione esta casilla de verificación para cifrar datos de audio |
| Codificar script | Seleccione esta casilla de verificación para cifrar datos de scripts (solo FLV) |
| Propiedades personalizadas | Especifique propiedades personalizadas para incluirlas en el contenido empaquetado. Estas propiedades estarán disponibles para el servidor de licencias al emitir una licencia. (Opcional) |

Una vez seleccionadas las opciones de empaquetado, haga clic en el botón **[!UICONTROL Package Media]** para comenzar a empaquetar los archivos.
