---
title: Ruta de actualización de AccessEnabler iOS/tvOS 3.7.0
description: Ruta de actualización de AccessEnabler iOS/tvOS 3.7.0
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Ruta de actualización de AccessEnabler iOS/tvOS 3.7.0 {#accessenabler-iostvos-370-upgrade-path}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>

Cambios en el almacenamiento del llavero desde el [nueva versión de AccessEnabler 3.7.0](/help/authentication/authn-rn-ios-tvos-370.md) no son compatibles con la implementación de almacenamiento de llaveros de la versión inferior a 3.7.0 de AccessEnabler.

La ruta de actualización para una aplicación que adopta la nueva versión 3.7.0 de AccessEnabler migrará todos los tokens de versiones anteriores del almacenamiento de Keychain. Por lo tanto, los usuarios finales **no deben experimentar pérdida de sesiones de autenticación/autorización** durante el proceso de actualización del marco de AccessEnabler.

## Limitaciones conocidas

Algunos implementadores pueden encontrar algunas limitaciones, que se describen a continuación.


1. El SSO regular (Adobe) no funcionará entre una aplicación que utilice la versión 3.7.0 de AccessEnabler y una aplicación que utilice versiones inferiores a 3.7.0 de AccessEnabler, incluso para aplicaciones desarrolladas por el mismo proveedor.

   - **Importante:**
      - El SSO de nivel de sistema (Apple) no se verá afectado.
      - El SSO regular (Adobe) seguirá funcionando si ambas aplicaciones son desarrolladas por el mismo proveedor y utilizan versiones de AccessEnabler inferiores a 3.7.0.
      - El SSO regular (Adobe) funcionará si el mismo proveedor desarrolla ambas aplicaciones y utiliza la versión 3.7.0 de AccessEnabler.

1. En la situación de reducir una aplicación que utilice la versión 3.7.0 de AccessEnabler a una versión inferior de AccessEnabler, no se migrarán los tokens nuevos generados. Por lo tanto, los usuarios finales pueden experimentar la pérdida de sesiones de autenticación/autorización sin esperarla.

   - **Importante:**
      - Los usuarios finales autenticados a través del SSO a nivel de sistema (Apple) no se verán afectados.
      - Los usuarios finales que ya estaban autenticados antes de actualizar a la nueva aplicación mediante AccessEnabler versión 3.7.0 no se verán afectados.

1. En la situación de reducir una aplicación que utilice la versión 3.7.0 de AccessEnabler a una versión inferior de AccessEnabler, no se reconocerán los tokens eliminados. Por lo tanto, los usuarios finales pueden experimentar la presencia de sesiones de autenticación/autorización sin esperarla.
