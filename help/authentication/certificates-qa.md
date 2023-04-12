---
title: Preguntas y respuestas sobre certificados
description: Preguntas y respuestas sobre certificados
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---



# Preguntas y respuestas sobre certificados {#certificates-q}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>

**T1:** ¿Es posible registrar certificados en iOS y Android?

**A:** El certificado para iOS y Android es el mismo en la configuración actual. El certificado nativo se utiliza para ambas plataformas.

</br>

**Segundo trimestre:** ¿Se pueden utilizar los mismos certificados de iOS que los certificados Primary &amp; Backup en los entornos Production y Staging? Si no se recomienda, ¿puede ofrecer una explicación?

**A:** No tiene sentido configurar el mismo certificado que el certificado principal y el de copia de seguridad. Tenemos el concepto de certificados de primaria y de copia de seguridad para que podamos configurar varios certificados para un programador en caso de que el certificado primario caduque o se revoque. Tener un certificado de copia de seguridad dará a los programadores tiempo para cambiar el primario sin afectar al entorno de versiones. Sin embargo, puede utilizar el mismo conjunto de certificados Primarios y de Copia de seguridad para los perfiles Producción y Ensayo.

</br>

**T3:** ¿Se necesita un nuevo certificado para las páginas web que utilicen el nuevo TempPass flexible? 

**A:** El certificado (y, de hecho, cualquier certificado) se configura en el nivel de empresa y programador de medios. FlexibleTempPass es un MVPD, no necesita configurar ningún certificado para él, por lo que si está integrando un Programador existente con TempPass flexible, se utilizará el certificado que ya está configurado a nivel de Programador / Empresa de Medios.

