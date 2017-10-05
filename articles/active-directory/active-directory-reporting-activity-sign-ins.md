---
title: "Report delle attività di accesso nel portale di Azure Active Directory | Microsoft Docs"
description: "Introduzione ai report delle attività di accesso nel portale di Azure Active Directory"
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
ms.openlocfilehash: b9e61950654ba427b09dd608d354589a0804aaa5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-activity-reports-in-the-azure-active-directory-portal"></a><span data-ttu-id="606f5-103">Report delle attività di accesso nel portale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="606f5-103">Sign-in activity reports in the Azure Active Directory portal</span></span>

<span data-ttu-id="606f5-104">I report di Azure Active Directory (Azure AD) nel [portale di Azure](https://portal.azure.com) offrono tutte le informazioni necessarie per determinare lo stato dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="606f5-104">With Azure Active Directory (Azure AD) reporting in the [Azure portal](https://portal.azure.com), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="606f5-105">L'architettura di reporting in Azure Active Directory include i componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="606f5-105">The reporting architecture in Azure Active Directory consists of the following components:</span></span>

- <span data-ttu-id="606f5-106">**Attività**</span><span class="sxs-lookup"><span data-stu-id="606f5-106">**Activity**</span></span> 
    - <span data-ttu-id="606f5-107">**Attività di accesso** : informazioni sull'utilizzo delle applicazioni gestite e sulle attività di accesso utente</span><span class="sxs-lookup"><span data-stu-id="606f5-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="606f5-108">**Log di controllo**: informazioni relative alle attività di sistema sulla gestione di utenti e gruppi, sulle applicazioni gestite e sulle attività di directory.</span><span class="sxs-lookup"><span data-stu-id="606f5-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="606f5-109">**Sicurezza**</span><span class="sxs-lookup"><span data-stu-id="606f5-109">**Security**</span></span> 
    - <span data-ttu-id="606f5-110">**Accessi a rischio**. Un accesso rischioso è indicativo di un tentativo di accesso che potrebbe essere stato eseguito da qualcuno che non è il legittimo proprietario di un account utente.</span><span class="sxs-lookup"><span data-stu-id="606f5-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="606f5-111">Per informazioni dettagliate, vedere Accessi a rischio.</span><span class="sxs-lookup"><span data-stu-id="606f5-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="606f5-112">**Utenti contrassegnati per il rischio**. Un utente rischioso è indicativo di un account utente che potrebbe essere stato compromesso.</span><span class="sxs-lookup"><span data-stu-id="606f5-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="606f5-113">Per informazioni dettagliate, vedere Utenti contrassegnati per il rischio.</span><span class="sxs-lookup"><span data-stu-id="606f5-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="606f5-114">In questo argomento viene offerta una panoramica delle attività di accesso.</span><span class="sxs-lookup"><span data-stu-id="606f5-114">This topic gives you an overview of the sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="606f5-115">Prerequisito.</span><span class="sxs-lookup"><span data-stu-id="606f5-115">Pre-requisite</span></span>

### <a name="who-can-access-the-data"></a><span data-ttu-id="606f5-116">Chi può accedere ai dati?</span><span class="sxs-lookup"><span data-stu-id="606f5-116">Who can access the data?</span></span>
* <span data-ttu-id="606f5-117">Gli utenti con ruolo di amministratore della sicurezza o con autorizzazioni di lettura per la sicurezza</span><span class="sxs-lookup"><span data-stu-id="606f5-117">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="606f5-118">Gli amministratori globali</span><span class="sxs-lookup"><span data-stu-id="606f5-118">Global Admins</span></span>
* <span data-ttu-id="606f5-119">Qualsiasi utente (non amministratore) può visualizzare i propri accessi</span><span class="sxs-lookup"><span data-stu-id="606f5-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-to-access-sign-in-activity"></a><span data-ttu-id="606f5-120">Quale licenza di Azure AD è necessaria per visualizzare le attività di accesso?</span><span class="sxs-lookup"><span data-stu-id="606f5-120">What Azure AD license do you need to access sign-in activity?</span></span>
* <span data-ttu-id="606f5-121">Per visualizzare il report completo delle attività di accesso, è necessario che al tenant sia associata una licenza di Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="606f5-121">Your tenant must have an Azure AD Premium license associated with it to see the all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="606f5-122">Attività di accesso</span><span class="sxs-lookup"><span data-stu-id="606f5-122">Signs-in activities</span></span>

<span data-ttu-id="606f5-123">Le informazioni contenute nel report relativo all'accesso utente consentono di rispondere a domande come le seguenti:</span><span class="sxs-lookup"><span data-stu-id="606f5-123">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

* <span data-ttu-id="606f5-124">Qual è il modello di accesso di un utente?</span><span class="sxs-lookup"><span data-stu-id="606f5-124">What is the sign-in pattern of a user?</span></span>
* <span data-ttu-id="606f5-125">Quanti utenti hanno effettuato l'accesso nell'arco di una settimana?</span><span class="sxs-lookup"><span data-stu-id="606f5-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="606f5-126">Qual è lo stato di questi accessi?</span><span class="sxs-lookup"><span data-stu-id="606f5-126">What’s the status of these sign-ins?</span></span>

<span data-ttu-id="606f5-127">Il primo punto di ingresso a tutte le attività di accesso è **Accessi** nella sezione **Attività** di Azure Active</span><span class="sxs-lookup"><span data-stu-id="606f5-127">Your first entry point to all sign-in activities data is **Sign-ins** in the Activity section of **Azure Active**.</span></span>


<span data-ttu-id="606f5-128">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/61.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="606f5-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="606f5-129">Un log di controllo è una visualizzazione elenco predefinita che include:</span><span class="sxs-lookup"><span data-stu-id="606f5-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="606f5-130">Utente correlato.</span><span class="sxs-lookup"><span data-stu-id="606f5-130">the related user</span></span>
- <span data-ttu-id="606f5-131">Applicazione a cui l'utente ha eseguito l'accesso.</span><span class="sxs-lookup"><span data-stu-id="606f5-131">the application the user has signed-in to</span></span>
- <span data-ttu-id="606f5-132">Stato dell'accesso.</span><span class="sxs-lookup"><span data-stu-id="606f5-132">the sign-in status</span></span>
- <span data-ttu-id="606f5-133">Orario di accesso.</span><span class="sxs-lookup"><span data-stu-id="606f5-133">the sign-in time</span></span>

<span data-ttu-id="606f5-134">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/41.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="606f5-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="606f5-135">Per personalizzare la visualizzazione elenco, fare clic su **Colonne** nella barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="606f5-135">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="606f5-136">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/19.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="606f5-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="606f5-137">In questo modo è possibile visualizzare campi aggiuntivi o rimuovere campi già visualizzati.</span><span class="sxs-lookup"><span data-stu-id="606f5-137">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="606f5-138">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/42.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="606f5-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="606f5-139">Facendo clic su un elemento nella visualizzazione elenco, è possibile ottenere tutti i dettagli disponibili sull'elemento.</span><span class="sxs-lookup"><span data-stu-id="606f5-139">By clicking an item in the list view, you get all available details about it.</span></span>

<span data-ttu-id="606f5-140">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/43.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="606f5-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="606f5-141">Filtro delle attività di accesso</span><span class="sxs-lookup"><span data-stu-id="606f5-141">Filtering sign-in activities</span></span>

<span data-ttu-id="606f5-142">Per limitare i dati segnalati in base alle esigenze, è possibile filtrare i dati di accesso usando i campi seguenti:</span><span class="sxs-lookup"><span data-stu-id="606f5-142">To narrow down the reported data to a level that works for you, you can filter the sign-ins data using the following fields:</span></span>

- <span data-ttu-id="606f5-143">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="606f5-143">Time interval</span></span>
- <span data-ttu-id="606f5-144">Utente</span><span class="sxs-lookup"><span data-stu-id="606f5-144">User</span></span>
- <span data-ttu-id="606f5-145">Applicazione</span><span class="sxs-lookup"><span data-stu-id="606f5-145">Application</span></span>
- <span data-ttu-id="606f5-146">Client</span><span class="sxs-lookup"><span data-stu-id="606f5-146">Client</span></span>
- <span data-ttu-id="606f5-147">Stato accesso</span><span class="sxs-lookup"><span data-stu-id="606f5-147">Sign-in status</span></span>

<span data-ttu-id="606f5-148">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/44.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="606f5-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="606f5-149">Il filtro **Intervallo di tempo** permette di definire un intervallo di tempo per i dati restituiti.</span><span class="sxs-lookup"><span data-stu-id="606f5-149">The **time interval** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="606f5-150">I valori possibili sono:</span><span class="sxs-lookup"><span data-stu-id="606f5-150">Possible values are:</span></span>

- <span data-ttu-id="606f5-151">1 mese</span><span class="sxs-lookup"><span data-stu-id="606f5-151">1 month</span></span>
- <span data-ttu-id="606f5-152">7 giorni</span><span class="sxs-lookup"><span data-stu-id="606f5-152">7 days</span></span>
- <span data-ttu-id="606f5-153">24 ore</span><span class="sxs-lookup"><span data-stu-id="606f5-153">24 hours</span></span>
- <span data-ttu-id="606f5-154">Personalizzate</span><span class="sxs-lookup"><span data-stu-id="606f5-154">Custom</span></span>

<span data-ttu-id="606f5-155">Quando si seleziona un intervallo di tempo personalizzato, è possibile configurare un'ora di inizio e un'ora di fine.</span><span class="sxs-lookup"><span data-stu-id="606f5-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="606f5-156">Il filtro **Utente** permette di specificare il nome o il nome dell'entità utente (UPN) per l'utente richiesto.</span><span class="sxs-lookup"><span data-stu-id="606f5-156">The **user** filter enables you to specify the name or the user principal name (UPN) of the user you care about.</span></span>

<span data-ttu-id="606f5-157">Il filtro **Applicazione** permette di specificare il nome dell'applicazione richiesta.</span><span class="sxs-lookup"><span data-stu-id="606f5-157">The **application** filter enables you to specify the name of the application you care about.</span></span>

<span data-ttu-id="606f5-158">Il filtro **Client** permette di specificare informazioni sul dispositivo richiesto.</span><span class="sxs-lookup"><span data-stu-id="606f5-158">The **client** filter enables you to specify information about the device you care about.</span></span>

<span data-ttu-id="606f5-159">Il filtro **Stato accesso** permette di selezionare uno dei filtri seguenti:</span><span class="sxs-lookup"><span data-stu-id="606f5-159">The **sign-in status** filter enables you to select one of the following filter:</span></span>

- <span data-ttu-id="606f5-160">Tutti</span><span class="sxs-lookup"><span data-stu-id="606f5-160">All</span></span>
- <span data-ttu-id="606f5-161">Success</span><span class="sxs-lookup"><span data-stu-id="606f5-161">Success</span></span>
- <span data-ttu-id="606f5-162">Esito negativo</span><span class="sxs-lookup"><span data-stu-id="606f5-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="606f5-163">Collegamenti alle attività di accesso</span><span class="sxs-lookup"><span data-stu-id="606f5-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="606f5-164">Oltre ad Azure Active Directory, il portale di Azure offre due ulteriori punti di ingresso ai dati sulle attività di accesso:</span><span class="sxs-lookup"><span data-stu-id="606f5-164">In addition to Azure Active Directory, the Azure portal provides you with two additional entry points to sign-in activities data:</span></span>

- <span data-ttu-id="606f5-165">Utenti e gruppi</span><span class="sxs-lookup"><span data-stu-id="606f5-165">Users and groups</span></span>
- <span data-ttu-id="606f5-166">Applicazioni aziendali</span><span class="sxs-lookup"><span data-stu-id="606f5-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="606f5-167">Attività di accesso di utenti e gruppi</span><span class="sxs-lookup"><span data-stu-id="606f5-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="606f5-168">Le informazioni contenute nel report relativo all'accesso utente consentono di rispondere a domande come le seguenti:</span><span class="sxs-lookup"><span data-stu-id="606f5-168">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

- <span data-ttu-id="606f5-169">Qual è il modello di accesso di un utente?</span><span class="sxs-lookup"><span data-stu-id="606f5-169">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="606f5-170">Quanti utenti hanno effettuato l'accesso nell'arco di una settimana?</span><span class="sxs-lookup"><span data-stu-id="606f5-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="606f5-171">Qual è lo stato di questi accessi?</span><span class="sxs-lookup"><span data-stu-id="606f5-171">What’s the status of these sign-ins?</span></span>



<span data-ttu-id="606f5-172">Il punto di ingresso a questi dati è il grafico relativo agli accessi utente della sezione **Panoramica** in **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="606f5-172">Your entry point to this data is the user sign-in graph in the **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="606f5-173">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/45.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="606f5-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="606f5-174">Il grafico degli accessi utente visualizza le aggregazioni settimanali degli accessi per tutti gli utenti in un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="606f5-174">The user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="606f5-175">Il periodo di tempo predefinito è di 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="606f5-175">The default for the time period is 30 days.</span></span>

<span data-ttu-id="606f5-176">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/46.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="606f5-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="606f5-177">Quando si fa clic su un giorno nel grafico degli accessi, si ottiene un elenco dettagliato delle attività di accesso per tale giorno.</span><span class="sxs-lookup"><span data-stu-id="606f5-177">When you click on a day in the sign-in graph, you get a detailed list of the sign-in activities for this day.</span></span>

<span data-ttu-id="606f5-178">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/41.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="606f5-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="606f5-179">Ogni riga nell'elenco di attività di accesso offre informazioni dettagliate sull'accesso selezionato, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="606f5-179">Each row in the sign-in activities list gives you the detailed information about the selected sign-in such as:</span></span>

* <span data-ttu-id="606f5-180">Chi ha effettuato l'accesso?</span><span class="sxs-lookup"><span data-stu-id="606f5-180">Who has signed in?</span></span>
* <span data-ttu-id="606f5-181">Qual era il nome UPN correlato?</span><span class="sxs-lookup"><span data-stu-id="606f5-181">What was the related UPN?</span></span>
* <span data-ttu-id="606f5-182">Qual era l'applicazione di destinazione dell'accesso?</span><span class="sxs-lookup"><span data-stu-id="606f5-182">What application was the target of the sign-in?</span></span>
* <span data-ttu-id="606f5-183">Qual è l'indirizzo IP dell'accesso?</span><span class="sxs-lookup"><span data-stu-id="606f5-183">What is the IP address of the sign-in?</span></span>
* <span data-ttu-id="606f5-184">Qual era lo stato dell'accesso?</span><span class="sxs-lookup"><span data-stu-id="606f5-184">What was the status of the sign-in?</span></span>

<span data-ttu-id="606f5-185">L'opzione **Accessi** offre una panoramica completa di tutti gli accessi utente.</span><span class="sxs-lookup"><span data-stu-id="606f5-185">The **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="606f5-186">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/51.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="606f5-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="606f5-187">Utilizzo di applicazioni gestite</span><span class="sxs-lookup"><span data-stu-id="606f5-187">Usage of managed applications</span></span>

<span data-ttu-id="606f5-188">Con una visualizzazione dei dati di accesso basata sulle applicazioni, è possibile rispondere a domande come:</span><span class="sxs-lookup"><span data-stu-id="606f5-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="606f5-189">Chi sta usando le applicazioni?</span><span class="sxs-lookup"><span data-stu-id="606f5-189">Who is using my applications?</span></span>
* <span data-ttu-id="606f5-190">Quali sono le prime 3 applicazioni nell'organizzazione?</span><span class="sxs-lookup"><span data-stu-id="606f5-190">What are the top 3 applications in your organization?</span></span>
* <span data-ttu-id="606f5-191">Di recente è stata implementata un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="606f5-191">I have recently rolled out an application.</span></span> <span data-ttu-id="606f5-192">Come sta andando?</span><span class="sxs-lookup"><span data-stu-id="606f5-192">How is it doing?</span></span>

<span data-ttu-id="606f5-193">Il punto di ingresso a questi dati sono le prime 3 applicazioni nell'organizzazione nel report sugli ultimi 30 giorni della sezione **Panoramica** in **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="606f5-193">Your entry point to this data is the top 3 applications in your organization within the last 30 days report in the **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="606f5-194">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/64.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="606f5-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="606f5-195">Il grafico sull'utilizzo delle app visualizza le aggregazioni settimanali degli accessi per le prime 3 applicazioni in un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="606f5-195">The app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="606f5-196">Il periodo di tempo predefinito è di 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="606f5-196">The default for the time period is 30 days.</span></span>

<span data-ttu-id="606f5-197">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/47.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="606f5-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="606f5-198">Se si preferisce, è possibile mettere in evidenza un'applicazione specifica.</span><span class="sxs-lookup"><span data-stu-id="606f5-198">If you want to, you can set the focus on a specific application.</span></span>


<span data-ttu-id="606f5-199">![Report](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Report")</span><span class="sxs-lookup"><span data-stu-id="606f5-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="606f5-200">Quando si fa clic su un giorno nel grafico dell'utilizzo dell'app, si ottiene un elenco dettagliato delle attività di accesso.</span><span class="sxs-lookup"><span data-stu-id="606f5-200">When you click on a day in the app usage graph, you get a detailed list of the sign-in activities.</span></span>


<span data-ttu-id="606f5-201">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/48.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="606f5-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="606f5-202">L'opzione **Accessi** offre una panoramica completa di tutti gli eventi di accesso nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="606f5-202">The **Sign-ins** option gives you a complete overview of all sign-in events to your applications.</span></span>

<span data-ttu-id="606f5-203">![Attività di accesso](./media/active-directory-reporting-activity-sign-ins/49.png "Attività di accesso")</span><span class="sxs-lookup"><span data-stu-id="606f5-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="606f5-204">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="606f5-204">Next steps</span></span>

<span data-ttu-id="606f5-205">Per altre informazioni sui codici di errore dell'attività di accesso, vedere [Codici di errore del report delle attività di accesso nel portale di Azure Active Directory](active-directory-reporting-activity-sign-ins-errors.md).</span><span class="sxs-lookup"><span data-stu-id="606f5-205">If you want to know more about sign-in activity error codes, see the [Sign-in activity report error codes in the Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

