---
title: Applicare tag alle risorse Azure per l'organizzazione logica | Documentazione Microsoft
description: Mostra come applicare i tag per organizzare le risorse Azure per la fatturazione e la gestione.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tomfitz
ms.openlocfilehash: 4f52c30614ad39da8a34ff6ecfb707b75400517f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-tags-to-organize-your-azure-resources"></a><span data-ttu-id="25ce8-103">Usare tag per organizzare le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="25ce8-103">Use tags to organize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="25ce8-104">È possibile applicare tag solo alle risorse che supportano le operazioni di Gestione Risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="25ce8-104">You can apply tags only to resources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="25ce8-105">Se è stata creata una macchina virtuale, una rete virtuale o un account di archiviazione tramite il modello di distribuzione classica, ad esempio tramite il portale di Azure classico, non è possibile applicare un tag a tale risorsa.</span><span class="sxs-lookup"><span data-stu-id="25ce8-105">If you created a virtual machine, virtual network, or storage account through the classic deployment model (such as through the Azure classic portal), you cannot apply a tag to that resource.</span></span> <span data-ttu-id="25ce8-106">Per supportare l'assegnazione di tag, distribuire nuovamente tali risorse tramite Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="25ce8-106">To support tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="25ce8-107">Tutte le altre risorse supportano l'assegnazione di tag.</span><span class="sxs-lookup"><span data-stu-id="25ce8-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="25ce8-108">Criteri per la coerenza dei tag</span><span class="sxs-lookup"><span data-stu-id="25ce8-108">Policies for tag consistency</span></span>

