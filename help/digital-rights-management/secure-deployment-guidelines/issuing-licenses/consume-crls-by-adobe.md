---
description: El SDK descarga periódicamente las CRL publicadas por Adobe. Debe asegurarse de que el acceso a estos archivos no esté bloqueado o de que no se impida la aplicación de estas CRL.
title: Consumo de listas CRL publicadas por Adobe
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Consumo de listas CRL publicadas por Adobe{#consuming-crls-published-by-adobe}

El SDK descarga periódicamente las CRL publicadas por Adobe. Debe asegurarse de que el acceso a estos archivos no esté bloqueado o de que no se impida la aplicación de estas CRL.

El SDK tiene una opción de configuración para ignorar los errores al recuperar las CRL de Adobe y solo puede aplicar esta opción en entornos de desarrollo. En entornos de producción, el servidor de licencias debe recuperar las CRL desde el Adobe. Si el servidor de licencias no puede obtener una CRL válida, se ha producido un error.
