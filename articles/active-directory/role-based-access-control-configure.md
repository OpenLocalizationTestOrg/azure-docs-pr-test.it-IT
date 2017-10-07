---
title: Controllo di accesso basato su aaaRole nel portale di Azure hello | Documenti Microsoft
description: Guida introduttiva nella gestione degli accessi in base al ruolo di controllo di accesso in hello portale di Azure. Utilizzare le risorse tooyour le autorizzazioni di ruolo assegnazioni tooassign.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a><span data-ttu-id="67cd9-104">Utilizzo delle risorse di controllo di accesso basato sui ruoli toomanage accesso tooyour sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="67cd9-104">Use Role-Based Access Control toomanage access tooyour Azure subscription resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="67cd9-105">Gestire l'accesso per utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="67cd9-105">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="67cd9-106">Gestire l'accesso per risorsa</span><span class="sxs-lookup"><span data-stu-id="67cd9-106">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="67cd9-107">Il Controllo degli accessi in base al ruolo di Azure (RBAC) consente la gestione specifica degli accessi per Azure.</span><span class="sxs-lookup"><span data-stu-id="67cd9-107">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="67cd9-108">Usa tale controllo, è possibile concedere solo quantità di hello di accesso che gli utenti devono tooperform i processi.</span><span class="sxs-lookup"><span data-stu-id="67cd9-108">Using RBAC, you can grant only hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="67cd9-109">In questo articolo consente di ottenere attivo e in esecuzione con RBAC in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="67cd9-109">This article helps you get up and running with RBAC in hello Azure portal.</span></span> <span data-ttu-id="67cd9-110">Per altri dettagli sulla gestione degli accessi, vedere l'articolo relativo al [Controllo degli accessi in base al ruolo](role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="67cd9-110">If you want more details about how RBAC helps you manage access, see [What is Role-Based Access Control](role-based-access-control-what-is.md).</span></span>

<span data-ttu-id="67cd9-111">All'interno di ogni sottoscrizione, è possibile concedere le assegnazioni di ruolo too2000.</span><span class="sxs-lookup"><span data-stu-id="67cd9-111">Within each subscription, you can grant up too2000 role assignments.</span></span> 

## <a name="view-access"></a><span data-ttu-id="67cd9-112">Visualizzare l'accesso</span><span class="sxs-lookup"><span data-stu-id="67cd9-112">View access</span></span>
<span data-ttu-id="67cd9-113">È possibile vedere chi ha accesso tooa risorsa, gruppo di risorse o sottoscrizione dal pannello principale in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="67cd9-113">You can see who has access tooa resource, resource group, or subscription from its main blade in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="67cd9-114">Ad esempio, è necessario toosee che dispone di accesso tooone i gruppi di risorse:</span><span class="sxs-lookup"><span data-stu-id="67cd9-114">For example, we want toosee who has access tooone of our resource groups:</span></span>

1. <span data-ttu-id="67cd9-115">Selezionare **gruppi di risorse** hello sinistra sulla barra di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="67cd9-115">Select **Resource groups** in hello navigation bar on hello left.</span></span>  
    <span data-ttu-id="67cd9-116">![Gruppi di risorse, icona](./media/role-based-access-control-configure/resourcegroups_icon.png)</span><span class="sxs-lookup"><span data-stu-id="67cd9-116">![Resource groups - icon](./media/role-based-access-control-configure/resourcegroups_icon.png)</span></span>
2. <span data-ttu-id="67cd9-117">Nome hello selezionare hello del gruppo di risorse da hello **gruppi di risorse** blade.</span><span class="sxs-lookup"><span data-stu-id="67cd9-117">Select hello name of hello resource group from hello **Resource groups** blade.</span></span>
3. <span data-ttu-id="67cd9-118">Selezionare **Access control (IAM)** dal menu a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="67cd9-118">Select **Access control (IAM)** from hello left menu.</span></span>  
4. <span data-ttu-id="67cd9-119">Pannello di controllo di accesso Hello Elenca tutti gli utenti, gruppi e le applicazioni che sono state concesse gruppo di risorse toohello di accesso.</span><span class="sxs-lookup"><span data-stu-id="67cd9-119">hello Access control blade lists all users, groups, and applications that have been granted access toohello resource group.</span></span>  
   
    ![Screenshot del pannello Utenti: accesso ereditato e assegnato](./media/role-based-access-control-configure/view-access.png)

