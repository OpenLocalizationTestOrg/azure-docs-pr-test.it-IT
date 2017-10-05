---
title: Gestire il controllo degli accessi in base al ruolo con Azure PowerShell | Documentazione Microsoft
description: Come gestire il controllo degli accessi in base al ruolo con Azure PowerShell, come elencare ruoli, assegnare ruoli ed eliminare assegnazioni di ruoli.
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
ms.openlocfilehash: d7b11df21650b5cb27f9c3dd8306f8d12664185e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a><span data-ttu-id="800aa-103">Gestire il controllo degli accessi in base al ruolo con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="800aa-103">Manage Role-Based Access Control with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="800aa-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="800aa-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="800aa-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="800aa-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="800aa-106">API REST</span><span class="sxs-lookup"><span data-stu-id="800aa-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="800aa-107">È possibile usare il controllo degli accessi in base al ruolo (RBAC) nel portale di Azure e nell'API di Azure Resource Manager per gestire con estrema precisione l'accesso alla propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="800aa-107">You can use Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Management API to manage access to your subscription at a fine-grained level.</span></span> <span data-ttu-id="800aa-108">Con questa funzionalità è possibile concedere l'accesso a utenti, gruppi o entità servizio di Active Directory assegnando loro dei ruoli in un determinato ambito.</span><span class="sxs-lookup"><span data-stu-id="800aa-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

<span data-ttu-id="800aa-109">Prima di usare PowerShell per gestire il controllo degli accessi in base al ruolo, è necessario avere i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="800aa-109">Before you can use PowerShell to manage RBAC, you need the following prerequisites:</span></span>

