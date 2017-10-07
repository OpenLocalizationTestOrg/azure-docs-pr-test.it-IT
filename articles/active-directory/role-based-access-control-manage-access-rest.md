---
title: Controllo degli accessi basato su aaaRole con altre, Azure AD | Documenti Microsoft
description: La gestione del controllo di accesso basato sui ruoli con hello API REST
services: active-directory
documentationcenter: na
author: andredm7
manager: femila
editor: 
ms.assetid: 1f90228a-7aac-4ea7-ad82-b57d222ab128
ms.service: active-directory
ms.workload: multiple
ms.tgt_pltfrm: rest-api
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: andredm
ms.openlocfilehash: ccd402fd4fe4583288076cac23753dd067694681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-rest-api"></a>Controllare l'accesso basato sui ruoli con hello API REST
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Interfaccia della riga di comando di Azure](role-based-access-control-manage-access-azure-cli.md)
> * [API REST](role-based-access-control-manage-access-rest.md)

Role-Based Access controllo (RBAC) nel portale di Azure hello e API di gestione risorse di Azure consente di gestire l'accesso tooyour sottoscrizione e le risorse a un livello con granularità fine. Con questa funzionalità, è possibile concedere l'accesso per utenti, gruppi o entità servizio Active Directory assegnando toothem alcuni ruoli a un particolare ambito.

## <a name="list-all-role-assignments"></a>Elencare tutte le assegnazioni di ruolo
Elenca tutte le assegnazioni di ruolo hello in hello specificato ambito e subscopes.

le assegnazioni di ruolo toolist, è necessario avere accesso troppo`Microsoft.Authorization/roleAssignments/read` operazione nell'ambito di hello. Tutti i ruoli predefiniti hello vengono concesse operazione toothis di accesso. Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).

### <a name="request"></a>Richiesta
Hello utilizzare **ottenere** metodo con hello seguente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:

1. Sostituire *{scope}* con ambito hello per i quali si desiderano toolist le assegnazioni di ruolo hello. Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli:

   * Sottoscrizione: /subscriptions/{subscription-id}  
   * Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Sostituire *{api-version}* con 2015-07-01.
3. Sostituire *{filter}* con condizione hello che si desidera l'elenco di assegnazione di ruolo di tooapply toofilter hello:

   * Elenco di assegnazioni di ruolo per solo hello specificato ambito, escluse le assegnazioni di ruolo hello in subscopes:`atScope()`    
   * Elencare le assegnazioni di ruolo solo per l'utente, il gruppo o l'applicazione specifici: `principalId%20eq%20'{objectId of user, group, or service principal}'`  
   * Elencare le assegnazioni di ruolo per un utente specifico, incluse quelle ereditate dai gruppi | `assignedTo('{objectId of user}')`

### <a name="response"></a>Response
Codice di stato: 200

```
{
  "value": [
    {
      "properties": {
        "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
        "principalId": "2f9d4375-cbf1-48e8-83c9-2a0be4cb33fb",
        "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
        "createdOn": "2015-10-08T07:28:24.3905077Z",
        "updatedOn": "2015-10-08T07:28:24.3905077Z",
        "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
        "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/baa6e199-ad19-4667-b768-623fde31aedd",
      "type": "Microsoft.Authorization/roleAssignments",
      "name": "baa6e199-ad19-4667-b768-623fde31aedd"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role-assignment"></a>Ottenere informazioni su un'assegnazione di ruolo
Ottiene informazioni su una singola assegnazione di ruolo specificata dall'identificatore di assegnazione di ruolo hello.

tooget informazioni su un'assegnazione di ruolo, è necessario avere accesso troppo`Microsoft.Authorization/roleAssignments/read` operazione. Tutti i ruoli predefiniti hello vengono concesse operazione toothis di accesso. Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).

### <a name="request"></a>Richiesta
Hello utilizzare **ottenere** metodo con hello seguente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:

1. Sostituire *{scope}* con ambito hello per i quali si desiderano toolist le assegnazioni di ruolo hello. Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli:

   * Sottoscrizione: /subscriptions/{subscription-id}  
   * Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Sostituire *{role-assignment-id}* con identificatore GUID hello hello assegnazione di ruolo.
3. Sostituire *{api-version}* con 2015-07-01.

### <a name="response"></a>Response
Codice di stato: 200

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "principalId": "672f1afa-526a-4ef6-819c-975c7cd79022",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "createdOn": "2015-10-05T08:36:26.4014813Z",
    "updatedOn": "2015-10-05T08:36:26.4014813Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/196965ae-6088-4121-a92a-f1e33fdcc73e",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "196965ae-6088-4121-a92a-f1e33fdcc73e"
}

```

