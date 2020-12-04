---
seo-title: Actualizar el archivo WAR del servidor de licencias
title: Actualizar el archivo WAR del servidor de licencias
uuid: 0cde53d6-185d-4bf2-84fc-0c31d17904a8
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# Actualizar el archivo WAR del servidor de licencias{#update-the-license-server-war-file}

Para admitir clientes que se han individualizado mediante un servidor de individualización local, debe actualizar la raíz de confianza del certificado del servidor de licencias para incluir las credenciales de CA de individualización recién adquiridas. Se incluye una secuencia de comandos Python ( [!DNL addIndivCert.py]) en la carpeta [!DNL update_license_server].

Para actualizar el servidor de licencias, haga lo siguiente:

1. Haga una copia de los archivos de la GUERRA para actualizar (ejemplos: [!DNL flashaccess.war], [!DNL faxsks.war]).
1. Asegúrese de que los archivos WAR están desbloqueados y de que tienen sus permisos establecidos para que se puedan modificar.
1. Ejecute la secuencia de comandos [!DNL addIndivCert.py] Python para actualizar los archivos de License Server WAR.

   Las entradas para la secuencia de comandos son las siguientes:

   * `cert`:: Archivo PKCS12 que contiene el certificado de CA de individualización
   * `war`:: Archivo WAR que se va a actualizar

   El archivo de salida es un archivo WAR actualizado.

   ```
   ./addIndivCert.py -cert NEW_IndivCA.cer -war flashaccess.war
   ```

Los archivos WAR se modificarán en su lugar. Si es necesario, puede editar el script Python para adaptarlo a sus necesidades particulares. Después de realizar las actualizaciones, puede implementar los archivos WAR normalmente.
