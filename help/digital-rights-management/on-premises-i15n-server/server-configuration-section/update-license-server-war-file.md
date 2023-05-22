---
title: Actualizar el archivo WAR del servidor de licencias
description: Actualizar el archivo WAR del servidor de licencias
copied-description: true
exl-id: a70d04e2-24a4-4848-9e9b-97467f2c1749
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Actualizar el archivo WAR del servidor de licencias{#update-the-license-server-war-file}

Para admitir clientes que se hayan individualizado a través de un servidor de individualización local, debe actualizar la raíz de confianza del certificado del servidor de licencias para incluir la credencial de CA de individualización recién adquirida. Un script Python ( [!DNL addIndivCert.py]) se incluye en la [!DNL update_license_server] carpeta.

Haga lo siguiente para actualizar el servidor de licencias:

1. Realice una copia de los archivos WAR que desea actualizar (ejemplos: [!DNL flashaccess.war], [!DNL faxsks.war]).
1. Asegúrese de que los archivos WAR estén desbloqueados y de que tengan los permisos establecidos para poder modificarlos.
1. Ejecute el [!DNL addIndivCert.py] Script de Python para actualizar los archivos WAR del servidor de licencias.

   Las entradas del script son las siguientes:

   * `cert`: archivo PKCS12 que contiene el certificado de CA de individualización
   * `war`: archivo WAR para actualizar

   El archivo de salida es un archivo WAR actualizado.

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

Los archivos WAR se modificarán en su lugar. Si es necesario, puede editar la secuencia de comandos de Python para adaptarla a sus necesidades particulares. Después de realizar las actualizaciones, puede implementar los archivos WAR normalmente.
