---
title: Limiti di richieste di Azure Resource Manager | Microsoft Docs
description: Viene descritto come usare la limitazione con le richieste di Azure Resource Manager quando sono stati raggiunti i limiti di sottoscrizioni.
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
ms.openlocfilehash: 6d7eeaf460674c3ab98425a5412ffa465b9ffd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="27384-103">Limitazione delle richieste di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="27384-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="27384-104">Per ogni sottoscrizione e tenant, Resource Manager definisce un limite di 15.000 richieste di lettura e 1.200 richieste di scrittura al giorno.</span><span class="sxs-lookup"><span data-stu-id="27384-104">For each subscription and tenant, Resource Manager limits read requests to 15,000 per hour and write requests to 1,200 per hour.</span></span> <span data-ttu-id="27384-105">Questi limiti si applicano a ogni istanza di Azure Resource Manager; sono presenti più istanze in ogni area di Azure e Azure Resource Manager viene distribuito a tutte le aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="27384-105">These limits apply to each Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed to all Azure regions.</span></span>  <span data-ttu-id="27384-106">Pertanto, in pratica, i limiti sono effettivamente molto superiori a quelli elencati in precedenza, poiché le richieste utente sono in genere gestite da molte istanze diverse.</span><span class="sxs-lookup"><span data-stu-id="27384-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="27384-107">Se l'applicazione o script raggiunge questi limiti, è necessario restringere le richieste.</span><span class="sxs-lookup"><span data-stu-id="27384-107">If your application or script reaches these limits, you need to throttle your requests.</span></span> <span data-ttu-id="27384-108">In questo argomento viene illustrato come determinare il numero di richieste rimanenti prima di raggiungere il limite e come rispondere in caso di raggiungimento.</span><span class="sxs-lookup"><span data-stu-id="27384-108">This topic shows you how to determine the remaining requests you have before reaching the limit, and how to respond when you have reached the limit.</span></span>

<span data-ttu-id="27384-109">Quando si raggiunge il limite, viene visualizzato il codice di stato HTTP **429 Too many requests** (429 Troppe richieste).</span><span class="sxs-lookup"><span data-stu-id="27384-109">When you reach the limit, you receive the HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="27384-110">Il numero di richieste ha come ambito la sottoscrizione o il tenant.</span><span class="sxs-lookup"><span data-stu-id="27384-110">The number of requests is scoped to either your subscription or your tenant.</span></span> <span data-ttu-id="27384-111">Se si dispone di più applicazioni simultanee che effettuano richieste nella sottoscrizione, le richieste da tali applicazioni vengono aggiunte insieme in modo da determinare il numero di richieste rimanenti.</span><span class="sxs-lookup"><span data-stu-id="27384-111">If you have multiple, concurrent applications making requests in your subscription, the requests from those applications are added together to determine the number of remaining requests.</span></span>

<span data-ttu-id="27384-112">Per le richieste nell'ambito della sottoscrizione occorre la trasmissione dell'ID sottoscrizione, ad esempio il recupero del gruppo di risorse nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="27384-112">Subscription scoped requests are ones the involve passing your subscription id, such as retrieving the resource groups in your subscription.</span></span> <span data-ttu-id="27384-113">Le richieste nell'ambito del tenant non includono l'ID sottoscrizione, ad esempio il recupero delle posizioni di Azure valide.</span><span class="sxs-lookup"><span data-stu-id="27384-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="27384-114">Richieste rimanenti</span><span class="sxs-lookup"><span data-stu-id="27384-114">Remaining requests</span></span>
<span data-ttu-id="27384-115">È possibile determinare il numero di richieste rimanenti esaminando le intestazioni di risposta.</span><span class="sxs-lookup"><span data-stu-id="27384-115">You can determine the number of remaining requests by examining response headers.</span></span> <span data-ttu-id="27384-116">Ogni richiesta include i valori per il numero di richieste di scrittura e lettura rimanenti.</span><span class="sxs-lookup"><span data-stu-id="27384-116">Each request includes values for the number of remaining read and write requests.</span></span> <span data-ttu-id="27384-117">Nella tabella seguente vengono descritte le intestazioni di risposta che è possibile esaminare per tali valori:</span><span class="sxs-lookup"><span data-stu-id="27384-117">The following table describes the response headers you can examine for those values:</span></span>