<span data-ttu-id="25ce8-109">È possibile usare i criteri delle risorse per creare regole standard per l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="25ce8-109">You can use resource policies to create standard rules for your organization.</span></span> <span data-ttu-id="25ce8-110">È possibile creare criteri che garantiscono che le risorse vengano contrassegnate con i valori appropriati.</span><span class="sxs-lookup"><span data-stu-id="25ce8-110">You can create policies that ensure resources are tagged with the appropriate values.</span></span> <span data-ttu-id="25ce8-111">Per altre informazioni, vedere [Applicare criteri delle risorse per i tag](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="25ce8-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="25ce8-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="25ce8-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="25ce8-113">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="25ce8-113">Azure CLI</span></span>

<span data-ttu-id="25ce8-114">Per visualizzare i tag esistenti per un *gruppo di risorse*, usare:</span><span class="sxs-lookup"><span data-stu-id="25ce8-114">To see the existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="25ce8-115">Lo script restituisce il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="25ce8-115">That script returns the following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="25ce8-116">Per visualizzare i tag esistenti per una *risorsa con un ID risorsa specificato*, usare:</span><span class="sxs-lookup"><span data-stu-id="25ce8-116">To see the existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="25ce8-117">In alternativa, per visualizzare i tag esistenti per una *risorsa con un nome, un tipo e un gruppo di risorse specificati*, usare:</span><span class="sxs-lookup"><span data-stu-id="25ce8-117">Or, to see the existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="25ce8-118">Per ottenere i gruppi di risorse con un tag specifico, usare `az group list`:</span><span class="sxs-lookup"><span data-stu-id="25ce8-118">To get resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="25ce8-119">Per ottenere tutte le risorse che hanno un tag e un valore specifici, usare `az resource list`:</span><span class="sxs-lookup"><span data-stu-id="25ce8-119">To get all the resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="25ce8-120">Ogni volta che si applicano tag a una risorsa o a un gruppo di risorse, si sovrascrivono i tag esistenti in tale risorsa o gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="25ce8-120">Every time you apply tags to a resource or a resource group, you overwrite the existing tags on that resource or resource group.</span></span> <span data-ttu-id="25ce8-121">È quindi necessario usare un approccio diverso se nella risorsa o nel gruppo di risorse esistono tag.</span><span class="sxs-lookup"><span data-stu-id="25ce8-121">Therefore, you must use a different approach based on whether the resource or resource group has existing tags.</span></span> 

<span data-ttu-id="25ce8-122">Per aggiungere tag a un *gruppo di risorse senza tag esistenti*, usare:</span><span class="sxs-lookup"><span data-stu-id="25ce8-122">To add tags to a *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="25ce8-123">Per aggiungere tag a una *risorsa senza tag esistenti*, usare:</span><span class="sxs-lookup"><span data-stu-id="25ce8-123">To add tags to a *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="25ce8-124">Per aggiungere tag a una risorsa che dispone già di tag, recuperare i tag esistenti, riformattare il valore e riapplicare i tag nuovi e già esistenti:</span><span class="sxs-lookup"><span data-stu-id="25ce8-124">To add tags to a resource that already has tags, retrieve the existing tags, reformat that value, and reapply the existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="25ce8-125">Per applicare tutti i tag da un gruppo di risorse alle risorse *senza mantenere i tag esistenti nelle risorse*, usare lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="25ce8-125">To apply all tags from a resource group to its resources, and *not retain existing tags on the resources*, use the following script:</span></span>

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    az resource tag --tags $t --id $resid
  done 
done
```

<span data-ttu-id="25ce8-126">Per applicare tutti i tag da un gruppo di risorse alle risorse e *mantenere i tag esistenti nelle risorse*, usare lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="25ce8-126">To apply all tags from a resource group to its resources, and *retain existing tags on resources*, use the following script:</span></span>

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    jsonrtag=$(az resource show --id $resid --query tags)
    rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
    az resource tag --tags $t$rt --id $resid
  done 
done
```


## <a name="templates"></a><span data-ttu-id="25ce8-127">Modelli</span><span class="sxs-lookup"><span data-stu-id="25ce8-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="25ce8-128">di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="25ce8-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="25ce8-129">API REST</span><span class="sxs-lookup"><span data-stu-id="25ce8-129">REST API</span></span>
<span data-ttu-id="25ce8-130">Sia il portale di Azure che PowerShell usano l' [API REST di Gestione Risorse](https://docs.microsoft.com/rest/api/resources/) dietro le quinte.</span><span class="sxs-lookup"><span data-stu-id="25ce8-130">The Azure portal and PowerShell both use the [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind the scenes.</span></span> <span data-ttu-id="25ce8-131">Se è necessario integrare l'assegnazione di tag in un altro ambiente, è possibile ottenere i tag tramite un'operazione **GET** sull'ID di risorsa e aggiornare il set di tag tramite una chiamata **PATCH**.</span><span class="sxs-lookup"><span data-stu-id="25ce8-131">If you need to integrate tagging into another environment, you can get tags by using **GET** on the resource ID and update the set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="25ce8-132">Tag e fatturazione</span><span class="sxs-lookup"><span data-stu-id="25ce8-132">Tags and billing</span></span>
<span data-ttu-id="25ce8-133">È possibile usare i tag per raggruppare i dati di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="25ce8-133">You can use tags to group your billing data.</span></span> <span data-ttu-id="25ce8-134">Ad esempio, se si eseguono più macchine virtuali per organizzazioni diverse, usare i tag per raggruppare l'utilizzo in base al centro di costo.</span><span class="sxs-lookup"><span data-stu-id="25ce8-134">For example, if you are running multiple VMs for different organizations, use the tags to group usage by cost center.</span></span> <span data-ttu-id="25ce8-135">È anche possibile usare i tag per classificare i costi in base all'ambiente di runtime; ad esempio, l'uso di fatturazione per le macchine virtuali in esecuzione nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="25ce8-135">You can also use tags to categorize costs by runtime environment, such as the billing usage for VMs running in the production environment.</span></span>


<span data-ttu-id="25ce8-136">Le informazioni sui tag possono essere recuperate tramite l' [API di utilizzo della risorsa di Azure e della Rate Card](../billing/billing-usage-rate-card-overview.md) o il file di utilizzo con valori delimitati da virgole (CSV).</span><span class="sxs-lookup"><span data-stu-id="25ce8-136">You can retrieve information about tags through the [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or the usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="25ce8-137">Il file di utilizzo può essere scaricato dal [portale dell'account di Azure](https://account.windowsazure.com/) o dal [portale EA](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="25ce8-137">You download the usage file from the [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="25ce8-138">Per altre informazioni sull'accesso a livello di codice alle informazioni sulla fatturazione, vedere [Ottenere informazioni dettagliate sul consumo delle risorse di Microsoft Azure](../billing/billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="25ce8-138">For more information about programmatic access to billing information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="25ce8-139">Per le operazioni API REST, vedere [Riferimento API REST alla fatturazione di Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span><span class="sxs-lookup"><span data-stu-id="25ce8-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="25ce8-140">Quando si scarica il CSV di utilizzo per i servizi che supportano i tag di fatturazione, i tag vengono visualizzati nella colonna **Tag** .</span><span class="sxs-lookup"><span data-stu-id="25ce8-140">When you download the usage CSV for services that support tags with billing, the tags appear in the **Tags** column.</span></span> <span data-ttu-id="25ce8-141">Per altre informazioni, vedere [Comprendere la fattura per Microsoft Azure](../billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="25ce8-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![Vedere i tag della fatturazione](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="25ce8-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25ce8-143">Next steps</span></span>
* <span data-ttu-id="25ce8-144">È possibile applicare restrizioni e convenzioni all'interno della sottoscrizione tramite criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="25ce8-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="25ce8-145">Un criterio che è stato definito potrebbe richiedere che per tutte le risorse sia impostato un determinato tag.</span><span class="sxs-lookup"><span data-stu-id="25ce8-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="25ce8-146">Per altre informazioni, vedere [Cenni preliminari sui criteri delle risorse](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="25ce8-146">For more information, see [Use policies to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="25ce8-147">Per un'introduzione all'uso di Azure PowerShell durante la distribuzione delle risorse, vedere [Uso di Azure PowerShell con Gestione risorse di Azure](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="25ce8-147">For an introduction to using Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="25ce8-148">Per un'introduzione all'uso dell'interfaccia della riga di comando di Azure durante la distribuzione delle risorse, vedere [Uso dell'interfaccia della riga di comando di Azure per Mac, Linux e Windows con Gestione risorse di Azure](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="25ce8-148">For an introduction to using the Azure CLI when you're deploying resources, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="25ce8-149">Per un'introduzione all'uso del portale, vedere [Uso del portale di Azure per gestire le risorse di Azure](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="25ce8-149">For an introduction to using the portal, see [Using the Azure portal to manage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="25ce8-150">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="25ce8-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

