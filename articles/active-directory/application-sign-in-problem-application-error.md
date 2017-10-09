---
title: aaaError nella pagina di un'applicazione dopo l'accesso | Documenti Microsoft
description: Come tooresolve problemi con Azure AD accesso quando un'applicazione hello stesso genera un errore
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
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="1ccd5-103">Errore nella pagina di un'applicazione dopo l'accesso</span><span class="sxs-lookup"><span data-stu-id="1ccd5-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="1ccd5-104">In questo scenario, Azure AD ha eseguito l'accesso utente hello in, ma un'applicazione hello viene visualizzato un errore non consentire hello utente toosuccessfully fine hello sign in flusso.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-104">In this scenario, Azure AD has signed hello user in, but hello application is displaying an error not allowing hello user toosuccessfully finish hello sign in flow.</span></span> <span data-ttu-id="1ccd5-105">In questo scenario, un'applicazione hello non accetta il problema di risposta hello da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-105">In this scenario, hello application is not accepting hello response issue by Azure AD.</span></span>

<span data-ttu-id="1ccd5-106">Esistono alcune delle possibili cause per cui un'applicazione hello rifiutata risposta hello da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-106">There are some possible reasons why hello application didn’t accept hello response from Azure AD.</span></span> <span data-ttu-id="1ccd5-107">Se l'errore hello in un'applicazione hello non è sufficientemente chiaro tooknow cosa manca in risposta hello, quindi:</span><span class="sxs-lookup"><span data-stu-id="1ccd5-107">If hello error in hello application is not clear enough tooknow what is missing in hello response, then:</span></span>

