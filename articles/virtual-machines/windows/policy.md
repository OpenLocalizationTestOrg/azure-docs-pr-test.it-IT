---
title: sicurezza aaaEnforce con i criteri in macchine virtuali di Windows in Azure | Documenti Microsoft
description: Come tooapply tooan un criterio macchina virtuale di Windows Azure Resource Manager
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
ms.openlocfilehash: b31c8a03ecf8eed6a929f97fe4146ea14364404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toowindows-vms-with-azure-resource-manager"></a><span data-ttu-id="965f7-103">Applicare i criteri tooWindows macchine virtuali con Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="965f7-103">Apply policies tooWindows VMs with Azure Resource Manager</span></span>
<span data-ttu-id="965f7-104">Con i criteri di un'organizzazione può applicare varie convenzioni e le regole di organizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="965f7-104">By using policies, an organization can enforce various conventions and rules throughout hello enterprise.</span></span> <span data-ttu-id="965f7-105">Imposizione del comportamento desiderato hello può ridurre i rischi contribuendo toohello successo dell'organizzazione hello stesso.</span><span class="sxs-lookup"><span data-stu-id="965f7-105">Enforcement of hello desired behavior can help mitigate risk while contributing toohello success of hello organization.</span></span> <span data-ttu-id="965f7-106">In questo articolo si descrivono come utilizzare il comportamento di gestione risorse di Azure criteri toodefine hello desiderato per le macchine virtuali dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="965f7-106">In this article, we describe how you can use Azure Resource Manager policies toodefine hello desired behavior for your organization’s Virtual Machines.</span></span>

