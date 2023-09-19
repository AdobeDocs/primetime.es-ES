---
title: Consumir CRL publicadas por Adobe
description: Consumir CRL publicadas por Adobe
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# Consumir CRL publicadas por Adobe{#consume-crls-published-by-adobe}

El SDK descarga periódicamente CRL publicadas por Adobe. No bloquee el acceso a estos archivos ni impida la aplicación de estas CRL.

El SDK tiene una opción de configuración para ignorar los errores al recuperar las CRL de Adobe. Esta opción solo se puede utilizar en entornos de desarrollo. En entornos de producción, el servidor de licencias debe poder recuperar las CRL de la Adobe. Error al obtener una CRL válida.
