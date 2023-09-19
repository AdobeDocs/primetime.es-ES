---
title: Información general de la utilidad AIR Publisher ID
description: Información general de la utilidad AIR Publisher ID
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Información general de la utilidad AIR Publisher ID {#air-publisher-id-utility-overview}

Como parte del proceso de creación de un archivo AIR, la Herramienta para desarrolladores de AIR (ADT) genera un ID de publicador. Este es un identificador único del certificado utilizado para generar el archivo AIR. Si vuelve a utilizar el mismo certificado para varias aplicaciones de AIR, tendrán el mismo identificador de publicador.La utilidad AIR Publisher ID se utiliza para calcular el identificador de publicador de una aplicación de AIR. Las versiones de AIR posteriores a la 1.5.2 no escriben el ID de publicador generado en un archivo, por lo que es necesario utilizar esta herramienta para determinar el ID de publicador si utiliza una lista de permitidos de aplicación de AIR.

>[!NOTE]
>
>El identificador de publicador, que se utiliza para la aplicación de listas de permitidos de AIR, no es el mismo que el identificador de publicador especificado por el publicador de la aplicación en el [!DNL application.xml] archivo.
