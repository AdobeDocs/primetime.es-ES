---
description: Personalice la implementación de referencia para integrar la autenticación Adobe Primetime en su entorno de producción.
seo-description: Personalice la implementación de referencia para integrar la autenticación Adobe Primetime en su entorno de producción.
seo-title: Integración de la autenticación Primetime
title: Integración de la autenticación Primetime
uuid: 34cdf1da-261e-462c-a194-4fcb439e5dfb
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Integración de la autenticación Primetime {#integrate-primetime-authentication}

Personalice la implementación de referencia para integrar la autenticación Adobe Primetime en su entorno de producción.

La integración Implementación de referencia del servicio de autenticación Primetime funciona de forma predeterminada como una demostración. Sin embargo, para utilizar la integración en un reproductor listo para la producción, debe implementar las siguientes personalizaciones:

1. Habilitar o deshabilitar los flujos de asignación de derechos.

   Primero `EntitlementManager` debe inicializar y obtener una instancia del SDK de autenticación Primetime para habilitarlo. Si la biblioteca `EntitlementManager` no inicializa esta biblioteca, se desactivará el administrador.
1. Habilite el `EntitlementManger`, desde la clase de aplicación principal:

   ```java
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. Utilice la `ManagerFactory` clase para obtener una instancia de la `EntitlementManager`.

   Siempre debe usar el `ManagerFactory` para obtener una instancia del `EntitlementManager`, ya que el `ManagerFactory` mantiene una sola instancia de EntitlementManager para la aplicación. No cree nunca instancias de las clases `EntitlementManager` o `EntitlementManagerOn` con sus constructores.

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   El `ManagerFactory` devuelve una instancia de `EntitlementManagerOn`, con los flujos de asignación de derechos activados, si ha llamado anteriormente `EntitlementManager.initializeAccessEnabler`. Si no llama primero `EntitlementManager.initializeAccessEnabler`, entonces el `ManagerFactory` devolverá una instancia de `EntitlementManager`, con los flujos de asignación desactivados. 1. Configure el ID del solicitante.

   La implementación de referencia viene preconfigurada con la ID del solicitante de prueba establecida en: &quot;REF&quot;. Puede utilizar este ID de solicitante para probar la aplicación. Cuando esté listo para usar el identificador del solicitante que le proporcionó el representante de autenticación de Primetime, actualice el [!DNL res/values/strings.xml] archivo de la aplicación con el identificador del solicitante.

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

   Además, es posible que tenga que cambiar las direcciones URL que utiliza la aplicación para conectarse a los servicios de autenticación Primetime. Entre ellos se incluyen las direcciones URL del servidor de producción y ensayo de autenticación Primetime y una dirección URL a un servicio de verificación de autentificación de tokens. Consulte a su representante de Adobe Primetime para obtener más información. 1. Firme el ID del solicitante.

   Para establecer la identidad del programador dentro del sistema de autenticación Primetime, el identificador del solicitante del programador se envía al sistema de autenticación Primetime. Como capa adicional de seguridad, el identificador del solicitante debe estar firmado por el programador antes de enviarlo a Adobe. Adobe recomienda que el programador configure un servicio para firmar el ID de solicitante en una red de confianza.

   La implementación de referencia de Primetime muestra cómo firmar el identificador del solicitante, aunque esto se hace únicamente con fines de demostración. Adobe recomienda enfáticamente que el certificado de firma y el código del generador de firmas, en `com.adobe.primetime.reference.crypto`, no se incluyan en una aplicación de producción. En su lugar, debe moverlo a un servicio de red de confianza.

1. Configure el entorno de servidor.

   El servicio de autenticación Primetime se puede ejecutar en dos entornos distintos:

   * Ensayo: el entorno de ensayo se utiliza para probar la aplicación.
   * Producción: el entorno de producción se utiliza para las implementaciones activas de la aplicación.
   Puede establecer los URI para los entornos de ensayo y producción mediante la aplicación, pero debe establecer cuál de ellos utiliza la aplicación dentro del código. En la `com.adobe.primetime.reference.manager.EntitlementManger` clase, establezca la `environmentUri` variable en `STAGING_URI` o `PRODUCTION_URI` en función del entorno de servicio de autenticación Primetime que esté utilizando.

   >[!NOTE]
   >
   >El ID del solicitante (&quot;REF&quot;) proporcionado solo debe usarse con el entorno de ensayo.

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

   La página de selección del proveedor de contenido muestra una tabla de los nueve MVPD principales que el usuario puede seleccionar. La aplicación extrae los nueve MVPD principales de una lista ordenada dentro de la aplicación que coincide con los MVPD disponibles integrados con el Programador en el sistema de autenticación Primetime. La lista ordenada de los MVPD primarios se encuentra en el ID de MVPD dentro del sistema de autenticación Primetime, no en el nombre para mostrar de MVPD. Es importante verificar que los ID de MVPD de la lista principal de MVPD coincidan con los ID de MVPD integrados con la cuenta del programador, ya que en algunos casos los ID pueden ser diferentes en las integraciones. A continuación se muestra la lista ordenada de MVPD principales que se encuentra en la clase `com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment`.

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

   La siguiente tabla proporciona un ejemplo de cómo se utiliza la lista ordenada de MVPD principales. En la primera columna se enumeran los MVPD integrados con el Programador. La segunda columna es la lista ordenada (abreviada) de MVPD. La tercera columna es la lista de resultados que se utiliza para mostrar los seis MVPD principales al usuario.

   En este ejemplo se utilizan los seis MVPD principales en lugar de los nueve reales para mantener el ejemplo sencillo. Observe cómo la lista de resultados contiene la intersección de las dos primeras listas y tiene el mismo orden que la segunda lista. Además, observe que AT&amp;T U-verse no está en la lista final, ya que sólo se toman los primeros seis MVPD coincidentes.

| MVPD disponibles | MVPD principales | Se mostraron 6 MVPD |
|--- |--- |--- |
| <ol><li>XFINITY de Comcast</li><li>TWC</li><li>Mediacom</li><li>RCN</li><li>Dish</li><li>U-verse de AT&amp;T</li><li>CableOne</li><li>Brighthouse</li><li>Banda ancha atlántica</li><li>¡WOW!</li><li>MetroCast</li><li>DirectTV </li><li>Cox</li><li>Cablevision Optimum</li></ol> | <ol><li>XFINITY de Comcast</li><li>DirectTV</li><li>Dish</li><li> TWC</li><li>Cox</li><li>Carta</li><li>Verizon FiOS</li><li>Cablevision Optimum</li><li>U-verse de AT&amp;T</li></ol> | <ol><li>XFINITY de Comcast</li><li>DirectTV</li><li>Dish</li><li>TWC</li><li>Cox</li><li>Cablevision Optimum</li></ol> |
