---
title: Applicare la sicurezza con criteri a macchine virtuali Windows in Azure | Documentazione Microsoft
description: Come applicare criteri a una macchina virtuale Windows di Azure Resource Manager
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0b71ba54-01db-43ad-9bca-8ab358ae141b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: kasing
ms.openlocfilehash: 246f5958478fd6d9afc9ba990413ab08429bd25d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="apply-policies-to-windows-vms-with-azure-resource-manager"></a><span data-ttu-id="e8a5a-103">Applicare criteri alle macchine virtuali Windows con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e8a5a-103">Apply policies to Windows VMs with Azure Resource Manager</span></span>
<span data-ttu-id="e8a5a-104">Tramite i criteri è possibile imporre diverse convenzioni e regole in tutta l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="e8a5a-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span></span> <span data-ttu-id="e8a5a-105">L'imposizione del comportamento desiderato consente di attenuare i rischi, contribuendo nello stesso tempo al successo dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="e8a5a-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span></span> <span data-ttu-id="e8a5a-106">Questo articolo illustra come usare i criteri di Azure Resource Manager per definire il comportamento desiderato per le macchine virtuali dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="e8a5a-106">In this article, we describe how you can use Azure Resource Manager policies to define the desired behavior for your organization’s Virtual Machines.</span></span>

