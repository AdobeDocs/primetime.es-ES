---
title: SSO en iOS al utilizar el Habilitador de acceso de autenticación de Primetime
description: SSO en iOS al utilizar el Habilitador de acceso de autenticación de Primetime
exl-id: 882f0abb-2e6e-461d-a375-3ab410991935
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---

# SSO en iOS al utilizar el Habilitador de acceso de autenticación de Primetime {#sso-on-ios-when-using-the-primetime-authentication-access-enabler}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

</br>

## Información general

El inicio de sesión único (SSO) entre aplicaciones con autenticación Primetime funciona de diferentes maneras según el sistema operativo subyacente.

Este documento se dirige a **SSO en iOS**, al utilizar la autenticación de Adobe Primetime **Habilitador de acceso**.

**Habilitador de acceso** **1,10** es la última versión del SDK nativo de iOS para autenticación de Adobe Primetime. El Adobe recomienda encarecidamente pasar a esta versión en lugar de quedarse con una versión anterior. Si utiliza una versión anterior del Habilitador de acceso, puede descargar la versión más reciente [aquí](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library).

El SSO en iOS viene determinado por las siguientes condiciones:

- Las aplicaciones deben utilizar el mismo **almacenamiento de tokens** (en forma de mesa de trabajo personalizada que crea el Habilitador de acceso).
- Las aplicaciones deben generar lo mismo **ID de dispositivo** (Access Enabler calcula el ID del dispositivo en función de la dirección de MAC o el IDFV, según la versión del sistema operativo).

## Comportamiento

El comportamiento de SSO es el siguiente:

- **iOS 6 y versiones posteriores**: SSO funciona automáticamente entre aplicaciones desarrolladas por el mismo equipo o por equipos diferentes. El ID del dispositivo se calcula en función de la dirección de MAC (el mismo valor se genera en todas las aplicaciones) y el área de almacenamiento es común a todas las aplicaciones (la mesa de trabajo personalizada se puede compartir entre las aplicaciones en iOS 6 y versiones posteriores).
   - **Importante:** Tenga en cuenta que la versión 1.9.4 del SDK para iOS tiene [se ha aumentado el objetivo mínimo de implementación de iOS a iOS 7.](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library) 
- **iOS 7 y versiones posteriores**: SSO funcionará en las siguientes condiciones:

1. Las aplicaciones se publican con el mismo perfil de distribución de Apple o perfiles que pertenecen al mismo equipo. Esta es la única manera en que las aplicaciones comparten paneles de trabajo personalizados en iOS 7 y versiones posteriores. En todos los demás casos, la mesa de trabajo se coloca en una zona protegida por aplicación. Desde [*https://developer.apple.com/library/IOs/releasenotes/General/RN-iOSSDK-7.0/index.html*](https://developer.apple.com/library/ios/releasenotes/General/RN-iOSSDK-7.0/index.html): \+\[UIPasteboardPasteboardWithName:create:\] y +\[UIPasteboard pasteboardWithUniqueName\] ahora permiten que el nombre dado sea único para permitir que solo las aplicaciones del mismo grupo de aplicaciones tengan acceso a la mesa de trabajo. Si el desarrollador intenta crear una mesa de trabajo con un nombre que ya existe y no forma parte del mismo grupo de aplicaciones, obtendrá su propia mesa de trabajo única y privada. Tenga en cuenta que esto no afecta al sistema, a los paneles de trabajo que se proporcionan, a las herramientas generales y a los buscadores.

1. Las aplicaciones tienen el mismo prefijo de ID de paquete (todos los componentes excepto el último). Solo las aplicaciones que comparten el mismo prefijo de ID de paquete calcularán el mismo IDFV. Desde [*https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice\_Class/index.html\#//apple\_ref/occ/instp/UIDevice/identifierForVendor*](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice_Class/index.html#//apple_ref/occ/instp/UIDevice/identifierForVendor): en IOS 7, se utilizan todos los componentes del paquete excepto el último componente para generar el ID de proveedor. Si el ID de paquete solo tiene un componente, se utiliza el ID de paquete completo.

Ahora vamos a centrarnos en la **&#39;iOS 7 y versiones posteriores&#39;** , ya que es el más frecuente para los usuarios reales:

Ambas condiciones (compartir un perfil del mismo equipo de desarrollo y tener un prefijo de identificador de paquete común) son condiciones obligatorias para SSO.

Estas son las combinaciones posibles y sus resultados:

- **Perfiles del mismo equipo y el mismo prefijo de ID de paquete**: las aplicaciones compartirán el mismo almacenamiento de mesa de trabajo y tendrán el mismo ID de dispositivo (IDFV). Un usuario solo tendrá que autenticarse una vez (en la primera aplicación utilizada) y el estado de autenticación se compartirá entre todas las demás aplicaciones. Flujo de ejemplo:

1. El usuario abre la aplicación A (con ID de paquete) *com.x.y.AppA*) y no está autenticado
1. El usuario realiza la autenticación en la aplicación A
1. El usuario abre la aplicación B (con ID de paquete) *com.x.y.AppB*) y se autentica automáticamente compartiendo los datos de asignación de derechos de la aplicación A (del paso 2)
1. El usuario abre la aplicación A y sigue estando autenticado (desde el paso 2)

 

