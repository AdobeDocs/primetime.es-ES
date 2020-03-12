---
seo-title: Preferencias de Packager
title: Preferencias de Packager
uuid: 3e9c971d-3a5f-4f3e-97e7-baab63b1f67f
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c

---


# Preferencias de Packager {#packager-preferences}

Esta ficha contiene la configuración necesaria para empaquetar contenido. En la tabla siguiente se describen estas preferencias:

| Preferencia | Descripción |
|--- |--- |
| Certificado de transporte del servidor de licencias | El certificado de transporte del servidor, emitido por Adobe. Este certificado se utiliza para asegurar las comunicaciones entre el cliente y el servidor de licencias. El archivo debe estar ubicado en el directorio de recursos. |
| Habilitar HSM | Especifica si los certificados y las credenciales se almacenan en un HSM. Si es así, las preferencias relacionadas con certificados y credenciales se desactivarán y se deberán especificar las propiedades de la ficha HSM. |
| Opciones de cifrado clave | Especifica cómo se cifra la clave de cifrado de contenido en el momento del empaquetado |
| Certificado de servidor de licencias | El certificado del servidor de licencias, emitido por Adobe. El archivo debe estar ubicado en el directorio de recursos. El CEK se cifra con la clave pública del servidor de licencias. Sólo los titulares de la clave privada del servidor de licencias pueden descifrar el CEK. |
| Credencial de Packager | La credencial del empaquetador, emitida por Adobe. Este archivo se utiliza para firmar los metadatos durante el empaquetado. |
| Nombre del archivo | El archivo `PKCS#12` (.pfx) que contiene el certificado y la clave privada. El archivo debe estar ubicado en el directorio de recursos. |
| Contraseña de archivo | Contraseña para el archivo .pfx |
| Propiedades de la carpeta vigilada global | Especifica la configuración común a todas las carpetas vigiladas configuradas en este servidor. |
| Comprobar intervalo en milisegundos | Especifica la frecuencia con la que las carpetas vigiladas deben comprobar si hay contenido nuevo para empaquetar. El servidor repite todas las carpetas vigiladas configuradas y luego duerme durante esta cantidad de tiempo. |
| Sufijo de nombre de archivo de salida | Especifica una extensión de archivo para agregarla a los archivos de salida. Por ejemplo, si se especifica .out y el archivo de entrada es video.flv, el archivo de salida será video.out.flv. |
| Archivos de entrada de copia de seguridad | Especifica si se debe guardar una copia del contenido original. Si esta opción no está seleccionada, el archivo original se eliminará una vez que el empaquetado se haya completado correctamente. |
| Nombre de subcarpeta de copia de seguridad de entrada | Si la opción Copia de seguridad de archivos de entrada está seleccionada, especifica una carpeta en la que se guardarán los archivos de entrada. Esta opción especifica un nombre de carpeta relativo al directorio de entrada Carpeta vigilada. Si la carpeta no existe, se creará durante el empaquetado. |
| Sobrescribir archivos de salida existentes | Especifica si se puede sobrescribir el archivo de salida si ya existe un archivo con el mismo nombre. Si esta opción no está seleccionada y el archivo de salida ya existe, se omitirá el procesamiento del archivo de entrada. |
