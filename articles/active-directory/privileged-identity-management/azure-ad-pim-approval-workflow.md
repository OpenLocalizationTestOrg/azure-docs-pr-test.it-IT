---
title: Flussi di lavoro di approvazione di Azure Privileged Identity Management | Documentazione Microsoft
description: Informazioni sui flussi di lavoro di approvazione di Privileged Identity Management (PIM)
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: cf6a9213fa0a1cba8725aabb42abe51b805ece7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="52696-103">Approvazioni (Anteprima)</span><span class="sxs-lookup"><span data-stu-id="52696-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="52696-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="52696-104">Overview</span></span>

<span data-ttu-id="52696-105">Con Approvazioni per Privileged Identity Management, è possibile configurare ruoli per richiedere l’approvazione per l’attivazione, e scegliere uno o più utenti o gruppi come responsabili approvazione con delega.</span><span class="sxs-lookup"><span data-stu-id="52696-105">With Approvals for Privileged Identity Management, you can configure roles to require approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="52696-106">Continuare a leggere per scoprire come configurare i ruoli e selezionare i responsabili approvazione.</span><span class="sxs-lookup"><span data-stu-id="52696-106">Keep reading to learn how to configure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="52696-107">Tenere presente che questa funzionalità è ancora in fase di sviluppo e che è possibile che si verifichino degli errori.</span><span class="sxs-lookup"><span data-stu-id="52696-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="52696-108">La funzionalità, inclusi il testo e le convenzioni di denominazione, sono soggetti a modifica e non devono essere considerati finali.</span><span class="sxs-lookup"><span data-stu-id="52696-108">The functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="52696-109">Terminologia chiave</span><span class="sxs-lookup"><span data-stu-id="52696-109">Key Terminology</span></span>

<span data-ttu-id="52696-110">*Eligible Role User (Utente con ruolo idoneo)*: un utente con ruolo idoneo è un utente dell’organizzazione assegnato come idoneo a un ruolo Azure AD (ruolo che richiede l’attivazione).</span><span class="sxs-lookup"><span data-stu-id="52696-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned to an Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="52696-111">*Delegated Approver (Responsabile approvazione con delega)*: un responsabile approvazione con delega è una o più persone o gruppo all’interno di Azure AD che sono responsabili dell’approvazione delle richieste di l’attivazione del ruolo.</span><span class="sxs-lookup"><span data-stu-id="52696-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="52696-112">Scenari</span><span class="sxs-lookup"><span data-stu-id="52696-112">Scenarios</span></span>

<span data-ttu-id="52696-113">L’anteprima privata supporta i seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="52696-113">The private preview supports the following scenarios:</span></span>

<span data-ttu-id="52696-114">**Come Amministratore dei ruoli con privilegi (PRA), è possibile:**</span><span class="sxs-lookup"><span data-stu-id="52696-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="52696-115">Abilitare l’approvazione per ruoli specifici</span><span class="sxs-lookup"><span data-stu-id="52696-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="52696-116">Specificare gli utenti e/o i gruppi approvatori per l’approvazione delle richieste</span><span class="sxs-lookup"><span data-stu-id="52696-116">specify approver users and/or groups to approve requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="52696-117">Visualizzare la cronologia delle richieste e delle approvazioni per tutti i ruoli con privilegi</span><span class="sxs-lookup"><span data-stu-id="52696-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="52696-118">**Come responsabile approvazione designato, è possibile:**</span><span class="sxs-lookup"><span data-stu-id="52696-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="52696-119">Visualizzare le approvazioni (richieste) in sospeso</span><span class="sxs-lookup"><span data-stu-id="52696-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="52696-120">Approvare o rifiutare le richieste di elevazione del ruolo (singolarmente e/o in blocco)</span><span class="sxs-lookup"><span data-stu-id="52696-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="52696-121">Fornire una giustificazione per l’approvazione/il rifiuto</span><span class="sxs-lookup"><span data-stu-id="52696-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="52696-122">**Come Eligible Role User (Utente con ruolo idoneo), è possibile:**</span><span class="sxs-lookup"><span data-stu-id="52696-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="52696-123">Richiedere l’attivazione di un ruolo che richiede approvazione</span><span class="sxs-lookup"><span data-stu-id="52696-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="52696-124">Visualizzare lo stato della richiesta da attivare</span><span class="sxs-lookup"><span data-stu-id="52696-124">view the status of your request to activate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="52696-125">Completare l’attività in Azure AD se l’attivazione è stata approvata</span><span class="sxs-lookup"><span data-stu-id="52696-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="52696-126">Navigazione</span><span class="sxs-lookup"><span data-stu-id="52696-126">Navigation</span></span>

