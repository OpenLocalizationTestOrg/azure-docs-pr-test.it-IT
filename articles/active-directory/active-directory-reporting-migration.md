---
title: "report relativi all'attività aaaFind nel portale di Azure hello | Documenti Microsoft"
description: "Informazioni su come i report di attività di Azure Active Directory toofind in hello portale di Azure."
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
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a><span data-ttu-id="fdf6f-103">Individuare i report di attività nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="fdf6f-103">Find activity reports in hello Azure portal</span></span>

<span data-ttu-id="fdf6f-104">Se si sposta da hello Azure toohello portale classico portale di Azure, viene visualizzato un nuovo aspetto log attività di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fdf6f-104">If you are moving from hello Azure classic portal toohello Azure portal, you get a new look at Azure Active Directory (Azure AD) activity logs.</span></span> <span data-ttu-id="fdf6f-105">In un recente [post di blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), viene descritto come è possibile visualizzare il log attività nel contesto di hello della risorsa hello si sta lavorando in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-105">In a recent [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/), we explain how you can see activity logs in hello context of hello resource you are working on in hello Azure portal.</span></span> <span data-ttu-id="fdf6f-106">In questo articolo viene descritto come toofind segnala che è stato utilizzato nel portale di Azure classico nel portale di Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-106">In this article, we describe how toofind reports that you used in hello Azure classic portal in hello Azure portal.</span></span>

## <a name="whats-new"></a><span data-ttu-id="fdf6f-107">Novità</span><span class="sxs-lookup"><span data-stu-id="fdf6f-107">What's new</span></span>

<span data-ttu-id="fdf6f-108">I report nel portale di Azure classico hello sono suddivisi in categorie:</span><span class="sxs-lookup"><span data-stu-id="fdf6f-108">Reports in hello Azure classic portal are separated into categories:</span></span>

1.  <span data-ttu-id="fdf6f-109">Report sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="fdf6f-109">Security reports</span></span>
2.  <span data-ttu-id="fdf6f-110">Report sull’attività</span><span class="sxs-lookup"><span data-stu-id="fdf6f-110">Activity reports</span></span>
3.  <span data-ttu-id="fdf6f-111">Report app integrate</span><span class="sxs-lookup"><span data-stu-id="fdf6f-111">Integrated app reports</span></span>

### <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="fdf6f-112">Report attività e app integrate</span><span class="sxs-lookup"><span data-stu-id="fdf6f-112">Activity and integrated app reports</span></span>

<span data-ttu-id="fdf6f-113">Basata sul contesto dei report nel portale di Azure hello, i report esistenti vengono uniti in una singola visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-113">For context-based reporting in hello Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="fdf6f-114">Una singola API sottostante visualizza hello dati toohello.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-114">A single, underlying API provides hello data toohello view.</span></span>

<span data-ttu-id="fdf6f-115">Questa vista in hello toosee **Azure Active Directory** pannello, in **attività**selezionare **log di controllo**.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-115">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="fdf6f-116">![Log di controllo](./media/active-directory-reporting-migration/482.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="fdf6f-116">![Audit logs](./media/active-directory-reporting-migration/482.png "Audit logs")</span></span>

<span data-ttu-id="fdf6f-117">Hello i report seguenti è consolidato in questa vista:</span><span class="sxs-lookup"><span data-stu-id="fdf6f-117">hello following reports are consolidated in this view:</span></span>

-   <span data-ttu-id="fdf6f-118">Report di controllo</span><span class="sxs-lookup"><span data-stu-id="fdf6f-118">Audit report</span></span>
-   <span data-ttu-id="fdf6f-119">Attività di reimpostazione password</span><span class="sxs-lookup"><span data-stu-id="fdf6f-119">Password reset activity</span></span>
-   <span data-ttu-id="fdf6f-120">Attività di registrazione reimpostazione password</span><span class="sxs-lookup"><span data-stu-id="fdf6f-120">Password reset registration activity</span></span>
-   <span data-ttu-id="fdf6f-121">Attività dei gruppi self-service</span><span class="sxs-lookup"><span data-stu-id="fdf6f-121">Self-service groups activity</span></span>
-   <span data-ttu-id="fdf6f-122">Modifiche del nome del gruppo di Office 365</span><span class="sxs-lookup"><span data-stu-id="fdf6f-122">Office365 Group Name Changes</span></span>
-   <span data-ttu-id="fdf6f-123">Attività di provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="fdf6f-123">Account provisioning activity</span></span>
-   <span data-ttu-id="fdf6f-124">Stato rollover della password</span><span class="sxs-lookup"><span data-stu-id="fdf6f-124">Password rollover status</span></span>
-   <span data-ttu-id="fdf6f-125">Errori di provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="fdf6f-125">Account provisioning errors</span></span>


