---
title: Actualizar el archivo WAR del servidor de licencias
description: Actualizar el archivo WAR del servidor de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# Actualizar el archivo WAR del servidor de licencias{#update-the-license-server-war-file}

Para admitir clientes que se han individualizado a través de un servidor de individualización On Premies, debe actualizar la raíz de confianza del certificado del servidor de licencias para incluir la credencial de CA de Individualización recién adquirida. Se incluye un script Python ( [!DNL addIndivCert.py]) en la carpeta [!DNL update_license_server].

Haga lo siguiente para actualizar el servidor de licencias:

1. Haga una copia de los archivos WAR que se actualizarán (ejemplos: [!DNL flashaccess.war], [!DNL faxsks.war]).
1. Asegúrese de que los archivos WAR estén desbloqueados y que tengan sus permisos establecidos para que se puedan modificar.
1. Ejecute el script [!DNL addIndivCert.py] Python para actualizar los archivos WAR del servidor de licencias.

   Las entradas para la secuencia de comandos son las siguientes:

   * `cert`: Archivo PKCS12 que contiene el certificado de CA de individualización
   * `war`: Archivo WAR que se va a actualizar

   El archivo de salida es un archivo WAR actualizado.

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

Los archivos de la GUERRA se modificarán en su lugar. Si es necesario, puede editar la secuencia de comandos de Python para adaptarla a sus necesidades particulares. Después de realizar las actualizaciones, puede implementar normalmente los archivos WAR.
