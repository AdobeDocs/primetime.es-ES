---
seo-title: Empaquetado de medios
title: Empaquetado de medios
uuid: f6e877be-d916-4766-bc44-99891a3df3a8
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Empaquetado de medios {#package-media}

Utilice la ficha Empaquetar medios para empaquetar contenido. La sección Propiedades de Packager muestra la configuración de Packager que se introdujo en la ficha Preferencias. Para modificar esta configuración, vaya a la ficha Preferencias, cambie la configuración y guarde.

Si desea empaquetar un solo archivo FLV o F4V, elija la **[!UICONTROL Select Single File]** opción e introduzca la ruta completa al archivo de origen y la ruta completa donde se debe guardar el archivo codificado.

Si desea empaquetar todos los archivos de una carpeta, elija la **[!UICONTROL Select Single Folder]** opción. Especifique la carpeta que contiene los archivos de origen. Solo se empaquetarán los archivos de la carpeta de entrada que coincidan con los **[!UICONTROL Input Media File Selection]** criterios (los archivos de las subcarpetas no se empaquetan). Elija cifrar [!DNL .flv] archivos, [!DNL .f4v] archivos o introducir una expresión normal personalizada (por ejemplo, &quot;.*&quot; cifra todos los archivos de la carpeta). Los archivos cifrados se guardarán en la carpeta de salida especificada, utilizando el mismo nombre de archivo que el archivo original.

>[!NOTE]
>
>Las rutas de archivos deben hacer referencia a los archivos disponibles para el servidor de empaquetado. Si está ejecutando el Administrador de Flashes Access en un equipo diferente al servidor de empaquetado, debe especificar una ruta a la que el servidor pueda acceder (ya sea en una unidad de red o en el propio servidor).

En la tabla siguiente se describen las preferencias de Package Media:

| Preferencia | Descripción |
|---|---|
| Nombre(s) de archivo de directiva | Seleccione una o varias directivas en la lista desplegable para aplicarlas al contenido. Para seleccionar varias directivas, mantenga presionada la tecla CTRL mientras selecciona las directivas. |
| Segundos sin cifrar | Especifica el número de segundos de contenido que se dejará sin cifrar al principio del archivo. Para cifrar desde el principio, escriba &quot;0&quot;. |
| Cifrar vídeo | Seleccione esta casilla de verificación para cifrar datos de vídeo |
| Nivel de codificación | Si el cifrado de vídeo está habilitado, seleccione el nivel de codificación para los datos de vídeo. El alto cifra todos los datos de vídeo. Las partes del vídeo se cifran de forma selectiva, media y baja. (Solo para F4V con vídeo H.264) |
| Cifrar audio | Seleccione esta casilla de verificación para cifrar datos de audio |
| Codificar script | Seleccione esta casilla de verificación para cifrar datos de secuencias de comandos (solo FLV) |
| Propiedades personalizadas | Especifique las propiedades personalizadas que se incluirán en el contenido empaquetado. Estas propiedades estarán disponibles para el servidor de licencias al emitir una licencia. (Opcional) |

Una vez seleccionadas las opciones de empaquetado, haga clic en el **[!UICONTROL Package Media]** botón para empezar a empaquetar los archivos.
