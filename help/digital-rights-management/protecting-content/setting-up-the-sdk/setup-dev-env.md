---
description: Si desea configurar Primetime DRM, copie los archivos del DVD. Estos archivos incluyen archivos JAR que incluyen código, certificados y clases de terceros. Además, debe solicitar un certificado de Adobe Systems, Incorporated. A continuación, Adobe le emite varias credenciales que utiliza para proteger la integridad del contenido empaquetado, las licencias y la comunicación entre el cliente y el servidor.
title: Configuración del entorno de desarrollo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# Configure el entorno de desarrollo {#set-up-your-development-environment}

Si desea configurar Primetime DRM, copie los archivos del DVD. Estos archivos incluyen archivos JAR que incluyen código, certificados y clases de terceros. Además, debe solicitar un certificado de Adobe Systems, Incorporated. A continuación, Adobe le emite varias credenciales que utiliza para proteger la integridad del contenido empaquetado, las licencias y la comunicación entre el cliente y el servidor.

Adobe proporciona el SDK de Primetime DRM en DVD:

1. Copie los siguientes archivos de [!DNL [DRM DVD]/SDK/] a su sistema de desarrollo (en su ruta de clase Java):

   * [!DNL adobe-flashaccess-certs.jar] - Incluye certificados raíz de Adobe
   * [!DNL adobe-flashaccess-sdk.jar] - Incluye clases principales de SDK de DRM de Primetime
   * [!DNL adobe-flashaccess-sdk-pro.jar] : incluye clases de SDK de Primetime DRM Professional, solo necesarias para funciones profesionales.

1. Copie los siguientes archivos de [!DNL [DRM DVD]/SDK/thirdparty] a su sistema de desarrollo:

   * [!DNL bcmail-jdk15-141.jar]
   * [!DNL bcprov-jdk15-141.jar]
   * [!DNL commons-discovery-0.4.jar]
   * [!DNL commons-logging-1.1.1.jar]
   * [!DNL cryptoj.jar]
   * [!DNL jaxb-api.jar]
   * [!DNL jaxb-impl.jar]
   * [!DNL jaxb-libs.jar]
   * [!DNL relaxngDatatype.jar]
   * [!DNL rm-pdrl.jar]
   * [!DNL xsdlib.jar]
   * [!DNL jackson-annotations-2.4.0-rc4-20140522.175222-3.jar]
   * [!DNL jackson-core--2.4.0-rc4-20140529.184520-13.jar]
   * [!DNL jackson-databind-2.4.0-rc4-20140603.005043-38.jar]

1. (Opcional) Para mejorar el rendimiento, puede habilitar la compatibilidad nativa con las operaciones criptográficas copiando la biblioteca específica de la plataforma adecuada de [!DNL [DRM DVD]/SDK/thirdparty/cryptoj/] a su sistema de desarrollo (recuerde colocar la ubicación en la ruta):

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

      >[!NOTE]
      >
      >Hay disponibles versiones de 32 y 64 bits de estas bibliotecas. Solo debe utilizar la versión de 64 bits si tiene un sistema operativo de 64 bits y ejecuta la versión de 64 bits de Java.

1. (Opcional) Para funciones relacionadas con la compatibilidad con el Servidor de Media Rights Management de Flash de Adobe (FMRMS) 1.x, copie `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` en el sistema de desarrollo:

   Implemente esto solo si ha implementado anteriormente FMRMS 1.x y no desea volver a empaquetar el contenido protegido por FMRMS. En este caso, debe añadir esta compatibilidad al servidor de licencias para que pueda administrar el contenido antiguo y los clientes.
