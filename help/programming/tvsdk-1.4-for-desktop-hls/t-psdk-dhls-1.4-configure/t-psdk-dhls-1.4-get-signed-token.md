---
description: El SDK de tiempo de ejecución de Flash necesita un token firmado para validar que tiene derecho a llamar a la API de TVSDK en el dominio en el que reside la aplicación.
title: Cargar el token firmado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# Cargue el token firmado {#load-your-signed-token}

El SDK de tiempo de ejecución de Flash necesita un token firmado para validar que tiene derecho a llamar a la API de TVSDK en el dominio en el que reside la aplicación.

1. Obtenga un token firmado del representante de su Adobe para cada uno de sus dominios (donde cada dominio podría ser un dominio específico o un dominio comodín).

       Para obtener un token, proporcione el Adobe del dominio en el que se almacenará o cargará la aplicación o, preferiblemente, el dominio como hash SHA256. A cambio, Adobe le proporciona un token firmado para cada dominio. Estos tokens adoptan una de estas formas:
   
   * Un archivo [!DNL .xml] que actúa como token para un dominio único o comodín.

      >[!NOTE]
      >
      >Un token para un dominio comodín cubre ese dominio y todos sus subdominios. Por ejemplo, un token comodín para el dominio [!DNL mycompany.com] también cubriría [!DNL vids.mycompany.com] y [!DNL private.vids.mycompany.com]; un token comodín para [!DNL vids.mycompany.com] también cubriría [!DNL private.vids.mycompany.com]. *Los tokens de dominio comodín solo se admiten para determinadas versiones de Flash Player.*

   * Archivo [!DNL .swf] que contiene información de token para varios dominios (sin incluir caracteres comodín) (único o comodín), que la aplicación puede cargar dinámicamente.

1. Almacene el archivo token en la misma ubicación o dominio que la aplicación.

   De forma predeterminada, TVSDK busca el token en esta ubicación. Como alternativa, puede especificar el nombre y la ubicación del token en `flash_vars` en el archivo HTML.
1. Si el archivo token es un único archivo XML:
   1. Utilice `utils.AuthorizedFeaturesHelper.loadFrom` para descargar los datos almacenados en la dirección URL especificada (el archivo token) y extraer la información `authorizedFeatures` de él.

      Este paso puede variar. Por ejemplo, es posible que desee realizar la autenticación antes de iniciar la aplicación o que reciba el token directamente desde el sistema de administración de contenido (CMS).

   1. TVSDK envía un evento `COMPLETED` si la carga se realiza correctamente o un evento `FAILED` en caso contrario. Realice las acciones adecuadas cuando detecte uno de los eventos.

      Esto debe ser correcto para que la aplicación proporcione los objetos `authorizedFeatures` necesarios a TVSDK en forma de `MediaPlayerContext`.
   Este ejemplo muestra cómo puede utilizar un archivo [!DNL .xml] de un solo token.

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

1. Si el token es un archivo [!DNL .swf]:
   1. Defina una clase `Loader` para cargar dinámicamente el archivo [!DNL .swf].
   1. Establezca `LoaderContext` para especificar la carga que debe estar en el dominio de aplicación actual, lo que permite que TVSDK elija el token correcto dentro del archivo [!DNL .swf]. Si no se especifica `LoaderContext`, la acción predeterminada de `Loader.load` es cargar el .swf en el dominio secundario del dominio actual.
   1. Escuche el evento COMPLETE que envía TVSDK si la carga se realiza correctamente.

      Escuche también el evento ERROR y tome las medidas adecuadas.
   1. Si la carga se realiza correctamente, utilice `AuthorizedFeaturesHelper` para obtener un `ByteArray` que contenga los datos de seguridad codificados con PCKS-7.

      Estos datos se utilizan a través de la API AVE V11 para obtener el reconocimiento de autorización de Flash Runtime Player. Si la matriz de bytes no tiene contenido, utilice el procedimiento para buscar un archivo token de un solo dominio.
   1. Utilice `AuthorizedFeatureHelper.loadFeatureFromData` para obtener los datos necesarios de la matriz de bytes.
   1. Descarga el archivo [!DNL .swf].

   Los siguientes ejemplos muestran cómo puede utilizar un archivo [!DNL .swf] de varios tokens.

   **Ejemplo 1 de varios tokens:**

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

   **Ejemplo 2 de varios tokens:**

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

