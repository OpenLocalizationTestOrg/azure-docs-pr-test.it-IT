---
title: criteri per le convenzioni di denominazione delle risorse aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="4b116-103">Applicare criteri delle risorse per nomi e testo</span><span class="sxs-lookup"><span data-stu-id="4b116-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="4b116-104">Questo argomento vengono illustrati diversi [criteri risorse](resource-manager-policy.md) è possibile applicare le convenzioni di denominazione e testo tooestablish.</span><span class="sxs-lookup"><span data-stu-id="4b116-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooestablish naming and text conventions.</span></span> <span data-ttu-id="4b116-105">Questi criteri assicurano la coerenza per i nomi delle risorse e i valori dei tag.</span><span class="sxs-lookup"><span data-stu-id="4b116-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="4b116-106">Impostare la convenzione di denominazione con caratteri jolly</span><span class="sxs-lookup"><span data-stu-id="4b116-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="4b116-107">Hello riportato di seguito utilizzo hello del carattere jolly, che è supportato da hello **come** condizione.</span><span class="sxs-lookup"><span data-stu-id="4b116-107">hello following example shows hello use of wildcard, which is supported by hello **like** condition.</span></span> <span data-ttu-id="4b116-108">Hello condizione indica che se hello nome deve corrispondere modello citato hello (namePrefix\*nameSuffix) quindi negare hello richiesta:</span><span class="sxs-lookup"><span data-stu-id="4b116-108">hello condition states that if hello name does match hello mentioned pattern (namePrefix\*nameSuffix) then deny hello request:</span></span>

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

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="4b116-109">Impostare la convenzione di denominazione con modelli</span><span class="sxs-lookup"><span data-stu-id="4b116-109">Set naming convention with pattern</span></span>

<span data-ttu-id="4b116-110">toospecify che i nomi delle risorse corrispondano a un criterio, utilizzare hello soddisfano una condizione.</span><span class="sxs-lookup"><span data-stu-id="4b116-110">toospecify that resource names match a pattern, use hello match condition.</span></span> <span data-ttu-id="4b116-111">l'esempio Hello necessario toostart nomi con `contoso` e contenere sei lettere aggiuntive:</span><span class="sxs-lookup"><span data-stu-id="4b116-111">hello following example requires names toostart with `contoso` and contain six additional letters:</span></span>

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

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="4b116-112">Impostare il modello di data per il valore di tag</span><span class="sxs-lookup"><span data-stu-id="4b116-112">Set date pattern for tag value</span></span>

<span data-ttu-id="4b116-113">un modello di data di utilizzo di due cifre, trattino, tre lettere, trattino e quattro cifre, toorequire:</span><span class="sxs-lookup"><span data-stu-id="4b116-113">toorequire a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4b116-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4b116-114">Next steps</span></span>
* <span data-ttu-id="4b116-115">Dopo aver definito una regola dei criteri (come illustrato in hello precedenti esempi), è necessario toocreate definizione dei criteri hello e assegnarlo tooa ambito.</span><span class="sxs-lookup"><span data-stu-id="4b116-115">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="4b116-116">Hello ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa.</span><span class="sxs-lookup"><span data-stu-id="4b116-116">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="4b116-117">criteri tooassign tramite il portale di hello, vedere [tooassign portale utilizzare Azure e gestire i criteri di risorse](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4b116-117">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="4b116-118">criteri di tooassign tramite l'API REST, PowerShell o l'interfaccia CLI di Azure, vedere [assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="4b116-118">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="4b116-119">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="4b116-119">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

