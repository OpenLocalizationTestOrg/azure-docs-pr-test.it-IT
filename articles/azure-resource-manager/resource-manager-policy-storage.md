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
# <a name="apply-resource-policies-toostorage-accounts"></a>Applicare gli account toostorage criteri delle risorse
Questo argomento vengono illustrati diversi [criteri risorse](resource-manager-policy.md) è possibile applicare gli account di archiviazione tooAzure. Questi criteri assicurano la coerenza per gli account di archiviazione hello distribuita nella propria organizzazione. 

## <a name="define-permitted-storage-account-types"></a>Definire i tipi di account di archiviazione consentiti

Hello seguente criterio limita le [tipi di account di archiviazione](../storage/common/storage-redundancy.md) può essere distribuito:

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

Una regola dei criteri simile con un parametro per accettare gli SKU consentito hello è disponibile come una definizione dei criteri predefiniti. criteri predefiniti Hello con ID risorsa hello `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`. 

## <a name="define-permitted-access-tier"></a>Definire il livello di accesso consentito

i criteri seguenti Hello specificano il tipo di hello di [livello di accesso](../storage/blobs/storage-blob-storage-tiers.md) che può essere specificata per gli account di archiviazione:

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

## <a name="ensure-encryption-is-enabled"></a>Verificare che la crittografia sia abilitata

i criteri seguenti Hello richiedono tutti tooenable gli account di archiviazione [la crittografia del servizio di archiviazione](../storage/common/storage-service-encryption.md):

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

Questa regola dei criteri è disponibile anche come una definizione dei criteri predefinite con l'ID della risorsa hello `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.

## <a name="next-steps"></a>Passaggi successivi
* Dopo aver definito una regola dei criteri (come illustrato in hello precedenti esempi), è necessario toocreate definizione dei criteri hello e assegnarlo tooa ambito. Hello ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa. criteri tooassign tramite il portale di hello, vedere [tooassign portale utilizzare Azure e gestire i criteri di risorse](resource-manager-policy-portal.md). criteri di tooassign tramite l'API REST, PowerShell o l'interfaccia CLI di Azure, vedere [assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md). 
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).

