---
title: limiti per le richieste di gestione delle risorse aaaAzure | Documenti Microsoft
description: Viene descritto come toouse la limitazione delle richieste con Gestione risorse di Azure richiede quando sono stati raggiunti i limiti della sottoscrizione.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="50734-103">Limitazione delle richieste di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="50734-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="50734-104">Per ogni sottoscrizione e tenant, i limiti di gestione risorse richieste too15, 000 all'ora di lettura e scrittura richieste too1, 200 all'ora.</span><span class="sxs-lookup"><span data-stu-id="50734-104">For each subscription and tenant, Resource Manager limits read requests too15,000 per hour and write requests too1,200 per hour.</span></span> <span data-ttu-id="50734-105">Questi limiti si applicano tooeach istanza di gestione risorse di Azure. sono presenti più istanze in ogni area di Azure e Gestione risorse di Azure viene distribuito tooall Azure aree.</span><span class="sxs-lookup"><span data-stu-id="50734-105">These limits apply tooeach Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed tooall Azure regions.</span></span>  <span data-ttu-id="50734-106">Pertanto, in pratica, i limiti sono effettivamente molto superiori a quelli elencati in precedenza, poiché le richieste utente sono in genere gestite da molte istanze diverse.</span><span class="sxs-lookup"><span data-stu-id="50734-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="50734-107">Se l'applicazione o script raggiunge questi limiti, è necessario toothrottle le richieste.</span><span class="sxs-lookup"><span data-stu-id="50734-107">If your application or script reaches these limits, you need toothrottle your requests.</span></span> <span data-ttu-id="50734-108">Questo argomento viene illustrato come le richieste di hello toodetermine rimanente è prima di raggiungere il limite di hello e come toorespond quando è stato raggiunto il limite di hello.</span><span class="sxs-lookup"><span data-stu-id="50734-108">This topic shows you how toodetermine hello remaining requests you have before reaching hello limit, and how toorespond when you have reached hello limit.</span></span>

<span data-ttu-id="50734-109">Quando si raggiunge il limite di hello, viene visualizzato il codice di stato HTTP hello **429 troppe richieste molti**.</span><span class="sxs-lookup"><span data-stu-id="50734-109">When you reach hello limit, you receive hello HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="50734-110">numero di richieste di Hello è tooeither con ambito la sottoscrizione o il tenant.</span><span class="sxs-lookup"><span data-stu-id="50734-110">hello number of requests is scoped tooeither your subscription or your tenant.</span></span> <span data-ttu-id="50734-111">Se si dispone di più, applicazioni simultanee effettua richieste nella sottoscrizione, le richieste di hello da tali applicazioni vengono sommate numero hello toodetermine delle richieste rimanenti.</span><span class="sxs-lookup"><span data-stu-id="50734-111">If you have multiple, concurrent applications making requests in your subscription, hello requests from those applications are added together toodetermine hello number of remaining requests.</span></span>

<span data-ttu-id="50734-112">Le richieste di sottoscrizione con ambito sono quelli hello comportano passando l'id sottoscrizione, ad esempio il recupero dei gruppi di risorse hello nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="50734-112">Subscription scoped requests are ones hello involve passing your subscription id, such as retrieving hello resource groups in your subscription.</span></span> <span data-ttu-id="50734-113">Le richieste nell'ambito del tenant non includono l'ID sottoscrizione, ad esempio il recupero delle posizioni di Azure valide.</span><span class="sxs-lookup"><span data-stu-id="50734-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="50734-114">Richieste rimanenti</span><span class="sxs-lookup"><span data-stu-id="50734-114">Remaining requests</span></span>
<span data-ttu-id="50734-115">È possibile determinare il numero di hello delle richieste rimanenti esaminando le intestazioni di risposta.</span><span class="sxs-lookup"><span data-stu-id="50734-115">You can determine hello number of remaining requests by examining response headers.</span></span> <span data-ttu-id="50734-116">Ogni richiesta include i valori per il numero di hello delle richieste di scrittura e lettura rimanente.</span><span class="sxs-lookup"><span data-stu-id="50734-116">Each request includes values for hello number of remaining read and write requests.</span></span> <span data-ttu-id="50734-117">Hello nella tabella seguente vengono descritte le intestazioni di risposta hello che è possibile esaminare per i valori:</span><span class="sxs-lookup"><span data-stu-id="50734-117">hello following table describes hello response headers you can examine for those values:</span></span>

