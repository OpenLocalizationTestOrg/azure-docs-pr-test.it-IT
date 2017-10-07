---
title: aaaProblems applicazione raccolta tooa configurata per federati l'accesso single sign-on | Documenti Microsoft
description: "Linee guida per errori specifici di hello quando si accede a un'applicazione che è stata configurata per basato su SAML single sign-on federato con Azure AD"
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
ms.openlocfilehash: ba20a4904860cf063967029cad33fb80f16e4956
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="e5293-103">Problemi durante l'accesso dell'applicazione raccolta tooa configurata per single sign-on federato</span><span class="sxs-lookup"><span data-stu-id="e5293-103">Problems signing in tooa gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="e5293-104">tootroubleshoot il problema, è necessario tooverify configurazione dell'applicazione hello in Azure AD come segue:</span><span class="sxs-lookup"><span data-stu-id="e5293-104">tootroubleshoot your problem, you need tooverify hello application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="e5293-105">Aver seguito tutti i passaggi di configurazione di hello per hello applicazione raccolta di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5293-105">You have followed all hello configuration steps for hello Azure AD gallery application.</span></span>

-   <span data-ttu-id="e5293-106">Identificatore Hello e configurata in AAD l'URL di risposta corrispondono sono i valori previsti in un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="e5293-106">hello Identifier and Reply URL configured in AAD match they expected values in hello application</span></span>

-   <span data-ttu-id="e5293-107">È stato assegnato agli utenti dell'applicazione toohello</span><span class="sxs-lookup"><span data-stu-id="e5293-107">You have assigned users toohello application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="e5293-108">Applicazione non trovata nella directory</span><span class="sxs-lookup"><span data-stu-id="e5293-108">Application not found in directory</span></span>

<span data-ttu-id="e5293-109">*Errore AADSTS70001: Impossibile trovare l'applicazione con identificatore 'https://contoso.com' nella directory hello*.</span><span class="sxs-lookup"><span data-stu-id="e5293-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in hello directory*.</span></span>

<span data-ttu-id="e5293-110">**Causa possibile**</span><span class="sxs-lookup"><span data-stu-id="e5293-110">**Possible cause**</span></span>

<span data-ttu-id="e5293-111">attributo dell'autorità di certificazione Hello invia da tooAzure applicazione hello che ad nella richiesta SAML hello non corrisponde al valore di identificatore hello configurato nell'applicazione hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5293-111">hello Issuer attribute sends from hello application tooAzure AD in hello SAML request doesn’t match hello Identifier value configured in hello application Azure AD.</span></span>

<span data-ttu-id="e5293-112">**Risoluzione**</span><span class="sxs-lookup"><span data-stu-id="e5293-112">**Resolution**</span></span>

<span data-ttu-id="e5293-113">Verificare che tale attributo dell'autorità di certificazione hello nella richiesta SAML hello che corrispondenza hello valore identificatore configurato in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="e5293-113">Ensure that hello Issuer attribute in hello SAML request it’s matching hello Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="e5293-114">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="e5293-114">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e5293-115">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-115">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e5293-116">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e5293-116">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e5293-117">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e5293-117">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e5293-118">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e5293-118">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e5293-119">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="e5293-119">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e5293-120">Selezionare l'applicazione hello da tooconfigure single sign-on</span><span class="sxs-lookup"><span data-stu-id="e5293-120">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="e5293-121">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-121">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e5293-122">Andare troppo**dominio e gli URL** sezione.</span><span class="sxs-lookup"><span data-stu-id="e5293-122">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="e5293-123">Verificare che il valore hello nella casella di testo corrispondenti valore hello per il valore di identificatore hello visualizzato per errore hello identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-123">Verify that hello value in hello Identifier textbox is matching hello value for hello identifier value displayed in hello error.</span></span>

<span data-ttu-id="e5293-124">Dopo che è stato aggiornato il valore di identificatore hello in Azure AD e il valore corrispondente a hello invia da un'applicazione hello nella richiesta SAML hello, si dovrebbe essere in grado di toosign toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="e5293-124">After you have updated hello Identifier value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a><span data-ttu-id="e5293-125">indirizzo di risposta Hello corrispondono agli indirizzi di risposta hello configurati per l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-125">hello reply address does not match hello reply addresses configured for hello application.</span></span>

