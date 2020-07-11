---
seo-title: Información general sobre la utilidad de ID de AIR Publisher
title: Información general sobre la utilidad de ID de AIR Publisher
uuid: 31aecc0e-ad9b-43ad-ba58-77d2c999f4a4
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# Información general sobre la utilidad de ID de AIR Publisher {#air-publisher-id-utility-overview}

Como parte del proceso de creación de un archivo de AIR, AIR Developer Tool (ADT) genera un ID de editor. Identificador exclusivo del certificado utilizado para generar el archivo de AIR. Si reutiliza el mismo certificado para varias aplicaciones de AIR, tendrán el mismo ID de editor.La utilidad de ID de editor de AIR se utiliza para calcular el ID de editor para una aplicación de AIR. Las versiones de AIR posteriores a 1.5.2 no escriben el ID de editor generado en un archivo, por lo que es necesario utilizar esta herramienta para determinar el ID de editor si se utiliza una lista de permitidos de aplicación de AIR.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>El ID de editor, utilizado para la aplicación de listas de permitidos de AIR, no es el mismo que el ID de editor especificado por el editor de la aplicación en el [!DNL application.xml] archivo de la aplicación.
