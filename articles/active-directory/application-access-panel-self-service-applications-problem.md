---
title: aaaProblem utilizzando l'accesso all'applicazione self-service | Documenti Microsoft
description: Risolvere i problemi correlati applicazione di servizio tooself accesso
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 2487be1df191a4e7fd0bcc0ebbe4ea62fae0fd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="d36fa-103">Errore durante l'accesso alle applicazioni self-service</span><span class="sxs-lookup"><span data-stu-id="d36fa-103">Problem using self-service application access</span></span>

<span data-ttu-id="d36fa-104">Accesso all'applicazione self-service è tooself di utenti tooallow un ottimo modo-individuare le applicazioni, se lo si desidera consentire hello business gruppo tooapprove accesso toothose applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d36fa-104">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="d36fa-105">È possibile consentire le credenziali di hello toomanage di hello business gruppo assegnati agli utenti di toothose per il diritto di Single Sign-in applicazioni Password dai loro pannelli di accesso.</span><span class="sxs-lookup"><span data-stu-id="d36fa-105">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="d36fa-106">Gli utenti self-possano individuare le applicazioni dal Pannello di accesso, è necessario tooenable **accesso all'applicazione self-service** tooany applicazioni che si desidera tooallow utenti tooself-individuare e richiedere l'accesso a.</span><span class="sxs-lookup"><span data-stu-id="d36fa-106">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="d36fa-107">Generale problemi toocheck prima</span><span class="sxs-lookup"><span data-stu-id="d36fa-107">General issues toocheck first</span></span>

-   <span data-ttu-id="d36fa-108">Assicurarsi che l'accesso alle applicazioni self-service sia configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="d36fa-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="d36fa-109">Vedere "Come applicazione self-service tooconfigure accesso".</span><span class="sxs-lookup"><span data-stu-id="d36fa-109">See “How tooconfigure self-service application access”.</span></span>

-   <span data-ttu-id="d36fa-110">Verificare che l'utente hello o un gruppo è stato abilitato l'accesso all'applicazione self-service toorequest.</span><span class="sxs-lookup"><span data-stu-id="d36fa-110">Make sure hello user or group has been enabled toorequest self-service application access.</span></span>

-   <span data-ttu-id="d36fa-111">Verificare che l'utente hello visita posizione corretta di hello per l'accesso all'applicazione self-service.</span><span class="sxs-lookup"><span data-stu-id="d36fa-111">Make sure hello user is visiting hello correct place for self-service application access.</span></span> <span data-ttu-id="d36fa-112">gli utenti possono spostarsi tootheir [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) e fare clic su hello **+ Aggiungi** pulsante toofind hello App toowhich è stato abilitato l'accesso self-service.</span><span class="sxs-lookup"><span data-stu-id="d36fa-112">users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled self-service access.</span></span>

-   <span data-ttu-id="d36fa-113">Se di recente è stato configurato l'accesso all'applicazione self-service, riprovare toosign avanti e indietro nel Pannello di accesso dell'utente hello dopo pochi minuti toosee se le modifiche di hello accesso self-service è sono rilevata.</span><span class="sxs-lookup"><span data-stu-id="d36fa-113">If self-service application access was just recently configured, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello self-service access changes have appeared.</span></span>

## <a name="how-tooconfigure-self-service-application-access"></a><span data-ttu-id="d36fa-114">Modalità di accesso dell'applicazione self-service tooconfigure</span><span class="sxs-lookup"><span data-stu-id="d36fa-114">How tooconfigure self-service application access</span></span>

