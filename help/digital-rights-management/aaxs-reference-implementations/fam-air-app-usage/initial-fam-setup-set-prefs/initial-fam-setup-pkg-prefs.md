---
title: Preferencias del empaquetador
description: Preferencias del empaquetador
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Preferencias del empaquetador {#packager-preferences}

Esta pestaña contiene la configuración necesaria para empaquetar contenido. En la tabla siguiente se describen estas preferencias:

| Preferencia | Descripción |
|--- |--- |
| Certificado de transporte del servidor de licencias | El certificado de transporte del servidor, emitido por el Adobe. Este certificado se utiliza para proteger las comunicaciones entre el cliente y el servidor de licencias. El archivo debe estar ubicado en el directorio de recursos. |
| Habilitar HSM | Especifica si los certificados y credenciales se almacenan en un HSM. Si es así, las preferencias relacionadas con los certificados y las credenciales se deshabilitarán y se deberán especificar las propiedades de la pestaña HSM. |
| Opciones de cifrado de claves | Especifica cómo se cifra la clave de cifrado de contenido en el momento del empaquetado |
| Certificado de servidor de licencias | El certificado del servidor de licencias, emitido por el Adobe. El archivo debe estar ubicado en el directorio de recursos. El CEK se cifra con la clave pública del servidor de licencias. Solo los titulares de la clave privada del servidor de licencias pueden descifrar el CEK. |
| Credencial del empaquetador | La credencial del empaquetador, emitida por Adobe. Este archivo se utiliza para firmar los metadatos durante el empaquetado. |
| Nombre de archivo | El `PKCS#12` ( .pfx) que contiene el certificado y la clave privada. El archivo debe estar ubicado en el directorio de recursos. |
| Contraseña de archivo | Contraseña para el archivo .pfx |
| Propiedades globales de carpeta inspeccionada | Especifica la configuración común a todas las carpetas inspeccionadas configuradas en este servidor. |
| Intervalo de comprobación en milisegundos | Especifica la frecuencia con la que las carpetas inspeccionadas deben comprobar si hay contenido nuevo que empaquetar. El servidor repite por todas las carpetas inspeccionadas configuradas y luego permanece en suspensión durante este período de tiempo. |
| Sufijo del nombre del archivo de salida | Especifica la extensión de archivo que se agregará a los archivos de salida. Por ejemplo, si se especifica .out y el archivo de entrada es video.flv, el archivo de salida sería video.out.flv. |
| Copia de seguridad de archivos de entrada | Especifica si se debe guardar una copia del contenido original. Si no se selecciona esta opción, el archivo original se eliminará una vez que el empaquetado se haya completado correctamente. |
| Nombre de subcarpeta de copia de seguridad de entrada | Si la opción Backup Input Files está seleccionada, especifica una carpeta en la que se guardarán los archivos de entrada. Esta opción especifica un nombre de carpeta relativo al directorio de entrada de la carpeta inspeccionada. Si la carpeta no existe, se crea durante el empaquetado. |
| Sobrescribir archivos de salida existentes | Especifica si el archivo de salida se puede sobrescribir si ya existe un archivo con el mismo nombre. Si esta opción no está seleccionada y el archivo de salida ya existe, se omitirá el procesamiento del archivo de entrada. |
