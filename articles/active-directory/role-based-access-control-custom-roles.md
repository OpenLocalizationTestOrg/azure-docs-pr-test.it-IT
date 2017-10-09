---
title: aaaCreate ruoli personalizzati per Azure RBAC | Documenti Microsoft
description: "Informazioni su come ruoli personalizzati toodefine con il controllo di accesso di gestire più precisa gestione delle identità nella sottoscrizione di Azure."
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
ms.openlocfilehash: 60df12632ef6c086d5feeb1809196d7c4ee5e021
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="d4681-103">Creare ruoli personalizzati per il controllo degli accessi in base al ruolo di Azure</span><span class="sxs-lookup"><span data-stu-id="d4681-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="d4681-104">Creare un ruolo personalizzato nel controllo di accesso gestire (RBAC), se nessuno dei ruoli predefiniti hello soddisfano le esigenze di accesso specifico.</span><span class="sxs-lookup"><span data-stu-id="d4681-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of hello built-in roles meet your specific access needs.</span></span> <span data-ttu-id="d4681-105">È possibile creare ruoli personalizzati utilizzando [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [interfaccia della riga di comando di Azure](role-based-access-control-manage-access-azure-cli.md) (CLI), hello e [API REST](role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="d4681-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and hello [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="d4681-106">Proprio come i ruoli predefiniti, è possibile assegnare ruoli personalizzati toousers, gruppi e le applicazioni di sottoscrizione, gruppo di risorse e gli ambiti di risorsa.</span><span class="sxs-lookup"><span data-stu-id="d4681-106">Just like built-in roles, you can assign custom roles toousers, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="d4681-107">I ruoli personalizzati vengono archiviati in un tenant di Azure AD e possono essere condivisi tra le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="d4681-107">Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.</span></span>

<span data-ttu-id="d4681-108">Ogni tenant può creare dei ruoli personalizzati too2000.</span><span class="sxs-lookup"><span data-stu-id="d4681-108">Each tenant can create up too2000 custom roles.</span></span> 

<span data-ttu-id="d4681-109">Hello seguente illustra un ruolo personalizzato per il monitoraggio e il riavvio delle macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="d4681-109">hello following example shows a custom role for monitoring and restarting virtual machines:</span></span>

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
## <a name="actions"></a><span data-ttu-id="d4681-110">Azioni</span><span class="sxs-lookup"><span data-stu-id="d4681-110">Actions</span></span>
<span data-ttu-id="d4681-111">Hello **azioni** proprietà di un ruolo personalizzato specifica hello Azure operazioni toowhich hello ruolo concede l'accesso.</span><span class="sxs-lookup"><span data-stu-id="d4681-111">hello **Actions** property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span> <span data-ttu-id="d4681-112">Si tratta di una raccolta di stringhe di operazione che identificano operazioni a protezione diretta dei provider di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4681-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="d4681-113">Stringhe di operazione seguono il formato di hello delle `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span><span class="sxs-lookup"><span data-stu-id="d4681-113">Operation strings follow hello format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="d4681-114">Le stringhe di operazione che contengono i caratteri jolly (\*) concedere l'accesso tooall operazioni che corrispondono a stringa hello dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="d4681-114">Operation strings that contain wildcards (\*) grant access tooall operations that match hello operation string.</span></span> <span data-ttu-id="d4681-115">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d4681-115">For instance:</span></span>

* <span data-ttu-id="d4681-116">`*/read`concede l'accesso tooread operazioni per tutti i tipi di risorse di tutti i provider di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4681-116">`*/read` grants access tooread operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="d4681-117">`Microsoft.Compute/*`concede l'accesso tooall operazioni per tutti i tipi di risorse di provider di risorse Microsoft. COMPUTE hello.</span><span class="sxs-lookup"><span data-stu-id="d4681-117">`Microsoft.Compute/*` grants access tooall operations for all resource types in hello Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="d4681-118">`Microsoft.Network/*/read`concede l'accesso tooread operazioni per tutti i tipi di risorsa nel provider di risorse Microsoft. Network hello di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4681-118">`Microsoft.Network/*/read` grants access tooread operations for all resource types in hello Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="d4681-119">`Microsoft.Compute/virtualMachines/*`concede l'accesso tooall operazioni delle macchine virtuali e i relativi tipi di risorsa figlio.</span><span class="sxs-lookup"><span data-stu-id="d4681-119">`Microsoft.Compute/virtualMachines/*` grants access tooall operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="d4681-120">`Microsoft.Web/sites/restart/Action`concede l'accesso di siti Web toorestart.</span><span class="sxs-lookup"><span data-stu-id="d4681-120">`Microsoft.Web/sites/restart/Action` grants access toorestart websites.</span></span>

<span data-ttu-id="d4681-121">Utilizzare `Get-AzureRmProviderOperation` (in PowerShell) o `azure provider operations show` (in Azure CLI) operazioni toolist di provider di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4681-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) toolist operations of Azure resource providers.</span></span> <span data-ttu-id="d4681-122">È anche possibile utilizzare questi comandi tooverify che una stringa di operazione è valida e tooexpand con caratteri jolly operazione stringhe.</span><span class="sxs-lookup"><span data-stu-id="d4681-122">You may also use these commands tooverify that an operation string is valid, and tooexpand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![Schermata PowerShell - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="d4681-124">Screenshot dell'interfaccia della riga di comando di Azure: azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span><span class="sxs-lookup"><span data-stu-id="d4681-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="d4681-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="d4681-125">NotActions</span></span>
<span data-ttu-id="d4681-126">Hello utilizzare **NotActions** proprietà se il set di hello di operazioni che si desidera tooallow è definito più facilmente escludendo operazioni con restrizioni.</span><span class="sxs-lookup"><span data-stu-id="d4681-126">Use hello **NotActions** property if hello set of operations that you wish tooallow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="d4681-127">Hello accesso concesso da un ruolo personalizzato viene calcolato sottraendo hello **NotActions** operazioni hello **azioni** operazioni.</span><span class="sxs-lookup"><span data-stu-id="d4681-127">hello access granted by a custom role is computed by subtracting hello **NotActions** operations from hello **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="d4681-128">Se un utente è assegnato un ruolo che esclude in un'operazione **NotActions**e viene assegnato un secondo ruolo che concede l'accesso toohello utente hello stessa operazione è consentita tooperform tale operazione.</span><span class="sxs-lookup"><span data-stu-id="d4681-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access toohello same operation, hello user is allowed tooperform that operation.</span></span> <span data-ttu-id="d4681-129">**NotActions** non è un'istruzione deny regola: è semplicemente un modo pratico toocreate un set di operazioni consentite quando operazioni specifiche necessitano toobe esclusi.</span><span class="sxs-lookup"><span data-stu-id="d4681-129">**NotActions** is not a deny rule – it is simply a convenient way toocreate a set of allowed operations when specific operations need toobe excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="d4681-130">AssignableScopes</span><span class="sxs-lookup"><span data-stu-id="d4681-130">AssignableScopes</span></span>
<span data-ttu-id="d4681-131">Hello **AssignableScopes** proprietà del ruolo personalizzata hello specifica ambiti hello (sottoscrizioni, gruppi di risorse o di risorse) all'interno delle quali hello è disponibile per l'assegnazione ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="d4681-131">hello **AssignableScopes** property of hello custom role specifies hello scopes (subscriptions, resource groups, or resources) within which hello custom role is available for assignment.</span></span> <span data-ttu-id="d4681-132">È possibile rendere disponibili per l'assegnazione di ruolo personalizzata hello in solo le sottoscrizioni di hello o gruppi di risorse che richiedono e non gli utenti di confusione esperienza per rest hello di sottoscrizioni hello o gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="d4681-132">You can make hello custom role available for assignment in only hello subscriptions or resource groups that require it, and not clutter user experience for hello rest of hello subscriptions or resource groups.</span></span>

<span data-ttu-id="d4681-133">Ecco alcuni esempi di ambiti assegnabili validi:</span><span class="sxs-lookup"><span data-stu-id="d4681-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="d4681-134">"le sottoscrizioni/c276fc76-9cd4-44c9-99a7-4fd71546436e", "sottoscrizioni/e91d47c4-76f3-4271-a796-21b4ecfe3624" - rende disponibili per l'assegnazione ruolo hello in due sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="d4681-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes hello role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="d4681-135">"le sottoscrizioni/c276fc76-9cd4-44c9-99a7-4fd71546436e" - rende disponibili per l'assegnazione ruolo hello in una singola sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d4681-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes hello role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="d4681-136">"/ sottoscrizioni/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/di rete" - rende hello ruolo disponibile per l'assegnazione solo nel gruppo di risorse di rete hello.</span><span class="sxs-lookup"><span data-stu-id="d4681-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes hello role available for assignment only in hello Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="d4681-137">È necessario usare almeno una sottoscrizione, un gruppo di risorse o un ID della risorsa.</span><span class="sxs-lookup"><span data-stu-id="d4681-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="d4681-138">Controllo di accesso ai ruoli personalizzati</span><span class="sxs-lookup"><span data-stu-id="d4681-138">Custom roles access control</span></span>
<span data-ttu-id="d4681-139">Hello **AssignableScopes** proprietà del ruolo personalizzata hello controlla inoltre che può visualizzare, modificare ed eliminare il ruolo di hello.</span><span class="sxs-lookup"><span data-stu-id="d4681-139">hello **AssignableScopes** property of hello custom role also controls who can view, modify, and delete hello role.</span></span>

* <span data-ttu-id="d4681-140">È necessario specificare gli utenti autorizzati a creare un ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="d4681-140">Who can create a custom role?</span></span>
    <span data-ttu-id="d4681-141">I ruoli Proprietario e Amministratore Accessi utenti di sottoscrizioni, gruppi di risorse e risorse possono creare ruoli personalizzati da usare in questi ambiti.</span><span class="sxs-lookup"><span data-stu-id="d4681-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="d4681-142">utente che Crea ruolo hello Hello deve tooperform in grado di toobe `Microsoft.Authorization/roleDefinition/write` operazione su tutti hello **AssignableScopes** del ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="d4681-142">hello user creating hello role needs toobe able tooperform `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of hello role.</span></span>
* <span data-ttu-id="d4681-143">È necessario specificare gli utenti autorizzati a modificare un ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="d4681-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="d4681-144">I ruoli Proprietario e Amministratore Accessi utenti di sottoscrizioni, gruppi di risorse e risorse possono modificare i ruoli personalizzati in questi ambiti.</span><span class="sxs-lookup"><span data-stu-id="d4681-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="d4681-145">Gli utenti devono hello in grado di tooperform toobe `Microsoft.Authorization/roleDefinition/write` operazione su tutti hello **AssignableScopes** di un ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="d4681-145">Users need toobe able tooperform hello `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="d4681-146">Chi può visualizzare i ruoli personalizzati</span><span class="sxs-lookup"><span data-stu-id="d4681-146">Who can view custom roles?</span></span>
    <span data-ttu-id="d4681-147">Tutti i ruoli predefiniti nel Controllo degli accessi in base al ruolo di Azure consentono la visualizzazione dei ruoli disponibili per l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="d4681-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="d4681-148">Gli utenti possono eseguire hello `Microsoft.Authorization/roleDefinition/read` operazione in un ambito è possibile visualizzare i ruoli RBAC hello che sono disponibili per l'assegnazione in quell'ambito.</span><span class="sxs-lookup"><span data-stu-id="d4681-148">Users who can perform hello `Microsoft.Authorization/roleDefinition/read` operation at a scope can view hello RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="d4681-149">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d4681-149">See also</span></span>
* <span data-ttu-id="d4681-150">[Controllo di accesso basato su ruoli](role-based-access-control-configure.md): Introduzione a RBAC in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4681-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="d4681-151">Informazioni su come accedere a toomanage con:</span><span class="sxs-lookup"><span data-stu-id="d4681-151">Learn how toomanage access with:</span></span>
  * [<span data-ttu-id="d4681-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4681-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="d4681-153">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="d4681-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="d4681-154">API REST</span><span class="sxs-lookup"><span data-stu-id="d4681-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="d4681-155">[Ruoli predefiniti](role-based-access-built-in-roles.md): ottenere informazioni sui ruoli hello forniti come standard in RBAC.</span><span class="sxs-lookup"><span data-stu-id="d4681-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
