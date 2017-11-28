---
title: aaaManage Role-Based Access Control (RBAC) with CLI di Azure | Documenti Microsoft
description: Informazioni su come interfaccia toomanage Role-Based Access Control (RBAC) with hello Azure della riga di comando dall'elenco di ruoli e ruolo azioni e assegnando ruoli toohello gli ambiti di sottoscrizione e dell'applicazione.
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
ms.openlocfilehash: 438418e5f6ee9b98908c9c264d516eb722a4e26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a><span data-ttu-id="5aea1-103">Controllare l'accesso basato sui ruoli con hello Azure interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="5aea1-103">Manage Role-Based Access Control with hello Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5aea1-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5aea1-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="5aea1-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="5aea1-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="5aea1-106">API REST</span><span class="sxs-lookup"><span data-stu-id="5aea1-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="5aea1-107">Controllo di accesso basato sui ruoli (RBAC) è possibile utilizzare nel portale di Azure hello e API di gestione risorse di Azure toomanage accesso tooyour sottoscrizione e le risorse a un livello con granularità fine.</span><span class="sxs-lookup"><span data-stu-id="5aea1-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API toomanage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="5aea1-108">Con questa funzionalità, è possibile concedere l'accesso per utenti, gruppi o entità servizio Active Directory assegnando toothem alcuni ruoli a un particolare ambito.</span><span class="sxs-lookup"><span data-stu-id="5aea1-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="5aea1-109">Prima di poter utilizzare hello Azure interfaccia della riga di comando (CLI) toomanage RBAC, è necessario disporre di hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="5aea1-109">Before you can use hello Azure command-line interface (CLI) toomanage RBAC, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="5aea1-110">Usare la versione 0.8.8 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="5aea1-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="5aea1-111">versione più recente di tooinstall hello e associare con la sottoscrizione di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5aea1-111">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="5aea1-112">Azure Resource Manager nell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="5aea1-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="5aea1-113">Andare troppo[Using hello CLI di Azure con Gestione risorse di hello](../xplat-cli-azure-resource-manager.md) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="5aea1-113">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="5aea1-114">Elenco dei ruoli</span><span class="sxs-lookup"><span data-stu-id="5aea1-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="5aea1-115">Elencare tutti i ruoli disponibili</span><span class="sxs-lookup"><span data-stu-id="5aea1-115">List all available roles</span></span>
<span data-ttu-id="5aea1-116">toolist tutti i ruoli disponibili, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="5aea1-116">toolist all available roles, use:</span></span>

        azure role list