<span data-ttu-id="e8a5a-107">Per un'introduzione ai criteri, vedere [Usare i criteri per gestire le risorse e controllare l'accesso](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="e8a5a-107">For an introduction to policies, see [Use Policy to manage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="e8a5a-108">Macchine virtuali permesse</span><span class="sxs-lookup"><span data-stu-id="e8a5a-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="e8a5a-109">Per assicurarsi che le macchine virtuali dell'organizzazione siano compatibili con un'applicazione, è possibile limitare i sistemi operativi consentiti.</span><span class="sxs-lookup"><span data-stu-id="e8a5a-109">To ensure that virtual machines for your organization are compatible with an application, you can restrict the permitted operating systems.</span></span> <span data-ttu-id="e8a5a-110">Nell'esempio di criterio che segue si consente solo la creazione di macchine virtuali Windows Server 2012 R2 Datacenter:</span><span class="sxs-lookup"><span data-stu-id="e8a5a-110">In the following policy example, you allow only Windows Server 2012 R2 Datacenter Virtual Machines to be created:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "in": [
          "Microsoft.Compute/disks",
          "Microsoft.Compute/virtualMachines",
          "Microsoft.Compute/VirtualMachineScaleSets"
        ]
      },
      {
        "not": {
          "allOf": [
            {
              "field": "Microsoft.Compute/imagePublisher",
              "in": [
                "MicrosoftWindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "WindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "2012-R2-Datacenter"
              ]
            },
            {
              "field": "Microsoft.Compute/imageVersion",
              "in": [
                "latest"
              ]
            }
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

<span data-ttu-id="e8a5a-111">Per modificare il criterio precedente e consentire qualsiasi immagine Windows Server Datacenter, usare un carattere jolly:</span><span class="sxs-lookup"><span data-stu-id="e8a5a-111">Use a wild card to modify the preceding policy to allow any Windows Server Datacenter image:</span></span>

```json
{
  "field": "Microsoft.Compute/imageSku",
  "like": "*Datacenter"
}
```

<span data-ttu-id="e8a5a-112">Per modificare il criterio precedente e consentire qualsiasi immagine Windows Server 2012 R2 Datacenter o versione successiva, usare anyOf:</span><span class="sxs-lookup"><span data-stu-id="e8a5a-112">Use anyOf to modify the preceding policy to allow any Windows Server 2012 R2 Datacenter or higher image:</span></span>

```json
{
  "anyOf": [
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2012-R2-Datacenter*"
    },
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2016-Datacenter*"
    }
  ]
}
```

<span data-ttu-id="e8a5a-113">Per informazioni sui campi dei criteri, vedere [Alias dei criteri](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="e8a5a-113">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="e8a5a-114">Dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="e8a5a-114">Managed disks</span></span>

<span data-ttu-id="e8a5a-115">Per richiedere l'uso dei dischi gestiti, usare il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="e8a5a-115">To require the use of managed disks, use the following policy:</span></span>

```json
{
  "if": {
    "anyOf": [
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/virtualMachines"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/osDisk.uri",
            "exists": true
          }
        ]
      },
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/VirtualMachineScaleSets"
          },
          {
            "anyOf": [
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osDisk.vhdContainers",
                "exists": true
              },
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl",
                "exists": true
              }
            ]
          }
        ]
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="images-for-virtual-machines"></a><span data-ttu-id="e8a5a-116">Immagini per macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e8a5a-116">Images for Virtual Machines</span></span>

<span data-ttu-id="e8a5a-117">Per motivi di sicurezza, è possibile richiedere che solo le immagini personalizzate approvate vengano distribuite nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="e8a5a-117">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="e8a5a-118">È possibile specificare il gruppo di risorse che contiene le immagini approvate o immagini approvate specifiche.</span><span class="sxs-lookup"><span data-stu-id="e8a5a-118">You can specify either the resource group that contains the approved images, or the specific approved images.</span></span>

<span data-ttu-id="e8a5a-119">L'esempio seguente richiede le immagini da un gruppo di risorse approvato:</span><span class="sxs-lookup"><span data-stu-id="e8a5a-119">The following example requires images from an approved resource group:</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in": [
                    "Microsoft.Compute/virtualMachines",
                    "Microsoft.Compute/VirtualMachineScaleSets"
                ]
            },
            {
                "not": {
                    "field": "Microsoft.Compute/imageId",
                    "contains": "resourceGroups/CustomImage"
                }
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
} 
```

<span data-ttu-id="e8a5a-120">L'esempio seguente specifica gli ID immagine approvati:</span><span class="sxs-lookup"><span data-stu-id="e8a5a-120">The following example specifies the approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="e8a5a-121">Estensioni di macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e8a5a-121">Virtual Machine extensions</span></span>

<span data-ttu-id="e8a5a-122">È possibile che si desideri proibire l'utilizzo di tipi specifici di estensioni.</span><span class="sxs-lookup"><span data-stu-id="e8a5a-122">You may want to forbid usage of certain types of extensions.</span></span> <span data-ttu-id="e8a5a-123">Un'estensione potrebbe non essere ad esempio compatibile con determinate immagini di macchina virtuale personalizzata.</span><span class="sxs-lookup"><span data-stu-id="e8a5a-123">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="e8a5a-124">L'esempio seguente mostra come bloccare un'estensione specifica.</span><span class="sxs-lookup"><span data-stu-id="e8a5a-124">The following example shows how to block a specific extension.</span></span> <span data-ttu-id="e8a5a-125">Usa server di pubblicazione e tipo per determinare l'estensione da bloccare.</span><span class="sxs-lookup"><span data-stu-id="e8a5a-125">It uses publisher and type to determine which extension to block.</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Compute/virtualMachines/extensions"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                "equals": "Microsoft.Compute"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/type",
                "equals": "{extension-type}"

      }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```


## <a name="azure-hybrid-use-benefit"></a><span data-ttu-id="e8a5a-126">Vantaggio Azure Hybrid Use</span><span class="sxs-lookup"><span data-stu-id="e8a5a-126">Azure Hybrid Use Benefit</span></span>

<span data-ttu-id="e8a5a-127">Quando si dispone di una licenza in locale, è possibile risparmiare il costo della licenza sulle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e8a5a-127">When you have an on-premise license, you can save the license fee on your virtual machines.</span></span> <span data-ttu-id="e8a5a-128">Se non si dispone di licenza, è consigliabile impedire questa possibilità.</span><span class="sxs-lookup"><span data-stu-id="e8a5a-128">When you don't have the license, you should forbid the option.</span></span> <span data-ttu-id="e8a5a-129">I criteri seguenti impediscono l'uso del vantaggio Azure Hybrid Use (AHUB):</span><span class="sxs-lookup"><span data-stu-id="e8a5a-129">The following policy forbids usage of Azure Hybrid Use Benefit (AHUB):</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in":[ "Microsoft.Compute/virtualMachines","Microsoft.Compute/VirtualMachineScaleSets"]
            },
            {
                "field": "Microsoft.Compute/licenseType",
                "exists": true
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="e8a5a-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e8a5a-130">Next steps</span></span>
* <span data-ttu-id="e8a5a-131">Dopo aver definito una regola di criterio, come mostrato negli esempi precedenti, è necessario creare la definizione di criterio e assegnarla a un ambito.</span><span class="sxs-lookup"><span data-stu-id="e8a5a-131">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="e8a5a-132">L'ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa.</span><span class="sxs-lookup"><span data-stu-id="e8a5a-132">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="e8a5a-133">Per assegnare i criteri tramite il portale, vedere [Use Azure portal to assign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md) (Usare il portale di Azure per assegnare e gestire i criteri delle risorse).</span><span class="sxs-lookup"><span data-stu-id="e8a5a-133">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="e8a5a-134">Per assegnare i criteri tramite l'API REST, PowerShell o l'interfaccia della riga di comando di Azure, vedere [Assegnare e gestire i criteri tramite script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="e8a5a-134">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="e8a5a-135">Per un'introduzione ai criteri delle risorse, vedere [Usare i criteri per gestire le risorse e controllare l'accesso](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="e8a5a-135">For an introduction to resource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="e8a5a-136">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="e8a5a-136">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
