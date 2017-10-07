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
# <a name="apply-resource-policies-for-names-and-text"></a>Applicare criteri delle risorse per nomi e testo
Questo argomento vengono illustrati diversi [criteri risorse](resource-manager-policy.md) è possibile applicare le convenzioni di denominazione e testo tooestablish. Questi criteri assicurano la coerenza per i nomi delle risorse e i valori dei tag. 

## <a name="set-naming-convention-with-wildcard"></a>Impostare la convenzione di denominazione con caratteri jolly
Hello riportato di seguito utilizzo hello del carattere jolly, che è supportato da hello **come** condizione. Hello condizione indica che se hello nome deve corrispondere modello citato hello (namePrefix\*nameSuffix) quindi negare hello richiesta:

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

## <a name="set-naming-convention-with-pattern"></a>Impostare la convenzione di denominazione con modelli

toospecify che i nomi delle risorse corrispondano a un criterio, utilizzare hello soddisfano una condizione. l'esempio Hello necessario toostart nomi con `contoso` e contenere sei lettere aggiuntive:

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

## <a name="set-date-pattern-for-tag-value"></a>Impostare il modello di data per il valore di tag

un modello di data di utilizzo di due cifre, trattino, tre lettere, trattino e quattro cifre, toorequire:

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

## <a name="next-steps"></a>Passaggi successivi
* Dopo aver definito una regola dei criteri (come illustrato in hello precedenti esempi), è necessario toocreate definizione dei criteri hello e assegnarlo tooa ambito. Hello ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa. criteri tooassign tramite il portale di hello, vedere [tooassign portale utilizzare Azure e gestire i criteri di risorse](resource-manager-policy-portal.md). criteri di tooassign tramite l'API REST, PowerShell o l'interfaccia CLI di Azure, vedere [assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md). 
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).