## <a name="create-a-role-assignment"></a>Creare un'assegnazione di ruolo
Creare un ruolo di assegnazione di hello specificato ambito per hello specificato principale concessione hello del ruolo specificato.

toocreate un'assegnazione di ruolo, è necessario avere accesso troppo`Microsoft.Authorization/roleAssignments/write` operazione. Di hello ruoli predefiniti, solo *proprietario* e *amministratore di accesso utente* vengono concesse operazione toothis di accesso. Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).

### <a name="request"></a>Richiesta
Hello utilizzare **inserire** metodo con hello seguente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:

1. Sostituire *{scope}* con ambito hello in corrispondenza del quale si desiderano toocreate le assegnazioni di ruolo hello. Quando si crea un'assegnazione di ruolo a un ambito padre, tutti gli ambiti figlio ereditano hello assegnazione di ruolo stesso. Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli:

   * Sottoscrizione: /subscriptions/{subscription-id}  
   * Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1   
   * Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Sostituire *{role-assignment-id}* con un nuovo GUID, che diventa l'identificatore GUID hello hello nuova assegnazione di ruolo.
3. Sostituire *{api-version}* con 2015-07-01.

Corpo della richiesta hello, fornire valori hello hello seguente formato:

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| Nome dell'elemento | Obbligatorio | Tipo | Descrizione |
| --- | --- | --- | --- |
| roleDefinitionId |Sì |String |Identificatore Hello del ruolo di hello. formato Hello dell'identificatore hello è:`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}` |
| principalId |Sì |String |objectId dell'entità hello Azure AD (utente, gruppo o entità servizio) viene assegnato il ruolo di hello toowhich. |

### <a name="response"></a>Response
Codice di stato: 201

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-16T00:27:19.6447515Z",
    "updatedOn": "2015-12-16T00:27:19.6447515Z",
    "createdBy": null,
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/2e9e86c8-0e91-4958-b21f-20f51f27bab2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "2e9e86c8-0e91-4958-b21f-20f51f27bab2"
}

```

## <a name="delete-a-role-assignment"></a>Eliminare un'assegnazione di ruolo
Elimina un'assegnazione di ruolo hello specificato ambito.

toodelete un'assegnazione di ruolo, è necessario disporre di accesso toohello `Microsoft.Authorization/roleAssignments/delete` operazione. Di hello ruoli predefiniti, solo *proprietario* e *amministratore di accesso utente* vengono concesse operazione toothis di accesso. Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).

### <a name="request"></a>Richiesta
Hello utilizzare **eliminare** metodo con hello seguente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:

1. Sostituire *{scope}* con ambito hello in corrispondenza del quale si desiderano toocreate le assegnazioni di ruolo hello. Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli:

   * Sottoscrizione: /subscriptions/{subscription-id}  
   * Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Sostituire *{role-assignment-id}* con l'id di assegnazione di ruolo hello GUID.
3. Sostituire *{api-version}* con 2015-07-01.

### <a name="response"></a>Response
Codice di stato: 200

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-17T23:21:40.8921564Z",
    "updatedOn": "2015-12-17T23:21:40.8921564Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/5eec22ee-ea5c-431e-8f41-82c560706fd2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "5eec22ee-ea5c-431e-8f41-82c560706fd2"
}

```

