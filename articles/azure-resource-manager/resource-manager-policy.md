---
title: criteri delle risorse aaaAzure | Documenti Microsoft
description: Viene descritto come toouse Azure Resource Manager criteri tooensure risorse coerente vengono impostate durante la distribuzione. I criteri possono essere applicati a hello sottoscrizione o gruppi di risorse.
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
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="a4b53-104">Cenni preliminari sui criteri delle risorse</span><span class="sxs-lookup"><span data-stu-id="a4b53-104">Resource policy overview</span></span>
<span data-ttu-id="a4b53-105">Criteri di risorse consentono di convenzioni tooestablish per le risorse dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="a4b53-105">Resource policies enable you tooestablish conventions for resources in your organization.</span></span> <span data-ttu-id="a4b53-106">Definendo le convenzioni, è possibile controllare i costi e gestire più facilmente le risorse.</span><span class="sxs-lookup"><span data-stu-id="a4b53-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="a4b53-107">È ad esempio possibile specificare che vengano consentiti solo determinati tipi di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="a4b53-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="a4b53-108">In alternativa, è possibile richiedere che tutte le risorse abbiano un tag specifico.</span><span class="sxs-lookup"><span data-stu-id="a4b53-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="a4b53-109">I criteri vengono ereditati da tutte le risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="a4b53-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="a4b53-110">Se il criterio viene applicato tooa gruppo di risorse, è pertanto applicabile tooall risorse di hello in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a4b53-110">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span>

<span data-ttu-id="a4b53-111">Esistono due concetti toounderstand sui criteri:</span><span class="sxs-lookup"><span data-stu-id="a4b53-111">There are two concepts toounderstand about policies:</span></span>

* <span data-ttu-id="a4b53-112">definizione dei criteri - descrivono criteri quando hello e quali tootake azione</span><span class="sxs-lookup"><span data-stu-id="a4b53-112">policy definition - you describe when hello policy is enforced and what action tootake</span></span>
* <span data-ttu-id="a4b53-113">assegnazione di criteri - si applica hello definizione tooa ambito dei criteri (sottoscrizione o gruppo di risorse)</span><span class="sxs-lookup"><span data-stu-id="a4b53-113">policy assignment - you apply hello policy definition tooa scope (subscription or resource group)</span></span>

