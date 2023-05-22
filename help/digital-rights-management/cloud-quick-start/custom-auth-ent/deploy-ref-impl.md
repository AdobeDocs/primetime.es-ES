---
title: Implementar la implementación de referencia de BEES
description: Implementar la implementación de referencia de BEES
copied-description: true
exl-id: 87f3f879-66b4-4b8c-a0c4-e15551f9b727
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---

# Implementar la implementación de referencia de BEES {#deploy-the-bees-reference-implementation}

1. Configure el servidor de aplicaciones Tomcat. (Consulte la documentación de Tomcat).
1. Copie el `[!DNL bees.war]` archivo en Tomcat&#39;s [!DNL webapps/] carpeta.
1. Envíe una solicitud a `https://localhost:8080/bees`.

   Si ve el mensaje &quot;BEES está operativo&quot;, la implementación se ha completado correctamente.
1. Habilite SSL en su servidor.
