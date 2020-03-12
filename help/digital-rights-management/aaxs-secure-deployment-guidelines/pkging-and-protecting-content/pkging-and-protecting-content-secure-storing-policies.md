---
seo-title: Almacenamiento seguro de directivas
title: Almacenamiento seguro de directivas
uuid: b1ac236f-6637-46d4-8405-a819d6093314
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Almacenamiento seguro de directivas{#securely-storing-policies}

El SDK de Adobe Access ofrece una buena flexibilidad en el desarrollo de aplicaciones para su uso en el empaquetado de contenido y la creación de políticas. Al crear estas aplicaciones, es posible que desee permitir que algunos usuarios creen y modifiquen políticas y limitar a otros usuarios de modo que solo puedan aplicar políticas existentes al contenido. Si este es el caso, debe implementar los controles de acceso necesarios para crear cuentas de usuario con diferentes privilegios para la creación de directivas y la aplicación de políticas al contenido.

Las políticas no se firman ni se protegen de ninguna otra forma de modificación hasta que se utilizan en el embalaje. Si le preocupan los usuarios de las herramientas de empaquetado que modifican las políticas, debe considerar la posibilidad de firmar las políticas para asegurarse de que no se puedan modificar.

Para obtener más información sobre la creación de aplicaciones mediante el SDK, consulte la Referencia *de la API de* Adobe Access.
