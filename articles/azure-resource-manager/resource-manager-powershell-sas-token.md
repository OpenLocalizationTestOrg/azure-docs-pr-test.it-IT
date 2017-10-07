---
title: modello di Azure con il token SAS e PowerShell aaaDeploy | Documenti Microsoft
description: "Utilizzare Gestione risorse di Azure e Azure PowerShell tooAzure toodeploy risorse da un modello che è protetta con token di firma di accesso condiviso."
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
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: b95e096591d6213f8ef79235c8cd85705c4b79ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a>Distribuire un modello di Resource Manager privato con un token di firma di accesso condiviso e Azure PowerShell

Quando il modello si trova in un account di archiviazione, è possibile limitare il modello di toohello access e fornire un token di firma di accesso condiviso durante la distribuzione. Questo argomento viene illustrato come toouse Azure PowerShell con Gestione risorse modelli tooprovide un token di firma di accesso condiviso durante la distribuzione. 

## <a name="add-private-template-toostorage-account"></a>Aggiungere modello privata toostorage account

È possibile aggiungere l'account di archiviazione di modelli tooa e collegarla toothem durante la distribuzione con un token di firma di accesso condiviso.

> [!IMPORTANT]
> Seguendo i passaggi di hello riportati di seguito, blob hello contenente il modello di hello è proprietario dell'account hello tooonly accessibile. Tuttavia, quando si crea un token di firma di accesso condiviso per il blob hello, blob hello è accessibile tooanyone con quell'URI. Se un altro utente intercetta hello URI, tale utente è il modello di hello in grado di tooaccess. Usando un token di firma di accesso condiviso è un buon metodo per limitare l'accesso tooyour modelli, ma non è necessario includere dati riservati, quali le password direttamente nel modello di hello.
> 
> 

Hello seguente esempio viene configurato un contenitore di account di archiviazione privato e carica un modello:
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a>Fornire il token SAS in fase di distribuzione
toodeploy un modello privato in un account di archiviazione, generare un token di firma di accesso condiviso e includerlo in hello URI per il modello di hello. Impostare tooallow ora di scadenza hello sufficiente distribuzione hello toocomplete.
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get hello URI with hello SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

Per un esempio sull'uso di un token di firma di accesso condiviso con modelli collegati, vedere [Uso di modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).


## <a name="next-steps"></a>Passaggi successivi
* Per i modelli di toodeploying un'introduzione, vedere [distribuire le risorse e modelli di gestione risorse di Azure PowerShell](resource-group-template-deploy.md).
* Per uno script di esempio completo che consente di distribuire un modello, vedere lo [script di distribuzione di modelli di Resource Manager](resource-manager-samples-powershell-deploy.md)
* toodefine i parametri di modello, vedere [creazione di modelli](resource-group-authoring-templates.md#parameters).
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).

