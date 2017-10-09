---
title: "flussi di lavoro di approvazione della gestione delle identità con privilegi aaaAzure | Documenti Microsoft"
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
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="ee4ec-103">Approvazioni (Anteprima)</span><span class="sxs-lookup"><span data-stu-id="ee4ec-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="ee4ec-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ee4ec-104">Overview</span></span>

<span data-ttu-id="ee4ec-105">Con approvazioni per Privileged Identity Management, è possibile configurare l'approvazione toorequire ruoli per l'attivazione e scegliere uno o più utenti o gruppi come delegati responsabili approvazione.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-105">With Approvals for Privileged Identity Management, you can configure roles toorequire approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="ee4ec-106">Continuare a leggere toolearn come ruoli tooconfigure e selezionare i responsabili approvazione.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-106">Keep reading toolearn how tooconfigure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="ee4ec-107">Tenere presente che questa funzionalità è ancora in fase di sviluppo e che è possibile che si verifichino degli errori.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="ee4ec-108">funzionalità di Hello, incluso il testo e convenzioni di denominazione sono soggetti a modifiche e non deve essere considerati finale.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-108">hello functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="ee4ec-109">Terminologia chiave</span><span class="sxs-lookup"><span data-stu-id="ee4ec-109">Key Terminology</span></span>

