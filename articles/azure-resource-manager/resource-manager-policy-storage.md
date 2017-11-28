---
title: criteri delle risorse per gli account di archiviazione aaaAzure | Documenti Microsoft
description: Descrive i criteri di gestione risorse di Azure per la Gestione distribuzione hello di account di archiviazione.
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
ms.openlocfilehash: d37fc4bcf7cdec71b0e14f6231fc138bfb6a7893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toostorage-accounts"></a><span data-ttu-id="590e5-103">Applicare gli account toostorage criteri delle risorse</span><span class="sxs-lookup"><span data-stu-id="590e5-103">Apply resource policies toostorage accounts</span></span>
<span data-ttu-id="590e5-104">Questo argomento vengono illustrati diversi [criteri risorse](resource-manager-policy.md) è possibile applicare gli account di archiviazione tooAzure.</span><span class="sxs-lookup"><span data-stu-id="590e5-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooAzure storage accounts.</span></span> <span data-ttu-id="590e5-105">Questi criteri assicurano la coerenza per gli account di archiviazione hello distribuita nella propria organizzazione.</span><span class="sxs-lookup"><span data-stu-id="590e5-105">These policies ensure consistency for hello storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="590e5-106">Definire i tipi di account di archiviazione consentiti</span><span class="sxs-lookup"><span data-stu-id="590e5-106">Define permitted storage account types</span></span>

<span data-ttu-id="590e5-107">Hello seguente criterio limita le [tipi di account di archiviazione](../storage/common/storage-redundancy.md) può essere distribuito:</span><span class="sxs-lookup"><span data-stu-id="590e5-107">hello following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

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

<span data-ttu-id="590e5-108">Una regola dei criteri simile con un parametro per accettare gli SKU consentito hello è disponibile come una definizione dei criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="590e5-108">A similar policy rule with a parameter for accepting hello allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="590e5-109">criteri predefiniti Hello con ID risorsa hello `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span><span class="sxs-lookup"><span data-stu-id="590e5-109">hello built-in policy has hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="590e5-110">Definire il livello di accesso consentito</span><span class="sxs-lookup"><span data-stu-id="590e5-110">Define permitted access tier</span></span>

<span data-ttu-id="590e5-111">i criteri seguenti Hello specificano il tipo di hello di [livello di accesso](../storage/blobs/storage-blob-storage-tiers.md) che può essere specificata per gli account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="590e5-111">hello following policy specifies hello type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

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

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="590e5-112">Verificare che la crittografia sia abilitata</span><span class="sxs-lookup"><span data-stu-id="590e5-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="590e5-113">i criteri seguenti Hello richiedono tutti tooenable gli account di archiviazione [la crittografia del servizio di archiviazione](../storage/common/storage-service-encryption.md):</span><span class="sxs-lookup"><span data-stu-id="590e5-113">hello following policy requires all storage accounts tooenable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

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

<span data-ttu-id="590e5-114">Questa regola dei criteri è disponibile anche come una definizione dei criteri predefinite con l'ID della risorsa hello `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span><span class="sxs-lookup"><span data-stu-id="590e5-114">This policy rule is also available as a built-in policy definition with hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="590e5-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="590e5-115">Next steps</span></span>
* <span data-ttu-id="590e5-116">Dopo aver definito una regola dei criteri (come illustrato in hello precedenti esempi), è necessario toocreate definizione dei criteri hello e assegnarlo tooa ambito.</span><span class="sxs-lookup"><span data-stu-id="590e5-116">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="590e5-117">Hello ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa.</span><span class="sxs-lookup"><span data-stu-id="590e5-117">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="590e5-118">criteri tooassign tramite il portale di hello, vedere [tooassign portale utilizzare Azure e gestire i criteri di risorse](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="590e5-118">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="590e5-119">criteri di tooassign tramite l'API REST, PowerShell o l'interfaccia CLI di Azure, vedere [assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="590e5-119">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="590e5-120">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="590e5-120">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

