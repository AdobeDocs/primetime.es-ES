---
description: El TVSDK de tiempo de ejecución de Flash necesita un token firmado para validar que tiene derecho a llamar a la API de TVSDK en el dominio en el que reside la aplicación.
title: Cargue el token firmado
exl-id: fef6b764-dc65-412e-a990-3f0b1fef94dd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Cargue el token firmado {#load-your-signed-token}

El TVSDK de tiempo de ejecución de Flash necesita un token firmado para validar que tiene derecho a llamar a la API de TVSDK en el dominio en el que reside la aplicación.

1. Obtenga un token firmado de su representante de Adobe para cada uno de sus dominios (donde cada dominio puede ser un dominio específico o un dominio comodín).

       Para obtener un token, proporcione Adobe con el dominio donde se almacenará o cargará la aplicación o, preferiblemente, el dominio como un hash SHA256. A cambio, el Adobe le proporciona un token firmado para cada dominio. Estos tokens adoptan una de estas formas:
   
   * Un [!DNL .xml] archivo que actúa como token para un único dominio o dominio comodín.

      >[!NOTE]
      >
      >Un token para un dominio comodín cubre ese dominio y todos sus subdominios. Por ejemplo, un token comodín para el dominio [!DNL mycompany.com] también cubriría [!DNL vids.mycompany.com] y [!DNL private.vids.mycompany.com]; un token comodín para [!DNL vids.mycompany.com] también cubriría [!DNL private.vids.mycompany.com]. *Los tokens de dominio comodín solo son compatibles con determinadas versiones de Flash Player.*

   * A [!DNL .swf] archivo que contiene información de token para varios dominios (sin incluir caracteres comodín) (único o comodín), que la aplicación puede cargar dinámicamente.

1. Almacene el archivo de tokens en la misma ubicación o dominio que la aplicación.

   De forma predeterminada, TVSDK busca el token en esta ubicación. También puede especificar el nombre y la ubicación del token en `flash_vars` en el archivo de HTML.
1. Si el archivo de token es un solo archivo XML:
   1. Uso `utils.AuthorizedFeaturesHelper.loadFrom` para descargar los datos almacenados en la dirección URL especificada (el archivo de token) y extraer `authorizedFeatures` información de la misma.

      Este paso puede variar. Por ejemplo, es posible que desee realizar la autenticación antes de iniciar la aplicación o que reciba el token directamente desde el sistema de administración de contenido (CMS).

   1. TVSDK envía un `COMPLETED` evento si la carga se realiza correctamente o un `FAILED` de lo contrario. Tome las medidas adecuadas cuando detecte cualquiera de estos eventos.

      Esto debe tener éxito para que la aplicación proporcione los datos necesarios `authorizedFeatures` objetos a TVSDK en forma de `MediaPlayerContext`.
   Este ejemplo muestra cómo puede utilizar un token único [!DNL .xml] archivo.

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
   1. Defina un `Loader` para cargar dinámicamente el objeto [!DNL .swf] archivo.
   1. Configure las variables `LoaderContext` para especificar la carga que se va a realizar en el dominio de aplicación actual, lo que permite a TVSDK elegir el token correcto dentro de [!DNL .swf] archivo. If `LoaderContext` no se ha especificado, la acción predeterminada de `Loader.load` es para cargar el .swf en el dominio secundario del dominio actual.
   1. Escuche el evento COMPLETE, que TVSDK envía si la carga se realiza correctamente.

      Escuche también el evento ERROR y tome las medidas adecuadas.
   1. Si la carga se realiza correctamente, utilice el `AuthorizedFeaturesHelper` para obtener una `ByteArray` que contiene los datos de seguridad codificados PCKS-7.

      Estos datos se utilizan a través de la API AVE V11 para obtener el reconocimiento de autorización del reproductor de Flash Runtime. Si la matriz de bytes no tiene contenido, utilice en su lugar el procedimiento para buscar un archivo de token de un solo dominio.
   1. Uso `AuthorizedFeatureHelper.loadFeatureFromData` para obtener los datos necesarios de la matriz de bytes.
   1. Descargue el [!DNL .swf] archivo.

   Los siguientes ejemplos muestran cómo se puede utilizar un token múltiple [!DNL .swf] archivo.

   **Ejemplo 1 de token múltiple:**

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

   **Ejemplo 2 de token múltiple:**

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
