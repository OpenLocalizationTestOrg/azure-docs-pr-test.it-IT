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
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a><span data-ttu-id="c3da6-103">Errore RequestDisallowedByPolicy con i criteri delle risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="c3da6-103">RequestDisallowedByPolicy error with Azure resource policy</span></span>

<span data-ttu-id="c3da6-104">Questo articolo descrive la causa di hello di hello RequestDisallowedByPolicy errore, nonché soluzioni per l'errore.</span><span class="sxs-lookup"><span data-stu-id="c3da6-104">This article describes hello cause of hello RequestDisallowedByPolicy error, it also provides solution for this error.</span></span>

## <a name="symptom"></a><span data-ttu-id="c3da6-105">Sintomo</span><span class="sxs-lookup"><span data-stu-id="c3da6-105">Symptom</span></span>

<span data-ttu-id="c3da6-106">Quando si tenta di toodo un'azione durante la distribuzione, è possibile ricevere un **RequestDisallowedByPolicy** errore che impedisce l'azione di hello essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="c3da6-106">When you try toodo an action during deployment, you might receive a **RequestDisallowedByPolicy** error that prevents hello action be performed.</span></span> <span data-ttu-id="c3da6-107">di seguito Hello è un esempio di errore hello:</span><span class="sxs-lookup"><span data-stu-id="c3da6-107">hello following is a sample of hello error:</span></span>

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a><span data-ttu-id="c3da6-108">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="c3da6-108">Troubleshooting</span></span>

<span data-ttu-id="c3da6-109">tooretrieve dettagli sui criteri hello bloccati la distribuzione, hello utilizzare uno dei metodi di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3da6-109">tooretrieve details about hello policy that blocked your deployment, use hello following one of hello methods:</span></span>

### <a name="method-1"></a><span data-ttu-id="c3da6-110">Metodo 1</span><span class="sxs-lookup"><span data-stu-id="c3da6-110">Method 1</span></span>

<span data-ttu-id="c3da6-111">In PowerShell, fornire tale identificatore dei criteri come hello **Id** dettagli sui criteri hello bloccati distribuzione tooretrieve del parametro.</span><span class="sxs-lookup"><span data-stu-id="c3da6-111">In PowerShell, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a><span data-ttu-id="c3da6-112">Metodo 2</span><span class="sxs-lookup"><span data-stu-id="c3da6-112">Method 2</span></span> 

<span data-ttu-id="c3da6-113">In Azure CLI 2.0, specificare il nome di hello della definizione di criteri hello:</span><span class="sxs-lookup"><span data-stu-id="c3da6-113">In Azure CLI 2.0, provide hello name of hello policy definition:</span></span> 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a><span data-ttu-id="c3da6-114">Soluzione</span><span class="sxs-lookup"><span data-stu-id="c3da6-114">Solution</span></span>

<span data-ttu-id="c3da6-115">Per assicurare la sicurezza o la conformità, il reparto IT può applicare un criterio di risorsa che impedisce la creazione di indirizzi IP pubblici, gruppi di sicurezza di rete, route definite dall'utente o tabelle di routing.</span><span class="sxs-lookup"><span data-stu-id="c3da6-115">For security or compliance, your IT department might enforce a resource policy that prohibits creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span></span> <span data-ttu-id="c3da6-116">Nell'esempio hello hello messaggio di errore descritto nella sezione "Sintomo" hello, denominato criteri hello **regionPolicyDefinition**, ma potrebbe essere diversa.</span><span class="sxs-lookup"><span data-stu-id="c3da6-116">In hello sample of hello error message that is described in hello "Symptoms" section, hello policy is named **regionPolicyDefinition**, but it could be different.</span></span>
<span data-ttu-id="c3da6-117">tooresolve questo problema, collaborare con i criteri delle risorse hello tooreview reparto IT e determinare come hello tooperform richiesta azione in conformità con i criteri.</span><span class="sxs-lookup"><span data-stu-id="c3da6-117">tooresolve this problem, work with your IT department tooreview hello resource policies, and determine how tooperform hello requested action in compliance with those policies.</span></span>


<span data-ttu-id="c3da6-118">Per ulteriori informazioni, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="c3da6-118">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="c3da6-119">Cenni preliminari sui criteri delle risorse</span><span class="sxs-lookup"><span data-stu-id="c3da6-119">Resource policy overview</span></span>](resource-manager-policy.md)
- [<span data-ttu-id="c3da6-120">Errori di distribuzione comuni -RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="c3da6-120">Common deployment errors-RequestDisallowedByPolicy</span></span>](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


