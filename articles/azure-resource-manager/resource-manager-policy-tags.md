---
title: criteri per i tag delle risorse aaaAzure | Documenti Microsoft
description: Fornisce esempi di criteri delle risorse per la gestione dei tag delle risorse
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
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a>Applicare criteri delle risorse per i tag

In questo argomento sono disponibili regole di criteri comuni che è possibile applicare tooensure l'utilizzo coerente di tag alle risorse.

L'applicazione di una sottoscrizione con le risorse esistenti o un gruppo di risorse tooa criteri tag non è applicabile modo retroattivo risorse toothose di hello criteri. criteri di hello tooenforce su tali risorse, attivare un toohello aggiornamento risorse esistenti. Questo articolo include un esempio di PowerShell per l'attivazione di un aggiornamento.

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a>Assicurarsi che tutte le risorse di un gruppo di risorse abbiano un tag/valore

Un requisito comune è che tutte le risorse di un gruppo di risorse abbiano un determinato tag e valore. Questo requisito è spesso necessario tootrack costi dal reparto. è necessario soddisfare Hello seguenti condizioni:

* Hello richiesto tag e il valore vengono aggiunti toonew e risorse che non contengono tag hello aggiornate.
* Hello necessario tag e valore non può essere rimosso da tutte le risorse esistenti.

Questo requisito è stato possibile mediante l'applicazione di gruppo di risorse di due criteri predefiniti tooa.

| ID | Descrizione |
| ---- | ---- |
| 2a0e14a6-b0a6-4fab-991a-187a4f81c498 | Si applica un tag obbligatorio e il relativo valore predefinito quando non viene specificato dall'utente hello. |
| 1e30110a-5ceb-460c-a204-c1c3969c6d62 | Applica un tag obbligatorio e il relativo valore. |

### <a name="powershell"></a>PowerShell

lo script di PowerShell seguente Hello assegna gruppo di risorse tooa definizioni hello due criteri predefiniti. Prima di eseguire script hello, assegnare il gruppo di risorse di tutti i tag richiesti toohello. È richiesto per le risorse nel gruppo hello hello ogni tag per il gruppo di risorse hello. gruppi di risorse tooall tooassign nella sottoscrizione, non forniscono hello `-Name` parametro durante il recupero di gruppi di risorse hello.

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

Dopo l'assegnazione di criteri di hello, è possibile attivare un tooall di aggiornamento esistente risorse tooenforce hello tag i criteri che sono stati aggiunti. Hello lo script seguente consente di mantenere qualsiasi altro tag già presente nel risorse hello:

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a>Richiedere tag per un tipo di rosorsa
Hello di esempio seguente viene illustrato come gli operatori logici di toonest toorequire un'applicazione tag per un solo tipo di risorsa specificata (in questo caso, gli account di archiviazione).

```json
{
    "if": {
        "allOf": [
          {
            "not": {
              "field": "tags",
              "containsKey": "application"
            }
          },
          {
            "field": "type",
            "equals": "Microsoft.Storage/storageAccounts"
          }
        ]
    },
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a>Tag richiesto
Hello seguente criterio Nega le richieste che non dispongono di un tag che contiene "costCenter" chiave (qualsiasi valore può essere applicato):

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a>Passaggi successivi
* Dopo aver definito una regola dei criteri (come illustrato in hello precedenti esempi), è necessario toocreate definizione dei criteri hello e assegnarlo tooa ambito. Hello ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa. criteri tooassign tramite il portale di hello, vedere [tooassign portale utilizzare Azure e gestire i criteri di risorse](resource-manager-policy-portal.md). criteri di tooassign tramite l'API REST, PowerShell o l'interfaccia CLI di Azure, vedere [assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md).
* Per i criteri di tooresource un'introduzione, vedere [Panoramica criteri delle risorse](resource-manager-policy.md).
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).

