---
title: aaaAssign e gestire i criteri di risorse di Azure | Documenti Microsoft
description: Viene descritto come tooapply Azure criteri toosubscriptions e risorse gruppi di risorse e come tooview criteri delle risorse.
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
ms.date: 07/26/2017
ms.author: tomfitz
ms.openlocfilehash: b6999b43bbcc80d2fde9911352fd4352fa453443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="71dd4-103">Assegnare e gestire i criteri delle risorse</span><span class="sxs-lookup"><span data-stu-id="71dd4-103">Assign and manage resource policies</span></span>

<span data-ttu-id="71dd4-104">tooimplement un criterio, è necessario eseguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="71dd4-104">tooimplement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="71dd4-105">Controllare criteri definizioni (inclusi i criteri predefiniti forniti da Azure) toosee se ne esiste già nella sottoscrizione che soddisfa i requisiti.</span><span class="sxs-lookup"><span data-stu-id="71dd4-105">Check policy definitions (including built-in policies provided by Azure) toosee if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="71dd4-106">Se ne esiste una, ottenerne il nome.</span><span class="sxs-lookup"><span data-stu-id="71dd4-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="71dd4-107">Se non esiste, definire una regola dei criteri di hello con JSON e aggiungerlo come una definizione dei criteri nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="71dd4-107">If one does not exist, define hello policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="71dd4-108">Questo passaggio rende disponibili per l'assegnazione dei criteri di hello ma non alla sottoscrizione di tooyour hello regole.</span><span class="sxs-lookup"><span data-stu-id="71dd4-108">This step makes hello policy available for assignment but does not apply hello rules tooyour subscription.</span></span>
4. <span data-ttu-id="71dd4-109">Per entrambi i casi, assegnare l'ambito di tooa hello criteri (ad esempio, un gruppo di risorse o di sottoscrizione).</span><span class="sxs-lookup"><span data-stu-id="71dd4-109">For either case, assign hello policy tooa scope (such as a subscription or resource group).</span></span> <span data-ttu-id="71dd4-110">vengono applicate le regole dei criteri di hello Hello.</span><span class="sxs-lookup"><span data-stu-id="71dd4-110">hello rules of hello policy are now enforced.</span></span>

