---
title: Gestire il controllo degli accessi in base al ruolo con l'interfaccia della riga di comando di Azure | Documentazione Microsoft
description: "Informazioni su come gestire il controllo degli accessi in base al ruolo (RBAC) con l'interfaccia della riga di comando di Azure, ad esempio ottenere un elenco dei ruoli e delle relative azioni, nonché assegnare i ruoli nell'ambito della sottoscrizione e dell'applicazione."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 3483ee01-8177-49e7-b337-4d5cb14f5e32
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: ad644de6d23950e699d99042d27381336626caab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-azure-command-line-interface"></a><span data-ttu-id="57bc3-103">Gestire il controllo degli accessi in base al ruolo con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="57bc3-103">Manage Role-Based Access Control with the Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="57bc3-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="57bc3-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="57bc3-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="57bc3-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="57bc3-106">API REST</span><span class="sxs-lookup"><span data-stu-id="57bc3-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="57bc3-107">È possibile usare il controllo degli accessi in base al ruolo nel portale di Azure e nell'API di Azure Resource Manager per gestire l'accesso alla sottoscrizione e alle risorse a un livello estremamente specifico.</span><span class="sxs-lookup"><span data-stu-id="57bc3-107">You can use Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API to manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="57bc3-108">Con questa funzionalità è possibile concedere l'accesso a utenti, gruppi o entità servizio di Active Directory assegnando loro dei ruoli in un determinato ambito.</span><span class="sxs-lookup"><span data-stu-id="57bc3-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

<span data-ttu-id="57bc3-109">Per usare l'interfaccia della riga di comando di Azure per gestire il controllo degli accessi in base al ruolo, è necessario disporre dei prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="57bc3-109">Before you can use the Azure command-line interface (CLI) to manage RBAC, you must have the following prerequisites:</span></span>

