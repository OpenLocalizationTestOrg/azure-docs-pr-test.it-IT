---
title: Operazioni asincrone in Azure |Microsoft Docs
description: Viene descritto come tenere traccia delle operazioni asincrone in Azure.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: 9fe3d98cd345aae45722295b6c1b7fc3e9036e95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="a0d38-103">Tenere traccia delle operazioni asincrone</span><span class="sxs-lookup"><span data-stu-id="a0d38-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="a0d38-104">Alcune operazioni REST in Azure vengono eseguite in modo asincrono perché non è possibile completarle rapidamente.</span><span class="sxs-lookup"><span data-stu-id="a0d38-104">Some Azure REST operations run asynchronously because the operation cannot be completed quickly.</span></span> <span data-ttu-id="a0d38-105">In questo articolo viene descritto come tenere traccia dello stato delle operazioni asincrone tramite i valori restituiti nella risposta.</span><span class="sxs-lookup"><span data-stu-id="a0d38-105">This topic describes how to track the status of asynchronous operations through values returned in the response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="a0d38-106">Codici di stato per le operazioni asincrone</span><span class="sxs-lookup"><span data-stu-id="a0d38-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="a0d38-107">Inizialmente, un'operazione asincrona restituisce un codice di stato HTTP del tipo:</span><span class="sxs-lookup"><span data-stu-id="a0d38-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="a0d38-108">201 (Creato) oppure</span><span class="sxs-lookup"><span data-stu-id="a0d38-108">201 (Created)</span></span>
* <span data-ttu-id="a0d38-109">202 (Accettato)</span><span class="sxs-lookup"><span data-stu-id="a0d38-109">202 (Accepted)</span></span> 

<span data-ttu-id="a0d38-110">Quando l'operazione viene completata correttamente, viene restituito uno dei codici seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0d38-110">When the operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="a0d38-111">200 (OK)</span><span class="sxs-lookup"><span data-stu-id="a0d38-111">200 (OK)</span></span>
* <span data-ttu-id="a0d38-112">204 (No Content (Nessun contenuto))</span><span class="sxs-lookup"><span data-stu-id="a0d38-112">204 (No Content)</span></span> 