<span data-ttu-id="52696-127">La navigazione è stata aggiornata per supportare le approvazioni</span><span class="sxs-lookup"><span data-stu-id="52696-127">We've updated the navigation to support approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="52696-128">La pagina di destinazione predefinita fornisce un pratico accesso alle informazioni su PIM e alla nuova documentazione sulle approvazioni.</span><span class="sxs-lookup"><span data-stu-id="52696-128">The default landing page provides convenient access to information about PIM and the new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="52696-129">È stata aggiunta anche una nuova sezione per tutti gli utenti di PIM: ’My Audit History’ (Cronologia delle approvazioni personali).</span><span class="sxs-lookup"><span data-stu-id="52696-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="52696-130">In questa sezione e è possibile trovare tutte le informazioni relative alla propria identità.</span><span class="sxs-lookup"><span data-stu-id="52696-130">Here you can find all the information relevant to your identity.</span></span> <span data-ttu-id="52696-131">Tutte le richieste in sospeso e completate, qualsiasi decisione presa sulle richieste risolte, e tutte le attivazioni precedenti dei ruoli sono incluse in un’unica pratica posizione.</span><span class="sxs-lookup"><span data-stu-id="52696-131">This includes all your pending and completed requests, any decisions you’ve made about the requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="52696-132">Abilitare l’approvazione per ruoli specifici</span><span class="sxs-lookup"><span data-stu-id="52696-132">Enable approval for specific roles</span></span>

<span data-ttu-id="52696-133">Per abilitare l’approvazione per un ruolo specifico, selezionare prima Ruoli della directory nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="52696-133">To enable approval for a specific role, first select Directory Roles from the left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="52696-134">Cercare e selezionare le impostazioni nel riquadro di spostamento sinistro Ruoli della directory.</span><span class="sxs-lookup"><span data-stu-id="52696-134">Find and select settings in the Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="52696-135">Selezionare i ruoli privilegiati:</span><span class="sxs-lookup"><span data-stu-id="52696-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="52696-136">Selezionare “Abilita” nella sezione Richiedi approvazione:</span><span class="sxs-lookup"><span data-stu-id="52696-136">Select “Enable” in the Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="52696-137">Una volta abilitato, il pannello si espande per mostrare i seguenti dettagli:</span><span class="sxs-lookup"><span data-stu-id="52696-137">Once enabled, the blade will expand to show the following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="52696-138">Se NON si specificano responsabili approvazione, i PRA diventano i responsabili approvazione predefiniti.</span><span class="sxs-lookup"><span data-stu-id="52696-138">If you DO NOT specify any approvers, the PRA(s) become the default approver(s).</span></span> <span data-ttu-id="52696-139">Ai PRA verrà richiesto di approvare TUTTE le richieste di attivazione per il ruolo.</span><span class="sxs-lookup"><span data-stu-id="52696-139">PRA(s) would be required to approve ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-to-approve-requests"></a><span data-ttu-id="52696-140">Specificare utenti e/o gruppi approvatori per approvare le richieste</span><span class="sxs-lookup"><span data-stu-id="52696-140">Specify approver users and/or groups to approve requests</span></span>

