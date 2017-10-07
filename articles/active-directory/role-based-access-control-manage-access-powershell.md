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
# <a name="manage-role-based-access-control-with-azure-powershell"></a><span data-ttu-id="dc6e1-103">Gestire il controllo degli accessi in base al ruolo con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc6e1-103">Manage Role-Based Access Control with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dc6e1-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc6e1-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="dc6e1-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="dc6e1-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="dc6e1-106">API REST</span><span class="sxs-lookup"><span data-stu-id="dc6e1-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="dc6e1-107">Controllo di accesso basato sui ruoli (RBAC) è possibile utilizzare in hello portale di Azure e sottoscrizione tooyour di API di gestione risorse di Azure toomanage accesso a un livello con granularità fine.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Management API toomanage access tooyour subscription at a fine-grained level.</span></span> <span data-ttu-id="dc6e1-108">Con questa funzionalità, è possibile concedere l'accesso per utenti, gruppi o entità servizio Active Directory assegnando toothem alcuni ruoli a un particolare ambito.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="dc6e1-109">Prima di poter utilizzare PowerShell toomanage RBAC, è necessario hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="dc6e1-109">Before you can use PowerShell toomanage RBAC, you need hello following prerequisites:</span></span>

* <span data-ttu-id="dc6e1-110">Azure PowerShell 0.8.8 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-110">Azure PowerShell version 0.8.8 or later.</span></span> <span data-ttu-id="dc6e1-111">versione più recente di tooinstall hello e associare con la sottoscrizione di Azure, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dc6e1-111">tooinstall hello latest version and associate it with your Azure subscription, see [how tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="dc6e1-112">Cmdlet di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dc6e1-112">Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="dc6e1-113">Installare hello [i cmdlet di Azure Resource Manager](/powershell/azure/overview) in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-113">Install hello [Azure Resource Manager cmdlets](/powershell/azure/overview) in PowerShell.</span></span>

## <a name="list-roles"></a><span data-ttu-id="dc6e1-114">Elenco dei ruoli</span><span class="sxs-lookup"><span data-stu-id="dc6e1-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="dc6e1-115">Elencare tutti i ruoli disponibili</span><span class="sxs-lookup"><span data-stu-id="dc6e1-115">List all available roles</span></span>
<span data-ttu-id="dc6e1-116">ruoli RBAC toolist disponibili per l'assegnazione e tooinspect hello operazioni toowhich concedere l'accesso, utilizzare `Get-AzureRmRoleDefinition`.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-116">toolist RBAC roles that are available for assignment and tooinspect hello operations toowhich they grant access, use `Get-AzureRmRoleDefinition`.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="dc6e1-118">Elencare le azioni di un ruolo</span><span class="sxs-lookup"><span data-stu-id="dc6e1-118">List actions of a role</span></span>
<span data-ttu-id="dc6e1-119">le azioni di hello toolist per un ruolo specifico, utilizzare `Get-AzureRmRoleDefinition <role name>`.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-119">toolist hello actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span></span>

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition per un ruolo specifico - Schermata](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a><span data-ttu-id="dc6e1-121">Assegnazioni di accesso</span><span class="sxs-lookup"><span data-stu-id="dc6e1-121">See who has access</span></span>
<span data-ttu-id="dc6e1-122">utilizzare assegnazioni di accesso RBAC toolist, `Get-AzureRmRoleAssignment`.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-122">toolist RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span></span>

### <a name="list-role-assignments-at-a-specific-scope"></a><span data-ttu-id="dc6e1-123">Elencare le assegnazioni di ruolo in un ambito specifico</span><span class="sxs-lookup"><span data-stu-id="dc6e1-123">List role assignments at a specific scope</span></span>
<span data-ttu-id="dc6e1-124">È possibile visualizzare tutte le assegnazioni di accesso hello per una sottoscrizione specificata, un gruppo di risorse o una risorsa.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-124">You can see all hello access assignments for a specified subscription, resource group, or resource.</span></span> <span data-ttu-id="dc6e1-125">Ad esempio, toosee hello tutte le assegnazioni active hello per un gruppo di risorse, utilizzare `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-125">For example, toosee hello all hello active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span></span>

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition per un gruppo di risorse - Schermata](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a><span data-ttu-id="dc6e1-127">Elenco ruoli assegnati tooa utente</span><span class="sxs-lookup"><span data-stu-id="dc6e1-127">List roles assigned tooa user</span></span>
<span data-ttu-id="dc6e1-128">toolist tutti i ruoli di hello assegnati tooa specificato utente e ruoli hello che sono assegnati dei gruppi toohello toowhich hello utente appartiene, utilizzare `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-128">toolist all hello roles that are assigned tooa specified user and hello roles that are assigned toohello groups toowhich hello user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span></span>

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition per un utente - Schermata](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a><span data-ttu-id="dc6e1-130">Elencare le assegnazioni di ruoli per l'amministratore e i coamministratori del servizio classici</span><span class="sxs-lookup"><span data-stu-id="dc6e1-130">List classic service administrator and coadmin role assignments</span></span>
<span data-ttu-id="dc6e1-131">le assegnazioni di accesso toolist per amministratore classico sottoscrizione hello e coadministrators, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="dc6e1-131">toolist access assignments for hello classic subscription administrator and coadministrators, use:</span></span>

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a><span data-ttu-id="dc6e1-132">Concedere l'accesso</span><span class="sxs-lookup"><span data-stu-id="dc6e1-132">Grant access</span></span>
### <a name="search-for-object-ids"></a><span data-ttu-id="dc6e1-133">Cercare gli ID oggetto</span><span class="sxs-lookup"><span data-stu-id="dc6e1-133">Search for object IDs</span></span>
<span data-ttu-id="dc6e1-134">tooassign un ruolo, è necessario tooidentify oggetti hello (utente, gruppo o applicazione) e ambito hello.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-134">tooassign a role, you need tooidentify both hello object (user, group, or application) and hello scope.</span></span>

<span data-ttu-id="dc6e1-135">Se non si conosce l'ID sottoscrizione hello, sarà possibile trovarlo in hello **sottoscrizioni** pannello nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-135">If you don't know hello subscription ID, you can find it in hello **Subscriptions** blade on hello Azure portal.</span></span> <span data-ttu-id="dc6e1-136">toolearn tooquery per l'ID sottoscrizione hello, vedere [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) su MSDN.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-136">toolearn how tooquery for hello subscription ID, see [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) on MSDN.</span></span>

<span data-ttu-id="dc6e1-137">ID di oggetto hello tooget per un gruppo di Azure AD, usare:</span><span class="sxs-lookup"><span data-stu-id="dc6e1-137">tooget hello object ID for an Azure AD group, use:</span></span>

    Get-AzureRmADGroup -SearchString <group name in quotes>

<span data-ttu-id="dc6e1-138">ID di oggetto hello tooget per un'entità servizio di Azure AD o l'applicazione, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="dc6e1-138">tooget hello object ID for an Azure AD service principal or application, use:</span></span>

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="dc6e1-139">Assegnare un'applicazione tooan ruolo nell'ambito di sottoscrizione hello</span><span class="sxs-lookup"><span data-stu-id="dc6e1-139">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="dc6e1-140">applicazione di tooan toogrant accesso all'ambito della sottoscrizione hello, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="dc6e1-140">toogrant access tooan application at hello subscription scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![Controllo degli accessi in base al ruolo di PowerShell - New-AzureRmRoleAssignment - Schermata](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="dc6e1-142">Assegnare un utente tooa ruolo nell'ambito del gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="dc6e1-142">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="dc6e1-143">toogrant accesso tooa utente nell'ambito di gruppo di risorse hello, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="dc6e1-143">toogrant access tooa user at hello resource group scope, use:</span></span>

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![Controllo degli accessi in base al ruolo di PowerShell - New-AzureRmRoleAssignment - Schermata](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="dc6e1-145">Assegnare un gruppo di tooa ruolo nell'ambito di risorsa hello</span><span class="sxs-lookup"><span data-stu-id="dc6e1-145">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="dc6e1-146">gruppo di tooa toogrant accesso nell'ambito di risorsa hello, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="dc6e1-146">toogrant access tooa group at hello resource scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![Controllo degli accessi in base al ruolo di PowerShell - New-AzureRmRoleAssignment - Schermata](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a><span data-ttu-id="dc6e1-148">Rimuovere un accesso</span><span class="sxs-lookup"><span data-stu-id="dc6e1-148">Remove access</span></span>
<span data-ttu-id="dc6e1-149">tooremove l'accesso per l'utilizzo di applicazioni, utenti e gruppi:</span><span class="sxs-lookup"><span data-stu-id="dc6e1-149">tooremove access for users, groups, and applications, use:</span></span>

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![Controllo degli accessi in base al ruolo di PowerShell - Remove-AzureRmRoleAssignment - Schermata](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="dc6e1-151">Creare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="dc6e1-151">Create a custom role</span></span>
<span data-ttu-id="dc6e1-152">toocreate un ruolo personalizzato, utilizzare hello ```New-AzureRmRoleDefinition``` comando.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-152">toocreate a custom role, use hello ```New-AzureRmRoleDefinition``` command.</span></span> <span data-ttu-id="dc6e1-153">Sono disponibili due metodi di strutturazione ruolo hello, utilizzare PSRoleDefinitionObject o un modello JSON.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-153">There are two methods of structuring hello role, using PSRoleDefinitionObject or a JSON template.</span></span> 

## <a name="get-actions-for-a-resource-provider"></a><span data-ttu-id="dc6e1-154">Ottenere le azioni per un provider di risorse</span><span class="sxs-lookup"><span data-stu-id="dc6e1-154">Get Actions for a Resource Provider</span></span>
<span data-ttu-id="dc6e1-155">Quando si crea ruoli personalizzati da zero, è importante tooknow tutti hello possibili operazioni dai provider di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-155">When You are creating custom roles from scratch, it is important tooknow all hello possible operations from hello resource providers.</span></span>
<span data-ttu-id="dc6e1-156">Hello utilizzare ```Get-AzureRMProviderOperation``` comando tooget queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-156">Use hello ```Get-AzureRMProviderOperation``` command tooget this information.</span></span>
<span data-ttu-id="dc6e1-157">Ad esempio, se si desidera toocheck tutte le operazioni disponibili hello per la macchina virtuale utilizzano questo comando:</span><span class="sxs-lookup"><span data-stu-id="dc6e1-157">For example, if you want toocheck all hello available operations for virtual Machine use this command:</span></span>

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a><span data-ttu-id="dc6e1-158">Creare un ruolo con PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="dc6e1-158">Create role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="dc6e1-159">Quando si usa PowerShell toocreate un ruolo personalizzato, è possibile iniziare da zero o uno di hello [ruoli predefiniti](role-based-access-built-in-roles.md) come punto di partenza.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-159">When you use PowerShell toocreate a custom role, you can start from scratch or use one of hello [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span></span> <span data-ttu-id="dc6e1-160">esempio Hello in questa sezione inizia con un ruolo incorporato e quindi si Personalizza con più privilegi.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-160">hello example in this section starts with a built-in role and then customizes it with more privileges.</span></span> <span data-ttu-id="dc6e1-161">Modifica hello tooadd gli attributi di hello *azioni*, *notActions*, o *ambiti* desiderato e quindi salvare le modifiche di hello come un nuovo ruolo.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-161">Edit hello attributes tooadd hello *Actions*, *notActions*, or *scopes* that you want, and then save hello changes as a new role.</span></span>

<span data-ttu-id="dc6e1-162">Hello esempio seguente viene avviato con hello *collaboratore alla macchina virtuale* ruolo e utilizza tale toocreate un ruolo personalizzato chiamato *operatore macchina virtuale*.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-162">hello following example starts with hello *Virtual Machine Contributor* role and uses that toocreate a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="dc6e1-163">nuovo ruolo Hello concede accesso tooall leggere le operazioni di *Microsoft. COMPUTE*, *Microsoft.Storage*, e *Network* provider e concede l'accesso alla risorsa toostart, riavviare e monitorare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-163">hello new role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="dc6e1-164">ruolo personalizzata Hello può essere utilizzato in due sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-164">hello custom role can be used in two subscriptions.</span></span>

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

### <a name="create-role-with-json-template"></a><span data-ttu-id="dc6e1-166">Creare un ruolo con il modello JSON</span><span class="sxs-lookup"><span data-stu-id="dc6e1-166">Create role with JSON template</span></span>
<span data-ttu-id="dc6e1-167">Un modello JSON può essere utilizzato come definizione dell'origine hello per ruolo personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-167">A JSON template can be used as hello source definition for hello custom role.</span></span> <span data-ttu-id="dc6e1-168">esempio Hello crea un ruolo personalizzato che consente l'accesso in lettura toostorage e le risorse di calcolo, accedere toosupport e aggiunge tale ruolo tootwo sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-168">hello following example creates a custom role that allows read access toostorage and compute resources, access toosupport, and adds that role tootwo subscriptions.</span></span> <span data-ttu-id="dc6e1-169">Creare un nuovo file `C:\CustomRoles\customrole1.json` con hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-169">Create a new file `C:\CustomRoles\customrole1.json` with hello following example.</span></span> <span data-ttu-id="dc6e1-170">Hello Id deve essere impostato troppo`null` durante la creazione di un ruolo iniziale come un nuovo ID viene generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-170">hello Id should be set too`null` on initial role creation as a new ID is generated automatically.</span></span> 

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
<span data-ttu-id="dc6e1-171">tooadd hello ruolo toohello sottoscrizioni, eseguire il comando PowerShell seguente hello:</span><span class="sxs-lookup"><span data-stu-id="dc6e1-171">tooadd hello role toohello subscriptions, run hello following PowerShell command:</span></span>
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a><span data-ttu-id="dc6e1-172">Modificare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="dc6e1-172">Modify a custom role</span></span>
<span data-ttu-id="dc6e1-173">Toocreating simile, un ruolo personalizzato, è possibile modificare un ruolo personalizzato esistente utilizza PSRoleDefinitionObject hello o un modello JSON.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-173">Similar toocreating a custom role, you can modify an existing custom role using either hello PSRoleDefinitionObject or a JSON template.</span></span>

### <a name="modify-role-with-psroledefinitionobject"></a><span data-ttu-id="dc6e1-174">Modificare un ruolo con PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="dc6e1-174">Modify role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="dc6e1-175">toomodify un ruolo personalizzato, utilizzare innanzitutto hello `Get-AzureRmRoleDefinition` la definizione di ruolo hello tooretrieve del comando.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-175">toomodify a custom role, first, use hello `Get-AzureRmRoleDefinition` command tooretrieve hello role definition.</span></span> <span data-ttu-id="dc6e1-176">In secondo luogo, apportare le modifiche desiderata hello toohello definizione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-176">Second, make hello desired changes toohello role definition.</span></span> <span data-ttu-id="dc6e1-177">Infine, utilizzare hello `Set-AzureRmRoleDefinition` hello toosave comando Modifica definizione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-177">Finally, use hello `Set-AzureRmRoleDefinition` command toosave hello modified role definition.</span></span>

<span data-ttu-id="dc6e1-178">esempio Hello aggiunge hello `Microsoft.Insights/diagnosticSettings/*` operazione toohello *operatore macchina virtuale* ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-178">hello following example adds hello `Microsoft.Insights/diagnosticSettings/*` operation toohello *Virtual Machine Operator* custom role.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![Controllo degli accessi in base al ruolo di PowerShell - Set-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

<span data-ttu-id="dc6e1-180">esempio Hello aggiunge una sottoscrizione di Azure toohello gli ambiti assegnabili di hello *operatore macchina virtuale* ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-180">hello following example adds an Azure subscription toohello assignable scopes of hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![Controllo degli accessi in base al ruolo di PowerShell - Set-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a><span data-ttu-id="dc6e1-182">Modificare un ruolo con il modello JSON</span><span class="sxs-lookup"><span data-stu-id="dc6e1-182">Modify role with JSON template</span></span>
<span data-ttu-id="dc6e1-183">Modello hello precedente JSON, è possibile modificare un tooadd ruolo personalizzato esistente o rimuovere le azioni.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-183">Using hello previous JSON template, you can easily modify an existing custom role tooadd or remove Actions.</span></span> <span data-ttu-id="dc6e1-184">Aggiorna modello JSON hello e aggiungere hello azione di lettura per la rete, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-184">Update hello JSON template and add hello read action for networking as shown in hello following example.</span></span> <span data-ttu-id="dc6e1-185">le definizioni di Hello elencate nel modello di hello non sono definizione esistente tooan applicato in modo cumulativo, vale a dire che viene visualizzata tale ruolo hello esattamente come specificato nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-185">hello definitions listed in hello template are not cumulatively applied tooan existing definition, meaning that hello role appears exactly as you specify in hello template.</span></span> <span data-ttu-id="dc6e1-186">È inoltre necessario tooupdate hello Id campo ID hello del ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-186">You also need tooupdate hello Id field with hello ID of hello role.</span></span> <span data-ttu-id="dc6e1-187">Se non si è certi che cos'è questo valore, è possibile utilizzare hello `Get-AzureRmRoleDefinition` tooget cmdlet queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-187">If you aren't sure what this value is, you can use hello `Get-AzureRmRoleDefinition` cmdlet tooget this information.</span></span>

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

<span data-ttu-id="dc6e1-188">tooupdate hello ruolo esistente, eseguire il comando PowerShell seguente hello:</span><span class="sxs-lookup"><span data-stu-id="dc6e1-188">tooupdate hello existing role, run hello following PowerShell command:</span></span>
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a><span data-ttu-id="dc6e1-189">Eliminare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="dc6e1-189">Delete a custom role</span></span>
<span data-ttu-id="dc6e1-190">toodelete un ruolo personalizzato, utilizzare hello `Remove-AzureRmRoleDefinition` comando.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-190">toodelete a custom role, use hello `Remove-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="dc6e1-191">esempio Hello rimuove hello *operatore macchina virtuale* ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-191">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![Controllo degli accessi in base al ruolo di PowerShell - Remove-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a><span data-ttu-id="dc6e1-193">Elencare ruoli personalizzati</span><span class="sxs-lookup"><span data-stu-id="dc6e1-193">List custom roles</span></span>
<span data-ttu-id="dc6e1-194">i ruoli di hello toolist che sono disponibili per l'assegnazione a un ambito, usano hello `Get-AzureRmRoleDefinition` comando.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-194">toolist hello roles that are available for assignment at a scope, use hello `Get-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="dc6e1-195">Hello di esempio seguente vengono elencati tutti i ruoli che sono disponibili per l'assegnazione nella sottoscrizione hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-195">hello following example lists all roles that are available for assignment in hello selected subscription.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

<span data-ttu-id="dc6e1-197">Nell'esempio seguente di hello, hello *operatore macchina virtuale* ruolo personalizzato non è disponibile in hello *Production4* sottoscrizione perché tale sottoscrizione non è in hello  **AssignableScopes** del ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="dc6e1-197">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a><span data-ttu-id="dc6e1-199">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="dc6e1-199">See also</span></span>
* <span data-ttu-id="dc6e1-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)] (Uso di Azure PowerShell con Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="dc6e1-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span></span>

