---
title: "Report delle attività di controllo nel portale di Azure Active Directory | Microsoft Docs"
description: "Introduzione ai report delle attività di controllo nel portale di Azure Active Directory"
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
ms.openlocfilehash: f2d0332d815c82d7d47625e020de2e9c5099deeb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="audit-activity-reports-in-the-azure-active-directory-portal"></a><span data-ttu-id="9d144-103">Report delle attività di controllo nel portale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d144-103">Audit activity reports in the Azure Active Directory portal</span></span> 

<span data-ttu-id="9d144-104">I report di Azure Active Directory (Azure AD) offrono tutte le informazioni necessarie per determinare lo stato dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="9d144-104">With reporting in Azure Active Directory (Azure AD), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="9d144-105">L'architettura di reporting in Azure AD include i componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9d144-105">The reporting architecture in Azure AD consists of the following components:</span></span>

- <span data-ttu-id="9d144-106">**Attività**</span><span class="sxs-lookup"><span data-stu-id="9d144-106">**Activity**</span></span> 
    - <span data-ttu-id="9d144-107">**Attività di accesso** : informazioni sull'utilizzo delle applicazioni gestite e sulle attività di accesso utente</span><span class="sxs-lookup"><span data-stu-id="9d144-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="9d144-108">**Log di controllo**: informazioni relative alle attività di sistema sulla gestione di utenti e gruppi, sulle applicazioni gestite e sulle attività di directory.</span><span class="sxs-lookup"><span data-stu-id="9d144-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="9d144-109">**Sicurezza**</span><span class="sxs-lookup"><span data-stu-id="9d144-109">**Security**</span></span> 
    - <span data-ttu-id="9d144-110">**Accessi a rischio**. Un accesso rischioso è indicativo di un tentativo di accesso che potrebbe essere stato eseguito da qualcuno che non è il legittimo proprietario di un account utente.</span><span class="sxs-lookup"><span data-stu-id="9d144-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="9d144-111">Per informazioni dettagliate, vedere Accessi a rischio.</span><span class="sxs-lookup"><span data-stu-id="9d144-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="9d144-112">**Utenti contrassegnati per il rischio**. Un utente rischioso è indicativo di un account utente che potrebbe essere stato compromesso.</span><span class="sxs-lookup"><span data-stu-id="9d144-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="9d144-113">Per informazioni dettagliate, vedere Utenti contrassegnati per il rischio.</span><span class="sxs-lookup"><span data-stu-id="9d144-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="9d144-114">In questo argomento viene offerta una panoramica delle attività di controllo.</span><span class="sxs-lookup"><span data-stu-id="9d144-114">This topic gives you an overview of the audit activities.</span></span>
 
## <a name="who-can-access-the-data"></a><span data-ttu-id="9d144-115">Chi può accedere ai dati?</span><span class="sxs-lookup"><span data-stu-id="9d144-115">Who can access the data?</span></span>
* <span data-ttu-id="9d144-116">Gli utenti con ruolo di amministratore della sicurezza o con autorizzazioni di lettura per la sicurezza</span><span class="sxs-lookup"><span data-stu-id="9d144-116">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="9d144-117">Gli amministratori globali</span><span class="sxs-lookup"><span data-stu-id="9d144-117">Global Admins</span></span>
* <span data-ttu-id="9d144-118">I singoli utenti (non amministratori) possono visualizzare le proprie attività</span><span class="sxs-lookup"><span data-stu-id="9d144-118">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="9d144-119">Log di controllo</span><span class="sxs-lookup"><span data-stu-id="9d144-119">Audit logs</span></span>

