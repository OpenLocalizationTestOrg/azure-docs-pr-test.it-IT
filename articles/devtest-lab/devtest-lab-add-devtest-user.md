---
title: Aggiungere proprietari e utenti in Azure DevTest Labs | Documentazione Microsoft
description: Aggiungere proprietari e utenti in Azure DevTest Labs usando il portale di Azure o PowerShell
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
ms.openlocfilehash: d67fa257574d6cb4ad4b18521900374fb51da290
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="ff451-103">Aggiungere proprietari e utenti in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ff451-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="ff451-104">L'accesso in Azure DevTest Labs è controllato dal [Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="ff451-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="ff451-105">Usando il Controllo degli accessi in base al ruolo, è possibile separare i compiti del team in *ruoli* in cui si concede solo la quantità di accesso necessaria agli utenti per svolgere il proprio lavoro.</span><span class="sxs-lookup"><span data-stu-id="ff451-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only the amount of access necessary to users to perform their jobs.</span></span> <span data-ttu-id="ff451-106">Tre di questi ruoli Controllo degli accessi in base al ruolo sono *Proprietario*, *Utente DevTest Labs* e *Collaboratore*.</span><span class="sxs-lookup"><span data-stu-id="ff451-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="ff451-107">In questo articolo vengono indicate le azioni che possono essere eseguite in ognuno dei tre ruoli Controllo degli accessi in base al ruolo principali.</span><span class="sxs-lookup"><span data-stu-id="ff451-107">In this article, you learn what actions can be performed in each of the three main RBAC roles.</span></span> <span data-ttu-id="ff451-108">Viene poi illustrato come aggiungere utenti a un lab, sia tramite il portale che tramite uno script di PowerShell, e come aggiungere utenti a livello di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ff451-108">From there, you learn how to add users to a lab - both via the portal and via a PowerShell script, and how to add users at the subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="ff451-109">Azioni che possono essere eseguite in ogni ruolo</span><span class="sxs-lookup"><span data-stu-id="ff451-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="ff451-110">Esistono tre ruoli principali che è possibile assegnare a un utente:</span><span class="sxs-lookup"><span data-stu-id="ff451-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="ff451-111">Proprietario</span><span class="sxs-lookup"><span data-stu-id="ff451-111">Owner</span></span>
* <span data-ttu-id="ff451-112">Utente DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ff451-112">DevTest Labs User</span></span>
* <span data-ttu-id="ff451-113">Collaboratore</span><span class="sxs-lookup"><span data-stu-id="ff451-113">Contributor</span></span>