<span data-ttu-id="fdf6f-126">report di utilizzo dell'applicazione Hello è stata migliorata ed è incluso in hello **accessi** visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-126">hello Application Usage report has been enhanced and is included in hello **Sign-ins** view.</span></span> <span data-ttu-id="fdf6f-127">Questa vista in hello toosee **Azure Active Directory** pannello, in **attività**selezionare **accessi**.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-127">toosee this view, on hello **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="fdf6f-128">![Visualizzazione Accessi](./media/active-directory-reporting-migration/483.png "Visualizzazione Accessi")</span><span class="sxs-lookup"><span data-stu-id="fdf6f-128">![Sign-ins view](./media/active-directory-reporting-migration/483.png "Sign-ins view")</span></span>

<span data-ttu-id="fdf6f-129">Hello **accessi** visualizzazione include tutti gli accessi utente. È possibile utilizzare queste informazioni sull'utilizzo di informazioni tooget applicazione.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-129">hello **Sign-ins** view includes all user sign-ins. You can use this information tooget application usage information.</span></span> <span data-ttu-id="fdf6f-130">È inoltre possibile visualizzare informazioni sull'utilizzo dell'applicazione in hello **applicazioni aziendali** panoramica, in hello **GESTISCI** sezione.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-130">You also can view application usage information in hello **Enterprise applications** overview, in hello **MANAGE** section.</span></span>