<span data-ttu-id="ee4ec-110">*Idonei ruolo utente* : un utente idoneo ruolo è un utente all'interno dell'organizzazione che è stato assegnato il ruolo di Azure AD tooan come idonee (ruolo richiede un'attivazione).</span><span class="sxs-lookup"><span data-stu-id="ee4ec-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned tooan Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="ee4ec-111">*Delegated Approver (Responsabile approvazione con delega)*: un responsabile approvazione con delega è una o più persone o gruppo all’interno di Azure AD che sono responsabili dell’approvazione delle richieste di l’attivazione del ruolo.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="ee4ec-112">Scenari</span><span class="sxs-lookup"><span data-stu-id="ee4ec-112">Scenarios</span></span>

<span data-ttu-id="ee4ec-113">Anteprima privata Hello supporta hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="ee4ec-113">hello private preview supports hello following scenarios:</span></span>

<span data-ttu-id="ee4ec-114">**Come Amministratore dei ruoli con privilegi (PRA), è possibile:**</span><span class="sxs-lookup"><span data-stu-id="ee4ec-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="ee4ec-115">Abilitare l’approvazione per ruoli specifici</span><span class="sxs-lookup"><span data-stu-id="ee4ec-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="ee4ec-116">specificare richieste tooapprove utenti e/o gruppi di responsabile approvazione</span><span class="sxs-lookup"><span data-stu-id="ee4ec-116">specify approver users and/or groups tooapprove requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="ee4ec-117">Visualizzare la cronologia delle richieste e delle approvazioni per tutti i ruoli con privilegi</span><span class="sxs-lookup"><span data-stu-id="ee4ec-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="ee4ec-118">**Come responsabile approvazione designato, è possibile:**</span><span class="sxs-lookup"><span data-stu-id="ee4ec-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="ee4ec-119">Visualizzare le approvazioni (richieste) in sospeso</span><span class="sxs-lookup"><span data-stu-id="ee4ec-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="ee4ec-120">Approvare o rifiutare le richieste di elevazione del ruolo (singolarmente e/o in blocco)</span><span class="sxs-lookup"><span data-stu-id="ee4ec-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="ee4ec-121">Fornire una giustificazione per l’approvazione/il rifiuto</span><span class="sxs-lookup"><span data-stu-id="ee4ec-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="ee4ec-122">**Come Eligible Role User (Utente con ruolo idoneo), è possibile:**</span><span class="sxs-lookup"><span data-stu-id="ee4ec-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="ee4ec-123">Richiedere l’attivazione di un ruolo che richiede approvazione</span><span class="sxs-lookup"><span data-stu-id="ee4ec-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="ee4ec-124">visualizzare lo stato di hello di tooactivate la richiesta</span><span class="sxs-lookup"><span data-stu-id="ee4ec-124">view hello status of your request tooactivate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="ee4ec-125">Completare l’attività in Azure AD se l’attivazione è stata approvata</span><span class="sxs-lookup"><span data-stu-id="ee4ec-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="ee4ec-126">Navigazione</span><span class="sxs-lookup"><span data-stu-id="ee4ec-126">Navigation</span></span>

<span data-ttu-id="ee4ec-127">Sono stati aggiornati approvazioni toosupport di navigazione hello</span><span class="sxs-lookup"><span data-stu-id="ee4ec-127">We've updated hello navigation toosupport approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="ee4ec-128">pagina di destinazione predefinita Hello fornisce un pratico accesso tooinformation su PIM e hello nuova documentazione approvazioni.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-128">hello default landing page provides convenient access tooinformation about PIM and hello new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="ee4ec-129">È stata aggiunta anche una nuova sezione per tutti gli utenti di PIM: ’My Audit History’ (Cronologia delle approvazioni personali).</span><span class="sxs-lookup"><span data-stu-id="ee4ec-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="ee4ec-130">Qui è possibile trovare tutte le identità di tooyour rilevanti informazioni hello.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-130">Here you can find all hello information relevant tooyour identity.</span></span> <span data-ttu-id="ee4ec-131">Questo include tutte le richieste in sospeso e completate, le decisioni che relative al richieste hello è risolvere e tutte le attivazioni di ruoli precedenti in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-131">This includes all your pending and completed requests, any decisions you’ve made about hello requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="ee4ec-132">Abilitare l’approvazione per ruoli specifici</span><span class="sxs-lookup"><span data-stu-id="ee4ec-132">Enable approval for specific roles</span></span>

<span data-ttu-id="ee4ec-133">approvazione tooenable per un ruolo specifico, selezionare innanzitutto i ruoli della Directory dal riquadro di spostamento sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-133">tooenable approval for a specific role, first select Directory Roles from hello left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="ee4ec-134">Individuare e selezionare le impostazioni in hello spostamento a sinistra i ruoli della Directory</span><span class="sxs-lookup"><span data-stu-id="ee4ec-134">Find and select settings in hello Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="ee4ec-135">Selezionare i ruoli privilegiati:</span><span class="sxs-lookup"><span data-stu-id="ee4ec-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="ee4ec-136">Selezionare "Abilita" hello richiedono una sezione di approvazione:</span><span class="sxs-lookup"><span data-stu-id="ee4ec-136">Select “Enable” in hello Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="ee4ec-137">Una volta abilitato, blade hello espanderà hello tooshow seguenti dettagli:</span><span class="sxs-lookup"><span data-stu-id="ee4ec-137">Once enabled, hello blade will expand tooshow hello following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="ee4ec-138">Se non si specifica tutti i revisori, hello PRA(s) diventano approvatori predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-138">If you DO NOT specify any approvers, hello PRA(s) become hello default approver(s).</span></span> <span data-ttu-id="ee4ec-139">PRA(s) sarebbe necessario tooapprove attivazione tutte le richieste per questo ruolo.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-139">PRA(s) would be required tooapprove ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a><span data-ttu-id="ee4ec-140">Specificare richieste tooapprove utenti e/o gruppi di responsabile approvazione</span><span class="sxs-lookup"><span data-stu-id="ee4ec-140">Specify approver users and/or groups tooapprove requests</span></span>

<span data-ttu-id="ee4ec-141">approvazione toodelegate, fare clic su hello opzione troppo "Select responsabili approvazione":</span><span class="sxs-lookup"><span data-stu-id="ee4ec-141">toodelegate approval, click hello option too“Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="ee4ec-142">Quando viene caricato il pannello di selezione responsabili approvazione hello, è possibile cercare un utente o gruppo specifico tramite la barra di ricerca hello a top hello o selezionare dall'elenco pre-popolato hello, quindi fare clic su "Select" al termine:</span><span class="sxs-lookup"><span data-stu-id="ee4ec-142">When hello Select approvers blade loads, you may search for a specific user or group using hello search bar at hello top, or selecting from hello pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="ee4ec-143">Nota: è possibile selezionare contemporaneamente più utenti o gruppi.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="ee4ec-144">La selezione verrà visualizzato nell'elenco di hello di responsabili approvazione selezionati, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ee4ec-144">Your selection will appear in hello list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="ee4ec-145">tooremove un revisore, fare semplicemente clic hello rimuovere pulsante Avanti tootheir il nome.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-145">tooremove an approver, simply click hello Remove button next tootheir name.</span></span>

<span data-ttu-id="ee4ec-146">approvazione tooadd aggiuntivi, il processo di ripetizione hello.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-146">tooadd additional approvers, repeat hello process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="ee4ec-147">Visualizzare la cronologia delle richieste e delle approvazioni per tutti i ruoli con privilegi</span><span class="sxs-lookup"><span data-stu-id="ee4ec-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="ee4ec-148">cronologia tooview di richiesta e l'approvazione per i ruoli con tutti i privilegi, selezionare la cronologia di controllo dal dashboard hello:</span><span class="sxs-lookup"><span data-stu-id="ee4ec-148">tooview request and approval history for all privileged roles, select Audit History from hello dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="ee4ec-149">È possibile ordinare i dati di hello per azione e cercare "Approved di attivazione"</span><span class="sxs-lookup"><span data-stu-id="ee4ec-149">You can sort hello data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="ee4ec-150">Visualizzare le approvazioni (richieste) in sospeso</span><span class="sxs-lookup"><span data-stu-id="ee4ec-150">View pending approvals (requests)</span></span>

<span data-ttu-id="ee4ec-151">In qualità di responsabile approvazione con delega riceverà notifiche e-mail quando una richiesta è in attesa di approvazione.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="ee4ec-152">tooview queste richieste nel portale PIM hello dalla scheda dashboard (nella nuova navigazione hello) Seleziona hello "in sospeso richieste di approvazione" hello, barra di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-152">tooview these requests in hello PIM portal, from the dashboard (in hello new navigation) select hello “Pending Approval Requests” tab in hello left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="ee4ec-153">Da qui, è possibile visualizzare un elenco delle richieste in attesa di approvazione:</span><span class="sxs-lookup"><span data-stu-id="ee4ec-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="ee4ec-154">Approvare o rifiutare le richieste di elevazione del ruolo (singolarmente e/o in blocco)</span><span class="sxs-lookup"><span data-stu-id="ee4ec-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="ee4ec-155">Selezionare desidera tooapprove o negare le richieste di hello e fare clic sul pulsante hello nella barra delle azioni che corrisponde a quanto deciso:</span><span class="sxs-lookup"><span data-stu-id="ee4ec-155">Select hello requests you wish tooapprove or deny, and click hello button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="ee4ec-156">Fornire una giustificazione per l’approvazione/il rifiuto</span><span class="sxs-lookup"><span data-stu-id="ee4ec-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="ee4ec-157">Verrà aprire un nuovo tooapprove pannello o negare più richieste contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-157">This will open a new blade tooapprove or deny multiple requests at once.</span></span> <span data-ttu-id="ee4ec-158">Immettere una motivazione per la decisione e fare clic su Approva (o negare) nella parte inferiore di hello o blade hello:</span><span class="sxs-lookup"><span data-stu-id="ee4ec-158">Enter a justification for your decision, and click approve (or deny) at hello bottom or hello blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="ee4ec-159">Una volta completato il processo di richiesta di hello, icona stato hello rifletterà la decisione presa (in questo esempio, la decisione hello è approvare):</span><span class="sxs-lookup"><span data-stu-id="ee4ec-159">When hello request process is complete, hello status symbol will reflect the decision you made (in this example, hello decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="ee4ec-160">Richiedere l’attivazione di un ruolo che richiede l’approvazione</span><span class="sxs-lookup"><span data-stu-id="ee4ec-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="ee4ec-161">Richiesta di attivazione di un ruolo che richiede l'approvazione può essere avviata dalla navigazione PIM precedente hello o nuova navigazione hello, come processo hello per ruolo attivazione rimane hello stesso.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-161">Requesting activation of a role that requires approval may be initiated from either hello old PIM navigation, or hello new navigation, as hello process for role activation remains hello same.</span></span> <span data-ttu-id="ee4ec-162">È sufficiente selezionare un ruolo dall'elenco di hello dei ruoli per attivare:</span><span class="sxs-lookup"><span data-stu-id="ee4ec-162">Simply select a role from hello list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="ee4ec-163">Se un ruolo con privilegi richiede la Multi-Factor Authentication, verrà richiesto di completare prima questa attività:</span><span class="sxs-lookup"><span data-stu-id="ee4ec-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="ee4ec-164">Al termine, fare clic su Attiva e fornire una giustificazione (se richiesta):</span><span class="sxs-lookup"><span data-stu-id="ee4ec-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="ee4ec-165">richiedente Hello verrà visualizzata una notifica che hello richiesta in attesa di approvazione:</span><span class="sxs-lookup"><span data-stu-id="ee4ec-165">hello requestor will see a notification that hello request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a><span data-ttu-id="ee4ec-166">Visualizzare lo stato di hello di tooactivate la richiesta</span><span class="sxs-lookup"><span data-stu-id="ee4ec-166">View hello status of your request tooactivate</span></span>

<span data-ttu-id="ee4ec-167">Visualizzazione stato hello di tooactivate una richiesta in sospeso deve essere accessibile dal riquadro di spostamento di nuovo.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-167">Viewing hello status of a pending request tooactivate must be accessed from the new navigation.</span></span> <span data-ttu-id="ee4ec-168">Barra di spostamento a sinistra di hello, selezionare scheda "Richieste di" hello:</span><span class="sxs-lookup"><span data-stu-id="ee4ec-168">From hello left navigation bar, select hello “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="ee4ec-169">stato richiesta Hello predefinite troppo "In sospeso", ma è possibile attivare o disattivare toosee tutti o richieste rifiutate.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-169">hello request state defaults too“Pending”, but you can toggle toosee all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="ee4ec-170">Completare l’attività in Azure AD se l’attivazione è stata approvata</span><span class="sxs-lookup"><span data-stu-id="ee4ec-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="ee4ec-171">Una volta approvata la richiesta di hello, ruolo hello è attiva ed è possibile procedere con le operazioni che richiedono questo ruolo.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-171">Once hello request is approved, hello role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="ee4ec-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ee4ec-172">Next steps</span></span>

<span data-ttu-id="ee4ec-173">Commenti e suggerimenti sono utili toous.</span><span class="sxs-lookup"><span data-stu-id="ee4ec-173">Your feedback is valuable toous.</span></span> <span data-ttu-id="ee4ec-174">Dettagli tooshare libero commenti o suggerimenti con noi qui!</span><span class="sxs-lookup"><span data-stu-id="ee4ec-174">Please feel free tooshare comments or feedback with us here!</span></span>
