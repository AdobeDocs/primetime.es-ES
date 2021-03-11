---
title: Información general sobre la utilidad AIR Publisher ID
description: Información general sobre la utilidad AIR Publisher ID
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Descripción general de la utilidad AIR Publisher ID {#air-publisher-id-utility-overview}

Como parte del proceso de creación de un archivo AIR, la herramienta para desarrolladores de AIR (ADT) genera un ID de editor. Se trata de un identificador exclusivo del certificado utilizado para crear el archivo de AIR. Si vuelve a utilizar el mismo certificado para varias aplicaciones de AIR, tendrán el mismo ID de editor. La utilidad ID de editor de AIR se utiliza para calcular el ID de editor para una aplicación de AIR. Las versiones de AIR posteriores a la 1.5.2 no escriben el ID de editor generado en un archivo, por lo que es necesario utilizar esta herramienta para determinar el ID de editor si utiliza una lista de permitidos de aplicación de AIR.

>[!NOTE]
>
>El ID de editor, utilizado para la aplicación de listas de permitidos de AIR, no es el mismo que el ID de editor especificado por el editor de la aplicación en el archivo [!DNL application.xml] de la aplicación.