## <a name="list-all-roles"></a>Elencare tutti i ruoli
Elenca tutti i ruoli di hello che sono disponibili per l'assegnazione hello specificato ambito.

i ruoli toolist, è necessario avere accesso troppo`Microsoft.Authorization/roleDefinitions/read` operazione nell'ambito di hello. Tutti i ruoli predefiniti hello vengono concesse operazione toothis di accesso. Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).

### <a name="request"></a>Richiesta
Hello utilizzare **ottenere** metodo con hello seguente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:

1. Sostituire *{scope}* con ambito hello per i quali si desiderano toolist ruoli hello. Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli:

   * Sottoscrizione: /subscriptions/{subscription-id}  
   * Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Sostituire *{api-version}* con 2015-07-01.
3. Sostituire *{filter}* con condizione hello che si desidera tooapply toofilter hello elenco ruoli:

   * Elenco di ruoli disponibili per l'assegnazione hello specificato ambito e i relativi ambiti figlio:`atScopeAndBelow()`
   * Cercare un ruolo usando l'esatto nome visualizzato: `roleName%20eq%20'{role-display-name}'`. Nome visualizzato hello del ruolo hello nel formato con codifica URL hello utilizzare. Ad esempio: `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |

### <a name="response"></a>Response
Codice di stato: 200

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role"></a>Ottenere informazioni su un ruolo
Ottiene informazioni su un singolo ruolo specificato dall'identificatore hello della definizione di ruolo. informazioni tooget su un singolo ruolo usando il nome visualizzato, vedere [l'elenco di tutti i ruoli](role-based-access-control-manage-access-rest.md#list-all-roles).

tooget informazioni su un ruolo, è necessario avere accesso troppo`Microsoft.Authorization/roleDefinitions/read` operazione. Tutti i ruoli predefiniti hello vengono concesse operazione toothis di accesso. Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).

### <a name="request"></a>Richiesta
Hello utilizzare **ottenere** metodo con hello seguente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:

1. Sostituire *{scope}* con ambito hello per i quali si desiderano toolist le assegnazioni di ruolo hello. Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli:

   * Sottoscrizione: /subscriptions/{subscription-id}  
   * Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Sostituire *{role-definition-id}* con identificatore GUID hello hello definizione del ruolo.
3. Sostituire *{api-version}* con 2015-07-01.

### <a name="response"></a>Response
Codice di stato: 200

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="create-a-custom-role"></a>Creare un ruolo personalizzato
È possibile creare un ruolo personalizzato.

toocreate un ruolo personalizzato, è necessario avere accesso troppo`Microsoft.Authorization/roleDefinitions/write` operazione su tutti hello `AssignableScopes`. Di hello ruoli predefiniti, solo *proprietario* e *amministratore di accesso utente* vengono concesse operazione toothis di accesso. Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).

### <a name="request"></a>Richiesta
Hello utilizzare **inserire** metodo con hello seguente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:

1. Sostituire *{scope}* con hello prima *AssignableScope* di ruolo personalizzata hello. Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli.

   * Sottoscrizione: /subscriptions/{subscription-id}  
   * Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Sostituire *{role-definition-id}* con un nuovo GUID, che diventa l'identificatore GUID hello del nuovo ruolo personalizzato hello.
3. Sostituire *{api-version}* con 2015-07-01.

Corpo della richiesta hello, fornire valori hello hello seguente formato:

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| Nome dell'elemento | Obbligatorio | Tipo | Descrizione |
| --- | --- | --- | --- |
| name |Sì |String |Identificatore GUID del ruolo personalizzata hello. |
| properties.roleName |Sì |String |Nome visualizzato del ruolo personalizzata hello. La dimensione massima è di 128 caratteri. |
| properties.description |No |String |Descrizione del ruolo personalizzata hello. La dimensione massima è di 1024 caratteri. |
| properties.type |Sì |String |Impostare troppo "CustomRole". |
| properties.permissions.actions |sì |String[] |Una matrice di azione di stringhe che specifica le operazioni di hello concesse dal ruolo personalizzata hello. |
| properties.permissions.notActions |No |String[] |Una matrice di stringhe di azione specifica hello operazioni tooexclude da operazioni di hello concesse dal ruolo personalizzata hello. |
| properties.assignableScopes |Sì |String[] |Matrice di ambiti in cui hello può essere utilizzato un ruolo personalizzato. |

