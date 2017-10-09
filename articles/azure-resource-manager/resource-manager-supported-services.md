---
title: aaaAzure i provider di risorse e i tipi di risorsa | Documenti Microsoft
description: Descrive i provider di risorse hello che supportano Gestione risorse, i relativi schemi e le versioni disponibili di API e le aree di hello in grado di ospitare le risorse di hello.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a>Provider e tipi di risorse

Durante la distribuzione di risorse, spesso necessario tooretrieve informazioni sui tipi e i provider di risorse hello. Questo articolo illustra come:

* Visualizzare tutti i provider di risorse in Azure
* Controllare lo stato di registrazione di un provider di risorse
* Registrare un provider di risorse
* Visualizzare i tipi di risorse per un provider di risorse
* Visualizzare le località valide per un tipo di risorsa
* Visualizzare le versioni API valide per un tipo di risorsa

È possibile eseguire questi passaggi tramite il portale di hello, PowerShell o CLI di Azure.

## <a name="powershell"></a>PowerShell

toosee tutti i provider di risorse in Azure e lo stato della registrazione hello per la sottoscrizione, utilizzano:

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

Che restituisce risultati simili a:

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

Registrazione di un provider di risorse Configura toowork l'abbonamento con provider di risorse hello. ambito Hello per la registrazione è sempre sottoscrizione hello. Per impostazione predefinita, molti provider di risorse vengono registrati automaticamente. Tuttavia, potrebbe essere necessario toomanually registrare alcuni provider di risorse. tooregister un provider di risorse, è necessario disporre di hello tooperform autorizzazione `/register/action` operazione hello provider di risorse. Questa operazione è incluso nei ruoli di proprietario e collaboratore hello.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

Che restituisce risultati simili a:

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

Non è possibile annullare la registrazione di un provider di risorse quando nella sottoscrizione sono ancora presenti tipi di risorsa di tale provider di risorse.

toosee informazioni per un provider di risorse specifico, utilizzare:

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

Che restituisce risultati simili a:

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

tipi di risorsa hello toosee per un provider di risorse, utilizzare:

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

Che restituisce:

```powershell
batchAccounts
operations
locations
locations/quotas
```

versione dell'API Hello corrisponde versione tooa di operazioni dell'API REST che vengono rilasciati dal provider di risorse hello. Un provider di risorse consente una nuova funzionalità, viene rilasciata una nuova versione di hello API REST. 

tooget hello API le versioni disponibili per un tipo di risorsa, utilizzare:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

Che restituisce:

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

Gestione risorse è supportata in tutte le aree, ma le risorse di hello che distribuire potrebbero non essere supportate in tutte le aree. Inoltre, potrebbe essere limitazioni per la sottoscrizione di impediscano l'utilizzo di alcune aree che supportano la risorsa hello. 

percorsi di tooget hello è supportato per un tipo di risorsa, utilizzare.

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

Che restituisce:

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure
toosee tutti i provider di risorse in Azure e lo stato della registrazione hello per la sottoscrizione, utilizzano:

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

Che restituisce risultati simili a:

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

Registrazione di un provider di risorse Configura toowork l'abbonamento con provider di risorse hello. ambito Hello per la registrazione è sempre sottoscrizione hello. Per impostazione predefinita, molti provider di risorse vengono registrati automaticamente. Tuttavia, potrebbe essere necessario toomanually registrare alcuni provider di risorse. tooregister un provider di risorse, è necessario disporre di hello tooperform autorizzazione `/register/action` operazione hello provider di risorse. Questa operazione è incluso nei ruoli di proprietario e collaboratore hello.

```azurecli
az provider register --namespace Microsoft.Batch
```

Che restituisce un messaggio di registrazione in corso.

Non è possibile annullare la registrazione di un provider di risorse quando nella sottoscrizione sono ancora presenti tipi di risorsa di tale provider di risorse.

toosee informazioni per un provider di risorse specifico, utilizzare:

```azurecli
az provider show --namespace Microsoft.Batch
```