<span data-ttu-id="5aea1-117">esempio Hello Mostra elenco hello di *tutti i ruoli disponibili*.</span><span class="sxs-lookup"><span data-stu-id="5aea1-117">hello following example shows hello list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Elenco di ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="5aea1-119">Elencare le azioni di un ruolo</span><span class="sxs-lookup"><span data-stu-id="5aea1-119">List actions of a role</span></span>
<span data-ttu-id="5aea1-120">azioni di hello toolist di un ruolo, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="5aea1-120">toolist hello actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="5aea1-121">Hello riportato di seguito azioni hello di hello *collaboratore* e *collaboratore alla macchina virtuale* ruoli.</span><span class="sxs-lookup"><span data-stu-id="5aea1-121">hello following example shows hello actions of hello *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Visualizzazione dei ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="5aea1-123">Elencare l'accesso</span><span class="sxs-lookup"><span data-stu-id="5aea1-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="5aea1-124">Elencare le assegnazioni di ruoli valide per un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="5aea1-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="5aea1-125">assegnazioni di ruolo hello toolist presenti in un gruppo di risorse, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="5aea1-125">toolist hello role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="5aea1-126">Hello esempio seguente illustra le assegnazioni di ruolo hello in hello *registrazione al pharma-vendite-projecforcast* gruppo.</span><span class="sxs-lookup"><span data-stu-id="5aea1-126">hello following example shows hello role assignments in hello *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Elenco di assegnazione di ruoli di Azure per gruppo - Schermata](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="5aea1-128">Elencare i ruoli assegnati a un utente</span><span class="sxs-lookup"><span data-stu-id="5aea1-128">List role assignments for a user</span></span>
<span data-ttu-id="5aea1-129">le assegnazioni di ruolo hello toolist per un utente specifico e le assegnazioni di hello assegnati a gruppi dell'utente tooa, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="5aea1-129">toolist hello role assignments for a specific user and hello assignments that are assigned tooa user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="5aea1-130">È inoltre possibile visualizzare le assegnazioni di ruolo vengono ereditate da gruppi modificando comando hello:</span><span class="sxs-lookup"><span data-stu-id="5aea1-130">You can also see role assignments that are inherited from groups by modifying hello command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="5aea1-131">Hello riportato di seguito le assegnazioni di ruolo hello concesse toohello  *sameert@aaddemo.com*  utente.</span><span class="sxs-lookup"><span data-stu-id="5aea1-131">hello following example shows hello role assignments that are granted toohello *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="5aea1-132">Sono inclusi i ruoli assegnati direttamente toohello utente e vengono ereditati dai gruppi.</span><span class="sxs-lookup"><span data-stu-id="5aea1-132">This includes roles that are assigned directly toohello user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Elenco di assegnazione di ruoli per utente - Schermata](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="5aea1-134">Concedere l'accesso</span><span class="sxs-lookup"><span data-stu-id="5aea1-134">Grant access</span></span>
<span data-ttu-id="5aea1-135">accesso toogrant dopo aver identificato il ruolo di hello che si desidera tooassign, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="5aea1-135">toogrant access after you have identified hello role that you want tooassign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a><span data-ttu-id="5aea1-136">Assegnare un ruolo toogroup nell'ambito di sottoscrizione hello</span><span class="sxs-lookup"><span data-stu-id="5aea1-136">Assign a role toogroup at hello subscription scope</span></span>
<span data-ttu-id="5aea1-137">tooassign un gruppo di ruoli tooa nell'ambito di sottoscrizione hello, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="5aea1-137">tooassign a role tooa group at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="5aea1-138">esempio Hello assegna hello *lettore* ruolo troppo*Team di Christine Koch* in hello *sottoscrizione* ambito.</span><span class="sxs-lookup"><span data-stu-id="5aea1-138">hello following example assigns hello *Reader* role too*Christine Koch's Team* at hello *subscription* scope.</span></span>

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Assegnazione di ruoli di Azure creata per gruppo - Schermata](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="5aea1-140">Assegnare un'applicazione tooan ruolo nell'ambito di sottoscrizione hello</span><span class="sxs-lookup"><span data-stu-id="5aea1-140">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="5aea1-141">tooassign un'applicazione tooan ruolo nell'ambito di sottoscrizione hello, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="5aea1-141">tooassign a role tooan application at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="5aea1-142">esempio Hello concede hello *collaboratore* ruolo tooan *AD Azure* applicazione hello selezionato una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5aea1-142">hello following example grants hello *Contributor* role tooan *Azure AD* application on hello selected subscription.</span></span>

 ![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Assegnazione di ruoli creata per applicazione](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="5aea1-144">Assegnare un utente tooa ruolo nell'ambito del gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="5aea1-144">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="5aea1-145">tooassign utente tooa ruolo nell'ambito di gruppo di risorse hello, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="5aea1-145">tooassign a role tooa user at hello resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="5aea1-146">esempio Hello concede hello *collaboratore alla macchina virtuale* ruolo troppo *samert@aaddemo.com*  utente hello *registrazione al Pharma-vendite-ProjectForcast* ambito del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5aea1-146">hello following example grants hello *Virtual Machine Contributor* role too*samert@aaddemo.com* user at hello *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Assegnazione di ruoli di Azure creata per utente - Schermata](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="5aea1-148">Assegnare un gruppo di tooa ruolo nell'ambito di risorsa hello</span><span class="sxs-lookup"><span data-stu-id="5aea1-148">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="5aea1-149">tooassign un gruppo di ruoli tooa nell'ambito di risorsa hello, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="5aea1-149">tooassign a role tooa group at hello resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="5aea1-150">esempio Hello concede hello *collaboratore alla macchina virtuale* ruolo tooan *AD Azure* gruppo un *subnet*.</span><span class="sxs-lookup"><span data-stu-id="5aea1-150">hello following example grants hello *Virtual Machine Contributor* role tooan *Azure AD* group on a *subnet*.</span></span>

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Assegnazione di ruoli di Azure creata per gruppo - Schermata](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="5aea1-152">Rimuovere un accesso</span><span class="sxs-lookup"><span data-stu-id="5aea1-152">Remove access</span></span>
<span data-ttu-id="5aea1-153">tooremove un'assegnazione di ruolo, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="5aea1-153">tooremove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

<span data-ttu-id="5aea1-154">esempio Hello rimuove hello *collaboratore alla macchina virtuale* assegnazione di ruolo da hello  *sammert@aaddemo.com*  utente hello *registrazione al Pharma-vendite-ProjectForcast* gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5aea1-154">hello following example removes hello *Virtual Machine Contributor* role assignment from hello *sammert@aaddemo.com* user on hello *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="5aea1-155">esempio Hello rimuove quindi l'assegnazione di ruolo hello da un gruppo sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="5aea1-155">hello example then removes hello role assignment from a group on hello subscription.</span></span>

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Eliminazione dell'assegnazione di ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="5aea1-157">Creare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="5aea1-157">Create a custom role</span></span>
<span data-ttu-id="5aea1-158">toocreate un ruolo personalizzato, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="5aea1-158">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="5aea1-159">esempio Hello crea un ruolo personalizzato chiamato *operatore macchina virtuale*.</span><span class="sxs-lookup"><span data-stu-id="5aea1-159">hello following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="5aea1-160">Concede l'accesso tooall leggere le operazioni di questo ruolo personalizzato *Microsoft. COMPUTE*, *Microsoft.Storage*, e *Network* provider e concede l'accesso alla risorsa toostart, riavviare e monitorare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5aea1-160">This custom role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="5aea1-161">Questo ruolo personalizzato può essere usato in due sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="5aea1-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="5aea1-162">In questo esempio viene usato un file JSON come input.</span><span class="sxs-lookup"><span data-stu-id="5aea1-162">This example uses a JSON file as an input.</span></span>

![JSON - Definizione di ruolo personalizzato - Schermata](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Creazione di ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="5aea1-165">Modificare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="5aea1-165">Modify a custom role</span></span>
<span data-ttu-id="5aea1-166">toomodify un ruolo personalizzato, utilizzare innanzitutto hello `azure role show` la definizione di ruolo tooretrieve del comando.</span><span class="sxs-lookup"><span data-stu-id="5aea1-166">toomodify a custom role, first use hello `azure role show` command tooretrieve role definition.</span></span> <span data-ttu-id="5aea1-167">In secondo luogo, verificare i file di definizione ruolo toohello hello modifiche desiderate.</span><span class="sxs-lookup"><span data-stu-id="5aea1-167">Second, make hello desired changes toohello role definition file.</span></span> <span data-ttu-id="5aea1-168">Infine, utilizzare `azure role set` toosave hello Modifica definizione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="5aea1-168">Finally, use `azure role set` toosave hello modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="5aea1-169">esempio Hello aggiunge hello *Microsoft.Insights/diagnosticSettings/* operazione toohello **azioni**, toohello una sottoscrizione di Azure e **AssignableScopes**di ruolo personalizzata di hello operatore macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5aea1-169">hello following example adds hello *Microsoft.Insights/diagnosticSettings/* operation toohello **Actions**, and an Azure subscription toohello **AssignableScopes** of hello Virtual Machine Operator custom role.</span></span>

![JSON - Modifica della definizione di ruolo personalizzata - Schermata](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Impostazione dei ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="5aea1-172">Eliminare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="5aea1-172">Delete a custom role</span></span>
<span data-ttu-id="5aea1-173">toodelete un ruolo personalizzato, utilizzare innanzitutto hello `azure role show` comando toodetermine hello **ID** del ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="5aea1-173">toodelete a custom role, first use hello `azure role show` command toodetermine hello **ID** of hello role.</span></span> <span data-ttu-id="5aea1-174">Utilizzare quindi hello `azure role delete` ruolo hello toodelete di comando specificando hello **ID**.</span><span class="sxs-lookup"><span data-stu-id="5aea1-174">Then, use hello `azure role delete` command toodelete hello role by specifying hello **ID**.</span></span>

<span data-ttu-id="5aea1-175">esempio Hello rimuove hello *operatore macchina virtuale* ruolo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="5aea1-175">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Eliminazione dei ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="5aea1-177">Elencare ruoli personalizzati</span><span class="sxs-lookup"><span data-stu-id="5aea1-177">List custom roles</span></span>
<span data-ttu-id="5aea1-178">i ruoli di hello toolist che sono disponibili per l'assegnazione a un ambito, usano hello `azure role list` comando.</span><span class="sxs-lookup"><span data-stu-id="5aea1-178">toolist hello roles that are available for assignment at a scope, use hello `azure role list` command.</span></span>

<span data-ttu-id="5aea1-179">Hello comando seguente elenca tutti i ruoli che sono disponibili per l'assegnazione nella sottoscrizione hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="5aea1-179">hello following command lists all roles that are available for assignment in hello selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Elenco di ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="5aea1-181">Nell'esempio seguente di hello, hello *operatore macchina virtuale* ruolo personalizzato non è disponibile in hello *Production4* sottoscrizione perché tale sottoscrizione non è in hello  **AssignableScopes** del ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="5aea1-181">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Elenco dei ruoli di Azure per i ruoli personalizzati - Schermata](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="5aea1-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5aea1-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

