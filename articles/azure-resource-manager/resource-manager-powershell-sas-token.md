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
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a><span data-ttu-id="dd6c4-103">Distribuire un modello di Resource Manager privato con un token di firma di accesso condiviso e Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd6c4-103">Deploy private Resource Manager template with SAS token and Azure PowerShell</span></span>

<span data-ttu-id="dd6c4-104">Quando il modello si trova in un account di archiviazione, è possibile limitare il modello di toohello access e fornire un token di firma di accesso condiviso durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="dd6c4-104">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="dd6c4-105">Questo argomento viene illustrato come toouse Azure PowerShell con Gestione risorse modelli tooprovide un token di firma di accesso condiviso durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="dd6c4-105">This topic explains how toouse Azure PowerShell with Resource Manager templates tooprovide a SAS token during deployment.</span></span> 

## <a name="add-private-template-toostorage-account"></a><span data-ttu-id="dd6c4-106">Aggiungere modello privata toostorage account</span><span class="sxs-lookup"><span data-stu-id="dd6c4-106">Add private template toostorage account</span></span>

<span data-ttu-id="dd6c4-107">È possibile aggiungere l'account di archiviazione di modelli tooa e collegarla toothem durante la distribuzione con un token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="dd6c4-107">You can add your templates tooa storage account and link toothem during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd6c4-108">Seguendo i passaggi di hello riportati di seguito, blob hello contenente il modello di hello è proprietario dell'account hello tooonly accessibile.</span><span class="sxs-lookup"><span data-stu-id="dd6c4-108">By following hello steps below, hello blob containing hello template is accessible tooonly hello account owner.</span></span> <span data-ttu-id="dd6c4-109">Tuttavia, quando si crea un token di firma di accesso condiviso per il blob hello, blob hello è accessibile tooanyone con quell'URI.</span><span class="sxs-lookup"><span data-stu-id="dd6c4-109">However, when you create a SAS token for hello blob, hello blob is accessible tooanyone with that URI.</span></span> <span data-ttu-id="dd6c4-110">Se un altro utente intercetta hello URI, tale utente è il modello di hello in grado di tooaccess.</span><span class="sxs-lookup"><span data-stu-id="dd6c4-110">If another user intercepts hello URI, that user is able tooaccess hello template.</span></span> <span data-ttu-id="dd6c4-111">Usando un token di firma di accesso condiviso è un buon metodo per limitare l'accesso tooyour modelli, ma non è necessario includere dati riservati, quali le password direttamente nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="dd6c4-111">Using a SAS token is a good way of limiting access tooyour templates, but you should not include sensitive data like passwords directly in hello template.</span></span>
> 
> 

<span data-ttu-id="dd6c4-112">Hello seguente esempio viene configurato un contenitore di account di archiviazione privato e carica un modello:</span><span class="sxs-lookup"><span data-stu-id="dd6c4-112">hello following example sets up a private storage account container and uploads a template:</span></span>
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="dd6c4-113">Fornire il token SAS in fase di distribuzione</span><span class="sxs-lookup"><span data-stu-id="dd6c4-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="dd6c4-114">toodeploy un modello privato in un account di archiviazione, generare un token di firma di accesso condiviso e includerlo in hello URI per il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="dd6c4-114">toodeploy a private template in a storage account, generate a SAS token and include it in hello URI for hello template.</span></span> <span data-ttu-id="dd6c4-115">Impostare tooallow ora di scadenza hello sufficiente distribuzione hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="dd6c4-115">Set hello expiry time tooallow enough time toocomplete hello deployment.</span></span>
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get hello URI with hello SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

<span data-ttu-id="dd6c4-116">Per un esempio sull'uso di un token di firma di accesso condiviso con modelli collegati, vedere [Uso di modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="dd6c4-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="dd6c4-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dd6c4-117">Next steps</span></span>
* <span data-ttu-id="dd6c4-118">Per i modelli di toodeploying un'introduzione, vedere [distribuire le risorse e modelli di gestione risorse di Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="dd6c4-118">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="dd6c4-119">Per uno script di esempio completo che consente di distribuire un modello, vedere lo [script di distribuzione di modelli di Resource Manager](resource-manager-samples-powershell-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="dd6c4-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md)</span></span>
* <span data-ttu-id="dd6c4-120">toodefine i parametri di modello, vedere [creazione di modelli](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="dd6c4-120">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="dd6c4-121">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="dd6c4-121">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