<span data-ttu-id="fdf6f-131">![Applicazioni aziendali](./media/active-directory-reporting-migration/484.png "Applicazioni aziendali")</span><span class="sxs-lookup"><span data-stu-id="fdf6f-131">![Enterprise applications](./media/active-directory-reporting-migration/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="fdf6f-132">Accedere a un report specifico</span><span class="sxs-lookup"><span data-stu-id="fdf6f-132">Access a specific report</span></span>

<span data-ttu-id="fdf6f-133">Sebbene hello portale di Azure offre una visualizzazione singola, è anche possibile esaminare i report specifici.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-133">Although hello Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="fdf6f-134">Log di controllo</span><span class="sxs-lookup"><span data-stu-id="fdf6f-134">Audit logs</span></span>

<span data-ttu-id="fdf6f-135">In commenti e suggerimenti toocustomer risposta, in hello portale di Azure, è possibile utilizzare avanzate dati hello tooaccess filtro desiderati.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-135">In response toocustomer feedback, in hello Azure portal, you can use advanced filtering tooaccess hello data you want.</span></span> <span data-ttu-id="fdf6f-136">È un filtro, è possibile utilizzare un *categoria attività*, che sono elencati hello diversi tipi di attività registra in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-136">One filter you can use is an *activity category*, which lists hello different types of activity logs in Azure AD.</span></span> <span data-ttu-id="fdf6f-137">toonarrow risultati toowhat che si sta cercando, è possibile selezionare una categoria.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-137">toonarrow results toowhat you are looking for, you can select a category.</span></span>

<span data-ttu-id="fdf6f-138">Ad esempio, se si è interessati solo la reimpostazione della password di tooself servizio correlato di attività, è possibile scegliere hello **la gestione delle Password Self-Service** categoria.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-138">For example, if you are interested only in activities related tooself-service password resets, you can choose hello **Self-service Password Management** category.</span></span> <span data-ttu-id="fdf6f-139">categorie di Hello che vedrai si basano sulla risorsa hello in che ci si trova.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-139">hello categories you see are based on hello resource you are working in.</span></span>  

<span data-ttu-id="fdf6f-140">![Le opzioni di categoria nella pagina di log di controllo filtro hello](./media/active-directory-reporting-migration/06.png "opzioni categoria hello filtro registri di controllo pagina")</span><span class="sxs-lookup"><span data-stu-id="fdf6f-140">![Category options on hello Filter Audit Logs page](./media/active-directory-reporting-migration/06.png "Category options on hello Filter Audit Logs page")</span></span>

<span data-ttu-id="fdf6f-141">Le categorie delle attività includono:</span><span class="sxs-lookup"><span data-stu-id="fdf6f-141">Activity categories include:</span></span>

- <span data-ttu-id="fdf6f-142">Directory principale</span><span class="sxs-lookup"><span data-stu-id="fdf6f-142">Core Directory</span></span>
- <span data-ttu-id="fdf6f-143">Gestione delle password self-service</span><span class="sxs-lookup"><span data-stu-id="fdf6f-143">Self-service Password Management</span></span>
- <span data-ttu-id="fdf6f-144">Gestione gruppi self-service</span><span class="sxs-lookup"><span data-stu-id="fdf6f-144">Self-service Group Management</span></span>
- <span data-ttu-id="fdf6f-145">Provisioning degli account</span><span class="sxs-lookup"><span data-stu-id="fdf6f-145">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="fdf6f-146">Utilizzo applicazioni</span><span class="sxs-lookup"><span data-stu-id="fdf6f-146">Application usage</span></span>

<span data-ttu-id="fdf6f-147">tooview i dettagli sull'utilizzo dell'applicazione per tutte le app o per una singola applicazione, in **attività**selezionare **accessi**. risultati hello toonarrow, sarà possibile filtrare per nome utente o nome dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-147">tooview details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**. toonarrow hello results, you can filter on user name or application name.</span></span>

<span data-ttu-id="fdf6f-148">![Pagina Filtra eventi di accesso](./media/active-directory-reporting-migration/07.png "Pagina Filtra eventi di accesso")</span><span class="sxs-lookup"><span data-stu-id="fdf6f-148">![Filter Sign-In Events page](./media/active-directory-reporting-migration/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="fdf6f-149">Report sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="fdf6f-149">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="fdf6f-150">Report di Anomalie dell'attività di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdf6f-150">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="fdf6f-151">Sicurezza di Azure AD attività anomale report dal portale di Azure classico hello sono stati consolidati tooprovide con a una vista centrale.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-151">Azure AD anomalous activity security reports from hello Azure classic portal have been consolidated tooprovide you with one, central view.</span></span> <span data-ttu-id="fdf6f-152">Questa visualizzazione mostra tutti gli eventi di rischio correlati alla sicurezza che Azure AD è in grado di rilevare e segnalare.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-152">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="fdf6f-153">Hello nella tabella seguente elenca i report di sicurezza di attività anomale hello Azure AD e corrispondenti tipi di eventi di rischio in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-153">hello following table lists hello Azure AD anomalous activity security reports, and corresponding risk event types in hello Azure portal.</span></span>

| <span data-ttu-id="fdf6f-154">Report di Anomalie dell'attività di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdf6f-154">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="fdf6f-155">Tipo di evento di rischio di Identity Protection</span><span class="sxs-lookup"><span data-stu-id="fdf6f-155">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="fdf6f-156">Utenti con credenziali perse</span><span class="sxs-lookup"><span data-stu-id="fdf6f-156">Users with leaked credentials</span></span> | <span data-ttu-id="fdf6f-157">Credenziali perse</span><span class="sxs-lookup"><span data-stu-id="fdf6f-157">Leaked credentials</span></span> |
| <span data-ttu-id="fdf6f-158">Attività di accesso irregolare</span><span class="sxs-lookup"><span data-stu-id="fdf6f-158">Irregular sign-in activity</span></span> | <span data-ttu-id="fdf6f-159">Comunicazione Impossibile tooatypical percorsi</span><span class="sxs-lookup"><span data-stu-id="fdf6f-159">Impossible travel tooatypical locations</span></span> |
| <span data-ttu-id="fdf6f-160">Accessi da dispositivi potenzialmente infetti</span><span class="sxs-lookup"><span data-stu-id="fdf6f-160">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="fdf6f-161">Accessi da dispositivi infetti</span><span class="sxs-lookup"><span data-stu-id="fdf6f-161">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="fdf6f-162">Accessi da origini sconosciute</span><span class="sxs-lookup"><span data-stu-id="fdf6f-162">Sign-ins from unknown sources</span></span> | <span data-ttu-id="fdf6f-163">Accessi da indirizzi IP anonimi</span><span class="sxs-lookup"><span data-stu-id="fdf6f-163">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="fdf6f-164">Accessi da indirizzi IP con attività sospette</span><span class="sxs-lookup"><span data-stu-id="fdf6f-164">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="fdf6f-165">Accessi da indirizzi IP con attività sospette</span><span class="sxs-lookup"><span data-stu-id="fdf6f-165">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="fdf6f-166">Accessi da posizioni non note</span><span class="sxs-lookup"><span data-stu-id="fdf6f-166">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="fdf6f-167">sicurezza di Azure AD attività anomale seguenti Hello report non sono inclusi come eventi di rischio in hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="fdf6f-167">hello following Azure AD anomalous activity security reports are not included as risk events in hello Azure portal:</span></span>

* <span data-ttu-id="fdf6f-168">Accessi dopo più errori</span><span class="sxs-lookup"><span data-stu-id="fdf6f-168">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="fdf6f-169">Accessi da più aree geografiche</span><span class="sxs-lookup"><span data-stu-id="fdf6f-169">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="fdf6f-170">Questi report sono ancora disponibili nel portale di Azure classico hello, ma sarà deprecate in un momento nel futuro hello.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-170">These reports are still available in hello Azure classic portal, but they will be deprecated at some time in hello future.</span></span>

<span data-ttu-id="fdf6f-171">Per altre informazioni, vedere [Eventi di rischio di Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="fdf6f-171">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="fdf6f-172">Eventi di rischio rilevati</span><span class="sxs-lookup"><span data-stu-id="fdf6f-172">Detected risk events</span></span>

<span data-ttu-id="fdf6f-173">Nel portale di Azure hello, è possibile accedere a report sugli eventi di rischio rilevati in hello **Azure Active Directory** pannello, in **sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-173">In hello Azure portal, you can access reports about detected risk events on hello **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="fdf6f-174">Eventi di rischio rilevati vengono rilevati in hello seguenti report:</span><span class="sxs-lookup"><span data-stu-id="fdf6f-174">Detected risk events are tracked in hello following reports:</span></span>   

- <span data-ttu-id="fdf6f-175">Utenti a rischio</span><span class="sxs-lookup"><span data-stu-id="fdf6f-175">Users at Risk</span></span>
- <span data-ttu-id="fdf6f-176">Accessi a rischio</span><span class="sxs-lookup"><span data-stu-id="fdf6f-176">Risky Sign-ins</span></span>

<span data-ttu-id="fdf6f-177">![Report di sicurezza](./media/active-directory-reporting-migration/04.png "Report di sicurezza")</span><span class="sxs-lookup"><span data-stu-id="fdf6f-177">![Security reports](./media/active-directory-reporting-migration/04.png "Security reports")</span></span>

<span data-ttu-id="fdf6f-178">Per altre informazioni sui report di sicurezza, vedere:</span><span class="sxs-lookup"><span data-stu-id="fdf6f-178">For more information about security reports, see:</span></span>

- [<span data-ttu-id="fdf6f-179">Utenti dei report di rischio per la sicurezza nel portale di Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="fdf6f-179">Users at Risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="fdf6f-180">Report accessi rischiosa nel portale di Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="fdf6f-180">Risky Sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a><span data-ttu-id="fdf6f-181">Report attività hello portale di Azure classico e hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fdf6f-181">Activity reports in hello Azure classic portal vs. hello Azure portal</span></span>

<span data-ttu-id="fdf6f-182">tabella Hello in questa sezione sono elencati i report esistenti nel portale di Azure classico hello.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-182">hello table in this section lists existing reports in hello Azure classic portal.</span></span> <span data-ttu-id="fdf6f-183">Viene inoltre descritto come ottenere hello stesse informazioni nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-183">It also describes how you can get hello same information in hello Azure portal.</span></span>

<span data-ttu-id="fdf6f-184">tooview tutti i dati, in hello del controllo **Azure Active Directory** pannello, in **attività**, andare troppo**log di controllo**.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-184">tooview all auditing data, on hello **Azure Active Directory** blade, under **ACTIVITY**, go too**Audit logs**.</span></span>

<span data-ttu-id="fdf6f-185">![Log di controllo](./media/active-directory-reporting-migration/61.png "Log di controllo")</span><span class="sxs-lookup"><span data-stu-id="fdf6f-185">![Audit logs](./media/active-directory-reporting-migration/61.png "Audit logs")</span></span>

| <span data-ttu-id="fdf6f-186">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="fdf6f-186">Azure classic portal</span></span>                 | <span data-ttu-id="fdf6f-187">toofind in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fdf6f-187">toofind in hello Azure portal</span></span>                                                         |
| ---                                  | ---                                                                        |
| <span data-ttu-id="fdf6f-188">Log di controllo</span><span class="sxs-lookup"><span data-stu-id="fdf6f-188">Audit logs</span></span>                           | <span data-ttu-id="fdf6f-189">Per **Categoria attività** selezionare **Core directory** (Directory principale).</span><span class="sxs-lookup"><span data-stu-id="fdf6f-189">For **Activity Category**, select **Core Directory**.</span></span>                       |
| <span data-ttu-id="fdf6f-190">Attività di reimpostazione password</span><span class="sxs-lookup"><span data-stu-id="fdf6f-190">Password reset activity</span></span>              | <span data-ttu-id="fdf6f-191">Per **Categoria attività** selezionare **Self Service Password Management** (Gestione delle password self-service).</span><span class="sxs-lookup"><span data-stu-id="fdf6f-191">For **Activity Category**, select **Self-service Password Management**.</span></span> |
| <span data-ttu-id="fdf6f-192">Attività di registrazione reimpostazione password</span><span class="sxs-lookup"><span data-stu-id="fdf6f-192">Password reset registration activity</span></span> | <span data-ttu-id="fdf6f-193">Per **Categoria attività** selezionare **Self Service Password Management** (Gestione delle password self-service).</span><span class="sxs-lookup"><span data-stu-id="fdf6f-193">For **Activity Category**, select **Self-service Password Management**.</span></span>     |
| <span data-ttu-id="fdf6f-194">Attività dei gruppi self-service</span><span class="sxs-lookup"><span data-stu-id="fdf6f-194">Self-service groups activity</span></span>         | <span data-ttu-id="fdf6f-195">Per **Categoria attività** selezionare **Gestione gruppi self-service**.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-195">For **Activity Category**, select **Self-service Group Management**.</span></span>        |
| <span data-ttu-id="fdf6f-196">Attività di provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="fdf6f-196">Account provisioning activity</span></span>        | <span data-ttu-id="fdf6f-197">Per **Categoria attività** selezionare **Account User Provisioning** (Provisioning dell'utente account).</span><span class="sxs-lookup"><span data-stu-id="fdf6f-197">For **Activity Category**, select **Account User Provisioning**.</span></span>         |
| <span data-ttu-id="fdf6f-198">Stato rollover della password</span><span class="sxs-lookup"><span data-stu-id="fdf6f-198">Password rollover status</span></span>             | <span data-ttu-id="fdf6f-199">Per **Categoria attività** selezionare **Automatic App Password Rollover** (Rollover password app automatico).</span><span class="sxs-lookup"><span data-stu-id="fdf6f-199">For **Activity Category**, select **Automatic App Password Rollover**.</span></span>      |
| <span data-ttu-id="fdf6f-200">Errori di provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="fdf6f-200">Account provisioning errors</span></span>          | <span data-ttu-id="fdf6f-201">Per **Categoria attività** selezionare **Account User Provisioning** (Provisioning dell'utente account).</span><span class="sxs-lookup"><span data-stu-id="fdf6f-201">For **Activity Category**, select **Account User Provisioning**.</span></span>        |
| <span data-ttu-id="fdf6f-202">Modifiche del nome del gruppo di Office 365</span><span class="sxs-lookup"><span data-stu-id="fdf6f-202">Office365 Group Name Changes</span></span>         | <span data-ttu-id="fdf6f-203">Per **Categoria attività** selezionare **Self Service Password Management** (Gestione delle password self-service).</span><span class="sxs-lookup"><span data-stu-id="fdf6f-203">For **Activity Category**, select **Self-service Password Management**.</span></span> <span data-ttu-id="fdf6f-204">Per **Activity Resource Type** (Tipo di risorsa attività) selezionare **Gruppo**.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-204">For **Activity Resource Type**, select **Group**.</span></span> <span data-ttu-id="fdf6f-205">Per **Origine attività** selezionare **O365 groups** (Gruppi di O365).</span><span class="sxs-lookup"><span data-stu-id="fdf6f-205">For **Activity Source**, select **O365 groups**.</span></span>|

<span data-ttu-id="fdf6f-206">hello tooview **utilizzo dell'applicazione** hello report **Azure Active Directory** pannello, in **GESTISCI**selezionare **applicazioni aziendali**, quindi selezionare **accessi**.</span><span class="sxs-lookup"><span data-stu-id="fdf6f-206">tooview hello **Application Usage** report, on hello **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


<span data-ttu-id="fdf6f-207">![Report degli accessi alle applicazioni aziendali](./media/active-directory-reporting-migration/199.png "Report degli accessi alle applicazioni aziendali")</span><span class="sxs-lookup"><span data-stu-id="fdf6f-207">![Enterprise Applications Sign-Ins report](./media/active-directory-reporting-migration/199.png "Enterprise Applications Sign-Ins report")</span></span>

## <a name="next-steps"></a><span data-ttu-id="fdf6f-208">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fdf6f-208">Next steps</span></span>

<span data-ttu-id="fdf6f-209">Per una panoramica di gestione di report, vedere hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fdf6f-209">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
