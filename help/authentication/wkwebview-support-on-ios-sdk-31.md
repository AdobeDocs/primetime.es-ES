---
title: Compatibilidad con WKWebView en el SDK 3.1+ de iOS
description: Compatibilidad con WKWebView en el SDK 3.1+ de iOS
exl-id: 90062be0-1a0a-44ae-8d8e-f4d97a92b17a
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Compatibilidad con WKWebView en el SDK 3.1+ de iOS {#wkwebview-support-on-ios-sdk-3.1}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

</br>

**Debido a que Apple ha desaprobado UIWebView en iOS, hemos actualizado el SDK 3.1 de iOS con compatibilidad con WKWebView.**

## Compatibilidad {#compatibility}

A partir de la versión 3.1 del SDK para iOS, los implementadores pueden utilizar ahora WKWebView o UIWebView de forma intercambiable. Dado que UIWebView está obsoleto en Apple, las aplicaciones deben migrar a WKWebView para evitar problemas con futuras versiones de iOS.

Tenga en cuenta que la migración implicaría simplemente cambiar la clase UIWebView con WKWebView, no hay ningún trabajo específico por hacer en relación con el AccessEnabler del Adobe.

## Problemas conocidos {#known-issues}

AccessEnabler de Adobe utilizó una instancia de UIWebView interna oculta para realizar &quot;[autenticación pasiva](/help/authentication/sso-passive-authn.md)&quot; para ciertas MVPD. El flujo &quot;pasivo&quot; resultó útil para las MVPD que requieren autenticación para cada ID de solicitante y, a partir de este flujo, se beneficiaron los programadores que utilizaron el mismo ID de equipo en varias aplicaciones de iOS para simular una experiencia SSO (Adobe SSO). Actualmente, esta función la utilizan un número limitado de MVPD.

La función utilizaba un comportamiento de UIWebView que permitía al Adobe capturar las cookies de autenticación y reproducirlas durante el flujo &quot;pasivo&quot;. WKWebView presenta una seguridad más sólida que evita que el Adobe capture las cookies configuradas al iniciar sesión y las reproduzca utilizando una instancia oculta de WKWebView. Debido a esta mejora de la seguridad y teniendo en cuenta que el flujo &quot;pasivo&quot; solo beneficiaba a un conjunto muy limitado de MVPD en un escenario de implementación muy específico (varias aplicaciones que utilizan el mismo ID de equipo), Adobe eliminó la función de &quot;autenticación pasiva&quot; para MVPD que utilizan vistas web para autenticarse.

La función sigue presente para las MVPD configuradas para utilizar SFSafariViewController, pero tenga en cuenta que en este caso la autenticación &quot;pasiva&quot; será visible para el usuario, ya que SFSafariViewController no se puede utilizar de forma &quot;oculta&quot;.
