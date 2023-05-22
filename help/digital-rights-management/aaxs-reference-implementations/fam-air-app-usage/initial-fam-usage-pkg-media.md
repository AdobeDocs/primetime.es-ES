---
title: Empaquetar medios
description: Empaquetar medios
copied-description: true
exl-id: fc2d1f12-8fab-4e62-8d4c-527911be347f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Empaquetar medios {#package-media}

Utilice la pestaña Medios del paquete para empaquetar contenido. La sección Propiedades del empaquetador muestra la configuración del empaquetador introducida en la pestaña Preferencias. Para modificar esta configuración, vaya a la pestaña Preferencias, cambie la configuración y haga clic en Guardar.

Si desea empaquetar un solo archivo FLV o F4V, elija la opción **[!UICONTROL Select Single File]** e introduzca la ruta completa al archivo de origen y la ruta completa donde se debe guardar el archivo cifrado.

Si desea empaquetar todos los archivos de una carpeta, elija la **[!UICONTROL Select Single Folder]** opción. Especifique la carpeta que contiene los archivos de origen. Solo los archivos de la carpeta de entrada que coincidan con **[!UICONTROL Input Media File Selection]** Los criterios de se empaquetarán (los archivos de las subcarpetas no se empaquetan). Elegir para cifrar [!DNL .flv] archivos, [!DNL .f4v] o introduzca una expresión regular personalizada (por ejemplo, &quot;.&#42;&quot; cifra todos los archivos de la carpeta). Los archivos cifrados se guardarán en la carpeta de salida especificada, con el mismo nombre de archivo que el archivo original.

>[!NOTE]
>
>Las rutas de archivo deben hacer referencia a los archivos disponibles en el servidor de empaquetado. Si está ejecutando el Administrador de Flash Access en un equipo diferente al servidor de empaquetado, debe especificar una ruta de acceso a la que pueda acceder el servidor (ya sea ubicada en una unidad de red o en el propio servidor).

La siguiente tabla describe las preferencias de medios del paquete:

| Preferencia | Descripción |
|---|---|
| Nombre(s) de archivo de política | Seleccione una o varias directivas de la lista desplegable para aplicarlas al contenido. Para seleccionar varias directivas, mantenga presionada la tecla CTRL mientras selecciona las directivas. |
| Segundos sin cifrar | Especifica el número de segundos de contenido que se dejarán sin cifrar al principio del archivo. Para cifrar empezando desde el principio, escriba &quot;0&quot;. |
| Cifrar vídeo | Seleccione esta casilla de verificación para cifrar datos de vídeo |
| Nivel de cifrado | Si el cifrado de vídeo está habilitado, seleccione el nivel de cifrado para los datos de vídeo. Alto cifra todos los datos de vídeo. Medio y bajo cifran selectivamente partes del vídeo. (Solo para F4V con vídeo H.264) |
| Cifrar audio | Seleccione esta casilla de verificación para cifrar datos de audio |
| Cifrar script | Seleccione esta casilla de verificación para cifrar datos de script (sólo FLV) |
| Propiedades personalizadas | Especifique propiedades personalizadas para incluirlas en el contenido empaquetado. Estas propiedades estarán disponibles para el servidor de licencias al emitir una licencia. (Opcional) |

Una vez seleccionadas las opciones de empaquetado, haga clic en **[!UICONTROL Package Media]** para empezar a empaquetar los archivos.
