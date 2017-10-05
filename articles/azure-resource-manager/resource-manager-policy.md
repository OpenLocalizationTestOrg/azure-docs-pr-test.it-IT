---
title: Criteri delle risorse di Azure | Microsoft Docs
description: "Viene descritto come utilizzare i criteri di Azure Resource Manager per l'impostazione di proprietà delle risorse coerenti durante la distribuzione. È possibile applicare i criteri alla sottoscrizione o a gruppi di risorse."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: 0ee2624f45a1de0c23cae4538a38ae3e302eedd3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="57272-104">Cenni preliminari sui criteri delle risorse</span><span class="sxs-lookup"><span data-stu-id="57272-104">Resource policy overview</span></span>
<span data-ttu-id="57272-105">I criteri delle risorse consentono di definire le convenzioni per le risorse nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="57272-105">Resource policies enable you to establish conventions for resources in your organization.</span></span> <span data-ttu-id="57272-106">Definendo le convenzioni, è possibile controllare i costi e gestire più facilmente le risorse.</span><span class="sxs-lookup"><span data-stu-id="57272-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="57272-107">È ad esempio possibile specificare che vengano consentiti solo determinati tipi di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="57272-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="57272-108">In alternativa, è possibile richiedere che tutte le risorse abbiano un tag specifico.</span><span class="sxs-lookup"><span data-stu-id="57272-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="57272-109">I criteri vengono ereditati da tutte le risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="57272-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="57272-110">Se quindi un criterio viene applicato a un gruppo di risorse, è applicabile a tutte le risorse in tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="57272-110">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span>

<span data-ttu-id="57272-111">È importante comprendere due concetti sui criteri:</span><span class="sxs-lookup"><span data-stu-id="57272-111">There are two concepts to understand about policies:</span></span>

* <span data-ttu-id="57272-112">definizione dei criteri: l'utente descrive quando i criteri vengono applicati e quale azione intraprendere</span><span class="sxs-lookup"><span data-stu-id="57272-112">policy definition - you describe when the policy is enforced and what action to take</span></span>
* <span data-ttu-id="57272-113">assegnazione di criteri: si applica la definizione di criteri a un ambito (sottoscrizione o gruppo di risorse)</span><span class="sxs-lookup"><span data-stu-id="57272-113">policy assignment - you apply the policy definition to a scope (subscription or resource group)</span></span>