| <span data-ttu-id="50734-118">Intestazione risposta</span><span class="sxs-lookup"><span data-stu-id="50734-118">Response header</span></span> | <span data-ttu-id="50734-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="50734-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="50734-120">x-ms-ratelimit-remaining-subscription-reads</span><span class="sxs-lookup"><span data-stu-id="50734-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="50734-121">Richieste di lettura rimanenti nell'ambito della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="50734-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="50734-122">x-ms-ratelimit-remaining-subscription-writes</span><span class="sxs-lookup"><span data-stu-id="50734-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="50734-123">Richieste di scrittura rimanenti nell'ambito della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="50734-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="50734-124">x-ms-ratelimit-remaining-tenant-reads</span><span class="sxs-lookup"><span data-stu-id="50734-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="50734-125">Richieste di lettura rimanenti nell'ambito del tenant</span><span class="sxs-lookup"><span data-stu-id="50734-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="50734-126">x-ms-ratelimit-remaining-tenant-writes</span><span class="sxs-lookup"><span data-stu-id="50734-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="50734-127">Richieste di scrittura rimanenti nell'ambito del tenant</span><span class="sxs-lookup"><span data-stu-id="50734-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="50734-128">x-ms-ratelimit-remaining-subscription-resource-requests</span><span class="sxs-lookup"><span data-stu-id="50734-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="50734-129">Richieste di tipo di risorsa rimanenti nell'ambito della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="50734-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="50734-130">Il valore dell'intestazione viene restituito solo se un servizio ha eseguito l'override di limite predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="50734-130">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="50734-131">Gestione risorse aggiunge questo valore anziché hello sottoscrizione letture o scritture.</span><span class="sxs-lookup"><span data-stu-id="50734-131">Resource Manager adds this value instead of hello subscription reads or writes.</span></span> |
| <span data-ttu-id="50734-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="50734-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="50734-133">Richieste di raccolta di tipo di risorsa rimanenti nell'ambito della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="50734-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="50734-134">Il valore dell'intestazione viene restituito solo se un servizio ha eseguito l'override di limite predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="50734-134">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="50734-135">Questo valore fornisce il numero di hello di richieste di raccolta rimanenti (risorse elenco).</span><span class="sxs-lookup"><span data-stu-id="50734-135">This value provides hello number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="50734-136">x-ms-ratelimit-remaining-tenant-resource-requests</span><span class="sxs-lookup"><span data-stu-id="50734-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="50734-137">Richieste di tipo di risorsa rimanenti nell'ambito del tenant.</span><span class="sxs-lookup"><span data-stu-id="50734-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="50734-138">Questa intestazione viene aggiunto solo per le richieste a livello di tenant, e solo se un servizio ha eseguito l'override limite predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="50734-138">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> <span data-ttu-id="50734-139">Gestione risorse aggiunge questo valore anziché hello tenant letture o scritture.</span><span class="sxs-lookup"><span data-stu-id="50734-139">Resource Manager adds this value instead of hello tenant reads or writes.</span></span> |
| <span data-ttu-id="50734-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="50734-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="50734-141">Richieste di raccolta di tipo di risorsa rimanenti nell'ambito del tenant.</span><span class="sxs-lookup"><span data-stu-id="50734-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="50734-142">Questa intestazione viene aggiunto solo per le richieste a livello di tenant, e solo se un servizio ha eseguito l'override limite predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="50734-142">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> |

## <a name="retrieving-hello-header-values"></a><span data-ttu-id="50734-143">Il recupero dei valori di intestazione hello</span><span class="sxs-lookup"><span data-stu-id="50734-143">Retrieving hello header values</span></span>
<span data-ttu-id="50734-144">Il recupero di questi valori di intestazione nel codice o nello script non è diverso rispetto al recupero di qualsiasi valore di intestazione.</span><span class="sxs-lookup"><span data-stu-id="50734-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="50734-145">Ad esempio, in **c#**, si recupera il valore di intestazione hello da un **HttpWebResponse** oggetto denominato **risposta** con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="50734-145">For example, in **C#**, you retrieve hello header value from an **HttpWebResponse** object named **response** with hello following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="50734-146">In **PowerShell**, recuperare il valore dell'intestazione hello un'operazione Invoke-WebRequest.</span><span class="sxs-lookup"><span data-stu-id="50734-146">In **PowerShell**, you retrieve hello header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="50734-147">In alternativa, se desidera toosee hello rimanenti richieste per il debug, è possibile fornire hello **-Debug** parametro il **PowerShell** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="50734-147">Or, if want toosee hello remaining requests for debugging, you can provide hello **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="50734-148">Restituisce molti valori, inclusi hello il valore di risposta seguente:</span><span class="sxs-lookup"><span data-stu-id="50734-148">Which returns many values, including hello following response value:</span></span>

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

<span data-ttu-id="50734-149">In **CLI di Azure**, si recupera il valore dell'intestazione hello utilizzando hello opzione più dettagliato.</span><span class="sxs-lookup"><span data-stu-id="50734-149">In **Azure CLI**, you retrieve hello header value by using hello more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="50734-150">Restituisce molti valori, inclusi hello seguente oggetto:</span><span class="sxs-lookup"><span data-stu-id="50734-150">Which returns many values, including hello following object:</span></span>

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="50734-151">Attesa prima dell'invio della richiesta successiva</span><span class="sxs-lookup"><span data-stu-id="50734-151">Waiting before sending next request</span></span>
<span data-ttu-id="50734-152">Quando si raggiunge il limite di richieste di hello, Gestione risorse restituisce hello **429** codice di stato HTTP e un **Retry-After** valore nell'intestazione di hello.</span><span class="sxs-lookup"><span data-stu-id="50734-152">When you reach hello request limit, Resource Manager returns hello **429** HTTP status code and a **Retry-After** value in hello header.</span></span> <span data-ttu-id="50734-153">Hello **Retry-After** valore specifica il numero di hello di secondi di attesa dell'applicazione (o sospensione) prima di inviare la richiesta successiva hello.</span><span class="sxs-lookup"><span data-stu-id="50734-153">hello **Retry-After** value specifies hello number of seconds your application should wait (or sleep) before sending hello next request.</span></span> <span data-ttu-id="50734-154">Se si invia una richiesta prima che sia trascorso il valore di retry hello, non è possibile elaborare la richiesta e viene restituito un nuovo valore dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="50734-154">If you send a request before hello retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50734-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="50734-155">Next steps</span></span>

* <span data-ttu-id="50734-156">Per altre informazioni sui limiti e quote, vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="50734-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="50734-157">toolearn sulla gestione di richieste REST asincrone, vedere [tenere traccia delle operazioni asincrone di Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="50734-157">toolearn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