<span data-ttu-id="d36fa-115">tooenable self-service accesso tooan applicazione, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="d36fa-115">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="d36fa-116">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="d36fa-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d36fa-117">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="d36fa-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d36fa-118">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="d36fa-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d36fa-119">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d36fa-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d36fa-120">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d36fa-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d36fa-121">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="d36fa-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d36fa-122">Selezionare un'applicazione hello tooenable accesso self-service toofrom hello elenco.</span><span class="sxs-lookup"><span data-stu-id="d36fa-122">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="d36fa-123">Una volta che un'applicazione hello caricato, fare clic su **self-service** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d36fa-123">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d36fa-124">tooenable accesso all'applicazione self-service per questa applicazione, attivare hello **consentire agli utenti dell'applicazione di toothis accesso toorequest?** attivare o disattivare troppo**Sì.**</span><span class="sxs-lookup"><span data-stu-id="d36fa-124">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="d36fa-125">Tooselect hello toowhich agli utenti del gruppo che richiedono accesso toothis applicazione deve essere aggiunto, fare quindi clic su Avanti toohello etichetta di hello selettore **toowhich gruppo deve assegnare gli utenti aggiunti?** e selezionare un gruppo.</span><span class="sxs-lookup"><span data-stu-id="d36fa-125">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="d36fa-126">**Facoltativo:** toorequire un'approvazione business prima che gli utenti sono autorizzati ad accedere, impostare hello **richiedono l'approvazione prima di concedere l'accesso toothis applicazione?** attivare o disattivare troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="d36fa-126">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="d36fa-127">**Facoltativo: per applicazioni tramite password single sign-on, solo** tooallow password hello toospecify responsabili approvazione business che vengono inviate toothis applicazione per gli utenti approvati, impostare hello **Consenti ai responsabili approvazione tooset password dell'utente per questa applicazione?**  attivare o disattivare troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="d36fa-127">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="d36fa-128">**Facoltativo:** toospecify hello business responsabili approvazione sono consentiti l'applicazione di toothis tooapprove accesso, fare clic sull'etichetta hello selettore successivo toohello **chi è autorizzato l'applicazione di toothis tooapprove accesso?** tooselect backup responsabili approvazione singole business too10.</span><span class="sxs-lookup"><span data-stu-id="d36fa-128">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="d36fa-129">I gruppi non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="d36fa-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="d36fa-130">**Facoltativo:** **per le applicazioni che espongono i ruoli**, se si desidera ruolo tooa di tooassign utenti approvati self-service, fare clic su Avanti toohello di hello selettore **toowhich ruolo devono essere assegnati agli utenti in questo applicazione?**  tooselect hello ruolo toowhich devono essere assegnati questi utenti.</span><span class="sxs-lookup"><span data-stu-id="d36fa-130">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="d36fa-131">Fare clic su hello **salvare** pulsante nella parte superiore di hello di hello pannello toofinish.</span><span class="sxs-lookup"><span data-stu-id="d36fa-131">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="d36fa-132">Dopo aver completato la configurazione dell'applicazione self-service, gli utenti possono spostarsi tootheir [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) e fare clic su hello **+ Aggiungi** pulsante toofind hello App toowhich è stata abilitata Accesso self-service.</span><span class="sxs-lookup"><span data-stu-id="d36fa-132">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="d36fa-133">Anche i responsabili approvazione aziendali visualizzano una notifica nel loro [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="d36fa-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="d36fa-134">È possibile attivare un messaggio di posta elettronica che comunica loro quando un utente ha richiesto l'applicazione di accesso tooan che richiede l'approvazione.</span><span class="sxs-lookup"><span data-stu-id="d36fa-134">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="d36fa-135">Queste approvazioni supportano solo flussi di lavoro, vale a dire che se si specificano più responsabili approvazione, qualsiasi Approvatore singolo può approvare applicazione toohello accesso.</span><span class="sxs-lookup"><span data-stu-id="d36fa-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="d36fa-136">Se i passaggi di risoluzione dei problemi non risolvono il problema di hello</span><span class="sxs-lookup"><span data-stu-id="d36fa-136">If these troubleshooting steps do not resolve hello issue</span></span> 

<span data-ttu-id="d36fa-137">Aprire un ticket di supporto con hello se disponibili le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="d36fa-137">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="d36fa-138">ID errore di correlazione</span><span class="sxs-lookup"><span data-stu-id="d36fa-138">Correlation error ID</span></span>

-   <span data-ttu-id="d36fa-139">UPN (indirizzo di posta elettronica dell'utente)</span><span class="sxs-lookup"><span data-stu-id="d36fa-139">UPN (user email address)</span></span>

-   <span data-ttu-id="d36fa-140">ID tenant</span><span class="sxs-lookup"><span data-stu-id="d36fa-140">TenantID</span></span>

-   <span data-ttu-id="d36fa-141">Tipo di browser</span><span class="sxs-lookup"><span data-stu-id="d36fa-141">Browser type</span></span>

-   <span data-ttu-id="d36fa-142">Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore</span><span class="sxs-lookup"><span data-stu-id="d36fa-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="d36fa-143">Tracce Fiddler</span><span class="sxs-lookup"><span data-stu-id="d36fa-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="d36fa-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d36fa-144">Next steps</span></span>
[<span data-ttu-id="d36fa-145">Configurazione di Azure Active Directory per la gestione self-service dei gruppi</span><span class="sxs-lookup"><span data-stu-id="d36fa-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