<span data-ttu-id="52696-141">Per delegare l’approvazione, fare clic sull’opzione “Selezionare responsabili approvazione”:</span><span class="sxs-lookup"><span data-stu-id="52696-141">To delegate approval, click the option to “Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="52696-142">Quando viene caricato il pannello Selezionare responsabili approvazione, è possibile cercare un utente o un gruppo specifico utilizzando la barra di ricerca in alto, oppure effettuare una selezione dall’elenco già popolato, quindi fare clic su “Seleziona” al termine:</span><span class="sxs-lookup"><span data-stu-id="52696-142">When the Select approvers blade loads, you may search for a specific user or group using the search bar at the top, or selecting from the pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="52696-143">Nota: è possibile selezionare contemporaneamente più utenti o gruppi.</span><span class="sxs-lookup"><span data-stu-id="52696-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="52696-144">La selezione viene visualizzata nell’elenco dei responsabili approvazione mostrata di seguito:</span><span class="sxs-lookup"><span data-stu-id="52696-144">Your selection will appear in the list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="52696-145">Per rimuovere un responsabile approvazione, fare semplicemente clic sul pulsante Rimuovi vicino al nome.</span><span class="sxs-lookup"><span data-stu-id="52696-145">To remove an approver, simply click the Remove button next to their name.</span></span>

<span data-ttu-id="52696-146">Per aggiungere responsabili approvazione aggiuntivi, ripetere il processo.</span><span class="sxs-lookup"><span data-stu-id="52696-146">To add additional approvers, repeat the process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="52696-147">Visualizzare la cronologia delle richieste e delle approvazioni per tutti i ruoli con privilegi</span><span class="sxs-lookup"><span data-stu-id="52696-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="52696-148">Per visualizzare la cronologia delle richieste e delle approvazioni per tutti i ruoli con privilegi, selezionare Cronologia controllo dal dashboard:</span><span class="sxs-lookup"><span data-stu-id="52696-148">To view request and approval history for all privileged roles, select Audit History from the dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="52696-149">È possibile ordinare i dati per azione e ricercare “L’attivazione è stata approvata”.</span><span class="sxs-lookup"><span data-stu-id="52696-149">You can sort the data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="52696-150">Visualizzare le approvazioni (richieste) in sospeso</span><span class="sxs-lookup"><span data-stu-id="52696-150">View pending approvals (requests)</span></span>