<span data-ttu-id="e5293-126">*Errore AADSTS50011: l'indirizzo di risposta hello 'https://contoso.com' non corrispondono agli indirizzi di risposta hello configurati per l'applicazione hello*</span><span class="sxs-lookup"><span data-stu-id="e5293-126">*Error AADSTS50011: hello reply address ‘https://contoso.com’ does not match hello reply addresses configured for hello application*</span></span>

<span data-ttu-id="e5293-127">**Causa possibile**</span><span class="sxs-lookup"><span data-stu-id="e5293-127">**Possible cause**</span></span>

<span data-ttu-id="e5293-128">Hello AssertionConsumerServiceURL valore nella richiesta SAML hello non corrisponde al valore di URL di risposta hello o un modello configurato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5293-128">hello AssertionConsumerServiceURL value in hello SAML request doesn't match hello Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="e5293-129">valore AssertionConsumerServiceURL nella richiesta SAML hello Hello è hello URL viene visualizzato l'errore hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-129">hello AssertionConsumerServiceURL value in hello SAML request is hello URL you see in hello error.</span></span>

<span data-ttu-id="e5293-130">**Risoluzione**</span><span class="sxs-lookup"><span data-stu-id="e5293-130">**Resolution**</span></span>

<span data-ttu-id="e5293-131">Verificare che tale valore AssertionConsumerServiceURL hello nella richiesta SAML hello di corrispondenza hello valore URL di risposta è configurata in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5293-131">Ensure that hello AssertionConsumerServiceURL value in hello SAML request it's matching hello Reply URL value configured in Azure AD.</span></span>

1.  <span data-ttu-id="e5293-132">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="e5293-132">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e5293-133">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-133">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e5293-134">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e5293-134">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e5293-135">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e5293-135">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e5293-136">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e5293-136">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e5293-137">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="e5293-137">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e5293-138">Selezionare l'applicazione hello da tooconfigure single sign-on</span><span class="sxs-lookup"><span data-stu-id="e5293-138">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="e5293-139">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-139">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e5293-140">Andare troppo**dominio e gli URL** sezione.</span><span class="sxs-lookup"><span data-stu-id="e5293-140">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="e5293-141">Verificare o aggiornare il valore di hello nella casella di testo toomatch hello AssertionConsumerServiceURL valore nella richiesta SAML hello di hello URL di risposta.</span><span class="sxs-lookup"><span data-stu-id="e5293-141">Verify or update hello value in hello Reply URL textbox toomatch hello AssertionConsumerServiceURL value in hello SAML request.</span></span>  
    * <span data-ttu-id="e5293-142">Se non viene visualizzato hello URL di risposta casella di testo, selezionare hello **Mostra URL impostazioni avanzate** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="e5293-142">If you don't see hello Reply URL textbox, select hello **Show advanced URL settings** checkbox.</span></span>

<span data-ttu-id="e5293-143">Dopo che è stato aggiornato il valore di URL di risposta hello in Azure AD e ha corrispondente valore hello viene inviato per un'applicazione hello in hello richiesta SAML, dovrebbe essere in grado di toosign toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="e5293-143">After you have updated hello Reply URL value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="e5293-144">All'utente non è stato assegnato un ruolo</span><span class="sxs-lookup"><span data-stu-id="e5293-144">User not assigned a role</span></span>

<span data-ttu-id="e5293-145">*Errore AADSTS50105: hello effettuato l'accesso utente 'brian@contoso.com' non è assegnato il ruolo di tooa per un'applicazione hello*.</span><span class="sxs-lookup"><span data-stu-id="e5293-145">*Error AADSTS50105: hello signed in user 'brian@contoso.com' is not assigned tooa role for hello application*.</span></span>

<span data-ttu-id="e5293-146">**Causa possibile**</span><span class="sxs-lookup"><span data-stu-id="e5293-146">**Possible cause**</span></span>

<span data-ttu-id="e5293-147">Hello utente non ha ottenuto accesso toohello applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5293-147">hello user has not been granted access toohello application in Azure AD.</span></span>

