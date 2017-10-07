---
title: aaaManage Role-Based Access Control (RBAC) with Azure PowerShell | Documenti Microsoft
description: Come toomanage RBAC con Azure PowerShell, inclusi l'elenco di ruoli, l'assegnazione dei ruoli e l'eliminazione di assegnazioni di ruolo.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 9e225dba-9044-4b13-b573-2f30d77925a9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: fa44991113e75b345177867b0bede38de4373e04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a>Gestire il controllo degli accessi in base al ruolo con Azure PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Interfaccia della riga di comando di Azure](role-based-access-control-manage-access-azure-cli.md)
> * [API REST](role-based-access-control-manage-access-rest.md)

Controllo di accesso basato sui ruoli (RBAC) è possibile utilizzare in hello portale di Azure e sottoscrizione tooyour di API di gestione risorse di Azure toomanage accesso a un livello con granularità fine. Con questa funzionalità, è possibile concedere l'accesso per utenti, gruppi o entità servizio Active Directory assegnando toothem alcuni ruoli a un particolare ambito.

Prima di poter utilizzare PowerShell toomanage RBAC, è necessario hello seguenti prerequisiti:

* Azure PowerShell 0.8.8 o versione successiva. versione più recente di tooinstall hello e associare con la sottoscrizione di Azure, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).
* Cmdlet di Azure Resource Manager Installare hello [i cmdlet di Azure Resource Manager](/powershell/azure/overview) in PowerShell.

