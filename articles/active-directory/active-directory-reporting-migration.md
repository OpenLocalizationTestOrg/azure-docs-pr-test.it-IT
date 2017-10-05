---
title: "Trovare i report attività nel portale di Azure | Microsoft Docs"
description: "Informazioni su come trovare i report attività di Azure Active Directory nel portale di Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f1875582476c3817b9eb0082b6548cc15043cb98
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="find-activity-reports-in-the-azure-portal"></a><span data-ttu-id="50401-103">Trovare i report attività nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="50401-103">Find activity reports in the Azure portal</span></span>

<span data-ttu-id="50401-104">Se è in corso la migrazione dal portale di Azure classico al portale di Azure, l'aspetto dei log attività di Azure Active Directory (Azure AD) cambierà.</span><span class="sxs-lookup"><span data-stu-id="50401-104">If you are moving from the Azure classic portal to the Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="50401-105">In un recente [post del blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/) viene illustrato come visualizzare i log attività nel contesto della risorsa su cui si sta lavorando nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="50401-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in the context of the resource you are working on in the Azure portal.</span></span> <span data-ttu-id="50401-106">Questo articolo descrive come trovare nel portale di Azure i report usati nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="50401-106">In this article, we describe how to find reports that you used in the Azure classic portal in the Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="50401-107">Novità</span><span class="sxs-lookup"><span data-stu-id="50401-107">What's new</span></span>

<span data-ttu-id="50401-108">I report nel portale di Azure classico sono suddivisi in categorie:</span><span class="sxs-lookup"><span data-stu-id="50401-108">Reports in the Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="50401-109">Report sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="50401-109">Security reports</span></span>
2.  <span data-ttu-id="50401-110">Report sull’attività</span><span class="sxs-lookup"><span data-stu-id="50401-110">Activity reports</span></span>
3.  <span data-ttu-id="50401-111">Report app integrate</span><span class="sxs-lookup"><span data-stu-id="50401-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="50401-112">Report attività e app integrate</span><span class="sxs-lookup"><span data-stu-id="50401-112">Activity and integrated app reports</span></span>

<span data-ttu-id="50401-113">Per i report basati sul contesto nel portale di Azure, i report esistenti vengono uniti in una singola visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="50401-113">For context-based reporting in the Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="50401-114">Una singola API sottostante fornisce i dati alla visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="50401-114">A single, underlying API provides the data to the view.</span></span>