<span data-ttu-id="57272-114">In questo argomento viene illustrata la definizione di criteri.</span><span class="sxs-lookup"><span data-stu-id="57272-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="57272-115">Per informazioni sull'assegnazione dei criteri, vedere [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) (Usare il portale di Azure per assegnare e gestire i criteri delle risorse) o [Assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="57272-115">For information about policy assignment, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="57272-116">I criteri vengono valutati durante la creazione e l'aggiornamento delle risorse (operazioni PUT e PATCH).</span><span class="sxs-lookup"><span data-stu-id="57272-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="57272-117">I tipi di risorsa che non supportano tag, tipologia, percorso non vengono attualmente valutati dal criterio, come ad esempio il tipo di risorsa Microsoft.Resources/deployments.</span><span class="sxs-lookup"><span data-stu-id="57272-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as the Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="57272-118">Il supporto di questo tipo di risorsa verrà aggiunto in futuro.</span><span class="sxs-lookup"><span data-stu-id="57272-118">This support will be added at a future time.</span></span> <span data-ttu-id="57272-119">Per evitare problemi di compatibilità con le versioni precedenti, è consigliabile specificare in modo esplicito il tipo durante la creazione di criteri.</span><span class="sxs-lookup"><span data-stu-id="57272-119">To avoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="57272-120">A tutti i tipi viene ad esempio applicato un criterio per i tag che non specifica i tipi,</span><span class="sxs-lookup"><span data-stu-id="57272-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="57272-121">in modo che la distribuzione del modello non venga completata in presenza di una risorsa annidata che non supporta il tag, mentre il tipo di risorsa della distribuzione sarà aggiunto alla valutazione criteri.</span><span class="sxs-lookup"><span data-stu-id="57272-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and the deployment resource type has been added to policy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="57272-122">Quali sono le differenze rispetto al controllo degli accessi in base al ruolo?</span><span class="sxs-lookup"><span data-stu-id="57272-122">How is it different from RBAC?</span></span>
<span data-ttu-id="57272-123">Esistono differenze importanti tra i criteri e il controllo degli accessi in base al ruoli (RBAC).</span><span class="sxs-lookup"><span data-stu-id="57272-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="57272-124">Il Controllo degli accessi in base al ruolo è incentrato sulle azioni dell'**utente** in ambiti diversi.</span><span class="sxs-lookup"><span data-stu-id="57272-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="57272-125">Ad esempio, un utente viene aggiunto al ruolo di collaboratore per un gruppo di risorse nell'ambito desiderato, in modo che possa apportare modifiche a tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="57272-125">For example, you are added to the contributor role for a resource group at the desired scope, so you can make changes to that resource group.</span></span> <span data-ttu-id="57272-126">I criteri si concentrano sulle proprietà delle **risorse** durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="57272-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="57272-127">Tramite i criteri, ad esempio, si possono controllare i tipi di risorse di cui è possibile effettuare il provisioning.</span><span class="sxs-lookup"><span data-stu-id="57272-127">For example, through policies, you can control the types of resources that can be provisioned.</span></span> <span data-ttu-id="57272-128">In alternativa, si possono limitare le posizioni in cui è possibile effettuare il provisioning delle risorse.</span><span class="sxs-lookup"><span data-stu-id="57272-128">Or, you can restrict the locations in which the resources can be provisioned.</span></span> <span data-ttu-id="57272-129">A differenza del controllo degli accessi in base al ruolo, i criteri rappresentano un sistema con autorizzazioni predefinite e negazione esplicita.</span><span class="sxs-lookup"><span data-stu-id="57272-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="57272-130">Per usare i criteri, l'utente deve essere autenticato tramite il controllo degli accessi in base al ruolo.</span><span class="sxs-lookup"><span data-stu-id="57272-130">To use policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="57272-131">In particolare, per l'account sono necessari:</span><span class="sxs-lookup"><span data-stu-id="57272-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="57272-132">`Microsoft.Authorization/policydefinitions/write` l'autorizzazione per definire un criterio</span><span class="sxs-lookup"><span data-stu-id="57272-132">`Microsoft.Authorization/policydefinitions/write` permission to define a policy</span></span>
* <span data-ttu-id="57272-133">`Microsoft.Authorization/policyassignments/write` l'autorizzazione per assegnare un criterio</span><span class="sxs-lookup"><span data-stu-id="57272-133">`Microsoft.Authorization/policyassignments/write` permission to assign a policy</span></span> 

<span data-ttu-id="57272-134">Queste autorizzazioni non sono incluse nel ruolo di **collaboratore**.</span><span class="sxs-lookup"><span data-stu-id="57272-134">These permissions are not included in the **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="57272-135">Criteri predefiniti</span><span class="sxs-lookup"><span data-stu-id="57272-135">Built-in policies</span></span>

<span data-ttu-id="57272-136">Azure offre alcune definizioni di criteri predefiniti che possono ridurre il numero di criteri da definire.</span><span class="sxs-lookup"><span data-stu-id="57272-136">Azure provides some built-in policy definitions that may reduce the number of policies you have to define.</span></span> <span data-ttu-id="57272-137">Prima di procedere con le definizioni dei criteri, è necessario considerare se un criterio predefinito fornisce già la definizione.</span><span class="sxs-lookup"><span data-stu-id="57272-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides the definition you need.</span></span> <span data-ttu-id="57272-138">Le definizioni di criteri predefinite sono:</span><span class="sxs-lookup"><span data-stu-id="57272-138">The built-in policy definitions are:</span></span>

* <span data-ttu-id="57272-139">Percorsi consentiti</span><span class="sxs-lookup"><span data-stu-id="57272-139">Allowed locations</span></span>
* <span data-ttu-id="57272-140">Tipi di risorse consentiti</span><span class="sxs-lookup"><span data-stu-id="57272-140">Allowed resource types</span></span>
* <span data-ttu-id="57272-141">SKU degli account di archiviazione consentiti</span><span class="sxs-lookup"><span data-stu-id="57272-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="57272-142">SKU delle macchine virtuali consentiti</span><span class="sxs-lookup"><span data-stu-id="57272-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="57272-143">Applicare il tag e il valore predefinito</span><span class="sxs-lookup"><span data-stu-id="57272-143">Apply tag and default value</span></span>
* <span data-ttu-id="57272-144">Applicare il tag e il valore</span><span class="sxs-lookup"><span data-stu-id="57272-144">Enforce tag and value</span></span>
* <span data-ttu-id="57272-145">Tipi di risorse non consentiti</span><span class="sxs-lookup"><span data-stu-id="57272-145">Not allowed resource types</span></span>
* <span data-ttu-id="57272-146">Richiedere SQL Server versione 12.0</span><span class="sxs-lookup"><span data-stu-id="57272-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="57272-147">Richiedere la crittografia dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="57272-147">Require storage account encryption</span></span>

