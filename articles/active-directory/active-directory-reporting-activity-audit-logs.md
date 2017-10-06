---
title: "report relativi all'attività aaaAudit nel portale di Azure Active Directory hello | Documenti Microsoft"
description: "Report di attività nel portale di Azure Active Directory hello di controllo toohello introduzione"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="7f8d8-103">Report attività nel portale di Azure Active Directory hello di controllo</span><span class="sxs-lookup"><span data-stu-id="7f8d8-103">Audit activity reports in hello Azure Active Directory portal</span></span> 

<span data-ttu-id="7f8d8-104">Grazie ai report in Azure Active Directory (Azure AD), è possibile ottenere informazioni hello necessarie toodetermine, svolgimento dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-104">With reporting in Azure Active Directory (Azure AD), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="7f8d8-105">architettura di reporting in Azure AD Hello è costituita da hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="7f8d8-105">hello reporting architecture in Azure AD consists of hello following components:</span></span>

- <span data-ttu-id="7f8d8-106">**Attività**</span><span class="sxs-lookup"><span data-stu-id="7f8d8-106">**Activity**</span></span> 
    - <span data-ttu-id="7f8d8-107">**Le attività di accesso** – informazioni sull'utilizzo di hello di applicazioni gestite e le attività di accesso dell'utente</span><span class="sxs-lookup"><span data-stu-id="7f8d8-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="7f8d8-108">**Log di controllo**: informazioni relative alle attività di sistema sulla gestione di utenti e gruppi, sulle applicazioni gestite e sulle attività di directory.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="7f8d8-109">**Sicurezza**</span><span class="sxs-lookup"><span data-stu-id="7f8d8-109">**Security**</span></span> 
    - <span data-ttu-id="7f8d8-110">**Accessi rischiosi** -un rischiosa l'accesso è un indicatore per un tentativo di accesso che siano stato eseguito da un utente che non è proprietario di legittimo hello di un account utente.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="7f8d8-111">Per informazioni dettagliate, vedere Accessi a rischio.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="7f8d8-112">**Utenti contrassegnati per il rischio**. Un utente rischioso è indicativo di un account utente che potrebbe essere stato compromesso.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="7f8d8-113">Per informazioni dettagliate, vedere Utenti contrassegnati per il rischio.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="7f8d8-114">In questo argomento offre una panoramica delle attività di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-114">This topic gives you an overview of hello audit activities.</span></span>
 
## <a name="who-can-access-hello-data"></a><span data-ttu-id="7f8d8-115">Chi può accedere a dati hello?</span><span class="sxs-lookup"><span data-stu-id="7f8d8-115">Who can access hello data?</span></span>
* <span data-ttu-id="7f8d8-116">Utenti nel ruolo di amministratore responsabile della sicurezza o di sicurezza Reader hello</span><span class="sxs-lookup"><span data-stu-id="7f8d8-116">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="7f8d8-117">Gli amministratori globali</span><span class="sxs-lookup"><span data-stu-id="7f8d8-117">Global Admins</span></span>
* <span data-ttu-id="7f8d8-118">I singoli utenti (non amministratori) possono visualizzare le proprie attività</span><span class="sxs-lookup"><span data-stu-id="7f8d8-118">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="7f8d8-119">Log di controllo</span><span class="sxs-lookup"><span data-stu-id="7f8d8-119">Audit logs</span></span>

