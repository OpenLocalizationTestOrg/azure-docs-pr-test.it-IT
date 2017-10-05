---
title: Distribuire un modello di Azure con un token di firma di accesso condiviso e l'interfaccia della riga di comando di Azure | Microsoft Docs
description: Usare Azure Resource Manager e l'interfaccia della riga di comando di Azure per distribuire risorse in Azure da un modello protetto con un token di firma di accesso condiviso.
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
ms.openlocfilehash: 22387aadd8f53a65efb76a29a9403c46a2c25954
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a><span data-ttu-id="bf5f9-103">Distribuire un modello di Resource Manager privato con un token di firma di accesso condiviso e l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="bf5f9-103">Deploy private Resource Manager template with SAS token and Azure CLI</span></span>

<span data-ttu-id="bf5f9-104">Quando il modello si trova in un account di archiviazione, è possibile limitare l'accesso al modello e fornire un token di firma di accesso condiviso in fase di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="bf5f9-104">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="bf5f9-105">Questo articolo illustra come usare Azure PowerShell con modelli di Resource Manager per fornire un token di firma di accesso condiviso durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="bf5f9-105">This topic explains how to use Azure PowerShell with Resource Manager templates to provide a SAS token during deployment.</span></span> 

## <a name="add-private-template-to-storage-account"></a><span data-ttu-id="bf5f9-106">Aggiungere un modello privato all'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="bf5f9-106">Add private template to storage account</span></span>

<span data-ttu-id="bf5f9-107">È possibile aggiungere i modelli a un account di archiviazione e collegarli durante la distribuzione con un token SAS.</span><span class="sxs-lookup"><span data-stu-id="bf5f9-107">You can add your templates to a storage account and link to them during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf5f9-108">Attenendosi alla seguente procedura, il BLOB contenente il modello sarà accessibile solo da parte del proprietario dell'account.</span><span class="sxs-lookup"><span data-stu-id="bf5f9-108">By following the steps below, the blob containing the template is accessible to only the account owner.</span></span> <span data-ttu-id="bf5f9-109">Tuttavia, quando si crea un token di firma di accesso condiviso per il BLOB, quest'ultimo sarà accessibile a tutti gli utenti con quell'URI.</span><span class="sxs-lookup"><span data-stu-id="bf5f9-109">However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI.</span></span> <span data-ttu-id="bf5f9-110">Se l'URI viene intercettato da un altro utente, quest'ultimo sarà in grado di accedere al modello.</span><span class="sxs-lookup"><span data-stu-id="bf5f9-110">If another user intercepts the URI, that user is able to access the template.</span></span> <span data-ttu-id="bf5f9-111">Utilizzare un token di firma di accesso condiviso è un buon metodo per limitare l'accesso ai modelli, ma è necessario non includere direttamente nel modello dati sensibili come le password.</span><span class="sxs-lookup"><span data-stu-id="bf5f9-111">Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.</span></span>
> 
> 

<span data-ttu-id="bf5f9-112">L'esempio seguente configura un contenitore dell'account di archiviazione privato e carica un modello:</span><span class="sxs-lookup"><span data-stu-id="bf5f9-112">The following example sets up a private storage account container and uploads a template:</span></span>
   
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

### <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="bf5f9-113">Fornire il token SAS in fase di distribuzione</span><span class="sxs-lookup"><span data-stu-id="bf5f9-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="bf5f9-114">Per distribuire un modello privato in un account di archiviazione, generare un token di firma di accesso condiviso e includerlo nell'URI del modello.</span><span class="sxs-lookup"><span data-stu-id="bf5f9-114">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span></span> <span data-ttu-id="bf5f9-115">Impostare l'ora di scadenza in modo da garantire un tempo sufficiente per completare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="bf5f9-115">Set the expiry time to allow enough time to complete the deployment.</span></span>
   
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

<span data-ttu-id="bf5f9-116">Per un esempio sull'uso di un token di firma di accesso condiviso con modelli collegati, vedere [Uso di modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="bf5f9-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf5f9-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bf5f9-117">Next steps</span></span>
* <span data-ttu-id="bf5f9-118">Per un'introduzione alla distribuzione dei modelli, vedere [Distribuire le risorse con i modelli di Resource Manager e Azure PowerShell](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bf5f9-118">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="bf5f9-119">Per uno script di esempio completo che consente di distribuire un modello, vedere lo [script di distribuzione di modelli di Resource Manager](resource-manager-samples-cli-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="bf5f9-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-cli-deploy.md)</span></span>
* <span data-ttu-id="bf5f9-120">Per definire i parametri nel modello, vedere [Creazione di modelli](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="bf5f9-120">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="bf5f9-121">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="bf5f9-121">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