<span data-ttu-id="57272-148">È possibile assegnare uno di questi criteri tramite il [portale](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell) o l'[interfaccia della riga di comando di Azure](resource-manager-policy-create-assign.md#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="57272-148">You can assign any of these policies through the [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="57272-149">Struttura delle definizioni di criteri</span><span class="sxs-lookup"><span data-stu-id="57272-149">Policy definition structure</span></span>
<span data-ttu-id="57272-150">Per creare una definizione di criterio è possibile usare JSON.</span><span class="sxs-lookup"><span data-stu-id="57272-150">You use JSON to create a policy definition.</span></span> <span data-ttu-id="57272-151">La definizione dei criteri contiene gli elementi per:</span><span class="sxs-lookup"><span data-stu-id="57272-151">The policy definition contains elements for:</span></span>

* <span data-ttu-id="57272-152">parameters</span><span class="sxs-lookup"><span data-stu-id="57272-152">parameters</span></span>
* <span data-ttu-id="57272-153">nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="57272-153">display name</span></span>
* <span data-ttu-id="57272-154">description</span><span class="sxs-lookup"><span data-stu-id="57272-154">description</span></span>
* <span data-ttu-id="57272-155">regola dei criteri</span><span class="sxs-lookup"><span data-stu-id="57272-155">policy rule</span></span>
  * <span data-ttu-id="57272-156">valutazione logica</span><span class="sxs-lookup"><span data-stu-id="57272-156">logical evaluation</span></span>
  * <span data-ttu-id="57272-157">effetto</span><span class="sxs-lookup"><span data-stu-id="57272-157">effect</span></span>

<span data-ttu-id="57272-158">L'esempio seguente illustra un criterio che limita i punti in cui vengono distribuite le risorse:</span><span class="sxs-lookup"><span data-stu-id="57272-158">The following example shows a policy that limits where resources are deployed:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a><span data-ttu-id="57272-159">Parametri</span><span class="sxs-lookup"><span data-stu-id="57272-159">Parameters</span></span>
<span data-ttu-id="57272-160">L'uso dei parametri consente di semplificare la gestione dei criteri, riducendone il numero di definizioni.</span><span class="sxs-lookup"><span data-stu-id="57272-160">Using parameters helps simplify your policy management by reducing the number of policy definitions.</span></span> <span data-ttu-id="57272-161">Definire un criterio per una proprietà della risorsa (ad esempio limitando i percorsi in cui le risorse possono essere distribuite) e includere i parametri nella definizione.</span><span class="sxs-lookup"><span data-stu-id="57272-161">You define a policy for a resource property (such as limiting the locations where resources can be deployed), and include parameters in the definition.</span></span> <span data-ttu-id="57272-162">Quindi, riutilizzare tale definizione dei criteri per diversi scenari passando per valori diversi (ad esempio specificando un insieme di percorsi per una sottoscrizione) quando viene assegnato il criterio.</span><span class="sxs-lookup"><span data-stu-id="57272-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning the policy.</span></span>

<span data-ttu-id="57272-163">I parametri vengono dichiarati quando si creano le definizioni dei criteri.</span><span class="sxs-lookup"><span data-stu-id="57272-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "The list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="57272-164">Il tipo di un parametro può essere stringa o matrice.</span><span class="sxs-lookup"><span data-stu-id="57272-164">The type of a parameter can be either string or array.</span></span> <span data-ttu-id="57272-165">La proprietà dei metadati viene usata per gli strumenti come il portale di Azure per visualizzare informazioni di tipo descrittivo.</span><span class="sxs-lookup"><span data-stu-id="57272-165">The metadata property is used for tools like Azure portal to display user-friendly information.</span></span> 

<span data-ttu-id="57272-166">Nella regola dei criteri, fare riferimento ai parametri con la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="57272-166">In the policy rule, you reference parameters with the following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="57272-167">Nome visualizzato e descrizione</span><span class="sxs-lookup"><span data-stu-id="57272-167">Display name and description</span></span>

