---
title: Almacenamiento seguro de políticas
description: Almacenamiento seguro de políticas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Almacenamiento seguro de directivas{#securely-storing-policies}

El SDK de acceso a Adobe proporciona una buena flexibilidad en el desarrollo de aplicaciones para su uso en el empaquetado de contenido y la creación de políticas. Al crear estas aplicaciones, es posible que desee permitir que algunos usuarios creen y modifiquen políticas, y limitar a otros usuarios de modo que solo puedan aplicar políticas existentes al contenido. Si este es el caso, debe implementar los controles de acceso necesarios para crear cuentas de usuario con diferentes privilegios para la creación de directivas y la aplicación de directivas al contenido.

Las políticas no están firmadas ni protegidas de ninguna otra manera contra modificaciones hasta que se utilizan en el embalaje. Si le preocupan los usuarios de las herramientas de empaquetado que modifican las directivas, debe considerar la posibilidad de firmar las directivas para garantizar que no se puedan modificar.

Para obtener más información sobre la creación de aplicaciones mediante el SDK, consulte la *Referencia de la API de acceso al Adobe*.