## <a name="list-roles"></a>Elenco dei ruoli
### <a name="list-all-available-roles"></a>Elencare tutti i ruoli disponibili
ruoli RBAC toolist disponibili per l'assegnazione e tooinspect hello operazioni toowhich concedere l'accesso, utilizzare `Get-AzureRmRoleDefinition`.

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a>Elencare le azioni di un ruolo
le azioni di hello toolist per un ruolo specifico, utilizzare `Get-AzureRmRoleDefinition <role name>`.

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition per un ruolo specifico - Schermata](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a>Assegnazioni di accesso
utilizzare assegnazioni di accesso RBAC toolist, `Get-AzureRmRoleAssignment`.

### <a name="list-role-assignments-at-a-specific-scope"></a>Elencare le assegnazioni di ruolo in un ambito specifico
È possibile visualizzare tutte le assegnazioni di accesso hello per una sottoscrizione specificata, un gruppo di risorse o una risorsa. Ad esempio, toosee hello tutte le assegnazioni active hello per un gruppo di risorse, utilizzare `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition per un gruppo di risorse - Schermata](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a>Elenco ruoli assegnati tooa utente
toolist tutti i ruoli di hello assegnati tooa specificato utente e ruoli hello che sono assegnati dei gruppi toohello toowhich hello utente appartiene, utilizzare `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition per un utente - Schermata](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a>Elencare le assegnazioni di ruoli per l'amministratore e i coamministratori del servizio classici
le assegnazioni di accesso toolist per amministratore classico sottoscrizione hello e coadministrators, utilizzare:

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a>Concedere l'accesso
### <a name="search-for-object-ids"></a>Cercare gli ID oggetto
tooassign un ruolo, è necessario tooidentify oggetti hello (utente, gruppo o applicazione) e ambito hello.

Se non si conosce l'ID sottoscrizione hello, sarà possibile trovarlo in hello **sottoscrizioni** pannello nel portale di Azure hello. toolearn tooquery per l'ID sottoscrizione hello, vedere [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) su MSDN.

ID di oggetto hello tooget per un gruppo di Azure AD, usare:

    Get-AzureRmADGroup -SearchString <group name in quotes>

ID di oggetto hello tooget per un'entità servizio di Azure AD o l'applicazione, utilizzare:

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Assegnare un'applicazione tooan ruolo nell'ambito di sottoscrizione hello
applicazione di tooan toogrant accesso all'ambito della sottoscrizione hello, utilizzare:

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![Controllo degli accessi in base al ruolo di PowerShell - New-AzureRmRoleAssignment - Schermata](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Assegnare un utente tooa ruolo nell'ambito del gruppo di risorse hello
toogrant accesso tooa utente nell'ambito di gruppo di risorse hello, utilizzare:

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![Controllo degli accessi in base al ruolo di PowerShell - New-AzureRmRoleAssignment - Schermata](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Assegnare un gruppo di tooa ruolo nell'ambito di risorsa hello
gruppo di tooa toogrant accesso nell'ambito di risorsa hello, utilizzare:

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![Controllo degli accessi in base al ruolo di PowerShell - New-AzureRmRoleAssignment - Schermata](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a>Rimuovere un accesso
tooremove l'accesso per l'utilizzo di applicazioni, utenti e gruppi:

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![Controllo degli accessi in base al ruolo di PowerShell - Remove-AzureRmRoleAssignment - Schermata](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a>Creare un ruolo personalizzato
toocreate un ruolo personalizzato, utilizzare hello ```New-AzureRmRoleDefinition``` comando. Sono disponibili due metodi di strutturazione ruolo hello, utilizzare PSRoleDefinitionObject o un modello JSON. 

## <a name="get-actions-for-a-resource-provider"></a>Ottenere le azioni per un provider di risorse
Quando si crea ruoli personalizzati da zero, è importante tooknow tutti hello possibili operazioni dai provider di risorse hello.
Hello utilizzare ```Get-AzureRMProviderOperation``` comando tooget queste informazioni.
Ad esempio, se si desidera toocheck tutte le operazioni disponibili hello per la macchina virtuale utilizzano questo comando:

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a>Creare un ruolo con PSRoleDefinitionObject
Quando si usa PowerShell toocreate un ruolo personalizzato, è possibile iniziare da zero o uno di hello [ruoli predefiniti](role-based-access-built-in-roles.md) come punto di partenza. esempio Hello in questa sezione inizia con un ruolo incorporato e quindi si Personalizza con più privilegi. Modifica hello tooadd gli attributi di hello *azioni*, *notActions*, o *ambiti* desiderato e quindi salvare le modifiche di hello come un nuovo ruolo.

Hello esempio seguente viene avviato con hello *collaboratore alla macchina virtuale* ruolo e utilizza tale toocreate un ruolo personalizzato chiamato *operatore macchina virtuale*. nuovo ruolo Hello concede accesso tooall leggere le operazioni di *Microsoft. COMPUTE*, *Microsoft.Storage*, e *Network* provider e concede l'accesso alla risorsa toostart, riavviare e monitorare le macchine virtuali. ruolo personalizzata Hello può essere utilizzato in due sottoscrizioni.

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Contributor"
$role.Id = $null
$role.Name = "Virtual Machine Operator"
$role.Description = "Can monitor and restart virtual machines."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/*/read")
$role.Actions.Add("Microsoft.Network/*/read")
$role.Actions.Add("Microsoft.Compute/*/read")
$role.Actions.Add("Microsoft.Compute/virtualMachines/start/action")
$role.Actions.Add("Microsoft.Compute/virtualMachines/restart/action")
$role.Actions.Add("Microsoft.Authorization/*/read")
$role.Actions.Add("Microsoft.Resources/subscriptions/resourceGroups/read")
$role.Actions.Add("Microsoft.Insights/alertRules/*")
$role.Actions.Add("Microsoft.Support/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e")
$role.AssignableScopes.Add("/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624")
New-AzureRmRoleDefinition -Role $role
```

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/2-new-azurermroledefinition.png)

### <a name="create-role-with-json-template"></a>Creare un ruolo con il modello JSON
Un modello JSON può essere utilizzato come definizione dell'origine hello per ruolo personalizzata hello. esempio Hello crea un ruolo personalizzato che consente l'accesso in lettura toostorage e le risorse di calcolo, accedere toosupport e aggiunge tale ruolo tootwo sottoscrizioni. Creare un nuovo file `C:\CustomRoles\customrole1.json` con hello di esempio seguente. Hello Id deve essere impostato troppo`null` durante la creazione di un ruolo iniziale come un nuovo ID viene generato automaticamente. 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```
tooadd hello ruolo toohello sottoscrizioni, eseguire il comando PowerShell seguente hello:
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a>Modificare un ruolo personalizzato
Toocreating simile, un ruolo personalizzato, è possibile modificare un ruolo personalizzato esistente utilizza PSRoleDefinitionObject hello o un modello JSON.

### <a name="modify-role-with-psroledefinitionobject"></a>Modificare un ruolo con PSRoleDefinitionObject
toomodify un ruolo personalizzato, utilizzare innanzitutto hello `Get-AzureRmRoleDefinition` la definizione di ruolo hello tooretrieve del comando. In secondo luogo, apportare le modifiche desiderata hello toohello definizione di ruolo. Infine, utilizzare hello `Set-AzureRmRoleDefinition` hello toosave comando Modifica definizione di ruolo.

esempio Hello aggiunge hello `Microsoft.Insights/diagnosticSettings/*` operazione toohello *operatore macchina virtuale* ruolo personalizzato.

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![Controllo degli accessi in base al ruolo di PowerShell - Set-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

esempio Hello aggiunge una sottoscrizione di Azure toohello gli ambiti assegnabili di hello *operatore macchina virtuale* ruolo personalizzato.

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![Controllo degli accessi in base al ruolo di PowerShell - Set-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a>Modificare un ruolo con il modello JSON
Modello hello precedente JSON, è possibile modificare un tooadd ruolo personalizzato esistente o rimuovere le azioni. Aggiorna modello JSON hello e aggiungere hello azione di lettura per la rete, come illustrato nell'esempio seguente hello. le definizioni di Hello elencate nel modello di hello non sono definizione esistente tooan applicato in modo cumulativo, vale a dire che viene visualizzata tale ruolo hello esattamente come specificato nel modello di hello. È inoltre necessario tooupdate hello Id campo ID hello del ruolo hello. Se non si è certi che cos'è questo valore, è possibile utilizzare hello `Get-AzureRmRoleDefinition` tooget cmdlet queste informazioni.

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```

tooupdate hello ruolo esistente, eseguire il comando PowerShell seguente hello:
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a>Eliminare un ruolo personalizzato
toodelete un ruolo personalizzato, utilizzare hello `Remove-AzureRmRoleDefinition` comando.

esempio Hello rimuove hello *operatore macchina virtuale* ruolo personalizzato.

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![Controllo degli accessi in base al ruolo di PowerShell - Remove-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a>Elencare ruoli personalizzati
i ruoli di hello toolist che sono disponibili per l'assegnazione a un ambito, usano hello `Get-AzureRmRoleDefinition` comando.

Hello di esempio seguente vengono elencati tutti i ruoli che sono disponibili per l'assegnazione nella sottoscrizione hello selezionato.

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

Nell'esempio seguente di hello, hello *operatore macchina virtuale* ruolo personalizzato non è disponibile in hello *Production4* sottoscrizione perché tale sottoscrizione non è in hello  **AssignableScopes** del ruolo hello.

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a>Vedere anche
* [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)] (Uso di Azure PowerShell con Azure Resource Manager)