<span data-ttu-id="71dd4-111">In questo articolo è incentrato sui hello passaggi toocreate una definizione dei criteri e assegnare tale ambito tooa definizione mediante Azure CLI, PowerShell o API REST.</span><span class="sxs-lookup"><span data-stu-id="71dd4-111">This article focuses on hello steps toocreate a policy definition and assign that definition tooa scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="71dd4-112">Se si preferiscono criteri di toouse hello tooassign portale, vedere [tooassign portale utilizzare Azure e gestire i criteri di risorse](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="71dd4-112">If you prefer toouse hello portal tooassign policies, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="71dd4-113">In questo articolo non si basa sulla sintassi da utilizzare per la creazione di una definizione di criteri hello hello.</span><span class="sxs-lookup"><span data-stu-id="71dd4-113">This article does not focus on hello syntax for creating hello policy definition.</span></span> <span data-ttu-id="71dd4-114">Per informazioni sulla sintassi dei criteri, vedere [Usare i criteri per gestire le risorse e controllare l'accesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="71dd4-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="71dd4-115">API REST</span><span class="sxs-lookup"><span data-stu-id="71dd4-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="71dd4-116">Creare una definizione di criterio</span><span class="sxs-lookup"><span data-stu-id="71dd4-116">Create policy definition</span></span>

<span data-ttu-id="71dd4-117">È possibile creare un criterio con hello [API REST per le definizioni dei criteri](/rest/api/resources/policydefinitions).</span><span class="sxs-lookup"><span data-stu-id="71dd4-117">You can create a policy with hello [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="71dd4-118">API REST Hello consente toocreate eliminare le definizioni dei criteri e ottenere informazioni sulle definizioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="71dd4-118">hello REST API enables you toocreate and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="71dd4-119">toocreate una definizione dei criteri, eseguire:</span><span class="sxs-lookup"><span data-stu-id="71dd4-119">toocreate a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="71dd4-120">Includere un toohello simile corpo della richiesta seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="71dd4-120">Include a request body similar toohello following example:</span></span>

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

### <a name="assign-policy"></a><span data-ttu-id="71dd4-121">Assegnare un criterio</span><span class="sxs-lookup"><span data-stu-id="71dd4-121">Assign policy</span></span>

<span data-ttu-id="71dd4-122">È possibile applicare una definizione di criteri hello ambito hello desiderato tramite hello [API REST per le assegnazioni di criteri](/rest/api/resources/policyassignments).</span><span class="sxs-lookup"><span data-stu-id="71dd4-122">You can apply hello policy definition at hello desired scope through hello [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="71dd4-123">API REST di Hello consente toocreate eliminare le assegnazioni di criteri e ottenere informazioni sulle assegnazioni esistente.</span><span class="sxs-lookup"><span data-stu-id="71dd4-123">hello REST API enables you toocreate and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="71dd4-124">toocreate un'assegnazione di criteri, eseguire:</span><span class="sxs-lookup"><span data-stu-id="71dd4-124">toocreate a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="71dd4-125">Hello {assegnazione criteri} è il nome di hello dell'assegnazione di criteri hello.</span><span class="sxs-lookup"><span data-stu-id="71dd4-125">hello {policy-assignment} is hello name of hello policy assignment.</span></span>

<span data-ttu-id="71dd4-126">Includere un toohello simile corpo della richiesta seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="71dd4-126">Include a request body similar toohello following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on hello subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="71dd4-127">Visualizzare un criterio</span><span class="sxs-lookup"><span data-stu-id="71dd4-127">View policy</span></span>
<span data-ttu-id="71dd4-128">tooget un criterio, utilizzare hello [prelevare la definizione di criteri](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operazione.</span><span class="sxs-lookup"><span data-stu-id="71dd4-128">tooget a policy, use hello [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="71dd4-129">Ottenere gli alias</span><span class="sxs-lookup"><span data-stu-id="71dd4-129">Get aliases</span></span>
<span data-ttu-id="71dd4-130">È possibile recuperare gli alias tramite hello API REST:</span><span class="sxs-lookup"><span data-stu-id="71dd4-130">You can retrieve aliases through hello REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="71dd4-131">Hello di esempio seguente viene illustrata una definizione di un alias.</span><span class="sxs-lookup"><span data-stu-id="71dd4-131">hello following example shows a definition of an alias.</span></span> <span data-ttu-id="71dd4-132">È possibile notare che un alias definisce percorsi in diverse versioni di API, anche in caso di una modifica del nome di una proprietà.</span><span class="sxs-lookup"><span data-stu-id="71dd4-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

```json
"aliases": [
    {
      "name": "Microsoft.Storage/storageAccounts/sku.name",
      "paths": [
        {
          "path": "properties.accountType",
          "apiVersions": [
            "2015-06-15",
            "2015-05-01-preview"
          ]
        },
        {
          "path": "sku.name",
          "apiVersions": [
            "2016-01-01"
          ]
        }
      ]
    }
]
```

## <a name="powershell"></a><span data-ttu-id="71dd4-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="71dd4-133">PowerShell</span></span>

<span data-ttu-id="71dd4-134">Prima di procedere con esempi di PowerShell hello, assicurarsi di avere [installata la versione più recente di hello](/powershell/azure/install-azurerm-ps) di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="71dd4-134">Before proceeding with hello PowerShell examples, make sure you have [installed hello latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="71dd4-135">I parametri dei criteri sono stati aggiunti nella versione 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="71dd4-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="71dd4-136">Se si dispone di una versione precedente, esempi di hello restituiscono che Impossibile trovare il parametro hello che indica un errore.</span><span class="sxs-lookup"><span data-stu-id="71dd4-136">If you have an earlier version, hello examples return an error indicating hello parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="71dd4-137">Visualizzare le definizioni dei criteri</span><span class="sxs-lookup"><span data-stu-id="71dd4-137">View policy definitions</span></span>
<span data-ttu-id="71dd4-138">toosee tutte le definizioni dei criteri nella sottoscrizione, utilizzare hello seguente comando:</span><span class="sxs-lookup"><span data-stu-id="71dd4-138">toosee all policy definitions in your subscription, use hello following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="71dd4-139">Restituisce tutte le definizioni dei criteri disponibili, inclusi i criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="71dd4-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="71dd4-140">Ogni criterio viene restituito in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="71dd4-140">Each policy is returned in hello following format:</span></span>

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict hello locations your organization can specify when deploying resources. Use tooenforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

<span data-ttu-id="71dd4-141">Prima di procedere toocreate una definizione dei criteri, esaminare i criteri predefiniti di hello.</span><span class="sxs-lookup"><span data-stu-id="71dd4-141">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="71dd4-142">Se si trova un criterio predefinito che applica limiti hello che è necessario, è possibile ignorare la creazione di una definizione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="71dd4-142">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="71dd4-143">Al contrario, assegnare ambito toohello desiderato dei criteri predefiniti hello.</span><span class="sxs-lookup"><span data-stu-id="71dd4-143">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="71dd4-144">Creare una definizione di criterio</span><span class="sxs-lookup"><span data-stu-id="71dd4-144">Create policy definition</span></span>
<span data-ttu-id="71dd4-145">È possibile creare una definizione dei criteri utilizzando hello `New-AzureRmPolicyDefinition` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="71dd4-145">You can create a policy definition using hello `New-AzureRmPolicyDefinition` cmdlet.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy '{
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
}'
```            

<span data-ttu-id="71dd4-146">output di Hello viene archiviato un `$definition` oggetto, che viene utilizzato durante l'assegnazione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="71dd4-146">hello output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="71dd4-147">Anziché specificare hello JSON come parametro, è possibile specificare i file con estensione JSON tooa percorso hello contenente una regola dei criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="71dd4-147">Rather than specifying hello JSON as a parameter, you can provide hello path tooa .json file containing hello policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="71dd4-148">Hello esempio seguente viene creata una definizione dei criteri che include i parametri:</span><span class="sxs-lookup"><span data-stu-id="71dd4-148">hello following example creates a policy definition that includes parameters:</span></span>

```powershell
$policy = '{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Storage/storageAccounts"
            },
            {
                "not": {
                    "field": "location",
                    "in": "[parameters(''allowedLocations'')]"
                }
            }
        ]
    },
    "then": {
        "effect": "Deny"
    }
}'

$parameters = '{
    "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy toospecify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a><span data-ttu-id="71dd4-149">Assegnare un criterio</span><span class="sxs-lookup"><span data-stu-id="71dd4-149">Assign policy</span></span>

<span data-ttu-id="71dd4-150">Si applicano criteri hello nell'ambito di hello desiderato utilizzando hello `New-AzureRmPolicyAssignment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="71dd4-150">You apply hello policy at hello desired scope by using hello `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="71dd4-151">Hello di esempio seguente assegna gruppo di risorse tooa hello criteri.</span><span class="sxs-lookup"><span data-stu-id="71dd4-151">hello following example assigns hello policy tooa resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="71dd4-152">tooassign un criterio che richiede parametri, creare e l'oggetto con tali valori.</span><span class="sxs-lookup"><span data-stu-id="71dd4-152">tooassign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="71dd4-153">Hello esempio recupera i criteri predefiniti e passa i valori di parametri:</span><span class="sxs-lookup"><span data-stu-id="71dd4-153">hello following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="71dd4-154">Visualizzare l'assegnazione di un criterio</span><span class="sxs-lookup"><span data-stu-id="71dd4-154">View policy assignment</span></span>

<span data-ttu-id="71dd4-155">tooget un'assegnazione di criteri specifico, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="71dd4-155">tooget a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="71dd4-156">regola dei criteri hello tooview per una definizione di criteri, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="71dd4-156">tooview hello policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="71dd4-157">Rimuovere l'assegnazione di un criterio</span><span class="sxs-lookup"><span data-stu-id="71dd4-157">Remove policy assignment</span></span> 

<span data-ttu-id="71dd4-158">tooremove un'assegnazione di criteri, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="71dd4-158">tooremove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="71dd4-159">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="71dd4-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="71dd4-160">Visualizzare le definizioni dei criteri</span><span class="sxs-lookup"><span data-stu-id="71dd4-160">View policy definitions</span></span>
<span data-ttu-id="71dd4-161">toosee tutte le definizioni dei criteri nella sottoscrizione, utilizzare hello seguente comando:</span><span class="sxs-lookup"><span data-stu-id="71dd4-161">toosee all policy definitions in your subscription, use hello following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="71dd4-162">Restituisce tutte le definizioni dei criteri disponibili, inclusi i criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="71dd4-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="71dd4-163">Ogni criterio viene restituito in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="71dd4-163">Each policy is returned in hello following format:</span></span>

```azurecli
{                                                            
  "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources. Use tooenforce your geo-compliance requirements.",                      
  "displayName": "Allowed locations",
  "id": "/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "name": "e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "policyRule": {
    "if": {
      "not": {
        "field": "location",
        "in": "[parameters('listOfAllowedLocations')]"
      }
    },
    "then": {
      "effect": "Deny"
    }
  },
  "policyType": "BuiltIn"
}
```

<span data-ttu-id="71dd4-164">Prima di procedere toocreate una definizione dei criteri, esaminare i criteri predefiniti di hello.</span><span class="sxs-lookup"><span data-stu-id="71dd4-164">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="71dd4-165">Se si trova un criterio predefinito che applica limiti hello che è necessario, è possibile ignorare la creazione di una definizione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="71dd4-165">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="71dd4-166">Al contrario, assegnare ambito toohello desiderato dei criteri predefiniti hello.</span><span class="sxs-lookup"><span data-stu-id="71dd4-166">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="71dd4-167">Creare una definizione di criterio</span><span class="sxs-lookup"><span data-stu-id="71dd4-167">Create policy definition</span></span>

<span data-ttu-id="71dd4-168">È possibile creare una definizione dei criteri usando l'interfaccia CLI di Azure con il comando di definizione dei criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="71dd4-168">You can create a policy definition using Azure CLI with hello policy definition command.</span></span>

```azurecli
az policy definition create --name coolAccessTier --description "Policy toospecify access tier." --rules '{
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
}'    
```

### <a name="assign-policy"></a><span data-ttu-id="71dd4-169">Assegnare un criterio</span><span class="sxs-lookup"><span data-stu-id="71dd4-169">Assign policy</span></span>

<span data-ttu-id="71dd4-170">È possibile applicare ambito toohello desiderato dei criteri hello comando assegnazione di criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="71dd4-170">You can apply hello policy toohello desired scope by using hello policy assignment command.</span></span> <span data-ttu-id="71dd4-171">Hello di esempio seguente consente di assegnare un gruppo di risorse tooa di criteri.</span><span class="sxs-lookup"><span data-stu-id="71dd4-171">hello following example assigns a policy tooa resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="71dd4-172">Visualizzare l'assegnazione di un criterio</span><span class="sxs-lookup"><span data-stu-id="71dd4-172">View policy assignment</span></span>

<span data-ttu-id="71dd4-173">tooview un'assegnazione di criteri, specificare nome dell'assegnazione dei criteri hello e ambito hello:</span><span class="sxs-lookup"><span data-stu-id="71dd4-173">tooview a policy assignment, provide hello policy assignment name and hello scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="71dd4-174">Rimuovere l'assegnazione di un criterio</span><span class="sxs-lookup"><span data-stu-id="71dd4-174">Remove policy assignment</span></span> 

<span data-ttu-id="71dd4-175">tooremove un'assegnazione di criteri, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="71dd4-175">tooremove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="71dd4-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="71dd4-176">Next steps</span></span>
* <span data-ttu-id="71dd4-177">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="71dd4-177">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