<span data-ttu-id="a0d38-113">Consultare la [documentazione dell'API REST](/rest/api/) per visualizzare le risposte dell'operazione in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a0d38-113">Refer to the [REST API documentation](/rest/api/) to see the responses for the operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="a0d38-114">Monitorare lo stato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="a0d38-114">Monitor status of operation</span></span>
<span data-ttu-id="a0d38-115">Le operazioni REST asincrone restituiscono i valori di intestazione, che consentono di determinare lo stato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="a0d38-115">The asynchronous REST operations return header values, which you use to determine the status of the operation.</span></span> <span data-ttu-id="a0d38-116">Potenzialmente esistono tre valori di intestazione da esaminare:</span><span class="sxs-lookup"><span data-stu-id="a0d38-116">There are potentially three header values to examine:</span></span>

* <span data-ttu-id="a0d38-117">`Azure-AsyncOperation` -URL per verificare lo stato attuale dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="a0d38-117">`Azure-AsyncOperation` - URL for checking the ongoing status of the operation.</span></span> <span data-ttu-id="a0d38-118">Se l'operazione restituisce questo valore, usarlo sempre (al posto di Location) per tenere traccia dello stato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="a0d38-118">If your operation returns this value, always use it (instead of Location) to track the status of the operation.</span></span>
* <span data-ttu-id="a0d38-119">`Location` -URL per determinare quando un'operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="a0d38-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="a0d38-120">Usare questo valore solo quando non viene restituito Azure-AsyncOperation.</span><span class="sxs-lookup"><span data-stu-id="a0d38-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="a0d38-121">`Retry-After` -Il numero di secondi di attesa prima di controllare lo stato dell'operazione asincrona.</span><span class="sxs-lookup"><span data-stu-id="a0d38-121">`Retry-After` - The number of seconds to wait before checking the status of the asynchronous operation.</span></span>

<span data-ttu-id="a0d38-122">Tuttavia, non tutte le operazioni asincrone restituiscono tutti questi valori.</span><span class="sxs-lookup"><span data-stu-id="a0d38-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="a0d38-123">Ad esempio, potrebbe essere necessario valutare il valore d'intestazione Azure-AsyncOperation per un'operazione e il valore d'intestazione Location per un'altra.</span><span class="sxs-lookup"><span data-stu-id="a0d38-123">For example, you may need to evaluate the Azure-AsyncOperation header value for one operation, and the Location header value for another operation.</span></span> 

<span data-ttu-id="a0d38-124">È possibile recuperare i valori d'intestazione eseguendo le stesse operazioni necessarie per il recupero di un valore d'intestazione qualsiasi di una richiesta.</span><span class="sxs-lookup"><span data-stu-id="a0d38-124">You retrieve the header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="a0d38-125">Ad esempio, in C# il valore d'intestazione viene recuperato da un oggetto `HttpWebResponse` denominato `response` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="a0d38-125">For example, in C#, you retrieve the header value from an `HttpWebResponse` object named `response` with the following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="a0d38-126">Richiesta e risposta di Azure AsyncOperation</span><span class="sxs-lookup"><span data-stu-id="a0d38-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="a0d38-127">Per ottenere lo stato dell'operazione asincrona, inviare una richiesta GET all'URL nel valore d'intestazione Azure-AsyncOperation.</span><span class="sxs-lookup"><span data-stu-id="a0d38-127">To get the status of the asynchronous operation, send a GET request to the URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="a0d38-128">Il corpo della risposta di questa operazione contiene le informazioni sull'operazione.</span><span class="sxs-lookup"><span data-stu-id="a0d38-128">The body of the response from this operation contains information about the operation.</span></span> <span data-ttu-id="a0d38-129">L'esempio seguente mostra i possibili valori restituiti dall'operazione:</span><span class="sxs-lookup"><span data-stu-id="a0d38-129">The following example shows the possible values returned from the operation:</span></span>

```json
{
    "id": "{resource path from GET operation}",
    "name": "{operation-id}", 
    "status" : "Succeeded | Failed | Canceled | {resource provider values}", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
    "percentComplete": {double between 0 and 100 },
    "properties": {
        /* Specific resource provider values for successful operations */
    },
    "error" : { 
        "code": "{error code}",  
        "message": "{error description}" 
    }
}
```

<span data-ttu-id="a0d38-130">Solo `status` viene restituito per tutte le risposte.</span><span class="sxs-lookup"><span data-stu-id="a0d38-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="a0d38-131">L'oggetto errore viene restituito quando lo stato è Operazione non riuscita oppure Operazione annullata.</span><span class="sxs-lookup"><span data-stu-id="a0d38-131">The error object is returned when the status is Failed or Canceled.</span></span> <span data-ttu-id="a0d38-132">Tutti gli altri valori sono facoltativi, pertanto la risposta che si riceve potrebbe presentare alcune differenze rispetto all'esempio.</span><span class="sxs-lookup"><span data-stu-id="a0d38-132">All other values are optional; therefore, the response you receive may look different than the example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="a0d38-133">Valori provisioningState</span><span class="sxs-lookup"><span data-stu-id="a0d38-133">provisioningState values</span></span>

<span data-ttu-id="a0d38-134">Le operazioni di creazione, aggiornamento o eliminazione (INSERISCI, PATCH, ELIMINA) di una risorsa restituiscono in genere un valore `provisioningState`.</span><span class="sxs-lookup"><span data-stu-id="a0d38-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="a0d38-135">Quando un'operazione viene completata, viene restituito uno dei tre valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0d38-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="a0d38-136">Operazione riuscita</span><span class="sxs-lookup"><span data-stu-id="a0d38-136">Succeeded</span></span>
* <span data-ttu-id="a0d38-137">Operazione non riuscita</span><span class="sxs-lookup"><span data-stu-id="a0d38-137">Failed</span></span>
* <span data-ttu-id="a0d38-138">Canceled</span><span class="sxs-lookup"><span data-stu-id="a0d38-138">Canceled</span></span>

<span data-ttu-id="a0d38-139">Tutti gli altri valori indicano che l'operazione è ancora in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a0d38-139">All other values indicate the operation is still running.</span></span> <span data-ttu-id="a0d38-140">Il provider di risorse può restituire un valore personalizzato che indica lo stato.</span><span class="sxs-lookup"><span data-stu-id="a0d38-140">The resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="a0d38-141">Ad esempio, potrebbe essere visualizzato **Accettato** quando la richiesta è stata ricevuta ed è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a0d38-141">For example, you may receive **Accepted** when the request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="a0d38-142">Esempi di richieste e risposte</span><span class="sxs-lookup"><span data-stu-id="a0d38-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="a0d38-143">Avviare la macchina virtuale (202 con Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="a0d38-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="a0d38-144">In questo esempio viene illustrato come determinare lo stato dell'operazione di **avvio** per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="a0d38-144">This example shows how to determine the status of **start** operation for virtual machines.</span></span> <span data-ttu-id="a0d38-145">La richiesta iniziale è nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="a0d38-145">The initial request is in the following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="a0d38-146">Restituisce il codice di stato 202.</span><span class="sxs-lookup"><span data-stu-id="a0d38-146">It returns status code 202.</span></span> <span data-ttu-id="a0d38-147">Tra i valori di intestazione compare:</span><span class="sxs-lookup"><span data-stu-id="a0d38-147">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="a0d38-148">Per controllare lo stato dell'operazione asincrona, inviare un'altra richiesta all'URL.</span><span class="sxs-lookup"><span data-stu-id="a0d38-148">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="a0d38-149">Il corpo della risposta contiene lo stato dell'operazione:</span><span class="sxs-lookup"><span data-stu-id="a0d38-149">The response body contains the status of the operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="a0d38-150">Distribuzione delle risorse (201 con Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="a0d38-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="a0d38-151">In questo esempio viene illustrato come determinare lo stato dell'operazione di **distribuzione** per la distribuzione delle risorse in Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d38-151">This example shows how to determine the status of **deployments** operation for deploying resources to Azure.</span></span> <span data-ttu-id="a0d38-152">La richiesta iniziale è nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="a0d38-152">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="a0d38-153">Restituisce il codice di stato 201.</span><span class="sxs-lookup"><span data-stu-id="a0d38-153">It returns status code 201.</span></span> <span data-ttu-id="a0d38-154">Il corpo della risposta include:</span><span class="sxs-lookup"><span data-stu-id="a0d38-154">The body of the response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="a0d38-155">Tra i valori di intestazione compare:</span><span class="sxs-lookup"><span data-stu-id="a0d38-155">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="a0d38-156">Per controllare lo stato dell'operazione asincrona, inviare un'altra richiesta all'URL.</span><span class="sxs-lookup"><span data-stu-id="a0d38-156">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="a0d38-157">Il corpo della risposta contiene lo stato dell'operazione:</span><span class="sxs-lookup"><span data-stu-id="a0d38-157">The response body contains the status of the operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="a0d38-158">Al termine della distribuzione, la risposta contiene:</span><span class="sxs-lookup"><span data-stu-id="a0d38-158">When the deployment is finished, the response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="a0d38-159">Creazione di un account di archiviazione (202 con Location e Retry-After)</span><span class="sxs-lookup"><span data-stu-id="a0d38-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="a0d38-160">In questo esempio viene illustrato come determinare lo stato dell'operazione di **creazione** per gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a0d38-160">This example shows how to determine the status of the **create** operation for storage accounts.</span></span> <span data-ttu-id="a0d38-161">La richiesta iniziale è nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="a0d38-161">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="a0d38-162">Il corpo della richiesta contiene le proprietà dell'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="a0d38-162">And the request body contains properties for the storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="a0d38-163">Restituisce il codice di stato 202.</span><span class="sxs-lookup"><span data-stu-id="a0d38-163">It returns status code 202.</span></span> <span data-ttu-id="a0d38-164">Tra i valori di intestazione, vengono visualizzati i due valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0d38-164">Among the header values, you see the following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="a0d38-165">Dopo aver atteso il numero di secondi specificato in Retry-After, verificare lo stato dell'operazione asincrona inviando un'altra richiesta all'URL.</span><span class="sxs-lookup"><span data-stu-id="a0d38-165">After waiting for number of seconds specified in Retry-After, check the status of the asynchronous operation by sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="a0d38-166">Se la richiesta è ancora in esecuzione, viene visualizzato il codice di stato 202.</span><span class="sxs-lookup"><span data-stu-id="a0d38-166">If the request is still running, you receive a status code 202.</span></span> <span data-ttu-id="a0d38-167">Se la richiesta è stata completata, viene visualizzato il codice di stato 200 e il corpo della risposta contiene le proprietà dell'account di archiviazione che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="a0d38-167">If the request has completed, your receive a status code 200, and the body of the response contains the properties of the storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0d38-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a0d38-168">Next steps</span></span>

* <span data-ttu-id="a0d38-169">Per la documentazione relativa a ogni operazione REST, consultare la [documentazione dell'API REST](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="a0d38-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="a0d38-170">Per informazioni sulla gestione delle risorse tramite Gestione risorse dell'API REST, consultare [Using the Resource Manager REST API](resource-manager-rest-api.md) (Uso di Gestione risorse dell'API REST).</span><span class="sxs-lookup"><span data-stu-id="a0d38-170">For information about managing resources through the Resource Manager REST API, see [Using the Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="a0d38-171">Per informazioni sui modelli di distribuzione tramite la Gestione risorse dell'API REST, vedere [Distribuire le risorse con i modelli e l'API REST di Gestione risorse](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="a0d38-171">for information about deploying templates through the Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>