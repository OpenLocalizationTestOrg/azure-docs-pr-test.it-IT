---
title: aaaAdd proprietari e utenti in Azure DevTest Labs | Documenti Microsoft
description: Aggiungere proprietari e utenti in Azure DevTest Labs con hello portale di Azure o PowerShell
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="2a0d6-103">Aggiungere proprietari e utenti in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2a0d6-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="2a0d6-104">L'accesso in Azure DevTest Labs è controllato dal [Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="2a0d6-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="2a0d6-105">Usa tale controllo, è possibile isolare il compiti all'interno del team in *ruoli* in cui si quantità di concessioni solo hello di accesso necessarie toousers tooperform il proprio lavoro.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only hello amount of access necessary toousers tooperform their jobs.</span></span> <span data-ttu-id="2a0d6-106">Tre di questi ruoli Controllo degli accessi in base al ruolo sono *Proprietario*, *Utente DevTest Labs* e *Collaboratore*.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="2a0d6-107">In questo articolo viene illustrato quali azioni possono essere eseguite in ciascuno dei tre ruoli RBAC principali hello.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-107">In this article, you learn what actions can be performed in each of hello three main RBAC roles.</span></span> <span data-ttu-id="2a0d6-108">Da qui, si apprenderà come entrambi tramite lab tooa agli utenti di tooadd - hello portale e tramite uno script di PowerShell, e come gli utenti tooadd hello livello di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-108">From there, you learn how tooadd users tooa lab - both via hello portal and via a PowerShell script, and how tooadd users at hello subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="2a0d6-109">Azioni che possono essere eseguite in ogni ruolo</span><span class="sxs-lookup"><span data-stu-id="2a0d6-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="2a0d6-110">Esistono tre ruoli principali che è possibile assegnare a un utente:</span><span class="sxs-lookup"><span data-stu-id="2a0d6-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="2a0d6-111">Proprietario</span><span class="sxs-lookup"><span data-stu-id="2a0d6-111">Owner</span></span>
* <span data-ttu-id="2a0d6-112">Utente DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2a0d6-112">DevTest Labs User</span></span>
* <span data-ttu-id="2a0d6-113">Collaboratore</span><span class="sxs-lookup"><span data-stu-id="2a0d6-113">Contributor</span></span>