- **Perfiles del mismo equipo, pero prefijos de ID de paquete diferentes**: las aplicaciones compartirán el mismo almacenamiento de mesa de trabajo, pero tendrán diferentes ID de dispositivo (IDFV). Un usuario deberá autenticarse una vez por cada aplicación. Flujo de ejemplo:

1. El usuario abre la aplicación A (con ID de paquete) *com.x.y.AppA*) y no está autenticado
1. El usuario realiza la autenticación en la aplicación A
1. El usuario abre la aplicación B (con ID de paquete) *com.z.AppB*) y Access Enabler detecta el token obtenido por la primera aplicación (porque el almacenamiento está compartido), pero no intentará utilizarlo mediante SSO debido a que los ID de dispositivo son diferentes
1. El usuario realiza la autenticación en la aplicación B
1. El usuario abre la aplicación A y sigue estando autenticado (desde el paso 2)

 

- **Perfiles de diferentes equipos (el ID de paquete no es relevante en este escenario)**: las aplicaciones tendrán diferentes almacenamientos de mesa de trabajo y el SSO se deshabilitará entre ellos. Un usuario deberá autenticarse una vez por cada aplicación y las sesiones de autenticación permanecerán persistentes al cambiar entre aplicaciones. Flujo de ejemplo:


1. El usuario abre la aplicación A y no está autenticado
1. El usuario realiza la autenticación en la aplicación A
1. El usuario abre la aplicación B y no está autenticado
1. El usuario realiza la autenticación en la aplicación B
1. El usuario abre la aplicación A y se autentica (desde el paso 2)
1. El usuario abre la aplicación B y se autentica (desde el paso 4)

**Nota:** Tenga en cuenta que las condiciones anteriores para SSO son aplicables al instalar aplicaciones a través de **Apple App Store**. Si las aplicaciones se implementan en un simulador (donde no se aplica la firma de aplicaciones), se instalan con Xcode o se distribuyen a través de un perfil ad hoc, puede obtener resultados diferentes.

**Importante:** Nota (**con respecto a AccessEnabler v1.8**): El segundo escenario descrito anteriormente (perfiles del mismo equipo, pero con prefijos de ID de paquete diferentes) creará una experiencia de usuario muy desagradable para los usuarios de **AccessEnabler v1.8** en todas las aplicaciones desarrolladas por el mismo equipo (empresa de medios). Se cerrará la sesión del usuario automáticamente al realizar la transición entre aplicaciones de la misma empresa de medios, por lo que los desarrolladores de aplicaciones deben tener cuidado al decidir el ID del paquete y el perfil de distribución. El escenario exacto en este caso se presenta a continuación:

Las aplicaciones compartirán el mismo almacenamiento de mesa de trabajo, pero tendrán ID de dispositivo (IDFV) diferentes. Un usuario deberá autenticarse una vez por cada aplicación, **pero las sesiones de autenticación se borrarán al cambiar entre aplicaciones**. Flujo de ejemplo:

1. El usuario abre la aplicación A (con ID de paquete) *com.x.y.AppA*) y no está autenticado
1. El usuario realiza la autenticación en la aplicación A
1. El usuario abre la aplicación B (con ID de paquete) *com.z.AppB*) y el activador de acceso (mecanismo de seguridad que detecta un conflicto entre el ID de dispositivo calculado actualmente en la aplicación B y el que se almacena en los tokens de derecho creados por la aplicación A) borra automáticamente los datos de derechos creados por la aplicación A
1. El usuario realiza la autenticación en la aplicación B
1. El usuario abre la aplicación A, y el activador de acceso borra automáticamente los datos de derechos creados por la aplicación B (mecanismo de seguridad que detecta un conflicto entre el ID de dispositivo calculado actualmente en la aplicación A y el almacenado en los tokens de derechos creados por la aplicación B)
