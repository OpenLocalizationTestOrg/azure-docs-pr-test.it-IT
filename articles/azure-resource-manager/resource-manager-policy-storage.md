---
title: Criteri delle risorse di Azure per gli account di archiviazione | Documentazione Microsoft
description: Descrive i criteri di Azure Resource Manager per gestire la distribuzione degli account di archiviazione.
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
ms.openlocfilehash: 6612ee61f5c50e743241b92030660cea7ae7094d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="apply-resource-policies-to-storage-accounts"></a><span data-ttu-id="a3c0d-103">Applicare i criteri delle risorse agli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="a3c0d-103">Apply resource policies to storage accounts</span></span>
<span data-ttu-id="a3c0d-104">Questo argomento indica diversi [criteri delle risorse](resource-manager-policy.md) che è possibile applicare agli account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3c0d-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to Azure storage accounts.</span></span> <span data-ttu-id="a3c0d-105">Questi criteri assicurano la coerenza per gli account di archiviazione distribuiti nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="a3c0d-105">These policies ensure consistency for the storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="a3c0d-106">Definire i tipi di account di archiviazione consentiti</span><span class="sxs-lookup"><span data-stu-id="a3c0d-106">Define permitted storage account types</span></span>

<span data-ttu-id="a3c0d-107">I criteri seguenti consentono di limitare i [tipi di account di archiviazione](../storage/common/storage-redundancy.md) che è possibile distribuire:</span><span class="sxs-lookup"><span data-stu-id="a3c0d-107">The following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/sku.name",
          "in": [
            "Standard_LRS",
            "Standard_GRS"
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

<span data-ttu-id="a3c0d-108">Una regola di criterio simile con un parametro per accettare gli SKU consentiti è disponibile come definizione di criterio predefinita.</span><span class="sxs-lookup"><span data-stu-id="a3c0d-108">A similar policy rule with a parameter for accepting the allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="a3c0d-109">Il criterio predefinito ha l'ID risorsa `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span><span class="sxs-lookup"><span data-stu-id="a3c0d-109">The built-in policy has the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="a3c0d-110">Definire il livello di accesso consentito</span><span class="sxs-lookup"><span data-stu-id="a3c0d-110">Define permitted access tier</span></span>

<span data-ttu-id="a3c0d-111">I criteri seguenti specificano il tipo di [livello di accesso](../storage/blobs/storage-blob-storage-tiers.md) che è possibile definire per gli account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="a3c0d-111">The following policy specifies the type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="a3c0d-112">Verificare che la crittografia sia abilitata</span><span class="sxs-lookup"><span data-stu-id="a3c0d-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="a3c0d-113">I criteri seguenti richiedono l'abilitazione della [crittografia del servizio di archiviazione](../storage/common/storage-service-encryption.md) per tutti gli account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="a3c0d-113">The following policy requires all storage accounts to enable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/enableBlobEncryption",
          "equals": "true"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

<span data-ttu-id="a3c0d-114">Questa regola di criterio è anche disponibile come definizione di criterio predefinita con l'ID risorsa `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span><span class="sxs-lookup"><span data-stu-id="a3c0d-114">This policy rule is also available as a built-in policy definition with the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3c0d-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3c0d-115">Next steps</span></span>
* <span data-ttu-id="a3c0d-116">Dopo aver definito una regola di criterio, come mostrato negli esempi precedenti, è necessario creare la definizione di criterio e assegnarla a un ambito.</span><span class="sxs-lookup"><span data-stu-id="a3c0d-116">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="a3c0d-117">L'ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa.</span><span class="sxs-lookup"><span data-stu-id="a3c0d-117">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="a3c0d-118">Per assegnare i criteri tramite il portale, vedere [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) (Usare il portale di Azure per assegnare e gestire i criteri delle risorse).</span><span class="sxs-lookup"><span data-stu-id="a3c0d-118">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="a3c0d-119">Per assegnare i criteri tramite l'API REST, PowerShell o l'interfaccia della riga di comando di Azure, vedere [Assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="a3c0d-119">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="a3c0d-120">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="a3c0d-120">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

