---
title: Almacenar directivas de forma segura
description: Almacenar directivas de forma segura
copied-description: true
exl-id: fd335a0c-7eb1-4159-958f-7302fce98cef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Almacenar directivas de forma segura{#securely-storing-policies}

El SDK de acceso a Adobe proporciona una buena flexibilidad en el desarrollo de aplicaciones para su uso en el empaquetado de contenido y la creación de directivas. Al crear estas aplicaciones, puede que desee permitir que algunos usuarios creen y modifiquen directivas, y limitar a otros usuarios de forma que sólo puedan aplicar directivas existentes al contenido. En este caso, debe implementar los controles de acceso necesarios para crear cuentas de usuario con privilegios diferentes para la creación de directivas y la aplicación de directivas al contenido.

Las directivas no se firman ni se protegen de ninguna otra forma contra modificaciones hasta que se utilizan en el empaquetado. Si le preocupan los usuarios de las herramientas de empaquetado que modifican las directivas, debe considerar la posibilidad de firmar las directivas para asegurarse de que no se puedan modificar.

Para obtener más información sobre la creación de aplicaciones mediante el SDK, consulte la *Referencia de API de acceso de Adobe*.