<span data-ttu-id="e5293-148">**Risoluzione**</span><span class="sxs-lookup"><span data-stu-id="e5293-148">**Resolution**</span></span>

<span data-ttu-id="e5293-149">tooassign uno o più applicazioni tooan utenti direttamente, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="e5293-149">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="e5293-150">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="e5293-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e5293-151">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e5293-152">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e5293-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e5293-153">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e5293-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e5293-154">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e5293-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e5293-155">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="e5293-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e5293-156">Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="e5293-156">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="e5293-157">Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-157">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e5293-158">Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="e5293-158">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="e5293-159">Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="e5293-159">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="e5293-160">Tipo di hello **nome completo** o **indirizzo di posta elettronica** dell'utente hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="e5293-160">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="e5293-161">Passare il mouse su hello **utente** in hello elenco tooreveal un **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="e5293-161">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="e5293-162">Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello dell'utente il toohello utente **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="e5293-162">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="e5293-163">**Facoltativo:** se si desidera troppo**aggiungere più di un utente**, in un altro tipo di **nome completo** o **indirizzo di posta elettronica** in hello **Cerca per nome o l'indirizzo di posta elettronica** casella di ricerca e fare clic su questo toohello utente hello casella di controllo tooadd **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="e5293-163">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="e5293-164">Al termine della selezione utenti, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="e5293-164">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="e5293-165">**Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un ruolo tooassign toohello utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="e5293-165">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="e5293-166">Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="e5293-166">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="e5293-167">Dopo un breve periodo di tempo, gli utenti di hello selezionato in toolaunch in grado di queste applicazioni utilizzano hello metodi descritti nella sezione Descrizione della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-167">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="e5293-168">La richiesta non è un messaggio SAML valido</span><span class="sxs-lookup"><span data-stu-id="e5293-168">Not a valid SAML Request</span></span>

<span data-ttu-id="e5293-169">*Errore AADSTS75005: hello richiesta non è un messaggio di protocollo Saml2 valido.*</span><span class="sxs-lookup"><span data-stu-id="e5293-169">*Error AADSTS75005: hello request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="e5293-170">**Causa possibile**</span><span class="sxs-lookup"><span data-stu-id="e5293-170">**Possible cause**</span></span>

<span data-ttu-id="e5293-171">Azure Active Directory non supporta hello SAML richiesta inviata da un'applicazione hello per Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="e5293-171">Azure AD doesn’t support hello SAML Request sent by hello application for Single Sign-on.</span></span> <span data-ttu-id="e5293-172">Alcuni problemi comuni sono:</span><span class="sxs-lookup"><span data-stu-id="e5293-172">Some common issues are:</span></span>

-   <span data-ttu-id="e5293-173">I campi obbligatori nella richiesta SAML hello mancante</span><span class="sxs-lookup"><span data-stu-id="e5293-173">Missing required fields in hello SAML request</span></span>

-   <span data-ttu-id="e5293-174">Metodo codificato della richiesta SAML</span><span class="sxs-lookup"><span data-stu-id="e5293-174">SAML request encoded method</span></span>

<span data-ttu-id="e5293-175">**Risoluzione**</span><span class="sxs-lookup"><span data-stu-id="e5293-175">**Resolution**</span></span>

1.  <span data-ttu-id="e5293-176">Acquisire la richiesta SAML.</span><span class="sxs-lookup"><span data-stu-id="e5293-176">Capture SAML request.</span></span> <span data-ttu-id="e5293-177">seguire l'esercitazione hello [come toodebug basato su SAML single sign-on tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn come toocapture hello SAML richiesta.</span><span class="sxs-lookup"><span data-stu-id="e5293-177">follow hello tutorial [How toodebug SAML-based single sign-on tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn how toocapture hello SAML request.</span></span>

