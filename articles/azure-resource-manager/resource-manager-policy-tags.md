---
title: Criteri delle risorse di Azure per i tag| Documentazione Microsoft
description: Fornisce esempi di criteri delle risorse per la gestione dei tag delle risorse
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
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 469bd8d637337e5900ea84c6bfaf88064695fb7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="2ca41-103">Applicare criteri delle risorse per i tag</span><span class="sxs-lookup"><span data-stu-id="2ca41-103">Apply resource policies for tags</span></span>

<span data-ttu-id="2ca41-104">Questo argomento fornisce regole di criterio comuni che è possibile applicare per garantire l'uso coerente dei tag delle risorse.</span><span class="sxs-lookup"><span data-stu-id="2ca41-104">This topic provides common policy rules you can apply to ensure consistent use of tags on resources.</span></span>

<span data-ttu-id="2ca41-105">Applicando un criterio di tag a un gruppo di risorse o a una sottoscrizione con risorse esistenti non si applica retroattivamente il criterio a tali risorse.</span><span class="sxs-lookup"><span data-stu-id="2ca41-105">Applying a tag policy to a resource group or subscription with existing resources does not retroactively apply the policy to those resources.</span></span> <span data-ttu-id="2ca41-106">Per applicare i criteri a queste risorse, avviare l'aggiornamento delle risorse esistenti.</span><span class="sxs-lookup"><span data-stu-id="2ca41-106">To enforce the policies on those resources, trigger an update to the existing resources.</span></span> <span data-ttu-id="2ca41-107">Questo articolo include un esempio di PowerShell per l'attivazione di un aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="2ca41-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="2ca41-108">Assicurarsi che tutte le risorse di un gruppo di risorse abbiano un tag/valore</span><span class="sxs-lookup"><span data-stu-id="2ca41-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="2ca41-109">Un requisito comune è che tutte le risorse di un gruppo di risorse abbiano un determinato tag e valore.</span><span class="sxs-lookup"><span data-stu-id="2ca41-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="2ca41-110">Questo requisito è spesso necessario per tenere traccia dei costi per reparto.</span><span class="sxs-lookup"><span data-stu-id="2ca41-110">This requirement is often needed to track costs by department.</span></span> <span data-ttu-id="2ca41-111">Le condizioni seguenti devono essere soddisfatte:</span><span class="sxs-lookup"><span data-stu-id="2ca41-111">The following conditions must be met:</span></span>

* <span data-ttu-id="2ca41-112">Il tag richiesto e il relativo valore vengono accodati alle risorse nuove e aggiornate che non hanno il tag.</span><span class="sxs-lookup"><span data-stu-id="2ca41-112">The required tag and value are appended to new and updated resources that do not have the tag.</span></span>
* <span data-ttu-id="2ca41-113">Non è possibile rimuovere il tag richiesto e il relativo valore da eventuali risorse esistenti.</span><span class="sxs-lookup"><span data-stu-id="2ca41-113">The required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="2ca41-114">È possibile soddisfare questo requisito applicando due criteri predefiniti a un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2ca41-114">You accomplish this requirement by applying two built-in policies to a resource group.</span></span>

| <span data-ttu-id="2ca41-115">ID</span><span class="sxs-lookup"><span data-stu-id="2ca41-115">ID</span></span> | <span data-ttu-id="2ca41-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ca41-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="2ca41-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="2ca41-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="2ca41-118">Applica un tag obbligatorio e il relativo valore predefinito quando non viene specificato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="2ca41-118">Applies a required tag and its default value when it is not specified by the user.</span></span> |
| <span data-ttu-id="2ca41-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="2ca41-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="2ca41-120">Applica un tag obbligatorio e il relativo valore.</span><span class="sxs-lookup"><span data-stu-id="2ca41-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="2ca41-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ca41-121">PowerShell</span></span>

<span data-ttu-id="2ca41-122">Lo script di PowerShell seguente assegna le due definizioni di criteri predefiniti a un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2ca41-122">The following PowerShell script assigns the two built-in policy definitions to a resource group.</span></span> <span data-ttu-id="2ca41-123">Prima di eseguire lo script, assegnare tutti i tag richiesti al gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2ca41-123">Before running the script, assign all required tags to the resource group.</span></span> <span data-ttu-id="2ca41-124">Ogni tag nel gruppo di risorse è richiesto per le risorse nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="2ca41-124">Each tag on the resource group is required for the resources in the group.</span></span> <span data-ttu-id="2ca41-125">Per eseguire l'assegnazione a tutti i gruppi di risorse nella sottoscrizione, non fornire il parametro `-Name` quando si recuperano i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="2ca41-125">To assign to all resource groups in your subscription, do not provide the `-Name` parameter when getting the resource groups.</span></span>

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

<span data-ttu-id="2ca41-126">Dopo aver assegnato i criteri, è possibile attivare l'aggiornamento di tutte le risorse esistenti per applicare i criteri dei tag aggiunti.</span><span class="sxs-lookup"><span data-stu-id="2ca41-126">After assigning the policies, you can trigger an update to all existing resources to enforce the tag policies you have added.</span></span> <span data-ttu-id="2ca41-127">Lo script seguente consente di mantenere gli altri tag presenti nelle risorse:</span><span class="sxs-lookup"><span data-stu-id="2ca41-127">The following script retains any other tags that existed on the resources:</span></span>

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="2ca41-128">Richiedere tag per un tipo di rosorsa</span><span class="sxs-lookup"><span data-stu-id="2ca41-128">Require tags for a resource type</span></span>
<span data-ttu-id="2ca41-129">L'esempio seguente illustra come nidificare gli operatori logici per richiedere un tag dell'applicazione solo per un determinato tipo di risorsa (in questo caso gli account di archiviazione).</span><span class="sxs-lookup"><span data-stu-id="2ca41-129">The following example shows how to nest logical operators to require an application tag for only a specified resource type (in this case, storage accounts).</span></span>

```json
{
    "if": {
        "allOf": [
          {
            "not": {
              "field": "tags",
              "containsKey": "application"
            }
          },
          {
            "field": "type",
            "equals": "Microsoft.Storage/storageAccounts"
          }
        ]
    },
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a><span data-ttu-id="2ca41-130">Tag richiesto</span><span class="sxs-lookup"><span data-stu-id="2ca41-130">Require tag</span></span>
<span data-ttu-id="2ca41-131">Il criterio seguente nega le richieste senza un tag con la chiave "costCenter" (è possibile applicare qualsiasi valore):</span><span class="sxs-lookup"><span data-stu-id="2ca41-131">The following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="2ca41-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2ca41-132">Next steps</span></span>
* <span data-ttu-id="2ca41-133">Dopo aver definito una regola di criterio, come mostrato negli esempi precedenti, è necessario creare la definizione di criterio e assegnarla a un ambito.</span><span class="sxs-lookup"><span data-stu-id="2ca41-133">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="2ca41-134">L'ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa.</span><span class="sxs-lookup"><span data-stu-id="2ca41-134">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="2ca41-135">Per assegnare i criteri tramite il portale, vedere [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) (Usare il portale di Azure per assegnare e gestire i criteri delle risorse).</span><span class="sxs-lookup"><span data-stu-id="2ca41-135">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="2ca41-136">Per assegnare i criteri tramite l'API REST, PowerShell o l'interfaccia della riga di comando di Azure, vedere [Assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="2ca41-136">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="2ca41-137">Per un'introduzione ai criteri delle risorse, vedere [Usare i criteri per gestire le risorse e controllare l'accesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="2ca41-137">For an introduction to resource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="2ca41-138">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="2ca41-138">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

