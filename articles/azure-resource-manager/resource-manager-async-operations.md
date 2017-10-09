---
title: operazioni asincrone aaaAzure | Documenti Microsoft
description: Viene descritto come tootrack di operazioni asincrone in Azure.
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
ms.openlocfilehash: b81254196013adf87998eff11a50993efa52d40d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="61d92-103">Tenere traccia delle operazioni asincrone</span><span class="sxs-lookup"><span data-stu-id="61d92-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="61d92-104">Alcune operazioni REST di Azure eseguiti in modo asincrono perché non è possibile completare l'operazione di hello rapidamente.</span><span class="sxs-lookup"><span data-stu-id="61d92-104">Some Azure REST operations run asynchronously because hello operation cannot be completed quickly.</span></span> <span data-ttu-id="61d92-105">In questo argomento viene descritto come stato di hello tootrack delle operazioni asincrone tramite i valori restituiti nella risposta hello.</span><span class="sxs-lookup"><span data-stu-id="61d92-105">This topic describes how tootrack hello status of asynchronous operations through values returned in hello response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="61d92-106">Codici di stato per le operazioni asincrone</span><span class="sxs-lookup"><span data-stu-id="61d92-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="61d92-107">Inizialmente, un'operazione asincrona restituisce un codice di stato HTTP del tipo:</span><span class="sxs-lookup"><span data-stu-id="61d92-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="61d92-108">201 (Creato) oppure</span><span class="sxs-lookup"><span data-stu-id="61d92-108">201 (Created)</span></span>
* <span data-ttu-id="61d92-109">202 (Accettato)</span><span class="sxs-lookup"><span data-stu-id="61d92-109">202 (Accepted)</span></span> 

<span data-ttu-id="61d92-110">Quando l'operazione hello è stata completata correttamente, viene restituito uno:</span><span class="sxs-lookup"><span data-stu-id="61d92-110">When hello operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="61d92-111">200 (OK)</span><span class="sxs-lookup"><span data-stu-id="61d92-111">200 (OK)</span></span>
* <span data-ttu-id="61d92-112">204 (No Content (Nessun contenuto))</span><span class="sxs-lookup"><span data-stu-id="61d92-112">204 (No Content)</span></span> 

