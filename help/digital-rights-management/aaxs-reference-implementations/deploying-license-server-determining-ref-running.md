---
title: Determinar si el servidor de licencias de implementación de referencia se está ejecutando correctamente
description: Determinar si el servidor de licencias de implementación de referencia se está ejecutando correctamente
copied-description: true
exl-id: ef28e169-f8d2-4c7f-b606-aa4e811aae9b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Determinar si el servidor de licencias de implementación de referencia se está ejecutando correctamente {#determining-if-reference-implementation-license-server-is-running-properly}

Existen varias formas de determinar si el servidor se ha iniciado correctamente. Visualización de la [!DNL catalina.log] es posible que los registros no sean suficientes, ya que el servidor de licencias inicia sesión en sus propios archivos de registro. Siga los pasos a continuación para asegurarse de que la implementación de referencia se ha iniciado correctamente.

* Compruebe su [!DNL AdobeFlashAccess.log] archivo. Aquí es donde la Implementación de referencia escribe la información de registro. La ubicación de este archivo de registro se indica mediante su [!DNL log4j.xml] y se puede modificar para que apunte a cualquier ubicación que desee. De forma predeterminada, el fichero log se envía al directorio de trabajo donde se ha ejecutado catalina.

* Vaya a la siguiente dirección URL: `https:///flashaccess/license/v4<your server:server port>`. Debería ver el texto &quot;El servidor de licencias está configurado correctamente&quot;.

Otra forma de probar si el servidor se está ejecutando correctamente es empaquetar un fragmento de contenido de prueba, configurar un reproductor de vídeo de muestra y reproducirlo. El siguiente procedimiento describe este proceso:

1. Vaya a [!DNL \Reference Implementation\Command Line Tools] carpeta. Para obtener información acerca de cómo instalar las herramientas de la línea de comandos, consulte [Instalación de las herramientas de línea de comandos](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools).

1. Cree una directiva anónima simple con el siguiente comando:

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   Para obtener más información sobre la creación de directivas mediante el Administrador de directivas, consulte [Uso de línea de comandos](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md).

1. Configure las variables `encrypt.license.serverurl` propiedad en el [!DNL flashaccesstools.properties] a la URL del servidor de licencias (por ejemplo, `https:// localhost:8080/`). El [!DNL flashaccesstools.properties] El archivo se encuentra en [!DNL \Reference Implementation\Command Line Tools] carpeta.

1. Empaquete un fragmento de contenido mediante el siguiente comando:

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

1. Copie los dos archivos generados en Tomcat [!DNL webapps\ROOT\Content] carpeta.
1. Vaya a `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` y copie el contenido en el Tomcat `webapps\ROOT\SVP\` carpeta.
1. Instale Flash Player 10.1 o posterior.
1. Abra el explorador web y vaya a la siguiente URL:

   `https:// localhost:8080/SVP/player.html`
1. Vaya a la siguiente dirección URL y haga clic en el botón Reproducir:

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. Si el vídeo no se reproduce, compruebe si se escribieron códigos de error en el panel de registro del reproductor de vídeo de muestra o en el `AdobeFlashAccess.log` archivo. La ubicación del `AdobeFlashAccess.log` El archivo de registro se indica mediante el archivo log4j.xml y se puede modificar para que señale a cualquier ubicación que desee. De forma predeterminada, el fichero de registro se escribe en el directorio de trabajo donde se ha ejecutado catalina.
