---
title: aaaSecure API utilizzando l'autenticazione del certificato client in Gestione API - Gestione API di Azure | Documenti Microsoft
description: Informazioni su come toosecure accedere tooAPIs mediante certificati client
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: apimpm
ms.openlocfilehash: 6ff78bda3d429829da79d0dc4d652f19669cc919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a>Come toosecure API che utilizzano client certificato di autenticazione in Gestione API

Gestione API fornisce hello funzionalità toosecure accesso tooAPIs (ad esempio, client tooAPI Management) utilizzando i certificati client. Attualmente, è possibile verificare l'identificazione personale hello del certificato client con un valore desiderato. È inoltre possibile verificare l'identificazione personale hello contro certificati esistenti caricato tooAPI Management.  

Per informazioni sulla sicurezza servizio di accesso toohello back-end di un'API tramite certificati client (ad esempio, gestione API tooback-end), vedere [toosecure servizi di back-end tramite client come certificato di autenticazione](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)

## <a name="checking-hello-expiration-date"></a>Verifica la data di scadenza hello

Di sotto di criteri può essere configurato toocheck se hello certificato è scaduto:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a>Controllo dell'autorità di certificazione hello e l'oggetto

Di sotto di criteri può essere configurato toocheck hello emittente e soggetto del certificato client:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a>Verifica l'identificazione personale hello

Di sotto di criteri può essere configurato toocheck hello identificazione di un certificato client:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a>Controllo un'identificazione digitale contro certificati caricati tooAPI gestione

Hello esempio seguente viene illustrato come identificazione personale hello toocheck di un certificato client con i certificati caricati tooAPI Management: 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a>Passaggio successivo

*  [Servizi back-end toosecure tramite client come certificato di autenticazione](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [La modalità certificati tooupload](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

