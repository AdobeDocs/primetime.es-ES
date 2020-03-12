---
description: El SDK descarga periódicamente las CRL publicadas por Adobe. Debe asegurarse de que no se bloquee el acceso a estos archivos o de que no se impida la aplicación de estas CRL.
seo-description: El SDK descarga periódicamente las CRL publicadas por Adobe. Debe asegurarse de que no se bloquee el acceso a estos archivos o de que no se impida la aplicación de estas CRL.
seo-title: Consumo de CRL publicadas por Adobe
title: Consumo de CRL publicadas por Adobe
uuid: 7a9088bd-dde6-4445-958c-3e7272215b3c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Consumo de CRL publicadas por Adobe{#consuming-crls-published-by-adobe}

El SDK descarga periódicamente las CRL publicadas por Adobe. Debe asegurarse de que no se bloquee el acceso a estos archivos o de que no se impida la aplicación de estas CRL.

El SDK tiene una opción de configuración para ignorar los errores al recuperar las CRL de Adobe y solo puede aplicar esta opción en entornos de desarrollo. En los entornos de producción, el servidor de licencias debe recuperar las CRL de Adobe. Si el servidor de licencias no puede obtener una CRL válida, se ha producido un error.
