---
description: Personalice la implementación de referencia para integrar la autenticación de Adobe Primetime en su entorno de producción.
title: Integrar la autenticación de Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# Integrar la autenticación de Primetime {#integrate-primetime-authentication}

Personalice la implementación de referencia para integrar la autenticación de Adobe Primetime en su entorno de producción.

La integración Implementación de referencia del servicio de autenticación de Primetime funciona de forma predeterminada como demostración. Sin embargo, para utilizar la integración en un reproductor listo para la producción, debe implementar las siguientes personalizaciones:

1. Habilite o deshabilite los flujos de derechos.

   El `EntitlementManager` Primero debe inicializar y obtener una instancia del SDK de autenticación de Primetime para habilitarlo. Si la variable `EntitlementManager` no inicializa esta biblioteca, se deshabilitará el administrador.
1. Habilite la `EntitlementManger`, desde la clase de aplicación principal:

   ```java
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. Utilice el `ManagerFactory` para obtener una instancia de `EntitlementManager`.

   Siempre debe utilizar la variable `ManagerFactory` para obtener una instancia de `EntitlementManager`, como el `ManagerFactory` mantiene una sola instancia de EntitlementManager para la aplicación. Nunca cree una instancia de `EntitlementManager` o `EntitlementManagerOn` mediante sus constructores.

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   El `ManagerFactory` devuelve una instancia de `EntitlementManagerOn`, con los flujos de derechos habilitados, si anteriormente ha llamado a `EntitlementManager.initializeAccessEnabler`. Si no llama primero a `EntitlementManager.initializeAccessEnabler`y, a continuación, el `ManagerFactory` devolverá una instancia de `EntitlementManager`, con los flujos de derechos desactivados. 1. Configure el ID del solicitante.

   La implementación de referencia viene preconfigurada con el ID de solicitante de prueba establecido en: &quot;REF&quot;. Puede utilizar este ID de solicitante para probar la aplicación. Cuando esté listo para usar el ID de solicitante que le proporcionó su representante de autenticación de Primetime, actualice el [!DNL res/values/strings.xml] con su ID de solicitante.

   ```xml
   <!-- Programmer Requestor ID, change to ID provided by your Adobe  
        Primetime pay-TV pass representative --> 
   <string name="adobepass_requestor_id">REF</string> 
   
   <!-- Adobe Primetime pay-TV pass service provider endpoint for production 
        environment --> 
   <string name="adobepass_sp_url_production">sp.auth.adobe.com</string> 
   
   <!-- Adobe Primetime pay-TV pass service provider endpoint for staging  
        environment --> 
   <string name="adobepass_sp_url_staging">sp.auth-staging.adobe.com</string>
   ```

   Además, es posible que tenga que cambiar las direcciones URL que utiliza la aplicación para conectarse a los servicios de autenticación de Primetime. Estas incluyen las URL del servidor de ensayo y producción de autenticación de Primetime y una URL a un servicio de verificación de tokens. Consulte con su representante de Adobe Primetime para obtener más información. 1. Firme el ID del solicitante.

   Para establecer la identidad del programador dentro del sistema de autenticación de Primetime, el ID de solicitante del programador se envía al sistema de autenticación de Primetime. Como nivel de seguridad adicional, el programador debe firmar el ID del solicitante antes de enviarlo al Adobe. El Adobe recomienda que el programador configure un servicio para firmar el ID del solicitante en una red de confianza.

   La implementación de referencia de Primetime muestra cómo firmar el ID de solicitante, aunque solo tiene fines demostrativos. El Adobe recomienda encarecidamente que el certificado de firma y el código del generador de firmas, en `com.adobe.primetime.reference.crypto`, no debe incluirse en una aplicación de producción. En su lugar, debe moverlo a un servicio de red de confianza.

1. Configure el Entorno del servidor.

   El servicio de autenticación de Primetime se puede ejecutar en dos entornos independientes:

   * Ensayo: el entorno de ensayo se utiliza para probar la aplicación.
   * Producción: el entorno de producción se utiliza para implementaciones activas de la aplicación.

   Los URI se establecen tanto para los entornos de ensayo como de producción mediante la aplicación. Sin embargo, dentro del código debe establecer cuál de ellos utiliza la aplicación. En el `com.adobe.primetime.reference.manager.EntitlementManger` , establezca el `environmentUri` variable a `STAGING_URI` o `PRODUCTION_URI` en función del entorno del servicio de autenticación de Primetime que esté utilizando.

   >[!NOTE]
   >
   >El ID de solicitante proporcionado (&quot;REF&quot;) solo debe utilizarse con el entorno de ensayo.

   `com.adobe.primetime.reference.manager.EntitlementManager`:

   ```java
     // Adobe Primetime authentication service provider endpoint for production environment 
     PRODUCTION_URI = 
         application.getResources().getString(R.string.adobepass_sp_url_production); 
   
     // Adobe Primetime authentication service provider endpoint for staging environment 
     STAGING_URI = 
       application.getResources().getString(R.string.adobepass_sp_url_staging); 
   
     // Set to STAGING_URI when testing against the staging/test environment 
     // Set to PRODUCTION_URI when deploying the application for production use 
     String environmentUri = STAGING_URI; 
   
     // Adobe Primetime authentication service URI used by this application 
     PAYTV_PASS_URI = environmentUri + "/adobe-services"; 
   
     // Token Verification Service URL 
     TVS_URL = "https://" + environmentUri + "/tvs/v1/validate";
   ```

1. Personalice la cuadrícula de selección de MVPD.

   La página de selección del proveedor de contenido muestra una tabla de las nueve MVPD principales que el usuario puede seleccionar. La aplicación extrae las nueve MVPD principales de una lista ordenada dentro de la aplicación que coincide con las MVPD disponibles integradas con el programador en el sistema de autenticación de Primetime. La lista ordenada de las MVPD principales está incrustada en el ID de MVPD dentro del sistema de autenticación de Primetime, no en el nombre para mostrar de MVPD. Es importante verificar que los ID de MVPD de la lista de MVPD principales coincidan con los ID de MVPD integrados con la cuenta del programador, ya que en algunos casos los ID pueden ser diferentes entre integraciones. A continuación se muestra la lista ordenada de MVPD principales que se encuentran en la clase `com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment`.

   ```java
   /* Array of MVPDs to display in a Grid of icons 
   When displaying a grid, only the MVPDs which intersect this array and the 
   ArrayList of all MVPDs are displayed. 
   The array contents are ordered by display preference as only a maximum of 
   MAX_DISPLAY_ICONS are displayed. 
   */ 
   private static final String[] PRIMARY_MVPDS = { 
   "Comcast_SSO",                         // Comcast XFINITY 
   "DTV",                                 // DirectTV 
   "Dish",                                // Dish 
   "TWC",                                 // Time Warner Cable 
   "Cox",                                 // Cox 
   "Charter_Direct",                      // Charter 
   "Verizon",                             // Verizon FiOS 
   "Cablevision",                         // Cablevision Optimum 
   "ATT",                                 // AT&T U-verse 
   "Brighthouse",                         // Brighthouse 
   "Suddenlink",                          // Suddenlink 
   "Mediacom",                            // Mediacom 
   "CableOne",                            // CableOne 
   "WOW",                                 // WOW! 
   "RCN",                                 // RCN 
   "auth_atlanticbb_net",                 // Atlantic Broadband 
   "auth_armstrongmywire_com",            // Armstrong 
   "knology_auth-gateway_net",            // KNOLOGY 
   "serviceelectric_auth-gateway_net",    // Service Electric Cablevision 
   "msauth_midco_net",                    // Midcontinent Communications 
   "auth_metrocast_net",                  // MetroCast 
   "www_websso_mybrctv_com",              // Blue Ridge Communications 
   };
   ```

   La siguiente tabla proporciona un ejemplo de cómo se utiliza la lista ordenada de MVPD principales. La primera columna enumera las MVPD integradas con el programador. La segunda columna es la lista ordenada (abreviada) de MVPD. La tercera columna es la lista de resultados utilizada para mostrar las seis MVPD principales al usuario.

   Este ejemplo utiliza los seis MVPD principales en lugar de los nueve reales solo para mantener el ejemplo simple. Observe cómo la lista de resultados contiene la intersección de las dos primeras listas y tiene el mismo orden que la segunda lista. Además, ten en cuenta que AT&amp;T U-verse no está en la lista final, ya que solo se toman los primeros seis MVPD que coinciden.

| MVPD disponibles | MVPD principales | Se muestran 6 MVPD |
|--- |--- |--- |
| <ol><li>Comcast XFINITY</li><li>TWC</li><li>Mediacom</li><li>RCN</li><li>Plato</li><li>AT&amp;T U-verse</li><li>CableOne</li><li>Faro</li><li>Banda ancha atlántica</li><li>¡GUAU!</li><li>MetroCast</li><li>DirectTV </li><li>Cox</li><li>Cablevision Optimum</li></ol> | <ol><li>Comcast XFINITY</li><li>DirectTV</li><li>Plato</li><li> TWC</li><li>Cox</li><li>Carta</li><li>Verizon FiOS</li><li>Cablevision Optimum</li><li>AT&amp;T U-verse</li></ol> | <ol><li>Comcast XFINITY</li><li>DirectTV</li><li>Plato</li><li>TWC</li><li>Cox</li><li>Cablevision Optimum</li></ol> |
