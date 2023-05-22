---
description: Para implementar DRM necesita certificados y claves particulares, incluida una clave de cifrado de contenido o CEK para cifrar el contenido, un autenticador de cliente para proteger las comunicaciones con los servidores ExpressPlay y CEKSID para identificar las claves de cifrado de contenido almacenadas en un sistema de administración de claves.
title: Claves, ID y autenticadores
exl-id: b769192d-92ad-4b93-84dd-80b182fc6c43
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---

# Claves, ID y autenticadores{#keys-ids-and-authenticators}

Para implementar DRM necesita certificados y claves particulares, incluida una clave de cifrado de contenido o CEK para cifrar el contenido, un autenticador de cliente para proteger las comunicaciones con los servidores ExpressPlay y CEKSID para identificar las claves de cifrado de contenido almacenadas en un sistema de administración de claves.

Necesita estos elementos para empaquetar, obtener una licencia y reproducir el contenido protegido:

## Clave de cifrado de contenido {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

La clave de cifrado de contenido (CEK) es una cadena de 16 bytes que se utiliza para cifrar contenido.

**¿Qué es el CEK?** - El CEK es la clave que utiliza su empaquetador para cifrar su contenido. Es una cadena de 16 bytes con codificación hexadecimal.

**¿De dónde viene el CEK?** - Usted (el proveedor de contenido) crea esta clave usted mismo, con una herramienta como OpenSSL o Notepad++. Por ejemplo:

```
openssl rand 16 -hex > cek_hex_file
```

o (para el empaquetador sin conexión de Adobe):

1. Genere la cadena con codificación hexadecimal de 16 bytes, como se ha indicado anteriormente, o utilizando otra herramienta. Tendrá un aspecto similar al siguiente:

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. Abra el Bloc de notas++ y pegue la cadena hexadecimal de 16 bytes.
1. Convierta este valor de ASCII hexadecimal codificando en Base64 el valor para crear su [!DNL keyfile.bin]. (Esto se trata en [](../../multi-drm-workflows/quick-start/package-your-content.md).)

**¿La misma llave, un nombre diferente?** - Sí, es posible que vea el CEK al que se hace referencia con otros nombres en otros lugares, como:

* ** [!DNL [somefile].bin]**: el empaquetador sin conexión de Adobe hace referencia a la CEK como [!DNL [somefile].bin]; p. ej., * [!DNL Keyfile.bin]* - Este es su CEK como lo utiliza el Packager sin conexión de Adobe, en forma de archivo en la máquina que utiliza para empaquetar contenido.

   Usted &quot;Base64&quot; su cadena hexagonal aleatoria CEK, y guardarlo como un archivo (por ejemplo, [!DNL keyfile.bin]), normalmente ubicado en el [!DNL creds] directorio debajo de [!DNL offlinepkgr/]. En el archivo de configuración de Packager (por ejemplo, podría llamarlo [!DNL widevine.xml] si está empaquetando para el Widevine (DRM), haga referencia a su CEK en el archivo de configuración de esta manera:

   ```
   <config>  
     <in_path>sample.mp4</in_path>  
     <out_type>dash</out_type>
     <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
     […] 
   </config> 
   ```

* **Clave de contenido** : También puede ver la CEK denominada como clave de contenido en las llamadas ( `&contentKey=`), en mensajes de error, en vales de soporte y en otra documentación.

**¿Cuándo/dónde lo uso?**

1. En primer lugar, debe tener el CEK disponible en la máquina en la que está haciendo su embalaje. La herramienta de empaquetado utiliza su CEK para cifrar su contenido.
1. En segundo lugar, debe almacenar la CEK en algún tipo de sistema de administración de claves (KMS), con cada CEK asociado a su propia CEK [Clave de cifrado de contenido](../../multi-drm-workflows/glossary/glossary-cek.md). Puede crear su propio KMS o utilizar [Almacenamiento de claves de ExpressPlay](https://www.expressplay.com/developer/key-storage/). Esto permite que su tienda (su servidor de autorizaciones, que gestiona los derechos de los clientes y la provisión de tokens de licencia) extraiga un token de licencia para el cliente del KMS con un ID de clave en lugar del CEK real (esto es mucho más seguro).

## ID de almacenamiento de clave de cifrado de contenido {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

El ID de almacenamiento de clave de cifrado de contenido (CEKSID) identifica de forma exclusiva la clave almacenada que descifra un fragmento cifrado de contenido de vídeo.

**¿Qué es el CEKSID?** : el CEKSID es el identificador único de una clave de cifrado de contenido (CEK). El CEK es necesario para desbloquear el contenido protegido; el CEKSID es necesario para acceder al CEK desde donde se almacena. Al probar la configuración, puede proporcionar un CEKSID y una CEK aleatorios en el momento del empaquetado, siempre y cuando utilice la misma información para las comprobaciones de licencias y reproducción.

**¿De dónde viene?** - Usted (el proveedor de contenido) puede crear este ID o puede utilizar un servicio como [Almacenamiento de claves de ExpressPlay](https://www.expressplay.com/developer/key-storage/) para generar CEKSID para cada una de las CEK (y almacenar ambas). Además, puede utilizar CEKSID generados aleatoriamente o utilizar un esquema que se adapte a su modelo empresarial. Por ejemplo, puede utilizar CEKSID que sean cadenas significativas en lugar de cadenas hexadecimales aleatorias (el nombre del ID puede constar de temas, fechas, horas, etc.)

**¿Cómo se llama el CEKSID?** - A veces se denomina *ID de contenido*.

## Autenticador de cliente {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

El autenticador de cliente es una clave que obtiene de ExpressPlay cuando configura una cuenta de administrador allí. El autenticador se utiliza en comunicaciones con servidores ExpressPlay.

**¿Qué son los autenticadores de cliente?** : Los dos autenticadores de cliente constituyen el par de ID (uno para pruebas y otro para producción) que ExpressPlay registra para usted cuando se registra en su servicio. Siempre están disponibles en su página de administración de ExpressPlay:
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**¿Cuándo debo usar esto?** - Esto se incluye en todas las llamadas a servidores ExpressPlay; por ejemplo, servidores de licencias, [Almacenamiento de claves ExpressPlay](https://www.expressplay.com/developer/key-storage/)y otras llamadas.
