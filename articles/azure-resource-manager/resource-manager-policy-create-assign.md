---
title: Assegnare e gestire i criteri delle risorse di Azure | Microsoft Docs
description: Descrive come applicare i criteri delle risorse di Azure alle sottoscrizioni e ai gruppi di risorse e come visualizzare i criteri delle risorse.
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
ms.openlocfilehash: b204cffa8fab0ad27a9f78a81c04f0a0225d95f5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="cb83a-103">Assegnare e gestire i criteri delle risorse</span><span class="sxs-lookup"><span data-stu-id="cb83a-103">Assign and manage resource policies</span></span>

<span data-ttu-id="cb83a-104">Per implementare i criteri, è necessario eseguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="cb83a-104">To implement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="cb83a-105">Controllare le definizioni dei criteri (inclusi i criteri predefiniti forniti da Azure) per verificare se ne esiste già una nella sottoscrizione che soddisfa i requisiti.</span><span class="sxs-lookup"><span data-stu-id="cb83a-105">Check policy definitions (including built-in policies provided by Azure) to see if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="cb83a-106">Se ne esiste una, ottenerne il nome.</span><span class="sxs-lookup"><span data-stu-id="cb83a-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="cb83a-107">In caso contrario, definire la regola dei criteri con JSON e aggiungerla come definizione dei criteri nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cb83a-107">If one does not exist, define the policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="cb83a-108">Questo passaggio rende disponibile il criterio per l'assegnazione ma non applica le regole alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cb83a-108">This step makes the policy available for assignment but does not apply the rules to your subscription.</span></span>
4. <span data-ttu-id="cb83a-109">In entrambi i casi, assegnare i criteri a un ambito (ad esempio una sottoscrizione o un gruppo di risorse).</span><span class="sxs-lookup"><span data-stu-id="cb83a-109">For either case, assign the policy to a scope (such as a subscription or resource group).</span></span> <span data-ttu-id="cb83a-110">A questo punto le regole del criterio vengono applicate.</span><span class="sxs-lookup"><span data-stu-id="cb83a-110">The rules of the policy are now enforced.</span></span>

<span data-ttu-id="cb83a-111">Questo articolo illustra i passaggi per creare una definizione di criterio e assegnare tale definizione a un ambito tramite l'API REST, PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb83a-111">This article focuses on the steps to create a policy definition and assign that definition to a scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="cb83a-112">Se si preferisce usare il portale per assegnare i criteri, vedere [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) (Usare il portale di Azure per assegnare e gestire i criteri delle risorse).</span><span class="sxs-lookup"><span data-stu-id="cb83a-112">If you prefer to use the portal to assign policies, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="cb83a-113">Questo articolo non tratta la sintassi per la creazione della definizione di un criterio.</span><span class="sxs-lookup"><span data-stu-id="cb83a-113">This article does not focus on the syntax for creating the policy definition.</span></span> <span data-ttu-id="cb83a-114">Per informazioni sulla sintassi dei criteri, vedere [Usare i criteri per gestire le risorse e controllare l'accesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="cb83a-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="cb83a-115">API REST</span><span class="sxs-lookup"><span data-stu-id="cb83a-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="cb83a-116">Creare una definizione di criterio</span><span class="sxs-lookup"><span data-stu-id="cb83a-116">Create policy definition</span></span>

<span data-ttu-id="cb83a-117">È possibile creare un criterio con l' [API REST per le definizioni dei criteri](/rest/api/resources/policydefinitions).</span><span class="sxs-lookup"><span data-stu-id="cb83a-117">You can create a policy with the [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="cb83a-118">L'API REST consente di creare ed eliminare le definizioni dei criteri, e di ottenere informazioni sulle definizioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="cb83a-118">The REST API enables you to create and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="cb83a-119">Per creare una definizione di criterio, eseguire:</span><span class="sxs-lookup"><span data-stu-id="cb83a-119">To create a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="cb83a-120">Includere un corpo della richiesta in modo simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="cb83a-120">Include a request body similar to the following example:</span></span>

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

### <a name="assign-policy"></a><span data-ttu-id="cb83a-121">Assegnare un criterio</span><span class="sxs-lookup"><span data-stu-id="cb83a-121">Assign policy</span></span>

