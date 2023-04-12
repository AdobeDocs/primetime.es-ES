---
title: Beneficios del uso del parámetro deviceType sin cliente en las métricas de autenticación de Primetime
description: Beneficios del uso del parámetro deviceType sin cliente en las métricas de autenticación de Primetime
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---


# Beneficios del uso del parámetro deviceType sin cliente en las métricas de autenticación de Primetime {#benefits-of-using-the-clientless-devicetype-parameter-in-primetime-authentication-metrics}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>

## Contexto

Aunque es opcional, el parámetro `deviceType` de la API sin cliente, cuando está presente, se utiliza en las métricas de autenticación de Primetime que se exponen a través de [Supervisión del servicio de derechos](/help/authentication/entitlement-service-monitoring-overview.md).

Considerando que la conexión entre `deviceType` y su **ventajas** en las métricas de autenticación de Primetime no se indicaron inicialmente, el ámbito de esta nota técnica es agregar más información sobre ellas.

## Explicación

La variable `deviceType` estaba presente en la API sin cliente desde la primera versión, pero sus implicaciones en las métricas de autenticación de Primetime se añadieron en una versión más reciente.



>[!IMPORTANT]
>
>Si el parámetro `deviceType` está correctamente configurado y tiene lo siguiente **beneficio** en la supervisión del servicio de derechos: ofrece métricas que [desglosado por tipo de dispositivo](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) al usar Clientless, de modo que se puedan realizar diferentes tipos de análisis para, por ejemplo, Roku, Apple TV, Xbox, etc.


Para obtener más información sobre la API de supervisión del servicio de derechos, consulte la [árbol de profundización,](/help/authentication/entitlement-service-monitoring-api.md#drill-down_tree) que ilustra el [dimensiones](/help/authentication/entitlement-service-monitoring-overview.md#esm_dimensions) (recursos) disponibles en ESM 2.0.

>[!NOTE]
>
>El contenido de esta nota técnica también se agregó al [API sin cliente](#clientless_device_type).




## Implementación

Para beneficiarse plenamente de las métricas de autenticación de Primetime, existen dos tipos de [API sin cliente](#web_srvs_summary) que se están utilizando actualmente y que necesitan tener la `deviceType` configurado:

1. API que tienen `regcode` como parámetro obligatorio y utilizará la variable `deviceType` que se estableció al crear el `regcode`, con la siguiente llamada de API:
   - [\&lt;reggie _fqdn=&quot;&quot;>/reggie/v1/{requestorId}/regcode](#reg_serv)

1. Las API que tienen la variable `deviceType` como parámetro opcional:
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/checkauthn](#check_authn_token)
   - [&lt;span class=&quot;s1&quot;>](#retrieve_authn_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/authorization](#init_authz)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/authz](#retrieve_authz_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/media](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/mediatoken](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/preauthorization](#PreAuthZ_Resources)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/logout](#init_logout)

Nuestra recomendación es usar la variable `deviceType` y pase el tipo de dispositivo sin cliente correcto para todas las API.


