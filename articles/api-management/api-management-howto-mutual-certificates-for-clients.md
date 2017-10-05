---
title: Proteggere le API usando l'autenticazione con certificato client in Gestione API - Gestione API di Azure | Documentazione Microsoft
description: Informazioni su come proteggere l'accesso alle API usando i certificati client
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
ms.openlocfilehash: d3d51d0575a6d2dacced931601d48eb1e51a4051
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="075f0-103">Come proteggere le API usando l'autenticazione con certificati client in Gestione API</span><span class="sxs-lookup"><span data-stu-id="075f0-103">How to secure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="075f0-104">Gestione API offre la possibilità di proteggere l'accesso alle API (ovvero dal client a Gestione API) mediante certificati client.</span><span class="sxs-lookup"><span data-stu-id="075f0-104">API Management provides the capability to secure access to APIs (i.e., client to API Management) using client certificates.</span></span> <span data-ttu-id="075f0-105">Attualmente è possibile controllare l'identificazione personale del certificato client rispetto a un valore desiderato.</span><span class="sxs-lookup"><span data-stu-id="075f0-105">Currently, you can check the thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="075f0-106">È inoltre possibile controllare l'identificazione personale rispetto a certificati esistenti caricati in Gestione API.</span><span class="sxs-lookup"><span data-stu-id="075f0-106">You can also check the thumbprint against existing certificates uploaded to API Management.</span></span>  

<span data-ttu-id="075f0-107">Per informazioni sulla protezione dell'accesso al servizio back-end di un'API tramite certificati client (ovvero da Gestione API al back-end), vedere [Come proteggere i servizi back-end usando l'autenticazione con certificati client](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span><span class="sxs-lookup"><span data-stu-id="075f0-107">For information about securing access to the back-end service of an API using client certificates (i.e., API Management to back-end), see [How to secure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-the-expiration-date"></a><span data-ttu-id="075f0-108">Controllo della data di scadenza</span><span class="sxs-lookup"><span data-stu-id="075f0-108">Checking the expiration date</span></span>

<span data-ttu-id="075f0-109">È possibile configurare i criteri riportati di seguito per controllare se il certificato è scaduto:</span><span class="sxs-lookup"><span data-stu-id="075f0-109">Below policies can be configured to check if the certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-issuer-and-subject"></a><span data-ttu-id="075f0-110">Controllo dell'autorità di certificazione e del soggetto</span><span class="sxs-lookup"><span data-stu-id="075f0-110">Checking the issuer and subject</span></span>

<span data-ttu-id="075f0-111">È possibile configurare i criteri riportati di seguito per controllare l'autorità di certificazione e il soggetto di un certificato client:</span><span class="sxs-lookup"><span data-stu-id="075f0-111">Below policies can be configured to check the issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-thumbprint"></a><span data-ttu-id="075f0-112">Controllo dell'identificazione personale</span><span class="sxs-lookup"><span data-stu-id="075f0-112">Checking the thumbprint</span></span>

<span data-ttu-id="075f0-113">I criteri riportati di seguito possono essere configurati per controllare l'identificazione personale del certificato client:</span><span class="sxs-lookup"><span data-stu-id="075f0-113">Below policies can be configured to check the thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-to-api-management"></a><span data-ttu-id="075f0-114">Controllo di un'identificazione personale rispetto a certificati caricati in Gestione API</span><span class="sxs-lookup"><span data-stu-id="075f0-114">Checking a thumbprint against certificates uploaded to API Management</span></span>

<span data-ttu-id="075f0-115">L'esempio seguente illustra come controllare l'identificazione personale di un certificato client rispetto a certificati caricati in Gestione API:</span><span class="sxs-lookup"><span data-stu-id="075f0-115">The following example shows how to check the thumbprint of a client certificate against certificates uploaded to API Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="075f0-116">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="075f0-116">Next step</span></span>

*  [<span data-ttu-id="075f0-117">Come proteggere i servizi back-end usando l'autenticazione con certificati client</span><span class="sxs-lookup"><span data-stu-id="075f0-117">How to secure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="075f0-118">Come caricare i certificati</span><span class="sxs-lookup"><span data-stu-id="075f0-118">How to upload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

