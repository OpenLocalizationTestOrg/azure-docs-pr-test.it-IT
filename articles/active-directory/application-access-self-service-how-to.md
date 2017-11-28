---
title: assegnazione di aaaHow tooconfigure applicazione self-service | Documenti Microsoft
description: Abilita applicazione self-service accesso tooallow utenti toofind delle proprie applicazioni
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
ms.openlocfilehash: d25a0146c4c8cebf9c2ae8c516f094a8eccb4570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-self-service-application-assignment"></a><span data-ttu-id="ba0d3-103">Come l'assegnazione tooconfigure applicazione self-service</span><span class="sxs-lookup"><span data-stu-id="ba0d3-103">How tooconfigure self-service application assignment</span></span>

<span data-ttu-id="ba0d3-104">Gli utenti self-possano individuare le applicazioni dal Pannello di accesso, è necessario tooenable **accesso all'applicazione self-service** tooany applicazioni che si desidera tooallow utenti tooself-individuare e richiedere l'accesso a.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-104">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

<span data-ttu-id="ba0d3-105">Questa funzionalità è un ottimo modo per si toosave tempo e denaro come un gruppo IT ed è consigliata come parte di una distribuzione di applicazioni moderne con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-105">This feature is a great way for you toosave time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="ba0d3-106">Questa funzionalità permette di:</span><span class="sxs-lookup"><span data-stu-id="ba0d3-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="ba0d3-107">Consentire agli utenti self-individuare le applicazioni da hello [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) senza richiedere l'intervento dell'IT hello gruppo.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-107">Let users self-discover applications from hello [Application Access Panel](https://myapps.microsoft.com/) without bothering hello IT group.</span></span>

-   <span data-ttu-id="ba0d3-108">Aggiungere tali gruppo di utenti tooa preconfigurato pertanto è possibile vedere chi ha richiesto l'accesso, rimuovere l'accesso e gestire i ruoli di hello assegnati toothem.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-108">Add those users tooa pre-configured group so you can see who has requested access, remove access, and manage hello roles assigned toothem.</span></span>

-   <span data-ttu-id="ba0d3-109">Facoltativamente consente un responsabile approvazione business tooapprove le richieste di accesso dell'applicazione in modo che non debba hello gruppo IT.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-109">Optionally allow a business approver tooapprove application access requests so hello IT group doesn’t have to.</span></span>

-   <span data-ttu-id="ba0d3-110">Configurare facoltativamente too10 chiunque possono approvare l'applicazione toothis di accesso.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-110">Optionally configure up too10 individuals who may approve access toothis application.</span></span>

-   <span data-ttu-id="ba0d3-111">Consente, facoltativamente, un responsabile approvazione business password hello tooset tali utenti possono utilizzare toosign nell'applicazione toohello, direttamente da del revisore business hello [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="ba0d3-111">Optionally allow a business approver tooset hello passwords those users can use toosign in toohello application, right from hello business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="ba0d3-112">Assegnare facoltativamente automaticamente ruolo applicazione di self-service agli utenti assegnati tooan direttamente.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-112">Optionally automatically assign self-service assigned users tooan application role directly.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="ba0d3-113">Abilita applicazione self-service accesso tooallow utenti toofind delle proprie applicazioni</span><span class="sxs-lookup"><span data-stu-id="ba0d3-113">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="ba0d3-114">Accesso all'applicazione self-service è tooself di utenti tooallow un ottimo modo-individuare le applicazioni, se lo si desidera consentire hello business gruppo tooapprove accesso toothose applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-114">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="ba0d3-115">È possibile consentire le credenziali di hello toomanage di hello business gruppo assegnati agli utenti di toothose per il diritto di Single Sign-in applicazioni Password dai loro pannelli di accesso.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-115">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="ba0d3-116">tooenable self-service accesso tooan applicazione, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="ba0d3-116">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="ba0d3-117">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="ba0d3-117">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="ba0d3-118">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-118">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ba0d3-119">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-119">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ba0d3-120">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-120">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ba0d3-121">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-121">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="ba0d3-122">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="ba0d3-122">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ba0d3-123">Selezionare un'applicazione hello tooenable accesso self-service toofrom hello elenco.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-123">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="ba0d3-124">Una volta che un'applicazione hello caricato, fare clic su **self-service** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-124">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ba0d3-125">tooenable accesso all'applicazione self-service per questa applicazione, attivare hello **consentire agli utenti dell'applicazione di toothis accesso toorequest?** attivare o disattivare troppo**Sì.**</span><span class="sxs-lookup"><span data-stu-id="ba0d3-125">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="ba0d3-126">Tooselect hello toowhich agli utenti del gruppo che richiedono accesso toothis applicazione deve essere aggiunto, fare quindi clic su Avanti toohello etichetta di hello selettore **toowhich gruppo deve assegnare gli utenti aggiunti?** e selezionare un gruppo.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-126">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="ba0d3-127">**Facoltativo:** toorequire un'approvazione business prima che gli utenti sono autorizzati ad accedere, impostare hello **richiedono l'approvazione prima di concedere l'accesso toothis applicazione?** attivare o disattivare troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-127">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="ba0d3-128">**Facoltativo: per applicazioni tramite password single sign-on, solo** tooallow password hello toospecify responsabili approvazione business che vengono inviate toothis applicazione per gli utenti approvati, impostare hello **Consenti ai responsabili approvazione tooset password dell'utente per questa applicazione?**  attivare o disattivare troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-128">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="ba0d3-129">**Facoltativo:** toospecify hello business responsabili approvazione sono consentiti l'applicazione di toothis tooapprove accesso, fare clic sull'etichetta hello selettore successivo toohello **chi è autorizzato l'applicazione di toothis tooapprove accesso?** tooselect backup responsabili approvazione singole business too10.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-129">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

   >[!NOTE]
   ><span data-ttu-id="ba0d3-130">I gruppi non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-130">Groups are not supported.</span></span>
   >
   >

13. <span data-ttu-id="ba0d3-131">**Facoltativo:** **per le applicazioni che espongono i ruoli**, se si desidera ruolo tooa di tooassign utenti approvati self-service, fare clic su Avanti toohello di hello selettore **toowhich ruolo devono essere assegnati agli utenti in questo applicazione?**  tooselect hello ruolo toowhich devono essere assegnati questi utenti.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-131">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="ba0d3-132">Fare clic su hello **salvare** pulsante nella parte superiore di hello di hello pannello toofinish.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-132">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="ba0d3-133">Dopo aver completato la configurazione dell'applicazione self-service, gli utenti possono spostarsi tootheir [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) e fare clic su hello **+ Aggiungi** pulsante toofind hello App toowhich è stata abilitata Accesso self-service.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-133">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="ba0d3-134">Anche i responsabili approvazione aziendali visualizzano una notifica nel loro [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="ba0d3-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="ba0d3-135">È possibile attivare un messaggio di posta elettronica che comunica loro quando un utente ha richiesto l'applicazione di accesso tooan che richiede l'approvazione.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-135">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="ba0d3-136">Queste approvazioni supportano solo flussi di lavoro, vale a dire che se si specificano più responsabili approvazione, qualsiasi Approvatore singolo può applicazione toohello di responsabile approvazione accesso.</span><span class="sxs-lookup"><span data-stu-id="ba0d3-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba0d3-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ba0d3-137">Next steps</span></span>
[<span data-ttu-id="ba0d3-138">Configurazione di Azure Active Directory per la gestione self-service dei gruppi</span><span class="sxs-lookup"><span data-stu-id="ba0d3-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
