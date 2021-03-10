---
title: Implementación de la implementación de referencia BEES
description: Implementación de la implementación de referencia BEES
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---


# Implementar la implementación de referencia de BEES {#deploy-the-bees-reference-implementation}

1. Configure el servidor de aplicaciones Tomcat. (Consulte la documentación de Tomcat.)
1. Copie el archivo `[!DNL bees.war]` en la carpeta [!DNL webapps/] de Tomcat.
1. Envíe una solicitud a `https://localhost:8080/bees`.

   Si ve el mensaje &quot;BEES is operation&quot;, la implementación se completa correctamente.
1. Habilite SSL en el servidor.