* <span data-ttu-id="800aa-110">Azure PowerShell 0.8.8 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="800aa-110">Azure PowerShell version 0.8.8 or later.</span></span> <span data-ttu-id="800aa-111">Per installare la versione più recente e associarla alla sottoscrizione di Azure, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="800aa-111">To install the latest version and associate it with your Azure subscription, see [how to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="800aa-112">Cmdlet di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="800aa-112">Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="800aa-113">Installare i [cmdlet di Azure Resource Manager](/powershell/azure/overview) in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="800aa-113">Install the [Azure Resource Manager cmdlets](/powershell/azure/overview) in PowerShell.</span></span>

## <a name="list-roles"></a><span data-ttu-id="800aa-114">Elenco dei ruoli</span><span class="sxs-lookup"><span data-stu-id="800aa-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="800aa-115">Elencare tutti i ruoli disponibili</span><span class="sxs-lookup"><span data-stu-id="800aa-115">List all available roles</span></span>
<span data-ttu-id="800aa-116">Per elencare i ruoli del controllo degli accessi in base al ruolo disponibili per l'assegnazione e controllare le operazioni a cui concedono l'accesso, usare `Get-AzureRmRoleDefinition`.</span><span class="sxs-lookup"><span data-stu-id="800aa-116">To list RBAC roles that are available for assignment and to inspect the operations to which they grant access, use `Get-AzureRmRoleDefinition`.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="800aa-118">Elencare le azioni di un ruolo</span><span class="sxs-lookup"><span data-stu-id="800aa-118">List actions of a role</span></span>
<span data-ttu-id="800aa-119">Per elencare le azioni per un ruolo specifico, usare `Get-AzureRmRoleDefinition <role name>`.</span><span class="sxs-lookup"><span data-stu-id="800aa-119">To list the actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span></span>

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition per un ruolo specifico - Schermata](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a><span data-ttu-id="800aa-121">Assegnazioni di accesso</span><span class="sxs-lookup"><span data-stu-id="800aa-121">See who has access</span></span>
<span data-ttu-id="800aa-122">Per elencare le assegnazioni di accesso al controllo degli accessi in base al ruolo, usare `Get-AzureRmRoleAssignment`.</span><span class="sxs-lookup"><span data-stu-id="800aa-122">To list RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span></span>

### <a name="list-role-assignments-at-a-specific-scope"></a><span data-ttu-id="800aa-123">Elencare le assegnazioni di ruolo in un ambito specifico</span><span class="sxs-lookup"><span data-stu-id="800aa-123">List role assignments at a specific scope</span></span>
<span data-ttu-id="800aa-124">È possibile elencare le assegnazioni di accesso in base a sottoscrizione, gruppo di risorse o risorsa specificati.</span><span class="sxs-lookup"><span data-stu-id="800aa-124">You can see all the access assignments for a specified subscription, resource group, or resource.</span></span> <span data-ttu-id="800aa-125">Ad esempio, per elencare tutte le assegnazioni attive per un gruppo di risorse, usare `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span><span class="sxs-lookup"><span data-stu-id="800aa-125">For example, to see the all the active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span></span>

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition per un gruppo di risorse - Schermata](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-to-a-user"></a><span data-ttu-id="800aa-127">Elencare i ruoli assegnati ad un utente</span><span class="sxs-lookup"><span data-stu-id="800aa-127">List roles assigned to a user</span></span>
<span data-ttu-id="800aa-128">Per elencare tutti i ruoli assegnati a un utente specifico e i ruoli assegnati ai gruppi a cui appartiene l'utente, usare `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span><span class="sxs-lookup"><span data-stu-id="800aa-128">To list all the roles that are assigned to a specified user and the roles that are assigned to the groups to which the user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span></span>

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition per un utente - Schermata](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a><span data-ttu-id="800aa-130">Elencare le assegnazioni di ruoli per l'amministratore e i coamministratori del servizio classici</span><span class="sxs-lookup"><span data-stu-id="800aa-130">List classic service administrator and coadmin role assignments</span></span>
<span data-ttu-id="800aa-131">Per elencare le assegnazioni dell'accesso per l'amministratore e i coamministratori della sottoscrizione classici, usare:</span><span class="sxs-lookup"><span data-stu-id="800aa-131">To list access assignments for the classic subscription administrator and coadministrators, use:</span></span>

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a><span data-ttu-id="800aa-132">Concedere l'accesso</span><span class="sxs-lookup"><span data-stu-id="800aa-132">Grant access</span></span>
### <a name="search-for-object-ids"></a><span data-ttu-id="800aa-133">Cercare gli ID oggetto</span><span class="sxs-lookup"><span data-stu-id="800aa-133">Search for object IDs</span></span>
<span data-ttu-id="800aa-134">Per assegnare un ruolo, è necessario identificare l'oggetto (utente, gruppo o applicazione) e l'ambito.</span><span class="sxs-lookup"><span data-stu-id="800aa-134">To assign a role, you need to identify both the object (user, group, or application) and the scope.</span></span>

<span data-ttu-id="800aa-135">Se non si conosce l'ID sottoscrizione, è possibile reperire tale informazione nel pannello **Sottoscrizioni** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="800aa-135">If you don't know the subscription ID, you can find it in the **Subscriptions** blade on the Azure portal.</span></span> <span data-ttu-id="800aa-136">Per informazioni su come eseguire una query per l'ID della sottoscrizione,vedere [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) (Get-AzureSubscription) in MSDN.</span><span class="sxs-lookup"><span data-stu-id="800aa-136">To learn how to query for the subscription ID, see [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) on MSDN.</span></span>

<span data-ttu-id="800aa-137">Per ottenere l'ID oggetto per un gruppo di Azure AD, usare:</span><span class="sxs-lookup"><span data-stu-id="800aa-137">To get the object ID for an Azure AD group, use:</span></span>

    Get-AzureRmADGroup -SearchString <group name in quotes>

<span data-ttu-id="800aa-138">Per ottenere l'ID oggetto per un'entità servizio di Azure AD o applicazione, usare:</span><span class="sxs-lookup"><span data-stu-id="800aa-138">To get the object ID for an Azure AD service principal or application, use:</span></span>

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-to-an-application-at-the-subscription-scope"></a><span data-ttu-id="800aa-139">Assegnare un ruolo a un'applicazione nell'ambito della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="800aa-139">Assign a role to an application at the subscription scope</span></span>
<span data-ttu-id="800aa-140">Per concedere l'accesso a un'applicazione nell'ambito della sottoscrizione, usare:</span><span class="sxs-lookup"><span data-stu-id="800aa-140">To grant access to an application at the subscription scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![Controllo degli accessi in base al ruolo di PowerShell - New-AzureRmRoleAssignment - Schermata](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-to-a-user-at-the-resource-group-scope"></a><span data-ttu-id="800aa-142">Assegnare un ruolo a un utente nell'ambito di un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="800aa-142">Assign a role to a user at the resource group scope</span></span>
<span data-ttu-id="800aa-143">Per concedere l'accesso a un utente nell'ambito di un gruppo di risorse, usare:</span><span class="sxs-lookup"><span data-stu-id="800aa-143">To grant access to a user at the resource group scope, use:</span></span>

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![Controllo degli accessi in base al ruolo di PowerShell - New-AzureRmRoleAssignment - Schermata](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-to-a-group-at-the-resource-scope"></a><span data-ttu-id="800aa-145">Assegnare un ruolo a un gruppo nell'ambito delle risorse</span><span class="sxs-lookup"><span data-stu-id="800aa-145">Assign a role to a group at the resource scope</span></span>
<span data-ttu-id="800aa-146">Per concedere l'accesso a un gruppo nell'ambito delle risorse, usare:</span><span class="sxs-lookup"><span data-stu-id="800aa-146">To grant access to a group at the resource scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![Controllo degli accessi in base al ruolo di PowerShell - New-AzureRmRoleAssignment - Schermata](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a><span data-ttu-id="800aa-148">Rimuovere un accesso</span><span class="sxs-lookup"><span data-stu-id="800aa-148">Remove access</span></span>
<span data-ttu-id="800aa-149">Per rimuovere l'accesso per utenti, gruppi e applicazioni, usare:</span><span class="sxs-lookup"><span data-stu-id="800aa-149">To remove access for users, groups, and applications, use:</span></span>

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![Controllo degli accessi in base al ruolo di PowerShell - Remove-AzureRmRoleAssignment - Schermata](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="800aa-151">Creare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="800aa-151">Create a custom role</span></span>
<span data-ttu-id="800aa-152">Per creare un ruolo personalizzato, usare il comando ```New-AzureRmRoleDefinition``` .</span><span class="sxs-lookup"><span data-stu-id="800aa-152">To create a custom role, use the ```New-AzureRmRoleDefinition``` command.</span></span> <span data-ttu-id="800aa-153">Esistono due metodi per strutturare il ruolo, usare PSRoleDefinitionObject o un modello JSON.</span><span class="sxs-lookup"><span data-stu-id="800aa-153">There are two methods of structuring the role, using PSRoleDefinitionObject or a JSON template.</span></span> 

## <a name="get-actions-for-a-resource-provider"></a><span data-ttu-id="800aa-154">Ottenere le azioni per un provider di risorse</span><span class="sxs-lookup"><span data-stu-id="800aa-154">Get Actions for a Resource Provider</span></span>
<span data-ttu-id="800aa-155">Quando si creano ruoli personalizzati da zero, è importante conoscere tutte le operazioni possibili dei provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="800aa-155">When You are creating custom roles from scratch, it is important to know all the possible operations from the resource providers.</span></span>
<span data-ttu-id="800aa-156">Utilizzare il comando ```Get-AzureRMProviderOperation``` per ottenere queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="800aa-156">Use the ```Get-AzureRMProviderOperation``` command to get this information.</span></span>
<span data-ttu-id="800aa-157">Ad esempio, se si desidera controllare tutte le operazioni disponibili per la macchina virtuale usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="800aa-157">For example, if you want to check all the available operations for virtual Machine use this command:</span></span>

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a><span data-ttu-id="800aa-158">Creare un ruolo con PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="800aa-158">Create role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="800aa-159">Quando si crea un ruolo personalizzato con PowerShell, è possibile iniziare da zero o usare uno dei [ruoli predefiniti](role-based-access-built-in-roles.md) come punto di partenza.</span><span class="sxs-lookup"><span data-stu-id="800aa-159">When you use PowerShell to create a custom role, you can start from scratch or use one of the [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span></span> <span data-ttu-id="800aa-160">Nell'esempio riportato in questa sezione si inizia con un ruolo predefinito e quindi lo si personalizza con più privilegi.</span><span class="sxs-lookup"><span data-stu-id="800aa-160">The example in this section starts with a built-in role and then customizes it with more privileges.</span></span> <span data-ttu-id="800aa-161">Modificare gli attributi e aggiungere gli attributi *Actions*, *notActions* o *scopes* desiderati e quindi salvare le modifiche come nuovo ruolo.</span><span class="sxs-lookup"><span data-stu-id="800aa-161">Edit the attributes to add the *Actions*, *notActions*, or *scopes* that you want, and then save the changes as a new role.</span></span>

<span data-ttu-id="800aa-162">L'esempio seguente inizia con il ruolo *Virtual Machine Contributor* e lo usa per creare un ruolo personalizzato denominato *Virtual Machine Operator*.</span><span class="sxs-lookup"><span data-stu-id="800aa-162">The following example starts with the *Virtual Machine Contributor* role and uses that to create a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="800aa-163">Il nuovo ruolo concede l'accesso a tutte le operazioni di lettura dei provider di risorse *Microsoft.Compute*, *Microsoft.Storage* e *Microsoft.Network* e concede l'accesso per avviare, riavviare e monitorare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="800aa-163">The new role grants access to all read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access to start, restart, and monitor virtual machines.</span></span> <span data-ttu-id="800aa-164">Il ruolo personalizzato può essere usato in due sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="800aa-164">The custom role can be used in two subscriptions.</span></span>

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

### <a name="create-role-with-json-template"></a><span data-ttu-id="800aa-166">Creare un ruolo con il modello JSON</span><span class="sxs-lookup"><span data-stu-id="800aa-166">Create role with JSON template</span></span>
<span data-ttu-id="800aa-167">È possibile usare un modello JSON come definizione di origine per il ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="800aa-167">A JSON template can be used as the source definition for the custom role.</span></span> <span data-ttu-id="800aa-168">Nell'esempio seguente viene creato un ruolo personalizzato che consente di accedere in lettura all'archiviazione e alle risorse di calcolo, di accedere come supporto e di aggiungere tale ruolo a due sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="800aa-168">The following example creates a custom role that allows read access to storage and compute resources, access to support, and adds that role to two subscriptions.</span></span> <span data-ttu-id="800aa-169">Creare un nuovo file `C:\CustomRoles\customrole1.json` con il seguente esempio.</span><span class="sxs-lookup"><span data-stu-id="800aa-169">Create a new file `C:\CustomRoles\customrole1.json` with the following example.</span></span> <span data-ttu-id="800aa-170">L'ID deve essere impostato su `null` all'inizio della creazione del ruolo quando viene generato in automatico un nuovo ID.</span><span class="sxs-lookup"><span data-stu-id="800aa-170">The Id should be set to `null` on initial role creation as a new ID is generated automatically.</span></span> 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access to Azure storage and compute resources and access to support",
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
<span data-ttu-id="800aa-171">Per aggiungere il ruolo alle sottoscrizioni, eseguire il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="800aa-171">To add the role to the subscriptions, run the following PowerShell command:</span></span>
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a><span data-ttu-id="800aa-172">Modificare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="800aa-172">Modify a custom role</span></span>
<span data-ttu-id="800aa-173">Così come per la creazione di un ruolo personalizzato, è possibile modificare un ruolo personalizzato esistente usando PSRoleDefinitionObject o un modello JSON.</span><span class="sxs-lookup"><span data-stu-id="800aa-173">Similar to creating a custom role, you can modify an existing custom role using either the PSRoleDefinitionObject or a JSON template.</span></span>

### <a name="modify-role-with-psroledefinitionobject"></a><span data-ttu-id="800aa-174">Modificare un ruolo con PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="800aa-174">Modify role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="800aa-175">Per modificare un ruolo personalizzato, usare innanzitutto il comando `Get-AzureRmRoleDefinition` per recuperare la definizione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="800aa-175">To modify a custom role, first, use the `Get-AzureRmRoleDefinition` command to retrieve the role definition.</span></span> <span data-ttu-id="800aa-176">Successivamente, apportare le modifiche desiderate alla definizione del ruolo.</span><span class="sxs-lookup"><span data-stu-id="800aa-176">Second, make the desired changes to the role definition.</span></span> <span data-ttu-id="800aa-177">Infine, usare il comando `Set-AzureRmRoleDefinition` per salvare la definizione del ruolo modificata.</span><span class="sxs-lookup"><span data-stu-id="800aa-177">Finally, use the `Set-AzureRmRoleDefinition` command to save the modified role definition.</span></span>

<span data-ttu-id="800aa-178">Nell'esempio seguente viene aggiunta l'operazione `Microsoft.Insights/diagnosticSettings/*` al ruolo personalizzato *Operatore macchina virtuale* .</span><span class="sxs-lookup"><span data-stu-id="800aa-178">The following example adds the `Microsoft.Insights/diagnosticSettings/*` operation to the *Virtual Machine Operator* custom role.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![Controllo degli accessi in base al ruolo di PowerShell - Set-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

<span data-ttu-id="800aa-180">Nell'esempio seguente viene aggiunta una sottoscrizione di Azure agli ambiti assegnabili del ruolo personalizzato *Virtual Machine Operator* .</span><span class="sxs-lookup"><span data-stu-id="800aa-180">The following example adds an Azure subscription to the assignable scopes of the *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![Controllo degli accessi in base al ruolo di PowerShell - Set-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a><span data-ttu-id="800aa-182">Modificare un ruolo con il modello JSON</span><span class="sxs-lookup"><span data-stu-id="800aa-182">Modify role with JSON template</span></span>
<span data-ttu-id="800aa-183">Usando il modello JSON precedente, è possibile modificare un ruolo personalizzato esistente per aggiungere o rimuovere le azioni.</span><span class="sxs-lookup"><span data-stu-id="800aa-183">Using the previous JSON template, you can easily modify an existing custom role to add or remove Actions.</span></span> <span data-ttu-id="800aa-184">Aggiornare il modello JSON e aggiungere l'azione di lettura per la rete, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="800aa-184">Update the JSON template and add the read action for networking as shown in the following example.</span></span> <span data-ttu-id="800aa-185">Le definizioni riportate nel modello non vengono applicate in modo cumulativo a una definizione esistente, vale a dire che il ruolo verrà visualizzato esattamente come specificato nel modello.</span><span class="sxs-lookup"><span data-stu-id="800aa-185">The definitions listed in the template are not cumulatively applied to an existing definition, meaning that the role appears exactly as you specify in the template.</span></span> <span data-ttu-id="800aa-186">È anche necessario aggiornare il campo ID con l'ID del ruolo.</span><span class="sxs-lookup"><span data-stu-id="800aa-186">You also need to update the Id field with the ID of the role.</span></span> <span data-ttu-id="800aa-187">Se non si è certi di quale sia questo valore, è possibile utilizzare il cmdlet `Get-AzureRmRoleDefinition` per ottenere queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="800aa-187">If you aren't sure what this value is, you can use the `Get-AzureRmRoleDefinition` cmdlet to get this information.</span></span>

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access to Azure storage and compute resources and access to support",
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

<span data-ttu-id="800aa-188">Per aggiornare il ruolo esistente, eseguire il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="800aa-188">To update the existing role, run the following PowerShell command:</span></span>
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a><span data-ttu-id="800aa-189">Eliminare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="800aa-189">Delete a custom role</span></span>
<span data-ttu-id="800aa-190">Per eliminare un ruolo personalizzato, usare il comando `Remove-AzureRmRoleDefinition` .</span><span class="sxs-lookup"><span data-stu-id="800aa-190">To delete a custom role, use the `Remove-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="800aa-191">Nell'esempio seguente viene rimosso il ruolo personalizzato *Operatore macchina virtuale* .</span><span class="sxs-lookup"><span data-stu-id="800aa-191">The following example removes the *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![Controllo degli accessi in base al ruolo di PowerShell - Remove-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a><span data-ttu-id="800aa-193">Elencare ruoli personalizzati</span><span class="sxs-lookup"><span data-stu-id="800aa-193">List custom roles</span></span>
<span data-ttu-id="800aa-194">Per elencare i ruoli disponibili per l'assegnazione a un ambito, usare il comando `Get-AzureRmRoleDefinition` .</span><span class="sxs-lookup"><span data-stu-id="800aa-194">To list the roles that are available for assignment at a scope, use the `Get-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="800aa-195">L'esempio seguente elenca tutti i ruoli disponibili per l'assegnazione nella sottoscrizione selezionata.</span><span class="sxs-lookup"><span data-stu-id="800aa-195">The following example lists all roles that are available for assignment in the selected subscription.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

<span data-ttu-id="800aa-197">Nell'esempio seguente il ruolo personalizzato *Virtual Machine Operator* non è disponibile nella sottoscrizione *Production4* perché la sottoscrizione non è inclusa in **AssignableScopes** per il ruolo.</span><span class="sxs-lookup"><span data-stu-id="800aa-197">In the following example, the *Virtual Machine Operator* custom role isn’t available in the *Production4* subscription because that subscription isn’t in the **AssignableScopes** of the role.</span></span>

![Controllo degli accessi in base al ruolo di PowerShell - Get-AzureRmRoleDefinition - Schermata](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a><span data-ttu-id="800aa-199">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="800aa-199">See also</span></span>
* <span data-ttu-id="800aa-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)] (Uso di Azure PowerShell con Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="800aa-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span></span>