<span data-ttu-id="57272-168">Usare **displayName** e **descrizione** per identificare la definizione dei criteri e fornire il contesto d'uso.</span><span class="sxs-lookup"><span data-stu-id="57272-168">You use the **displayName** and **description** to identify the policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="57272-169">Regola dei criteri</span><span class="sxs-lookup"><span data-stu-id="57272-169">Policy rule</span></span>

<span data-ttu-id="57272-170">La regola dei criteri è costituita dai blocchi **If** e **Then** blocchi.</span><span class="sxs-lookup"><span data-stu-id="57272-170">The policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="57272-171">Nel blocco **If**, si definiscono una o più condizioni che specificano quando i criteri vengono applicati.</span><span class="sxs-lookup"><span data-stu-id="57272-171">In the **If** block, you define one or more conditions that specify when the policy is enforced.</span></span> <span data-ttu-id="57272-172">È possibile applicare gli operatori logici a queste condizioni per definire con precisione lo scenario di un criterio.</span><span class="sxs-lookup"><span data-stu-id="57272-172">You can apply logical operators to these conditions to precisely define the scenario for a policy.</span></span> <span data-ttu-id="57272-173">Nel blocco **Then** si definisce l'effetto che si verifica quando le condizioni **If** sono soddisfatte.</span><span class="sxs-lookup"><span data-stu-id="57272-173">In the **Then** block, you define the effect that happens when the **If** conditions are fulfilled.</span></span>

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a><span data-ttu-id="57272-174">Operatori logici</span><span class="sxs-lookup"><span data-stu-id="57272-174">Logical operators</span></span>
<span data-ttu-id="57272-175">Gli operatori logici supportati sono:</span><span class="sxs-lookup"><span data-stu-id="57272-175">The supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="57272-176">La sintassi **not** inverte il risultato della condizione.</span><span class="sxs-lookup"><span data-stu-id="57272-176">The **not** syntax inverts the result of the condition.</span></span> <span data-ttu-id="57272-177">La sintassi **allOf** (simile all'operazione logica **And**) richiede che tutte le condizioni siano vere.</span><span class="sxs-lookup"><span data-stu-id="57272-177">The **allOf** syntax (similar to the logical **And** operation) requires all conditions to be true.</span></span> <span data-ttu-id="57272-178">La sintassi **anyOf** (simile all'operazione logica **Or**) richiede che una o più condizioni siano vere.</span><span class="sxs-lookup"><span data-stu-id="57272-178">The **anyOf** syntax (similar to the logical **Or** operation) requires one or more conditions to be true.</span></span>

<span data-ttu-id="57272-179">È possibile annidare gli operatori logici.</span><span class="sxs-lookup"><span data-stu-id="57272-179">You can nest logical operators.</span></span> <span data-ttu-id="57272-180">L'esempio seguente illustra un'operazione **not** nidificata in un'operazione **allOf**.</span><span class="sxs-lookup"><span data-stu-id="57272-180">The following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

```json
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
```

### <a name="conditions"></a><span data-ttu-id="57272-181">Condizioni</span><span class="sxs-lookup"><span data-stu-id="57272-181">Conditions</span></span>
<span data-ttu-id="57272-182">La condizione valuta se un **campo** soddisfa determinati criteri.</span><span class="sxs-lookup"><span data-stu-id="57272-182">The condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="57272-183">Le condizioni supportate sono:</span><span class="sxs-lookup"><span data-stu-id="57272-183">The supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="57272-184">Quando si usa la condizione **like**, è possibile inserire un carattere jolly (*) nel valore.</span><span class="sxs-lookup"><span data-stu-id="57272-184">When using the **like** condition, you can provide a wildcard (*) in the value.</span></span>