<span data-ttu-id="9d144-120">I log di controllo in Azure Active Directory forniscono i record delle attività di sistema per la conformità.</span><span class="sxs-lookup"><span data-stu-id="9d144-120">The audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="9d144-121">Il primo punto di ingresso a tutti i dati di controllo è **Log di controllo** nella sezione **Attività** di **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d144-121">Your first entry point to all auditing data is **Audit logs** in the **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="9d144-122">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/61.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="9d144-122">![Audit logs](./media/active-directory-reporting-activity-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="9d144-123">Un log di controllo è una visualizzazione elenco predefinita che include:</span><span class="sxs-lookup"><span data-stu-id="9d144-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="9d144-124">Data e ora dell'occorrenza.</span><span class="sxs-lookup"><span data-stu-id="9d144-124">the date and time of the occurrence</span></span>
- <span data-ttu-id="9d144-125">Iniziatore o attore di un'attività (*chi*)</span><span class="sxs-lookup"><span data-stu-id="9d144-125">the initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="9d144-126">Attività (*cosa*)</span><span class="sxs-lookup"><span data-stu-id="9d144-126">the activity (*what*)</span></span> 
- <span data-ttu-id="9d144-127">Destinazione</span><span class="sxs-lookup"><span data-stu-id="9d144-127">the target</span></span>