| <span data-ttu-id="27384-118">Intestazione risposta</span><span class="sxs-lookup"><span data-stu-id="27384-118">Response header</span></span> | <span data-ttu-id="27384-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="27384-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="27384-120">x-ms-ratelimit-remaining-subscription-reads</span><span class="sxs-lookup"><span data-stu-id="27384-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="27384-121">Richieste di lettura rimanenti nell'ambito della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="27384-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="27384-122">x-ms-ratelimit-remaining-subscription-writes</span><span class="sxs-lookup"><span data-stu-id="27384-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="27384-123">Richieste di scrittura rimanenti nell'ambito della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="27384-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="27384-124">x-ms-ratelimit-remaining-tenant-reads</span><span class="sxs-lookup"><span data-stu-id="27384-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="27384-125">Richieste di lettura rimanenti nell'ambito del tenant</span><span class="sxs-lookup"><span data-stu-id="27384-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="27384-126">x-ms-ratelimit-remaining-tenant-writes</span><span class="sxs-lookup"><span data-stu-id="27384-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="27384-127">Richieste di scrittura rimanenti nell'ambito del tenant</span><span class="sxs-lookup"><span data-stu-id="27384-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="27384-128">x-ms-ratelimit-remaining-subscription-resource-requests</span><span class="sxs-lookup"><span data-stu-id="27384-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="27384-129">Richieste di tipo di risorsa rimanenti nell'ambito della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="27384-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="27384-130">Questo valore di intestazione viene restituito solo se un servizio ha superato il limite predefinito.</span><span class="sxs-lookup"><span data-stu-id="27384-130">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="27384-131">Resource Manager aggiunge questo valore invece delle richieste di lettura o scrittura per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="27384-131">Resource Manager adds this value instead of the subscription reads or writes.</span></span> |
| <span data-ttu-id="27384-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="27384-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="27384-133">Richieste di raccolta di tipo di risorsa rimanenti nell'ambito della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="27384-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="27384-134">Questo valore di intestazione viene restituito solo se un servizio ha superato il limite predefinito.</span><span class="sxs-lookup"><span data-stu-id="27384-134">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="27384-135">Questo valore fornisce il numero di richieste di raccolta rimanenti (elenco di risorse).</span><span class="sxs-lookup"><span data-stu-id="27384-135">This value provides the number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="27384-136">x-ms-ratelimit-remaining-tenant-resource-requests</span><span class="sxs-lookup"><span data-stu-id="27384-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="27384-137">Richieste di tipo di risorsa rimanenti nell'ambito del tenant.</span><span class="sxs-lookup"><span data-stu-id="27384-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="27384-138">Questa intestazione viene aggiunta solo per le richieste a livello di tenant e solo se un sevizio ha superato il limite predefinito.</span><span class="sxs-lookup"><span data-stu-id="27384-138">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> <span data-ttu-id="27384-139">Resource Manager aggiunge questo valore invece delle richieste di lettura o scrittura per il tenant.</span><span class="sxs-lookup"><span data-stu-id="27384-139">Resource Manager adds this value instead of the tenant reads or writes.</span></span> |
| <span data-ttu-id="27384-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="27384-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="27384-141">Richieste di raccolta di tipo di risorsa rimanenti nell'ambito del tenant.</span><span class="sxs-lookup"><span data-stu-id="27384-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="27384-142">Questa intestazione viene aggiunta solo per le richieste a livello di tenant e solo se un sevizio ha superato il limite predefinito.</span><span class="sxs-lookup"><span data-stu-id="27384-142">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> |

## <a name="retrieving-the-header-values"></a><span data-ttu-id="27384-143">Recupero dei valori di intestazione</span><span class="sxs-lookup"><span data-stu-id="27384-143">Retrieving the header values</span></span>
<span data-ttu-id="27384-144">Il recupero di questi valori di intestazione nel codice o nello script non è diverso rispetto al recupero di qualsiasi valore di intestazione.</span><span class="sxs-lookup"><span data-stu-id="27384-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="27384-145">Ad esempio, in **C#** viene recuperato il valore di intestazione da un oggetto **HttpWebResponse** di nome **response** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="27384-145">For example, in **C#**, you retrieve the header value from an **HttpWebResponse** object named **response** with the following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="27384-146">In **PowerShell** viene recuperato il valore di intestazione da un'operazione Invoke-WebRequest.</span><span class="sxs-lookup"><span data-stu-id="27384-146">In **PowerShell**, you retrieve the header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="27384-147">In alternativa, se desidera visualizzare le richieste rimanenti per il debug, è possibile fornire il parametro **-Debug** nel cmdlet **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="27384-147">Or, if want to see the remaining requests for debugging, you can provide the **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="27384-148">Tale parametro restituisce molti valori, incluso il valore di risposta seguente:</span><span class="sxs-lookup"><span data-stu-id="27384-148">Which returns many values, including the following response value:</span></span>

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

<span data-ttu-id="27384-149">In **Interfaccia della riga di comando di Azure** il valore di intestazione viene recuperato tramite l'opzione più dettagliata.</span><span class="sxs-lookup"><span data-stu-id="27384-149">In **Azure CLI**, you retrieve the header value by using the more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="27384-150">Tale opzione restituisce numerosi valori, inclusi l'oggetto seguente:</span><span class="sxs-lookup"><span data-stu-id="27384-150">Which returns many values, including the following object:</span></span>

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

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="27384-151">Attesa prima dell'invio della richiesta successiva</span><span class="sxs-lookup"><span data-stu-id="27384-151">Waiting before sending next request</span></span>
<span data-ttu-id="27384-152">Quando si raggiunge il limite di richieste, Resource Manager restituisce il codice di stato HTTP **429** e un valore **Retry-After** nell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="27384-152">When you reach the request limit, Resource Manager returns the **429** HTTP status code and a **Retry-After** value in the header.</span></span> <span data-ttu-id="27384-153">Il valore **Retry-After** specifica il numero di secondi durante i quali l'applicazione deve attendere (o restare in sospensione) prima di inviare la richiesta successiva.</span><span class="sxs-lookup"><span data-stu-id="27384-153">The **Retry-After** value specifies the number of seconds your application should wait (or sleep) before sending the next request.</span></span> <span data-ttu-id="27384-154">Se si invia una richiesta prima che sia trascorso il valore per la ripetizione del tentativo, la richiesta non viene elaborata e viene restituito un nuovo valore per la ripetizione del tentativo.</span><span class="sxs-lookup"><span data-stu-id="27384-154">If you send a request before the retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27384-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="27384-155">Next steps</span></span>

* <span data-ttu-id="27384-156">Per altre informazioni sui limiti e quote, vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="27384-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="27384-157">Per altre informazioni sulla gestione delle richieste REST asincrone, vedere [Track asynchronous Azure operations](resource-manager-async-operations.md) (Tenere traccia delle operazioni asincrone di Azure).</span><span class="sxs-lookup"><span data-stu-id="27384-157">To learn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
