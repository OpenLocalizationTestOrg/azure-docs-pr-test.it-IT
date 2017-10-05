---
title: Criteri delle risorse di Azure per le convenzioni di denominazione| Microsoft Docs
description: Descrive i criteri di Azure Resource Manager per le convenzioni di denominazione delle risorse.
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
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 51b3519bbba8cb4c768bfdd7dadf92fced434f22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="03f6b-103">Applicare criteri delle risorse per nomi e testo</span><span class="sxs-lookup"><span data-stu-id="03f6b-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="03f6b-104">Questo argomento indica diversi [criteri delle risorse](resource-manager-policy.md) che è possibile applicare per stabilire le convenzioni di denominazione e testo.</span><span class="sxs-lookup"><span data-stu-id="03f6b-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to establish naming and text conventions.</span></span> <span data-ttu-id="03f6b-105">Questi criteri assicurano la coerenza per i nomi delle risorse e i valori dei tag.</span><span class="sxs-lookup"><span data-stu-id="03f6b-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="03f6b-106">Impostare la convenzione di denominazione con caratteri jolly</span><span class="sxs-lookup"><span data-stu-id="03f6b-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="03f6b-107">L'esempio seguente illustra l'uso dei caratteri jolly supportato dalla condizione **like**.</span><span class="sxs-lookup"><span data-stu-id="03f6b-107">The following example shows the use of wildcard, which is supported by the **like** condition.</span></span> <span data-ttu-id="03f6b-108">La condizione dichiara che la richiesta deve essere negata se il nome non corrisponde al modello indicato (namePrefix\*nameSuffix):</span><span class="sxs-lookup"><span data-stu-id="03f6b-108">The condition states that if the name does match the mentioned pattern (namePrefix\*nameSuffix) then deny the request:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="03f6b-109">Impostare la convenzione di denominazione con modelli</span><span class="sxs-lookup"><span data-stu-id="03f6b-109">Set naming convention with pattern</span></span>

<span data-ttu-id="03f6b-110">Per specificare che i nomi di risorsa corrispondono a un modello, usare la condizione match.</span><span class="sxs-lookup"><span data-stu-id="03f6b-110">To specify that resource names match a pattern, use the match condition.</span></span> <span data-ttu-id="03f6b-111">Nell'esempio seguente i nomi devono iniziare con `contoso` e contenere altre sei lettere:</span><span class="sxs-lookup"><span data-stu-id="03f6b-111">The following example requires names to start with `contoso` and contain six additional letters:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="03f6b-112">Impostare il modello di data per il valore di tag</span><span class="sxs-lookup"><span data-stu-id="03f6b-112">Set date pattern for tag value</span></span>

<span data-ttu-id="03f6b-113">Per imporre un modello di data di due cifre, trattino, tre lettere, trattino e quattro cifre, usare:</span><span class="sxs-lookup"><span data-stu-id="03f6b-113">To require a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="03f6b-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="03f6b-114">Next steps</span></span>
* <span data-ttu-id="03f6b-115">Dopo aver definito una regola di criterio, come mostrato negli esempi precedenti, è necessario creare la definizione di criterio e assegnarla a un ambito.</span><span class="sxs-lookup"><span data-stu-id="03f6b-115">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="03f6b-116">L'ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa.</span><span class="sxs-lookup"><span data-stu-id="03f6b-116">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="03f6b-117">Per assegnare i criteri tramite il portale, vedere [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) (Usare il portale di Azure per assegnare e gestire i criteri delle risorse).</span><span class="sxs-lookup"><span data-stu-id="03f6b-117">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="03f6b-118">Per assegnare i criteri tramite l'API REST, PowerShell o l'interfaccia della riga di comando di Azure, vedere [Assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="03f6b-118">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="03f6b-119">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="03f6b-119">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

