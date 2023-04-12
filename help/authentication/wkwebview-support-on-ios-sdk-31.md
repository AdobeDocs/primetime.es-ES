---
title: Compatibilidad con WKWebView en el SDK para iOS 3.1+
description: Compatibilidad con WKWebView en el SDK para iOS 3.1+
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Compatibilidad con WKWebView en el SDK para iOS 3.1+ {#wkwebview-support-on-ios-sdk-3.1}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>

**Debido a que Apple dejó de utilizar UIWebView en iOS, se ha actualizado el SDK 3.1 de iOS con compatibilidad con WKWebView.**

## Compatibilidad {#compatibility}

A partir de la versión 3.1 del SDK para iOS, los implementadores ahora pueden utilizar WKWebView o UIWebView de forma intercambiable. Dado que Apple deja de utilizar UIWebView, las aplicaciones deben migrar a WKWebView para evitar problemas con futuras versiones de iOS.

Tenga en cuenta que la migración implicaría simplemente cambiar la clase UIWebView por WKWebView, no hay trabajo específico por hacer con AccessEnabler de Adobe.

## Problemas conocidos {#known-issues}

AccessEnabler de Adobe usó una instancia interna oculta de UIWebView para realizar &quot;[autenticación pasiva](/help/authentication/sso-passive-authn.md)&quot; para algunos MVPD. El flujo &quot;pasivo&quot; era útil para los MVPD que requieren autenticación para cada id de solicitante y, a partir de este flujo, beneficiaba a los programadores que utilizaban el mismo id de equipo en varias aplicaciones de iOS para simular una experiencia de SSO (SSO de Adobe). Actualmente, esta función la utiliza un número limitado de MVPD.

La función utilizaba un comportamiento de UIWebView que permitía a Adobe capturar las cookies de autenticación y reproducirlas durante el flujo &quot;pasivo&quot;. WKWebView presenta una seguridad más fuerte que impide que el Adobe capture las cookies configuradas en el inicio de sesión y las vuelva a reproducir utilizando una instancia oculta de WKWebView. Debido a esta mejora de la seguridad y considerando que el flujo &quot;pasivo&quot; solo benefició a un conjunto muy limitado de MVPD en un escenario de implementación muy específico (varias aplicaciones que usan el mismo id de equipo), Adobe eliminó la función de &quot;autenticación pasiva&quot; para MVPD que usan webviews para autenticarse.

La función sigue presente para los MVPD configurados para utilizar SFSafariViewController, pero tenga en cuenta que en este caso la autenticación &quot;pasiva&quot; será visible para el usuario, ya que SFSafariViewController no se puede usar de forma &quot;oculta&quot;.
