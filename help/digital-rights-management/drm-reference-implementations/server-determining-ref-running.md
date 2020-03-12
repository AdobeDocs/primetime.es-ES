---
description: 'null'
seo-description: 'null'
seo-title: Determinación de si el servidor de licencias de implementación de referencia se ejecuta correctamente
title: Determinación de si el servidor de licencias de implementación de referencia se ejecuta correctamente
uuid: afd82d6d-a11c-48ff-b48c-8f81d4b406a0
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Determinación de si el servidor de licencias de implementación de referencia se ejecuta correctamente {#determining-if-reference-implementation-license-server-runs-properly}

Existen varias formas de determinar si el servidor de licencias de implementación de referencia se ha iniciado correctamente. Puede ver los [!DNL catalina.log] registros que no son suficientes, ya que el servidor de licencias inicia sesión en sus propios archivos de registro. Siga los pasos a continuación para asegurarse de que la implementación de referencia se ha iniciado correctamente.

* Compruebe su [!DNL AdobeFlashAccess.log] archivo. Aquí es donde la Implementación de referencia escribe la información del registro. El archivo indica la ubicación de este archivo de registro y se puede modificar para que señale a cualquier ubicación que desee. [!DNL log4j.xml] De forma predeterminada, el archivo de registro se copia en el directorio de trabajo donde se ejecuta Catalina.

* Vaya a la siguiente URL: [!DNL https:// flashaccess/license/v4]*su servidor:puerto *de servidor. Debería ver el texto &quot;El servidor de licencias está configurado correctamente&quot;.

Otra forma de comprobar si el servidor se ejecuta correctamente es empaquetar un segmento del contenido de prueba, configurar un reproductor de vídeo de muestra y reproducirlo.

El siguiente procedimiento describe este proceso:

1. Vaya a la [!DNL \Reference Implementation\Command Line Tools] carpeta.

   Consulte [Instalación de las herramientas](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) de la línea de comandos sobre cómo instalar las herramientas de la línea de comandos.

1. Escriba el siguiente comando para crear una directiva DRM anónima simple:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Consulte Uso [de la línea de](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) comandos para crear políticas de DRM con el Administrador de directivas de DRM.

1. Establezca la `encrypt.license.serverurl` propiedad del [!DNL flashaccesstools.properties] archivo en la dirección URL del servidor de licencias.

   Por ejemplo, [!DNL https:// localhost:8080/]. El [!DNL flashaccesstools.properties] archivo se encuentra en la [!DNL \Reference Implementation\Command Line Tools] carpeta.

1. Escriba el siguiente comando para empaquetar un segmento del contenido:

```
       java -jar libs\AdobePackager.jar  
       <i class="+ topic ph hi-d="" i "="">
         test_input_FLV  
        <i class="+ topic ph hi-d="" i "="">
       output_file  
               -p policy_test.pol 
       </i class="+ topic> 
       </i class="+ topic>
```

1. Copie los dos archivos generados en la [!DNL webapps\ROOT\Content] carpeta del servidor Tomcat.
1. Vaya al [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] directorio y copie el contenido en la carpeta [!DNL webapps\ROOT\SVP\] del servidor Tomcat.

1. Instale Flash Player versión 10.1 o posterior.
1. Abra un navegador web y vaya a la siguiente URL: [!DNL        https:// localhost:8080/SVP/player.html]

1. Vaya a la siguiente URL y haga clic en **[!UICONTROL Play]**: [!DNL https:// localhost:8080/Content/]*`your_encrypted_FLV`*.

1. Si el vídeo no se puede reproducir, compruebe si se muestra algún código de error en el panel de registro del reproductor de vídeo de muestra o si se agrega al [!DNL AdobeFlashAccess.log] archivo.

   Ahora puede buscar la ubicación del archivo de [!DNL AdobeFlashAccess.log] registro en el archivo log4j.xml y luego modificarlo. De forma predeterminada, el archivo de registro se copia en el directorio de trabajo donde se ejecuta Catalina.