Che restituisce risultati simili a:

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

tipi di risorsa hello toosee per un provider di risorse, utilizzare:

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

Che restituisce:

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

versione dell'API Hello corrisponde versione tooa di operazioni dell'API REST che vengono rilasciati dal provider di risorse hello. Un provider di risorse consente una nuova funzionalità, viene rilasciata una nuova versione di hello API REST. 

tooget hello API le versioni disponibili per un tipo di risorsa, utilizzare:

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

Che restituisce:

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

Gestione risorse è supportata in tutte le aree, ma le risorse di hello che distribuire potrebbero non essere supportate in tutte le aree. Inoltre, potrebbe essere limitazioni per la sottoscrizione di impediscano l'utilizzo di alcune aree che supportano la risorsa hello. 

percorsi di tooget hello è supportato per un tipo di risorsa, utilizzare.

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

Che restituisce:

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a>di Microsoft Azure

Selezionare tutti i provider di risorse in Azure e per la sottoscrizione, lo stato della registrazione hello toosee **sottoscrizioni**.

![selezionare sottoscrizioni](./media/resource-manager-supported-services/select-subscriptions.png)

Scegliere tooview sottoscrizione hello.

![specificare la sottoscrizione](./media/resource-manager-supported-services/subscription.png)

Selezionare **i provider di risorse** e visualizzare l'elenco hello dei provider di risorse disponibili.

![visualizzare i provider di risorse](./media/resource-manager-supported-services/show-resource-providers.png)

Registrazione di un provider di risorse Configura toowork l'abbonamento con provider di risorse hello. ambito Hello per la registrazione è sempre sottoscrizione hello. Per impostazione predefinita, molti provider di risorse vengono registrati automaticamente. Tuttavia, potrebbe essere necessario toomanually registrare alcuni provider di risorse. tooregister un provider di risorse, è necessario disporre di hello tooperform autorizzazione `/register/action` operazione hello provider di risorse. Questa operazione è incluso nei ruoli di proprietario e collaboratore hello. Selezionare un provider di risorse, tooregister **registrare**.

![registrare un provider di risorse](./media/resource-manager-supported-services/register-provider.png)

Non è possibile annullare la registrazione di un provider di risorse quando nella sottoscrizione sono ancora presenti tipi di risorsa di tale provider di risorse.

toosee informazioni per un provider di risorse specifico, selezionare **più servizi**.

![selezionare altri servizi](./media/resource-manager-supported-services/more-services.png)

Cercare **Esplora inventario risorse** e selezionare le opzioni disponibili hello.

![selezionare resource explorer](./media/resource-manager-supported-services/select-resource-explorer.png)

Selezionare **Provider**.

![Selezionare i provider](./media/resource-manager-supported-services/select-providers.png)

Tipo di risorsa e il provider di risorse hello selezionare da tooview.

![Selezionare il tipo di risorsa](./media/resource-manager-supported-services/select-resource-type.png)

Gestione risorse è supportata in tutte le aree, ma le risorse di hello che distribuire potrebbero non essere supportate in tutte le aree. Inoltre, potrebbe essere limitazioni per la sottoscrizione di impediscano l'utilizzo di alcune aree che supportano la risorsa hello. Esplora inventario risorse Hello consente di visualizzare le posizioni valide per il tipo di risorsa hello.

![Visualizzare le località](./media/resource-manager-supported-services/show-locations.png)

versione dell'API Hello corrisponde versione tooa di operazioni dell'API REST che vengono rilasciati dal provider di risorse hello. Un provider di risorse consente una nuova funzionalità, viene rilasciata una nuova versione di hello API REST. Esplora inventario risorse Hello Visualizza versioni API valide per il tipo di risorsa hello.

![Visualizzare le versioni API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a>Passaggi successivi
* toolearn sulla creazione di modelli di gestione delle risorse, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* toolearn sulla distribuzione di risorse, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).
* operazioni di hello tooview per un provider di risorse, vedere [API REST di Azure](/rest/api/).

