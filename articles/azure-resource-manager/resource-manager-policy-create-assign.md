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
# <a name="assign-and-manage-resource-policies"></a>Assegnare e gestire i criteri delle risorse

tooimplement un criterio, è necessario eseguire questi passaggi:

1. Controllare criteri definizioni (inclusi i criteri predefiniti forniti da Azure) toosee se ne esiste già nella sottoscrizione che soddisfa i requisiti.
2. Se ne esiste una, ottenerne il nome.
3. Se non esiste, definire una regola dei criteri di hello con JSON e aggiungerlo come una definizione dei criteri nella sottoscrizione. Questo passaggio rende disponibili per l'assegnazione dei criteri di hello ma non alla sottoscrizione di tooyour hello regole.
4. Per entrambi i casi, assegnare l'ambito di tooa hello criteri (ad esempio, un gruppo di risorse o di sottoscrizione). vengono applicate le regole dei criteri di hello Hello.

In questo articolo è incentrato sui hello passaggi toocreate una definizione dei criteri e assegnare tale ambito tooa definizione mediante Azure CLI, PowerShell o API REST. Se si preferiscono criteri di toouse hello tooassign portale, vedere [tooassign portale utilizzare Azure e gestire i criteri di risorse](resource-manager-policy-portal.md). In questo articolo non si basa sulla sintassi da utilizzare per la creazione di una definizione di criteri hello hello. Per informazioni sulla sintassi dei criteri, vedere [Usare i criteri per gestire le risorse e controllare l'accesso](resource-manager-policy.md).

## <a name="rest-api"></a>API REST

### <a name="create-policy-definition"></a>Creare una definizione di criterio

È possibile creare un criterio con hello [API REST per le definizioni dei criteri](/rest/api/resources/policydefinitions). API REST Hello consente toocreate eliminare le definizioni dei criteri e ottenere informazioni sulle definizioni esistenti.

toocreate una definizione dei criteri, eseguire:

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

Includere un toohello simile corpo della richiesta seguente esempio:

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

### <a name="assign-policy"></a>Assegnare un criterio

È possibile applicare una definizione di criteri hello ambito hello desiderato tramite hello [API REST per le assegnazioni di criteri](/rest/api/resources/policyassignments). API REST di Hello consente toocreate eliminare le assegnazioni di criteri e ottenere informazioni sulle assegnazioni esistente.

toocreate un'assegnazione di criteri, eseguire:

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

Hello {assegnazione criteri} è il nome di hello dell'assegnazione di criteri hello.

Includere un toohello simile corpo della richiesta seguente esempio:

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

### <a name="view-policy"></a>Visualizzare un criterio
tooget un criterio, utilizzare hello [prelevare la definizione di criteri](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operazione.

### <a name="get-aliases"></a>Ottenere gli alias
È possibile recuperare gli alias tramite hello API REST:

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

Hello di esempio seguente viene illustrata una definizione di un alias. È possibile notare che un alias definisce percorsi in diverse versioni di API, anche in caso di una modifica del nome di una proprietà. 

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

## <a name="powershell"></a>PowerShell

Prima di procedere con esempi di PowerShell hello, assicurarsi di avere [installata la versione più recente di hello](/powershell/azure/install-azurerm-ps) di Azure PowerShell. I parametri dei criteri sono stati aggiunti nella versione 3.6.0. Se si dispone di una versione precedente, esempi di hello restituiscono che Impossibile trovare il parametro hello che indica un errore.

### <a name="view-policy-definitions"></a>Visualizzare le definizioni dei criteri
toosee tutte le definizioni dei criteri nella sottoscrizione, utilizzare hello seguente comando:

```powershell
Get-AzureRmPolicyDefinition
```

Restituisce tutte le definizioni dei criteri disponibili, inclusi i criteri predefiniti. Ogni criterio viene restituito in hello seguente formato:

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

Prima di procedere toocreate una definizione dei criteri, esaminare i criteri predefiniti di hello. Se si trova un criterio predefinito che applica limiti hello che è necessario, è possibile ignorare la creazione di una definizione dei criteri. Al contrario, assegnare ambito toohello desiderato dei criteri predefiniti hello.

### <a name="create-policy-definition"></a>Creare una definizione di criterio
È possibile creare una definizione dei criteri utilizzando hello `New-AzureRmPolicyDefinition` cmdlet.

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

output di Hello viene archiviato un `$definition` oggetto, che viene utilizzato durante l'assegnazione dei criteri. 

Anziché specificare hello JSON come parametro, è possibile specificare i file con estensione JSON tooa percorso hello contenente una regola dei criteri di hello.

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

Hello esempio seguente viene creata una definizione dei criteri che include i parametri:

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

### <a name="assign-policy"></a>Assegnare un criterio

Si applicano criteri hello nell'ambito di hello desiderato utilizzando hello `New-AzureRmPolicyAssignment` cmdlet. Hello di esempio seguente assegna gruppo di risorse tooa hello criteri.

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

tooassign un criterio che richiede parametri, creare e l'oggetto con tali valori. Hello esempio recupera i criteri predefiniti e passa i valori di parametri:

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a>Visualizzare l'assegnazione di un criterio

tooget un'assegnazione di criteri specifico, utilizzare:

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

regola dei criteri hello tooview per una definizione di criteri, utilizzare:

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a>Rimuovere l'assegnazione di un criterio 

tooremove un'assegnazione di criteri, utilizzare:

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

### <a name="view-policy-definitions"></a>Visualizzare le definizioni dei criteri
toosee tutte le definizioni dei criteri nella sottoscrizione, utilizzare hello seguente comando:

```azurecli
az policy definition list
```

Restituisce tutte le definizioni dei criteri disponibili, inclusi i criteri predefiniti. Ogni criterio viene restituito in hello seguente formato:

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

Prima di procedere toocreate una definizione dei criteri, esaminare i criteri predefiniti di hello. Se si trova un criterio predefinito che applica limiti hello che è necessario, è possibile ignorare la creazione di una definizione dei criteri. Al contrario, assegnare ambito toohello desiderato dei criteri predefiniti hello.

### <a name="create-policy-definition"></a>Creare una definizione di criterio

È possibile creare una definizione dei criteri usando l'interfaccia CLI di Azure con il comando di definizione dei criteri di hello.

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

### <a name="assign-policy"></a>Assegnare un criterio

È possibile applicare ambito toohello desiderato dei criteri hello comando assegnazione di criteri di hello. Hello di esempio seguente consente di assegnare un gruppo di risorse tooa di criteri.

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a>Visualizzare l'assegnazione di un criterio

tooview un'assegnazione di criteri, specificare nome dell'assegnazione dei criteri hello e ambito hello:

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a>Rimuovere l'assegnazione di un criterio 

tooremove un'assegnazione di criteri, utilizzare:

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a>Passaggi successivi
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).

