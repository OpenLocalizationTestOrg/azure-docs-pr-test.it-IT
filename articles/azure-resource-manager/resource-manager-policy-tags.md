---
title: criteri per i tag delle risorse aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="7e5dd-103">Applicare criteri delle risorse per i tag</span><span class="sxs-lookup"><span data-stu-id="7e5dd-103">Apply resource policies for tags</span></span>

<span data-ttu-id="7e5dd-104">In questo argomento sono disponibili regole di criteri comuni che è possibile applicare tooensure l'utilizzo coerente di tag alle risorse.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-104">This topic provides common policy rules you can apply tooensure consistent use of tags on resources.</span></span>

<span data-ttu-id="7e5dd-105">L'applicazione di una sottoscrizione con le risorse esistenti o un gruppo di risorse tooa criteri tag non è applicabile modo retroattivo risorse toothose di hello criteri.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-105">Applying a tag policy tooa resource group or subscription with existing resources does not retroactively apply hello policy toothose resources.</span></span> <span data-ttu-id="7e5dd-106">criteri di hello tooenforce su tali risorse, attivare un toohello aggiornamento risorse esistenti.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-106">tooenforce hello policies on those resources, trigger an update toohello existing resources.</span></span> <span data-ttu-id="7e5dd-107">Questo articolo include un esempio di PowerShell per l'attivazione di un aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="7e5dd-108">Assicurarsi che tutte le risorse di un gruppo di risorse abbiano un tag/valore</span><span class="sxs-lookup"><span data-stu-id="7e5dd-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="7e5dd-109">Un requisito comune è che tutte le risorse di un gruppo di risorse abbiano un determinato tag e valore.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="7e5dd-110">Questo requisito è spesso necessario tootrack costi dal reparto.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-110">This requirement is often needed tootrack costs by department.</span></span> <span data-ttu-id="7e5dd-111">è necessario soddisfare Hello seguenti condizioni:</span><span class="sxs-lookup"><span data-stu-id="7e5dd-111">hello following conditions must be met:</span></span>

* <span data-ttu-id="7e5dd-112">Hello richiesto tag e il valore vengono aggiunti toonew e risorse che non contengono tag hello aggiornate.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-112">hello required tag and value are appended toonew and updated resources that do not have hello tag.</span></span>
* <span data-ttu-id="7e5dd-113">Hello necessario tag e valore non può essere rimosso da tutte le risorse esistenti.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-113">hello required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="7e5dd-114">Questo requisito è stato possibile mediante l'applicazione di gruppo di risorse di due criteri predefiniti tooa.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-114">You accomplish this requirement by applying two built-in policies tooa resource group.</span></span>

| <span data-ttu-id="7e5dd-115">ID</span><span class="sxs-lookup"><span data-stu-id="7e5dd-115">ID</span></span> | <span data-ttu-id="7e5dd-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7e5dd-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="7e5dd-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="7e5dd-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="7e5dd-118">Si applica un tag obbligatorio e il relativo valore predefinito quando non viene specificato dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-118">Applies a required tag and its default value when it is not specified by hello user.</span></span> |
| <span data-ttu-id="7e5dd-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="7e5dd-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="7e5dd-120">Applica un tag obbligatorio e il relativo valore.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="7e5dd-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e5dd-121">PowerShell</span></span>

<span data-ttu-id="7e5dd-122">lo script di PowerShell seguente Hello assegna gruppo di risorse tooa definizioni hello due criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-122">hello following PowerShell script assigns hello two built-in policy definitions tooa resource group.</span></span> <span data-ttu-id="7e5dd-123">Prima di eseguire script hello, assegnare il gruppo di risorse di tutti i tag richiesti toohello.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-123">Before running hello script, assign all required tags toohello resource group.</span></span> <span data-ttu-id="7e5dd-124">È richiesto per le risorse nel gruppo hello hello ogni tag per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-124">Each tag on hello resource group is required for hello resources in hello group.</span></span> <span data-ttu-id="7e5dd-125">gruppi di risorse tooall tooassign nella sottoscrizione, non forniscono hello `-Name` parametro durante il recupero di gruppi di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-125">tooassign tooall resource groups in your subscription, do not provide hello `-Name` parameter when getting hello resource groups.</span></span>

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

<span data-ttu-id="7e5dd-126">Dopo l'assegnazione di criteri di hello, è possibile attivare un tooall di aggiornamento esistente risorse tooenforce hello tag i criteri che sono stati aggiunti.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-126">After assigning hello policies, you can trigger an update tooall existing resources tooenforce hello tag policies you have added.</span></span> <span data-ttu-id="7e5dd-127">Hello lo script seguente consente di mantenere qualsiasi altro tag già presente nel risorse hello:</span><span class="sxs-lookup"><span data-stu-id="7e5dd-127">hello following script retains any other tags that existed on hello resources:</span></span>

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

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="7e5dd-128">Richiedere tag per un tipo di rosorsa</span><span class="sxs-lookup"><span data-stu-id="7e5dd-128">Require tags for a resource type</span></span>
<span data-ttu-id="7e5dd-129">Hello di esempio seguente viene illustrato come gli operatori logici di toonest toorequire un'applicazione tag per un solo tipo di risorsa specificata (in questo caso, gli account di archiviazione).</span><span class="sxs-lookup"><span data-stu-id="7e5dd-129">hello following example shows how toonest logical operators toorequire an application tag for only a specified resource type (in this case, storage accounts).</span></span>

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

## <a name="require-tag"></a><span data-ttu-id="7e5dd-130">Tag richiesto</span><span class="sxs-lookup"><span data-stu-id="7e5dd-130">Require tag</span></span>
<span data-ttu-id="7e5dd-131">Hello seguente criterio Nega le richieste che non dispongono di un tag che contiene "costCenter" chiave (qualsiasi valore può essere applicato):</span><span class="sxs-lookup"><span data-stu-id="7e5dd-131">hello following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7e5dd-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7e5dd-132">Next steps</span></span>
* <span data-ttu-id="7e5dd-133">Dopo aver definito una regola dei criteri (come illustrato in hello precedenti esempi), è necessario toocreate definizione dei criteri hello e assegnarlo tooa ambito.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-133">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="7e5dd-134">Hello ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa.</span><span class="sxs-lookup"><span data-stu-id="7e5dd-134">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="7e5dd-135">criteri tooassign tramite il portale di hello, vedere [tooassign portale utilizzare Azure e gestire i criteri di risorse](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7e5dd-135">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="7e5dd-136">criteri di tooassign tramite l'API REST, PowerShell o l'interfaccia CLI di Azure, vedere [assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="7e5dd-136">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="7e5dd-137">Per i criteri di tooresource un'introduzione, vedere [Panoramica criteri delle risorse](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="7e5dd-137">For an introduction tooresource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="7e5dd-138">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="7e5dd-138">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

