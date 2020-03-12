---
description: El SDK de Flash Runtime necesita un token firmado para validar que tiene derecho a llamar a la API de TVSDK en el dominio en el que reside la aplicación.
seo-description: El SDK de Flash Runtime necesita un token firmado para validar que tiene derecho a llamar a la API de TVSDK en el dominio en el que reside la aplicación.
seo-title: Cargar el token firmado
title: Cargar el token firmado
uuid: 8760eab3-3d6d-47c6-9aa7-f64f6aa5ddcf
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Cargar el token firmado {#load-your-signed-token}

El SDK de Flash Runtime necesita un token firmado para validar que tiene derecho a llamar a la API de TVSDK en el dominio en el que reside la aplicación.

1. Obtenga un token firmado del representante de Adobe para cada uno de los dominios (donde cada dominio puede ser un dominio específico o un dominio comodín).

       Para obtener un token, proporcione a Adobe el dominio en el que se almacenará o cargará la aplicación o, preferiblemente, el dominio como hash SHA256. A cambio, Adobe le proporciona un token firmado para cada dominio. Estos tokens tienen una de estas formas:
   
   * Un [!DNL .xml] archivo que actúa como token para un único dominio o dominio comodín.

      >[!NOTE]
      >
      >Un token para un dominio comodín cubre ese dominio y todos sus subdominios. Por ejemplo, un token comodín para el dominio también [!DNL mycompany.com] abarcaría [!DNL vids.mycompany.com] y [!DNL private.vids.mycompany.com]; un token comodín para [!DNL vids.mycompany.com] también cubriría [!DNL private.vids.mycompany.com]. *Los tokens de dominio comodín solo son compatibles con ciertas versiones de Flash Player.*

   * Un [!DNL .swf] archivo que contiene información de token para varios dominios (sin incluir caracteres comodín) (único o comodín), que la aplicación puede cargar dinámicamente.

1. Almacene el archivo token en la misma ubicación o dominio que la aplicación.

   De forma predeterminada, TVSDK busca el token en esta ubicación. También puede especificar el nombre y la ubicación del token en `flash_vars` el archivo HTML.
1. Si el archivo de token es un único archivo XML:
   1. Utilice `utils.AuthorizedFeaturesHelper.loadFrom` para descargar los datos almacenados en la dirección URL especificada (el archivo token) y extraer la `authorizedFeatures` información de ella.

      Este paso puede variar. Por ejemplo, es posible que desee realizar la autenticación antes de iniciar la aplicación o que reciba el token directamente desde el sistema de administración de contenido (CMS).

   1. TVSDK distribuye un `COMPLETED` evento si la carga se realiza correctamente o si se produce un `FAILED` evento de otro tipo. Tome las medidas adecuadas cuando detecte cualquiera de los eventos.

      Esto debe realizarse correctamente para que la aplicación proporcione los objetos necesarios `authorizedFeatures` a TVSDK en forma de `MediaPlayerContext`.
   Este ejemplo muestra cómo se puede utilizar un archivo de un solo token [!DNL .xml] .

   ```
   private function loadDirectTokenURL():void { 
       var url:String = constructAuthorizedFeatureTokenURL(); 
       _logger.debug("#onApplicationComplete Loading token from [{0}].", url); 
       _authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       _authorizedFeatureHelper.addEventListener(Event.COMPLETE,  
           onFeatureComplete); 
       _authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR,  
           onFeatureError); 
        _authorizedFeatureHelper.loadFrom(url); 
    }
   ```

1. Si el token es un [!DNL .swf] archivo:
   1. Defina una `Loader` clase para cargar dinámicamente el [!DNL .swf] archivo.
   1. Configure el `LoaderContext` para especificar que la carga se encuentre en el dominio de la aplicación actual, lo que permite que TVSDK elija el token correcto dentro del [!DNL .swf] archivo. Si no `LoaderContext` se especifica, la acción predeterminada de `Loader.load` es cargar el archivo .swf en el dominio secundario del dominio actual.
   1. Escuche el evento COMPLETE, que TVSDK distribuye si la carga se realiza correctamente.

      Escuche también el evento ERROR y tome las medidas adecuadas.
   1. Si la carga es correcta, utilice el `AuthorizedFeaturesHelper` para obtener un `ByteArray` que contenga los datos de seguridad codificados PCKS-7.

      Estos datos se utilizan a través de la API de AVE V11 para obtener la confirmación de autorización de Flash Runtime Player. Si la matriz de bytes no tiene contenido, utilice el procedimiento para buscar un archivo de token de un solo dominio.
   1. Se utiliza `AuthorizedFeatureHelper.loadFeatureFromData` para obtener los datos necesarios de la matriz de bytes.
   1. Descargue el [!DNL .swf] archivo.
   Los siguientes ejemplos muestran cómo se puede utilizar un archivo de varios tokens [!DNL .swf] .

   **Ejemplo de varios tokens 1:**

   ```
   private function onApplicationComplete(event:FlexEvent):void { 
       var url:String = constructAuthorizedFeatureTokenURLFromSwf();   
       _loader = new Loader(); 
       var swfUrl:URLRequest = new URLRequest(url); 
       var loaderContext:LoaderContext =  
           new LoaderContext(false, ApplicationDomain.currentDomain, null); 
       _loader.contentLoaderInfo.addEventListener(Event.COMPLETE,  
           modEventHandler); 
       _loader.contentLoaderInfo.addEventListener(IOErrorEvent.IO_ERROR,  
           errEventHandler); 
       _loader.contentLoaderInfo.addEventListener(ProgressEvent.PROGRESS,  
           onProgressHandler); 
       _loader.uncaughtErrorEvents.addEventListener(UncaughtErrorEvent. 
           UNCAUGHT_ERROR, uncaughtEventHandler); 
       _logger.debug("# Loading token swf with context from [{0}].", url); 
       _loader.load(swfUrl, loaderContext); 
   } 
   
   private function modEventHandler(e:Event):void { 
       _logger.debug("loadSWF with domainID {0}",  
       SecurityDomain.currentDomain.domainID); 
       var loader : Loader = e.currentTarget.loader as Loader; 
       var myAuthorizedTokensLoaderClass:Class =  
           loader.contentLoaderInfo.applicationDomain. 
           getDefinition("AuthorizedTokensLoader") as Class; 
       var myTokens:Object = new myAuthorizedTokensLoaderClass(); 
       _authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       _authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       _authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       var byteArray:ByteArray = myTokens. 
           FetchToken(SecurityDomain.currentDomain.domainID); 
       if (myTokens == null || byteArray == null || byteArray.length == 0) 
           loadDirectTokenURL(); 
       else { 
           _logger.debug("token bytearry size {0}", byteArray.length); 
           _authorizedFeatureHelper.loadFeatureFromData(byteArray); 
       } 
       _loader.unload(); 
   } 
   ```

   **Ejemplo de varios tokens 2:**

   ```
   private function tokenSwfLoadedHandler(e:Event):void { 
       trace("loadSWF with domainID {0}", SecurityDomain.currentDomain.domainID); 
       var loader : Loader = e.currentTarget.loader as Loader; 
       var myAuthorizedTokensLoaderClass:Class =  
         loader.contentLoaderInfo.applicationDomain. 
         getDefinition("AuthorizedTokensLoader") as Class; 
       var myTokens:Object = new myAuthorizedTokensLoaderClass(); 
       authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       var byteArray:ByteArray =  
           myTokens.FetchToken(SecurityDomain.currentDomain.domainID); 
       var myDomains:Array = ["domain.com"]; 
       if (byteArray == null || byteArray.length == 0) { 
           // check for wildcard tokens 
           if (myTokens.hasOwnProperty("FetchWildCardToken") == true) { 
               // contains wildcard domains 
               for each (var domain:String in myDomains) { 
                   byteArray = myTokens.FetchWildCardToken(domain); 
                   if (byteArray != null && byteArray.length != 0) { 
                       break; 
                   } 
               }; 
           } 
       } 
   
       if (myTokens == null || byteArray == null || byteArray.length == 0) 
           loadDirectTokenURL(); 
       else { 
           trace("token bytearry size {0}", byteArray.length); 
           authorizedFeatureHelper.loadFeatureFromData(byteArray); 
       } 
       _loader.unload(); 
   } 
   
   private function loadDirectTokenURL():void { 
       trace("#onApplicationComplete Loading token from [{0}].", tokenUrl); 
       authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       authorizedFeatureHelper.loadFrom(tokenUrl); 
   }
   ```

