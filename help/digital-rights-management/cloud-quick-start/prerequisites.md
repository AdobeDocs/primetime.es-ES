---
title: Requisitos previos
description: Requisitos previos
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Requisitos previos {#prerequisites}

Antes de empaquetar contenido, se requiere un certificado de empaquetador DRM de Primetime. Debe solicitarse a través del proceso de inscripción de certificados DRM de Primetime. Solo se requiere un certificado de empaquetador (sin servidor de licencias ni transporte). Indique en el correo electrónico de solicitud de certificado que la solicitud es para un certificado que se utilizará con el servicio DRM.

[Guía de inscripción de certificados](../../digital-rights-management/certificate-enrollment-guide/about-certs.md)

Existen dos niveles de certificados de embalaje: PRODUCCIÓN y PRUEBA. El contenido empaquetado con certificados TRIAL solo se utiliza para desarrollo y no se reproducirá después de que caduque el certificado. Todas las licencias emitidas para el contenido de PRUEBA tendrán una fecha de caducidad máxima de la directiva codificada igual a la fecha de caducidad del certificado (si no se establece en la directiva DRM).