<span data-ttu-id="57272-185">Quando si usa la condizione **match**, specificare `#` per rappresentare una cifra, `?` per una lettera e qualsiasi altro carattere per rappresentare il carattere effettivo.</span><span class="sxs-lookup"><span data-stu-id="57272-185">When using the **match** condition, provide `#` to represent a digit, `?` for a letter, and any other character to represent that actual character.</span></span> <span data-ttu-id="57272-186">Per gli esempi, vedere [Applicare criteri delle risorse per nomi e testo](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="57272-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="57272-187">Fields</span><span class="sxs-lookup"><span data-stu-id="57272-187">Fields</span></span>
<span data-ttu-id="57272-188">Le condizioni vengono formate usando i campi.</span><span class="sxs-lookup"><span data-stu-id="57272-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="57272-189">Un campo rappresenta le proprietà nel payload delle richieste di risorse usato per descrivere lo stato della risorsa.</span><span class="sxs-lookup"><span data-stu-id="57272-189">A field represents properties in the resource request payload that is used to describe the state of the resource.</span></span>  

<span data-ttu-id="57272-190">Sono supportati i seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="57272-190">The following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="57272-191">alias delle proprietà; per un elenco, vedere [alias](#aliases).</span><span class="sxs-lookup"><span data-stu-id="57272-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="57272-192">Effetto</span><span class="sxs-lookup"><span data-stu-id="57272-192">Effect</span></span>
<span data-ttu-id="57272-193">Il criterio supporta tre tipi di effetto: `deny`, `audit` e `append`.</span><span class="sxs-lookup"><span data-stu-id="57272-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="57272-194">**Deny** genera un evento nel log di controllo e nega la richiesta</span><span class="sxs-lookup"><span data-stu-id="57272-194">**Deny** generates an event in the audit log and fails the request</span></span>
* <span data-ttu-id="57272-195">**Audit** genera un evento di avviso nel log di controllo, ma non nega la richiesta</span><span class="sxs-lookup"><span data-stu-id="57272-195">**Audit** generates a warning event in audit log but does not fail the request</span></span>
* <span data-ttu-id="57272-196">**Append** aggiunge il set di campi definiti alla richiesta</span><span class="sxs-lookup"><span data-stu-id="57272-196">**Append** adds the defined set of fields to the request</span></span> 

<span data-ttu-id="57272-197">In caso di **aggiunta**, è necessario specificare questi dettagli:</span><span class="sxs-lookup"><span data-stu-id="57272-197">For **append**, you must provide the following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of the field"
  }
]
```

<span data-ttu-id="57272-198">Il valore può essere una stringa o un oggetto formato JSON.</span><span class="sxs-lookup"><span data-stu-id="57272-198">The value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="57272-199">Alias</span><span class="sxs-lookup"><span data-stu-id="57272-199">Aliases</span></span>

<span data-ttu-id="57272-200">Usare gli alias delle proprietà per accedere alle proprietà specifiche per un tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="57272-200">You use property aliases to access specific properties for a resource type.</span></span> <span data-ttu-id="57272-201">Gli alias consentono di limitare le condizioni o i valori consentiti per una proprietà su una risorsa.</span><span class="sxs-lookup"><span data-stu-id="57272-201">Aliases enable you to restrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="57272-202">Ogni alias esegue il mapping ai percorsi in versioni di API diverse per un tipo di risorsa specificato.</span><span class="sxs-lookup"><span data-stu-id="57272-202">Each alias maps to paths in different API versions for a given resource type.</span></span> <span data-ttu-id="57272-203">Durante la valutazione dei criteri, il motore dei criteri ottiene il percorso della proprietà per la versione API specificata.</span><span class="sxs-lookup"><span data-stu-id="57272-203">During policy evaluation, the policy engine gets the property path for that API version.</span></span>

<span data-ttu-id="57272-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="57272-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="57272-205">Alias</span><span class="sxs-lookup"><span data-stu-id="57272-205">Alias</span></span> | <span data-ttu-id="57272-206">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57272-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="57272-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="57272-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="57272-208">Impostare se la porta non-ssl del server Redis (6379) è abilitata.</span><span class="sxs-lookup"><span data-stu-id="57272-208">Set whether the non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="57272-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="57272-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="57272-210">Impostare il numero di partizioni da creare in una cache di cluster Premium.</span><span class="sxs-lookup"><span data-stu-id="57272-210">Set the number of shards to be created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="57272-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="57272-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="57272-212">Impostare la dimensione della cache Redis da distribuire.</span><span class="sxs-lookup"><span data-stu-id="57272-212">Set the size of the Redis cache to deploy.</span></span>  |
| <span data-ttu-id="57272-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="57272-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="57272-214">Impostare la famiglia di SKU da usare.</span><span class="sxs-lookup"><span data-stu-id="57272-214">Set the SKU family to use.</span></span> |
| <span data-ttu-id="57272-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="57272-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="57272-216">Impostare il tipo di cache Redis da distribuire.</span><span class="sxs-lookup"><span data-stu-id="57272-216">Set the type of Redis Cache to deploy.</span></span> |

<span data-ttu-id="57272-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="57272-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="57272-218">Alias</span><span class="sxs-lookup"><span data-stu-id="57272-218">Alias</span></span> | <span data-ttu-id="57272-219">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57272-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="57272-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="57272-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="57272-221">Impostare il nome del livello di prezzo.</span><span class="sxs-lookup"><span data-stu-id="57272-221">Set the name of the pricing tier.</span></span> |

<span data-ttu-id="57272-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="57272-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="57272-223">Alias</span><span class="sxs-lookup"><span data-stu-id="57272-223">Alias</span></span> | <span data-ttu-id="57272-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57272-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="57272-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="57272-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="57272-226">Impostare l'offerta dell'immagine di piattaforma o immagine del marketplace utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-226">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="57272-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="57272-228">Impostare il server di pubblicazione dell'immagine di piattaforma o immagine del marketplace utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-228">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="57272-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="57272-230">Impostare lo SKU dell'immagine di piattaforma o immagine del marketplace utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-230">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="57272-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="57272-232">Impostare la versione dell'immagine di piattaforma o immagine del marketplace utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-232">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |


<span data-ttu-id="57272-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="57272-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="57272-234">Alias</span><span class="sxs-lookup"><span data-stu-id="57272-234">Alias</span></span> | <span data-ttu-id="57272-235">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57272-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="57272-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="57272-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="57272-237">Impostare l'identificatore dell'immagine utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-237">Set the identifier of the image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="57272-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="57272-239">Impostare l'offerta dell'immagine di piattaforma o immagine del marketplace utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-239">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="57272-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="57272-241">Impostare il server di pubblicazione dell'immagine di piattaforma o immagine del marketplace utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-241">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="57272-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="57272-243">Impostare lo SKU dell'immagine di piattaforma o immagine del marketplace utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-243">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="57272-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="57272-245">Impostare la versione dell'immagine di piattaforma o immagine del marketplace utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-245">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="57272-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="57272-247">Impostare che l'immagine o il disco è concesso in licenza in locale.</span><span class="sxs-lookup"><span data-stu-id="57272-247">Set that the image or disk is licensed on-premises.</span></span> <span data-ttu-id="57272-248">Questo valore viene usato solo per le immagini che contengono il sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="57272-248">This value is only used for images that contain the Windows Server operating system.</span></span>  |
| <span data-ttu-id="57272-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="57272-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="57272-250">Impostare l'offerta dell'immagine di piattaforma o immagine del marketplace utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-250">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="57272-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="57272-252">Impostare il server di pubblicazione dell'immagine di piattaforma o immagine del marketplace utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-252">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="57272-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="57272-254">Impostare lo SKU dell'immagine di piattaforma o immagine del marketplace utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-254">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="57272-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="57272-256">Impostare la versione dell'immagine di piattaforma o immagine del marketplace utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-256">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="57272-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="57272-258">Impostare l'URI del disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-258">Set the vhd URI.</span></span> |
| <span data-ttu-id="57272-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="57272-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="57272-260">Impostare le dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-260">Set the size of the virtual machine.</span></span> |

<span data-ttu-id="57272-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="57272-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="57272-262">Alias</span><span class="sxs-lookup"><span data-stu-id="57272-262">Alias</span></span> | <span data-ttu-id="57272-263">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57272-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="57272-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="57272-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="57272-265">Impostare il nome del server di pubblicazione dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="57272-265">Set the name of the extension’s publisher.</span></span> |
| <span data-ttu-id="57272-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="57272-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="57272-267">Impostare il tipo di estensione.</span><span class="sxs-lookup"><span data-stu-id="57272-267">Set the type of extension.</span></span> |
| <span data-ttu-id="57272-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="57272-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="57272-269">Impostare versione dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="57272-269">Set the version of the extension.</span></span> |

<span data-ttu-id="57272-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="57272-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="57272-271">Alias</span><span class="sxs-lookup"><span data-stu-id="57272-271">Alias</span></span> | <span data-ttu-id="57272-272">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57272-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="57272-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="57272-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="57272-274">Impostare l'identificatore dell'immagine utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-274">Set the identifier of the image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="57272-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="57272-276">Impostare l'offerta dell'immagine di piattaforma o immagine del marketplace utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-276">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="57272-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="57272-278">Impostare il server di pubblicazione dell'immagine di piattaforma o immagine del marketplace utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-278">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="57272-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="57272-280">Impostare lo SKU dell'immagine di piattaforma o immagine del marketplace utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-280">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="57272-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="57272-282">Impostare la versione dell'immagine di piattaforma o immagine del marketplace utilizzata per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-282">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="57272-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="57272-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="57272-284">Impostare che l'immagine o il disco è concesso in licenza in locale.</span><span class="sxs-lookup"><span data-stu-id="57272-284">Set that the image or disk is licensed on-premises.</span></span> <span data-ttu-id="57272-285">Questo valore viene usato solo per le immagini che contengono il sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="57272-285">This value is only used for images that contain the Windows Server operating system.</span></span> |
| <span data-ttu-id="57272-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="57272-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="57272-287">Impostare il prefisso del nome del computer per tutte le macchine virtuali nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="57272-287">Set the computer name prefix for all  the virtual machines in the scale set.</span></span> |
| <span data-ttu-id="57272-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="57272-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="57272-289">Impostare l'URI del BLOB per l'immagine utente.</span><span class="sxs-lookup"><span data-stu-id="57272-289">Set the blob URI for user image.</span></span> |
| <span data-ttu-id="57272-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="57272-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="57272-291">Impostare gli URL del contenitore che vengono usati per archiviare i dischi del sistema operativo per il set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="57272-291">Set the container URLs that are used to store operating system disks for the scale set.</span></span> |
| <span data-ttu-id="57272-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="57272-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="57272-293">Impostare la dimensione delle macchine virtuali in un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="57272-293">Set the size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="57272-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="57272-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="57272-295">Impostare il livello delle macchine virtuali in un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="57272-295">Set the tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="57272-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="57272-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="57272-297">Alias</span><span class="sxs-lookup"><span data-stu-id="57272-297">Alias</span></span> | <span data-ttu-id="57272-298">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57272-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="57272-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="57272-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="57272-300">Impostare la dimensione del gateway.</span><span class="sxs-lookup"><span data-stu-id="57272-300">Set the size of the gateway.</span></span> |

<span data-ttu-id="57272-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="57272-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="57272-302">Alias</span><span class="sxs-lookup"><span data-stu-id="57272-302">Alias</span></span> | <span data-ttu-id="57272-303">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57272-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="57272-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="57272-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="57272-305">Impostare il tipo di questo gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="57272-305">Set the type of this virtual network gateway.</span></span> |
| <span data-ttu-id="57272-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="57272-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="57272-307">Impostare il nome dello SKU del gateway.</span><span class="sxs-lookup"><span data-stu-id="57272-307">Set the gateway SKU name.</span></span> |

<span data-ttu-id="57272-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="57272-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="57272-309">Alias</span><span class="sxs-lookup"><span data-stu-id="57272-309">Alias</span></span> | <span data-ttu-id="57272-310">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57272-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="57272-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="57272-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="57272-312">Impostare la versione del server.</span><span class="sxs-lookup"><span data-stu-id="57272-312">Set the version of the server.</span></span> |

<span data-ttu-id="57272-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="57272-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="57272-314">Alias</span><span class="sxs-lookup"><span data-stu-id="57272-314">Alias</span></span> | <span data-ttu-id="57272-315">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57272-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="57272-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="57272-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="57272-317">Impostare l'edizione del database.</span><span class="sxs-lookup"><span data-stu-id="57272-317">Set the edition of the database.</span></span> |
| <span data-ttu-id="57272-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="57272-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="57272-319">Impostare il nome del pool elastico in cui si trova in database.</span><span class="sxs-lookup"><span data-stu-id="57272-319">Set the name of the elastic pool the database is in.</span></span> |
| <span data-ttu-id="57272-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="57272-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="57272-321">Impostare l'ID obiettivo del livello di servizio configurato del database.</span><span class="sxs-lookup"><span data-stu-id="57272-321">Set the configured service level objective ID of the database.</span></span> |
| <span data-ttu-id="57272-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="57272-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="57272-323">Impostare il nome dell'obiettivo del livello di servizio configurato del database.</span><span class="sxs-lookup"><span data-stu-id="57272-323">Set the name of the configured service level objective of the database.</span></span>  |

<span data-ttu-id="57272-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="57272-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="57272-325">Alias</span><span class="sxs-lookup"><span data-stu-id="57272-325">Alias</span></span> | <span data-ttu-id="57272-326">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57272-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="57272-327">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="57272-327">servers/elasticpools</span></span> | <span data-ttu-id="57272-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="57272-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="57272-329">Impostare il valore DTU totale condiviso per il pool elastico del database.</span><span class="sxs-lookup"><span data-stu-id="57272-329">Set the total shared DTU for the database elastic pool.</span></span> |
| <span data-ttu-id="57272-330">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="57272-330">servers/elasticpools</span></span> | <span data-ttu-id="57272-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="57272-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="57272-332">Impostare l'edizione del pool elastico.</span><span class="sxs-lookup"><span data-stu-id="57272-332">Set the edition of the elastic pool.</span></span> |

<span data-ttu-id="57272-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="57272-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="57272-334">Alias</span><span class="sxs-lookup"><span data-stu-id="57272-334">Alias</span></span> | <span data-ttu-id="57272-335">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57272-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="57272-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="57272-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="57272-337">Impostare il livello di accesso utilizzato per la fatturazione.</span><span class="sxs-lookup"><span data-stu-id="57272-337">Set the access tier used for billing.</span></span> |
| <span data-ttu-id="57272-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="57272-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="57272-339">Impostare il nome di SKU.</span><span class="sxs-lookup"><span data-stu-id="57272-339">Set the SKU name.</span></span> |
| <span data-ttu-id="57272-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="57272-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="57272-341">Specificare se il servizio crittografa i dati quando vengono archiviati nel servizio di archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="57272-341">Set whether the service encrypts the data as it is stored in the blob storage service.</span></span> |
| <span data-ttu-id="57272-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="57272-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="57272-343">Specificare se il servizio crittografa i dati quando vengono archiviati nel servizio di archiviazione file.</span><span class="sxs-lookup"><span data-stu-id="57272-343">Set whether the service encrypts the data as it is stored in the file storage service.</span></span> |
| <span data-ttu-id="57272-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="57272-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="57272-345">Impostare il nome di SKU.</span><span class="sxs-lookup"><span data-stu-id="57272-345">Set the SKU name.</span></span> |
| <span data-ttu-id="57272-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="57272-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="57272-347">Impostato per consentire solo il traffico https al servizio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="57272-347">Set to allow only https traffic to storage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="57272-348">Esempi di criteri</span><span class="sxs-lookup"><span data-stu-id="57272-348">Policy examples</span></span>

<span data-ttu-id="57272-349">I seguenti argomenti contengono esempi di criteri:</span><span class="sxs-lookup"><span data-stu-id="57272-349">The following topics contain policy examples:</span></span>

* <span data-ttu-id="57272-350">Per gli esempi di criteri di tag, vedere [Applicare criteri delle risorse per i tag](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="57272-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="57272-351">Per alcuni esempi di modelli di denominazione e di testo, vedere [Apply resource policies for names and text](resource-manager-policy-naming-convention.md) (Applicare criteri di risorse per nomi e testo).</span><span class="sxs-lookup"><span data-stu-id="57272-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="57272-352">Per gli esempi di criteri di archiviazione, vedere [Applicare i criteri delle risorse agli account di archiviazione](resource-manager-policy-storage.md).</span><span class="sxs-lookup"><span data-stu-id="57272-352">For examples of storage policies, see [Apply resource policies to storage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="57272-353">Per gli esempi di criteri di macchine virtuali, vedere [Applicare criteri delle risorse alle macchine virtuali di Linux](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) e [Applicare criteri delle risorse alle macchine virtuali di Windows](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="57272-353">For examples of virtual machine policies, see [Apply resource policies to Linux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies to Windows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="57272-354">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="57272-354">Next steps</span></span>
* <span data-ttu-id="57272-355">Dopo aver definito una regola dei criteri, assegnarla a un ambito.</span><span class="sxs-lookup"><span data-stu-id="57272-355">After defining a policy rule, assign it to a scope.</span></span> <span data-ttu-id="57272-356">Per assegnare i criteri tramite il portale, vedere [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) (Usare il portale di Azure per assegnare e gestire i criteri delle risorse).</span><span class="sxs-lookup"><span data-stu-id="57272-356">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="57272-357">Per assegnare i criteri tramite l'API REST, PowerShell o l'interfaccia della riga di comando di Azure, vedere [Assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="57272-357">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="57272-358">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="57272-358">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="57272-359">Lo schema del criterio è pubblicato in [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="57272-359">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

