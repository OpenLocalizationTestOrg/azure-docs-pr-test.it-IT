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
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="b10e8-103">Come toosecure API che utilizzano client certificato di autenticazione in Gestione API</span><span class="sxs-lookup"><span data-stu-id="b10e8-103">How toosecure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="b10e8-104">Gestione API fornisce hello funzionalità toosecure accesso tooAPIs (ad esempio, client tooAPI Management) utilizzando i certificati client.</span><span class="sxs-lookup"><span data-stu-id="b10e8-104">API Management provides hello capability toosecure access tooAPIs (i.e., client tooAPI Management) using client certificates.</span></span> <span data-ttu-id="b10e8-105">Attualmente, è possibile verificare l'identificazione personale hello del certificato client con un valore desiderato.</span><span class="sxs-lookup"><span data-stu-id="b10e8-105">Currently, you can check hello thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="b10e8-106">È inoltre possibile verificare l'identificazione personale hello contro certificati esistenti caricato tooAPI Management.</span><span class="sxs-lookup"><span data-stu-id="b10e8-106">You can also check hello thumbprint against existing certificates uploaded tooAPI Management.</span></span>  

<span data-ttu-id="b10e8-107">Per informazioni sulla sicurezza servizio di accesso toohello back-end di un'API tramite certificati client (ad esempio, gestione API tooback-end), vedere [toosecure servizi di back-end tramite client come certificato di autenticazione](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span><span class="sxs-lookup"><span data-stu-id="b10e8-107">For information about securing access toohello back-end service of an API using client certificates (i.e., API Management tooback-end), see [How toosecure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-hello-expiration-date"></a><span data-ttu-id="b10e8-108">Verifica la data di scadenza hello</span><span class="sxs-lookup"><span data-stu-id="b10e8-108">Checking hello expiration date</span></span>

<span data-ttu-id="b10e8-109">Di sotto di criteri può essere configurato toocheck se hello certificato è scaduto:</span><span class="sxs-lookup"><span data-stu-id="b10e8-109">Below policies can be configured toocheck if hello certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a><span data-ttu-id="b10e8-110">Controllo dell'autorità di certificazione hello e l'oggetto</span><span class="sxs-lookup"><span data-stu-id="b10e8-110">Checking hello issuer and subject</span></span>

<span data-ttu-id="b10e8-111">Di sotto di criteri può essere configurato toocheck hello emittente e soggetto del certificato client:</span><span class="sxs-lookup"><span data-stu-id="b10e8-111">Below policies can be configured toocheck hello issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a><span data-ttu-id="b10e8-112">Verifica l'identificazione personale hello</span><span class="sxs-lookup"><span data-stu-id="b10e8-112">Checking hello thumbprint</span></span>

<span data-ttu-id="b10e8-113">Di sotto di criteri può essere configurato toocheck hello identificazione di un certificato client:</span><span class="sxs-lookup"><span data-stu-id="b10e8-113">Below policies can be configured toocheck hello thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a><span data-ttu-id="b10e8-114">Controllo un'identificazione digitale contro certificati caricati tooAPI gestione</span><span class="sxs-lookup"><span data-stu-id="b10e8-114">Checking a thumbprint against certificates uploaded tooAPI Management</span></span>

<span data-ttu-id="b10e8-115">Hello esempio seguente viene illustrato come identificazione personale hello toocheck di un certificato client con i certificati caricati tooAPI Management:</span><span class="sxs-lookup"><span data-stu-id="b10e8-115">hello following example shows how toocheck hello thumbprint of a client certificate against certificates uploaded tooAPI Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="b10e8-116">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="b10e8-116">Next step</span></span>

*  [<span data-ttu-id="b10e8-117">Servizi back-end toosecure tramite client come certificato di autenticazione</span><span class="sxs-lookup"><span data-stu-id="b10e8-117">How toosecure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="b10e8-118">La modalità certificati tooupload</span><span class="sxs-lookup"><span data-stu-id="b10e8-118">How tooupload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