<span data-ttu-id="a4b53-114">In questo argomento viene illustrata la definizione di criteri.</span><span class="sxs-lookup"><span data-stu-id="a4b53-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="a4b53-115">Per informazioni sull'assegnazione di criteri, vedere [tooassign portale utilizzare Azure e gestire i criteri di risorse](resource-manager-policy-portal.md) o [assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="a4b53-115">For information about policy assignment, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="a4b53-116">I criteri vengono valutati durante la creazione e l'aggiornamento delle risorse (operazioni PUT e PATCH).</span><span class="sxs-lookup"><span data-stu-id="a4b53-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="a4b53-117">Attualmente, criteri non restituiscono i tipi di risorsa che non supportano i tag, tipo e posizione, ad esempio il tipo di risorsa Microsoft.Resources/deployments hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as hello Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="a4b53-118">Il supporto di questo tipo di risorsa verrà aggiunto in futuro.</span><span class="sxs-lookup"><span data-stu-id="a4b53-118">This support will be added at a future time.</span></span> <span data-ttu-id="a4b53-119">problemi di compatibilità con le versioni precedenti di tooavoid, sarà necessario specificare tipo in modo esplicito durante la creazione di criteri.</span><span class="sxs-lookup"><span data-stu-id="a4b53-119">tooavoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="a4b53-120">A tutti i tipi viene ad esempio applicato un criterio per i tag che non specifica i tipi,</span><span class="sxs-lookup"><span data-stu-id="a4b53-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="a4b53-121">In tal caso, una distribuzione modello potrebbe non riuscire se è presente una risorsa annidata che non supporta i tag e tipo di risorsa distribuzione hello è stato aggiunto toopolicy valutazione.</span><span class="sxs-lookup"><span data-stu-id="a4b53-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and hello deployment resource type has been added toopolicy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="a4b53-122">Quali sono le differenze rispetto al controllo degli accessi in base al ruolo?</span><span class="sxs-lookup"><span data-stu-id="a4b53-122">How is it different from RBAC?</span></span>
<span data-ttu-id="a4b53-123">Esistono differenze importanti tra i criteri e il controllo degli accessi in base al ruoli (RBAC).</span><span class="sxs-lookup"><span data-stu-id="a4b53-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="a4b53-124">Il Controllo degli accessi in base al ruolo è incentrato sulle azioni dell'**utente** in ambiti diversi.</span><span class="sxs-lookup"><span data-stu-id="a4b53-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="a4b53-125">Ad esempio, vengono aggiunti il ruolo di collaboratore toohello per un gruppo di risorse nell'ambito di hello desiderato, pertanto è possibile apportare le modifiche toothat gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a4b53-125">For example, you are added toohello contributor role for a resource group at hello desired scope, so you can make changes toothat resource group.</span></span> <span data-ttu-id="a4b53-126">I criteri si concentrano sulle proprietà delle **risorse** durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a4b53-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="a4b53-127">Ad esempio, tramite i criteri, è possibile controllare i tipi di hello delle risorse che è possono effettuare il provisioning.</span><span class="sxs-lookup"><span data-stu-id="a4b53-127">For example, through policies, you can control hello types of resources that can be provisioned.</span></span> <span data-ttu-id="a4b53-128">In alternativa, è possibile limitare i percorsi di hello in cui è possono effettuare il provisioning di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-128">Or, you can restrict hello locations in which hello resources can be provisioned.</span></span> <span data-ttu-id="a4b53-129">A differenza del controllo degli accessi in base al ruolo, i criteri rappresentano un sistema con autorizzazioni predefinite e negazione esplicita.</span><span class="sxs-lookup"><span data-stu-id="a4b53-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="a4b53-130">toouse criteri, è necessario che l'autenticazione tramite RBAC.</span><span class="sxs-lookup"><span data-stu-id="a4b53-130">toouse policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="a4b53-131">In particolare, per l'account sono necessari:</span><span class="sxs-lookup"><span data-stu-id="a4b53-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="a4b53-132">`Microsoft.Authorization/policydefinitions/write`autorizzazione toodefine un criterio</span><span class="sxs-lookup"><span data-stu-id="a4b53-132">`Microsoft.Authorization/policydefinitions/write` permission toodefine a policy</span></span>
* <span data-ttu-id="a4b53-133">`Microsoft.Authorization/policyassignments/write`autorizzazione tooassign un criterio</span><span class="sxs-lookup"><span data-stu-id="a4b53-133">`Microsoft.Authorization/policyassignments/write` permission tooassign a policy</span></span> 

<span data-ttu-id="a4b53-134">Queste autorizzazioni non sono incluse in hello **collaboratore** ruolo.</span><span class="sxs-lookup"><span data-stu-id="a4b53-134">These permissions are not included in hello **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="a4b53-135">Criteri predefiniti</span><span class="sxs-lookup"><span data-stu-id="a4b53-135">Built-in policies</span></span>

<span data-ttu-id="a4b53-136">Azure offre alcune definizioni di criteri predefiniti che possono ridurre il numero di hello dei criteri è toodefine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-136">Azure provides some built-in policy definitions that may reduce hello number of policies you have toodefine.</span></span> <span data-ttu-id="a4b53-137">Prima di procedere con le definizioni dei criteri, è necessario considerare se un criterio incorporato fornisce già definizione hello che è necessario.</span><span class="sxs-lookup"><span data-stu-id="a4b53-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides hello definition you need.</span></span> <span data-ttu-id="a4b53-138">le definizioni dei criteri predefiniti di Hello sono:</span><span class="sxs-lookup"><span data-stu-id="a4b53-138">hello built-in policy definitions are:</span></span>

* <span data-ttu-id="a4b53-139">Percorsi consentiti</span><span class="sxs-lookup"><span data-stu-id="a4b53-139">Allowed locations</span></span>
* <span data-ttu-id="a4b53-140">Tipi di risorse consentiti</span><span class="sxs-lookup"><span data-stu-id="a4b53-140">Allowed resource types</span></span>
* <span data-ttu-id="a4b53-141">SKU degli account di archiviazione consentiti</span><span class="sxs-lookup"><span data-stu-id="a4b53-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="a4b53-142">SKU delle macchine virtuali consentiti</span><span class="sxs-lookup"><span data-stu-id="a4b53-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="a4b53-143">Applicare il tag e il valore predefinito</span><span class="sxs-lookup"><span data-stu-id="a4b53-143">Apply tag and default value</span></span>
* <span data-ttu-id="a4b53-144">Applicare il tag e il valore</span><span class="sxs-lookup"><span data-stu-id="a4b53-144">Enforce tag and value</span></span>
* <span data-ttu-id="a4b53-145">Tipi di risorse non consentiti</span><span class="sxs-lookup"><span data-stu-id="a4b53-145">Not allowed resource types</span></span>
* <span data-ttu-id="a4b53-146">Richiedere SQL Server versione 12.0</span><span class="sxs-lookup"><span data-stu-id="a4b53-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="a4b53-147">Richiedere la crittografia dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="a4b53-147">Require storage account encryption</span></span>

