---
title: SSO en iOS al utilizar el activador de acceso de autenticación de Primetime
description: SSO en iOS al utilizar el activador de acceso de autenticación de Primetime
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---


# SSO en iOS al utilizar el activador de acceso de autenticación de Primetime {#sso-on-ios-when-using-the-primetime-authentication-access-enabler}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>

## Información general

El inicio de sesión único (SSO) entre aplicaciones con autenticación de Primetime funciona de diferentes maneras según el sistema operativo subyacente.

Esta dirección de documento **SSO en iOS**, al utilizar la autenticación de Adobe Primetime **Access Enabler**.

**Access Enabler** **1,10** es la última versión del SDK nativo de iOS de autenticación de Adobe Primetime. Adobe recomienda que pase a esta versión en lugar de quedarse con una versión anterior. Si utiliza una versión anterior de Access Enabler, puede descargar la versión más reciente [here](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library).

SSO en iOS está dictado por las siguientes condiciones:

- Las aplicaciones deben utilizar el mismo **almacenamiento de token** (en forma de tablero de trabajo personalizado creado por Access Enabler).
- Las aplicaciones deben generar lo mismo **ID del dispositivo** (Access Enabler calcula el ID del dispositivo en función de la dirección de MAC o el IDFV, según la versión del sistema operativo).

## Comportamiento

El comportamiento de SSO es el siguiente:

- **iOS 6 y versiones posteriores**: SSO funciona automáticamente entre aplicaciones desarrolladas por el mismo equipo o por distintos equipos. El ID del dispositivo se calcula en función de la dirección de MAC (el mismo valor se produce en todas las aplicaciones) y el área de almacenamiento es común a todas las aplicaciones (el panel de control personalizado se puede compartir en todas las aplicaciones de iOS 6 y versiones posteriores).
   - **Importante:** Tenga en cuenta que la versión 1.9.4 del SDK para iOS tiene [se ha aumentado el objetivo mínimo de implementación de iOS a iOS 7.](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library) 
- **iOS 7 y superior**: SSO funcionará en las siguientes condiciones:

1. Las aplicaciones se publican con el mismo perfil de distribución de Apple o perfiles que pertenecen al mismo equipo. Esta es la única forma en que las aplicaciones comparten paneles personalizados en iOS 7 y superior. En todos los demás escenarios, la mesa de trabajo se fija por aplicación. De [*https://developer.apple.com/library/IOs/releasenotes/General/RN-iOSSDK-7.0/index.html*](https://developer.apple.com/library/ios/releasenotes/General/RN-iOSSDK-7.0/index.html): \+\[UIPasteboard pasteboardWithName:create:\] y +\[UIPasteboard pasteboardWithUniqueName\] ahora hacen único el nombre dado para permitir que solo las aplicaciones del mismo grupo de aplicaciones tengan acceso al panel de control. Si el desarrollador intenta crear un tablero con un nombre que ya existe y que no forma parte del mismo grupo de aplicaciones, obtendrá su propia mesa de trabajo privada y única. Tenga en cuenta que esto no afecta al sistema proporcionado en los tableros, generales y de búsqueda.

1. Las aplicaciones tienen el mismo prefijo de ID de paquete (todos los componentes excepto el último). Solo las aplicaciones que comparten el mismo prefijo de ID de paquete calcularán el mismo IDFV. De [*https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice\_Class/index.html\#//apple\_ref/occ/instp/UIDevice/identifierForVendor*](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice_Class/index.html#//apple_ref/occ/instp/UIDevice/identifierForVendor): En IOS 7, todos los componentes del paquete excepto el último componente se utilizan para generar el ID de proveedor. Si el ID de paquete solo tiene un componente único, se utiliza el ID de paquete completo.

Centrémonos ahora en el **&#39;iOS 7 y posteriores&#39;** , ya que es el más frecuente para los usuarios reales:

Ambas condiciones (compartir un perfil del mismo equipo de desarrollo y tener un prefijo de identificador de paquete común) son condiciones obligatorias para SSO.

Estas son las combinaciones posibles y sus resultados:

- **Perfiles del mismo equipo y el mismo prefijo de ID de paquete**: las aplicaciones compartirán el mismo almacenamiento en la mesa de trabajo y tendrán el mismo ID de dispositivo (IDFV). Un usuario solo tendrá que autenticarse una vez (en la primera aplicación utilizada) y el estado de autenticación se compartirá entre todas las demás aplicaciones. Flujo de ejemplo:

1. El usuario abre la aplicación A (con ID de paquete) *com.x.y.AppA*) y no está autenticado
1. El usuario realiza la autenticación en la aplicación A
1. El usuario abre la aplicación B (con ID de paquete) *com.x.y.AppB*) y se autentica automáticamente al compartir los datos de asignación de derechos de la aplicación A (desde el paso 2)
1. El usuario abre la aplicación A y sigue autenticado (desde el paso 2)

 

