---
title: Creare ruoli personalizzati per il controllo degli accessi in base al ruolo di Azure | Documentazione Microsoft
description: "Informazioni su come definire i ruoli personalizzati con il Controllo degli accessi in base al ruolo per una gestione più precisa delle identità nella sottoscrizione di Azure."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8e72f2c8095d13c4b6df3c6576bd58806a3c0f2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="9c35f-103">Creare ruoli personalizzati per il controllo degli accessi in base al ruolo di Azure</span><span class="sxs-lookup"><span data-stu-id="9c35f-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="9c35f-104">Creare un ruolo personalizzato nel Controllo degli accessi in base al ruolo di Azure, se nessuno dei ruoli predefiniti soddisfa le esigenze di accesso specifiche.</span><span class="sxs-lookup"><span data-stu-id="9c35f-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of the built-in roles meet your specific access needs.</span></span> <span data-ttu-id="9c35f-105">I ruoli personalizzati possono essere creati usando [Azure PowerShell](role-based-access-control-manage-access-powershell.md), l'[interfaccia della riga di comando di Azure](role-based-access-control-manage-access-azure-cli.md) e l'[API REST](role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="9c35f-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and the [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="9c35f-106">Analogamente ai ruoli predefiniti, è possibile assegnare ruoli personalizzati a utenti, gruppi e applicazioni nell'ambito della sottoscrizione, del gruppo di risorse e delle risorse.</span><span class="sxs-lookup"><span data-stu-id="9c35f-106">Just like built-in roles, you can assign custom roles to users, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="9c35f-107">I ruoli personalizzati vengono archiviati in un tenant di Azure AD e possono essere condivisi tra le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="9c35f-107">Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.</span></span>

<span data-ttu-id="9c35f-108">Ogni tenant può creare fino a 2000 ruoli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="9c35f-108">Each tenant can create up to 2000 custom roles.</span></span> 

<span data-ttu-id="9c35f-109">L'esempio seguente mostra un ruolo personalizzato, che consente il monitoraggio e il riavvio di macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="9c35f-109">The following example shows a custom role for monitoring and restarting virtual machines:</span></span>

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a><span data-ttu-id="9c35f-110">Azioni</span><span class="sxs-lookup"><span data-stu-id="9c35f-110">Actions</span></span>
<span data-ttu-id="9c35f-111">La proprietà **Actions** di un ruolo personalizzato specifica le operazioni di Azure a cui il ruolo concede l'accesso.</span><span class="sxs-lookup"><span data-stu-id="9c35f-111">The **Actions** property of a custom role specifies the Azure operations to which the role grants access.</span></span> <span data-ttu-id="9c35f-112">Si tratta di una raccolta di stringhe di operazione che identificano operazioni a protezione diretta dei provider di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c35f-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="9c35f-113">Le stringhe di operazione seguono il formato di `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span><span class="sxs-lookup"><span data-stu-id="9c35f-113">Operation strings follow the format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="9c35f-114">Le stringhe di operazione che contengono caratteri jolly (\*) concedono l'accesso a tutte le operazioni corrispondenti alla stringa di operazione.</span><span class="sxs-lookup"><span data-stu-id="9c35f-114">Operation strings that contain wildcards (\*) grant access to all operations that match the operation string.</span></span> <span data-ttu-id="9c35f-115">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9c35f-115">For instance:</span></span>

* <span data-ttu-id="9c35f-116">`*/read` concede l'accesso a operazioni di lettura per tutti i tipi di risorsa di tutti i provider di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c35f-116">`*/read` grants access to read operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="9c35f-117">`Microsoft.Compute/*` concede l'accesso a tutte le operazioni per tutti i tipi di risorsa nel provider di risorse Microsoft.Compute.</span><span class="sxs-lookup"><span data-stu-id="9c35f-117">`Microsoft.Compute/*` grants access to all operations for all resource types in the Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="9c35f-118">`Microsoft.Network/*/read` concede l'accesso a operazioni di lettura per tutti i tipi di risorsa nel provider di risorse Microsoft.Network di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c35f-118">`Microsoft.Network/*/read` grants access to read operations for all resource types in the Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="9c35f-119">`Microsoft.Compute/virtualMachines/*` concede l'accesso a tutte le operazioni delle macchine virtuali e ai relativi tipi di risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="9c35f-119">`Microsoft.Compute/virtualMachines/*` grants access to all operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="9c35f-120">`Microsoft.Web/sites/restart/Action` concede l'accesso per il riavvio dei siti Web.</span><span class="sxs-lookup"><span data-stu-id="9c35f-120">`Microsoft.Web/sites/restart/Action` grants access to restart websites.</span></span>

<span data-ttu-id="9c35f-121">Usare `Get-AzureRmProviderOperation` in PowerShell o `azure provider operations show` nell'interfaccia della riga di comando di Azure per elencare le operazioni dei provider di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c35f-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) to list operations of Azure resource providers.</span></span> <span data-ttu-id="9c35f-122">È anche possibile usare questi comandi per verificare la validità di una stringa di operazione e per espandere le stringhe di operazione con caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="9c35f-122">You may also use these commands to verify that an operation string is valid, and to expand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![Schermata PowerShell - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="9c35f-124">Screenshot dell'interfaccia della riga di comando di Azure: azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span><span class="sxs-lookup"><span data-stu-id="9c35f-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="9c35f-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="9c35f-125">NotActions</span></span>
<span data-ttu-id="9c35f-126">Usare la proprietà **NotActions** se il set di operazioni che si vuole consentire viene più facilmente definito escludendo le operazioni con restrizioni.</span><span class="sxs-lookup"><span data-stu-id="9c35f-126">Use the **NotActions** property if the set of operations that you wish to allow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="9c35f-127">L'accesso concesso da un ruolo personalizzato viene calcolato sottraendo le operazioni **NotActions** dalle operazioni **Actions**.</span><span class="sxs-lookup"><span data-stu-id="9c35f-127">The access granted by a custom role is computed by subtracting the **NotActions** operations from the **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="9c35f-128">Se a un utente viene assegnato un ruolo che esclude un'operazione in **NotActions** e un secondo ruolo che concede l'accesso alla stessa operazione, l'utente può eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="9c35f-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access to the same operation, the user is allowed to perform that operation.</span></span> <span data-ttu-id="9c35f-129">**NotActions** non è una regola di negazione. È semplicemente un modo comodo per creare una serie di operazioni consentite quando è necessario escludere operazioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="9c35f-129">**NotActions** is not a deny rule – it is simply a convenient way to create a set of allowed operations when specific operations need to be excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="9c35f-130">AssignableScopes</span><span class="sxs-lookup"><span data-stu-id="9c35f-130">AssignableScopes</span></span>
<span data-ttu-id="9c35f-131">La proprietà **AssignableScopes** del ruolo personalizzato specifica gli ambiti, ovvero sottoscrizioni, gruppi di risorse o risorse, entro i quali il ruolo personalizzato è disponibile per l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="9c35f-131">The **AssignableScopes** property of the custom role specifies the scopes (subscriptions, resource groups, or resources) within which the custom role is available for assignment.</span></span> <span data-ttu-id="9c35f-132">È possibile rendere disponibile il ruolo personalizzato per l'assegnazione solo nelle sottoscrizioni o nei gruppi di risorse che lo richiedono, in modo da non complicare l'esperienza utente per le altre sottoscrizioni o gli altri gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="9c35f-132">You can make the custom role available for assignment in only the subscriptions or resource groups that require it, and not clutter user experience for the rest of the subscriptions or resource groups.</span></span>

<span data-ttu-id="9c35f-133">Ecco alcuni esempi di ambiti assegnabili validi:</span><span class="sxs-lookup"><span data-stu-id="9c35f-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="9c35f-134">"/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e", "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624": rende disponibile il ruolo per l'assegnazione in due sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="9c35f-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes the role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="9c35f-135">"/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e": rende disponibile il ruolo per l'assegnazione in una singola sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9c35f-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes the role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="9c35f-136">"/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network": rende disponibile il ruolo per l'assegnazione solo nel gruppo di risorse Network.</span><span class="sxs-lookup"><span data-stu-id="9c35f-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes the role available for assignment only in the Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="9c35f-137">È necessario usare almeno una sottoscrizione, un gruppo di risorse o un ID della risorsa.</span><span class="sxs-lookup"><span data-stu-id="9c35f-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="9c35f-138">Controllo di accesso ai ruoli personalizzati</span><span class="sxs-lookup"><span data-stu-id="9c35f-138">Custom roles access control</span></span>
<span data-ttu-id="9c35f-139">La proprietà **AssignableScopes** del ruolo personalizzato controlla anche quali utenti possono visualizzare, modificare ed eliminare il ruolo.</span><span class="sxs-lookup"><span data-stu-id="9c35f-139">The **AssignableScopes** property of the custom role also controls who can view, modify, and delete the role.</span></span>

* <span data-ttu-id="9c35f-140">È necessario specificare gli utenti autorizzati a creare un ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="9c35f-140">Who can create a custom role?</span></span>
    <span data-ttu-id="9c35f-141">I ruoli Proprietario e Amministratore Accessi utenti di sottoscrizioni, gruppi di risorse e risorse possono creare ruoli personalizzati da usare in questi ambiti.</span><span class="sxs-lookup"><span data-stu-id="9c35f-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="9c35f-142">L'utente che crea il ruolo deve poter eseguire l'operazione `Microsoft.Authorization/roleDefinition/write` in tutte le proprietà **AssignableScopes** del ruolo.</span><span class="sxs-lookup"><span data-stu-id="9c35f-142">The user creating the role needs to be able to perform `Microsoft.Authorization/roleDefinition/write` operation on all the **AssignableScopes** of the role.</span></span>
* <span data-ttu-id="9c35f-143">È necessario specificare gli utenti autorizzati a modificare un ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="9c35f-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="9c35f-144">I ruoli Proprietario e Amministratore Accessi utenti di sottoscrizioni, gruppi di risorse e risorse possono modificare i ruoli personalizzati in questi ambiti.</span><span class="sxs-lookup"><span data-stu-id="9c35f-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="9c35f-145">Gli utenti devono poter eseguire l'operazione `Microsoft.Authorization/roleDefinition/write` in tutte le proprietà **AssignableScopes** di un ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="9c35f-145">Users need to be able to perform the `Microsoft.Authorization/roleDefinition/write` operation on all the **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="9c35f-146">Chi può visualizzare i ruoli personalizzati</span><span class="sxs-lookup"><span data-stu-id="9c35f-146">Who can view custom roles?</span></span>
    <span data-ttu-id="9c35f-147">Tutti i ruoli predefiniti nel Controllo degli accessi in base al ruolo di Azure consentono la visualizzazione dei ruoli disponibili per l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="9c35f-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="9c35f-148">Gli utenti che possono eseguire l'operazione `Microsoft.Authorization/roleDefinition/read` a livello di ambito possono visualizzare i ruoli del Controllo degli accessi in base al ruolo disponibili per l'assegnazione in tale ambito.</span><span class="sxs-lookup"><span data-stu-id="9c35f-148">Users who can perform the `Microsoft.Authorization/roleDefinition/read` operation at a scope can view the RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="9c35f-149">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9c35f-149">See also</span></span>
* <span data-ttu-id="9c35f-150">[Controllo degli accessi in base al ruolo](role-based-access-control-configure.md): introduzione al controllo degli accessi in base al ruolo nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c35f-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="9c35f-151">Informazioni su come gestire l'accesso con:</span><span class="sxs-lookup"><span data-stu-id="9c35f-151">Learn how to manage access with:</span></span>
  * [<span data-ttu-id="9c35f-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c35f-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="9c35f-153">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="9c35f-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="9c35f-154">API REST</span><span class="sxs-lookup"><span data-stu-id="9c35f-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="9c35f-155">[Ruoli predefiniti](role-based-access-built-in-roles.md): informazioni dettagliate sui ruoli predefiniti del controllo degli accessi in base al ruolo.</span><span class="sxs-lookup"><span data-stu-id="9c35f-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>