<span data-ttu-id="9d144-128">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/18.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="9d144-128">![Audit logs](./media/active-directory-reporting-activity-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="9d144-129">Per personalizzare la visualizzazione elenco, fare clic su **Colonne** nella barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="9d144-129">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="9d144-130">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/19.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="9d144-130">![Audit logs](./media/active-directory-reporting-activity-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="9d144-131">In questo modo è possibile visualizzare campi aggiuntivi o rimuovere campi già visualizzati.</span><span class="sxs-lookup"><span data-stu-id="9d144-131">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="9d144-132">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/21.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="9d144-132">![Audit logs](./media/active-directory-reporting-activity-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="9d144-133">Facendo clic su un elemento nella visualizzazione elenco, è possibile ottenere tutti i dettagli disponibili sull'elemento.</span><span class="sxs-lookup"><span data-stu-id="9d144-133">By clicking an item in the list view, you get all available details about it.</span></span>

<span data-ttu-id="9d144-134">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/22.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="9d144-134">![Audit logs](./media/active-directory-reporting-activity-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="9d144-135">Filtro dei log di controllo</span><span class="sxs-lookup"><span data-stu-id="9d144-135">Filtering audit logs</span></span>

<span data-ttu-id="9d144-136">Per limitare i dati segnalati in base alle esigenze, è possibile filtrare i dati di controllo usando i campi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9d144-136">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span></span>

- <span data-ttu-id="9d144-137">Intervallo di date</span><span class="sxs-lookup"><span data-stu-id="9d144-137">Date range</span></span>
- <span data-ttu-id="9d144-138">Azione avviata da (attore)</span><span class="sxs-lookup"><span data-stu-id="9d144-138">Initiated by (Actor)</span></span>
- <span data-ttu-id="9d144-139">Categoria</span><span class="sxs-lookup"><span data-stu-id="9d144-139">Category</span></span>
- <span data-ttu-id="9d144-140">Activity resource type (Tipo di risorsa dell'attività)</span><span class="sxs-lookup"><span data-stu-id="9d144-140">Activity resource type</span></span>
- <span data-ttu-id="9d144-141">Attività</span><span class="sxs-lookup"><span data-stu-id="9d144-141">Activity</span></span>

<span data-ttu-id="9d144-142">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/23.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="9d144-142">![Audit logs](./media/active-directory-reporting-activity-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="9d144-143">Il filtro **Intervallo di date** permette di definire un intervallo di tempo per i dati restituiti.</span><span class="sxs-lookup"><span data-stu-id="9d144-143">The **date range** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="9d144-144">I valori possibili sono:</span><span class="sxs-lookup"><span data-stu-id="9d144-144">Possible values are:</span></span>

- <span data-ttu-id="9d144-145">1 mese</span><span class="sxs-lookup"><span data-stu-id="9d144-145">1 month</span></span>
- <span data-ttu-id="9d144-146">7 giorni</span><span class="sxs-lookup"><span data-stu-id="9d144-146">7 days</span></span>
- <span data-ttu-id="9d144-147">24 ore</span><span class="sxs-lookup"><span data-stu-id="9d144-147">24 hours</span></span>
- <span data-ttu-id="9d144-148">Personalizzate</span><span class="sxs-lookup"><span data-stu-id="9d144-148">Custom</span></span>

<span data-ttu-id="9d144-149">Quando si seleziona un intervallo di tempo personalizzato, è possibile configurare un'ora di inizio e un'ora di fine.</span><span class="sxs-lookup"><span data-stu-id="9d144-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="9d144-150">Il filtro **Avviato da** permette di definire il nome di un attore o il relativo nome UPN (Universal Principal Name).</span><span class="sxs-lookup"><span data-stu-id="9d144-150">The **initiated by** filter enables you to define an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="9d144-151">Il filtro **Categoria** permette di selezionare uno dei filtri seguenti:</span><span class="sxs-lookup"><span data-stu-id="9d144-151">The **category** filter enables you to select one of the following filter:</span></span>

- <span data-ttu-id="9d144-152">Tutti</span><span class="sxs-lookup"><span data-stu-id="9d144-152">All</span></span>
- <span data-ttu-id="9d144-153">Categoria principale</span><span class="sxs-lookup"><span data-stu-id="9d144-153">Core category</span></span>
- <span data-ttu-id="9d144-154">Directory principale</span><span class="sxs-lookup"><span data-stu-id="9d144-154">Core directory</span></span>
- <span data-ttu-id="9d144-155">Gestione delle password self-service</span><span class="sxs-lookup"><span data-stu-id="9d144-155">Self-service password management</span></span>
- <span data-ttu-id="9d144-156">Gestione di gruppi self-service</span><span class="sxs-lookup"><span data-stu-id="9d144-156">Self-service group management</span></span>
- <span data-ttu-id="9d144-157">Provisioning degli account e rollover automatizzato delle password</span><span class="sxs-lookup"><span data-stu-id="9d144-157">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="9d144-158">Utenti invitati</span><span class="sxs-lookup"><span data-stu-id="9d144-158">Invited users</span></span>
- <span data-ttu-id="9d144-159">Servizio MIM</span><span class="sxs-lookup"><span data-stu-id="9d144-159">MIM service</span></span>
- <span data-ttu-id="9d144-160">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="9d144-160">Identity Protection</span></span>
- <span data-ttu-id="9d144-161">B2C</span><span class="sxs-lookup"><span data-stu-id="9d144-161">B2C</span></span>

<span data-ttu-id="9d144-162">Il filtro **Tipo di risorsa attività** permette di selezionare uno dei filtri seguenti:</span><span class="sxs-lookup"><span data-stu-id="9d144-162">The **activity resource type** filter enables you to select one of the following filters:</span></span>

- <span data-ttu-id="9d144-163">Tutti</span><span class="sxs-lookup"><span data-stu-id="9d144-163">All</span></span> 
- <span data-ttu-id="9d144-164">Gruppo</span><span class="sxs-lookup"><span data-stu-id="9d144-164">Group</span></span>
- <span data-ttu-id="9d144-165">Directory</span><span class="sxs-lookup"><span data-stu-id="9d144-165">Directory</span></span>
- <span data-ttu-id="9d144-166">Utente</span><span class="sxs-lookup"><span data-stu-id="9d144-166">User</span></span>
- <span data-ttu-id="9d144-167">Applicazione</span><span class="sxs-lookup"><span data-stu-id="9d144-167">Application</span></span>
- <span data-ttu-id="9d144-168">Criteri</span><span class="sxs-lookup"><span data-stu-id="9d144-168">Policy</span></span>
- <span data-ttu-id="9d144-169">Dispositivo</span><span class="sxs-lookup"><span data-stu-id="9d144-169">Device</span></span>
- <span data-ttu-id="9d144-170">Altri</span><span class="sxs-lookup"><span data-stu-id="9d144-170">Other</span></span>

<span data-ttu-id="9d144-171">Quando si seleziona **Gruppo** come **Tipo di risorsa attività**, si ottiene una categoria di filtro aggiuntiva che permette di specificare anche un'**Origine**:</span><span class="sxs-lookup"><span data-stu-id="9d144-171">When you select **Group** as **activity resource type**, you get an additional filter category that enables you to also provide a **Source**:</span></span>

- <span data-ttu-id="9d144-172">Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d144-172">Azure AD</span></span>
- <span data-ttu-id="9d144-173">O365</span><span class="sxs-lookup"><span data-stu-id="9d144-173">O365</span></span>


<span data-ttu-id="9d144-174">Il filtro **Attività** filtro si basa sulla categoria e sul tipo di risorsa attività selezionati.</span><span class="sxs-lookup"><span data-stu-id="9d144-174">The **activity** filter is based on the category and Activity resource type selection you make.</span></span> <span data-ttu-id="9d144-175">È possibile selezionare un'attività specifica da visualizzare o selezionarle tutte.</span><span class="sxs-lookup"><span data-stu-id="9d144-175">You can select a specific activity you want to see or choose all.</span></span> 

<span data-ttu-id="9d144-176">È possibile ottenere l'elenco di tutte le attività di controllo usando l'API Graph https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, dove $tenantdomain è il nome del dominio. In alternativa, vedere l'articolo relativo agli [eventi del report di controllo](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="9d144-176">You can get the list of all Audit Activities using the Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer to the article [audit report events](active-directory-reporting-audit-events.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="9d144-177">Collegamenti ai log di controllo</span><span class="sxs-lookup"><span data-stu-id="9d144-177">Audit logs shortcuts</span></span>

<span data-ttu-id="9d144-178">Oltre ad **Azure Active Directory**, il portale di Azure offre due ulteriori punti di ingresso ai dati di controllo:</span><span class="sxs-lookup"><span data-stu-id="9d144-178">In addition to **Azure Active Directory**, the Azure portal provides you with two additional entry points to audit data:</span></span>

- <span data-ttu-id="9d144-179">Utenti e gruppi</span><span class="sxs-lookup"><span data-stu-id="9d144-179">Users and groups</span></span>
- <span data-ttu-id="9d144-180">Applicazioni aziendali</span><span class="sxs-lookup"><span data-stu-id="9d144-180">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="9d144-181">Log di controllo di utenti e gruppi</span><span class="sxs-lookup"><span data-stu-id="9d144-181">Users and groups audit logs</span></span>

<span data-ttu-id="9d144-182">Con i report di controllo basati su utenti e gruppi, è possibile ottenere risposte a domande come:</span><span class="sxs-lookup"><span data-stu-id="9d144-182">With user and group-based audit reports, you can get answers to questions such as:</span></span>

- <span data-ttu-id="9d144-183">Quali tipi di aggiornamenti sono stati applicati agli utenti?</span><span class="sxs-lookup"><span data-stu-id="9d144-183">What types of updates have been applied the users?</span></span>

- <span data-ttu-id="9d144-184">Quanti utenti sono stati modificati?</span><span class="sxs-lookup"><span data-stu-id="9d144-184">How many users were changed?</span></span>

- <span data-ttu-id="9d144-185">Quante password sono state modificate?</span><span class="sxs-lookup"><span data-stu-id="9d144-185">How many passwords were changed?</span></span>

- <span data-ttu-id="9d144-186">Quali operazioni ha eseguito un amministratore in una directory?</span><span class="sxs-lookup"><span data-stu-id="9d144-186">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="9d144-187">Quali sono i gruppi che sono stati aggiunti?</span><span class="sxs-lookup"><span data-stu-id="9d144-187">What are the groups that have been added?</span></span>

- <span data-ttu-id="9d144-188">Sono presenti gruppi con modifiche all'appartenenza?</span><span class="sxs-lookup"><span data-stu-id="9d144-188">Are there groups with membership changes?</span></span>

- <span data-ttu-id="9d144-189">I proprietari dei gruppi sono stati modificati?</span><span class="sxs-lookup"><span data-stu-id="9d144-189">Have the owners of group been changed?</span></span>

- <span data-ttu-id="9d144-190">Quali licenze sono state assegnate a un gruppo o a un utente?</span><span class="sxs-lookup"><span data-stu-id="9d144-190">What licenses have been assigned to a group or a user?</span></span>

<span data-ttu-id="9d144-191">Per esaminare semplicemente i dati di controllo relativi a utenti e gruppi, è disponibile una visualizzazione filtrata in **Log di controllo** nella sezione **Attività** di **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9d144-191">If you just want to review auditing data that is related to users and groups, you can find a filtered view under **Audit logs** in the **Activity** section of the **Users and Groups**.</span></span> <span data-ttu-id="9d144-192">Per questo punto di ingresso, **Tipo di risorsa attività** preselezionato è **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9d144-192">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="9d144-193">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/93.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="9d144-193">![Audit logs](./media/active-directory-reporting-activity-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="9d144-194">Log di controllo di applicazioni aziendali</span><span class="sxs-lookup"><span data-stu-id="9d144-194">Enterprise applications audit logs</span></span>

<span data-ttu-id="9d144-195">Con i report di controllo basati sulle applicazioni, è possibile ottenere risposte a domande come:</span><span class="sxs-lookup"><span data-stu-id="9d144-195">With application-based audit reports, you can get answers to questions such as:</span></span>

* <span data-ttu-id="9d144-196">Quali sono le applicazioni che sono state aggiunte o aggiornate?</span><span class="sxs-lookup"><span data-stu-id="9d144-196">What are the applications that have been added or updated?</span></span>
* <span data-ttu-id="9d144-197">Quali sono le applicazioni che sono state rimosse?</span><span class="sxs-lookup"><span data-stu-id="9d144-197">What are the applications that have been removed?</span></span>
* <span data-ttu-id="9d144-198">È stata modificata un'entità servizio per un'applicazione?</span><span class="sxs-lookup"><span data-stu-id="9d144-198">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="9d144-199">I nomi delle applicazioni sono stati modificati?</span><span class="sxs-lookup"><span data-stu-id="9d144-199">Have the names of applications been changed?</span></span>
* <span data-ttu-id="9d144-200">Chi ha dato il consenso a un'applicazione?</span><span class="sxs-lookup"><span data-stu-id="9d144-200">Who gave consent to an application?</span></span>

<span data-ttu-id="9d144-201">Per esaminare semplicemente i dati di controllo relativi alle applicazioni, è disponibile una visualizzazione filtrata in **Log di controllo** nella sezione **Attività** del pannello **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="9d144-201">If you just want to review auditing data that is related to your applications, you can find a filtered view under **Audit logs** in the **Activity** section of the **Enterprise applications** blade.</span></span> <span data-ttu-id="9d144-202">Per questo punto di ingresso, il **Tipo di risorsa attività** preselezionato è **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="9d144-202">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="9d144-203">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/134.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="9d144-203">![Audit logs](./media/active-directory-reporting-activity-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="9d144-204">È possibile filtrare ulteriormente questa visualizzazione per vedere solo i **gruppi** o gli **utenti**.</span><span class="sxs-lookup"><span data-stu-id="9d144-204">You can filter this view further down to just **groups** or just **users**.</span></span>

<span data-ttu-id="9d144-205">![Log di controllo](./media/active-directory-reporting-activity-audit-logs/25.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="9d144-205">![Audit logs](./media/active-directory-reporting-activity-audit-logs/25.png "Audit logs")</span></span>


## <a name="next-steps"></a><span data-ttu-id="9d144-206">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9d144-206">Next steps</span></span>

<span data-ttu-id="9d144-207">Per una panoramica della creazione di report, vedere [Creazione di report in Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9d144-207">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

