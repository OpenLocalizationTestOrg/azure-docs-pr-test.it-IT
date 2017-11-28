---
title: applicazione tooan utenti e gruppi aaaHow tooassign | Documenti Microsoft
description: Assegnare gli utenti l'accesso toogrant toohello applicazione
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
ms.openlocfilehash: e039a26e4b8f88ad747354859f1071b8f74b6789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-and-groups-tooan-application"></a><span data-ttu-id="8ccca-103">Come applicazione di tooan tooassign utenti e gruppi</span><span class="sxs-lookup"><span data-stu-id="8ccca-103">How tooassign users and groups tooan application</span></span>

<span data-ttu-id="8ccca-104">Prima che gli utenti possono eseguire hello sotto per un'applicazione specifica, è necessario toofirst **assegnarli applicazione toohello** toogrant loro l'accesso:</span><span class="sxs-lookup"><span data-stu-id="8ccca-104">Before your users can do any of hello below for a specific application, you need toofirst **assign them toohello application** toogrant them access:</span></span>

-   <span data-ttu-id="8ccca-105">Accedere a un'applicazione da **passando direttamente l'URL dell'applicazione toohello** (noto anche come SP initiated sign-on).</span><span class="sxs-lookup"><span data-stu-id="8ccca-105">Access an application by **navigating toohello application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="8ccca-106">Accedere a un'applicazione utilizzando hello **URL di accesso utente** in un'applicazione **proprietà** pagina (noto anche come avviata da IDP sign-on).</span><span class="sxs-lookup"><span data-stu-id="8ccca-106">Access an application by using hello **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="8ccca-107">Visualizzare un'applicazione nel [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) o l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8ccca-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="8ccca-108">Visualizzare un'applicazione nell'[icona di avvio delle app di Office 365](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span><span class="sxs-lookup"><span data-stu-id="8ccca-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-tooassign-applications-with-azure-active-directory"></a><span data-ttu-id="8ccca-109">Applicazioni tooassign metodi con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ccca-109">Methods tooassign applications with Azure Active Directory</span></span> 

<span data-ttu-id="8ccca-110">Esistono 3 modi per poter assegnare applicazioni con Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="8ccca-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="8ccca-111">Assegnare un utente direttamente tooan applicazione come amministratore</span><span class="sxs-lookup"><span data-stu-id="8ccca-111">Assign a user directly tooan application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="8ccca-112">Assegnare un gruppo direttamente tooan applicazione come amministratore</span><span class="sxs-lookup"><span data-stu-id="8ccca-112">Assign a group directly tooan application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="8ccca-113">Abilita applicazione self-service accesso tooallow utenti toofind delle proprie applicazioni</span><span class="sxs-lookup"><span data-stu-id="8ccca-113">Enable self-service application access tooallow users toofind their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="8ccca-114">Assegnare un utente direttamente come amministratore</span><span class="sxs-lookup"><span data-stu-id="8ccca-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="8ccca-115">tooassign uno o più applicazioni tooan utenti direttamente, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="8ccca-115">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="8ccca-116">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="8ccca-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="8ccca-117">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="8ccca-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8ccca-118">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="8ccca-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8ccca-119">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ccca-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8ccca-120">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8ccca-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="8ccca-121">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="8ccca-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="8ccca-122">Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="8ccca-122">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="8ccca-123">Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8ccca-123">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="8ccca-124">Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="8ccca-124">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="8ccca-125">Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="8ccca-125">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="8ccca-126">Tipo di hello **nome completo** o **indirizzo di posta elettronica** dell'utente hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="8ccca-126">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="8ccca-127">Passare il mouse su hello **utente** in hello elenco tooreveal un **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="8ccca-127">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="8ccca-128">Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello dell'utente il toohello utente **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="8ccca-128">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="8ccca-129">**Facoltativo:** se si desidera troppo**aggiungere più di un utente**, in un altro tipo di **nome completo** o **indirizzo di posta elettronica** in hello **Cerca per nome o l'indirizzo di posta elettronica** casella di ricerca e fare clic su questo toohello utente hello casella di controllo tooadd **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="8ccca-129">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="8ccca-130">Al termine della selezione utenti, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="8ccca-130">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="8ccca-131">**Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un ruolo tooassign toohello utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="8ccca-131">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="8ccca-132">Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="8ccca-132">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="8ccca-133">Dopo un breve periodo di tempo, gli utenti di hello selezionato in toolaunch in grado di queste applicazioni utilizzano hello metodi descritti nella sezione Descrizione della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="8ccca-133">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a><span data-ttu-id="8ccca-134">Assegnare un gruppo direttamente tooan applicazione come amministratore</span><span class="sxs-lookup"><span data-stu-id="8ccca-134">Assign a group directly tooan application as an administrator</span></span>

<span data-ttu-id="8ccca-135">tooassign uno o più gruppi di applicazioni tooan direttamente, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="8ccca-135">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="8ccca-136">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="8ccca-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="8ccca-137">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="8ccca-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8ccca-138">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="8ccca-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8ccca-139">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ccca-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8ccca-140">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8ccca-140">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="8ccca-141">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="8ccca-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="8ccca-142">Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="8ccca-142">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="8ccca-143">Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8ccca-143">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="8ccca-144">Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="8ccca-144">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="8ccca-145">Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="8ccca-145">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="8ccca-146">Tipo di hello **nome del gruppo completo** del gruppo di hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="8ccca-146">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="8ccca-147">Passare il mouse su hello **gruppo** in hello elenco tooreveal un **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="8ccca-147">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="8ccca-148">Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello del gruppo toohello l'utente **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="8ccca-148">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="8ccca-149">**Facoltativo:** se si desidera troppo**aggiungere più di un gruppo**, in un altro tipo di **nome del gruppo completo** in hello **ricerca per nome o indirizzo di posta** casella di ricerca Fare clic su hello casella di controllo tooadd toohello questo gruppo **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="8ccca-149">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="8ccca-150">Al termine della selezione gruppi, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="8ccca-150">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="8ccca-151">**Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un toohello tooassign ruolo gruppi di sicurezza selezionato.</span><span class="sxs-lookup"><span data-stu-id="8ccca-151">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="8ccca-152">Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gruppi selezionati.</span><span class="sxs-lookup"><span data-stu-id="8ccca-152">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="8ccca-153">Dopo un breve periodo di tempo, gli utenti di hello all'interno di gruppi di hello selezionati in toolaunch in grado di queste applicazioni utilizzano hello metodi descritti nella sezione Descrizione della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="8ccca-153">After a short period of time, hello users within hello groups you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span> <span data-ttu-id="8ccca-154">Se i gruppi sono dinamici, potrebbe verificarsi un ritardo di elaborazione aggiuntivo nella visualizzazione di queste assegnazioni per gli utenti dei gruppi assegnati.</span><span class="sxs-lookup"><span data-stu-id="8ccca-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="8ccca-155">Abilita applicazione self-service accesso tooallow utenti toofind delle proprie applicazioni</span><span class="sxs-lookup"><span data-stu-id="8ccca-155">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="8ccca-156">Accesso all'applicazione self-service è tooself di utenti tooallow un ottimo modo-individuare le applicazioni, se lo si desidera consentire hello business gruppo tooapprove accesso toothose applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8ccca-156">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="8ccca-157">È possibile consentire le credenziali di hello toomanage di hello business gruppo assegnati agli utenti di toothose per il diritto di Single Sign-in applicazioni Password dai loro pannelli di accesso.</span><span class="sxs-lookup"><span data-stu-id="8ccca-157">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="8ccca-158">tooenable self-service accesso tooan applicazione, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="8ccca-158">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="8ccca-159">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="8ccca-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="8ccca-160">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="8ccca-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8ccca-161">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="8ccca-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8ccca-162">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ccca-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8ccca-163">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8ccca-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="8ccca-164">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="8ccca-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="8ccca-165">Selezionare un'applicazione hello tooenable accesso self-service toofrom hello elenco.</span><span class="sxs-lookup"><span data-stu-id="8ccca-165">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="8ccca-166">Una volta che un'applicazione hello caricato, fare clic su **self-service** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8ccca-166">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="8ccca-167">tooenable accesso all'applicazione self-service per questa applicazione, attivare hello **consentire agli utenti dell'applicazione di toothis accesso toorequest?** attivare o disattivare troppo**Sì.**</span><span class="sxs-lookup"><span data-stu-id="8ccca-167">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="8ccca-168">Tooselect hello toowhich agli utenti del gruppo che richiedono accesso toothis applicazione deve essere aggiunto, fare quindi clic su Avanti toohello etichetta di hello selettore **toowhich gruppo deve assegnare gli utenti aggiunti?** e selezionare un gruppo.</span><span class="sxs-lookup"><span data-stu-id="8ccca-168">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="8ccca-169">**Facoltativo:** toorequire un'approvazione business prima che gli utenti sono autorizzati ad accedere, impostare hello **richiedono l'approvazione prima di concedere l'accesso toothis applicazione?** attivare o disattivare troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="8ccca-169">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="8ccca-170">**Facoltativo: per applicazioni tramite password single sign-on, solo** tooallow password hello toospecify responsabili approvazione business che vengono inviate toothis applicazione per gli utenti approvati, impostare hello **Consenti ai responsabili approvazione tooset password dell'utente per questa applicazione?**  attivare o disattivare troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="8ccca-170">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="8ccca-171">**Facoltativo:** toospecify hello business responsabili approvazione sono consentiti l'applicazione di toothis tooapprove accesso, fare clic sull'etichetta hello selettore successivo toohello **chi è autorizzato l'applicazione di toothis tooapprove accesso?** tooselect backup responsabili approvazione singole business too10.</span><span class="sxs-lookup"><span data-stu-id="8ccca-171">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="8ccca-172">I gruppi non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="8ccca-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="8ccca-173">**Facoltativo:** **per le applicazioni che espongono i ruoli**, se si desidera ruolo tooa di tooassign utenti approvati self-service, fare clic su Avanti toohello di hello selettore **toowhich ruolo devono essere assegnati agli utenti in questo applicazione?**  tooselect hello ruolo toowhich devono essere assegnati questi utenti.</span><span class="sxs-lookup"><span data-stu-id="8ccca-173">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="8ccca-174">Fare clic su hello **salvare** pulsante nella parte superiore di hello di hello pannello toofinish.</span><span class="sxs-lookup"><span data-stu-id="8ccca-174">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="8ccca-175">Dopo aver completato la configurazione dell'applicazione self-service, gli utenti possono spostarsi tootheir [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) e fare clic su hello **+ Aggiungi** pulsante toofind hello App toowhich è stata abilitata Accesso self-service.</span><span class="sxs-lookup"><span data-stu-id="8ccca-175">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="8ccca-176">Anche i responsabili approvazione aziendali visualizzano una notifica nel loro [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="8ccca-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="8ccca-177">È possibile attivare un messaggio di posta elettronica che comunica loro quando un utente ha richiesto l'applicazione di accesso tooan che richiede l'approvazione.</span><span class="sxs-lookup"><span data-stu-id="8ccca-177">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="8ccca-178">Queste approvazioni supportano solo flussi di lavoro, vale a dire che se si specificano più responsabili approvazione, qualsiasi Approvatore singolo può applicazione toohello di responsabile approvazione accesso.</span><span class="sxs-lookup"><span data-stu-id="8ccca-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ccca-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8ccca-179">Next steps</span></span>
[<span data-ttu-id="8ccca-180">Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="8ccca-180">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
