---
title: Criteri delle risorse di Azure per le risorse di rete | Microsoft Docs
description: Descrive i criteri di Azure Resource Manager per gestire la distribuzione delle risorse di rete.
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
ms.openlocfilehash: bca66bbdd9da9b3e4099d0d961f42c9368a17f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-to-network-resources"></a><span data-ttu-id="c5031-103">Applicare i criteri delle risorse alle risorse di rete</span><span class="sxs-lookup"><span data-stu-id="c5031-103">Apply resource policies to network resources</span></span>
<span data-ttu-id="c5031-104">In questo articolo viene illustrato un esempio di [criteri delle risorse](resource-manager-policy.md) che è possibile applicare ai gateway di rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5031-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply to Azure virtual network gateways.</span></span> <span data-ttu-id="c5031-105">Questi criteri assicurano la coerenza per i gateway distribuiti nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="c5031-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="c5031-106">Definire lo SKU dei gateway di rete virtuale consentiti</span><span class="sxs-lookup"><span data-stu-id="c5031-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="c5031-107">I criteri seguenti consentono di limitare gli SKU che è possibile distribuire per i gateway di rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="c5031-107">The following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c5031-108">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c5031-108">Next steps</span></span>
* <span data-ttu-id="c5031-109">Dopo aver definito una regola di criterio, come mostrato negli esempi precedenti, è necessario creare la definizione di criterio e assegnarla a un ambito.</span><span class="sxs-lookup"><span data-stu-id="c5031-109">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="c5031-110">L'ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa.</span><span class="sxs-lookup"><span data-stu-id="c5031-110">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="c5031-111">Per assegnare i criteri tramite il portale, vedere [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) (Usare il portale di Azure per assegnare e gestire i criteri delle risorse).</span><span class="sxs-lookup"><span data-stu-id="c5031-111">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="c5031-112">Per assegnare i criteri tramite l'API REST, PowerShell o l'interfaccia della riga di comando di Azure, vedere [Assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="c5031-112">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="c5031-113">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="c5031-113">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

