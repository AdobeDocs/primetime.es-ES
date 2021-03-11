---
title: Determinación de si el servidor de licencias de implementación de referencia se ejecuta correctamente
description: Determinación de si el servidor de licencias de implementación de referencia se ejecuta correctamente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Determinación de si el servidor de licencias de implementación de referencia se ejecuta correctamente {#determining-if-reference-implementation-license-server-runs-properly}

Existen varias formas de determinar si el Servidor de licencias de implementación de referencia se ha iniciado correctamente. Puede que no sea suficiente ver los registros [!DNL catalina.log], ya que el servidor de licencias inicia sesión en sus propios archivos de registro. Siga los pasos a continuación para asegurarse de que la Implementación de referencia se ha iniciado correctamente.

* Compruebe el archivo [!DNL AdobeFlashAccess.log]. Aquí es donde la Implementación de referencia escribe la información de registro. La ubicación de este archivo de registro la indica su archivo [!DNL log4j.xml] y se puede modificar para que apunte a cualquier ubicación que desee. De forma predeterminada, el archivo de registro se copia en el directorio de trabajo donde ejecuta catalina.

* Vaya a la siguiente URL: [!DNL https:// flashaccess/license/v4]*su servidor:puerto del servidor*. Debería ver el texto &quot;El servidor de licencias está configurado correctamente&quot;.

Otra forma de comprobar si el servidor se ejecuta correctamente es empaquetar un segmento del contenido de prueba, configurar un reproductor de vídeo de muestra y reproducirlo.

El siguiente procedimiento describe este proceso:

1. Vaya a la carpeta [!DNL \Reference Implementation\Command Line Tools] .

   Consulte [Instalación de las herramientas de la línea de comandos](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) sobre cómo instalar las herramientas de la línea de comandos.

1. Escriba el siguiente comando para crear una política DRM anónima simple:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Consulte [Uso de la línea de comandos](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) sobre cómo crear políticas de DRM con el Administrador de políticas de DRM.

1. Establezca la propiedad `encrypt.license.serverurl` en el archivo [!DNL flashaccesstools.properties] en la URL del servidor de licencias.

   Por ejemplo, [!DNL https:// localhost:8080/]. El archivo [!DNL flashaccesstools.properties] se encuentra en la carpeta [!DNL \Reference Implementation\Command Line Tools].

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

1. Copie los dos archivos generados en la carpeta [!DNL webapps\ROOT\Content] del servidor Tomcat.
1. Vaya al directorio [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] y copie el contenido en la carpeta [!DNL webapps\ROOT\SVP\] del servidor Tomcat.

1. Instale Flash Player versión 10.1 o posterior.
1. Abra un explorador web y vaya a la siguiente URL: [!DNL        https:// localhost:8080/SVP/player.html]

1. Vaya a la siguiente dirección URL y haga clic en **[!UICONTROL Play]**: [!DNL https:// localhost:8080/Content/] *`your_encrypted_FLV`*.

1. Si no se puede reproducir el vídeo, compruebe si se muestran códigos de error en el panel de registro del reproductor de vídeo de ejemplo o si se añaden al archivo [!DNL AdobeFlashAccess.log] .

   Ahora puede buscar la ubicación del archivo de registro [!DNL AdobeFlashAccess.log] en el archivo log4j.xml y luego modificarlo. De forma predeterminada, el archivo de registro se copia en el directorio de trabajo donde ejecuta catalina.

