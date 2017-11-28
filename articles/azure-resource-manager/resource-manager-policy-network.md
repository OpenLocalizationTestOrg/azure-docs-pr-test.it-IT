---
title: criteri delle risorse per le risorse di rete aaaAzure | Documenti Microsoft
description: Descrive i criteri di gestione risorse di Azure per la Gestione distribuzione hello di risorse di rete.
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
ms.date: 07/05/2017
ms.author: tomfitz
ms.openlocfilehash: a6072c1c30db0a4e4a1cae04efc7828d14069709
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toonetwork-resources"></a><span data-ttu-id="12b48-103">Applicare toonetwork risorse criteri</span><span class="sxs-lookup"><span data-stu-id="12b48-103">Apply resource policies toonetwork resources</span></span>
<span data-ttu-id="12b48-104">In questo articolo viene illustrato un esempio [criterio risorse](resource-manager-policy.md) è possibile applicare tooAzure gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="12b48-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply tooAzure virtual network gateways.</span></span> <span data-ttu-id="12b48-105">Questi criteri assicurano la coerenza per i gateway distribuiti nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="12b48-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="12b48-106">Definire lo SKU dei gateway di rete virtuale consentiti</span><span class="sxs-lookup"><span data-stu-id="12b48-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="12b48-107">Hello seguente criterio limita gli SKU di cui possono essere distribuiti per gateway di rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="12b48-107">hello following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Network/virtualNetworkGateways"
      },
      {
        "not": {
          "field": "Microsoft.Network/virtualNetworkGateways/sku.name",
          "in": [
            "Basic",
            "VpnGw1"
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="12b48-108">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="12b48-108">Next steps</span></span>
* <span data-ttu-id="12b48-109">Dopo aver definito una regola dei criteri (come illustrato in hello precedenti esempi), è necessario toocreate definizione dei criteri hello e assegnarlo tooa ambito.</span><span class="sxs-lookup"><span data-stu-id="12b48-109">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="12b48-110">Hello ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa.</span><span class="sxs-lookup"><span data-stu-id="12b48-110">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="12b48-111">criteri tooassign tramite il portale di hello, vedere [tooassign portale utilizzare Azure e gestire i criteri di risorse](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="12b48-111">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="12b48-112">criteri di tooassign tramite l'API REST, PowerShell o l'interfaccia CLI di Azure, vedere [assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="12b48-112">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="12b48-113">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="12b48-113">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