<span data-ttu-id="cb83a-122">È possibile applicare la definizione dei criteri all'ambito desiderato tramite l' [API REST per le assegnazioni dei criteri](/rest/api/resources/policyassignments).</span><span class="sxs-lookup"><span data-stu-id="cb83a-122">You can apply the policy definition at the desired scope through the [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="cb83a-123">L'API REST consente di creare ed eliminare le assegnazioni dei criteri e ottenere informazioni sulle assegnazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="cb83a-123">The REST API enables you to create and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="cb83a-124">Per creare un'assegnazione di criteri, eseguire:</span><span class="sxs-lookup"><span data-stu-id="cb83a-124">To create a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="cb83a-125">{policy-assignment} è il nome dell'assegnazione di criteri.</span><span class="sxs-lookup"><span data-stu-id="cb83a-125">The {policy-assignment} is the name of the policy assignment.</span></span>

<span data-ttu-id="cb83a-126">Includere un corpo della richiesta in modo simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="cb83a-126">Include a request body similar to the following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on the subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="cb83a-127">Visualizzare un criterio</span><span class="sxs-lookup"><span data-stu-id="cb83a-127">View policy</span></span>
<span data-ttu-id="cb83a-128">Per ottenere un criterio, usare l'operazione [Ottieni definizione criteri](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get).</span><span class="sxs-lookup"><span data-stu-id="cb83a-128">To get a policy, use the [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="cb83a-129">Ottenere gli alias</span><span class="sxs-lookup"><span data-stu-id="cb83a-129">Get aliases</span></span>
<span data-ttu-id="cb83a-130">È possibile recuperare gli alias tramite l'API REST:</span><span class="sxs-lookup"><span data-stu-id="cb83a-130">You can retrieve aliases through the REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="cb83a-131">L'esempio seguente illustra la definizione di un alias.</span><span class="sxs-lookup"><span data-stu-id="cb83a-131">The following example shows a definition of an alias.</span></span> <span data-ttu-id="cb83a-132">È possibile notare che un alias definisce percorsi in diverse versioni di API, anche in caso di una modifica del nome di una proprietà.</span><span class="sxs-lookup"><span data-stu-id="cb83a-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

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

## <a name="powershell"></a><span data-ttu-id="cb83a-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb83a-133">PowerShell</span></span>

<span data-ttu-id="cb83a-134">Prima di passare agli esempi di PowerShell, verificare di avere [installato la versione più recente](/powershell/azure/install-azurerm-ps) di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cb83a-134">Before proceeding with the PowerShell examples, make sure you have [installed the latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="cb83a-135">I parametri dei criteri sono stati aggiunti nella versione 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="cb83a-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="cb83a-136">Se si ha una versione precedente, gli esempi restituiscono un errore che indica che non è possibile trovare il parametro.</span><span class="sxs-lookup"><span data-stu-id="cb83a-136">If you have an earlier version, the examples return an error indicating the parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="cb83a-137">Visualizzare le definizioni dei criteri</span><span class="sxs-lookup"><span data-stu-id="cb83a-137">View policy definitions</span></span>
<span data-ttu-id="cb83a-138">Per visualizzare tutte le definizioni dei criteri nella sottoscrizione, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cb83a-138">To see all policy definitions in your subscription, use the following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="cb83a-139">Restituisce tutte le definizioni dei criteri disponibili, inclusi i criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="cb83a-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="cb83a-140">Tutti i criteri vengono restituiti nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="cb83a-140">Each policy is returned in the following format:</span></span>

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict the locations your organization can specify when deploying resources. Use to enforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

<span data-ttu-id="cb83a-141">Prima di procedere per creare una definizione dei criteri, esaminare i criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="cb83a-141">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="cb83a-142">Se si trovano i criteri predefiniti che applicano i limiti necessari, è possibile ignorare la creazione di una definizione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="cb83a-142">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="cb83a-143">Al contrario, assegnare i criteri predefiniti all'ambito desiderato.</span><span class="sxs-lookup"><span data-stu-id="cb83a-143">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="cb83a-144">Creare una definizione di criterio</span><span class="sxs-lookup"><span data-stu-id="cb83a-144">Create policy definition</span></span>
<span data-ttu-id="cb83a-145">È possibile creare una definizione di criterio usando il cmdlet `New-AzureRmPolicyDefinition`.</span><span class="sxs-lookup"><span data-stu-id="cb83a-145">You can create a policy definition using the `New-AzureRmPolicyDefinition` cmdlet.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy '{
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

<span data-ttu-id="cb83a-146">L'output viene archiviato in un oggetto `$definition` che viene usato durante l'assegnazione del criterio.</span><span class="sxs-lookup"><span data-stu-id="cb83a-146">The output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="cb83a-147">Anziché specificare JSON come parametro, è possibile fornire il percorso al file con estensione .json contenente la regola del criterio.</span><span class="sxs-lookup"><span data-stu-id="cb83a-147">Rather than specifying the JSON as a parameter, you can provide the path to a .json file containing the policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="cb83a-148">L'esempio seguente crea una definizione del criterio che include i parametri:</span><span class="sxs-lookup"><span data-stu-id="cb83a-148">The following example creates a policy definition that includes parameters:</span></span>

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
          "description": "The list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy to specify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a><span data-ttu-id="cb83a-149">Assegnare un criterio</span><span class="sxs-lookup"><span data-stu-id="cb83a-149">Assign policy</span></span>

<span data-ttu-id="cb83a-150">Si applicano i criteri nell'ambito desiderato mediante il cmdlet `New-AzureRmPolicyAssignment`.</span><span class="sxs-lookup"><span data-stu-id="cb83a-150">You apply the policy at the desired scope by using the `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="cb83a-151">L'esempio seguente descrive come assegnare i criteri a un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="cb83a-151">The following example assigns the policy to a resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="cb83a-152">Per assegnare i criteri che richiedono parametri, creare un oggetto con tali valori.</span><span class="sxs-lookup"><span data-stu-id="cb83a-152">To assign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="cb83a-153">L'esempio seguente descrive come recuperare i criteri predefiniti e passare i valori dei parametri:</span><span class="sxs-lookup"><span data-stu-id="cb83a-153">The following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="cb83a-154">Visualizzare l'assegnazione di un criterio</span><span class="sxs-lookup"><span data-stu-id="cb83a-154">View policy assignment</span></span>

<span data-ttu-id="cb83a-155">Per ottenere un'assegnazione di criteri specifica, usare:</span><span class="sxs-lookup"><span data-stu-id="cb83a-155">To get a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="cb83a-156">Per visualizzare la regola dei criteri per una definizione di criteri, usare:</span><span class="sxs-lookup"><span data-stu-id="cb83a-156">To view the policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="cb83a-157">Rimuovere l'assegnazione di un criterio</span><span class="sxs-lookup"><span data-stu-id="cb83a-157">Remove policy assignment</span></span> 

<span data-ttu-id="cb83a-158">Per rimuovere un'assegnazione di criteri, usare:</span><span class="sxs-lookup"><span data-stu-id="cb83a-158">To remove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="cb83a-159">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="cb83a-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="cb83a-160">Visualizzare le definizioni dei criteri</span><span class="sxs-lookup"><span data-stu-id="cb83a-160">View policy definitions</span></span>
<span data-ttu-id="cb83a-161">Per visualizzare tutte le definizioni dei criteri nella sottoscrizione, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cb83a-161">To see all policy definitions in your subscription, use the following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="cb83a-162">Restituisce tutte le definizioni dei criteri disponibili, inclusi i criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="cb83a-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="cb83a-163">Tutti i criteri vengono restituiti nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="cb83a-163">Each policy is returned in the following format:</span></span>

```azurecli
{                                                            
  "description": "This policy enables you to restrict the locations your organization can specify when deploying resources. Use to enforce your geo-compliance requirements.",                      
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

<span data-ttu-id="cb83a-164">Prima di procedere per creare una definizione dei criteri, esaminare i criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="cb83a-164">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="cb83a-165">Se si trovano i criteri predefiniti che applicano i limiti necessari, è possibile ignorare la creazione di una definizione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="cb83a-165">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="cb83a-166">Al contrario, assegnare i criteri predefiniti all'ambito desiderato.</span><span class="sxs-lookup"><span data-stu-id="cb83a-166">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="cb83a-167">Creare una definizione di criterio</span><span class="sxs-lookup"><span data-stu-id="cb83a-167">Create policy definition</span></span>

<span data-ttu-id="cb83a-168">È possibile creare una definizione di criteri usando l'interfaccia della riga di comando di Azure con il comando di definizione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="cb83a-168">You can create a policy definition using Azure CLI with the policy definition command.</span></span>

```azurecli
az policy definition create --name coolAccessTier --description "Policy to specify access tier." --rules '{
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

### <a name="assign-policy"></a><span data-ttu-id="cb83a-169">Assegnare un criterio</span><span class="sxs-lookup"><span data-stu-id="cb83a-169">Assign policy</span></span>

<span data-ttu-id="cb83a-170">È possibile applicare i criteri all'ambito desiderato usando il comando per l'assegnazione di criteri.</span><span class="sxs-lookup"><span data-stu-id="cb83a-170">You can apply the policy to the desired scope by using the policy assignment command.</span></span> <span data-ttu-id="cb83a-171">L'esempio seguente descrive come assegnare i criteri a un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="cb83a-171">The following example assigns a policy to a resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="cb83a-172">Visualizzare l'assegnazione di un criterio</span><span class="sxs-lookup"><span data-stu-id="cb83a-172">View policy assignment</span></span>

<span data-ttu-id="cb83a-173">Per visualizzare l'assegnazione di criteri, specificare il nome dell'assegnazione dei criteri e l'ambito:</span><span class="sxs-lookup"><span data-stu-id="cb83a-173">To view a policy assignment, provide the policy assignment name and the scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="cb83a-174">Rimuovere l'assegnazione di un criterio</span><span class="sxs-lookup"><span data-stu-id="cb83a-174">Remove policy assignment</span></span> 

<span data-ttu-id="cb83a-175">Per rimuovere un'assegnazione di criteri, usare:</span><span class="sxs-lookup"><span data-stu-id="cb83a-175">To remove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="cb83a-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cb83a-176">Next steps</span></span>
* <span data-ttu-id="cb83a-177">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="cb83a-177">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

