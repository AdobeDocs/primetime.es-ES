---
title: Determinación de si el servidor de licencias de implementación de referencia se está ejecutando correctamente
description: Determinación de si el servidor de licencias de implementación de referencia se está ejecutando correctamente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Determinación de si el servidor de licencias de implementación de referencia se está ejecutando correctamente {#determining-if-reference-implementation-license-server-is-running-properly}

Existen varias formas de determinar si el servidor se ha iniciado correctamente. Puede que no sea suficiente ver los registros [!DNL catalina.log], ya que el servidor de licencias inicia sesión en sus propios archivos de registro. Siga los pasos a continuación para asegurarse de que la Implementación de referencia se ha iniciado correctamente.

* Compruebe el archivo [!DNL AdobeFlashAccess.log]. Aquí es donde la Implementación de referencia escribe la información de registro. La ubicación de este archivo de registro la indica su archivo [!DNL log4j.xml] y se puede modificar para que apunte a cualquier ubicación que desee. De forma predeterminada, el archivo de registro se enviará al directorio de trabajo donde ha ejecutado catalina.

* Vaya a la siguiente URL: `https:///flashaccess/license/v4<your server:server port>`. Debería ver el texto &quot;El servidor de licencias está configurado correctamente&quot;.

Otra forma de comprobar si el servidor se está ejecutando correctamente es empaquetar un fragmento de contenido de prueba, configurar un reproductor de vídeo de muestra y reproducirlo. El siguiente procedimiento describe este proceso:

1. Vaya a la carpeta [!DNL \Reference Implementation\Command Line Tools] . Para obtener información sobre la instalación de las herramientas de línea de comandos, consulte [Instalación de las herramientas de línea de comandos](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools).

1. Cree una política anónima simple mediante el siguiente comando:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Para obtener más información sobre la creación de directivas mediante el Administrador de directivas, consulte [Uso de la línea de comandos](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md).

1. Establezca la propiedad `encrypt.license.serverurl` en el archivo [!DNL flashaccesstools.properties] en la URL del servidor de licencias (por ejemplo, `https:// localhost:8080/`). El archivo [!DNL flashaccesstools.properties] se encuentra en la carpeta [!DNL \Reference Implementation\Command Line Tools].

1. Empaquete un fragmento de contenido utilizando el siguiente comando:

   ```java
       java -jar libs\AdobePackager.jar  
   <i class="+ topic ph hi-d="" i "="">
   test_input_FLV  
   <i class="+ topic ph hi-d="" i "="">
   output_file  
               -p policy_test.pol 
   </i class="+ topic> 
   </i class="+ topic>
   ```

1. Copie los 2 archivos generados en la carpeta Tomcat [!DNL webapps\ROOT\Content] .
1. Vaya a `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` y copie el contenido en la carpeta Tomcat `webapps\ROOT\SVP\` .
1. Instale el Flash Player 10.1 o posterior.
1. Abra el explorador web y vaya a la siguiente dirección URL:

   `https:// localhost:8080/SVP/player.html`
1. Vaya a la siguiente URL y, a continuación, haga clic en el botón Reproducir :

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. Si el vídeo no se reproduce, compruebe si se han escrito códigos de error en el panel de registro del reproductor de vídeo de ejemplo o en el archivo `AdobeFlashAccess.log` . La ubicación del archivo de registro `AdobeFlashAccess.log` está indicada por el archivo log4j.xml y se puede modificar para que apunte a cualquier ubicación que desee. De forma predeterminada, el archivo de registro se escribe en el directorio de trabajo donde ha ejecutado catalina.