### <a name="response"></a>Response
Codice di stato: 201

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="update-a-custom-role"></a>Aggiornare un ruolo personalizzato
È possibile modificare un ruolo personalizzato.

toomodify un ruolo personalizzato, è necessario avere accesso troppo`Microsoft.Authorization/roleDefinitions/write` operazione su tutti hello `AssignableScopes`. Di hello ruoli predefiniti, solo *proprietario* e *amministratore di accesso utente* vengono concesse operazione toothis di accesso. Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).

### <a name="request"></a>Richiesta
Hello utilizzare **inserire** metodo con hello seguente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:

1. Sostituire *{scope}* con hello prima *AssignableScope* di ruolo personalizzata hello. Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli:

   * Sottoscrizione: /subscriptions/{subscription-id}  
   * Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Sostituire *{role-definition-id}* con identificatore GUID hello di ruolo personalizzata hello.
3. Sostituire *{api-version}* con 2015-07-01.

Corpo della richiesta hello, fornire valori hello hello seguente formato:

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| Nome dell'elemento | Obbligatorio | Tipo | Descrizione |
| --- | --- | --- | --- |
| name |Sì |String |Identificatore GUID del ruolo personalizzata hello. |
| properties.roleName |Sì |String |Nome visualizzato del ruolo personalizzata aggiornata hello. |
| properties.description |No |String |Descrizione di hello aggiornamento ruolo personalizzato. |
| properties.type |Sì |String |Impostare troppo "CustomRole". |
| properties.permissions.actions |sì |String[] |Una matrice di stringhe di azione specifica hello toowhich operazioni di hello aggiornato personalizzato ruolo concede l'accesso. |
| properties.permissions.notActions |No |String[] |Una matrice di azione stringhe specificando tooexclude di operazioni di hello dalle operazioni hello quali hello aggiornato concessioni di ruoli personalizzato. |
| properties.assignableScopes |Sì |String[] |Matrice di ambiti in cui hello può essere usato ruolo personalizzato aggiornato. |

### <a name="response"></a>Response
Codice di stato: 201

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="delete-a-custom-role"></a>Eliminare un ruolo personalizzato
È possibile eliminare un ruolo personalizzato.

toodelete un ruolo personalizzato, è necessario avere accesso troppo`Microsoft.Authorization/roleDefinitions/delete` operazione su tutti hello `AssignableScopes`. Di hello ruoli predefiniti, solo *proprietario* e *amministratore di accesso utente* vengono concesse operazione toothis di accesso. Per altre informazioni sulle assegnazioni di ruolo e la gestione dell'accesso per le risorse di Azure, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md).

### <a name="request"></a>Richiesta
Hello utilizzare **eliminare** metodo con hello seguente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

All'interno di hello URI, effettuare hello seguente le sostituzioni toocustomize la richiesta:

1. Sostituire *{scope}* con ambito hello in corrispondenza del quale si desidera definizione di ruolo toodelete hello. Hello seguono esempi Mostra come toospecify hello ambito per diversi livelli:

   * Sottoscrizione: /subscriptions/{subscription-id}  
   * Gruppo di risorse: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Risorsa: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Sostituire *{role-definition-id}* con id di definizione di ruolo hello GUID del ruolo personalizzata hello.
3. Sostituire *{api-version}* con 2015-07-01.

### <a name="response"></a>Response
Codice di stato: 200

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-16T00:07:02.9236555Z",
    "updatedOn": "2015-12-16T00:07:02.9236555Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/0bd62a70-e1b8-4e0b-a7c2-75cab365c95b",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "0bd62a70-e1b8-4e0b-a7c2-75cab365c95b"
}

```

## <a name="next-steps"></a>Passaggi successivi

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