<span data-ttu-id="7f8d8-120">i log di controllo Hello in Azure Active Directory forniscono i record di attività di sistema per la conformità.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-120">hello audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="7f8d8-121">È il primo dati di controllo di voce punto tooall **log di controllo** in hello **attività** sezione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-121">Your first entry point tooall auditing data is **Audit logs** in hello **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="7f8d8-122">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/61.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="7f8d8-122">![Audit logs](./media/active-directory-reporting-activity-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="7f8d8-123">Un log di controllo è una visualizzazione elenco predefinita che include:</span><span class="sxs-lookup"><span data-stu-id="7f8d8-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="7f8d8-124">Hello data e ora dell'occorrenza hello</span><span class="sxs-lookup"><span data-stu-id="7f8d8-124">hello date and time of hello occurrence</span></span>
- <span data-ttu-id="7f8d8-125">Hello iniziatore / attore (*che*) di un'attività</span><span class="sxs-lookup"><span data-stu-id="7f8d8-125">hello initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="7f8d8-126">attività Hello (*cosa*)</span><span class="sxs-lookup"><span data-stu-id="7f8d8-126">hello activity (*what*)</span></span> 
- <span data-ttu-id="7f8d8-127">destinazione Hello</span><span class="sxs-lookup"><span data-stu-id="7f8d8-127">hello target</span></span>

<span data-ttu-id="7f8d8-128">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/18.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="7f8d8-128">![Audit logs](./media/active-directory-reporting-activity-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="7f8d8-129">È possibile personalizzare una visualizzazione elenco hello facendo **colonne** nella barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-129">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="7f8d8-130">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/19.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="7f8d8-130">![Audit logs](./media/active-directory-reporting-activity-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="7f8d8-131">Questo consente toodisplay altri campi o rimuovere campi già visualizzati.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-131">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="7f8d8-132">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/21.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="7f8d8-132">![Audit logs](./media/active-directory-reporting-activity-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="7f8d8-133">Facendo clic su un elemento in visualizzazione elenco hello, ottenere tutte le informazioni disponibili su di esso.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-133">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="7f8d8-134">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/22.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="7f8d8-134">![Audit logs](./media/active-directory-reporting-activity-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="7f8d8-135">Filtro dei log di controllo</span><span class="sxs-lookup"><span data-stu-id="7f8d8-135">Filtering audit logs</span></span>

<span data-ttu-id="7f8d8-136">toonarrow verso il basso hello segnalati livello tooa dati che funziona per l'utente, è possibile filtrare i dati di controllo hello utilizzando hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="7f8d8-136">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="7f8d8-137">Intervallo di date</span><span class="sxs-lookup"><span data-stu-id="7f8d8-137">Date range</span></span>
- <span data-ttu-id="7f8d8-138">Azione avviata da (attore)</span><span class="sxs-lookup"><span data-stu-id="7f8d8-138">Initiated by (Actor)</span></span>
- <span data-ttu-id="7f8d8-139">Categoria</span><span class="sxs-lookup"><span data-stu-id="7f8d8-139">Category</span></span>
- <span data-ttu-id="7f8d8-140">Activity resource type (Tipo di risorsa dell'attività)</span><span class="sxs-lookup"><span data-stu-id="7f8d8-140">Activity resource type</span></span>
- <span data-ttu-id="7f8d8-141">Attività</span><span class="sxs-lookup"><span data-stu-id="7f8d8-141">Activity</span></span>

<span data-ttu-id="7f8d8-142">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/23.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="7f8d8-142">![Audit logs](./media/active-directory-reporting-activity-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="7f8d8-143">Hello **intervallo di date** toodefine tooyou di filtro consente un intervallo di tempo per hello ha restituito dati.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-143">hello **date range** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="7f8d8-144">I valori possibili sono:</span><span class="sxs-lookup"><span data-stu-id="7f8d8-144">Possible values are:</span></span>

- <span data-ttu-id="7f8d8-145">1 mese</span><span class="sxs-lookup"><span data-stu-id="7f8d8-145">1 month</span></span>
- <span data-ttu-id="7f8d8-146">7 giorni</span><span class="sxs-lookup"><span data-stu-id="7f8d8-146">7 days</span></span>
- <span data-ttu-id="7f8d8-147">24 ore</span><span class="sxs-lookup"><span data-stu-id="7f8d8-147">24 hours</span></span>
- <span data-ttu-id="7f8d8-148">Personalizzate</span><span class="sxs-lookup"><span data-stu-id="7f8d8-148">Custom</span></span>

<span data-ttu-id="7f8d8-149">Quando si seleziona un intervallo di tempo personalizzato, è possibile configurare un'ora di inizio e un'ora di fine.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="7f8d8-150">Hello **avviato da** filtro consente toodefine è il nome di un attore o il nome dell'entità universal (UPN).</span><span class="sxs-lookup"><span data-stu-id="7f8d8-150">hello **initiated by** filter enables you toodefine an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="7f8d8-151">Hello **categoria** filtro consente tooselect di hello filtro seguente:</span><span class="sxs-lookup"><span data-stu-id="7f8d8-151">hello **category** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="7f8d8-152">Tutti</span><span class="sxs-lookup"><span data-stu-id="7f8d8-152">All</span></span>
- <span data-ttu-id="7f8d8-153">Categoria principale</span><span class="sxs-lookup"><span data-stu-id="7f8d8-153">Core category</span></span>
- <span data-ttu-id="7f8d8-154">Directory principale</span><span class="sxs-lookup"><span data-stu-id="7f8d8-154">Core directory</span></span>
- <span data-ttu-id="7f8d8-155">Gestione delle password self-service</span><span class="sxs-lookup"><span data-stu-id="7f8d8-155">Self-service password management</span></span>
- <span data-ttu-id="7f8d8-156">Gestione di gruppi self-service</span><span class="sxs-lookup"><span data-stu-id="7f8d8-156">Self-service group management</span></span>
- <span data-ttu-id="7f8d8-157">Provisioning degli account e rollover automatizzato delle password</span><span class="sxs-lookup"><span data-stu-id="7f8d8-157">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="7f8d8-158">Utenti invitati</span><span class="sxs-lookup"><span data-stu-id="7f8d8-158">Invited users</span></span>
- <span data-ttu-id="7f8d8-159">Servizio MIM</span><span class="sxs-lookup"><span data-stu-id="7f8d8-159">MIM service</span></span>
- <span data-ttu-id="7f8d8-160">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="7f8d8-160">Identity Protection</span></span>
- <span data-ttu-id="7f8d8-161">B2C</span><span class="sxs-lookup"><span data-stu-id="7f8d8-161">B2C</span></span>

<span data-ttu-id="7f8d8-162">Hello **il tipo di risorsa attività** filtro consente tooselect hello seguenti filtri:</span><span class="sxs-lookup"><span data-stu-id="7f8d8-162">hello **activity resource type** filter enables you tooselect one of hello following filters:</span></span>

- <span data-ttu-id="7f8d8-163">Tutti</span><span class="sxs-lookup"><span data-stu-id="7f8d8-163">All</span></span> 
- <span data-ttu-id="7f8d8-164">Gruppo</span><span class="sxs-lookup"><span data-stu-id="7f8d8-164">Group</span></span>
- <span data-ttu-id="7f8d8-165">Directory</span><span class="sxs-lookup"><span data-stu-id="7f8d8-165">Directory</span></span>
- <span data-ttu-id="7f8d8-166">Utente</span><span class="sxs-lookup"><span data-stu-id="7f8d8-166">User</span></span>
- <span data-ttu-id="7f8d8-167">Applicazione</span><span class="sxs-lookup"><span data-stu-id="7f8d8-167">Application</span></span>
- <span data-ttu-id="7f8d8-168">Criteri</span><span class="sxs-lookup"><span data-stu-id="7f8d8-168">Policy</span></span>
- <span data-ttu-id="7f8d8-169">Dispositivo</span><span class="sxs-lookup"><span data-stu-id="7f8d8-169">Device</span></span>
- <span data-ttu-id="7f8d8-170">Altre</span><span class="sxs-lookup"><span data-stu-id="7f8d8-170">Other</span></span>

<span data-ttu-id="7f8d8-171">Quando si seleziona **gruppo** come **il tipo di risorsa attività**, si ottiene tooalso a una categoria di filtro aggiuntivo che consente di fornire un **origine**:</span><span class="sxs-lookup"><span data-stu-id="7f8d8-171">When you select **Group** as **activity resource type**, you get an additional filter category that enables you tooalso provide a **Source**:</span></span>

- <span data-ttu-id="7f8d8-172">Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f8d8-172">Azure AD</span></span>
- <span data-ttu-id="7f8d8-173">O365</span><span class="sxs-lookup"><span data-stu-id="7f8d8-173">O365</span></span>


<span data-ttu-id="7f8d8-174">Hello **attività** filtro è basato sulla categoria di hello e selezione tipo di risorsa attività effettuata.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-174">hello **activity** filter is based on hello category and Activity resource type selection you make.</span></span> <span data-ttu-id="7f8d8-175">È possibile selezionare un'attività specifica, è preferibile toosee o scegliere tutte.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-175">You can select a specific activity you want toosee or choose all.</span></span> 

<span data-ttu-id="7f8d8-176">È possibile ottenere l'elenco di hello di tutte le attività di controllo utilizzando l'API Graph https://graph.windows.net/$ hello tenantdomain/attività/auditActivityTypes? api-version = beta, in cui $tenantdomain = il nome di dominio o consultare l'articolo toohello [report di controllo eventi](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="7f8d8-176">You can get hello list of all Audit Activities using hello Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer toohello article [audit report events](active-directory-reporting-audit-events.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="7f8d8-177">Collegamenti ai log di controllo</span><span class="sxs-lookup"><span data-stu-id="7f8d8-177">Audit logs shortcuts</span></span>

<span data-ttu-id="7f8d8-178">Inoltre troppo**Azure Active Directory**, hello portale di Azure offre due punti di ingresso aggiuntivi tooaudit dati:</span><span class="sxs-lookup"><span data-stu-id="7f8d8-178">In addition too**Azure Active Directory**, hello Azure portal provides you with two additional entry points tooaudit data:</span></span>

- <span data-ttu-id="7f8d8-179">Utenti e gruppi</span><span class="sxs-lookup"><span data-stu-id="7f8d8-179">Users and groups</span></span>
- <span data-ttu-id="7f8d8-180">Applicazioni aziendali</span><span class="sxs-lookup"><span data-stu-id="7f8d8-180">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="7f8d8-181">Log di controllo di utenti e gruppi</span><span class="sxs-lookup"><span data-stu-id="7f8d8-181">Users and groups audit logs</span></span>

<span data-ttu-id="7f8d8-182">Con l'utente e i report di controllo in base al gruppo, è possibile ottenere risposte tooquestions, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7f8d8-182">With user and group-based audit reports, you can get answers tooquestions such as:</span></span>

- <span data-ttu-id="7f8d8-183">I tipi di aggiornamenti sono stati gli utenti di applicare hello?</span><span class="sxs-lookup"><span data-stu-id="7f8d8-183">What types of updates have been applied hello users?</span></span>

- <span data-ttu-id="7f8d8-184">Quanti utenti sono stati modificati?</span><span class="sxs-lookup"><span data-stu-id="7f8d8-184">How many users were changed?</span></span>

- <span data-ttu-id="7f8d8-185">Quante password sono state modificate?</span><span class="sxs-lookup"><span data-stu-id="7f8d8-185">How many passwords were changed?</span></span>

- <span data-ttu-id="7f8d8-186">Quali operazioni ha eseguito un amministratore in una directory?</span><span class="sxs-lookup"><span data-stu-id="7f8d8-186">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="7f8d8-187">Quali sono i gruppi che sono stati aggiunti hello?</span><span class="sxs-lookup"><span data-stu-id="7f8d8-187">What are hello groups that have been added?</span></span>

- <span data-ttu-id="7f8d8-188">Sono presenti gruppi con modifiche all'appartenenza?</span><span class="sxs-lookup"><span data-stu-id="7f8d8-188">Are there groups with membership changes?</span></span>

- <span data-ttu-id="7f8d8-189">Sono stati modificati per i proprietari del gruppo hello?</span><span class="sxs-lookup"><span data-stu-id="7f8d8-189">Have hello owners of group been changed?</span></span>

- <span data-ttu-id="7f8d8-190">Le licenze sono state assegnate a un utente o gruppo tooa?</span><span class="sxs-lookup"><span data-stu-id="7f8d8-190">What licenses have been assigned tooa group or a user?</span></span>

<span data-ttu-id="7f8d8-191">Se si desidera tooreview dati toousers correlati e i gruppi di controllo, è possibile trovare una visualizzazione filtrata in **log di controllo** in hello **attività** sezione di hello **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-191">If you just want tooreview auditing data that is related toousers and groups, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Users and Groups**.</span></span> <span data-ttu-id="7f8d8-192">Per questo punto di ingresso, **Tipo di risorsa attività** preselezionato è **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-192">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="7f8d8-193">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/93.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="7f8d8-193">![Audit logs](./media/active-directory-reporting-activity-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="7f8d8-194">Log di controllo di applicazioni aziendali</span><span class="sxs-lookup"><span data-stu-id="7f8d8-194">Enterprise applications audit logs</span></span>

<span data-ttu-id="7f8d8-195">Report di controllo con basato sull'applicazione, è possibile ottenere risposte tooquestions, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7f8d8-195">With application-based audit reports, you can get answers tooquestions such as:</span></span>

* <span data-ttu-id="7f8d8-196">Quali sono le applicazioni che sono stati aggiunti o aggiornate hello?</span><span class="sxs-lookup"><span data-stu-id="7f8d8-196">What are hello applications that have been added or updated?</span></span>
* <span data-ttu-id="7f8d8-197">Quali sono le applicazioni che sono state rimosse hello?</span><span class="sxs-lookup"><span data-stu-id="7f8d8-197">What are hello applications that have been removed?</span></span>
* <span data-ttu-id="7f8d8-198">È stata modificata un'entità servizio per un'applicazione?</span><span class="sxs-lookup"><span data-stu-id="7f8d8-198">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="7f8d8-199">Sono stati modificati i nomi di hello delle applicazioni?</span><span class="sxs-lookup"><span data-stu-id="7f8d8-199">Have hello names of applications been changed?</span></span>
* <span data-ttu-id="7f8d8-200">Che ha fornito il consenso tooan applicazione?</span><span class="sxs-lookup"><span data-stu-id="7f8d8-200">Who gave consent tooan application?</span></span>

<span data-ttu-id="7f8d8-201">Se si desidera controllare i dati di applicazioni correlate tooyour tooreview, è possibile trovare una visualizzazione filtrata in **log di controllo** in hello **attività** sezione di hello **applicazioni aziendali**  blade.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-201">If you just want tooreview auditing data that is related tooyour applications, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Enterprise applications** blade.</span></span> <span data-ttu-id="7f8d8-202">Per questo punto di ingresso, il **Tipo di risorsa attività** preselezionato è **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-202">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="7f8d8-203">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/134.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="7f8d8-203">![Audit logs](./media/active-directory-reporting-activity-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="7f8d8-204">È possibile filtrare la visualizzazione ulteriormente verso il basso toojust **gruppi** o semplicemente **utenti**.</span><span class="sxs-lookup"><span data-stu-id="7f8d8-204">You can filter this view further down toojust **groups** or just **users**.</span></span>

<span data-ttu-id="7f8d8-205">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/25.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="7f8d8-205">![Audit logs](./media/active-directory-reporting-activity-audit-logs/25.png "Audit logs")</span></span>


## <a name="next-steps"></a><span data-ttu-id="7f8d8-206">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f8d8-206">Next steps</span></span>

<span data-ttu-id="7f8d8-207">Per una panoramica di gestione di report, vedere hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7f8d8-207">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

