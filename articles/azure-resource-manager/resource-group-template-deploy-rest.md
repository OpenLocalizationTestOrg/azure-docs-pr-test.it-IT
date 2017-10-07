---
title: risorse aaaDeploy con API REST e modello | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure e il REST API di gestione risorse toodeploy un tooAzure di risorse. risorse di Hello vengono definite in un modello di gestione risorse.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a>Distribuire le risorse con i modelli e l'API REST di Resource Manager
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Interfaccia della riga di comando di Azure](resource-group-template-deploy-cli.md)
> * [Portale](resource-group-template-deploy-portal.md)
> * [API REST](resource-group-template-deploy-rest.md)
> 
> 

Questo articolo spiega come toouse hello REST API di gestione risorse con Gestione risorse modelli toodeploy tooAzure le risorse.  

> [!TIP]
> Per informazioni su come eseguire il debug di un errore durante la distribuzione, vedere:
> 
> * [Per visualizzare le operazioni di distribuzione](resource-manager-deployment-operations.md) toolearn sul recupero di informazioni che consentono di risolvere l'errore
> * [Risolvere gli errori comuni durante la distribuzione di risorse tooAzure con Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn come tooresolve comuni errori di distribuzione
> 
> 

Il modello può essere un file locale oppure un file esterno disponibile tramite un URI. Quando il modello si trova in un account di archiviazione, è possibile limitare il modello di toohello access e fornire un token di firma di accesso condiviso durante la distribuzione.

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a>Distribuire con hello API REST
1. Impostare [parametri e intestazioni comuni](https://docs.microsoft.com/rest/api/index), tra cui i token di autenticazione.
2. Se non è già disponibile un gruppo di risorse, crearne uno. Specificare l'ID sottoscrizione, nome hello del nuovo gruppo di risorse hello e il percorso che è necessario per la soluzione. Per ulteriori informazioni, vedere [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate) (Creare un gruppo di risorse).
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. Convalidare la distribuzione prima dell'esecuzione eseguendo hello [convalidare una distribuzione modello](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operazione. Durante il test di distribuzione di hello, specificare i parametri, esattamente come quando si esegue la distribuzione di hello (illustrata nel passaggio successivo hello).
4. Creare una distribuzione. Specificare l'ID sottoscrizione, il nome di hello hello del gruppo di risorse, nome hello della distribuzione di hello e un modello di tooyour di collegamento. Per informazioni sul file di modello hello, vedere [file parametro](#parameter-file). Per ulteriori informazioni sulle API REST di hello toocreate un gruppo di risorse, vedere [creare una distribuzione modello](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate). Hello preavviso **modalità** è troppo**incrementale**. impostare una distribuzione completa, toorun **modalità** troppo**completa**. Prestare attenzione quando si utilizza modalità di completamento hello come è possibile eliminare inavvertitamente le risorse che non sono presenti nel modello.
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      Se si desidera toolog del contenuto della risposta, il contenuto della richiesta o entrambi, includere **debugSetting** nella richiesta di hello.
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      È possibile impostare il toouse di account di archiviazione un token di firma di accesso condiviso. Per altre informazioni, vedere [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature) (Delega dell'accesso con una firma di accesso condiviso).
5. Ottenere lo stato di hello di distribuzione del modello hello. Per altre informazioni, vedere [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) (Ottenere informazioni sulla distribuzione di un modello).
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a>File di parametri

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a>Passaggi successivi
* toolearn sulla gestione di operazioni asincrone di REST, vedere [tenere traccia delle operazioni asincrone di Azure](resource-manager-async-operations.md).
* Per un esempio di distribuzione delle risorse tramite una libreria client .NET di hello, vedere [distribuire le risorse con le librerie .NET e un modello](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* toodefine i parametri di modello, vedere [creazione di modelli](resource-group-authoring-templates.md#parameters).
* Per istruzioni sulla distribuzione negli ambienti toodifferent soluzione, vedere [gli ambienti di sviluppo e test in Microsoft Azure](solution-dev-test-environments.md).
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).

