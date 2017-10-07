---
title: configurazione delle password single sign-on per un'applicazione non raccolta aaaProblem | Documenti Microsoft
description: Comprendere faccia persone problemi comuni di hello quando si configura Password Single Sign-on per le applicazioni non raccolta personalizzate che non sono elencate in hello raccolta di applicazioni Azure AD
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
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="037cd-103">Problema nella configurazione dell'accesso Single Sign-On basato su password per un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="037cd-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="037cd-104">Questo articolo è utile faccia di persone di toounderstand hello comuni problemi quando si configura **Password single sign-on** con un'applicazione non raccolta.</span><span class="sxs-lookup"><span data-stu-id="037cd-104">This article help you toounderstand hello common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-toocapture-sign-in-fields-for-an-application"></a><span data-ttu-id="037cd-105">Accedi toocapture come campi di un'applicazione</span><span class="sxs-lookup"><span data-stu-id="037cd-105">How toocapture sign-in fields for an application</span></span>

<span data-ttu-id="037cd-106">L'acquisizione dei campi di accesso è supportata solo per le pagine di accesso basate su HTML e **non è supportata per le pagine di accesso non standard**, ad esempio le pagine che usano Flash o altre tecnologie non basate su HTML.</span><span class="sxs-lookup"><span data-stu-id="037cd-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="037cd-107">Esistono due modi per acquisire i campi di accesso per le applicazioni personalizzate:</span><span class="sxs-lookup"><span data-stu-id="037cd-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="037cd-108">Acquisizione automatica dei campi di accesso</span><span class="sxs-lookup"><span data-stu-id="037cd-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="037cd-109">Acquisizione manuale dei campi di accesso</span><span class="sxs-lookup"><span data-stu-id="037cd-109">Manual sign-in field capture</span></span>

<span data-ttu-id="037cd-110">**Acquisizione di campo accesso automatico** funziona correttamente con la maggior parte delle abilitato HTML delle pagine di accesso, se si utilizza **ID DIV noti hello username e password di input** campo.</span><span class="sxs-lookup"><span data-stu-id="037cd-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for hello username and password input** field.</span></span> <span data-ttu-id="037cd-111">Hello pratica è da scraping hello HTML nella pagina di hello toofind ID DIV che corrispondono a determinati criteri e salvando quindi che i metadati per questa applicazione, pertanto è possibile riprodurre tooit le password in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="037cd-111">hello way this works is by scraping hello HTML on hello page toofind DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords tooit later.</span></span>

<span data-ttu-id="037cd-112">**Acquisizione manuale Accedi campo** può essere usata in caso di hello che hello applicazione **fornitore non etichetta** hello input campi utilizzati per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="037cd-112">**Manual sign-in field capture** can be used in hello case that hello application **vendor does not label** hello input fields used for sign in.</span></span> <span data-ttu-id="037cd-113">Acquisizione manuale Accedi campo può essere usata anche in caso di hello quando hello **fornitore esegue il rendering di più campi** che non può essere rilevata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="037cd-113">Manual sign-in field capture can also be used in hello case when hello **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="037cd-114">Azure AD possono archiviare i dati per come firma un numero di campi si trovano in hello nella pagina, purché si informazioni in tali campi sono nella pagina hello.</span><span class="sxs-lookup"><span data-stu-id="037cd-114">Azure AD can store data for as many fields as are on hello sign in page, so long as you tell us where those fields are on hello page.</span></span>

<span data-ttu-id="037cd-115">In generale, **se acquisizione campo accesso automatico non funziona, è sempre consigliabile opzione manuale di hello durante il tentativo.**</span><span class="sxs-lookup"><span data-stu-id="037cd-115">In general, **if automatic sign-in field capture does not work, we always suggest trying hello manual option.**</span></span>

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="037cd-116">Come tooautomatically acquisire i campi di accesso per un'applicazione</span><span class="sxs-lookup"><span data-stu-id="037cd-116">How tooautomatically capture sign-in fields for an application</span></span>

