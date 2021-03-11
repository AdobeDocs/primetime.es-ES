---
title: Consumir listas CRL publicadas por Adobe
description: Consumir listas CRL publicadas por Adobe
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# Consumir listas CRL publicadas por Adobe{#consume-crls-published-by-adobe}

El SDK descarga periódicamente las CRL publicadas por Adobe. No bloquee el acceso a estos archivos ni impida la aplicación de estas CRL.

El SDK tiene una opción de configuración para ignorar los errores al recuperar las CRL de Adobe. Esta opción solo puede utilizarse en entornos de desarrollo. En entornos de producción, el servidor de licencias debe poder recuperar las CRL desde el Adobe. Error al obtener una CRL válida.