<span data-ttu-id="a4b53-148">È possibile assegnare uno di questi criteri tramite hello [portale](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), o [CLI di Azure](resource-manager-policy-create-assign.md#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a4b53-148">You can assign any of these policies through hello [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="a4b53-149">Struttura delle definizioni di criteri</span><span class="sxs-lookup"><span data-stu-id="a4b53-149">Policy definition structure</span></span>
<span data-ttu-id="a4b53-150">Utilizzare JSON toocreate una definizione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="a4b53-150">You use JSON toocreate a policy definition.</span></span> <span data-ttu-id="a4b53-151">definizione dei criteri Hello contiene elementi per:</span><span class="sxs-lookup"><span data-stu-id="a4b53-151">hello policy definition contains elements for:</span></span>

* <span data-ttu-id="a4b53-152">parameters</span><span class="sxs-lookup"><span data-stu-id="a4b53-152">parameters</span></span>
* <span data-ttu-id="a4b53-153">nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="a4b53-153">display name</span></span>
* <span data-ttu-id="a4b53-154">description</span><span class="sxs-lookup"><span data-stu-id="a4b53-154">description</span></span>
* <span data-ttu-id="a4b53-155">regola dei criteri</span><span class="sxs-lookup"><span data-stu-id="a4b53-155">policy rule</span></span>
  * <span data-ttu-id="a4b53-156">valutazione logica</span><span class="sxs-lookup"><span data-stu-id="a4b53-156">logical evaluation</span></span>
  * <span data-ttu-id="a4b53-157">effetto</span><span class="sxs-lookup"><span data-stu-id="a4b53-157">effect</span></span>

<span data-ttu-id="a4b53-158">Hello di esempio seguente viene illustrato un criterio che limiti in cui vengono distribuite le risorse:</span><span class="sxs-lookup"><span data-stu-id="a4b53-158">hello following example shows a policy that limits where resources are deployed:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
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

## <a name="parameters"></a><span data-ttu-id="a4b53-159">parameters</span><span class="sxs-lookup"><span data-stu-id="a4b53-159">Parameters</span></span>
<span data-ttu-id="a4b53-160">Utilizzo di parametri consente di semplificare la gestione dei criteri, riducendo il numero di hello di definizioni dei criteri.</span><span class="sxs-lookup"><span data-stu-id="a4b53-160">Using parameters helps simplify your policy management by reducing hello number of policy definitions.</span></span> <span data-ttu-id="a4b53-161">Si definisce un criterio per una proprietà della risorsa (ad esempio limitando i percorsi di hello in cui le risorse possono essere distribuite) e includono i parametri nella definizione di hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-161">You define a policy for a resource property (such as limiting hello locations where resources can be deployed), and include parameters in hello definition.</span></span> <span data-ttu-id="a4b53-162">Quindi, riutilizzare tale definizione dei criteri per i diversi scenari passando valori diversi (ad esempio specificando un insieme di località per una sottoscrizione) quando l'assegnazione di criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning hello policy.</span></span>

<span data-ttu-id="a4b53-163">I parametri vengono dichiarati quando si creano le definizioni dei criteri.</span><span class="sxs-lookup"><span data-stu-id="a4b53-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="a4b53-164">tipo di Hello di un parametro può essere stringa o matrice.</span><span class="sxs-lookup"><span data-stu-id="a4b53-164">hello type of a parameter can be either string or array.</span></span> <span data-ttu-id="a4b53-165">proprietà dei metadati Hello viene utilizzato per strumenti come informazioni descrittive toodisplay portale Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b53-165">hello metadata property is used for tools like Azure portal toodisplay user-friendly information.</span></span> 

<span data-ttu-id="a4b53-166">Nella regola dei criteri di hello, fare riferimento ai parametri con hello la seguente sintassi:</span><span class="sxs-lookup"><span data-stu-id="a4b53-166">In hello policy rule, you reference parameters with hello following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="a4b53-167">Nome visualizzato e descrizione</span><span class="sxs-lookup"><span data-stu-id="a4b53-167">Display name and description</span></span>

<span data-ttu-id="a4b53-168">Utilizzare hello **displayName** e **descrizione** tooidentify hello definizione dei criteri e forniscono un contesto per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="a4b53-168">You use hello **displayName** and **description** tooidentify hello policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="a4b53-169">Regola dei criteri</span><span class="sxs-lookup"><span data-stu-id="a4b53-169">Policy rule</span></span>

<span data-ttu-id="a4b53-170">regola dei criteri di Hello costituita **se** e **quindi** blocchi.</span><span class="sxs-lookup"><span data-stu-id="a4b53-170">hello policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="a4b53-171">In hello **se** blocco, si definiscono una o più condizioni che specificano i criteri quando hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-171">In hello **If** block, you define one or more conditions that specify when hello policy is enforced.</span></span> <span data-ttu-id="a4b53-172">È possibile applicare le condizioni di operatori logici toothese tooprecisely definire scenario hello per un criterio.</span><span class="sxs-lookup"><span data-stu-id="a4b53-172">You can apply logical operators toothese conditions tooprecisely define hello scenario for a policy.</span></span> <span data-ttu-id="a4b53-173">In hello **quindi** blocco, è definire l'effetto di hello quando hello **se** condizioni sono soddisfatte.</span><span class="sxs-lookup"><span data-stu-id="a4b53-173">In hello **Then** block, you define hello effect that happens when hello **If** conditions are fulfilled.</span></span>

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

### <a name="logical-operators"></a><span data-ttu-id="a4b53-174">Operatori logici</span><span class="sxs-lookup"><span data-stu-id="a4b53-174">Logical operators</span></span>
<span data-ttu-id="a4b53-175">operatori logici Hello supportato sono:</span><span class="sxs-lookup"><span data-stu-id="a4b53-175">hello supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="a4b53-176">Hello **non** sintassi inverte il risultato di hello della condizione di hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-176">hello **not** syntax inverts hello result of hello condition.</span></span> <span data-ttu-id="a4b53-177">Hello **tutto** sintassi (simile toohello logico **e** operazione) richiede tutte true toobe di condizioni.</span><span class="sxs-lookup"><span data-stu-id="a4b53-177">hello **allOf** syntax (similar toohello logical **And** operation) requires all conditions toobe true.</span></span> <span data-ttu-id="a4b53-178">Hello **anyOf** sintassi (simile toohello logico **o** operazione) richiede uno o più true toobe condizioni.</span><span class="sxs-lookup"><span data-stu-id="a4b53-178">hello **anyOf** syntax (similar toohello logical **Or** operation) requires one or more conditions toobe true.</span></span>

<span data-ttu-id="a4b53-179">È possibile annidare gli operatori logici.</span><span class="sxs-lookup"><span data-stu-id="a4b53-179">You can nest logical operators.</span></span> <span data-ttu-id="a4b53-180">Hello seguente esempio viene illustrato un **non** operazione nidificato all'interno di un **tutto** operazione.</span><span class="sxs-lookup"><span data-stu-id="a4b53-180">hello following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

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

### <a name="conditions"></a><span data-ttu-id="a4b53-181">Condizioni</span><span class="sxs-lookup"><span data-stu-id="a4b53-181">Conditions</span></span>
<span data-ttu-id="a4b53-182">condizione Hello valuta se un **campo** soddisfa determinati criteri.</span><span class="sxs-lookup"><span data-stu-id="a4b53-182">hello condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="a4b53-183">le condizioni di Hello supportato sono:</span><span class="sxs-lookup"><span data-stu-id="a4b53-183">hello supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="a4b53-184">Quando si utilizza hello **come** condizione, è possibile specificare un carattere jolly (*) nel valore hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-184">When using hello **like** condition, you can provide a wildcard (*) in hello value.</span></span>

<span data-ttu-id="a4b53-185">Quando si utilizza hello **corrispondono** condizione, fornire `#` toorepresent una cifra, `?` per una lettera e qualsiasi altro carattere toorepresent tale carattere effettivo.</span><span class="sxs-lookup"><span data-stu-id="a4b53-185">When using hello **match** condition, provide `#` toorepresent a digit, `?` for a letter, and any other character toorepresent that actual character.</span></span> <span data-ttu-id="a4b53-186">Per gli esempi, vedere [Applicare criteri delle risorse per nomi e testo](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="a4b53-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="a4b53-187">Fields</span><span class="sxs-lookup"><span data-stu-id="a4b53-187">Fields</span></span>
<span data-ttu-id="a4b53-188">Le condizioni vengono formate usando i campi.</span><span class="sxs-lookup"><span data-stu-id="a4b53-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="a4b53-189">Un campo rappresenta le proprietà nel payload di richiesta di risorsa hello ovvero toodescribe utilizzati hello stato della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-189">A field represents properties in hello resource request payload that is used toodescribe hello state of hello resource.</span></span>  

<span data-ttu-id="a4b53-190">è supportato i seguenti campi Hello:</span><span class="sxs-lookup"><span data-stu-id="a4b53-190">hello following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="a4b53-191">alias delle proprietà; per un elenco, vedere [alias](#aliases).</span><span class="sxs-lookup"><span data-stu-id="a4b53-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="a4b53-192">Effetto</span><span class="sxs-lookup"><span data-stu-id="a4b53-192">Effect</span></span>
<span data-ttu-id="a4b53-193">Il criterio supporta tre tipi di effetto: `deny`, `audit` e `append`.</span><span class="sxs-lookup"><span data-stu-id="a4b53-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="a4b53-194">**Negare** genera un evento nel Registro di controllo hello e si verifica un errore di richiesta di hello</span><span class="sxs-lookup"><span data-stu-id="a4b53-194">**Deny** generates an event in hello audit log and fails hello request</span></span>
* <span data-ttu-id="a4b53-195">**Controllo** genera un evento di avviso nel Registro di controllo ma non viene interrotta richiesta hello</span><span class="sxs-lookup"><span data-stu-id="a4b53-195">**Audit** generates a warning event in audit log but does not fail hello request</span></span>
* <span data-ttu-id="a4b53-196">**Aggiungere** aggiunge hello definito set di campi toohello richiesta</span><span class="sxs-lookup"><span data-stu-id="a4b53-196">**Append** adds hello defined set of fields toohello request</span></span> 

<span data-ttu-id="a4b53-197">Per **aggiungere**, è necessario fornire hello seguenti dettagli:</span><span class="sxs-lookup"><span data-stu-id="a4b53-197">For **append**, you must provide hello following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

<span data-ttu-id="a4b53-198">il valore di Hello può essere una stringa o un oggetto formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a4b53-198">hello value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="a4b53-199">Alias</span><span class="sxs-lookup"><span data-stu-id="a4b53-199">Aliases</span></span>

<span data-ttu-id="a4b53-200">Utilizzare gli alias tooaccess specifici delle proprietà per un tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="a4b53-200">You use property aliases tooaccess specific properties for a resource type.</span></span> <span data-ttu-id="a4b53-201">Gli alias consentono di toorestrict quali i valori consentiti per una proprietà su una risorsa.</span><span class="sxs-lookup"><span data-stu-id="a4b53-201">Aliases enable you toorestrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="a4b53-202">Ogni alias esegue il mapping toopaths in versioni diverse di API per un tipo di risorsa specificato.</span><span class="sxs-lookup"><span data-stu-id="a4b53-202">Each alias maps toopaths in different API versions for a given resource type.</span></span> <span data-ttu-id="a4b53-203">Durante la valutazione dei criteri, il motore dei criteri di hello Ottiene percorso della proprietà hello per la versione API.</span><span class="sxs-lookup"><span data-stu-id="a4b53-203">During policy evaluation, hello policy engine gets hello property path for that API version.</span></span>

<span data-ttu-id="a4b53-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="a4b53-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="a4b53-205">Alias</span><span class="sxs-lookup"><span data-stu-id="a4b53-205">Alias</span></span> | <span data-ttu-id="a4b53-206">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4b53-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="a4b53-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="a4b53-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="a4b53-208">Impostato se la porta server Redis non ssl di hello (6379) è abilitato.</span><span class="sxs-lookup"><span data-stu-id="a4b53-208">Set whether hello non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="a4b53-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="a4b53-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="a4b53-210">Impostare il numero di hello di partizioni toobe creato in una Cache di Cluster Premium.</span><span class="sxs-lookup"><span data-stu-id="a4b53-210">Set hello number of shards toobe created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="a4b53-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="a4b53-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="a4b53-212">Impostare dimensioni hello del hello Redis cache toodeploy.</span><span class="sxs-lookup"><span data-stu-id="a4b53-212">Set hello size of hello Redis cache toodeploy.</span></span>  |
| <span data-ttu-id="a4b53-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="a4b53-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="a4b53-214">Impostare toouse famiglia di SKU hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-214">Set hello SKU family toouse.</span></span> |
| <span data-ttu-id="a4b53-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="a4b53-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="a4b53-216">Impostare il tipo di hello di Cache Redis toodeploy.</span><span class="sxs-lookup"><span data-stu-id="a4b53-216">Set hello type of Redis Cache toodeploy.</span></span> |

<span data-ttu-id="a4b53-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="a4b53-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="a4b53-218">Alias</span><span class="sxs-lookup"><span data-stu-id="a4b53-218">Alias</span></span> | <span data-ttu-id="a4b53-219">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4b53-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="a4b53-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="a4b53-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="a4b53-221">Impostare il nome di hello del livello di prezzo hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-221">Set hello name of hello pricing tier.</span></span> |

<span data-ttu-id="a4b53-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="a4b53-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="a4b53-223">Alias</span><span class="sxs-lookup"><span data-stu-id="a4b53-223">Alias</span></span> | <span data-ttu-id="a4b53-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4b53-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="a4b53-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="a4b53-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="a4b53-226">Set hello offerta dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-226">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="a4b53-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="a4b53-228">Set hello editore dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-228">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="a4b53-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="a4b53-230">Set hello SKU dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-230">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="a4b53-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="a4b53-232">Imposta la versione dell'immagine della piattaforma hello o un'immagine del marketplace hello utilizzata toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-232">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |


<span data-ttu-id="a4b53-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="a4b53-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="a4b53-234">Alias</span><span class="sxs-lookup"><span data-stu-id="a4b53-234">Alias</span></span> | <span data-ttu-id="a4b53-235">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4b53-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="a4b53-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="a4b53-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="a4b53-237">Impostare l'identificatore hello della macchina virtuale di hello immagine usata toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-237">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="a4b53-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="a4b53-239">Set hello offerta dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-239">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="a4b53-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="a4b53-241">Set hello editore dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-241">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="a4b53-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="a4b53-243">Set hello SKU dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-243">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="a4b53-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="a4b53-245">Imposta la versione dell'immagine della piattaforma hello o un'immagine del marketplace hello utilizzata toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-245">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="a4b53-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="a4b53-247">Impostare l'immagine di hello o su disco è concesso in licenza in locale.</span><span class="sxs-lookup"><span data-stu-id="a4b53-247">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="a4b53-248">Questo valore viene utilizzato solo per le immagini che contengono hello del sistema operativo di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a4b53-248">This value is only used for images that contain hello Windows Server operating system.</span></span>  |
| <span data-ttu-id="a4b53-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="a4b53-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="a4b53-250">Set hello offerta dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-250">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="a4b53-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="a4b53-252">Set hello editore dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-252">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="a4b53-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="a4b53-254">Set hello SKU dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-254">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="a4b53-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="a4b53-256">Imposta la versione dell'immagine della piattaforma hello o un'immagine del marketplace hello utilizzata toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-256">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="a4b53-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="a4b53-258">Impostare hello vhd URI.</span><span class="sxs-lookup"><span data-stu-id="a4b53-258">Set hello vhd URI.</span></span> |
| <span data-ttu-id="a4b53-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="a4b53-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="a4b53-260">Impostare dimensioni hello della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-260">Set hello size of hello virtual machine.</span></span> |

<span data-ttu-id="a4b53-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="a4b53-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="a4b53-262">Alias</span><span class="sxs-lookup"><span data-stu-id="a4b53-262">Alias</span></span> | <span data-ttu-id="a4b53-263">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4b53-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="a4b53-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="a4b53-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="a4b53-265">Impostare il nome di hello del server di pubblicazione dell'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-265">Set hello name of hello extension’s publisher.</span></span> |
| <span data-ttu-id="a4b53-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="a4b53-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="a4b53-267">Impostare il tipo di hello di estensione.</span><span class="sxs-lookup"><span data-stu-id="a4b53-267">Set hello type of extension.</span></span> |
| <span data-ttu-id="a4b53-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="a4b53-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="a4b53-269">Impostare la versione di hello dell'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-269">Set hello version of hello extension.</span></span> |

<span data-ttu-id="a4b53-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="a4b53-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="a4b53-271">Alias</span><span class="sxs-lookup"><span data-stu-id="a4b53-271">Alias</span></span> | <span data-ttu-id="a4b53-272">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4b53-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="a4b53-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="a4b53-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="a4b53-274">Impostare l'identificatore hello della macchina virtuale di hello immagine usata toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-274">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="a4b53-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="a4b53-276">Set hello offerta dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-276">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="a4b53-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="a4b53-278">Set hello editore dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-278">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="a4b53-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="a4b53-280">Set hello SKU dell'immagine della piattaforma hello o un'immagine del marketplace utilizzata toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-280">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="a4b53-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="a4b53-282">Imposta la versione dell'immagine della piattaforma hello o un'immagine del marketplace hello utilizzata toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4b53-282">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="a4b53-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="a4b53-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="a4b53-284">Impostare l'immagine di hello o su disco è concesso in licenza in locale.</span><span class="sxs-lookup"><span data-stu-id="a4b53-284">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="a4b53-285">Questo valore viene utilizzato solo per le immagini che contengono hello del sistema operativo di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a4b53-285">This value is only used for images that contain hello Windows Server operating system.</span></span> |
| <span data-ttu-id="a4b53-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="a4b53-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="a4b53-287">Impostare prefisso del nome di computer per tutte le macchine virtuali hello hello in set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-287">Set hello computer name prefix for all  hello virtual machines in hello scale set.</span></span> |
| <span data-ttu-id="a4b53-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="a4b53-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="a4b53-289">Impostare l'URI del blob hello per l'immagine utente.</span><span class="sxs-lookup"><span data-stu-id="a4b53-289">Set hello blob URI for user image.</span></span> |
| <span data-ttu-id="a4b53-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="a4b53-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="a4b53-291">Impostare gli URL del contenitore hello che vengono utilizzati toostore dischi del sistema operativo per il set di scalabilità di hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-291">Set hello container URLs that are used toostore operating system disks for hello scale set.</span></span> |
| <span data-ttu-id="a4b53-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="a4b53-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="a4b53-293">Impostare dimensioni hello delle macchine virtuali in un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="a4b53-293">Set hello size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="a4b53-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="a4b53-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="a4b53-295">Impostare il livello di hello di macchine virtuali in un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="a4b53-295">Set hello tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="a4b53-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="a4b53-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="a4b53-297">Alias</span><span class="sxs-lookup"><span data-stu-id="a4b53-297">Alias</span></span> | <span data-ttu-id="a4b53-298">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4b53-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="a4b53-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="a4b53-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="a4b53-300">Impostare dimensioni hello del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-300">Set hello size of hello gateway.</span></span> |

<span data-ttu-id="a4b53-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="a4b53-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="a4b53-302">Alias</span><span class="sxs-lookup"><span data-stu-id="a4b53-302">Alias</span></span> | <span data-ttu-id="a4b53-303">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4b53-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="a4b53-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="a4b53-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="a4b53-305">Impostare il tipo di hello del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4b53-305">Set hello type of this virtual network gateway.</span></span> |
| <span data-ttu-id="a4b53-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="a4b53-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="a4b53-307">Nome SKU di gateway hello del set.</span><span class="sxs-lookup"><span data-stu-id="a4b53-307">Set hello gateway SKU name.</span></span> |

<span data-ttu-id="a4b53-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="a4b53-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="a4b53-309">Alias</span><span class="sxs-lookup"><span data-stu-id="a4b53-309">Alias</span></span> | <span data-ttu-id="a4b53-310">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4b53-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="a4b53-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="a4b53-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="a4b53-312">Impostare la versione hello del server di hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-312">Set hello version of hello server.</span></span> |

<span data-ttu-id="a4b53-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="a4b53-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="a4b53-314">Alias</span><span class="sxs-lookup"><span data-stu-id="a4b53-314">Alias</span></span> | <span data-ttu-id="a4b53-315">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4b53-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="a4b53-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="a4b53-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="a4b53-317">Impostare hello edition del database hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-317">Set hello edition of hello database.</span></span> |
| <span data-ttu-id="a4b53-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="a4b53-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="a4b53-319">Nome hello del set di database di hello hello pool elastico è in.</span><span class="sxs-lookup"><span data-stu-id="a4b53-319">Set hello name of hello elastic pool hello database is in.</span></span> |
| <span data-ttu-id="a4b53-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="a4b53-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="a4b53-321">Set hello configurato ID obiettivo livello di servizio del database hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-321">Set hello configured service level objective ID of hello database.</span></span> |
| <span data-ttu-id="a4b53-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="a4b53-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="a4b53-323">Impostare il nome di hello dell'obiettivo del livello di servizio configurato hello del database hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-323">Set hello name of hello configured service level objective of hello database.</span></span>  |

<span data-ttu-id="a4b53-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="a4b53-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="a4b53-325">Alias</span><span class="sxs-lookup"><span data-stu-id="a4b53-325">Alias</span></span> | <span data-ttu-id="a4b53-326">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4b53-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="a4b53-327">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="a4b53-327">servers/elasticpools</span></span> | <span data-ttu-id="a4b53-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="a4b53-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="a4b53-329">Totale hello set condivisa DTU per il pool elastico di hello database.</span><span class="sxs-lookup"><span data-stu-id="a4b53-329">Set hello total shared DTU for hello database elastic pool.</span></span> |
| <span data-ttu-id="a4b53-330">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="a4b53-330">servers/elasticpools</span></span> | <span data-ttu-id="a4b53-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="a4b53-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="a4b53-332">Impostare edition hello del pool elastico hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-332">Set hello edition of hello elastic pool.</span></span> |

<span data-ttu-id="a4b53-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="a4b53-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="a4b53-334">Alias</span><span class="sxs-lookup"><span data-stu-id="a4b53-334">Alias</span></span> | <span data-ttu-id="a4b53-335">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4b53-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="a4b53-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="a4b53-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="a4b53-337">Livello di accesso hello set utilizzato per la fatturazione.</span><span class="sxs-lookup"><span data-stu-id="a4b53-337">Set hello access tier used for billing.</span></span> |
| <span data-ttu-id="a4b53-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="a4b53-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="a4b53-339">Impostare il nome SKU hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-339">Set hello SKU name.</span></span> |
| <span data-ttu-id="a4b53-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="a4b53-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="a4b53-341">Specificare se il servizio hello crittografa i dati di hello archiviato nel servizio di archiviazione blob di hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-341">Set whether hello service encrypts hello data as it is stored in hello blob storage service.</span></span> |
| <span data-ttu-id="a4b53-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="a4b53-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="a4b53-343">Specificare se il servizio hello crittografa i dati di hello archiviato nel servizio di archiviazione di file hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-343">Set whether hello service encrypts hello data as it is stored in hello file storage service.</span></span> |
| <span data-ttu-id="a4b53-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="a4b53-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="a4b53-345">Impostare il nome SKU hello.</span><span class="sxs-lookup"><span data-stu-id="a4b53-345">Set hello SKU name.</span></span> |
| <span data-ttu-id="a4b53-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="a4b53-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="a4b53-347">Impostare tooallow solo https servizio toostorage del traffico.</span><span class="sxs-lookup"><span data-stu-id="a4b53-347">Set tooallow only https traffic toostorage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="a4b53-348">Esempi di criteri</span><span class="sxs-lookup"><span data-stu-id="a4b53-348">Policy examples</span></span>

<span data-ttu-id="a4b53-349">Hello seguenti argomenti contenga esempi di criteri:</span><span class="sxs-lookup"><span data-stu-id="a4b53-349">hello following topics contain policy examples:</span></span>

* <span data-ttu-id="a4b53-350">Per gli esempi di criteri di tag, vedere [Applicare criteri delle risorse per i tag](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="a4b53-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="a4b53-351">Per alcuni esempi di modelli di denominazione e di testo, vedere [Apply resource policies for names and text](resource-manager-policy-naming-convention.md) (Applicare criteri di risorse per nomi e testo).</span><span class="sxs-lookup"><span data-stu-id="a4b53-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="a4b53-352">Per esempi di criteri di archiviazione, vedere [si applicano agli account delle risorse criteri toostorage](resource-manager-policy-storage.md).</span><span class="sxs-lookup"><span data-stu-id="a4b53-352">For examples of storage policies, see [Apply resource policies toostorage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="a4b53-353">Per esempi di criteri di macchina virtuale, vedere [applicare i criteri di risorse tooLinux macchine virtuali](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) e [applicare i criteri di risorse tooWindows macchine virtuali](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a4b53-353">For examples of virtual machine policies, see [Apply resource policies tooLinux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies tooWindows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="a4b53-354">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4b53-354">Next steps</span></span>
* <span data-ttu-id="a4b53-355">Dopo aver definito una regola dei criteri, assegnare tooa ambito.</span><span class="sxs-lookup"><span data-stu-id="a4b53-355">After defining a policy rule, assign it tooa scope.</span></span> <span data-ttu-id="a4b53-356">criteri tooassign tramite il portale di hello, vedere [tooassign portale utilizzare Azure e gestire i criteri di risorse](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a4b53-356">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="a4b53-357">criteri di tooassign tramite l'API REST, PowerShell o l'interfaccia CLI di Azure, vedere [assegnare e gestire i criteri tramite script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="a4b53-357">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="a4b53-358">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="a4b53-358">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="a4b53-359">schema dei criteri di Hello è pubblicato nella [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="a4b53-359">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