-   <span data-ttu-id="1ccd5-108">Se un'applicazione hello raccolta hello Azure AD, verificare di aver seguito tutti i passaggi nell'articolo hello hello [come toodebug basato su SAML single sign-on tooapplications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="1ccd5-108">If hello application is hello Azure AD Gallery, verify you have followed all hello steps in hello article [How toodebug SAML-based single sign-on tooapplications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="1ccd5-109">Utilizzare uno strumento come [Fiddler](http://www.telerik.com/fiddler) toocapture SAML richiesta, risposta SAML e token SAML.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) toocapture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="1ccd5-110">Condividere risposta SAML hello con hello applicazione fornitore tooknow cosa manca.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-110">Share hello SAML response with hello application vendor tooknow what is missing.</span></span>

## <a name="missing-attributes-in-hello-saml-response"></a><span data-ttu-id="1ccd5-111">Attributi mancanti hello risposta SAML</span><span class="sxs-lookup"><span data-stu-id="1ccd5-111">Missing attributes in hello SAML response</span></span>

<span data-ttu-id="1ccd5-112">un attributo in toobe di configurazione di Azure AD hello inviato in risposta hello Azure AD, tooadd procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="1ccd5-112">tooadd an attribute in hello Azure AD configuration toobe sent in hello Azure AD response, follow hello steps below:</span></span>

1.  <span data-ttu-id="1ccd5-113">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="1ccd5-113">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1ccd5-114">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-114">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1ccd5-115">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-115">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1ccd5-116">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-116">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1ccd5-117">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-117">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="1ccd5-118">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="1ccd5-118">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1ccd5-119">Selezionare l'applicazione hello tooconfigure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-119">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="1ccd5-120">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-120">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1ccd5-121">Fare clic su **visualizzare e modificare gli attributi di tutti gli altri utenti in** hello **gli attributi utente** hello tooedit sezione attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-121">click **View and edit all other user attributes under** hello **User Attributes** section tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="1ccd5-122">un attributo tooadd:</span><span class="sxs-lookup"><span data-stu-id="1ccd5-122">tooadd an attribute:</span></span>

   * <span data-ttu-id="1ccd5-123">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-123">click **Add attribute**.</span></span> <span data-ttu-id="1ccd5-124">Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-124">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   * <span data-ttu-id="1ccd5-125">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-125">Click **Save.**</span></span> <span data-ttu-id="1ccd5-126">Vedrai hello nuovo attributo tabella hello.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-126">You see hello new attribute in hello table.</span></span>

9.  <span data-ttu-id="1ccd5-127">Salvare la configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-127">Save hello configuration.</span></span>

<span data-ttu-id="1ccd5-128">Successivo accesso dell'applicazione toohello, hello utente Azure AD inviare nuovo attributo hello hello risposta SAML.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-128">Next time hello user signs in toohello application, Azure AD send hello new attribute in hello SAML response.</span></span>

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="1ccd5-129">un'applicazione Hello prevede un formato o un valore di identificatore utente diverso</span><span class="sxs-lookup"><span data-stu-id="1ccd5-129">hello application expects a different User Identifier value or format</span></span>

<span data-ttu-id="1ccd5-130">Hello Accedi toohello applicazione non riesce perché hello risposta SAML mancano gli attributi, ad esempio i ruoli o un'applicazione hello è previsto un formato diverso per l'attributo EntityID hello.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-130">hello sign-in toohello application is failing because hello SAML response is missing attributes such as roles or because hello application is expecting a different format for hello EntityID attribute.</span></span>

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a><span data-ttu-id="1ccd5-131">Aggiungere un attributo nella configurazione dell'applicazione hello Azure AD:</span><span class="sxs-lookup"><span data-stu-id="1ccd5-131">Add an attribute in hello Azure AD application configuration:</span></span>

<span data-ttu-id="1ccd5-132">hello toochange valore identificatore utente, effettuare i passaggi di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="1ccd5-132">toochange hello User Identifier value, follow hello steps below:</span></span>

1.  <span data-ttu-id="1ccd5-133">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="1ccd5-133">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1ccd5-134">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-134">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1ccd5-135">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-135">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1ccd5-136">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-136">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1ccd5-137">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-137">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="1ccd5-138">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="1ccd5-138">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1ccd5-139">Selezionare l'applicazione hello tooconfigure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-139">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="1ccd5-140">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-140">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1ccd5-141">In hello **gli attributi utente**, selezionare hello identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-141">Under hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="1ccd5-142">Modificare il formato di EntityID (ID utente)</span><span class="sxs-lookup"><span data-stu-id="1ccd5-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="1ccd5-143">Se un'applicazione hello prevede che un altro formato per l'attributo EntityID hello.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-143">If hello application expects another format for hello EntityID attribute.</span></span> <span data-ttu-id="1ccd5-144">Quindi, non sarà formato EntityID (ID utente) di hello tooselect in grado di Azure AD invia toohello applicazione in risposta hello dopo l'autenticazione utente.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-144">Then, you won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="1ccd5-145">Azure AD selezionare hello formato attributo NameID hello (ID utente) in base al valore di hello selezionato o per hello formato richiesto da un'applicazione hello in hello AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-145">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="1ccd5-146">Per ulteriori informazioni visitare articolo hello [protocollo Single Sign-On SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) in hello sezione NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-146">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a><span data-ttu-id="1ccd5-147">un'applicazione Hello prevede un metodo di firma diversa per la risposta SAML hello</span><span class="sxs-lookup"><span data-stu-id="1ccd5-147">hello application expects a different signature method for hello SAML response</span></span>

<span data-ttu-id="1ccd5-148">toochange quali parti del token SAML hello sono firmate digitalmente da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-148">toochange what parts of hello SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="1ccd5-149">Attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="1ccd5-149">Follow hello steps below:</span></span>

1.  <span data-ttu-id="1ccd5-150">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="1ccd5-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1ccd5-151">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1ccd5-152">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1ccd5-153">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1ccd5-154">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1ccd5-155">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="1ccd5-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1ccd5-156">Selezionare l'applicazione hello tooconfigure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-156">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="1ccd5-157">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-157">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1ccd5-158">Fare clic su **Mostra impostazioni di firma certificato avanzate** in hello **certificato di firma SAML** sezione.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-158">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="1ccd5-159">Seleziona hello appropriato **opzione firma** previsto dall'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="1ccd5-159">Select hello appropriate **Signing Option** expected by hello application:</span></span>

  * <span data-ttu-id="1ccd5-160">Firma risposta SAML</span><span class="sxs-lookup"><span data-stu-id="1ccd5-160">Sign SAML response</span></span>

  * <span data-ttu-id="1ccd5-161">Firma asserzione e risposta SAML</span><span class="sxs-lookup"><span data-stu-id="1ccd5-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="1ccd5-162">Firma asserzione SAML</span><span class="sxs-lookup"><span data-stu-id="1ccd5-162">Sign SAML assertion</span></span>

<span data-ttu-id="1ccd5-163">Successivo accesso dell'applicazione toohello, hello utente l'accesso di Azure AD hello parte della risposta SAML hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-163">Next time hello user signs in toohello application, Azure AD sign hello part of hello SAML response selected.</span></span>

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a><span data-ttu-id="1ccd5-164">un'applicazione Hello prevede hello firma toobe algoritmo SHA-1</span><span class="sxs-lookup"><span data-stu-id="1ccd5-164">hello application expects hello signing algorithm toobe SHA-1</span></span>

<span data-ttu-id="1ccd5-165">Per impostazione predefinita, Azure AD firma token SAML hello utilizzando hello la maggior parte delle algoritmo di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-165">By default, Azure AD signs hello SAML token using hello most security algorithm.</span></span> <span data-ttu-id="1ccd5-166">Si consiglia di non modificare hello sign algoritmo tooSHA-1 se non richiesto da un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-166">Changing hello sign algorithm tooSHA-1 is not recommended unless required by hello application.</span></span>

<span data-ttu-id="1ccd5-167">toochange hello algoritmo di firma, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="1ccd5-167">toochange hello signing algorithm, follow hello steps below:</span></span>

1.  <span data-ttu-id="1ccd5-168">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="1ccd5-168">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1ccd5-169">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-169">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1ccd5-170">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-170">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1ccd5-171">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-171">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1ccd5-172">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-172">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="1ccd5-173">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="1ccd5-173">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1ccd5-174">Selezionare l'applicazione hello tooconfigure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-174">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="1ccd5-175">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-175">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1ccd5-176">Fare clic su **Mostra impostazioni di firma certificato avanzate** in hello **certificato di firma SAML** sezione.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-176">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="1ccd5-177">Selezionare SHA-1, hello **algoritmo di firma**.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-177">Select SHA-1, in hello **Signing Algorithm**.</span></span>

<span data-ttu-id="1ccd5-178">Successivo hello utente esegue l'accesso nell'applicazione toohello, accesso di Azure AD hello token SAML con l'algoritmo SHA-1.</span><span class="sxs-lookup"><span data-stu-id="1ccd5-178">Next time hello user signs in toohello application, Azure AD sign hello SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ccd5-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1ccd5-179">Next steps</span></span>
[<span data-ttu-id="1ccd5-180">Come toodebug basato su SAML single sign-on tooapplications in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ccd5-180">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
