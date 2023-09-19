---
title: Determinar si el servidor de licencias de implementación de referencia se ejecuta correctamente
description: Determinar si el servidor de licencias de implementación de referencia se ejecuta correctamente
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Determinar si el servidor de licencias de implementación de referencia se ejecuta correctamente {#determining-if-reference-implementation-license-server-runs-properly}

Existen varias formas de determinar si el servidor de licencias de implementación de referencia se ha iniciado correctamente. Puede ver el [!DNL catalina.log] es posible que los registros no sean suficientes, ya que el servidor de licencias inicia sesión en sus propios archivos de registro. Siga los pasos a continuación para asegurarse de que la implementación de referencia se ha iniciado correctamente.

* Compruebe su [!DNL AdobeFlashAccess.log] archivo. Aquí es donde la Implementación de referencia escribe la información de registro. La ubicación de este archivo de registro se indica mediante su [!DNL log4j.xml] y se puede modificar para que apunte a cualquier ubicación que desee. De forma predeterminada, el fichero de registro se copia en el directorio de trabajo donde se ejecuta catalina.

* Vaya a la siguiente dirección URL: [!DNL https:// flashaccess/license/v4]*su servidor:puerto de servidor*. Debería ver el texto &quot;El servidor de licencias está configurado correctamente&quot;.

Otra forma de probar si el servidor se ejecuta correctamente es empaquetar un segmento del contenido de prueba, configurar un reproductor de vídeo de muestra y luego reproducirlo.

El siguiente procedimiento describe este proceso:

1. Vaya a la [!DNL \Reference Implementation\Command Line Tools] carpeta.

   Consulte [Instalación de las herramientas de línea de comandos](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) sobre cómo instalar las herramientas de la línea de comandos.

1. Escriba el siguiente comando para crear una directiva de DRM anónima simple:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Consulte [Uso de línea de comandos](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) sobre cómo crear políticas de DRM con el Administrador de políticas de DRM.

1. Configure las variables `encrypt.license.serverurl` propiedad en el [!DNL flashaccesstools.properties] a la URL del servidor de licencias.

   Por ejemplo, [!DNL https:// localhost:8080/]. El [!DNL flashaccesstools.properties] El archivo se encuentra en [!DNL \Reference Implementation\Command Line Tools] carpeta.

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

1. Copie los dos archivos generados en [!DNL webapps\ROOT\Content] en el servidor Tomcat.
1. Vaya a la [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] y copie el contenido en el [!DNL webapps\ROOT\SVP\] en el servidor Tomcat.

1. Instale la versión 10.1 o posterior del Flash Player de.
1. Abra un explorador web y vaya a la siguiente URL: [!DNL        https:// localhost:8080/SVP/player.html]

1. Vaya a la siguiente dirección URL y haga clic en **[!UICONTROL Play]**: [!DNL https:// localhost:8080/Content/] *`your_encrypted_FLV`*.

1. Si el vídeo no se reproduce, compruebe si se muestran códigos de error en el panel de registro del reproductor de vídeo de muestra o si se agregan a [!DNL AdobeFlashAccess.log] archivo.

   Ahora puede buscar la ubicación del [!DNL AdobeFlashAccess.log] en el archivo log4j.xml y, a continuación, modifíquelo. De forma predeterminada, el fichero log se copia en el directorio de trabajo donde se ejecuta catalina.