<span data-ttu-id="67cd9-121">Si noti che l'ambito di alcuni ruoli sono troppo**questa risorsa** mentre altri sono **Inherited** da un altro ambito.</span><span class="sxs-lookup"><span data-stu-id="67cd9-121">Notice that some roles are scoped too**This resource** while others are **Inherited** it from another scope.</span></span> <span data-ttu-id="67cd9-122">L'accesso è assegnato in modo specifico il gruppo di risorse toohello o ereditato da una sottoscrizione di assegnazione toohello padre.</span><span class="sxs-lookup"><span data-stu-id="67cd9-122">Access is either assigned specifically toohello resource group or inherited from an assignment toohello parent subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="67cd9-123">Gli amministratori delle sottoscrizioni classico e coamministratori sono considerati proprietari della sottoscrizione hello nel nuovo modello di RBAC hello.</span><span class="sxs-lookup"><span data-stu-id="67cd9-123">Classic subscription admins and co-admins are considered owners of hello subscription in hello new RBAC model.</span></span>

## <a name="add-access"></a><span data-ttu-id="67cd9-124">Aggiungere un accesso</span><span class="sxs-lookup"><span data-stu-id="67cd9-124">Add Access</span></span>
<span data-ttu-id="67cd9-125">È concedere accesso dall'interno sottoscrizione ambito hello hello assegnazione di ruolo, gruppo di risorse o risorse hello.</span><span class="sxs-lookup"><span data-stu-id="67cd9-125">You grant access from within hello resource, resource group, or subscription that is hello scope of hello role assignment.</span></span>

1. <span data-ttu-id="67cd9-126">Selezionare **Aggiungi** nel Pannello di controllo di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="67cd9-126">Select **Add** on hello Access control blade.</span></span>  
2. <span data-ttu-id="67cd9-127">Ruolo selezionare hello che si desidera tooassign da hello **selezionare un ruolo** blade.</span><span class="sxs-lookup"><span data-stu-id="67cd9-127">Select hello role that you wish tooassign from hello **Select a role** blade.</span></span>
3. <span data-ttu-id="67cd9-128">Selezionare hello utente, gruppo o dell'applicazione nella directory che si desidera toogrant accesso a.</span><span class="sxs-lookup"><span data-stu-id="67cd9-128">Select hello user, group, or application in your directory that you wish toogrant access to.</span></span> <span data-ttu-id="67cd9-129">È possibile cercare la directory hello con i nomi visualizzati, indirizzi di posta elettronica e gli identificatori di oggetto.</span><span class="sxs-lookup"><span data-stu-id="67cd9-129">You can search hello directory with display names, email addresses, and object identifiers.</span></span>  
   
    ![Screenshot del pannello Aggiungi utenti: casella di ricerca](./media/role-based-access-control-configure/grant-access2.png)