<span data-ttu-id="61d92-113">Fare riferimento toohello [documentazione dell'API REST](/rest/api/) risposte hello toosee per l'operazione di hello in caso di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="61d92-113">Refer toohello [REST API documentation](/rest/api/) toosee hello responses for hello operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="61d92-114">Monitorare lo stato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="61d92-114">Monitor status of operation</span></span>
<span data-ttu-id="61d92-115">Hello asincrona REST operazioni restituiti valori di intestazione, cui è stato hello toodetermine di hello operazione.</span><span class="sxs-lookup"><span data-stu-id="61d92-115">hello asynchronous REST operations return header values, which you use toodetermine hello status of hello operation.</span></span> <span data-ttu-id="61d92-116">Esistono potenzialmente tooexamine di intestazione tre valori:</span><span class="sxs-lookup"><span data-stu-id="61d92-116">There are potentially three header values tooexamine:</span></span>

* <span data-ttu-id="61d92-117">`Azure-AsyncOperation`-URL per controllare lo stato in corso di hello dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="61d92-117">`Azure-AsyncOperation` - URL for checking hello ongoing status of hello operation.</span></span> <span data-ttu-id="61d92-118">Se l'operazione restituisce questo valore, utilizzare sempre lo stato di hello tootrack it (anziché percorso) dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="61d92-118">If your operation returns this value, always use it (instead of Location) tootrack hello status of hello operation.</span></span>
* <span data-ttu-id="61d92-119">`Location` -URL per determinare quando un'operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="61d92-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="61d92-120">Usare questo valore solo quando non viene restituito Azure-AsyncOperation.</span><span class="sxs-lookup"><span data-stu-id="61d92-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="61d92-121">`Retry-After`-hello numero di secondi toowait prima di archiviare lo stato di hello dell'operazione asincrona di hello.</span><span class="sxs-lookup"><span data-stu-id="61d92-121">`Retry-After` - hello number of seconds toowait before checking hello status of hello asynchronous operation.</span></span>

<span data-ttu-id="61d92-122">Tuttavia, non tutte le operazioni asincrone restituiscono tutti questi valori.</span><span class="sxs-lookup"><span data-stu-id="61d92-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="61d92-123">Ad esempio, potrebbe essere il valore dell'intestazione tooevaluate hello Azure AsyncOperation per un'operazione e valore dell'intestazione Location hello per un'altra operazione.</span><span class="sxs-lookup"><span data-stu-id="61d92-123">For example, you may need tooevaluate hello Azure-AsyncOperation header value for one operation, and hello Location header value for another operation.</span></span> 

<span data-ttu-id="61d92-124">Per recuperare valori di intestazione di hello come è possibile recuperare qualsiasi valore di intestazione per una richiesta.</span><span class="sxs-lookup"><span data-stu-id="61d92-124">You retrieve hello header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="61d92-125">Ad esempio, in c#, recuperare il valore di intestazione hello da un `HttpWebResponse` oggetto denominato `response` con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="61d92-125">For example, in C#, you retrieve hello header value from an `HttpWebResponse` object named `response` with hello following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="61d92-126">Richiesta e risposta di Azure AsyncOperation</span><span class="sxs-lookup"><span data-stu-id="61d92-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="61d92-127">stato hello tooget dell'operazione asincrona di hello, inviare un URL di toohello richiesta GET nel valore dell'intestazione AsyncOperation di Azure.</span><span class="sxs-lookup"><span data-stu-id="61d92-127">tooget hello status of hello asynchronous operation, send a GET request toohello URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="61d92-128">Hello corpo della risposta hello da questa operazione contiene informazioni sull'operazione hello.</span><span class="sxs-lookup"><span data-stu-id="61d92-128">hello body of hello response from this operation contains information about hello operation.</span></span> <span data-ttu-id="61d92-129">Hello seguente illustra i valori possibili hello restituiti dall'operazione hello:</span><span class="sxs-lookup"><span data-stu-id="61d92-129">hello following example shows hello possible values returned from hello operation:</span></span>

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

<span data-ttu-id="61d92-130">Solo `status` viene restituito per tutte le risposte.</span><span class="sxs-lookup"><span data-stu-id="61d92-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="61d92-131">oggetto error Hello viene restituito quando lo stato di hello è non riuscito o annullato.</span><span class="sxs-lookup"><span data-stu-id="61d92-131">hello error object is returned when hello status is Failed or Canceled.</span></span> <span data-ttu-id="61d92-132">Tutti gli altri valori sono facoltative. Pertanto, si riceve risposta di hello può avere un aspetto diverso esempio hello.</span><span class="sxs-lookup"><span data-stu-id="61d92-132">All other values are optional; therefore, hello response you receive may look different than hello example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="61d92-133">Valori provisioningState</span><span class="sxs-lookup"><span data-stu-id="61d92-133">provisioningState values</span></span>

<span data-ttu-id="61d92-134">Le operazioni di creazione, aggiornamento o eliminazione (INSERISCI, PATCH, ELIMINA) di una risorsa restituiscono in genere un valore `provisioningState`.</span><span class="sxs-lookup"><span data-stu-id="61d92-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="61d92-135">Quando un'operazione viene completata, viene restituito uno dei tre valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="61d92-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="61d92-136">Operazione riuscita</span><span class="sxs-lookup"><span data-stu-id="61d92-136">Succeeded</span></span>
* <span data-ttu-id="61d92-137">Operazione non riuscita</span><span class="sxs-lookup"><span data-stu-id="61d92-137">Failed</span></span>
* <span data-ttu-id="61d92-138">Canceled</span><span class="sxs-lookup"><span data-stu-id="61d92-138">Canceled</span></span>

<span data-ttu-id="61d92-139">Tutti gli altri valori indicano l'operazione di hello è ancora in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="61d92-139">All other values indicate hello operation is still running.</span></span> <span data-ttu-id="61d92-140">provider di risorse Hello può restituire un valore personalizzato che indica lo stato.</span><span class="sxs-lookup"><span data-stu-id="61d92-140">hello resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="61d92-141">Ad esempio, potrebbe essere visualizzato **accettato** quando richiesta hello viene ricevuto e in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="61d92-141">For example, you may receive **Accepted** when hello request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="61d92-142">Esempi di richieste e risposte</span><span class="sxs-lookup"><span data-stu-id="61d92-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="61d92-143">Avviare la macchina virtuale (202 con Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="61d92-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="61d92-144">Questo esempio viene illustrato come toodetermine hello stato **avviare** operazione per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="61d92-144">This example shows how toodetermine hello status of **start** operation for virtual machines.</span></span> <span data-ttu-id="61d92-145">richiesta iniziale Hello è nel seguente formato hello:</span><span class="sxs-lookup"><span data-stu-id="61d92-145">hello initial request is in hello following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="61d92-146">Restituisce il codice di stato 202.</span><span class="sxs-lookup"><span data-stu-id="61d92-146">It returns status code 202.</span></span> <span data-ttu-id="61d92-147">Tra i valori di intestazione hello, vedere:</span><span class="sxs-lookup"><span data-stu-id="61d92-147">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="61d92-148">stato di hello toocheck dell'operazione asincrona di hello, l'invio di un altro URL toothat della richiesta.</span><span class="sxs-lookup"><span data-stu-id="61d92-148">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="61d92-149">corpo della risposta Hello contiene lo stato di hello dell'operazione hello:</span><span class="sxs-lookup"><span data-stu-id="61d92-149">hello response body contains hello status of hello operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="61d92-150">Distribuzione delle risorse (201 con Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="61d92-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="61d92-151">Questo esempio viene illustrato come toodetermine hello stato **distribuzioni** operazione per la distribuzione di risorse tooAzure.</span><span class="sxs-lookup"><span data-stu-id="61d92-151">This example shows how toodetermine hello status of **deployments** operation for deploying resources tooAzure.</span></span> <span data-ttu-id="61d92-152">richiesta iniziale Hello è nel seguente formato hello:</span><span class="sxs-lookup"><span data-stu-id="61d92-152">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="61d92-153">Restituisce il codice di stato 201.</span><span class="sxs-lookup"><span data-stu-id="61d92-153">It returns status code 201.</span></span> <span data-ttu-id="61d92-154">Hello corpo della risposta hello include:</span><span class="sxs-lookup"><span data-stu-id="61d92-154">hello body of hello response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="61d92-155">Tra i valori di intestazione hello, vedere:</span><span class="sxs-lookup"><span data-stu-id="61d92-155">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="61d92-156">stato di hello toocheck dell'operazione asincrona di hello, l'invio di un altro URL toothat della richiesta.</span><span class="sxs-lookup"><span data-stu-id="61d92-156">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="61d92-157">corpo della risposta Hello contiene lo stato di hello dell'operazione hello:</span><span class="sxs-lookup"><span data-stu-id="61d92-157">hello response body contains hello status of hello operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="61d92-158">Al termine, la distribuzione di hello risposta hello contiene:</span><span class="sxs-lookup"><span data-stu-id="61d92-158">When hello deployment is finished, hello response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="61d92-159">Creazione di un account di archiviazione (202 con Location e Retry-After)</span><span class="sxs-lookup"><span data-stu-id="61d92-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="61d92-160">Questo esempio viene illustrato come toodetermine hello lo stato di hello **creare** operazione per gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="61d92-160">This example shows how toodetermine hello status of hello **create** operation for storage accounts.</span></span> <span data-ttu-id="61d92-161">richiesta iniziale Hello è nel seguente formato hello:</span><span class="sxs-lookup"><span data-stu-id="61d92-161">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="61d92-162">E il corpo della richiesta hello contiene le proprietà per l'account di archiviazione hello:</span><span class="sxs-lookup"><span data-stu-id="61d92-162">And hello request body contains properties for hello storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="61d92-163">Restituisce il codice di stato 202.</span><span class="sxs-lookup"><span data-stu-id="61d92-163">It returns status code 202.</span></span> <span data-ttu-id="61d92-164">Tra i valori di intestazione hello, vedrai hello due valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="61d92-164">Among hello header values, you see hello following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="61d92-165">Dopo aver atteso il numero di secondi specificato in Retry-After, controllare lo stato di hello dell'operazione asincrona di hello mediante l'invio di un altro URL toothat della richiesta.</span><span class="sxs-lookup"><span data-stu-id="61d92-165">After waiting for number of seconds specified in Retry-After, check hello status of hello asynchronous operation by sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="61d92-166">Se la richiesta hello è ancora in esecuzione, verrà visualizzato un codice di stato 202.</span><span class="sxs-lookup"><span data-stu-id="61d92-166">If hello request is still running, you receive a status code 202.</span></span> <span data-ttu-id="61d92-167">Se hello richiesta è stata completata, la ricezione di un codice di stato 200 e corpo hello della risposta hello contiene proprietà di hello hello dell'account di archiviazione che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="61d92-167">If hello request has completed, your receive a status code 200, and hello body of hello response contains hello properties of hello storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61d92-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="61d92-168">Next steps</span></span>

* <span data-ttu-id="61d92-169">Per la documentazione relativa a ogni operazione REST, consultare la [documentazione dell'API REST](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="61d92-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="61d92-170">Per informazioni sulla gestione delle risorse tramite hello REST API di gestione risorse, vedere [hello tramite REST API di gestione risorse](resource-manager-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="61d92-170">For information about managing resources through hello Resource Manager REST API, see [Using hello Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="61d92-171">Per informazioni sulla distribuzione di modelli tramite hello REST API di gestione risorse, vedere [distribuire le risorse con i modelli di gestione risorse e il REST API di gestione risorse](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="61d92-171">for information about deploying templates through hello Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>