2.  <span data-ttu-id="e5293-178">Contattare il fornitore dell'applicazione hello e condivisione:</span><span class="sxs-lookup"><span data-stu-id="e5293-178">Contact hello application vendor and share:</span></span>

   -   <span data-ttu-id="e5293-179">Richiesta SAML</span><span class="sxs-lookup"><span data-stu-id="e5293-179">SAML request</span></span>

   -   [<span data-ttu-id="e5293-180">Requisiti del protocollo SAML per Single Sign-On di Azure</span><span class="sxs-lookup"><span data-stu-id="e5293-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="e5293-181">È necessario convalidare supportano l'implementazione di Azure AD SAML hello per Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="e5293-181">They should validate they support hello Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="e5293-182">Nessuna risorsa nell'elenco requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="e5293-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="e5293-183">*Errore AADSTS65005:hello client applicazione ha richiesto l'accesso tooresource ' 00000002-0000-0000-c000-000000000000'. Questa richiesta non riuscito perché il client hello questa risorsa non è specificato nel relativo elenco requiredResourceAccess*.</span><span class="sxs-lookup"><span data-stu-id="e5293-183">*Error AADSTS65005:hello client application has requested access tooresource '00000002-0000-0000-c000-000000000000'. This request has failed because hello client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="e5293-184">**Causa possibile**</span><span class="sxs-lookup"><span data-stu-id="e5293-184">**Possible cause**</span></span>

<span data-ttu-id="e5293-185">oggetto applicazione Hello è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="e5293-185">hello application object is corrupted.</span></span>

<span data-ttu-id="e5293-186">**Risoluzione: opzione 1**</span><span class="sxs-lookup"><span data-stu-id="e5293-186">**Resolution: option 1**</span></span>

<span data-ttu-id="e5293-187">problema di hello toosolve, aggiungere il valore dell'identificatore univoco di hello nella configurazione di hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5293-187">toosolve hello problem, add hello unique Identifier value in hello Azure AD configuration.</span></span> <span data-ttu-id="e5293-188">un valore dell'identificatore, tooadd procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="e5293-188">tooadd a Identifier value, follow hello steps below:</span></span>

1.  <span data-ttu-id="e5293-189">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="e5293-189">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e5293-190">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-190">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e5293-191">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e5293-191">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e5293-192">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e5293-192">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e5293-193">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e5293-193">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e5293-194">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="e5293-194">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e5293-195">Selezionare un'applicazione hello è stato configurato single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e5293-195">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="e5293-196">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="e5293-196">Once hello application loads, click on hello **Single sign-on** from hello application’s left hand navigation menu</span></span>

8.  <span data-ttu-id="e5293-197">In hello **dominio e l'URL** sezione, verificare hello **Mostra URL impostazioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="e5293-197">Under hello **Domain and URL** section, check on hello **Show advanced URL settings**.</span></span>

9.  <span data-ttu-id="e5293-198">in hello **identificatore** casella di testo digitare un identificatore univoco per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-198">in hello **Identifier** textbox type a unique identifier for hello application.</span></span>

10. <span data-ttu-id="e5293-199">**Salvare** configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-199">**Save** hello configuration.</span></span>


<span data-ttu-id="e5293-200">**Risoluzione: opzione 2**</span><span class="sxs-lookup"><span data-stu-id="e5293-200">**Resolution option 2**</span></span>

<span data-ttu-id="e5293-201">Se l'opzione 1 sopra non non risolvere il problema, provare a rimuovere l'applicazione hello dalla directory hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-201">If option 1 above did not work for you, try removing hello application from hello directory.</span></span> <span data-ttu-id="e5293-202">Quindi, aggiungere e riconfigurare un'applicazione hello, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="e5293-202">Then, add and reconfigure hello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="e5293-203">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="e5293-203">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e5293-204">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-204">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e5293-205">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e5293-205">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e5293-206">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e5293-206">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e5293-207">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e5293-207">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e5293-208">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="e5293-208">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e5293-209">Selezionare l'applicazione hello da tooconfigure single sign-on</span><span class="sxs-lookup"><span data-stu-id="e5293-209">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="e5293-210">Fare clic su **eliminare** in hello alto a sinistra di un'applicazione hello **Panoramica** blade.</span><span class="sxs-lookup"><span data-stu-id="e5293-210">Click **Delete** at hello top-left of hello application **Overview** blade.</span></span>

8.  <span data-ttu-id="e5293-211">Aggiornare Azure AD e aggiungere un'applicazione hello hello raccolta di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5293-211">Refresh Azure AD and Add hello application from hello Azure AD gallery.</span></span> <span data-ttu-id="e5293-212">Quindi, configurare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="e5293-212">Then, Configure hello application</span></span>

<span data-ttu-id="e5293-213"><span id="_Hlk477190176" class="anchor"></span>Dopo la riconfigurazione di un'applicazione hello, si dovrebbe essere in grado di toosign toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="e5293-213"><span id="_Hlk477190176" class="anchor"></span>After reconfiguring hello application, you should be able toosign in toohello application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="e5293-214">Chiave o certificato non configurato</span><span class="sxs-lookup"><span data-stu-id="e5293-214">Certificate or key not configured</span></span>

<span data-ttu-id="e5293-215">*Error AADSTS50003: No signing key configured.* (Errore AADSTS50003: nessuna chiave di firma configurata).</span><span class="sxs-lookup"><span data-stu-id="e5293-215">*Error AADSTS50003: No signing key configured.*</span></span>

<span data-ttu-id="e5293-216">**Causa possibile**</span><span class="sxs-lookup"><span data-stu-id="e5293-216">**Possible cause**</span></span>

<span data-ttu-id="e5293-217">oggetto applicazione Hello è danneggiato e Azure AD non riconosce il certificato di hello configurato per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-217">hello application object is corrupted and Azure AD doesn’t recognize hello certificate configured for hello application.</span></span>

<span data-ttu-id="e5293-218">**Risoluzione**</span><span class="sxs-lookup"><span data-stu-id="e5293-218">**Resolution**</span></span>

<span data-ttu-id="e5293-219">toodelete e creare un nuovo certificato, seguire i passaggi di hello riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="e5293-219">toodelete and create a new certificate, follow hello steps below:</span></span>

1.  <span data-ttu-id="e5293-220">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="e5293-220">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e5293-221">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-221">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e5293-222">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e5293-222">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e5293-223">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e5293-223">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e5293-224">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e5293-224">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="e5293-225">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="e5293-225">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e5293-226">Selezionare l'applicazione hello da tooconfigure single sign-on</span><span class="sxs-lookup"><span data-stu-id="e5293-226">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="e5293-227">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-227">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e5293-228">Fare clic su **Crea nuovo certificato** in hello **SAML certificato di firma** sezione.</span><span class="sxs-lookup"><span data-stu-id="e5293-228">click **Create new certificate** under hello **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="e5293-229">Selezionare la data di scadenza.</span><span class="sxs-lookup"><span data-stu-id="e5293-229">Select Expiration date.</span></span> <span data-ttu-id="e5293-230">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e5293-230">Then, click **Save.**</span></span>

10. <span data-ttu-id="e5293-231">Controllare **attivare di nuovo certificato** toooverride certificato active di hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-231">Check **Make new certificate active** toooverride hello active certificate.</span></span> <span data-ttu-id="e5293-232">Quindi, fare clic su **salvare** nella parte superiore di hello del pannello hello e accettare il certificato di rollover tooactivate hello.</span><span class="sxs-lookup"><span data-stu-id="e5293-232">Then, click **Save** at hello top of hello blade and accept tooactivate hello rollover certificate.</span></span>

11. <span data-ttu-id="e5293-233">In hello **certificato di firma SAML** fare clic su **rimuovere** tooremove hello **inutilizzato** certificato.</span><span class="sxs-lookup"><span data-stu-id="e5293-233">Under hello **SAML Signing Certificate** section, click **remove** tooremove hello **Unused** certificate.</span></span>

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="e5293-234">Problema durante la personalizzazione delle attestazioni SAML hello inviati tooan applicazione</span><span class="sxs-lookup"><span data-stu-id="e5293-234">Problem when customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="e5293-235">toolearn come le attestazioni degli attributi toocustomize hello SAML inviato tooyour applicazione, vedere [attestazioni mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="e5293-235">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5293-236">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e5293-236">Next steps</span></span>
[<span data-ttu-id="e5293-237">Come toodebug basato su SAML single sign-on tooapplications in Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5293-237">How toodebug SAML-based single sign-on tooapplications in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