- **Perfiles del mismo equipo pero diferentes prefijos de ID de paquete**: las aplicaciones compartirán el mismo almacenamiento en la mesa de trabajo, pero tendrán ID de dispositivo (IDFV) diferentes. Un usuario deberá autenticarse una vez por cada aplicación. Flujo de ejemplo:

1. El usuario abre la aplicación A (con ID de paquete) *com.x.y.AppA*) y no está autenticado
1. El usuario realiza la autenticación en la aplicación A
1. El usuario abre la aplicación B (con ID de paquete) *com.z.AppB*) y Access Enabler detecta el token obtenido por la primera aplicación (porque el almacenamiento se comparte), pero no intenta utilizarlo mediante SSO debido a los distintos ID de dispositivo
1. El usuario realiza la autenticación en la aplicación B
1. El usuario abre la aplicación A y sigue autenticado (desde el paso 2)

 

- **Perfiles de diferentes equipos (el ID de paquete no es relevante en este escenario)**: las aplicaciones tendrán diferentes almacenamientos de mesa de trabajo y SSO se deshabilitará entre ellas. Un usuario deberá autenticarse una vez por cada aplicación y las sesiones de autenticación permanecerán persistentes al cambiar entre aplicaciones. Flujo de ejemplo:


1. El usuario abre la aplicación A y no está autenticado
1. El usuario realiza la autenticación en la aplicación A
1. El usuario abre la aplicación B y no está autenticado
1. El usuario realiza la autenticación en la aplicación B
1. El usuario abre la aplicación A y está autenticado (desde el paso 2)
1. El usuario abre la aplicación B y está autenticado (desde el paso 4)

**Nota:** Tenga en cuenta que las condiciones anteriores para SSO son aplicables cuando se instalan aplicaciones a través del **Apple App Store**. Si las aplicaciones se implementan en un simulador (donde no se aplica la firma de aplicaciones), se instalan con Xcode o se distribuyen mediante un perfil ad hoc, es posible que se obtengan resultados diferentes.

**Importante:** Nota (**con respecto a AccessEnabler v1.8**): El segundo escenario descrito anteriormente (perfiles del mismo equipo pero distintos prefijos de ID de paquete) creará una experiencia de usuario muy desagradable para los usuarios del **AccessEnabler v1.8** entre aplicaciones desarrolladas por el mismo equipo (empresa multimedia). Se cerrará la sesión del usuario automáticamente al realizar la transición entre aplicaciones de la misma empresa de medios, por lo que los desarrolladores de aplicaciones deben tener cuidado al decidir el ID del paquete y el perfil de distribución. El escenario exacto en este caso se presenta a continuación:

Las aplicaciones compartirán el mismo almacenamiento en la mesa de trabajo, pero tendrán ID de dispositivo (IDFV) diferentes. Un usuario deberá autenticarse una vez por cada aplicación, **pero las sesiones de autenticación se borran al cambiar entre aplicaciones**. Flujo de ejemplo:

1. El usuario abre la aplicación A (con ID de paquete) *com.x.y.AppA*) y no está autenticado
1. El usuario realiza la autenticación en la aplicación A
1. El usuario abre la aplicación B (con ID de paquete) *com.z.AppB*) y los datos de asignación de derechos creados por la aplicación A los borra automáticamente Access Enabler (mecanismo de seguridad que detecta un choque entre el ID de dispositivo actualmente calculado en la aplicación B y el que está almacenado en los tokens de asignación de derechos (creados por la aplicación A)
1. El usuario realiza la autenticación en la aplicación B
1. El usuario abre la aplicación A y el activador de acceso (mecanismo de seguridad que detecta un choque entre el ID de dispositivo computado actualmente en la aplicación A y el almacenado en los tokens de asignación de derechos (creado por la aplicación B) elimina automáticamente los datos de asignación de derechos creados por la aplicación B

