---
title: aaaTag Azure le risorse per l'organizzazione logica | Documenti Microsoft
description: Viene illustrato come tooapply tag tooorganize Azure risorse per la fatturazione e la gestione.
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
ms.openlocfilehash: e07470463d160f8cefe5c80bc91e66a96af6ca45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-tags-tooorganize-your-azure-resources"></a><span data-ttu-id="059db-103">Utilizzare tag tooorganize le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="059db-103">Use tags tooorganize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="059db-104">È possibile applicare tooresources solo tag che supportano le operazioni di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="059db-104">You can apply tags only tooresources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="059db-105">Se è stato creato una macchina virtuale, una rete virtuale o un account di archiviazione tramite il modello di distribuzione classica hello (ad esempio mediante hello portale di Azure classico), è possibile applicare una risorsa toothat tag.</span><span class="sxs-lookup"><span data-stu-id="059db-105">If you created a virtual machine, virtual network, or storage account through hello classic deployment model (such as through hello Azure classic portal), you cannot apply a tag toothat resource.</span></span> <span data-ttu-id="059db-106">assegnazione di tag, toosupport ridistribuire tali risorse tramite Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="059db-106">toosupport tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="059db-107">Tutte le altre risorse supportano l'assegnazione di tag.</span><span class="sxs-lookup"><span data-stu-id="059db-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="059db-108">Criteri per la coerenza dei tag</span><span class="sxs-lookup"><span data-stu-id="059db-108">Policies for tag consistency</span></span>