<span data-ttu-id="ff451-114">La tabella seguente illustra le azioni che possono essere eseguite dagli utenti in ognuno di questi ruoli:</span><span class="sxs-lookup"><span data-stu-id="ff451-114">The following table illustrates the actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="ff451-115">**Azioni che gli utenti in questo ruolo possono eseguire**</span><span class="sxs-lookup"><span data-stu-id="ff451-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="ff451-116">**Utente DevTest Labs**</span><span class="sxs-lookup"><span data-stu-id="ff451-116">**DevTest Labs User**</span></span> | <span data-ttu-id="ff451-117">**Proprietario**</span><span class="sxs-lookup"><span data-stu-id="ff451-117">**Owner**</span></span> | <span data-ttu-id="ff451-118">**Collaboratore**</span><span class="sxs-lookup"><span data-stu-id="ff451-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ff451-119">**Attività lab**</span><span class="sxs-lookup"><span data-stu-id="ff451-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="ff451-120">Aggiungere utenti a un lab</span><span class="sxs-lookup"><span data-stu-id="ff451-120">Add users to a lab</span></span> |<span data-ttu-id="ff451-121">No</span><span class="sxs-lookup"><span data-stu-id="ff451-121">No</span></span> |<span data-ttu-id="ff451-122">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-122">Yes</span></span> |<span data-ttu-id="ff451-123">No</span><span class="sxs-lookup"><span data-stu-id="ff451-123">No</span></span> |
| <span data-ttu-id="ff451-124">Aggiornare le impostazioni dei costi</span><span class="sxs-lookup"><span data-stu-id="ff451-124">Update cost settings</span></span> |<span data-ttu-id="ff451-125">No</span><span class="sxs-lookup"><span data-stu-id="ff451-125">No</span></span> |<span data-ttu-id="ff451-126">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-126">Yes</span></span> |<span data-ttu-id="ff451-127">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-127">Yes</span></span> |
| <span data-ttu-id="ff451-128">**Attività di base delle VM**</span><span class="sxs-lookup"><span data-stu-id="ff451-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="ff451-129">Aggiungere e rimuovere immagini personalizzate</span><span class="sxs-lookup"><span data-stu-id="ff451-129">Add and remove custom images</span></span> |<span data-ttu-id="ff451-130">No</span><span class="sxs-lookup"><span data-stu-id="ff451-130">No</span></span> |<span data-ttu-id="ff451-131">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-131">Yes</span></span> |<span data-ttu-id="ff451-132">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-132">Yes</span></span> |
| <span data-ttu-id="ff451-133">Aggiungere, aggiornare ed eliminare formule</span><span class="sxs-lookup"><span data-stu-id="ff451-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="ff451-134">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-134">Yes</span></span> |<span data-ttu-id="ff451-135">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-135">Yes</span></span> |<span data-ttu-id="ff451-136">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-136">Yes</span></span> |
| <span data-ttu-id="ff451-137">Aggiungere all'elenco elementi consentiti le immagini di Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="ff451-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="ff451-138">No</span><span class="sxs-lookup"><span data-stu-id="ff451-138">No</span></span> |<span data-ttu-id="ff451-139">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-139">Yes</span></span> |<span data-ttu-id="ff451-140">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-140">Yes</span></span> |
| <span data-ttu-id="ff451-141">**Attività della macchina virtuale**</span><span class="sxs-lookup"><span data-stu-id="ff451-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="ff451-142">Creare VM</span><span class="sxs-lookup"><span data-stu-id="ff451-142">Create VMs</span></span> |<span data-ttu-id="ff451-143">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-143">Yes</span></span> |<span data-ttu-id="ff451-144">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-144">Yes</span></span> |<span data-ttu-id="ff451-145">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-145">Yes</span></span> |
| <span data-ttu-id="ff451-146">Avviare, arrestare ed eliminare VM</span><span class="sxs-lookup"><span data-stu-id="ff451-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="ff451-147">Solo VM create dall'utente</span><span class="sxs-lookup"><span data-stu-id="ff451-147">Only VMs created by the user</span></span> |<span data-ttu-id="ff451-148">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-148">Yes</span></span> |<span data-ttu-id="ff451-149">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-149">Yes</span></span> |
| <span data-ttu-id="ff451-150">Aggiornare i criteri delle VM</span><span class="sxs-lookup"><span data-stu-id="ff451-150">Update VM policies</span></span> |<span data-ttu-id="ff451-151">No</span><span class="sxs-lookup"><span data-stu-id="ff451-151">No</span></span> |<span data-ttu-id="ff451-152">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-152">Yes</span></span> |<span data-ttu-id="ff451-153">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-153">Yes</span></span> |
| <span data-ttu-id="ff451-154">Aggiungere/Rimuovere dischi dati nelle VM</span><span class="sxs-lookup"><span data-stu-id="ff451-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="ff451-155">Solo VM create dall'utente</span><span class="sxs-lookup"><span data-stu-id="ff451-155">Only VMs created by the user</span></span> |<span data-ttu-id="ff451-156">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-156">Yes</span></span> |<span data-ttu-id="ff451-157">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-157">Yes</span></span> |
| <span data-ttu-id="ff451-158">**Attività degli elementi**</span><span class="sxs-lookup"><span data-stu-id="ff451-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="ff451-159">Aggiungere e rimuovere repository di elementi</span><span class="sxs-lookup"><span data-stu-id="ff451-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="ff451-160">No</span><span class="sxs-lookup"><span data-stu-id="ff451-160">No</span></span> |<span data-ttu-id="ff451-161">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-161">Yes</span></span> |<span data-ttu-id="ff451-162">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-162">Yes</span></span> |
| <span data-ttu-id="ff451-163">Applicare elementi</span><span class="sxs-lookup"><span data-stu-id="ff451-163">Apply artifacts</span></span> |<span data-ttu-id="ff451-164">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-164">Yes</span></span> |<span data-ttu-id="ff451-165">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-165">Yes</span></span> |<span data-ttu-id="ff451-166">Sì</span><span class="sxs-lookup"><span data-stu-id="ff451-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="ff451-167">Quando un utente crea una VM, tale utente viene automaticamente assegnato al ruolo **Proprietario** della VM creata.</span><span class="sxs-lookup"><span data-stu-id="ff451-167">When a user creates a VM, that user is automatically assigned to the **Owner** role of the created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-the-lab-level"></a><span data-ttu-id="ff451-168">Aggiungere un utente o un proprietario a livello di lab</span><span class="sxs-lookup"><span data-stu-id="ff451-168">Add an owner or user at the lab level</span></span>
<span data-ttu-id="ff451-169">Proprietari e utenti possono essere aggiunti a livello di lab tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ff451-169">Owners and users can be added at the lab level via the Azure portal.</span></span> <span data-ttu-id="ff451-170">Sono inclusi gli utenti esterni con un [account Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account)valido.</span><span class="sxs-lookup"><span data-stu-id="ff451-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="ff451-171">Il processo di aggiunta di un proprietario o di un utente a un lab in Azure DevTest Labs prevede i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ff451-171">The following steps guide you through the process of adding an owner or user to a lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="ff451-172">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="ff451-172">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="ff451-173">Selezionare **Altri servizi** e quindi **DevTest Labs** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="ff451-173">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="ff451-174">Nell'elenco dei lab selezionare il lab desiderato.</span><span class="sxs-lookup"><span data-stu-id="ff451-174">From the list of labs, select the desired lab.</span></span>
4. <span data-ttu-id="ff451-175">Nel pannello del lab selezionare **Configurazione**.</span><span class="sxs-lookup"><span data-stu-id="ff451-175">On the lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="ff451-176">Nel pannello **Configurazione** selezionare **Utenti**.</span><span class="sxs-lookup"><span data-stu-id="ff451-176">On the **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="ff451-177">Nel pannello **Utenti** selezionare **+Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ff451-177">On the **Users** blade, select **+Add**.</span></span>
   
    ![Add user](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="ff451-179">Nel pannello **Selezionare un ruolo** selezionare il ruolo desiderato.</span><span class="sxs-lookup"><span data-stu-id="ff451-179">On the **Select a role** blade, select the desired role.</span></span> <span data-ttu-id="ff451-180">La sezione [Azioni che possono essere eseguite in ogni ruolo](#actions-that-can-be-performed-in-each-role) elenca le diverse azioni che possono essere eseguite dagli utenti nei ruoli Proprietario, Utente DevTest Labs e Collaboratore.</span><span class="sxs-lookup"><span data-stu-id="ff451-180">The section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists the various actions that can be performed by users in the Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="ff451-181">Nel pannello **Aggiungi utenti** immettere l'indirizzo di posta elettronica o il nome dell'utente che si vuole aggiungere nel ruolo specificato.</span><span class="sxs-lookup"><span data-stu-id="ff451-181">On the **Add users** blade, enter the email address or name of the user you want to add in the role you specified.</span></span> <span data-ttu-id="ff451-182">Se l'utente non viene trovato, un messaggio di errore spiega il problema.</span><span class="sxs-lookup"><span data-stu-id="ff451-182">If the user can't be found, an error message explains the issue.</span></span> <span data-ttu-id="ff451-183">Se l'utente viene trovato, tale utente è elencato e selezionato.</span><span class="sxs-lookup"><span data-stu-id="ff451-183">If the user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="ff451-184">Scegliere **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="ff451-184">Select **Select**.</span></span>
10. <span data-ttu-id="ff451-185">Selezionare **OK** per chiudere il pannello **Aggiungi accesso**.</span><span class="sxs-lookup"><span data-stu-id="ff451-185">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="ff451-186">Quando si torna al pannello **Utenti** , l'utente risulta aggiunto.</span><span class="sxs-lookup"><span data-stu-id="ff451-186">When you return to the **Users** blade, the user has been added.</span></span>  

## <a name="add-an-external-user-to-a-lab-using-powershell"></a><span data-ttu-id="ff451-187">Aggiungere un utente esterno a un lab usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff451-187">Add an external user to a lab using PowerShell</span></span>
<span data-ttu-id="ff451-188">Oltre ad aggiungere gli utenti nel portale di Azure, è possibile aggiungere un utente esterno al lab usando uno script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff451-188">In addition to adding users in the Azure portal, you can add an external user to your lab using a PowerShell script.</span></span> <span data-ttu-id="ff451-189">Nell'esempio seguente, è sufficiente modificare i valori dei parametri nel commento **Values to change** (Valori da modificare).</span><span class="sxs-lookup"><span data-stu-id="ff451-189">In the following example, simply modify the parameter values under the **Values to change** comment.</span></span>
<span data-ttu-id="ff451-190">È possibile recuperare i valori `subscriptionId`, `labResourceGroup` e `labName` dal pannello Lab nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ff451-190">You can retrieve the `subscriptionId`, `labResourceGroup`, and `labName` values from the lab blade in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="ff451-191">Lo script di esempio presume che l'utente specificato sia stato aggiunto come guest ad Active Directory. In caso contrario, avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="ff451-191">The sample script assumes that the specified user has been added as a guest to the Active Directory, and will fail if that is not the case.</span></span> <span data-ttu-id="ff451-192">Per aggiungere a un lab un utente non presente in Active Directory, usare il portale di Azure per assegnare l'utente a un ruolo come illustrato nella sezione [Aggiungere un utente o un proprietario a livello di lab](#add-an-owner-or-user-at-the-lab-level).</span><span class="sxs-lookup"><span data-stu-id="ff451-192">To add a user not in the Active Directory to a lab, use the Azure portal to assign the user to a role as illustrated in the section, [Add an owner or user at the lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role to a lab
    # Ensure that guest users can be added to the Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values to change
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select the Azure subscription that contains the lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve the user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create the role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-the-subscription-level"></a><span data-ttu-id="ff451-193">Aggiungere un utente o un proprietario a livello di sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="ff451-193">Add an owner or user at the subscription level</span></span>
<span data-ttu-id="ff451-194">Le autorizzazioni di Azure vengono propagate dall'ambito padre all'ambito figlio in Azure.</span><span class="sxs-lookup"><span data-stu-id="ff451-194">Azure permissions are propagated from parent scope to child scope in Azure.</span></span> <span data-ttu-id="ff451-195">Quindi i proprietari di una sottoscrizione di Azure contenente lab sono automaticamente proprietari di tali lab.</span><span class="sxs-lookup"><span data-stu-id="ff451-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="ff451-196">Sono proprietari anche delle VM e delle altre risorse create dagli utenti del lab e dal servizio Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="ff451-196">They also own the VMs and other resources created by the lab's users, and the Azure DevTest Labs service.</span></span> 

<span data-ttu-id="ff451-197">È possibile aggiungere altri proprietari a un lab tramite il pannello del lab nel [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="ff451-197">You can add additional owners to a lab via the lab's blade in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="ff451-198">L'ambito di amministrazione del proprietario aggiunto è tuttavia più limitato dell'ambito del proprietario della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ff451-198">However, the added owner's scope of administration is more narrow than the subscription owner's scope.</span></span> <span data-ttu-id="ff451-199">I proprietari aggiunti, ad esempio, non hanno accesso completo ad alcune delle risorse create nella sottoscrizione dal servizio DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="ff451-199">For example, the added owners do not have full access to some of the resources that are created in the subscription by the DevTest Labs service.</span></span> 

<span data-ttu-id="ff451-200">Per aggiungere un proprietario a una sottoscrizione di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="ff451-200">To add an owner to an Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="ff451-201">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="ff451-201">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="ff451-202">Selezionare **Altri servizi** e quindi **Sottoscrizioni** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="ff451-202">Select **More Services**, and then select **Subscriptions** from the list.</span></span>
3. <span data-ttu-id="ff451-203">Selezionare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="ff451-203">Select the desired subscription.</span></span>
4. <span data-ttu-id="ff451-204">Selezionare l'icona **Accesso** .</span><span class="sxs-lookup"><span data-stu-id="ff451-204">Select **Access** icon.</span></span> 
   
    ![Utenti di accesso](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="ff451-206">Nel pannello **Utenti** selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ff451-206">On the **Users** blade, select **Add**.</span></span>
   
    ![Add user](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="ff451-208">Nel pannello **Selezionare un ruolo** selezionare **Proprietario**.</span><span class="sxs-lookup"><span data-stu-id="ff451-208">On the **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="ff451-209">Nel pannello **Aggiungi utenti** immettere l'indirizzo di posta elettronica o il nome dell'utente che si vuole aggiungere come proprietario.</span><span class="sxs-lookup"><span data-stu-id="ff451-209">On the **Add users** blade, enter the email address or name of the user you want to add as an owner.</span></span> <span data-ttu-id="ff451-210">Se l'utente non viene trovato, si riceve un messaggio di errore che spiega il problema.</span><span class="sxs-lookup"><span data-stu-id="ff451-210">If the user can't be found, you get an error message explaining the issue.</span></span> <span data-ttu-id="ff451-211">Se l'utente viene trovato, tale utente viene elencato sotto la casella di testo **Utente** .</span><span class="sxs-lookup"><span data-stu-id="ff451-211">If the user is found, that user is listed under the **User** text box.</span></span>
8. <span data-ttu-id="ff451-212">Selezionare il nome utente individuato.</span><span class="sxs-lookup"><span data-stu-id="ff451-212">Select the located user name.</span></span>
9. <span data-ttu-id="ff451-213">Scegliere **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="ff451-213">Select **Select**.</span></span>
10. <span data-ttu-id="ff451-214">Selezionare **OK** per chiudere il pannello **Aggiungi accesso**.</span><span class="sxs-lookup"><span data-stu-id="ff451-214">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="ff451-215">Quando si torna al pannello **Utenti** , l'utente risulta aggiunto come proprietario.</span><span class="sxs-lookup"><span data-stu-id="ff451-215">When you return to the **Users** blade, the user has been added as an owner.</span></span> <span data-ttu-id="ff451-216">Questo utente è ora un proprietario di qualsiasi lab creato in questa sottoscrizione e quindi può eseguire le attività del proprietario.</span><span class="sxs-lookup"><span data-stu-id="ff451-216">This user is now an owner of any labs created under this subscription, and thus be able to perform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