<span data-ttu-id="965f7-107">Per toopolicies un'introduzione, vedere [risorse toomanage criteri di utilizzo e controllare l'accesso](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="965f7-107">For an introduction toopolicies, see [Use Policy toomanage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="965f7-108">Macchine virtuali permesse</span><span class="sxs-lookup"><span data-stu-id="965f7-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="965f7-109">tooensure che le macchine virtuali per l'organizzazione sono compatibili con un'applicazione, è possibile limitare hello sistemi operativi è consentito.</span><span class="sxs-lookup"><span data-stu-id="965f7-109">tooensure that virtual machines for your organization are compatible with an application, you can restrict hello permitted operating systems.</span></span> <span data-ttu-id="965f7-110">Nel seguente esempio di criterio di hello, si consente solo toobe di macchine virtuali di Windows Server 2012 R2 Datacenter creato:</span><span class="sxs-lookup"><span data-stu-id="965f7-110">In hello following policy example, you allow only Windows Server 2012 R2 Datacenter Virtual Machines toobe created:</span></span>

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

<span data-ttu-id="965f7-111">Utilizzare un hello toomodify con caratteri jolly precedente tooallow criteri qualsiasi immagine di Windows Server Datacenter:</span><span class="sxs-lookup"><span data-stu-id="965f7-111">Use a wild card toomodify hello preceding policy tooallow any Windows Server Datacenter image:</span></span>

```json
{
  "field": "Microsoft.Compute/imageSku",
  "like": "*Datacenter"
}
```

<span data-ttu-id="965f7-112">Utilizzare anyOf toomodify hello precedente tooallow criteri qualsiasi Data Center di Windows Server 2012 R2 o immagine superiore:</span><span class="sxs-lookup"><span data-stu-id="965f7-112">Use anyOf toomodify hello preceding policy tooallow any Windows Server 2012 R2 Datacenter or higher image:</span></span>

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

<span data-ttu-id="965f7-113">Per informazioni sui campi dei criteri, vedere [Alias dei criteri](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="965f7-113">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="965f7-114">Dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="965f7-114">Managed disks</span></span>

<span data-ttu-id="965f7-115">toorequire hello utilizzo di dischi gestiti, utilizzare hello seguenti criteri:</span><span class="sxs-lookup"><span data-stu-id="965f7-115">toorequire hello use of managed disks, use hello following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="965f7-116">Immagini per macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="965f7-116">Images for Virtual Machines</span></span>

<span data-ttu-id="965f7-117">Per motivi di sicurezza, è possibile richiedere che solo le immagini personalizzate approvate vengano distribuite nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="965f7-117">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="965f7-118">È possibile specificare gruppo di risorse hello contenente immagini hello approvato o immagini approvate specifico hello.</span><span class="sxs-lookup"><span data-stu-id="965f7-118">You can specify either hello resource group that contains hello approved images, or hello specific approved images.</span></span>

<span data-ttu-id="965f7-119">Hello di esempio seguente richiede le immagini da un gruppo di risorse approvati:</span><span class="sxs-lookup"><span data-stu-id="965f7-119">hello following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="965f7-120">Hello esempio seguente specifica immagine hello approvato ID:</span><span class="sxs-lookup"><span data-stu-id="965f7-120">hello following example specifies hello approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="965f7-121">Estensioni di macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="965f7-121">Virtual Machine extensions</span></span>

<span data-ttu-id="965f7-122">È opportuno tooforbid utilizzo di determinati tipi di estensioni.</span><span class="sxs-lookup"><span data-stu-id="965f7-122">You may want tooforbid usage of certain types of extensions.</span></span> <span data-ttu-id="965f7-123">Un'estensione potrebbe non essere ad esempio compatibile con determinate immagini di macchina virtuale personalizzata.</span><span class="sxs-lookup"><span data-stu-id="965f7-123">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="965f7-124">Hello seguente esempio viene illustrato come tooblock un'estensione specifica.</span><span class="sxs-lookup"><span data-stu-id="965f7-124">hello following example shows how tooblock a specific extension.</span></span> <span data-ttu-id="965f7-125">Usa toodetermine server di pubblicazione e il tipo cui tooblock di estensione.</span><span class="sxs-lookup"><span data-stu-id="965f7-125">It uses publisher and type toodetermine which extension tooblock.</span></span>

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


## <a name="azure-hybrid-use-benefit"></a><span data-ttu-id="965f7-126">Vantaggio Azure Hybrid Use</span><span class="sxs-lookup"><span data-stu-id="965f7-126">Azure Hybrid Use Benefit</span></span>

<span data-ttu-id="965f7-127">Quando si dispone di una licenza in locale, è possibile salvare l'onere di licenza hello nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="965f7-127">When you have an on-premise license, you can save hello license fee on your virtual machines.</span></span> <span data-ttu-id="965f7-128">Quando non si dispone di licenza di hello, si dovrebbe proibire l'opzione hello.</span><span class="sxs-lookup"><span data-stu-id="965f7-128">When you don't have hello license, you should forbid hello option.</span></span> <span data-ttu-id="965f7-129">Hello seguente criteri impedisce l'uso del vantaggio di utilizzare Azure ibrida (AHUB):</span><span class="sxs-lookup"><span data-stu-id="965f7-129">hello following policy forbids usage of Azure Hybrid Use Benefit (AHUB):</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="965f7-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="965f7-130">Next steps</span></span>
* <span data-ttu-id="965f7-131">Dopo aver definito una regola dei criteri (come illustrato in hello precedenti esempi), è necessario toocreate definizione dei criteri hello e assegnarlo tooa ambito.</span><span class="sxs-lookup"><span data-stu-id="965f7-131">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="965f7-132">Hello ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa.</span><span class="sxs-lookup"><span data-stu-id="965f7-132">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="965f7-133">criteri tooassign tramite il portale di hello, vedere [tooassign portale utilizzare Azure e gestire i criteri di risorse](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="965f7-133">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="965f7-134">criteri di tooassign tramite l'API REST, PowerShell o l'interfaccia CLI di Azure, vedere [assegnare e gestire i criteri tramite script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="965f7-134">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="965f7-135">Per i criteri di tooresource un'introduzione, vedere [Panoramica criteri delle risorse](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="965f7-135">For an introduction tooresource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="965f7-136">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="965f7-136">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
