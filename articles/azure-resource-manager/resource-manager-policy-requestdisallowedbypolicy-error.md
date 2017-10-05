---
title: Errore RequestDisallowedByPolicy con i criteri delle risorse di Azure | Microsoft Docs
description: Descrive la causa dell'errore RequestDisallowedByPolicy.
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
ms.openlocfilehash: 182a27e444c2f5db66d518a1a0c608d3e319d553
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a><span data-ttu-id="b6dd9-103">Errore RequestDisallowedByPolicy con i criteri delle risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="b6dd9-103">RequestDisallowedByPolicy error with Azure resource policy</span></span>

<span data-ttu-id="b6dd9-104">Questo articolo descrive la causa dell'errore RequestDisallowedByPolicy e indica la relativa soluzione.</span><span class="sxs-lookup"><span data-stu-id="b6dd9-104">This article describes the cause of the RequestDisallowedByPolicy error, it also provides solution for this error.</span></span>

## <a name="symptom"></a><span data-ttu-id="b6dd9-105">Sintomo</span><span class="sxs-lookup"><span data-stu-id="b6dd9-105">Symptom</span></span>

<span data-ttu-id="b6dd9-106">Quando si tenta di eseguire un'azione durante la distribuzione, è possibile che venga visualizzato un errore **RequestDisallowedByPolicy** che impedisce l'esecuzione dell'azione.</span><span class="sxs-lookup"><span data-stu-id="b6dd9-106">When you try to do an action during deployment, you might receive a **RequestDisallowedByPolicy** error that prevents the action be performed.</span></span> <span data-ttu-id="b6dd9-107">Di seguito è riportato un esempio dell'errore:</span><span class="sxs-lookup"><span data-stu-id="b6dd9-107">The following is a sample of the error:</span></span>

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a><span data-ttu-id="b6dd9-108">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="b6dd9-108">Troubleshooting</span></span>

<span data-ttu-id="b6dd9-109">Per recuperare i dettagli sui criteri bloccati nella distribuzione, usare uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b6dd9-109">To retrieve details about the policy that blocked your deployment, use the following one of the methods:</span></span>

### <a name="method-1"></a><span data-ttu-id="b6dd9-110">Metodo 1</span><span class="sxs-lookup"><span data-stu-id="b6dd9-110">Method 1</span></span>

<span data-ttu-id="b6dd9-111">In PowerShell specificare l'identificatore di criteri come parametro **Id** per recuperare i dettagli relativi al criterio che ha bloccato la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b6dd9-111">In PowerShell, provide that policy identifier as the **Id** parameter to retrieve details about the policy that blocked your deployment.</span></span>

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a><span data-ttu-id="b6dd9-112">Metodo 2</span><span class="sxs-lookup"><span data-stu-id="b6dd9-112">Method 2</span></span> 

<span data-ttu-id="b6dd9-113">Nell'interfaccia della riga di comando di Azure 2.0 specificare il nome della definizione del criterio:</span><span class="sxs-lookup"><span data-stu-id="b6dd9-113">In Azure CLI 2.0, provide the name of the policy definition:</span></span> 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a><span data-ttu-id="b6dd9-114">Soluzione</span><span class="sxs-lookup"><span data-stu-id="b6dd9-114">Solution</span></span>

<span data-ttu-id="b6dd9-115">Per assicurare la sicurezza o la conformità, il reparto IT può applicare un criterio di risorsa che impedisce la creazione di indirizzi IP pubblici, gruppi di sicurezza di rete, route definite dall'utente o tabelle di routing.</span><span class="sxs-lookup"><span data-stu-id="b6dd9-115">For security or compliance, your IT department might enforce a resource policy that prohibits creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span></span> <span data-ttu-id="b6dd9-116">Nell'esempio di messaggio di errore descritto nella sezione "Sintomi", il criterio è denominato **regionPolicyDefinition**, ma potrebbe essere diverso.</span><span class="sxs-lookup"><span data-stu-id="b6dd9-116">In the sample of the error message that is described in the "Symptoms" section, the policy is named **regionPolicyDefinition**, but it could be different.</span></span>
<span data-ttu-id="b6dd9-117">Per risolvere questo problema, collaborare con il reparto IT per controllare i criteri delle risorse e determinare come eseguire l'azione richiesta in conformità con questi criteri.</span><span class="sxs-lookup"><span data-stu-id="b6dd9-117">To resolve this problem, work with your IT department to review the resource policies, and determine how to perform the requested action in compliance with those policies.</span></span>


<span data-ttu-id="b6dd9-118">Per altre informazioni, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="b6dd9-118">For more information, see the following articles:</span></span>

- [<span data-ttu-id="b6dd9-119">Cenni preliminari sui criteri delle risorse</span><span class="sxs-lookup"><span data-stu-id="b6dd9-119">Resource policy overview</span></span>](resource-manager-policy.md)
- [<span data-ttu-id="b6dd9-120">Errori di distribuzione comuni -RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="b6dd9-120">Common deployment errors-RequestDisallowedByPolicy</span></span>](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