<span data-ttu-id="52696-151">In qualità di responsabile approvazione con delega riceverà notifiche e-mail quando una richiesta è in attesa di approvazione.</span><span class="sxs-lookup"><span data-stu-id="52696-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="52696-152">Per visualizzare queste richieste nel portale PIM, dal dashboard (nella nuova navigazione) selezionare la scheda “Richieste di approvazione in sospeso” nella barra di navigazione sinistra.</span><span class="sxs-lookup"><span data-stu-id="52696-152">To view these requests in the PIM portal, from the dashboard (in the new navigation) select the “Pending Approval Requests” tab in the left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="52696-153">Da qui, è possibile visualizzare un elenco delle richieste in attesa di approvazione:</span><span class="sxs-lookup"><span data-stu-id="52696-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="52696-154">Approvare o rifiutare le richieste di elevazione del ruolo (singolarmente e/o in blocco)</span><span class="sxs-lookup"><span data-stu-id="52696-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="52696-155">Selezionare le richieste che si desidera approvare o rifiutare, quindi fare clic sul pulsante della barra delle azioni che corrisponde alla decisione:</span><span class="sxs-lookup"><span data-stu-id="52696-155">Select the requests you wish to approve or deny, and click the button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="52696-156">Fornire una giustificazione per l’approvazione/il rifiuto</span><span class="sxs-lookup"><span data-stu-id="52696-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="52696-157">Viene aperto un nuovo pannello in cui è possibile approvare o rifiutare più richieste con una sola operazione.</span><span class="sxs-lookup"><span data-stu-id="52696-157">This will open a new blade to approve or deny multiple requests at once.</span></span> <span data-ttu-id="52696-158">Immettere una giustificazione per la decisione e fare su Approva (o Rifiuta) in fondo al pannello:</span><span class="sxs-lookup"><span data-stu-id="52696-158">Enter a justification for your decision, and click approve (or deny) at the bottom or the blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="52696-159">Al termine del processo di richiesta, il simbolo dello stato riflette la decisione presa (in questo esempio, la decisione è un’approvazione):</span><span class="sxs-lookup"><span data-stu-id="52696-159">When the request process is complete, the status symbol will reflect the decision you made (in this example, the decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="52696-160">Richiedere l’attivazione di un ruolo che richiede l’approvazione</span><span class="sxs-lookup"><span data-stu-id="52696-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="52696-161">È possibile avviare la richiesta di attivazione di un ruolo che richiede approvazione dalla navigazione PIM precedente o dalla nuova navigazione, poichè il processo di attivazione del ruolo è rimasto invariato.</span><span class="sxs-lookup"><span data-stu-id="52696-161">Requesting activation of a role that requires approval may be initiated from either the old PIM navigation, or the new navigation, as the process for role activation remains the same.</span></span> <span data-ttu-id="52696-162">Selezionare semplicemente il ruolo dall’elenco dei ruoli da attivare:</span><span class="sxs-lookup"><span data-stu-id="52696-162">Simply select a role from the list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="52696-163">Se un ruolo con privilegi richiede la Multi-Factor Authentication, verrà richiesto di completare prima questa attività:</span><span class="sxs-lookup"><span data-stu-id="52696-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="52696-164">Al termine, fare clic su Attiva e fornire una giustificazione (se richiesta):</span><span class="sxs-lookup"><span data-stu-id="52696-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="52696-165">Verrà visualizzata una notifica che indica al richiedente che la richiesta è in attesa di approvazione:</span><span class="sxs-lookup"><span data-stu-id="52696-165">The requestor will see a notification that the request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-the-status-of-your-request-to-activate"></a><span data-ttu-id="52696-166">Visualizzare lo stato della richiesta da attivare</span><span class="sxs-lookup"><span data-stu-id="52696-166">View the status of your request to activate</span></span>

<span data-ttu-id="52696-167">Per visualizzare lo stato di una richiesta in sospeso da attivare, è necessario accedere dalla nuova navigazione.</span><span class="sxs-lookup"><span data-stu-id="52696-167">Viewing the status of a pending request to activate must be accessed from the new navigation.</span></span> <span data-ttu-id="52696-168">Dalla barra di navigazione sinistra selezionare la scheda “My Requests” (Richieste personali):</span><span class="sxs-lookup"><span data-stu-id="52696-168">From the left navigation bar, select the “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="52696-169">Per impostazione predefinita, lo stato della richiesta viene impostato su “In sospeso” ma è possibile alternare la visualizzazione tra tutte le richieste e quelle rifiutate.</span><span class="sxs-lookup"><span data-stu-id="52696-169">The request state defaults to “Pending”, but you can toggle to see all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="52696-170">Completare l’attività in Azure AD se l’attivazione è stata approvata</span><span class="sxs-lookup"><span data-stu-id="52696-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="52696-171">Una volta che la richiesta è stata approvata, il ruolo è attivo ed è possibile procedere con qualsiasi altra azione necessaria per il ruolo.</span><span class="sxs-lookup"><span data-stu-id="52696-171">Once the request is approved, the role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="52696-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="52696-172">Next steps</span></span>

<span data-ttu-id="52696-173">La sua opinione è importante per noi.</span><span class="sxs-lookup"><span data-stu-id="52696-173">Your feedback is valuable to us.</span></span> <span data-ttu-id="52696-174">Può condividere i suoi commenti o suggerimenti facendo clic qui.</span><span class="sxs-lookup"><span data-stu-id="52696-174">Please feel free to share comments or feedback with us here!</span></span>
