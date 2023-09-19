---
title: Almacenar directivas de forma segura
description: Almacenar directivas de forma segura
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Almacenar directivas de forma segura{#securely-storing-policies}

El SDK de acceso a Adobe proporciona una gran flexibilidad en el desarrollo de aplicaciones para su uso en el empaquetado de contenido y en la creación de políticas. Al crear estas aplicaciones, puede que desee permitir que algunos usuarios creen y modifiquen directivas, y limitar a otros usuarios de forma que sólo puedan aplicar directivas existentes al contenido. En este caso, debe implementar los controles de acceso necesarios para crear cuentas de usuario con privilegios diferentes para la creación de directivas y la aplicación de directivas al contenido.

Las directivas no se firman ni se protegen de ninguna otra forma contra modificaciones hasta que se utilizan en el empaquetado. Si le preocupan los usuarios de las herramientas de empaquetado que modifican las directivas, debe considerar la posibilidad de firmar las directivas para asegurarse de que no se puedan modificar.

Para obtener más información sobre la creación de aplicaciones mediante el SDK, consulte la *Referencia de API de acceso de Adobe*.
