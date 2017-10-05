---
title: Controllo degli accessi in base al ruolo nel portale di Azure | Microsoft Docs
description: Introduzione alla gestione degli accessi con il Controllo degli accessi in base al ruolo nel portale di Azure. Usare le assegnazioni di ruolo per assegnare autorizzazioni alle risorse.
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
ms.openlocfilehash: 9df7f7851ef1fc6b4ed03b981aa5062d6b0913ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-role-based-access-control-to-manage-access-to-your-azure-subscription-resources"></a><span data-ttu-id="e113b-104">Usare il controllo degli accessi in base al ruolo per gestire l'accesso alle risorse della sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="e113b-104">Use Role-Based Access Control to manage access to your Azure subscription resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e113b-105">Gestire l'accesso per utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="e113b-105">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="e113b-106">Gestire l'accesso per risorsa</span><span class="sxs-lookup"><span data-stu-id="e113b-106">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="e113b-107">Il Controllo degli accessi in base al ruolo di Azure (RBAC) consente la gestione specifica degli accessi per Azure.</span><span class="sxs-lookup"><span data-stu-id="e113b-107">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="e113b-108">L'uso del Controllo degli accessi in base al ruolo permette di concedere agli utenti solo il livello di accesso necessario per lavorare.</span><span class="sxs-lookup"><span data-stu-id="e113b-108">Using RBAC, you can grant only the amount of access that users need to perform their jobs.</span></span> <span data-ttu-id="e113b-109">Questo articolo permette di iniziare subito a usare il Controllo degli accessi in base al ruolo nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e113b-109">This article helps you get up and running with RBAC in the Azure portal.</span></span> <span data-ttu-id="e113b-110">Per altri dettagli sulla gestione degli accessi, vedere l'articolo relativo al [Controllo degli accessi in base al ruolo](role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="e113b-110">If you want more details about how RBAC helps you manage access, see [What is Role-Based Access Control](role-based-access-control-what-is.md).</span></span>

<span data-ttu-id="e113b-111">In ogni sottoscrizione è possibile concedere fino a 2000 assegnazioni di ruolo.</span><span class="sxs-lookup"><span data-stu-id="e113b-111">Within each subscription, you can grant up to 2000 role assignments.</span></span> 

## <a name="view-access"></a><span data-ttu-id="e113b-112">Visualizzare l'accesso</span><span class="sxs-lookup"><span data-stu-id="e113b-112">View access</span></span>
<span data-ttu-id="e113b-113">È possibile visualizzare chi ha accesso a una risorsa, a un gruppo di risorse o a una sottoscrizione dal relativo pannello principale nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e113b-113">You can see who has access to a resource, resource group, or subscription from its main blade in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e113b-114">Ad esempio, si vuole vedere chi ha accesso a uno dei gruppi di risorse:</span><span class="sxs-lookup"><span data-stu-id="e113b-114">For example, we want to see who has access to one of our resource groups:</span></span>

1. <span data-ttu-id="e113b-115">Selezionare **Gruppi di risorse** nella barra di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="e113b-115">Select **Resource groups** in the navigation bar on the left.</span></span>  
    <span data-ttu-id="e113b-116">![Gruppi di risorse, icona](./media/role-based-access-control-configure/resourcegroups_icon.png)</span><span class="sxs-lookup"><span data-stu-id="e113b-116">![Resource groups - icon](./media/role-based-access-control-configure/resourcegroups_icon.png)</span></span>
2. <span data-ttu-id="e113b-117">Selezionare il nome del gruppo di risorse nel pannello **Gruppi di risorse** .</span><span class="sxs-lookup"><span data-stu-id="e113b-117">Select the name of the resource group from the **Resource groups** blade.</span></span>
3. <span data-ttu-id="e113b-118">Selezionare **Controllo di accesso (IAM)** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="e113b-118">Select **Access control (IAM)** from the left menu.</span></span>  
4. <span data-ttu-id="e113b-119">Il pannello Controllo di accesso elenca tutti gli utenti, i gruppi e le applicazioni a cui è stato concesso l'accesso al gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e113b-119">The Access control blade lists all users, groups, and applications that have been granted access to the resource group.</span></span>  
   
    ![Screenshot del pannello Utenti: accesso ereditato e assegnato](./media/role-based-access-control-configure/view-access.png)

<span data-ttu-id="e113b-121">Si noti che l'ambito di alcuni ruoli è **Questa risorsa**, mentre quello di altri è **Ereditato** da un altro ambito.</span><span class="sxs-lookup"><span data-stu-id="e113b-121">Notice that some roles are scoped to **This resource** while others are **Inherited** it from another scope.</span></span> <span data-ttu-id="e113b-122">L'accesso viene assegnato in modo specifico al gruppo di risorse oppure ereditato da un'assegnazione nella sottoscrizione padre.</span><span class="sxs-lookup"><span data-stu-id="e113b-122">Access is either assigned specifically to the resource group or inherited from an assignment to the parent subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="e113b-123">Gli utenti con i ruoli Amministratore sottoscrizione classico e Coamministratore sono considerati proprietari della sottoscrizione nel nuovo modello Controllo degli accessi in base al ruolo.</span><span class="sxs-lookup"><span data-stu-id="e113b-123">Classic subscription admins and co-admins are considered owners of the subscription in the new RBAC model.</span></span>

## <a name="add-access"></a><span data-ttu-id="e113b-124">Aggiungere un accesso</span><span class="sxs-lookup"><span data-stu-id="e113b-124">Add Access</span></span>
<span data-ttu-id="e113b-125">Si concede l'accesso dalla risorsa, dal gruppo di risorse o dalla sottoscrizione che costituisce l'ambito dell'assegnazione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="e113b-125">You grant access from within the resource, resource group, or subscription that is the scope of the role assignment.</span></span>

1. <span data-ttu-id="e113b-126">Selezionare **Aggiungi** nel pannello Controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="e113b-126">Select **Add** on the Access control blade.</span></span>  
2. <span data-ttu-id="e113b-127">Selezionare il ruolo da assegnare nel pannello **Selezionare un ruolo** .</span><span class="sxs-lookup"><span data-stu-id="e113b-127">Select the role that you wish to assign from the **Select a role** blade.</span></span>
3. <span data-ttu-id="e113b-128">Selezionare l'utente, il gruppo o l'applicazione nella directory a cui si vuole concedere l'accesso.</span><span class="sxs-lookup"><span data-stu-id="e113b-128">Select the user, group, or application in your directory that you wish to grant access to.</span></span> <span data-ttu-id="e113b-129">È possibile cercare nella directory usando nomi visualizzati, indirizzi di posta elettronica e identificatori di oggetto.</span><span class="sxs-lookup"><span data-stu-id="e113b-129">You can search the directory with display names, email addresses, and object identifiers.</span></span>  
   
    ![Screenshot del pannello Aggiungi utenti: casella di ricerca](./media/role-based-access-control-configure/grant-access2.png)
4. <span data-ttu-id="e113b-131">Selezionare **OK** per creare l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="e113b-131">Select **OK** to create the assignment.</span></span> <span data-ttu-id="e113b-132">Il popup **Aggiunta dell'utente in corso** tiene traccia dello stato.</span><span class="sxs-lookup"><span data-stu-id="e113b-132">The **Adding user** popup tracks the progress.</span></span>  
    <span data-ttu-id="e113b-133">![Indicatore di stato dell'aggiunta di utenti, schermata](./media/role-based-access-control-configure/addinguser_popup.png)</span><span class="sxs-lookup"><span data-stu-id="e113b-133">![Adding user progress bar - screenshot](./media/role-based-access-control-configure/addinguser_popup.png)</span></span>

<span data-ttu-id="e113b-134">Dopo aver aggiunto un'assegnazione di ruolo, viene visualizzato il pannello **Utenti** .</span><span class="sxs-lookup"><span data-stu-id="e113b-134">After successfully adding a role assignment, it will appear on the **Users** blade.</span></span>

## <a name="remove-access"></a><span data-ttu-id="e113b-135">Rimuovere un accesso</span><span class="sxs-lookup"><span data-stu-id="e113b-135">Remove Access</span></span>
1. <span data-ttu-id="e113b-136">Passare il puntatore del mouse sul nome dell'assegnazione da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="e113b-136">Hover your cursor over the name of the assignment that you want to remove.</span></span> <span data-ttu-id="e113b-137">Accanto al nome verrà visualizzata una casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="e113b-137">A check box appears next to the name.</span></span>
2. <span data-ttu-id="e113b-138">Usare le caselle di controllo per selezionare una o più assegnazioni di ruolo.</span><span class="sxs-lookup"><span data-stu-id="e113b-138">Use the check boxes to select one or more role assignments.</span></span>
2. <span data-ttu-id="e113b-139">Selezionare **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="e113b-139">Select **Remove**.</span></span>  
3. <span data-ttu-id="e113b-140">Selezionare **Sì** per confermare la rimozione.</span><span class="sxs-lookup"><span data-stu-id="e113b-140">Select **Yes** to confirm the removal.</span></span>

<span data-ttu-id="e113b-141">Le assegnazioni ereditate non possono essere rimosse.</span><span class="sxs-lookup"><span data-stu-id="e113b-141">Inherited assignments cannot be removed.</span></span> <span data-ttu-id="e113b-142">Se si desidera rimuovere un'assegnazione ereditata, è necessario eseguire questa operazione laddove è stata creata l'assegnazione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="e113b-142">If you need to remove an inherited assignment, you need to do it at the scope where the role assignment was created.</span></span> <span data-ttu-id="e113b-143">Nella colonna **Ambito**, accanto a **Ereditato** è presente un collegamento che consente di visualizzare le risorse in cui è stato assegnato questo ruolo.</span><span class="sxs-lookup"><span data-stu-id="e113b-143">In the **Scope** column, next to **Inherited** there is a link that takes you to the resources where this role was assigned.</span></span> <span data-ttu-id="e113b-144">Passare alla risorsa inclusa nell'elenco per rimuovere l'assegnazione di ruolo.</span><span class="sxs-lookup"><span data-stu-id="e113b-144">Go to the resource listed there to remove the role assignment.</span></span>

![Screenshot del pannello Utenti: l'accesso ereditato disabilita il pulsante Rimuovi](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-to-manage-access"></a><span data-ttu-id="e113b-146">Altri strumenti per gestire l'accesso</span><span class="sxs-lookup"><span data-stu-id="e113b-146">Other tools to manage access</span></span>
<span data-ttu-id="e113b-147">È possibile assegnare i ruoli e gestire l'accesso con i comandi del Controllo degli accessi in base al ruolo di Azure in strumenti diversi dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e113b-147">You can assign roles and manage access with Azure RBAC commands in tools other than the Azure portal.</span></span>  <span data-ttu-id="e113b-148">Per altre informazioni sui prerequisiti e iniziare a usare i comandi del Controllo degli accessi in base al ruolo di Azure, usare i collegamenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="e113b-148">Follow the links to learn more about the prerequisites and get started with the Azure RBAC commands.</span></span>

* [<span data-ttu-id="e113b-149">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e113b-149">Azure PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
* [<span data-ttu-id="e113b-150">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e113b-150">Azure Command-Line Interface</span></span>](role-based-access-control-manage-access-azure-cli.md)
* [<span data-ttu-id="e113b-151">API REST</span><span class="sxs-lookup"><span data-stu-id="e113b-151">REST API</span></span>](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a><span data-ttu-id="e113b-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e113b-152">Next Steps</span></span>
* [<span data-ttu-id="e113b-153">Creare un report della cronologia delle modifiche relative all'accesso</span><span class="sxs-lookup"><span data-stu-id="e113b-153">Create an access change history report</span></span>](role-based-access-control-access-change-history-report.md)
* <span data-ttu-id="e113b-154">Vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="e113b-154">See the [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>
* <span data-ttu-id="e113b-155">Definire i [ruoli personalizzati nel Controllo degli accessi in base al ruolo di Azure](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="e113b-155">Define your own [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>