* <span data-ttu-id="57bc3-110">Usare la versione 0.8.8 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="57bc3-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="57bc3-111">Per installare la versione più recente e associarla alla sottoscrizione di Azure, vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="57bc3-111">To install the latest version and associate it with your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="57bc3-112">Azure Resource Manager nell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="57bc3-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="57bc3-113">Per altre informazioni, vedere [Uso dell'interfaccia della riga di comando di Azure con Resource Manager](../xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="57bc3-113">Go to [Using the Azure CLI with the Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="57bc3-114">Elenco dei ruoli</span><span class="sxs-lookup"><span data-stu-id="57bc3-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="57bc3-115">Elencare tutti i ruoli disponibili</span><span class="sxs-lookup"><span data-stu-id="57bc3-115">List all available roles</span></span>
<span data-ttu-id="57bc3-116">Per elencare tutti i ruoli disponibili, usare:</span><span class="sxs-lookup"><span data-stu-id="57bc3-116">To list all available roles, use:</span></span>

        azure role list

<span data-ttu-id="57bc3-117">L'esempio seguente mostra l'elenco di *tutti i ruoli disponibili*.</span><span class="sxs-lookup"><span data-stu-id="57bc3-117">The following example shows the list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Elenco di ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="57bc3-119">Elencare le azioni di un ruolo</span><span class="sxs-lookup"><span data-stu-id="57bc3-119">List actions of a role</span></span>
<span data-ttu-id="57bc3-120">Per elencare le azioni di un ruolo, usare:</span><span class="sxs-lookup"><span data-stu-id="57bc3-120">To list the actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="57bc3-121">L'esempio seguente mostra le azioni dei ruoli *Collaboratore* e *Collaboratore Macchina virtuale*.</span><span class="sxs-lookup"><span data-stu-id="57bc3-121">The following example shows the actions of the *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Visualizzazione dei ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="57bc3-123">Elencare l'accesso</span><span class="sxs-lookup"><span data-stu-id="57bc3-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="57bc3-124">Elencare le assegnazioni di ruoli valide per un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="57bc3-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="57bc3-125">Per elencare le assegnazioni di ruolo in un gruppo di risorse, usare:</span><span class="sxs-lookup"><span data-stu-id="57bc3-125">To list the role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="57bc3-126">L'esempio seguente indica le assegnazioni di ruolo nel gruppo *pharma-sales-projecforcast* .</span><span class="sxs-lookup"><span data-stu-id="57bc3-126">The following example shows the role assignments in the *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Elenco di assegnazione di ruoli di Azure per gruppo - Schermata](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="57bc3-128">Elencare i ruoli assegnati a un utente</span><span class="sxs-lookup"><span data-stu-id="57bc3-128">List role assignments for a user</span></span>
<span data-ttu-id="57bc3-129">Per avere un elenco dei ruoli assegnati a un determinato utente e delle assegnazioni ai gruppi di utenti, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="57bc3-129">To list the role assignments for a specific user and the assignments that are assigned to a user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="57bc3-130">È anche possibile visualizzare le assegnazioni di ruolo ereditate dai gruppi modificando il comando:</span><span class="sxs-lookup"><span data-stu-id="57bc3-130">You can also see role assignments that are inherited from groups by modifying the command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="57bc3-131">L'esempio seguente indica le assegnazioni di ruolo concesse all'utente *sameert@aaddemo.com* .</span><span class="sxs-lookup"><span data-stu-id="57bc3-131">The following example shows the role assignments that are granted to the *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="57bc3-132">Include i ruoli assegnati direttamente all'utente, oltre ai ruoli ereditati dai gruppi.</span><span class="sxs-lookup"><span data-stu-id="57bc3-132">This includes roles that are assigned directly to the user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Elenco di assegnazione di ruoli per utente - Schermata](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="57bc3-134">Concedere l'accesso</span><span class="sxs-lookup"><span data-stu-id="57bc3-134">Grant access</span></span>
<span data-ttu-id="57bc3-135">Per concedere l'accesso dopo aver individuato il ruolo da assegnare, usare:</span><span class="sxs-lookup"><span data-stu-id="57bc3-135">To grant access after you have identified the role that you want to assign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-to-group-at-the-subscription-scope"></a><span data-ttu-id="57bc3-136">Assegnare un ruolo a un gruppo nell'ambito della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="57bc3-136">Assign a role to group at the subscription scope</span></span>
<span data-ttu-id="57bc3-137">Per assegnare un ruolo a un gruppo nell'ambito della sottoscrizione, usare:</span><span class="sxs-lookup"><span data-stu-id="57bc3-137">To assign a role to a group at the subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="57bc3-138">L'esempio seguente assegna il ruolo *Reader* (Lettore) a *Christine Koch Team* nell'ambito *subscriptions*.</span><span class="sxs-lookup"><span data-stu-id="57bc3-138">The following example assigns the *Reader* role to *Christine Koch's Team* at the *subscription* scope.</span></span>

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Assegnazione di ruoli di Azure creata per gruppo - Schermata](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-to-an-application-at-the-subscription-scope"></a><span data-ttu-id="57bc3-140">Assegnare un ruolo a un'applicazione nell'ambito della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="57bc3-140">Assign a role to an application at the subscription scope</span></span>
<span data-ttu-id="57bc3-141">Per assegnare un ruolo a un'applicazione nell'ambito della sottoscrizione, usare:</span><span class="sxs-lookup"><span data-stu-id="57bc3-141">To assign a role to an application at the subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="57bc3-142">L'esempio seguente assegna il ruolo *Contributor* (Collaboratore) a un'applicazione *Azure AD* nella sottoscrizione selezionata.</span><span class="sxs-lookup"><span data-stu-id="57bc3-142">The following example grants the *Contributor* role to an *Azure AD* application on the selected subscription.</span></span>

 ![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Assegnazione di ruoli creata per applicazione](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-to-a-user-at-the-resource-group-scope"></a><span data-ttu-id="57bc3-144">Assegnare un ruolo a un utente nell'ambito di un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="57bc3-144">Assign a role to a user at the resource group scope</span></span>
<span data-ttu-id="57bc3-145">Per assegnare un ruolo a un utente nell'ambito di un gruppo di risorse, usare:</span><span class="sxs-lookup"><span data-stu-id="57bc3-145">To assign a role to a user at the resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="57bc3-146">L'esempio seguente assegna il ruolo *Virtual Machine Contributor* (Collaboratore Macchina virtuale) all'utente *samert@aaddemo.com* nell'ambito del gruppo di risorse *Pharma-Sales-ProjectForcast*.</span><span class="sxs-lookup"><span data-stu-id="57bc3-146">The following example grants the *Virtual Machine Contributor* role to *samert@aaddemo.com* user at the *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Assegnazione di ruoli di Azure creata per utente - Schermata](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-to-a-group-at-the-resource-scope"></a><span data-ttu-id="57bc3-148">Assegnare un ruolo a un gruppo nell'ambito delle risorse</span><span class="sxs-lookup"><span data-stu-id="57bc3-148">Assign a role to a group at the resource scope</span></span>
<span data-ttu-id="57bc3-149">Per assegnare un ruolo a un gruppo nell'ambito di un gruppo di risorse, usare:</span><span class="sxs-lookup"><span data-stu-id="57bc3-149">To assign a role to a group at the resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="57bc3-150">L'esempio seguente assegna il ruolo *Virtual Machine Contributor* (Collaboratore Macchina virtuale) a un gruppo *Azure AD* in una *subnet*.</span><span class="sxs-lookup"><span data-stu-id="57bc3-150">The following example grants the *Virtual Machine Contributor* role to an *Azure AD* group on a *subnet*.</span></span>

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Assegnazione di ruoli di Azure creata per gruppo - Schermata](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="57bc3-152">Rimuovere un accesso</span><span class="sxs-lookup"><span data-stu-id="57bc3-152">Remove access</span></span>
<span data-ttu-id="57bc3-153">Per rimuovere un'assegnazione di ruolo, usare:</span><span class="sxs-lookup"><span data-stu-id="57bc3-153">To remove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id to from which to remove role> --roleName "<role name>"

<span data-ttu-id="57bc3-154">L'esempio seguente rimuove l'assegnazione del ruolo *Virtual Machine Contributor* (Collaboratore Macchina virtuale) dall'utente *sammert@aaddemo.com* nel gruppo di risorse *Pharma-Sales-ProjectForcast*.</span><span class="sxs-lookup"><span data-stu-id="57bc3-154">The following example removes the *Virtual Machine Contributor* role assignment from the *sammert@aaddemo.com* user on the *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="57bc3-155">Nell'esempio viene quindi rimossa l'assegnazione del ruolo da un gruppo nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="57bc3-155">The example then removes the role assignment from a group on the subscription.</span></span>

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Eliminazione dell'assegnazione di ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="57bc3-157">Creare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="57bc3-157">Create a custom role</span></span>
<span data-ttu-id="57bc3-158">Per creare un ruolo personalizzato, usare:</span><span class="sxs-lookup"><span data-stu-id="57bc3-158">To create a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="57bc3-159">Nell'esempio seguente viene creato il ruolo personalizzato denominato *Operatore macchina virtuale*.</span><span class="sxs-lookup"><span data-stu-id="57bc3-159">The following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="57bc3-160">Questo ruolo personalizzato concede l'accesso a tutte le operazioni di lettura dei provider di risorse *Microsoft.Compute*, *Microsoft.Storage* e *Microsoft.Network* e concede l'accesso per avviare, riavviare e monitorare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="57bc3-160">This custom role grants access to all read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access to start, restart, and monitor virtual machines.</span></span> <span data-ttu-id="57bc3-161">Questo ruolo personalizzato può essere usato in due sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="57bc3-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="57bc3-162">In questo esempio viene usato un file JSON come input.</span><span class="sxs-lookup"><span data-stu-id="57bc3-162">This example uses a JSON file as an input.</span></span>

![JSON - Definizione di ruolo personalizzato - Schermata](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Creazione di ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="57bc3-165">Modificare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="57bc3-165">Modify a custom role</span></span>
<span data-ttu-id="57bc3-166">Per modificare un ruolo personalizzato, usare il comando `azure role show` per recuperare la definizione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="57bc3-166">To modify a custom role, first use the `azure role show` command to retrieve role definition.</span></span> <span data-ttu-id="57bc3-167">Successivamente, apportare le modifiche desiderate al file di definizione del ruolo.</span><span class="sxs-lookup"><span data-stu-id="57bc3-167">Second, make the desired changes to the role definition file.</span></span> <span data-ttu-id="57bc3-168">Usare infine `azure role set` per salvare la definizione del ruolo modificata.</span><span class="sxs-lookup"><span data-stu-id="57bc3-168">Finally, use `azure role set` to save the modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="57bc3-169">L'esempio seguente aggiunge l'operazione *Microsoft.Insights/diagnosticSettings/* alle **Azioni** e una sottoscrizione di Azure ad **AssignableScopes** del ruolo personalizzato Operatore macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="57bc3-169">The following example adds the *Microsoft.Insights/diagnosticSettings/* operation to the **Actions**, and an Azure subscription to the **AssignableScopes** of the Virtual Machine Operator custom role.</span></span>

![JSON - Modifica della definizione di ruolo personalizzata - Schermata](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Impostazione dei ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="57bc3-172">Eliminare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="57bc3-172">Delete a custom role</span></span>
<span data-ttu-id="57bc3-173">Per eliminare un ruolo personalizzato, usare prima di tutto il comando `azure role show` per determinare l' **ID** del ruolo.</span><span class="sxs-lookup"><span data-stu-id="57bc3-173">To delete a custom role, first use the `azure role show` command to determine the **ID** of the role.</span></span> <span data-ttu-id="57bc3-174">Usare quindi il comando `azure role delete` per eliminare il ruolo specificando l' **ID**.</span><span class="sxs-lookup"><span data-stu-id="57bc3-174">Then, use the `azure role delete` command to delete the role by specifying the **ID**.</span></span>

<span data-ttu-id="57bc3-175">Nell'esempio seguente viene rimosso il ruolo personalizzato *Operatore macchina virtuale* .</span><span class="sxs-lookup"><span data-stu-id="57bc3-175">The following example removes the *Virtual Machine Operator* custom role.</span></span>

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Eliminazione dei ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="57bc3-177">Elencare ruoli personalizzati</span><span class="sxs-lookup"><span data-stu-id="57bc3-177">List custom roles</span></span>
<span data-ttu-id="57bc3-178">Per elencare i ruoli disponibili per l'assegnazione a un ambito, usare il comando `azure role list` .</span><span class="sxs-lookup"><span data-stu-id="57bc3-178">To list the roles that are available for assignment at a scope, use the `azure role list` command.</span></span>

<span data-ttu-id="57bc3-179">Il comando seguente elenca tutti i ruoli disponibili per l'assegnazione nella sottoscrizione selezionata.</span><span class="sxs-lookup"><span data-stu-id="57bc3-179">The following command lists all roles that are available for assignment in the selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Elenco di ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="57bc3-181">Nell'esempio seguente il ruolo personalizzato *Virtual Machine Operator* (Operatore macchina virtuale) non è disponibile nella sottoscrizione *Production4* perché la sottoscrizione non è inclusa in **AssignableScopes** per il ruolo.</span><span class="sxs-lookup"><span data-stu-id="57bc3-181">In the following example, the *Virtual Machine Operator* custom role isn’t available in the *Production4* subscription because that subscription isn’t in the **AssignableScopes** of the role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Elenco dei ruoli di Azure per i ruoli personalizzati - Schermata](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="57bc3-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="57bc3-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

