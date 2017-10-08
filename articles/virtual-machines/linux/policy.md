---
title: sicurezza aaaEnforce con i criteri in macchine virtuali Linux in Azure | Documenti Microsoft
description: Come tooapply tooan un criterio macchina virtuale Linux di Azure Resource Manager
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: singhkay
ms.openlocfilehash: 5abd0c937578aba7e72b62c65b4eef9a9737aa2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toolinux-vms-with-azure-resource-manager"></a><span data-ttu-id="4822f-103">Applicare i criteri tooLinux macchine virtuali con Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="4822f-103">Apply policies tooLinux VMs with Azure Resource Manager</span></span>
<span data-ttu-id="4822f-104">Con i criteri di un'organizzazione può applicare varie convenzioni e le regole di organizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="4822f-104">By using policies, an organization can enforce various conventions and rules throughout hello enterprise.</span></span> <span data-ttu-id="4822f-105">Imposizione del comportamento desiderato hello può ridurre i rischi contribuendo toohello successo dell'organizzazione hello stesso.</span><span class="sxs-lookup"><span data-stu-id="4822f-105">Enforcement of hello desired behavior can help mitigate risk while contributing toohello success of hello organization.</span></span> <span data-ttu-id="4822f-106">In questo articolo si descrivono come utilizzare il comportamento di gestione risorse di Azure criteri toodefine hello desiderato per le macchine virtuali dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="4822f-106">In this article, we describe how you can use Azure Resource Manager policies toodefine hello desired behavior for your organization's Virtual Machines.</span></span>

<span data-ttu-id="4822f-107">Per toopolicies un'introduzione, vedere [risorse toomanage criteri di utilizzo e controllare l'accesso](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4822f-107">For an introduction toopolicies, see [Use Policy toomanage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="4822f-108">Macchine virtuali permesse</span><span class="sxs-lookup"><span data-stu-id="4822f-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="4822f-109">tooensure che le macchine virtuali per l'organizzazione sono compatibili con un'applicazione, è possibile limitare hello sistemi operativi è consentito.</span><span class="sxs-lookup"><span data-stu-id="4822f-109">tooensure that virtual machines for your organization are compatible with an application, you can restrict hello permitted operating systems.</span></span> <span data-ttu-id="4822f-110">Nel seguente esempio di criterio di hello, si consentono solo Ubuntu 14.04.2-LTS le macchine virtuali toobe creato.</span><span class="sxs-lookup"><span data-stu-id="4822f-110">In hello following policy example, you allow only Ubuntu 14.04.2-LTS Virtual Machines toobe created.</span></span>

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
                "Canonical"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "UbuntuServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "14.04.2-LTS"
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

<span data-ttu-id="4822f-111">Utilizzare un hello toomodify con caratteri jolly che precede di qualsiasi immagine LTS Ubuntu tooallow criteri:</span><span class="sxs-lookup"><span data-stu-id="4822f-111">Use a wild card toomodify hello preceding policy tooallow any Ubuntu LTS image:</span></span> 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

<span data-ttu-id="4822f-112">Per informazioni sui campi dei criteri, vedere [Alias dei criteri](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="4822f-112">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="4822f-113">Dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="4822f-113">Managed disks</span></span>

<span data-ttu-id="4822f-114">toorequire hello utilizzo di dischi gestiti, utilizzare hello seguenti criteri:</span><span class="sxs-lookup"><span data-stu-id="4822f-114">toorequire hello use of managed disks, use hello following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="4822f-115">Immagini per macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="4822f-115">Images for Virtual Machines</span></span>

<span data-ttu-id="4822f-116">Per motivi di sicurezza, è possibile richiedere che solo le immagini personalizzate approvate vengano distribuite nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="4822f-116">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="4822f-117">È possibile specificare gruppo di risorse hello contenente immagini hello approvato o immagini approvate specifico hello.</span><span class="sxs-lookup"><span data-stu-id="4822f-117">You can specify either hello resource group that contains hello approved images, or hello specific approved images.</span></span>

<span data-ttu-id="4822f-118">Hello di esempio seguente richiede le immagini da un gruppo di risorse approvati:</span><span class="sxs-lookup"><span data-stu-id="4822f-118">hello following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="4822f-119">Hello esempio seguente specifica immagine hello approvato ID:</span><span class="sxs-lookup"><span data-stu-id="4822f-119">hello following example specifies hello approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="4822f-120">Estensioni di macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4822f-120">Virtual Machine extensions</span></span>

<span data-ttu-id="4822f-121">È opportuno tooforbid utilizzo di determinati tipi di estensioni.</span><span class="sxs-lookup"><span data-stu-id="4822f-121">You may want tooforbid usage of certain types of extensions.</span></span> <span data-ttu-id="4822f-122">Un'estensione potrebbe non essere ad esempio compatibile con determinate immagini di macchina virtuale personalizzata.</span><span class="sxs-lookup"><span data-stu-id="4822f-122">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="4822f-123">Hello seguente esempio viene illustrato come tooblock un'estensione specifica.</span><span class="sxs-lookup"><span data-stu-id="4822f-123">hello following example shows how tooblock a specific extension.</span></span> <span data-ttu-id="4822f-124">Usa toodetermine server di pubblicazione e il tipo cui tooblock di estensione.</span><span class="sxs-lookup"><span data-stu-id="4822f-124">It uses publisher and type toodetermine which extension tooblock.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="4822f-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4822f-125">Next steps</span></span>
* <span data-ttu-id="4822f-126">Dopo aver definito una regola dei criteri (come illustrato in hello precedenti esempi), è necessario toocreate definizione dei criteri hello e assegnarlo tooa ambito.</span><span class="sxs-lookup"><span data-stu-id="4822f-126">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="4822f-127">Hello ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa.</span><span class="sxs-lookup"><span data-stu-id="4822f-127">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="4822f-128">criteri tooassign tramite il portale di hello, vedere [tooassign portale utilizzare Azure e gestire i criteri di risorse](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4822f-128">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="4822f-129">criteri di tooassign tramite l'API REST, PowerShell o l'interfaccia CLI di Azure, vedere [assegnare e gestire i criteri tramite script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="4822f-129">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="4822f-130">Per i criteri di tooresource un'introduzione, vedere [Panoramica criteri delle risorse](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4822f-130">For an introduction tooresource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="4822f-131">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="4822f-131">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
