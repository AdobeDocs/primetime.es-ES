---
title: Habilitar los servicios de derechos de Primetime para un programador en Xbox 360 y XboxOne sin cliente
description: Habilitar los servicios de derechos de Primetime para un programador en Xbox 360 y XboxOne sin cliente
exl-id: ff7254de-9ea4-4c27-a186-d1c2eea12222
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# Habilitar los servicios de derechos de Primetime para un programador en Xbox 360 y XboxOne sin cliente {#enabling-primetime-entitlement-services-for-a-programer-on-xbox-360-and-xboxone-clientless}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.




1. El programador crea un ticket de Zendesk para habilitar Xbox 360/One para la solución cliente de autenticación de Primetime al proporcionar la siguiente información:

   1. Plataforma: por ejemplo, Xbox 360 o Xbox One

   1. ID del solicitante: p. ej. netgeo, CNN, etc.

1. El Adobe creará certificados X509 y configurará la clave privada y la contraseña al final.

1. El Adobe proporcionará el certificado público (de certificado X509) al programador en el ticket o por correo electrónico.

1. El programador tendría que instalar ese certificado público en el portal del PNG para la aplicación registrada en Microsoft.

1. El programador solicitará el token JWT (token web de Java) o STS para XboxOne o 360 respectivamente desde el servicio Xbox Live de Microsoft, que se cifraría con el certificado público X509 proporcionado en el paso 3.

1. Estos son los tokens que contienen el ID de dispositivo único para dispositivos Xbox. Incluya el token (JWT o STS) en el encabezado de Autorización utilizando un parámetro &quot;x&quot; como se muestra a continuación:

   1. Para Xbox 360, el token XSTS debe estar codificado en Base64 antes de enviarlo a la autenticación de televisión de pago de Primetime.
   1. Para Xbox One, el JWT ya está codificado correctamente, por lo que no debería producirse ninguna codificación adicional.

1. Todas las llamadas de API desde el dispositivo Xbox deben contener el encabezado de autorización con el token mencionado anteriormente en el parámetro x.



>[!NOTE]
>
>La Xbox en particular tiene algunos requisitos únicos relacionados con la firma digital. El ID de dispositivo de la consola de XBox se incluye en el token XSTS.  Para Xbox 360, se trata de una afirmación de SAML cifrada; para Xbox One, se trata de un JWT cifrado. La aplicación de consola XBox envía todo el token XSTS a la autenticación de televisión de pago de Primetime. La autenticación de Primetime Pay-TV descifra el token mediante su clave pública, lo analiza y extrae el deviceId de él.

>[!NOTE]
>
>Debido a la gran longitud del token XSTS, la consola de XBox tiene una limitación técnica: no puede enviar el token como parámetro de GET HTTP a las API de autenticación de TV de pago de Primetime. Para solucionarlo, la autenticación de TV de pago de Primetime permite enviar el token XSTS como parte del encabezado HTTP &quot;Autorización&quot; al llamar a las API. El token XSTS debe cifrarse con la clave pública del certificado X.509 emitido al programador desde la autenticación de televisión de pago de Primetime. La autenticación de TV paga de Primetime almacena la clave privada asociada y la utiliza para descifrar el token XSTS y extraer el deviceId de él.