<span data-ttu-id="037cd-117">tooconfigure **basato su Password Single Sign-on** per un'applicazione mediante **acquisizione automatica Accedi campo**, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="037cd-117">tooconfigure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="037cd-118">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="037cd-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="037cd-119">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="037cd-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="037cd-120">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="037cd-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="037cd-121">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="037cd-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="037cd-122">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="037cd-122">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="037cd-123">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="037cd-123">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="037cd-124">Selezionare l'applicazione hello tooconfigure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="037cd-124">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="037cd-125">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="037cd-125">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="037cd-126">Modalità di selezione hello **basato su Password Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="037cd-126">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="037cd-127">Immettere hello **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="037cd-127">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="037cd-128">Si tratta hello URL in cui gli utenti immettono il nome utente e password toosign in a.</span><span class="sxs-lookup"><span data-stu-id="037cd-128">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="037cd-129">**Verificare che i campi di accesso hello siano visibili nell'URL hello è fornire**.</span><span class="sxs-lookup"><span data-stu-id="037cd-129">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="037cd-130">Fare clic su hello **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="037cd-130">Click hello **Save** button.</span></span>

11. <span data-ttu-id="037cd-131">Una volta tale scopo, si verrà automaticamente cercare come URL per un nome utente e password casella di input e consentono di toouse AD Azure toosecurely trasmettere applicazione toothat le password utilizzando l'estensione browser del Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="037cd-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span>

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="037cd-132">Come toomanually acquisire i campi di accesso per un'applicazione</span><span class="sxs-lookup"><span data-stu-id="037cd-132">How toomanually capture sign-in fields for an application</span></span>

