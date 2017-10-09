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
# <a name="track-asynchronous-azure-operations"></a>Tenere traccia delle operazioni asincrone
Alcune operazioni REST di Azure eseguiti in modo asincrono perché non è possibile completare l'operazione di hello rapidamente. In questo argomento viene descritto come stato di hello tootrack delle operazioni asincrone tramite i valori restituiti nella risposta hello.  

## <a name="status-codes-for-asynchronous-operations"></a>Codici di stato per le operazioni asincrone
Inizialmente, un'operazione asincrona restituisce un codice di stato HTTP del tipo:

* 201 (Creato) oppure
* 202 (Accettato) 

Quando l'operazione hello è stata completata correttamente, viene restituito uno:

* 200 (OK)
* 204 (No Content (Nessun contenuto)) 

Fare riferimento toohello [documentazione dell'API REST](/rest/api/) risposte hello toosee per l'operazione di hello in caso di esecuzione. 

## <a name="monitor-status-of-operation"></a>Monitorare lo stato dell'operazione
Hello asincrona REST operazioni restituiti valori di intestazione, cui è stato hello toodetermine di hello operazione. Esistono potenzialmente tooexamine di intestazione tre valori:

* `Azure-AsyncOperation`-URL per controllare lo stato in corso di hello dell'operazione di hello. Se l'operazione restituisce questo valore, utilizzare sempre lo stato di hello tootrack it (anziché percorso) dell'operazione di hello.
* `Location` -URL per determinare quando un'operazione è stata completata. Usare questo valore solo quando non viene restituito Azure-AsyncOperation.
* `Retry-After`-hello numero di secondi toowait prima di archiviare lo stato di hello dell'operazione asincrona di hello.

Tuttavia, non tutte le operazioni asincrone restituiscono tutti questi valori. Ad esempio, potrebbe essere il valore dell'intestazione tooevaluate hello Azure AsyncOperation per un'operazione e valore dell'intestazione Location hello per un'altra operazione. 

Per recuperare valori di intestazione di hello come è possibile recuperare qualsiasi valore di intestazione per una richiesta. Ad esempio, in c#, recuperare il valore di intestazione hello da un `HttpWebResponse` oggetto denominato `response` con hello seguente codice:

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a>Richiesta e risposta di Azure AsyncOperation

stato hello tooget dell'operazione asincrona di hello, inviare un URL di toohello richiesta GET nel valore dell'intestazione AsyncOperation di Azure.

Hello corpo della risposta hello da questa operazione contiene informazioni sull'operazione hello. Hello seguente illustra i valori possibili hello restituiti dall'operazione hello:

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

Solo `status` viene restituito per tutte le risposte. oggetto error Hello viene restituito quando lo stato di hello è non riuscito o annullato. Tutti gli altri valori sono facoltative. Pertanto, si riceve risposta di hello può avere un aspetto diverso esempio hello.

## <a name="provisioningstate-values"></a>Valori provisioningState

Le operazioni di creazione, aggiornamento o eliminazione (INSERISCI, PATCH, ELIMINA) di una risorsa restituiscono in genere un valore `provisioningState`. Quando un'operazione viene completata, viene restituito uno dei tre valori seguenti: 

* Operazione riuscita
* Operazione non riuscita
* Canceled

Tutti gli altri valori indicano l'operazione di hello è ancora in esecuzione. provider di risorse Hello può restituire un valore personalizzato che indica lo stato. Ad esempio, potrebbe essere visualizzato **accettato** quando richiesta hello viene ricevuto e in esecuzione.

## <a name="example-requests-and-responses"></a>Esempi di richieste e risposte

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a>Avviare la macchina virtuale (202 con Azure-AsyncOperation)
Questo esempio viene illustrato come toodetermine hello stato **avviare** operazione per le macchine virtuali. richiesta iniziale Hello è nel seguente formato hello:

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

Restituisce il codice di stato 202. Tra i valori di intestazione hello, vedere:

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

stato di hello toocheck dell'operazione asincrona di hello, l'invio di un altro URL toothat della richiesta.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

corpo della risposta Hello contiene lo stato di hello dell'operazione hello:

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a>Distribuzione delle risorse (201 con Azure-AsyncOperation)

Questo esempio viene illustrato come toodetermine hello stato **distribuzioni** operazione per la distribuzione di risorse tooAzure. richiesta iniziale Hello è nel seguente formato hello:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

Restituisce il codice di stato 201. Hello corpo della risposta hello include:

```json
"provisioningState":"Accepted",
```

Tra i valori di intestazione hello, vedere:

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

stato di hello toocheck dell'operazione asincrona di hello, l'invio di un altro URL toothat della richiesta.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

corpo della risposta Hello contiene lo stato di hello dell'operazione hello:

```json
{"status":"Running"}
```

Al termine, la distribuzione di hello risposta hello contiene:

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a>Creazione di un account di archiviazione (202 con Location e Retry-After)

Questo esempio viene illustrato come toodetermine hello lo stato di hello **creare** operazione per gli account di archiviazione. richiesta iniziale Hello è nel seguente formato hello:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

E il corpo della richiesta hello contiene le proprietà per l'account di archiviazione hello:

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

Restituisce il codice di stato 202. Tra i valori di intestazione hello, vedrai hello due valori seguenti:

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

Dopo aver atteso il numero di secondi specificato in Retry-After, controllare lo stato di hello dell'operazione asincrona di hello mediante l'invio di un altro URL toothat della richiesta.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

Se la richiesta hello è ancora in esecuzione, verrà visualizzato un codice di stato 202. Se hello richiesta è stata completata, la ricezione di un codice di stato 200 e corpo hello della risposta hello contiene proprietà di hello hello dell'account di archiviazione che è stato creato.

## <a name="next-steps"></a>Passaggi successivi

* Per la documentazione relativa a ogni operazione REST, consultare la [documentazione dell'API REST](/rest/api/).
* Per informazioni sulla gestione delle risorse tramite hello REST API di gestione risorse, vedere [hello tramite REST API di gestione risorse](resource-manager-rest-api.md).
* Per informazioni sulla distribuzione di modelli tramite hello REST API di gestione risorse, vedere [distribuire le risorse con i modelli di gestione risorse e il REST API di gestione risorse](resource-group-template-deploy-rest.md).
