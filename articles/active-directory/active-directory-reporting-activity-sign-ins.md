---
title: "report attività aaaSign aggiuntivo nel portale di Azure Active Directory hello | Documenti Microsoft"
description: "Report attività di toosign introduzione nel portale di Azure Active Directory hello"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="faec6-103">Report attività di accesso nel portale di Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="faec6-103">Sign-in activity reports in hello Azure Active Directory portal</span></span>

<span data-ttu-id="faec6-104">Con Azure Active Directory (Azure AD) reporting in hello [portale di Azure](https://portal.azure.com), è possibile ottenere informazioni hello necessarie toodetermine, svolgimento dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="faec6-104">With Azure Active Directory (Azure AD) reporting in hello [Azure portal](https://portal.azure.com), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="faec6-105">architettura di report in Azure Active Directory Hello è costituita da hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="faec6-105">hello reporting architecture in Azure Active Directory consists of hello following components:</span></span>

- <span data-ttu-id="faec6-106">**Attività**</span><span class="sxs-lookup"><span data-stu-id="faec6-106">**Activity**</span></span> 
    - <span data-ttu-id="faec6-107">**Le attività di accesso** – informazioni sull'utilizzo di hello di applicazioni gestite e le attività di accesso dell'utente</span><span class="sxs-lookup"><span data-stu-id="faec6-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="faec6-108">**Log di controllo**: informazioni relative alle attività di sistema sulla gestione di utenti e gruppi, sulle applicazioni gestite e sulle attività di directory.</span><span class="sxs-lookup"><span data-stu-id="faec6-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="faec6-109">**Sicurezza**</span><span class="sxs-lookup"><span data-stu-id="faec6-109">**Security**</span></span> 
    - <span data-ttu-id="faec6-110">**Accessi rischiosi** -un rischiosa l'accesso è un indicatore per un tentativo di accesso che siano stato eseguito da un utente che non è proprietario di legittimo hello di un account utente.</span><span class="sxs-lookup"><span data-stu-id="faec6-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="faec6-111">Per informazioni dettagliate, vedere Accessi a rischio.</span><span class="sxs-lookup"><span data-stu-id="faec6-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="faec6-112">**Utenti contrassegnati per il rischio**. Un utente rischioso è indicativo di un account utente che potrebbe essere stato compromesso.</span><span class="sxs-lookup"><span data-stu-id="faec6-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="faec6-113">Per informazioni dettagliate, vedere Utenti contrassegnati per il rischio.</span><span class="sxs-lookup"><span data-stu-id="faec6-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="faec6-114">In questo argomento fornisce una panoramica delle attività di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="faec6-114">This topic gives you an overview of hello sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="faec6-115">Prerequisito.</span><span class="sxs-lookup"><span data-stu-id="faec6-115">Pre-requisite</span></span>

### <a name="who-can-access-hello-data"></a><span data-ttu-id="faec6-116">Chi può accedere a dati hello?</span><span class="sxs-lookup"><span data-stu-id="faec6-116">Who can access hello data?</span></span>
* <span data-ttu-id="faec6-117">Utenti nel ruolo di amministratore responsabile della sicurezza o di sicurezza Reader hello</span><span class="sxs-lookup"><span data-stu-id="faec6-117">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="faec6-118">Gli amministratori globali</span><span class="sxs-lookup"><span data-stu-id="faec6-118">Global Admins</span></span>
* <span data-ttu-id="faec6-119">Qualsiasi utente (non amministratore) può visualizzare i propri accessi</span><span class="sxs-lookup"><span data-stu-id="faec6-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a><span data-ttu-id="faec6-120">Licenza Azure AD è necessario tooaccess attività di accesso?</span><span class="sxs-lookup"><span data-stu-id="faec6-120">What Azure AD license do you need tooaccess sign-in activity?</span></span>
* <span data-ttu-id="faec6-121">Il tenant deve avere una licenza di Azure AD Premium è report le attività di accesso di hello toosee</span><span class="sxs-lookup"><span data-stu-id="faec6-121">Your tenant must have an Azure AD Premium license associated with it toosee hello all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="faec6-122">Attività di accesso</span><span class="sxs-lookup"><span data-stu-id="faec6-122">Signs-in activities</span></span>

<span data-ttu-id="faec6-123">Con informazioni hello fornite dai report di accesso utente hello, trovare risposte tooquestions, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="faec6-123">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

* <span data-ttu-id="faec6-124">Che cos'è hello sign-in schema di un utente?</span><span class="sxs-lookup"><span data-stu-id="faec6-124">What is hello sign-in pattern of a user?</span></span>
* <span data-ttu-id="faec6-125">Quanti utenti hanno effettuato l'accesso nell'arco di una settimana?</span><span class="sxs-lookup"><span data-stu-id="faec6-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="faec6-126">Qual è stato hello di tali accessi?</span><span class="sxs-lookup"><span data-stu-id="faec6-126">What’s hello status of these sign-ins?</span></span>

<span data-ttu-id="faec6-127">La prima voce tooall punto Accedi attività dati **accessi** nella sezione attività hello **Azure Active**.</span><span class="sxs-lookup"><span data-stu-id="faec6-127">Your first entry point tooall sign-in activities data is **Sign-ins** in hello Activity section of **Azure Active**.</span></span>


<span data-ttu-id="faec6-128">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/61.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="faec6-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="faec6-129">Un log di controllo è una visualizzazione elenco predefinita che include:</span><span class="sxs-lookup"><span data-stu-id="faec6-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="faec6-130">utente correlato Hello</span><span class="sxs-lookup"><span data-stu-id="faec6-130">hello related user</span></span>
- <span data-ttu-id="faec6-131">utente hello dell'applicazione Hello è firmato in</span><span class="sxs-lookup"><span data-stu-id="faec6-131">hello application hello user has signed-in to</span></span>
- <span data-ttu-id="faec6-132">Stato accesso Hello</span><span class="sxs-lookup"><span data-stu-id="faec6-132">hello sign-in status</span></span>
- <span data-ttu-id="faec6-133">ora di accesso Hello</span><span class="sxs-lookup"><span data-stu-id="faec6-133">hello sign-in time</span></span>

<span data-ttu-id="faec6-134">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/41.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="faec6-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="faec6-135">È possibile personalizzare una visualizzazione elenco hello facendo **colonne** nella barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="faec6-135">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="faec6-136">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/19.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="faec6-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="faec6-137">Questo consente toodisplay altri campi o rimuovere campi già visualizzati.</span><span class="sxs-lookup"><span data-stu-id="faec6-137">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="faec6-138">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/42.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="faec6-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="faec6-139">Facendo clic su un elemento in visualizzazione elenco hello, ottenere tutte le informazioni disponibili su di esso.</span><span class="sxs-lookup"><span data-stu-id="faec6-139">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="faec6-140">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/43.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="faec6-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="faec6-141">Filtro delle attività di accesso</span><span class="sxs-lookup"><span data-stu-id="faec6-141">Filtering sign-in activities</span></span>

<span data-ttu-id="faec6-142">toonarrow verso il basso hello segnalati livello tooa dati che funziona per l'utente, è possibile filtrare i dati di accessi hello utilizzando hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="faec6-142">toonarrow down hello reported data tooa level that works for you, you can filter hello sign-ins data using hello following fields:</span></span>

- <span data-ttu-id="faec6-143">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="faec6-143">Time interval</span></span>
- <span data-ttu-id="faec6-144">Utente</span><span class="sxs-lookup"><span data-stu-id="faec6-144">User</span></span>
- <span data-ttu-id="faec6-145">Applicazione</span><span class="sxs-lookup"><span data-stu-id="faec6-145">Application</span></span>
- <span data-ttu-id="faec6-146">Client</span><span class="sxs-lookup"><span data-stu-id="faec6-146">Client</span></span>
- <span data-ttu-id="faec6-147">Stato accesso</span><span class="sxs-lookup"><span data-stu-id="faec6-147">Sign-in status</span></span>

<span data-ttu-id="faec6-148">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/44.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="faec6-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="faec6-149">Hello **intervallo di tempo** toodefine tooyou di filtro consente un intervallo di tempo per hello ha restituito dati.</span><span class="sxs-lookup"><span data-stu-id="faec6-149">hello **time interval** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="faec6-150">I valori possibili sono:</span><span class="sxs-lookup"><span data-stu-id="faec6-150">Possible values are:</span></span>

- <span data-ttu-id="faec6-151">1 mese</span><span class="sxs-lookup"><span data-stu-id="faec6-151">1 month</span></span>
- <span data-ttu-id="faec6-152">7 giorni</span><span class="sxs-lookup"><span data-stu-id="faec6-152">7 days</span></span>
- <span data-ttu-id="faec6-153">24 ore</span><span class="sxs-lookup"><span data-stu-id="faec6-153">24 hours</span></span>
- <span data-ttu-id="faec6-154">Personalizzate</span><span class="sxs-lookup"><span data-stu-id="faec6-154">Custom</span></span>

<span data-ttu-id="faec6-155">Quando si seleziona un intervallo di tempo personalizzato, è possibile configurare un'ora di inizio e un'ora di fine.</span><span class="sxs-lookup"><span data-stu-id="faec6-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="faec6-156">Hello **utente** filtro consente di nome hello toospecify o hello user principal name (UPN) dell'utente hello è rilevante.</span><span class="sxs-lookup"><span data-stu-id="faec6-156">hello **user** filter enables you toospecify hello name or hello user principal name (UPN) of hello user you care about.</span></span>

<span data-ttu-id="faec6-157">Hello **applicazione** filtro consente nome hello toospecify dell'applicazione hello è rilevante.</span><span class="sxs-lookup"><span data-stu-id="faec6-157">hello **application** filter enables you toospecify hello name of hello application you care about.</span></span>

<span data-ttu-id="faec6-158">Hello **client** filtro consente toospecify informazioni sul dispositivo hello è rilevante.</span><span class="sxs-lookup"><span data-stu-id="faec6-158">hello **client** filter enables you toospecify information about hello device you care about.</span></span>

<span data-ttu-id="faec6-159">Hello **stato accesso** filtro consente tooselect di hello filtro seguente:</span><span class="sxs-lookup"><span data-stu-id="faec6-159">hello **sign-in status** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="faec6-160">Tutti</span><span class="sxs-lookup"><span data-stu-id="faec6-160">All</span></span>
- <span data-ttu-id="faec6-161">Success</span><span class="sxs-lookup"><span data-stu-id="faec6-161">Success</span></span>
- <span data-ttu-id="faec6-162">Esito negativo</span><span class="sxs-lookup"><span data-stu-id="faec6-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="faec6-163">Collegamenti alle attività di accesso</span><span class="sxs-lookup"><span data-stu-id="faec6-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="faec6-164">Inoltre tooAzure Active Directory, hello portale di Azure fornisce due voce aggiuntiva punti toosign-in attività dati:</span><span class="sxs-lookup"><span data-stu-id="faec6-164">In addition tooAzure Active Directory, hello Azure portal provides you with two additional entry points toosign-in activities data:</span></span>

- <span data-ttu-id="faec6-165">Utenti e gruppi</span><span class="sxs-lookup"><span data-stu-id="faec6-165">Users and groups</span></span>
- <span data-ttu-id="faec6-166">Applicazioni aziendali</span><span class="sxs-lookup"><span data-stu-id="faec6-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="faec6-167">Attività di accesso di utenti e gruppi</span><span class="sxs-lookup"><span data-stu-id="faec6-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="faec6-168">Con informazioni hello fornite dai report di accesso utente hello, trovare risposte tooquestions, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="faec6-168">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

- <span data-ttu-id="faec6-169">Che cos'è hello sign-in schema di un utente?</span><span class="sxs-lookup"><span data-stu-id="faec6-169">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="faec6-170">Quanti utenti hanno effettuato l'accesso nell'arco di una settimana?</span><span class="sxs-lookup"><span data-stu-id="faec6-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="faec6-171">Qual è stato hello di tali accessi?</span><span class="sxs-lookup"><span data-stu-id="faec6-171">What’s hello status of these sign-ins?</span></span>



<span data-ttu-id="faec6-172">I dati di toothis punto di ingresso sono hello utente Accedi grafico in hello **Panoramica** sezione nel **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="faec6-172">Your entry point toothis data is hello user sign-in graph in hello **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="faec6-173">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/45.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="faec6-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="faec6-174">Hello utente Accedi grafico Mostra aggregazioni settimanale di accesso aggiuntivi per tutti gli utenti in un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="faec6-174">hello user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="faec6-175">valore predefinito di Hello per hello periodo di tempo è 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="faec6-175">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="faec6-176">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/46.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="faec6-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="faec6-177">Quando si fa clic in un giorno nel grafico hello di accesso, si ottiene un elenco dettagliato delle attività di accesso hello per il giorno corrente.</span><span class="sxs-lookup"><span data-stu-id="faec6-177">When you click on a day in hello sign-in graph, you get a detailed list of hello sign-in activities for this day.</span></span>

<span data-ttu-id="faec6-178">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/41.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="faec6-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="faec6-179">Ogni riga hello Accedi attività elenco offre che Hello informazioni dettagliate su hello selezionato Accedi, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="faec6-179">Each row in hello sign-in activities list gives you hello detailed information about hello selected sign-in such as:</span></span>

* <span data-ttu-id="faec6-180">Chi ha effettuato l'accesso?</span><span class="sxs-lookup"><span data-stu-id="faec6-180">Who has signed in?</span></span>
* <span data-ttu-id="faec6-181">Qual era hello correlati UPN?</span><span class="sxs-lookup"><span data-stu-id="faec6-181">What was hello related UPN?</span></span>
* <span data-ttu-id="faec6-182">Individuare l'applicazione è stata hello destinazione Accedi hello?</span><span class="sxs-lookup"><span data-stu-id="faec6-182">What application was hello target of hello sign-in?</span></span>
* <span data-ttu-id="faec6-183">Che cos'è l'indirizzo IP hello del Accedi hello?</span><span class="sxs-lookup"><span data-stu-id="faec6-183">What is hello IP address of hello sign-in?</span></span>
* <span data-ttu-id="faec6-184">Qual era stato hello di Accedi hello?</span><span class="sxs-lookup"><span data-stu-id="faec6-184">What was hello status of hello sign-in?</span></span>

<span data-ttu-id="faec6-185">Hello **accessi** opzione offre una panoramica completa di tutti gli accessi utente.</span><span class="sxs-lookup"><span data-stu-id="faec6-185">hello **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="faec6-186">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/51.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="faec6-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="faec6-187">Utilizzo di applicazioni gestite</span><span class="sxs-lookup"><span data-stu-id="faec6-187">Usage of managed applications</span></span>

<span data-ttu-id="faec6-188">Con una visualizzazione dei dati di accesso basata sulle applicazioni, è possibile rispondere a domande come:</span><span class="sxs-lookup"><span data-stu-id="faec6-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="faec6-189">Chi sta usando le applicazioni?</span><span class="sxs-lookup"><span data-stu-id="faec6-189">Who is using my applications?</span></span>
* <span data-ttu-id="faec6-190">Quali sono prime 3 applicazioni hello nell'organizzazione?</span><span class="sxs-lookup"><span data-stu-id="faec6-190">What are hello top 3 applications in your organization?</span></span>
* <span data-ttu-id="faec6-191">Di recente è stata implementata un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="faec6-191">I have recently rolled out an application.</span></span> <span data-ttu-id="faec6-192">Come sta andando?</span><span class="sxs-lookup"><span data-stu-id="faec6-192">How is it doing?</span></span>

<span data-ttu-id="faec6-193">I dati di toothis punto di ingresso sono hello superiore 3 applicazioni dell'organizzazione all'interno di report di 30 giorni ultimo di hello in hello **Panoramica** sezione nel **applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="faec6-193">Your entry point toothis data is hello top 3 applications in your organization within hello last 30 days report in hello **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="faec6-194">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/64.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="faec6-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="faec6-195">Hello app utilizzo grafico settimanale aggregazioni di accessi per le applicazioni primi 3 in un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="faec6-195">hello app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="faec6-196">valore predefinito di Hello per hello periodo di tempo è 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="faec6-196">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="faec6-197">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/47.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="faec6-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="faec6-198">Se si desidera, è possibile impostare lo stato attivo hello in un'applicazione specifica.</span><span class="sxs-lookup"><span data-stu-id="faec6-198">If you want to, you can set hello focus on a specific application.</span></span>


<span data-ttu-id="faec6-199">![Report](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Report")</span><span class="sxs-lookup"><span data-stu-id="faec6-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="faec6-200">Quando si fa clic in un giorno nel grafico di utilizzo di app hello, ottenere un elenco dettagliato delle attività di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="faec6-200">When you click on a day in hello app usage graph, you get a detailed list of hello sign-in activities.</span></span>


<span data-ttu-id="faec6-201">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/48.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="faec6-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="faec6-202">Hello **accessi** opzione offre una panoramica completa di tutte le applicazioni tooyour eventi di accesso.</span><span class="sxs-lookup"><span data-stu-id="faec6-202">hello **Sign-ins** option gives you a complete overview of all sign-in events tooyour applications.</span></span>

<span data-ttu-id="faec6-203">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/49.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="faec6-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="faec6-204">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="faec6-204">Next steps</span></span>

<span data-ttu-id="faec6-205">Se si desidera tooknow ulteriori informazioni sui codici di errore attività di accesso, vedere hello [Accedi attività report codici di errore nel portale di Azure Active Directory hello](active-directory-reporting-activity-sign-ins-errors.md).</span><span class="sxs-lookup"><span data-stu-id="faec6-205">If you want tooknow more about sign-in activity error codes, see hello [Sign-in activity report error codes in hello Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