<span data-ttu-id="059db-109">È possibile utilizzare regole standard toocreate dei criteri di risorse dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="059db-109">You can use resource policies toocreate standard rules for your organization.</span></span> <span data-ttu-id="059db-110">È possibile creare criteri che garantiscono le risorse sono contrassegnate con i valori appropriati di hello.</span><span class="sxs-lookup"><span data-stu-id="059db-110">You can create policies that ensure resources are tagged with hello appropriate values.</span></span> <span data-ttu-id="059db-111">Per altre informazioni, vedere [Applicare criteri delle risorse per i tag](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="059db-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="059db-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="059db-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="059db-113">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="059db-113">Azure CLI</span></span>

<span data-ttu-id="059db-114">toosee hello tag esistenti per un *gruppo di risorse*, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="059db-114">toosee hello existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="059db-115">Lo script restituisce hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="059db-115">That script returns hello following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="059db-116">toosee hello tag esistenti per un *risorsa con un ID di risorsa specificato*, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="059db-116">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="059db-117">In alternativa, toosee hello tag esistenti per un *risorse che dispone di un gruppo di nome e tipo di risorsa specificato*, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="059db-117">Or, toosee hello existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="059db-118">gruppi di risorse tooget che dispongono di un tag specifico, utilizzare `az group list`:</span><span class="sxs-lookup"><span data-stu-id="059db-118">tooget resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="059db-119">utilizzare tutte le risorse di hello con un tag specifico e un valore, tooget `az resource list`:</span><span class="sxs-lookup"><span data-stu-id="059db-119">tooget all hello resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="059db-120">Ogni volta che si applica tag tooa risorsa o un gruppo di risorse, sovrascrivere i tag esistenti hello su tale risorsa o un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="059db-120">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="059db-121">Pertanto, è necessario utilizzare un approccio diverso in base a se hello risorsa o il gruppo dispone di tag esistenti.</span><span class="sxs-lookup"><span data-stu-id="059db-121">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="059db-122">tooadd tag tooa *gruppo di risorse senza i tag esistenti*, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="059db-122">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="059db-123">tooadd tag tooa *risorsa senza i tag esistenti*, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="059db-123">tooadd tags tooa *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="059db-124">tooadd tag tooa risorse che dispone già di tag, recuperare i tag esistenti hello, tale valore consente di riformattare e riapplicare tag nuove ed esistenti di hello:</span><span class="sxs-lookup"><span data-stu-id="059db-124">tooadd tags tooa resource that already has tags, retrieve hello existing tags, reformat that value, and reapply hello existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="059db-125">tooapply tutti i tag da un gruppo tooits di risorse, e *non mantenere i tag esistenti risorse hello*, utilizzare hello lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="059db-125">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

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

<span data-ttu-id="059db-126">tooapply tutti i tag da un gruppo tooits di risorse, e *preservare i tag esistenti risorse*, utilizzare hello lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="059db-126">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources*, use hello following script:</span></span>

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


## <a name="templates"></a><span data-ttu-id="059db-127">Modelli</span><span class="sxs-lookup"><span data-stu-id="059db-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="059db-128">di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="059db-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="059db-129">API REST</span><span class="sxs-lookup"><span data-stu-id="059db-129">REST API</span></span>
<span data-ttu-id="059db-130">Hello portale di Azure e PowerShell utilizzare hello [REST API di gestione risorse](https://docs.microsoft.com/rest/api/resources/) background hello.</span><span class="sxs-lookup"><span data-stu-id="059db-130">hello Azure portal and PowerShell both use hello [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind hello scenes.</span></span> <span data-ttu-id="059db-131">Se è necessario toointegrate tag in un altro ambiente, è possibile ottenere i tag con **ottenere** hello risorse ID e aggiornamento hello set di tag usando un **PATCH** chiamare.</span><span class="sxs-lookup"><span data-stu-id="059db-131">If you need toointegrate tagging into another environment, you can get tags by using **GET** on hello resource ID and update hello set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="059db-132">Tag e fatturazione</span><span class="sxs-lookup"><span data-stu-id="059db-132">Tags and billing</span></span>
<span data-ttu-id="059db-133">È possibile utilizzare tag toogroup i dati di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="059db-133">You can use tags toogroup your billing data.</span></span> <span data-ttu-id="059db-134">Ad esempio, se si eseguono più macchine virtuali per le organizzazioni diverse, è possibile utilizzare hello tag toogroup utilizzo dal centro di costo.</span><span class="sxs-lookup"><span data-stu-id="059db-134">For example, if you are running multiple VMs for different organizations, use hello tags toogroup usage by cost center.</span></span> <span data-ttu-id="059db-135">È anche possibile utilizzare tag toocategorize costi dall'ambiente di runtime, quali l'utilizzo della fatturazione hello per le macchine virtuali in esecuzione nell'ambiente di produzione hello.</span><span class="sxs-lookup"><span data-stu-id="059db-135">You can also use tags toocategorize costs by runtime environment, such as hello billing usage for VMs running in hello production environment.</span></span>


<span data-ttu-id="059db-136">È possibile recuperare informazioni sui tag tramite hello [utilizzo delle risorse di Azure e RateCard APIs](../billing/billing-usage-rate-card-overview.md) o hello utilizzo con valori delimitati da virgole (CSV) file.</span><span class="sxs-lookup"><span data-stu-id="059db-136">You can retrieve information about tags through hello [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or hello usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="059db-137">Si scarica il file di utilizzo hello da hello [portale per gli account Azure](https://account.windowsazure.com/) o [portale EA](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="059db-137">You download hello usage file from hello [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="059db-138">Per ulteriori informazioni sulla toobilling accesso a livello di codice, vedere [ottenere informazioni approfondite del consumo di risorse di Microsoft Azure](../billing/billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="059db-138">For more information about programmatic access toobilling information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="059db-139">Per le operazioni API REST, vedere [Riferimento API REST alla fatturazione di Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span><span class="sxs-lookup"><span data-stu-id="059db-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="059db-140">Quando si scarica utilizzo hello CSV per i servizi che supportano i tag con fatturazione, tag di hello vengono visualizzati in hello **tag** colonna.</span><span class="sxs-lookup"><span data-stu-id="059db-140">When you download hello usage CSV for services that support tags with billing, hello tags appear in hello **Tags** column.</span></span> <span data-ttu-id="059db-141">Per altre informazioni, vedere [Comprendere la fattura per Microsoft Azure](../billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="059db-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![Vedere i tag della fatturazione](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="059db-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="059db-143">Next steps</span></span>
* <span data-ttu-id="059db-144">È possibile applicare restrizioni e convenzioni all'interno della sottoscrizione tramite criteri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="059db-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="059db-145">Un criterio che è stato definito potrebbe richiedere che per tutte le risorse sia impostato un determinato tag.</span><span class="sxs-lookup"><span data-stu-id="059db-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="059db-146">Per ulteriori informazioni, vedere [utilizzare criteri toomanage risorse e controllare l'accesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="059db-146">For more information, see [Use policies toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="059db-147">Per un toousing introduzione di Azure PowerShell quando si distribuisce le risorse, vedere [tramite Azure PowerShell con Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="059db-147">For an introduction toousing Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="059db-148">Per un hello toousing introduzione CLI di Azure quando si distribuisce le risorse, vedere [Using hello CLI di Azure per Mac, Linux e Windows con Gestione risorse di Azure](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="059db-148">For an introduction toousing hello Azure CLI when you're deploying resources, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="059db-149">Per un portale di hello toousing introduzione, vedere [Using hello toomanage portale Azure le risorse di Azure](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="059db-149">For an introduction toousing hello portal, see [Using hello Azure portal toomanage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="059db-150">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="059db-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