<span data-ttu-id="2a0d6-114">Hello nella tabella seguente vengono illustrate le azioni che possono essere eseguite dagli utenti in ciascuno di questi ruoli hello:</span><span class="sxs-lookup"><span data-stu-id="2a0d6-114">hello following table illustrates hello actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="2a0d6-115">**Azioni che gli utenti in questo ruolo possono eseguire**</span><span class="sxs-lookup"><span data-stu-id="2a0d6-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="2a0d6-116">**Utente DevTest Labs**</span><span class="sxs-lookup"><span data-stu-id="2a0d6-116">**DevTest Labs User**</span></span> | <span data-ttu-id="2a0d6-117">**Proprietario**</span><span class="sxs-lookup"><span data-stu-id="2a0d6-117">**Owner**</span></span> | <span data-ttu-id="2a0d6-118">**Collaboratore**</span><span class="sxs-lookup"><span data-stu-id="2a0d6-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2a0d6-119">**Attività lab**</span><span class="sxs-lookup"><span data-stu-id="2a0d6-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="2a0d6-120">Aggiungere lab tooa utenti</span><span class="sxs-lookup"><span data-stu-id="2a0d6-120">Add users tooa lab</span></span> |<span data-ttu-id="2a0d6-121">No</span><span class="sxs-lookup"><span data-stu-id="2a0d6-121">No</span></span> |<span data-ttu-id="2a0d6-122">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-122">Yes</span></span> |<span data-ttu-id="2a0d6-123">No</span><span class="sxs-lookup"><span data-stu-id="2a0d6-123">No</span></span> |
| <span data-ttu-id="2a0d6-124">Aggiornare le impostazioni dei costi</span><span class="sxs-lookup"><span data-stu-id="2a0d6-124">Update cost settings</span></span> |<span data-ttu-id="2a0d6-125">No</span><span class="sxs-lookup"><span data-stu-id="2a0d6-125">No</span></span> |<span data-ttu-id="2a0d6-126">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-126">Yes</span></span> |<span data-ttu-id="2a0d6-127">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-127">Yes</span></span> |
| <span data-ttu-id="2a0d6-128">**Attività di base delle VM**</span><span class="sxs-lookup"><span data-stu-id="2a0d6-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="2a0d6-129">Aggiungere e rimuovere immagini personalizzate</span><span class="sxs-lookup"><span data-stu-id="2a0d6-129">Add and remove custom images</span></span> |<span data-ttu-id="2a0d6-130">No</span><span class="sxs-lookup"><span data-stu-id="2a0d6-130">No</span></span> |<span data-ttu-id="2a0d6-131">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-131">Yes</span></span> |<span data-ttu-id="2a0d6-132">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-132">Yes</span></span> |
| <span data-ttu-id="2a0d6-133">Aggiungere, aggiornare ed eliminare formule</span><span class="sxs-lookup"><span data-stu-id="2a0d6-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="2a0d6-134">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-134">Yes</span></span> |<span data-ttu-id="2a0d6-135">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-135">Yes</span></span> |<span data-ttu-id="2a0d6-136">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-136">Yes</span></span> |
| <span data-ttu-id="2a0d6-137">Aggiungere all'elenco elementi consentiti le immagini di Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="2a0d6-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="2a0d6-138">No</span><span class="sxs-lookup"><span data-stu-id="2a0d6-138">No</span></span> |<span data-ttu-id="2a0d6-139">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-139">Yes</span></span> |<span data-ttu-id="2a0d6-140">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-140">Yes</span></span> |
| <span data-ttu-id="2a0d6-141">**Attività della macchina virtuale**</span><span class="sxs-lookup"><span data-stu-id="2a0d6-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="2a0d6-142">Creare VM</span><span class="sxs-lookup"><span data-stu-id="2a0d6-142">Create VMs</span></span> |<span data-ttu-id="2a0d6-143">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-143">Yes</span></span> |<span data-ttu-id="2a0d6-144">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-144">Yes</span></span> |<span data-ttu-id="2a0d6-145">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-145">Yes</span></span> |
| <span data-ttu-id="2a0d6-146">Avviare, arrestare ed eliminare VM</span><span class="sxs-lookup"><span data-stu-id="2a0d6-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="2a0d6-147">Solo macchine virtuali create dall'utente hello</span><span class="sxs-lookup"><span data-stu-id="2a0d6-147">Only VMs created by hello user</span></span> |<span data-ttu-id="2a0d6-148">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-148">Yes</span></span> |<span data-ttu-id="2a0d6-149">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-149">Yes</span></span> |
| <span data-ttu-id="2a0d6-150">Aggiornare i criteri delle VM</span><span class="sxs-lookup"><span data-stu-id="2a0d6-150">Update VM policies</span></span> |<span data-ttu-id="2a0d6-151">No</span><span class="sxs-lookup"><span data-stu-id="2a0d6-151">No</span></span> |<span data-ttu-id="2a0d6-152">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-152">Yes</span></span> |<span data-ttu-id="2a0d6-153">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-153">Yes</span></span> |
| <span data-ttu-id="2a0d6-154">Aggiungere/Rimuovere dischi dati nelle VM</span><span class="sxs-lookup"><span data-stu-id="2a0d6-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="2a0d6-155">Solo macchine virtuali create dall'utente hello</span><span class="sxs-lookup"><span data-stu-id="2a0d6-155">Only VMs created by hello user</span></span> |<span data-ttu-id="2a0d6-156">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-156">Yes</span></span> |<span data-ttu-id="2a0d6-157">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-157">Yes</span></span> |
| <span data-ttu-id="2a0d6-158">**Attività degli elementi**</span><span class="sxs-lookup"><span data-stu-id="2a0d6-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="2a0d6-159">Aggiungere e rimuovere repository di elementi</span><span class="sxs-lookup"><span data-stu-id="2a0d6-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="2a0d6-160">No</span><span class="sxs-lookup"><span data-stu-id="2a0d6-160">No</span></span> |<span data-ttu-id="2a0d6-161">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-161">Yes</span></span> |<span data-ttu-id="2a0d6-162">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-162">Yes</span></span> |
| <span data-ttu-id="2a0d6-163">Applicare elementi</span><span class="sxs-lookup"><span data-stu-id="2a0d6-163">Apply artifacts</span></span> |<span data-ttu-id="2a0d6-164">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-164">Yes</span></span> |<span data-ttu-id="2a0d6-165">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-165">Yes</span></span> |<span data-ttu-id="2a0d6-166">Sì</span><span class="sxs-lookup"><span data-stu-id="2a0d6-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="2a0d6-167">Quando un utente crea una macchina virtuale, tale utente viene assegnato automaticamente toohello **proprietario** ruolo di macchina virtuale creata hello.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-167">When a user creates a VM, that user is automatically assigned toohello **Owner** role of hello created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a><span data-ttu-id="2a0d6-168">Aggiungere un proprietario o un utente a livello di hello lab</span><span class="sxs-lookup"><span data-stu-id="2a0d6-168">Add an owner or user at hello lab level</span></span>
<span data-ttu-id="2a0d6-169">I proprietari e gli utenti possono essere aggiunti al livello di lab hello tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-169">Owners and users can be added at hello lab level via hello Azure portal.</span></span> <span data-ttu-id="2a0d6-170">Sono inclusi gli utenti esterni con un [account Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account)valido.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="2a0d6-171">Hello alla procedura seguente consentono di eseguire il processo di hello di aggiunta di un ambiente lab tooa proprietario o l'utente in Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="2a0d6-171">hello following steps guide you through hello process of adding an owner or user tooa lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="2a0d6-172">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="2a0d6-172">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="2a0d6-173">Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-173">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="2a0d6-174">Elenco dei laboratori hello selezionare lab desiderato hello.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-174">From hello list of labs, select hello desired lab.</span></span>
4. <span data-ttu-id="2a0d6-175">Nel pannello del lab hello, selezionare **configurazione**.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-175">On hello lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="2a0d6-176">In hello **configurazione** pannello seleziona **utenti**.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-176">On hello **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="2a0d6-177">In hello **utenti** pannello seleziona **+ Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-177">On hello **Users** blade, select **+Add**.</span></span>
   
    ![Add user](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="2a0d6-179">In hello **selezionare un ruolo** blade, ruolo desiderato selezionare hello.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-179">On hello **Select a role** blade, select hello desired role.</span></span> <span data-ttu-id="2a0d6-180">Hello sezione [azioni che possono essere eseguite in ogni ruolo](#actions-that-can-be-performed-in-each-role) elenchi hello diverse azioni che possono essere eseguite dagli utenti nei ruoli di proprietario, di utente DevTest e collaboratore hello.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-180">hello section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists hello various actions that can be performed by users in hello Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="2a0d6-181">In hello **aggiungere utenti** pannello, immettere l'indirizzo di posta elettronica hello o il nome dell'utente di hello si vuole tooadd nel ruolo hello è specificato.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-181">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd in hello role you specified.</span></span> <span data-ttu-id="2a0d6-182">Se non è possibile trovare l'utente hello, un messaggio di errore viene illustrato il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-182">If hello user can't be found, an error message explains hello issue.</span></span> <span data-ttu-id="2a0d6-183">Se l'utente hello viene trovato, tale utente sia elencato e selezionato.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-183">If hello user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="2a0d6-184">Scegliere **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-184">Select **Select**.</span></span>
10. <span data-ttu-id="2a0d6-185">Selezionare **OK** tooclose hello **aggiungere accesso** blade.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-185">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="2a0d6-186">Quando si torna toohello **utenti** pannello hello utente è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-186">When you return toohello **Users** blade, hello user has been added.</span></span>  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a><span data-ttu-id="2a0d6-187">Aggiungere un ambiente lab tooa utente esterno tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a0d6-187">Add an external user tooa lab using PowerShell</span></span>
<span data-ttu-id="2a0d6-188">Inoltre gli utenti tooadding hello portale di Azure, è possibile aggiungere un ambiente lab tooyour utente esterno utilizzando uno script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-188">In addition tooadding users in hello Azure portal, you can add an external user tooyour lab using a PowerShell script.</span></span> <span data-ttu-id="2a0d6-189">In hello seguente esempio, è sufficiente modificare i valori dei parametri hello in hello **toochange valori** commento.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-189">In hello following example, simply modify hello parameter values under hello **Values toochange** comment.</span></span>
<span data-ttu-id="2a0d6-190">È possibile recuperare hello `subscriptionId`, `labResourceGroup`, e `labName` valori dal pannello lab hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-190">You can retrieve hello `subscriptionId`, `labResourceGroup`, and `labName` values from hello lab blade in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="2a0d6-191">script di esempio Hello si presuppone che hello specificato l'utente è stato aggiunto come un toohello guest Active Directory e avrà esito negativo se non è questo caso di hello.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-191">hello sample script assumes that hello specified user has been added as a guest toohello Active Directory, and will fail if that is not hello case.</span></span> <span data-ttu-id="2a0d6-192">tooadd un utente non hello lab tooa Active Directory, utilizzare ruolo tooa di hello tooassign portale Azure hello utente come illustrato nella sezione hello, [aggiungere un proprietario o un utente a livello di lab hello](#add-an-owner-or-user-at-the-lab-level).</span><span class="sxs-lookup"><span data-stu-id="2a0d6-192">tooadd a user not in hello Active Directory tooa lab, use hello Azure portal tooassign hello user tooa role as illustrated in hello section, [Add an owner or user at hello lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a><span data-ttu-id="2a0d6-193">Aggiungere un proprietario o un utente a livello di sottoscrizione hello</span><span class="sxs-lookup"><span data-stu-id="2a0d6-193">Add an owner or user at hello subscription level</span></span>
<span data-ttu-id="2a0d6-194">Autorizzazioni di Azure vengono propagate dall'ambito di toochild ambito padre in Azure.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-194">Azure permissions are propagated from parent scope toochild scope in Azure.</span></span> <span data-ttu-id="2a0d6-195">Quindi i proprietari di una sottoscrizione di Azure contenente lab sono automaticamente proprietari di tali lab.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="2a0d6-196">Possiedono anche le macchine virtuali hello e altre risorse create da utenti dell'ambiente di test di hello e servizio Azure DevTest Labs hello.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-196">They also own hello VMs and other resources created by hello lab's users, and hello Azure DevTest Labs service.</span></span> 

<span data-ttu-id="2a0d6-197">È possibile aggiungere lab tooa proprietari aggiuntivi tramite il pannello del lab hello in hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="2a0d6-197">You can add additional owners tooa lab via hello lab's blade in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="2a0d6-198">Tuttavia, hello aggiunta ambiti del proprietario di amministrazione non sono più ampia di ambito del proprietario della sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-198">However, hello added owner's scope of administration is more narrow than hello subscription owner's scope.</span></span> <span data-ttu-id="2a0d6-199">Ad esempio hello aggiunta di proprietari non dispone di accesso completo toosome delle risorse di hello che vengono creati nella sottoscrizione hello hello servizio DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-199">For example, hello added owners do not have full access toosome of hello resources that are created in hello subscription by hello DevTest Labs service.</span></span> 

<span data-ttu-id="2a0d6-200">tooadd un tooan proprietario sottoscrizione di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="2a0d6-200">tooadd an owner tooan Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="2a0d6-201">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="2a0d6-201">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="2a0d6-202">Selezionare **più servizi**, quindi selezionare **sottoscrizioni** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-202">Select **More Services**, and then select **Subscriptions** from hello list.</span></span>
3. <span data-ttu-id="2a0d6-203">Selezionare la sottoscrizione hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-203">Select hello desired subscription.</span></span>
4. <span data-ttu-id="2a0d6-204">Selezionare l'icona **Accesso** .</span><span class="sxs-lookup"><span data-stu-id="2a0d6-204">Select **Access** icon.</span></span> 
   
    ![Utenti di accesso](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="2a0d6-206">In hello **utenti** pannello seleziona **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-206">On hello **Users** blade, select **Add**.</span></span>
   
    ![Add user](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="2a0d6-208">In hello **selezionare un ruolo** pannello selezionare **proprietario**.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-208">On hello **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="2a0d6-209">In hello **aggiungere utenti** pannello, immettere l'indirizzo di posta elettronica hello o il nome dell'utente hello desiderato tooadd come proprietario.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-209">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd as an owner.</span></span> <span data-ttu-id="2a0d6-210">Se l'utente hello non viene trovato, viene visualizzato un messaggio di errore che spiega il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-210">If hello user can't be found, you get an error message explaining hello issue.</span></span> <span data-ttu-id="2a0d6-211">Se l'utente hello viene trovato, tale utente è elencato in hello **utente** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-211">If hello user is found, that user is listed under hello **User** text box.</span></span>
8. <span data-ttu-id="2a0d6-212">Selezionare il nome di un utente si trova hello.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-212">Select hello located user name.</span></span>
9. <span data-ttu-id="2a0d6-213">Scegliere **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-213">Select **Select**.</span></span>
10. <span data-ttu-id="2a0d6-214">Selezionare **OK** tooclose hello **aggiungere accesso** blade.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-214">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="2a0d6-215">Quando si torna toohello **utenti** pannello hello utente è stato aggiunto come proprietario.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-215">When you return toohello **Users** blade, hello user has been added as an owner.</span></span> <span data-ttu-id="2a0d6-216">L'utente è ora un proprietario di un lab creato in questa sottoscrizione e pertanto essere tooperform in grado di attività di proprietario.</span><span class="sxs-lookup"><span data-stu-id="2a0d6-216">This user is now an owner of any labs created under this subscription, and thus be able tooperform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