<span data-ttu-id="037cd-133">toomanually acquisizione i campi di accesso, è necessario aver installato estensione Browser Pannello di accesso di hello e **non sia in esecuzione in modalità inPrivate, incognito o private.**</span><span class="sxs-lookup"><span data-stu-id="037cd-133">toomanually capture sign in fields, you must first have hello Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="037cd-134">estensione del browser di hello tooinstall, seguire la procedura seguente hello in hello [come tooinstall hello estensione Browser Pannello di accesso](#i-cannot-manually-detect-sign-in-fields-for-my-application) sezione.</span><span class="sxs-lookup"><span data-stu-id="037cd-134">tooinstall hello browser extension, follow hello steps in hello [How tooinstall hello Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="037cd-135">tooconfigure **basato su Password Single Sign-on** per un'applicazione mediante **acquisizione manuale Accedi campo**, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="037cd-135">tooconfigure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="037cd-136">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="037cd-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="037cd-137">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="037cd-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="037cd-138">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="037cd-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="037cd-139">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="037cd-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="037cd-140">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="037cd-140">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="037cd-141">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="037cd-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="037cd-142">Selezionare l'applicazione hello tooconfigure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="037cd-142">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="037cd-143">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="037cd-143">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="037cd-144">Modalità di selezione hello **basato su Password Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="037cd-144">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="037cd-145">Immettere hello **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="037cd-145">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="037cd-146">Si tratta hello URL in cui gli utenti immettono il nome utente e password toosign in a.</span><span class="sxs-lookup"><span data-stu-id="037cd-146">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="037cd-147">**Verificare che i campi di accesso hello siano visibili nell'URL hello è fornire**.</span><span class="sxs-lookup"><span data-stu-id="037cd-147">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="037cd-148">Fare clic su hello **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="037cd-148">Click hello **Save** button.</span></span>

11. <span data-ttu-id="037cd-149">Una volta tale scopo, si verrà automaticamente cercare come URL per un nome utente e password casella di input e consentono di toouse AD Azure toosecurely trasmettere applicazione toothat le password utilizzando l'estensione browser del Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="037cd-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span> <span data-ttu-id="037cd-150">In caso di hello che l'operazione non riesce, è possibile **hello Accedi modalità toouse manuale Accedi campo acquisizione delle modifiche** continuando toostep 12.</span><span class="sxs-lookup"><span data-stu-id="037cd-150">In hello case that this fails, you can **change hello sign-in mode toouse manual sign-in field capture** by continuing toostep 12.</span></span>

12. <span data-ttu-id="037cd-151">Fare clic su **Configura impostazioni Password Single Sign-On per &lt;nomeapp&gt;**.</span><span class="sxs-lookup"><span data-stu-id="037cd-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="037cd-152">Seleziona hello **rilevare manualmente Accedi campi** opzione di configurazione.</span><span class="sxs-lookup"><span data-stu-id="037cd-152">Select hello **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="037cd-153">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="037cd-153">Click **Ok**.</span></span>

15. <span data-ttu-id="037cd-154">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="037cd-154">Click **Save**.</span></span>

16. <span data-ttu-id="037cd-155">Seguire hello schermata istruzioni toouse hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="037cd-155">Follow hello on screen instructions toouse hello Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="037cd-156">Errore "Non sono stati trovati campi di accesso nell'URL specificato"</span><span class="sxs-lookup"><span data-stu-id="037cd-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="037cd-157">Questo errore viene visualizzato quando il rilevamento automatico dei campi di accesso ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="037cd-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="037cd-158">Questo problema, provare manuale Accedi campo rilevamento da hello seguendo i passaggi in hello tooresolve [come toomanually acquisire i campi di accesso per un'applicazione](#how-to-manually-capture-sign-in-fields-for-an-application) sezione.</span><span class="sxs-lookup"><span data-stu-id="037cd-158">tooresolve this issue, try manual sign-in field detection by following hello steps in hello [How toomanually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a><span data-ttu-id="037cd-159">Viene visualizzato un errore di "configurazione Single Sign-on non è possibile toosave"</span><span class="sxs-lookup"><span data-stu-id="037cd-159">I see an “Unable toosave Single Sign-on configuration” error</span></span>

<span data-ttu-id="037cd-160">In alcuni casi rari, l'aggiornamento della configurazione hello single sign-on può avere esito negativo.</span><span class="sxs-lookup"><span data-stu-id="037cd-160">In certain rare cases, updating hello single sign-on configuration can fail.</span></span> <span data-ttu-id="037cd-161">tooresolve questo provare a salvare hello configurazione single sign-on nuovamente.</span><span class="sxs-lookup"><span data-stu-id="037cd-161">tooresolve this try saving hello single sign-on configuration again.</span></span>

<span data-ttu-id="037cd-162">Se il problema persiste toofail in modo coerente, assistenza al supporto tecnico e fornire informazioni di hello raccolte in hello [come dettagli di hello toosee di una notifica tramite il portale](#i-cannot-manually-detect-sign-in-fields-for-my-application) e [come la Guida mediante l'invio di notifiche dettagli tooa tooget il supporto tecnico](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sezioni.</span><span class="sxs-lookup"><span data-stu-id="037cd-162">If this continues toofail consistently, open a support case and provide hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="037cd-163">Non è possibile rilevare manualmente i campi di accesso per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="037cd-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="037cd-164">Alcuni dei comportamenti hello che si potrebbero verificare quando il rilevamento manuale non funziona:</span><span class="sxs-lookup"><span data-stu-id="037cd-164">Some of hello behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="037cd-165">il processo di acquisizione manuale di Hello sembrava toowork, ma i campi di hello acquisiti non sono corretti</span><span class="sxs-lookup"><span data-stu-id="037cd-165">hello manual capture process appeared toowork, but hello fields captured were not correct</span></span>

-   <span data-ttu-id="037cd-166">Hello destra campi non vengono evidenziati quando si esegue il processo di acquisizione hello</span><span class="sxs-lookup"><span data-stu-id="037cd-166">hello right fields don’t get highlighted when performing hello capture process</span></span>

-   <span data-ttu-id="037cd-167">il processo di acquisizione Hello viene visualizzata la pagina di accesso dell'applicazione toohello come previsto, ma non accade nulla</span><span class="sxs-lookup"><span data-stu-id="037cd-167">hello capture process takes me toohello application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="037cd-168">Acquisizione manuale visualizzata toowork SSO non verificarsi quando gli utenti visitano toohello applicazione hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="037cd-168">Manual capture appears toowork, but SSO doesn’t happen when my users navigate toohello application from hello Access Panel.</span></span>

<span data-ttu-id="037cd-169">Se si verifica uno di questi problemi, verificare i seguenti di hello:</span><span class="sxs-lookup"><span data-stu-id="037cd-169">check hello following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="037cd-170">Verificare di disporre di più recente dell'estensione del browser del Pannello di accesso hello hello **installato** e **abilitato** seguendo procedure hello hello [come tooinstall hello Browser Pannello di accesso estensione](#how-to-install-the-access-panel-browser-extension) sezione.</span><span class="sxs-lookup"><span data-stu-id="037cd-170">Ensure that you have hello latest version of hello access panel browser extension **installed** and **enabled** by following hello steps in hello [How tooinstall hello Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="037cd-171">Verificare che non si stia tentando il processo di acquisizione hello durante il browser **modalità privata, inPrivate o incognito**.</span><span class="sxs-lookup"><span data-stu-id="037cd-171">Ensure that you are not attempting hello capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="037cd-172">estensione del Pannello di accesso Hello non è supportata in queste modalità.</span><span class="sxs-lookup"><span data-stu-id="037cd-172">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="037cd-173">Verificare che gli utenti non siano cercando toosign nell'applicazione toohello dal Pannello di accesso hello durante in **modalità privata, inPrivate o incognito**.</span><span class="sxs-lookup"><span data-stu-id="037cd-173">Ensure that your users are not trying toosign in toohello application from hello access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="037cd-174">estensione del Pannello di accesso Hello non è supportata in queste modalità.</span><span class="sxs-lookup"><span data-stu-id="037cd-174">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="037cd-175">Riprovare il processo di acquisizione manuale di hello, verifica i marcatori di hello rosso sono campi corretti hello.</span><span class="sxs-lookup"><span data-stu-id="037cd-175">Try hello manual capture process again, ensuring hello red markers are over hello correct fields.</span></span>

-   <span data-ttu-id="037cd-176">Se il processo di acquisizione manuale di hello sembra toohang, o pagina di accesso hello non esegue alcuna operazione (caso 3 sopra), riprovare il processo di acquisizione manuale di hello.</span><span class="sxs-lookup"><span data-stu-id="037cd-176">If hello manual capture process seems toohang, or hello sign in page doesn’t do anything (case 3 above), try hello manual capture process again.</span></span> <span data-ttu-id="037cd-177">Ma questa volta dopo aver completato il processo di hello, premere hello **F12** pulsante tooopen console per sviluppatori del browser.</span><span class="sxs-lookup"><span data-stu-id="037cd-177">But, this time after completing hello process, press hello **F12** button tooopen your browser’s developer console.</span></span> <span data-ttu-id="037cd-178">Una volta, aprire hello **console** e tipo **window.location= "&lt;immettere hello sign in url specificato quando si configura l'applicazione hello&gt;"** e quindi premere  **Immettere**.</span><span class="sxs-lookup"><span data-stu-id="037cd-178">Once there, open hello **console** and type **window.location=”&lt;enter hello sign in url you specified when configuring hello app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="037cd-179">Questa forza una pagina di reindirizzamento cui terminare il processo di acquisizione hello e archiviare hello campi che sono stati acquisiti.</span><span class="sxs-lookup"><span data-stu-id="037cd-179">This force a page redirect which end hello capture process and store hello fields that have been captured.</span></span>

<span data-ttu-id="037cd-180">Se nessuno di questi approcci risolve il problema, rivolgersi al supporto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="037cd-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="037cd-181">Assistenza al supporto tecnico con i dettagli di hello di ciò che si è tentato, nonché informazioni hello raccolte in hello [come dettagli di hello toosee di una notifica tramite il portale](#i-cannot-manually-detect-sign-in-fields-for-my-application) e [informazioni tooget inviando i dettagli sulla notifica tooa supporto tecnico](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sezioni (se applicabile).</span><span class="sxs-lookup"><span data-stu-id="037cd-181">Open a support case with hello details of what you tried, as well as hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="037cd-182">Come tooinstall hello estensione Browser Pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="037cd-182">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="037cd-183">hello tooinstall estensione Browser Pannello di accesso, le operazioni di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="037cd-183">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="037cd-184">Aprire hello [Pannello di accesso](https://myapps.microsoft.com) in uno dei browser supportato hello e accedere come un **utente** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="037cd-184">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="037cd-185">Fare clic su un **applicazione password SSO** in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="037cd-185">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="037cd-186">Hello prompt dei comandi in cui viene chiesto tooinstall hello selezionare software **installa**.</span><span class="sxs-lookup"><span data-stu-id="037cd-186">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="037cd-187">Basata sul browser è il collegamento di download toohello diretto.</span><span class="sxs-lookup"><span data-stu-id="037cd-187">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="037cd-188">**Aggiungere** browser tooyour di estensione hello.</span><span class="sxs-lookup"><span data-stu-id="037cd-188">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="037cd-189">Se il browser viene richiesto, selezionare tooeither **abilitare** o **Consenti** hello estensione.</span><span class="sxs-lookup"><span data-stu-id="037cd-189">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="037cd-190">Al termine dell'installazione, **riavviare** la sessione del browser.</span><span class="sxs-lookup"><span data-stu-id="037cd-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="037cd-191">Accedere in hello Pannello di accesso e di vedere se è possibile **avviare** applicazioni password SSO.</span><span class="sxs-lookup"><span data-stu-id="037cd-191">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="037cd-192">È anche possibile scaricare l'estensione hello per Chrome e Firefox dai collegamenti diretti hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="037cd-192">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="037cd-193">Estensione Pannello di accesso per Chrome</span><span class="sxs-lookup"><span data-stu-id="037cd-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="037cd-194">Estensione Pannello di accesso per Firefox</span><span class="sxs-lookup"><span data-stu-id="037cd-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a><span data-ttu-id="037cd-195">Modalità dettagli hello toosee di una notifica del portale</span><span class="sxs-lookup"><span data-stu-id="037cd-195">How toosee hello details of a portal notification</span></span>

<span data-ttu-id="037cd-196">È possibile visualizzare i dettagli di hello di qualsiasi notifica tramite il portale seguendo i passaggi di hello riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="037cd-196">You can see hello details of any portal notification by following hello steps below:</span></span>

1.  <span data-ttu-id="037cd-197">Fare clic su hello **notifiche** icona (campana hello) in alto a destra hello di hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="037cd-197">click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal</span></span>

2.  <span data-ttu-id="037cd-198">Selezionare qualsiasi notifica in un **errore** stato (quelli con un toothem Avanti rosso (!)).</span><span class="sxs-lookup"><span data-stu-id="037cd-198">Select any notification in an **Error** state (those with a red (!) next toothem).</span></span>

  ><span data-ttu-id="037cd-199">!NOTA] Non è possibile fare clic sulle notifiche in uno stato di **Operazione completata** o **In corso**.</span><span class="sxs-lookup"><span data-stu-id="037cd-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="037cd-200">Questo hello aprire **i dettagli sulla notifica** blade.</span><span class="sxs-lookup"><span data-stu-id="037cd-200">This open hello **Notification Details** blade.</span></span>

4.  <span data-ttu-id="037cd-201">Utilizzare queste informazioni manualmente toounderstand ulteriori dettagli sul problema hello.</span><span class="sxs-lookup"><span data-stu-id="037cd-201">Use this information yourself toounderstand more details about hello problem.</span></span>

5.  <span data-ttu-id="037cd-202">Se è ancora necessario della Guida, è possibile condividere queste informazioni con il problema con un supporto tecnico o hello gruppo tooget Guida del prodotto.</span><span class="sxs-lookup"><span data-stu-id="037cd-202">If you still need help, you can also share this information with a support engineer or hello product group tooget help with your problem.</span></span>

6.  <span data-ttu-id="037cd-203">Fare clic su hello **copia** **icona** toohello diritto di hello **copiare errore** toocopy textbox tutti hello tooshare dettagli di notifica con un ingegnere del supporto o il prodotto gruppo.</span><span class="sxs-lookup"><span data-stu-id="037cd-203">Click hello **copy** **icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer.</span></span>

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a><span data-ttu-id="037cd-204">Informazioni tooget inviando al supporto tecnico tooa dettagli di notifica</span><span class="sxs-lookup"><span data-stu-id="037cd-204">How tooget help by sending notification details tooa support engineer</span></span>

<span data-ttu-id="037cd-205">È molto importante che si condivide **tutti hello dettagli riportati di seguito** con un supporto tecnico per assistenza, in modo che tali eventi consentono rapidamente.</span><span class="sxs-lookup"><span data-stu-id="037cd-205">It is very important that you share **all hello details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="037cd-206">Tale scopo, **acquisire uno screenshot,** o facendo clic su hello **sull'icona di errore di copia**, trovato toohello destra di hello **copiare errore** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="037cd-206">You can do this easily by **taking a screenshot,** or by clicking hello **Copy error icon**, found toohello right of hello **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="037cd-207">Spiegazione dei dettagli della notifica</span><span class="sxs-lookup"><span data-stu-id="037cd-207">Notification Details Explained</span></span>

<span data-ttu-id="037cd-208">Hello seguente illustra più quali tutti gli elementi hello notifica significa e fornisce esempi di ognuno di essi.</span><span class="sxs-lookup"><span data-stu-id="037cd-208">hello below explains more what each of hello notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="037cd-209">Elementi essenziali della notifica</span><span class="sxs-lookup"><span data-stu-id="037cd-209">Essential Notification Items</span></span>

-   <span data-ttu-id="037cd-210">**Titolo** : hello titolo descrittivo della notifica hello</span><span class="sxs-lookup"><span data-stu-id="037cd-210">**Title** – hello descriptive title of hello notification</span></span>

    -   <span data-ttu-id="037cd-211">Esempio: **Impostazioni proxy di applicazione**</span><span class="sxs-lookup"><span data-stu-id="037cd-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="037cd-212">**Descrizione** : hello descrizione di ciò che si è verificato in seguito a operazione hello</span><span class="sxs-lookup"><span data-stu-id="037cd-212">**Description** – hello description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="037cd-213">Esempio: **L'URL interno immesso è già usato da un'altra applicazione**</span><span class="sxs-lookup"><span data-stu-id="037cd-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="037cd-214">**Id di notifica** : id univoco di hello della notifica hello</span><span class="sxs-lookup"><span data-stu-id="037cd-214">**Notification Id** – hello unique id of hello notification</span></span>

    -   <span data-ttu-id="037cd-215">Esempio: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="037cd-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="037cd-216">**Id richiesta client** : id richiesta specifico hello apportate dal browser</span><span class="sxs-lookup"><span data-stu-id="037cd-216">**Client Request Id** – hello specific request id made by your browser</span></span>

    -   <span data-ttu-id="037cd-217">Esempio: **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="037cd-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="037cd-218">**Ora UTC timbro** : hello timestamp durante il quale la notifica hello si è verificato, in formato UTC</span><span class="sxs-lookup"><span data-stu-id="037cd-218">**Time Stamp UTC** – hello timestamp during which hello notification occurred, in UTC</span></span>

    -   <span data-ttu-id="037cd-219">Esempio: **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="037cd-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="037cd-220">**Id della transazione interna** : hello ID interno, è possibile utilizzare l'errore hello toolook nei nostri sistemi</span><span class="sxs-lookup"><span data-stu-id="037cd-220">**Internal Transaction Id** – hello internal ID we can use toolook hello error up in our systems</span></span>

    -   <span data-ttu-id="037cd-221">Esempio: **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="037cd-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="037cd-222">**UPN** – utente hello che ha eseguito l'operazione di hello</span><span class="sxs-lookup"><span data-stu-id="037cd-222">**UPN** – hello user who performed hello operation</span></span>

    -   <span data-ttu-id="037cd-223">Esempio: **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="037cd-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="037cd-224">**Id tenant** : hello ID univoco del tenant hello che hello utente che ha eseguito l'operazione di hello è un membro di</span><span class="sxs-lookup"><span data-stu-id="037cd-224">**Tenant Id** – hello unique ID of hello tenant that hello user who performed hello operation was a member of</span></span>

    -   <span data-ttu-id="037cd-225">Esempio: **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="037cd-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="037cd-226">**L'Id di oggetto utente** : hello ID univoco dell'utente di hello che ha eseguito l'operazione di hello</span><span class="sxs-lookup"><span data-stu-id="037cd-226">**User object Id** – hello unique ID of hello user who performed hello operation</span></span>

    -   <span data-ttu-id="037cd-227">Esempio: **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="037cd-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="037cd-228">Elementi della notifica dettagliati</span><span class="sxs-lookup"><span data-stu-id="037cd-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="037cd-229">**Nome visualizzato** – **(può essere vuoto)** un nome di visualizzazione più dettagliato per correggere l'errore hello</span><span class="sxs-lookup"><span data-stu-id="037cd-229">**Display Name** – **(can be empty)** a more detailed display name for hello error</span></span>

    -   <span data-ttu-id="037cd-230">Esempio*: **impostazioni del proxy di applicazione**</span><span class="sxs-lookup"><span data-stu-id="037cd-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="037cd-231">**Stato** : hello specifico stato di notifica di hello</span><span class="sxs-lookup"><span data-stu-id="037cd-231">**Status** – hello specific status of hello notification</span></span>

    -   <span data-ttu-id="037cd-232">Esempio*: **Operazione non riuscita**</span><span class="sxs-lookup"><span data-stu-id="037cd-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="037cd-233">**Id di oggetto** – **(può essere vuoto)** hello ID di oggetto su cui hello è stata eseguita l'operazione</span><span class="sxs-lookup"><span data-stu-id="037cd-233">**Object Id** – **(can be empty)** hello object ID against which hello operation was performed</span></span>

    -   <span data-ttu-id="037cd-234">Esempio: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="037cd-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="037cd-235">**Dettagli** : hello descrizione dettagliata dell'accaduto come risultato di operazione hello</span><span class="sxs-lookup"><span data-stu-id="037cd-235">**Details** – hello detailed description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="037cd-236">Esempio: **L'URL interno "http://bing.com/" non è valido perché è già in uso**</span><span class="sxs-lookup"><span data-stu-id="037cd-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="037cd-237">**Copiare l'errore** – fare clic su hello **sull'icona Copia** toohello diritto di hello **copiare errore** toocopy textbox tutti hello tooshare dettagli di notifica con un ingegnere del supporto o il prodotto gruppo</span><span class="sxs-lookup"><span data-stu-id="037cd-237">**Copy error** – Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer</span></span>

    -   <span data-ttu-id="037cd-238">Esempio: ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="037cd-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="037cd-239">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="037cd-239">Next steps</span></span>
[<span data-ttu-id="037cd-240">Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="037cd-240">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

