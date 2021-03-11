---
title: Preferencias de paquetes
description: Preferencias de paquetes
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Preferencias de paquete {#packager-preferences}

Esta pestaña contiene la configuración necesaria para empaquetar contenido. En la tabla siguiente se describen estas preferencias:

| Preferencia | Descripción |
|--- |--- |
| Certificado de transporte del servidor de licencias | El certificado de transporte del servidor, emitido por Adobe. Este certificado se utiliza para proteger las comunicaciones entre el cliente y el servidor de licencias. El archivo debe estar ubicado en el Directorio de recursos. |
| Habilitar HSM | Especifica si los certificados y las credenciales se almacenan en un HSM. Si es así, las preferencias relacionadas con certificados y credenciales se desactivarán y se deben especificar las propiedades de la pestaña HSM. |
| Opciones de cifrado clave | Especifica cómo se cifra la clave de cifrado de contenido en el momento del empaquetado |
| Certificado de servidor de licencias | Certificado de servidor de licencias, emitido por Adobe. El archivo debe estar ubicado en el Directorio de recursos. El CEK está cifrado con la clave pública del servidor de licencias. Solo los titulares de la clave privada del servidor de licencias pueden descifrar el CEK. |
| Credencial de Packager | La credencial del empaquetador, emitida por Adobe. Este archivo se utiliza para firmar los metadatos durante el empaquetado. |
| Nombre del archivo | El archivo `PKCS#12` (.pfx) que contiene certificado y clave privada. El archivo debe estar ubicado en el Directorio de recursos. |
| Contraseña del archivo | Contraseña del archivo .pfx |
| Propiedades de la carpeta global vigilada | Especifica la configuración común a todas las carpetas vigiladas configuradas en este servidor. |
| Comprobar intervalo en milisegundos | Especifica la frecuencia con la que las carpetas vigiladas deben comprobar si hay contenido nuevo en el paquete. El servidor se repite a través de todas las carpetas vigiladas configuradas y luego duerme durante esta cantidad de tiempo. |
| Sufijo de nombre de archivo de salida | Especifica una extensión de archivo para agregarla a los archivos de salida. Por ejemplo, si se especifica .out y el archivo de entrada es video.flv, el archivo de salida sería video.out.flv. |
| Archivos de entrada de copia de seguridad | Especifica si se debe guardar una copia del contenido original. Si no se selecciona esta opción, el archivo original se eliminará una vez que el paquete se haya completado correctamente. |
| Nombre de subcarpeta de copia de seguridad de entrada | Si la opción Copia de seguridad de archivos de entrada está seleccionada, especifica una carpeta donde se guardarán los archivos de entrada. Esta opción especifica un nombre de carpeta relativo al directorio de entrada Carpeta vigilada. Si la carpeta no existe, se creará durante el empaquetado. |
| Sobrescribir archivos de salida existentes | Especifica si el archivo de salida se puede sobrescribir si ya existe un archivo con el mismo nombre. Si esta opción no está seleccionada y el archivo de salida ya existe, el procesamiento del archivo de entrada se omitirá. |
