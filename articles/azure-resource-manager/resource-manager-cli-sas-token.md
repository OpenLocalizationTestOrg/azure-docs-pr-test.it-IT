---
title: modello di Azure con Azure CLI e il token SAS aaaDeploy | Documenti Microsoft
description: "Utilizzare Gestione risorse di Azure e Azure CLI tooAzure toodeploy risorse da un modello che è protetta con token di firma di accesso condiviso."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 59c64616d6e1f5e456d88a72854d0ed99e1bdc0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a>Distribuire un modello di Resource Manager privato con un token di firma di accesso condiviso e l'interfaccia della riga di comando di Azure

Quando il modello si trova in un account di archiviazione, è possibile limitare il modello di toohello access e fornire un token di firma di accesso condiviso durante la distribuzione. Questo argomento viene illustrato come toouse Azure PowerShell con Gestione risorse modelli tooprovide un token di firma di accesso condiviso durante la distribuzione. 

## <a name="add-private-template-toostorage-account"></a>Aggiungere modello privata toostorage account

È possibile aggiungere l'account di archiviazione di modelli tooa e collegarla toothem durante la distribuzione con un token di firma di accesso condiviso.

> [!IMPORTANT]
> Seguendo i passaggi di hello riportati di seguito, blob hello contenente il modello di hello è proprietario dell'account hello tooonly accessibile. Tuttavia, quando si crea un token di firma di accesso condiviso per il blob hello, blob hello è accessibile tooanyone con quell'URI. Se un altro utente intercetta hello URI, tale utente è il modello di hello in grado di tooaccess. Usando un token di firma di accesso condiviso è un buon metodo per limitare l'accesso tooyour modelli, ma non è necessario includere dati riservati, quali le password direttamente nel modello di hello.
> 
> 

Hello seguente esempio viene configurato un contenitore di account di archiviazione privato e carica un modello:
   
```azurecli
az group create --name "ManageGroup" --location "South Central US"
az storage account create \
    --resource-group ManageGroup \
    --location "South Central US" \
    --sku Standard_LRS \
    --kind Storage \
    --name {your-unique-name}
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
az storage container create \
    --name templates \
    --public-access Off \
    --connection-string $connection
az storage blob upload \
    --container-name templates \
    --file vmlinux.json \
    --name vmlinux.json \
    --connection-string $connection
```

### <a name="provide-sas-token-during-deployment"></a>Fornire il token SAS in fase di distribuzione
toodeploy un modello privato in un account di archiviazione, generare un token di firma di accesso condiviso e includerlo in hello URI per il modello di hello. Impostare tooallow ora di scadenza hello sufficiente distribuzione hello toocomplete.
   
```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
token=$(az storage blob generate-sas \
    --container-name templates \
    --name vmlinux.json \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name vmlinux.json \
    --output tsv \
    --connection-string $connection)
az group deployment create --resource-group ExampleGroup --template-uri $url?$token
```

Per un esempio sull'uso di un token di firma di accesso condiviso con modelli collegati, vedere [Uso di modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).

## <a name="next-steps"></a>Passaggi successivi
* Per i modelli di toodeploying un'introduzione, vedere [distribuire le risorse e modelli di gestione risorse di Azure PowerShell](resource-group-template-deploy-cli.md).
* Per uno script di esempio completo che consente di distribuire un modello, vedere lo [script di distribuzione di modelli di Resource Manager](resource-manager-samples-cli-deploy.md)
* toodefine i parametri di modello, vedere [creazione di modelli](resource-group-authoring-templates.md#parameters).
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).