<span data-ttu-id="50401-115">Per accedere a questa visualizzazione, nel pannello **Azure Active Directory**, in **ATTIVITÀ** selezionare **Log di controllo**.</span><span class="sxs-lookup"><span data-stu-id="50401-115">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="50401-116">![Log di controllo](./media/active-directory-reporting-migration/482.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="50401-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="50401-117">In questa visualizzazione sono consolidati i report seguenti:</span><span class="sxs-lookup"><span data-stu-id="50401-117">The following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="50401-118">Report di controllo</span><span class="sxs-lookup"><span data-stu-id="50401-118">Audit report</span></span>
-   <span data-ttu-id="50401-119">Attività di reimpostazione password</span><span class="sxs-lookup"><span data-stu-id="50401-119">Password reset activity</span></span>
-   <span data-ttu-id="50401-120">Attività di registrazione reimpostazione password</span><span class="sxs-lookup"><span data-stu-id="50401-120">Password reset registration activity</span></span>
-   <span data-ttu-id="50401-121">Attività dei gruppi self-service</span><span class="sxs-lookup"><span data-stu-id="50401-121">Self-service groups activity</span></span>
-   <span data-ttu-id="50401-122">Modifiche del nome del gruppo di Office 365</span><span class="sxs-lookup"><span data-stu-id="50401-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="50401-123">Attività di provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="50401-123">Account provisioning activity</span></span>
-   <span data-ttu-id="50401-124">Stato rollover della password</span><span class="sxs-lookup"><span data-stu-id="50401-124">Password rollover status</span></span>
-   <span data-ttu-id="50401-125">Errori di provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="50401-125">Account provisioning errors</span></span>


<span data-ttu-id="50401-126">Il report Utilizzo delle applicazioni è stato migliorato e incluso nella visualizzazione **Accessi**.</span><span class="sxs-lookup"><span data-stu-id="50401-126">The Application Usage report has been enhanced and is included in the **Sign-ins** view.</span></span> <span data-ttu-id="50401-127">Per accedere a questa visualizzazione, nel pannello **Azure Active Directory**, in **ATTIVITÀ** selezionare **Accessi**.</span><span class="sxs-lookup"><span data-stu-id="50401-127">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="50401-128">![Visualizzazione Accessi](./media/active-directory-reporting-migration/483.png "Visualizzazione Accessi")</span><span class="sxs-lookup"><span data-stu-id="50401-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="50401-129">La visualizzazione **Accessi** include tutti gli accessi dell'utente.</span><span class="sxs-lookup"><span data-stu-id="50401-129">The **Sign-ins** view includes all user sign-ins.</span></span> <span data-ttu-id="50401-130">È possibile usare queste informazioni per ottenere informazioni sull'utilizzo dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="50401-130">You can use this information to get application usage information.</span></span> <span data-ttu-id="50401-131">È anche possibile visualizzare le informazioni sull'utilizzo dell'applicazione nella panoramica **Applicazioni aziendali**, nella sezione **GESTISCI**.</span><span class="sxs-lookup"><span data-stu-id="50401-131">You also can view application usage information in the **Enterprise applications** overview, in the **MANAGE** section.</span></span>

<span data-ttu-id="50401-132">![Applicazioni aziendali](./media/active-directory-reporting-migration/484.png "Applicazioni aziendali")</span><span class="sxs-lookup"><span data-stu-id="50401-132">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="50401-133">Accedere a un report specifico</span><span class="sxs-lookup"><span data-stu-id="50401-133">Access a specific report</span></span>

<span data-ttu-id="50401-134">Sebbene il portale di Azure offra una visualizzazione singola, è possibile anche esaminare report specifici.</span><span class="sxs-lookup"><span data-stu-id="50401-134">Although the Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="50401-135">Log di controllo</span><span class="sxs-lookup"><span data-stu-id="50401-135">Audit logs</span></span>

<span data-ttu-id="50401-136">In risposta ai commenti dei clienti, nel portale di Azure è possibile usare filtri avanzati per accedere ai dati.</span><span class="sxs-lookup"><span data-stu-id="50401-136">In response to customer feedback, in the Azure portal, you can use advanced filtering to access the data you want.</span></span> <span data-ttu-id="50401-137">Uno dei filtri che è possibile usare riguarda la *categoria di attività*, che elenca i diversi tipi di log attività disponibili in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50401-137">One filter you can use is an *activity category*, which lists the different types of activity logs in Azure AD.</span></span> <span data-ttu-id="50401-138">Per restringere i risultati della ricerca, è possibile selezionare una categoria.</span><span class="sxs-lookup"><span data-stu-id="50401-138">To narrow results to what you are looking for, you can select a category.</span></span>

<span data-ttu-id="50401-139">Ad esempio, se si è interessati solo alle attività relative alla reimpostazione password self-service, è possibile scegliere la categoria **Self-service Password Management** (Gestione delle password self-service).</span><span class="sxs-lookup"><span data-stu-id="50401-139">For example, if you are interested only in activities related to self-service password resets, you can choose the **Self-service Password Management** category.</span></span> <span data-ttu-id="50401-140">Le categorie visualizzate sono basate sulla risorsa in cui si sta lavorando.</span><span class="sxs-lookup"><span data-stu-id="50401-140">The categories you see are based on the resource you are working in.</span></span>  

<span data-ttu-id="50401-141">![Opzioni Categoria nella pagina Filtra log di controllo](./media/active-directory-reporting-migration/06.png "Opzioni Categoria nella pagina Filtra log di controllo")</span><span class="sxs-lookup"><span data-stu-id="50401-141">![Category options on the Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on the Filter Audit Logs page")</span></span>

<span data-ttu-id="50401-142">Le categorie delle attività includono:</span><span class="sxs-lookup"><span data-stu-id="50401-142">Activity categories include:</span></span>

- <span data-ttu-id="50401-143">Directory principale</span><span class="sxs-lookup"><span data-stu-id="50401-143">Core Directory</span></span>
- <span data-ttu-id="50401-144">Gestione delle password self-service</span><span class="sxs-lookup"><span data-stu-id="50401-144">Self-service Password Management</span></span>
- <span data-ttu-id="50401-145">Gestione gruppi self-service</span><span class="sxs-lookup"><span data-stu-id="50401-145">Self-service Group Management</span></span>
- <span data-ttu-id="50401-146">Provisioning degli account</span><span class="sxs-lookup"><span data-stu-id="50401-146">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="50401-147">Utilizzo applicazioni</span><span class="sxs-lookup"><span data-stu-id="50401-147">Application usage</span></span>

<span data-ttu-id="50401-148">Per visualizzare informazioni dettagliate sull'utilizzo dell'applicazione per tutte le applicazioni o per una singola applicazione, in **ATTIVITÀ** selezionare **Accessi**.</span><span class="sxs-lookup"><span data-stu-id="50401-148">To view details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**.</span></span> <span data-ttu-id="50401-149">Per restringere i risultati, è possibile filtrare in base a nome utente o nome applicazione.</span><span class="sxs-lookup"><span data-stu-id="50401-149">To narrow the results, you can filter on user name or application name.</span></span>

<span data-ttu-id="50401-150">![Pagina Filtra eventi di accesso](./media/active-directory-reporting-migration/07.png "Pagina Filtra eventi di accesso")</span><span class="sxs-lookup"><span data-stu-id="50401-150">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="50401-151">Report sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="50401-151">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="50401-152">Report di Anomalie dell'attività di Azure AD</span><span class="sxs-lookup"><span data-stu-id="50401-152">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="50401-153">I report di sicurezza sulle attività anomale di Azure AD del portale di Azure classico sono stati consolidati per fornire una singola visualizzazione centralizzata.</span><span class="sxs-lookup"><span data-stu-id="50401-153">Azure AD anomalous activity security reports from the Azure classic portal have been consolidated to provide you with one, central view.</span></span> <span data-ttu-id="50401-154">Questa visualizzazione mostra tutti gli eventi di rischio correlati alla sicurezza che Azure AD è in grado di rilevare e segnalare.</span><span class="sxs-lookup"><span data-stu-id="50401-154">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="50401-155">La tabella seguente elenca i report di sicurezza sulle attività anomale di Azure AD e le corrispondenti tipologie degli eventi di rischio nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="50401-155">The following table lists the Azure AD anomalous activity security reports, and corresponding risk event types in the Azure portal.</span></span>

| <span data-ttu-id="50401-156">Report di Anomalie dell'attività di Azure AD</span><span class="sxs-lookup"><span data-stu-id="50401-156">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="50401-157">Tipo di evento di rischio di Identity Protection</span><span class="sxs-lookup"><span data-stu-id="50401-157">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="50401-158">Utenti con credenziali perse</span><span class="sxs-lookup"><span data-stu-id="50401-158">Users with leaked credentials</span></span> | <span data-ttu-id="50401-159">Credenziali perse</span><span class="sxs-lookup"><span data-stu-id="50401-159">Leaked credentials</span></span> |
| <span data-ttu-id="50401-160">Attività di accesso irregolare</span><span class="sxs-lookup"><span data-stu-id="50401-160">Irregular sign-in activity</span></span> | <span data-ttu-id="50401-161">Trasferimento impossibile a posizioni atipiche</span><span class="sxs-lookup"><span data-stu-id="50401-161">Impossible travel to atypical locations</span></span> |
| <span data-ttu-id="50401-162">Accessi da dispositivi potenzialmente infetti</span><span class="sxs-lookup"><span data-stu-id="50401-162">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="50401-163">Accessi da dispositivi infetti</span><span class="sxs-lookup"><span data-stu-id="50401-163">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="50401-164">Accessi da origini sconosciute</span><span class="sxs-lookup"><span data-stu-id="50401-164">Sign-ins from unknown sources</span></span> | <span data-ttu-id="50401-165">Accessi da indirizzi IP anonimi</span><span class="sxs-lookup"><span data-stu-id="50401-165">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="50401-166">Accessi da indirizzi IP con attività sospette</span><span class="sxs-lookup"><span data-stu-id="50401-166">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="50401-167">Accessi da indirizzi IP con attività sospette</span><span class="sxs-lookup"><span data-stu-id="50401-167">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="50401-168">Accessi da posizioni non note</span><span class="sxs-lookup"><span data-stu-id="50401-168">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="50401-169">I report di sicurezza sulle attività anomale di Azure AD seguenti non sono inclusi come eventi di rischio nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="50401-169">The following Azure AD anomalous activity security reports are not included as risk events in the Azure portal:</span></span>

* <span data-ttu-id="50401-170">Accessi dopo più errori</span><span class="sxs-lookup"><span data-stu-id="50401-170">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="50401-171">Accessi da più aree geografiche</span><span class="sxs-lookup"><span data-stu-id="50401-171">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="50401-172">Questi report sono ancora disponibili nel portale di Azure classico, ma in futuro saranno deprecati.</span><span class="sxs-lookup"><span data-stu-id="50401-172">These reports are still available in the Azure classic portal, but they will be deprecated at some time in the future.</span></span>

<span data-ttu-id="50401-173">Per altre informazioni, vedere [Eventi di rischio di Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="50401-173">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="50401-174">Eventi di rischio rilevati</span><span class="sxs-lookup"><span data-stu-id="50401-174">Detected risk events</span></span>

<span data-ttu-id="50401-175">Nel portale di Azure è possibile accedere ai report sugli eventi di rischio rilevati nella sezione **SICUREZZA** del pannello **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="50401-175">In the Azure portal, you can access reports about detected risk events on the **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="50401-176">Gli eventi di rischio rilevati vengono registrati nei report seguenti:</span><span class="sxs-lookup"><span data-stu-id="50401-176">Detected risk events are tracked in the following reports:</span></span>   

- <span data-ttu-id="50401-177">Utenti a rischio</span><span class="sxs-lookup"><span data-stu-id="50401-177">Users at Risk</span></span>
- <span data-ttu-id="50401-178">Accessi a rischio</span><span class="sxs-lookup"><span data-stu-id="50401-178">Risky Sign-ins</span></span>

<span data-ttu-id="50401-179">![Report di sicurezza](./media/active-directory-reporting-migration/04.png "Report di sicurezza")</span><span class="sxs-lookup"><span data-stu-id="50401-179">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="50401-180">Per altre informazioni sui report di sicurezza, vedere:</span><span class="sxs-lookup"><span data-stu-id="50401-180">For more information about security reports, see:</span></span>

- [<span data-ttu-id="50401-181">Report di sicurezza per gli utenti a rischio nel portale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50401-181">Users at Risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="50401-182">Report degli accessi a rischio nel portale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50401-182">Risky Sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-the-azure-classic-portal-vs-the-azure-portal"></a><span data-ttu-id="50401-183">Report sulle attività nel portale di Azure classico rispetto al portale di Azure</span><span class="sxs-lookup"><span data-stu-id="50401-183">Activity reports in the Azure classic portal vs. the Azure portal</span></span>

<span data-ttu-id="50401-184">La tabella in questa sezione elenca i report esistenti nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="50401-184">The table in this section lists existing reports in the Azure classic portal.</span></span> <span data-ttu-id="50401-185">La tabella descrive anche come ottenere le stesse informazioni nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="50401-185">It also describes how you can get the same information in the Azure portal.</span></span>

<span data-ttu-id="50401-186">Per visualizzare tutti i dati di controllo, nel pannello **Azure Active Directory**, in **ATTIVITÀ** andare a **Log di controllo**.</span><span class="sxs-lookup"><span data-stu-id="50401-186">To view all auditing data, on the **Azure Active Directory** blade, under **ACTIVITY**, go to **Audit logs**.</span></span>

<span data-ttu-id="50401-187">![Log di controllo](./media/active-directory-reporting-migration/61.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="50401-187">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="50401-188">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="50401-188">Azure classic portal</span></span>                 | <span data-ttu-id="50401-189">Nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="50401-189">To find in the Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="50401-190">Log di controllo</span><span class="sxs-lookup"><span data-stu-id="50401-190">Audit logs</span></span>                           | <span data-ttu-id="50401-191">Per **Categoria attività** selezionare **Core directory** (Directory principale).</span><span class="sxs-lookup"><span data-stu-id="50401-191">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="50401-192">Attività di reimpostazione password</span><span class="sxs-lookup"><span data-stu-id="50401-192">Password reset activity</span></span>              | <span data-ttu-id="50401-193">Per **Categoria attività** selezionare **Self Service Password Management** (Gestione delle password self-service).</span><span class="sxs-lookup"><span data-stu-id="50401-193">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="50401-194">Attività di registrazione reimpostazione password</span><span class="sxs-lookup"><span data-stu-id="50401-194">Password reset registration activity</span></span> | <span data-ttu-id="50401-195">Per **Categoria attività** selezionare **Self Service Password Management** (Gestione delle password self-service).</span><span class="sxs-lookup"><span data-stu-id="50401-195">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="50401-196">Attività dei gruppi self-service</span><span class="sxs-lookup"><span data-stu-id="50401-196">Self-service groups activity</span></span>         | <span data-ttu-id="50401-197">Per **Categoria attività** selezionare **Gestione gruppi self-service**.</span><span class="sxs-lookup"><span data-stu-id="50401-197">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="50401-198">Attività di provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="50401-198">Account provisioning activity</span></span>        | <span data-ttu-id="50401-199">Per **Categoria attività** selezionare **Account User Provisioning** (Provisioning dell'utente account).</span><span class="sxs-lookup"><span data-stu-id="50401-199">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="50401-200">Stato rollover della password</span><span class="sxs-lookup"><span data-stu-id="50401-200">Password rollover status</span></span>             | <span data-ttu-id="50401-201">Per **Categoria attività** selezionare **Automatic App Password Rollover** (Rollover password app automatico).</span><span class="sxs-lookup"><span data-stu-id="50401-201">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="50401-202">Errori di provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="50401-202">Account provisioning errors</span></span>          | <span data-ttu-id="50401-203">Per **Categoria attività** selezionare **Account User Provisioning** (Provisioning dell'utente account).</span><span class="sxs-lookup"><span data-stu-id="50401-203">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="50401-204">Modifiche del nome del gruppo di Office 365</span><span class="sxs-lookup"><span data-stu-id="50401-204">Office365 Group Name Changes</span></span>         | <span data-ttu-id="50401-205">Per **Categoria attività** selezionare **Self Service Password Management** (Gestione delle password self-service).</span><span class="sxs-lookup"><span data-stu-id="50401-205">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="50401-206">Per **Activity Resource Type** (Tipo di risorsa attività) selezionare **Gruppo**.</span><span class="sxs-lookup"><span data-stu-id="50401-206">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="50401-207">Per **Origine attività** selezionare **O365 groups** (Gruppi di O365).</span><span class="sxs-lookup"><span data-stu-id="50401-207">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="50401-208">Per visualizzare il report **Utilizzo applicazioni**, nel pannello **Azure Active Directory**, in **GESTISCI** selezionare **Applicazioni aziendali** e scegliere **Accessi**.</span><span class="sxs-lookup"><span data-stu-id="50401-208">To view the **Application Usage** report, on the **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="50401-209">![Report degli accessi alle applicazioni aziendali](./media/active-directory-reporting-migration/199.png "Report degli accessi alle applicazioni aziendali")</span><span class="sxs-lookup"><span data-stu-id="50401-209">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="50401-210">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="50401-210">Next steps</span></span>

<span data-ttu-id="50401-211">Per una panoramica della creazione di report, vedere [Creazione di report in Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="50401-211">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
