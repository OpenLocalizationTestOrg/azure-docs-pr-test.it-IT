---
title: Errore aaaRequestDisallowedByPolicy criteri delle risorse di Azure | Documenti Microsoft
description: Descrive la causa hello di hello RequestDisallowedByPolicy errore.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 7870e40205cf433ccb4ba02376b5fe809f20d0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a>Errore RequestDisallowedByPolicy con i criteri delle risorse di Azure

Questo articolo descrive la causa di hello di hello RequestDisallowedByPolicy errore, nonché soluzioni per l'errore.

## <a name="symptom"></a>Sintomo

Quando si tenta di toodo un'azione durante la distribuzione, è possibile ricevere un **RequestDisallowedByPolicy** errore che impedisce l'azione di hello essere eseguita. di seguito Hello è un esempio di errore hello:

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a>Risoluzione dei problemi

tooretrieve dettagli sui criteri hello bloccati la distribuzione, hello utilizzare uno dei metodi di hello seguenti:

### <a name="method-1"></a>Metodo 1

In PowerShell, fornire tale identificatore dei criteri come hello **Id** dettagli sui criteri hello bloccati distribuzione tooretrieve del parametro.

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a>Metodo 2 

In Azure CLI 2.0, specificare il nome di hello della definizione di criteri hello: 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a>Soluzione

Per assicurare la sicurezza o la conformità, il reparto IT può applicare un criterio di risorsa che impedisce la creazione di indirizzi IP pubblici, gruppi di sicurezza di rete, route definite dall'utente o tabelle di routing. Nell'esempio hello hello messaggio di errore descritto nella sezione "Sintomo" hello, denominato criteri hello **regionPolicyDefinition**, ma potrebbe essere diversa.
tooresolve questo problema, collaborare con i criteri delle risorse hello tooreview reparto IT e determinare come hello tooperform richiesta azione in conformità con i criteri.


Per ulteriori informazioni, vedere hello seguenti articoli:

- [Cenni preliminari sui criteri delle risorse](resource-manager-policy.md)
- [Errori di distribuzione comuni -RequestDisallowedByPolicy](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