4. <span data-ttu-id="67cd9-131">Selezionare **OK** assegnazione hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="67cd9-131">Select **OK** toocreate hello assignment.</span></span> <span data-ttu-id="67cd9-132">Hello **aggiunta utente** popup tiene traccia dell'avanzamento di hello.</span><span class="sxs-lookup"><span data-stu-id="67cd9-132">hello **Adding user** popup tracks hello progress.</span></span>  
    <span data-ttu-id="67cd9-133">![Indicatore di stato dell'aggiunta di utenti, schermata](./media/role-based-access-control-configure/addinguser_popup.png)</span><span class="sxs-lookup"><span data-stu-id="67cd9-133">![Adding user progress bar - screenshot](./media/role-based-access-control-configure/addinguser_popup.png)</span></span>

<span data-ttu-id="67cd9-134">Dopo aver aggiunto correttamente un'assegnazione di ruolo, che verrà visualizzata nella hello **utenti** blade.</span><span class="sxs-lookup"><span data-stu-id="67cd9-134">After successfully adding a role assignment, it will appear on hello **Users** blade.</span></span>

## <a name="remove-access"></a><span data-ttu-id="67cd9-135">Rimuovere un accesso</span><span class="sxs-lookup"><span data-stu-id="67cd9-135">Remove Access</span></span>
1. <span data-ttu-id="67cd9-136">Posiziona il cursore sul nome hello di assegnazione di hello che si desidera tooremove.</span><span class="sxs-lookup"><span data-stu-id="67cd9-136">Hover your cursor over hello name of hello assignment that you want tooremove.</span></span> <span data-ttu-id="67cd9-137">Una casella di controllo viene visualizzato il nome toohello successivo.</span><span class="sxs-lookup"><span data-stu-id="67cd9-137">A check box appears next toohello name.</span></span>
2. <span data-ttu-id="67cd9-138">Utilizzare hello caselle di controllo tooselect uno o più assegnazioni di ruolo.</span><span class="sxs-lookup"><span data-stu-id="67cd9-138">Use hello check boxes tooselect one or more role assignments.</span></span>
2. <span data-ttu-id="67cd9-139">Selezionare **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="67cd9-139">Select **Remove**.</span></span>  
3. <span data-ttu-id="67cd9-140">Selezionare **Sì** rimozione hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="67cd9-140">Select **Yes** tooconfirm hello removal.</span></span>

<span data-ttu-id="67cd9-141">Le assegnazioni ereditate non possono essere rimosse.</span><span class="sxs-lookup"><span data-stu-id="67cd9-141">Inherited assignments cannot be removed.</span></span> <span data-ttu-id="67cd9-142">Se è necessario tooremove un'assegnazione ereditata, è necessario toodo in hello ambito in cui è stato creato l'assegnazione di ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="67cd9-142">If you need tooremove an inherited assignment, you need toodo it at hello scope where hello role assignment was created.</span></span> <span data-ttu-id="67cd9-143">In hello **ambito** colonna, accanto troppo**Inherited** è presente un collegamento che consente di passare toohello risorse in cui è stato assegnato questo ruolo.</span><span class="sxs-lookup"><span data-stu-id="67cd9-143">In hello **Scope** column, next too**Inherited** there is a link that takes you toohello resources where this role was assigned.</span></span> <span data-ttu-id="67cd9-144">Passare toohello risorse elencate assegnazione di ruolo tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="67cd9-144">Go toohello resource listed there tooremove hello role assignment.</span></span>

![Screenshot del pannello Utenti: l'accesso ereditato disabilita il pulsante Rimuovi](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a><span data-ttu-id="67cd9-146">Accesso toomanage altri strumenti</span><span class="sxs-lookup"><span data-stu-id="67cd9-146">Other tools toomanage access</span></span>
<span data-ttu-id="67cd9-147">È possibile assegnare i ruoli e gestire l'accesso con i comandi di Azure RBAC in strumenti diversi da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="67cd9-147">You can assign roles and manage access with Azure RBAC commands in tools other than hello Azure portal.</span></span>  <span data-ttu-id="67cd9-148">Seguire hello collegamenti toolearn informazioni sui prerequisiti hello e iniziare a utilizzare i comandi di Azure RBAC hello.</span><span class="sxs-lookup"><span data-stu-id="67cd9-148">Follow hello links toolearn more about hello prerequisites and get started with hello Azure RBAC commands.</span></span>

* [<span data-ttu-id="67cd9-149">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="67cd9-149">Azure PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
* [<span data-ttu-id="67cd9-150">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="67cd9-150">Azure Command-Line Interface</span></span>](role-based-access-control-manage-access-azure-cli.md)
* [<span data-ttu-id="67cd9-151">API REST</span><span class="sxs-lookup"><span data-stu-id="67cd9-151">REST API</span></span>](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a><span data-ttu-id="67cd9-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67cd9-152">Next Steps</span></span>
* [<span data-ttu-id="67cd9-153">Creare un report della cronologia delle modifiche relative all'accesso</span><span class="sxs-lookup"><span data-stu-id="67cd9-153">Create an access change history report</span></span>](role-based-access-control-access-change-history-report.md)
* <span data-ttu-id="67cd9-154">Vedere hello [ruoli predefiniti RBAC](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="67cd9-154">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>
* <span data-ttu-id="67cd9-155">Definire i [ruoli personalizzati nel Controllo degli accessi in base al ruolo di Azure](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="67cd9-155">Define your own [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>

