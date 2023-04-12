---
title: Habilitación de los servicios de derecho de Primetime para un programador en Xbox 360 y XboxOne sin clientes
description: Habilitación de los servicios de derecho de Primetime para un programador en Xbox 360 y XboxOne sin clientes
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# Habilitación de los servicios de derecho de Primetime para un programador en Xbox 360 y XboxOne sin clientes {#enabling-primetime-entitlement-services-for-a-programer-on-xbox-360-and-xboxone-clientless}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.




1. El programador crea un ticket de Zendesk para habilitar la solución para clientes sin autenticación Xbox 360/One para Primetime proporcionando la siguiente información:

   1. Plataforma: Por ejemplo, Xbox 360, Xbox One

   1. ID del solicitante: Por ejemplo: netgeo, CNN, etc.

1. Adobe creará certificados X509 y configurará la clave privada y la contraseña en su extremo.

1. Adobe proporcionará el certificado público (de certificado X509) a Programer en el ticket o por correo electrónico.

1. El programador tendría que instalar ese certificado público en el portal GDNP para la aplicación registrada en Microsoft.

1. El programador solicitará entonces el JWT (token web de Java) o el token STS para XboxOne o 360 respectivamente del servicio Xbox Live de Microsoft, que se cifrará usando el certificado público X509 que se proporciona en el paso 3.

1. Estos son los tokens que contienen el deviceId único para dispositivos Xbox. Incluya el token (JWT o STS) en el encabezado Autorización utilizando un parámetro &quot;x&quot; como se muestra a continuación:

   1. Para Xbox 360, el token XSTS debe estar codificado en Base64 antes de enviar a la autenticación de Primetime pay-TV.
   1. Para Xbox One, el JWT ya está codificado correctamente, por lo que no debería producirse ninguna codificación adicional. 

1. Todas las llamadas de API del dispositivo Xbox deben contener el encabezado de autorización con el token mencionado anteriormente en el parámetro x.

 

>[!NOTE]
>
>La Xbox en particular tiene algunos requisitos únicos relacionados con la firma digital. El ID del dispositivo de la consola XBox se incluye en el token XSTS.  Para Xbox 360, esta es una afirmación de SAML cifrada; para Xbox One, esto es un JWT cifrado. La aplicación de consola XBox envía todo el token XSTS a la autenticación de Primetime pay-TV. La autenticación de Primetime pay-TV descifra el token mediante su clave pública, analiza el token y extrae el deviceId de él.

>[!NOTE]
>
>Debido a la gran longitud del token XSTS, la consola XBox tiene una limitación técnica: no puede enviar el token como un parámetro de GET HTTP a las API de autenticación de pago-TV de Primetime. Para solucionarlo, la autenticación de Primetime pay-TV permite enviar el token XSTS como parte del encabezado HTTP &quot;Autorización&quot; al llamar a las API. El token XSTS debe cifrarse con la clave pública del certificado X.509 emitido al programador desde la autenticación Primetime pay-TV. La autenticación de Primetime pay-TV almacena la clave privada asociada y la utiliza para descifrar el token XSTS y extraer el deviceId de él.  


