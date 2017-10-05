---
title: Problema nella configurazione dell'accesso Single Sign-On basato su password per un'applicazione non inclusa nella raccolta | Microsoft Docs
description: Informazioni sui problemi comuni che si possono incontrare durante la configurazione dell'accesso Single Sign-On basato su password per applicazioni personalizzate non incluse nella raccolta delle applicazioni di Azure AD
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
ms.openlocfilehash: 9c76b6f3495e2dd759a156fcef97b57aece8d632
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="97b49-103">Problema nella configurazione dell'accesso Single Sign-On basato su password per un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="97b49-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="97b49-104">L'articolo descrive i problemi comuni che si possono incontrare durante la configurazione dell'accesso**Single Sign-On basato su password** per un'applicazione non inclusa nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="97b49-104">This article help you to understand the common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-to-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="97b49-105">Come acquisire i campi di accesso per un'applicazione</span><span class="sxs-lookup"><span data-stu-id="97b49-105">How to capture sign-in fields for an application</span></span>

<span data-ttu-id="97b49-106">L'acquisizione dei campi di accesso è supportata solo per le pagine di accesso basate su HTML e **non è supportata per le pagine di accesso non standard**, ad esempio le pagine che usano Flash o altre tecnologie non basate su HTML.</span><span class="sxs-lookup"><span data-stu-id="97b49-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="97b49-107">Esistono due modi per acquisire i campi di accesso per le applicazioni personalizzate:</span><span class="sxs-lookup"><span data-stu-id="97b49-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="97b49-108">Acquisizione automatica dei campi di accesso</span><span class="sxs-lookup"><span data-stu-id="97b49-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="97b49-109">Acquisizione manuale dei campi di accesso</span><span class="sxs-lookup"><span data-stu-id="97b49-109">Manual sign-in field capture</span></span>

<span data-ttu-id="97b49-110">L'**acquisizione automatica dei campi di accesso** funziona bene con la maggior parte delle pagine di accesso basate su HTML, se usano **ID DIV noti per il campo di input del nome utente e della password**.</span><span class="sxs-lookup"><span data-stu-id="97b49-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for the username and password input** field.</span></span> <span data-ttu-id="97b49-111">Questo approccio esamina il codice HTML nella pagina alla ricerca di ID DIV che corrispondano ai criteri specifici e salva i metadati per questa applicazione consentendo così di riprodurre le password in momenti successivi.</span><span class="sxs-lookup"><span data-stu-id="97b49-111">The way this works is by scraping the HTML on the page to find DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords to it later.</span></span>

<span data-ttu-id="97b49-112">L'**acquisizione manuale dei campi di accesso** può essere usata nel caso in cui il **fornitore dell'applicazione non etichetti** i campi di input usati per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="97b49-112">**Manual sign-in field capture** can be used in the case that the application **vendor does not label** the input fields used for sign in.</span></span> <span data-ttu-id="97b49-113">L'acquisizione manuale dei campi di accesso può inoltre essere usata nel caso in cui il **fornitore fornisce più campi** che non possono essere rilevati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="97b49-113">Manual sign-in field capture can also be used in the case when the **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="97b49-114">Azure AD può archiviare i dati per tutti i campi presenti nella pagina di accesso purché venga indicato dove si trovano questi campi nella pagina.</span><span class="sxs-lookup"><span data-stu-id="97b49-114">Azure AD can store data for as many fields as are on the sign in page, so long as you tell us where those fields are on the page.</span></span>

<span data-ttu-id="97b49-115">Come regola generale, **se non funziona l'acquisizione automatica dei campi di accesso, è consigliabile provare l'approccio manuale.**</span><span class="sxs-lookup"><span data-stu-id="97b49-115">In general, **if automatic sign-in field capture does not work, we always suggest trying the manual option.**</span></span>

### <a name="how-to-automatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="97b49-116">Come acquisire automaticamente i campi di accesso per un'applicazione</span><span class="sxs-lookup"><span data-stu-id="97b49-116">How to automatically capture sign-in fields for an application</span></span>

<span data-ttu-id="97b49-117">Per configurare l'**accesso Single Sign-On basato su password** per un'applicazione usando l'**acquisizione automatica dei campi di accesso**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="97b49-117">To configure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="97b49-118">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="97b49-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="97b49-119">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="97b49-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="97b49-120">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="97b49-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="97b49-121">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="97b49-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="97b49-122">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="97b49-122">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="97b49-123">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="97b49-123">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="97b49-124">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="97b49-124">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="97b49-125">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="97b49-125">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="97b49-126">Selezionare la modalità **Accesso basato su password**.</span><span class="sxs-lookup"><span data-stu-id="97b49-126">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="97b49-127">Immettere l'**URL di accesso**.</span><span class="sxs-lookup"><span data-stu-id="97b49-127">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="97b49-128">Questo è l'URL in cui gli utenti immettono il nome utente e la password per accedere.</span><span class="sxs-lookup"><span data-stu-id="97b49-128">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="97b49-129">**Assicurarsi che i campi di accesso siano visibili nell'URL fornito**.</span><span class="sxs-lookup"><span data-stu-id="97b49-129">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="97b49-130">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="97b49-130">Click the **Save** button.</span></span>

11. <span data-ttu-id="97b49-131">Dopo questa operazione, dall'URL verrà creata automaticamente una casella di input per nome utente e password e sarà possibile usare Azure AD per la trasmissione sicura delle password all'applicazione tramite l'estensione del browser del pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="97b49-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span>

## <a name="how-to-manually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="97b49-132">Come acquisire manualmente i campi di accesso per un'applicazione</span><span class="sxs-lookup"><span data-stu-id="97b49-132">How to manually capture sign-in fields for an application</span></span>

<span data-ttu-id="97b49-133">Per acquisire manualmente i campi di accesso, è necessario prima di tutto avere installato l'estensione del browser per il pannello di accesso e **non deve essere in esecuzione in modalità privata o in incognito.**</span><span class="sxs-lookup"><span data-stu-id="97b49-133">To manually capture sign in fields, you must first have the Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="97b49-134">Per installare l'estensione del browser, seguire la procedura descritta nella sezione [Come installare l'estensione del browser per il pannello di accesso](#i-cannot-manually-detect-sign-in-fields-for-my-application).</span><span class="sxs-lookup"><span data-stu-id="97b49-134">To install the browser extension, follow the steps in the [How to install the Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="97b49-135">Per configurare l'**accesso Single Sign-On basato su password** per un'applicazione usando l'**acquisizione manuale dei campi di accesso**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="97b49-135">To configure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="97b49-136">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="97b49-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="97b49-137">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="97b49-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="97b49-138">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="97b49-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="97b49-139">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="97b49-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="97b49-140">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="97b49-140">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="97b49-141">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="97b49-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="97b49-142">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="97b49-142">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="97b49-143">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="97b49-143">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="97b49-144">Selezionare la modalità **Accesso basato su password**.</span><span class="sxs-lookup"><span data-stu-id="97b49-144">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="97b49-145">Immettere l'**URL di accesso**.</span><span class="sxs-lookup"><span data-stu-id="97b49-145">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="97b49-146">Questo è l'URL in cui gli utenti immettono il nome utente e la password per accedere.</span><span class="sxs-lookup"><span data-stu-id="97b49-146">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="97b49-147">**Assicurarsi che i campi di accesso siano visibili nell'URL fornito**.</span><span class="sxs-lookup"><span data-stu-id="97b49-147">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="97b49-148">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="97b49-148">Click the **Save** button.</span></span>

11. <span data-ttu-id="97b49-149">Dopo questa operazione, dall'URL verrà creata automaticamente una casella di input per nome utente e password e sarà possibile usare Azure AD per la trasmissione sicura delle password all'applicazione tramite l'estensione del browser del pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="97b49-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span> <span data-ttu-id="97b49-150">Nel caso in cui l'operazione non riesca, è possibile **modificare la modalità di accesso per usare l'acquisizione manuale dei campi di accesso** andando al passaggio 12.</span><span class="sxs-lookup"><span data-stu-id="97b49-150">In the case that this fails, you can **change the sign-in mode to use manual sign-in field capture** by continuing to step 12.</span></span>

12. <span data-ttu-id="97b49-151">Fare clic su **Configura impostazioni Password Single Sign-On per &lt;nomeapp&gt;**.</span><span class="sxs-lookup"><span data-stu-id="97b49-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="97b49-152">Selezionare l'opzione di configurazione **Rileva manualmente i campi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="97b49-152">Select the **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="97b49-153">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="97b49-153">Click **Ok**.</span></span>

15. <span data-ttu-id="97b49-154">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="97b49-154">Click **Save**.</span></span>

16. <span data-ttu-id="97b49-155">Seguire le istruzioni visualizzate per usare il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="97b49-155">Follow the on screen instructions to use the Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="97b49-156">Errore "Non sono stati trovati campi di accesso nell'URL specificato"</span><span class="sxs-lookup"><span data-stu-id="97b49-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="97b49-157">Questo errore viene visualizzato quando il rilevamento automatico dei campi di accesso ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="97b49-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="97b49-158">Per risolvere il problema, provare il rilevamento manuale dei campi di accesso seguendo la procedura descritta nella sezione [Come acquisire manualmente i campi di accesso per un'applicazione](#how-to-manually-capture-sign-in-fields-for-an-application).</span><span class="sxs-lookup"><span data-stu-id="97b49-158">To resolve this issue, try manual sign-in field detection by following the steps in the [How to manually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-to-save-single-sign-on-configuration-error"></a><span data-ttu-id="97b49-159">Errore "Non è possibile salvare la configurazione Single Sign-On"</span><span class="sxs-lookup"><span data-stu-id="97b49-159">I see an “Unable to save Single Sign-on configuration” error</span></span>

<span data-ttu-id="97b49-160">In casi rari, l'aggiornamento della configurazione Single Sign-On può avere esito negativo.</span><span class="sxs-lookup"><span data-stu-id="97b49-160">In certain rare cases, updating the single sign-on configuration can fail.</span></span> <span data-ttu-id="97b49-161">Per risolvere il problema, provare a salvare nuovamente la configurazione Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="97b49-161">TO resolve this try saving the single sign-on configuration again.</span></span>

<span data-ttu-id="97b49-162">Se il problema persiste, aprire un caso di supporto e immettere le informazioni raccolte nelle sezioni[Come visualizzare i dettagli di una notifica del portale](#i-cannot-manually-detect-sign-in-fields-for-my-application) e [Come ottenere assistenza inviando i dettagli di notifica a un tecnico del supporto](#how-to-get-help-by-sending-notification-details-to-a-support-engineer).</span><span class="sxs-lookup"><span data-stu-id="97b49-162">If this continues to fail consistently, open a support case and provide the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="97b49-163">Non è possibile rilevare manualmente i campi di accesso per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="97b49-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="97b49-164">Tra i comportamenti che potrebbero verificarsi quando il rilevamento manuale non funziona sono inclusi i seguenti:</span><span class="sxs-lookup"><span data-stu-id="97b49-164">Some of the behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="97b49-165">È sembrato che il processo di acquisizione manuale funzionasse, ma i campi acquisiti non sono corretti</span><span class="sxs-lookup"><span data-stu-id="97b49-165">The manual capture process appeared to work, but the fields captured were not correct</span></span>

-   <span data-ttu-id="97b49-166">Non vengono evidenziati i campi giusti quando si esegue il processo di acquisizione</span><span class="sxs-lookup"><span data-stu-id="97b49-166">The right fields don’t get highlighted when performing the capture process</span></span>

-   <span data-ttu-id="97b49-167">Il processo di acquisizione indirizza alla pagina di accesso dell'applicazione come previsto, ma non accade nulla</span><span class="sxs-lookup"><span data-stu-id="97b49-167">The capture process takes me to the application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="97b49-168">L'acquisizione manuale sembra funzionare, ma non avviene l'accesso SSO quando gli utenti passano all'applicazione dal pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="97b49-168">Manual capture appears to work, but SSO doesn’t happen when my users navigate to the application from the Access Panel.</span></span>

<span data-ttu-id="97b49-169">Se si verifica uno di questi problemi, verificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="97b49-169">check the following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="97b49-170">Assicurarsi di avere **installato** e **abilitato** la versione più recente dell'estensione del browser del pannello di accesso seguendo la procedura indicata nella sezione [Come installare l'estensione del browser del pannello di accesso](#how-to-install-the-access-panel-browser-extension).</span><span class="sxs-lookup"><span data-stu-id="97b49-170">Ensure that you have the latest version of the access panel browser extension **installed** and **enabled** by following the steps in the [How to install the Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="97b49-171">Non tentare di eseguire il processo di acquisizione mentre il browser è in **modalità privata o in incognito**.</span><span class="sxs-lookup"><span data-stu-id="97b49-171">Ensure that you are not attempting the capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="97b49-172">L'estensione del pannello di accesso non è supportata in queste modalità.</span><span class="sxs-lookup"><span data-stu-id="97b49-172">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="97b49-173">Assicurarsi che gli utenti non stiano tentando di accedere all'applicazione dal pannello di accesso in **modalità privata o in incognito**.</span><span class="sxs-lookup"><span data-stu-id="97b49-173">Ensure that your users are not trying to sign in to the application from the access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="97b49-174">L'estensione del pannello di accesso non è supportata in queste modalità.</span><span class="sxs-lookup"><span data-stu-id="97b49-174">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="97b49-175">Provare di nuovo il processo di acquisizione manuale, assicurarsi che gli indicatori rossi si trovino sui campi corretti.</span><span class="sxs-lookup"><span data-stu-id="97b49-175">Try the manual capture process again, ensuring the red markers are over the correct fields.</span></span>

-   <span data-ttu-id="97b49-176">Se il processo di acquisizione manuale sembra bloccarsi o nella pagina di accesso non esegue alcuna operazione (caso 3 precedente), tentare di eseguirlo nuovamente.</span><span class="sxs-lookup"><span data-stu-id="97b49-176">If the manual capture process seems to hang, or the sign in page doesn’t do anything (case 3 above), try the manual capture process again.</span></span> <span data-ttu-id="97b49-177">Questa volta, tuttavia, al termine del processo, premere il tasto **F12** per aprire la console per sviluppatori del browser.</span><span class="sxs-lookup"><span data-stu-id="97b49-177">But, this time after completing the process, press the **F12** button to open your browser’s developer console.</span></span> <span data-ttu-id="97b49-178">Aprire la **console** e digitare **window.location="&lt;immettere l'URL di accesso specificato durante la configurazione dell'app&gt;"** e quindi premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="97b49-178">Once there, open the **console** and type **window.location=”&lt;enter the sign in url you specified when configuring the app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="97b49-179">Questa operazione forza il reindirizzamento della pagina, termina il processo di acquisizione e memorizza i campi che sono stati acquisiti.</span><span class="sxs-lookup"><span data-stu-id="97b49-179">This force a page redirect which end the capture process and store the fields that have been captured.</span></span>

<span data-ttu-id="97b49-180">Se nessuno di questi approcci risolve il problema, rivolgersi al supporto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="97b49-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="97b49-181">Aprire una richiesta di assistenza con i dettagli delle azioni tentate, nonché le informazioni raccolte nelle sezioni [Come visualizzare i dettagli di una notifica del portale](#i-cannot-manually-detect-sign-in-fields-for-my-application) e [Come ottenere assistenza inviando i dettagli di notifica a un tecnico del supporto](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) (se applicabile).</span><span class="sxs-lookup"><span data-stu-id="97b49-181">Open a support case with the details of what you tried, as well as the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="97b49-182">Come installare l'estensione del browser per il pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="97b49-182">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="97b49-183">Per installare l'estensione del browser per il pannello di accesso, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="97b49-183">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="97b49-184">Aprire il [pannello di accesso](https://myapps.microsoft.com) in uno dei browser supportati e accedere come **utente** ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97b49-184">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="97b49-185">Fare clic su un'**applicazione con accesso SSO basato su password** nel pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="97b49-185">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="97b49-186">Quando viene richiesto di installare il software, selezionare **Installa ora**.</span><span class="sxs-lookup"><span data-stu-id="97b49-186">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="97b49-187">A seconda del browser in uso, si verrà indirizzati al collegamento per il download.</span><span class="sxs-lookup"><span data-stu-id="97b49-187">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="97b49-188">**Aggiungere** l'estensione al browser.</span><span class="sxs-lookup"><span data-stu-id="97b49-188">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="97b49-189">Se richiesto dal browser, scegliere se **abilitare** o **consentire** l'uso dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="97b49-189">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="97b49-190">Al termine dell'installazione, **riavviare** la sessione del browser.</span><span class="sxs-lookup"><span data-stu-id="97b49-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="97b49-191">Accedere al pannello di accesso e verificare se è possibile **avviare** le applicazioni con accesso SSO basato su password.</span><span class="sxs-lookup"><span data-stu-id="97b49-191">Sign in into the Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="97b49-192">È anche possibile scaricare l'estensione per Chrome e Firefox dai collegamenti diretti seguenti:</span><span class="sxs-lookup"><span data-stu-id="97b49-192">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="97b49-193">Estensione Pannello di accesso per Chrome</span><span class="sxs-lookup"><span data-stu-id="97b49-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="97b49-194">Estensione Pannello di accesso per Firefox</span><span class="sxs-lookup"><span data-stu-id="97b49-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="97b49-195">Come visualizzare i dettagli di una notifica del portale</span><span class="sxs-lookup"><span data-stu-id="97b49-195">How to see the details of a portal notification</span></span>

<span data-ttu-id="97b49-196">È possibile visualizzare i dettagli di qualsiasi notifica del portale seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="97b49-196">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="97b49-197">Fare clic sull'icona **Notifiche** (la campanella) nella parte superiore destra del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="97b49-197">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="97b49-198">Selezionare una notifica in uno stato di **Errore** (quelle con accanto un (!) di colore rosso).</span><span class="sxs-lookup"><span data-stu-id="97b49-198">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

  ><span data-ttu-id="97b49-199">!NOTA] Non è possibile fare clic sulle notifiche in uno stato di **Operazione completata** o **In corso**.</span><span class="sxs-lookup"><span data-stu-id="97b49-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="97b49-200">Verrà aperto il pannello **Dettagli notifica**.</span><span class="sxs-lookup"><span data-stu-id="97b49-200">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="97b49-201">Usare queste informazioni per ottenere più dettagli sul problema.</span><span class="sxs-lookup"><span data-stu-id="97b49-201">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="97b49-202">In caso sia ancora necessaria assistenza sul problema, è possibile condividere queste informazioni con un tecnico di supporto o con il gruppo del prodotto.</span><span class="sxs-lookup"><span data-stu-id="97b49-202">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="97b49-203">Fare clic sull'**icona** **Copia** a destra della casella di testo **Copia errore** per copiare tutti i dettagli della notifica da condividere con un tecnico del supporto o con il gruppo del prodotto.</span><span class="sxs-lookup"><span data-stu-id="97b49-203">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="97b49-204">Come ottenere assistenza inviando i dettagli di notifica a un tecnico del supporto</span><span class="sxs-lookup"><span data-stu-id="97b49-204">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="97b49-205">È molto importante condividere **tutti i dettagli elencati di seguito** con un tecnico del supporto per poter ricevere assistenza immediata.</span><span class="sxs-lookup"><span data-stu-id="97b49-205">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="97b49-206">A tale scopo, è possibile **acquisire uno screenshot** o fare clic sull'**icona Copia errore** che si trova a destra della casella di testo **Copia errore**.</span><span class="sxs-lookup"><span data-stu-id="97b49-206">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="97b49-207">Spiegazione dei dettagli della notifica</span><span class="sxs-lookup"><span data-stu-id="97b49-207">Notification Details Explained</span></span>

<span data-ttu-id="97b49-208">La sezione seguente illustra in dettaglio il significato degli elementi della notifica e offre esempi per ognuno di essi.</span><span class="sxs-lookup"><span data-stu-id="97b49-208">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="97b49-209">Elementi essenziali della notifica</span><span class="sxs-lookup"><span data-stu-id="97b49-209">Essential Notification Items</span></span>

-   <span data-ttu-id="97b49-210">**Titolo**: il titolo descrittivo della notifica</span><span class="sxs-lookup"><span data-stu-id="97b49-210">**Title** – the descriptive title of the notification</span></span>

    -   <span data-ttu-id="97b49-211">Esempio: **Impostazioni proxy di applicazione**</span><span class="sxs-lookup"><span data-stu-id="97b49-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="97b49-212">**Descrizione**: la descrizione di ciò che si è verificato a seguito dell'operazione</span><span class="sxs-lookup"><span data-stu-id="97b49-212">**Description** – the description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="97b49-213">Esempio: **L'URL interno immesso è già usato da un'altra applicazione**</span><span class="sxs-lookup"><span data-stu-id="97b49-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="97b49-214">**ID notifica**: l'ID univoco della notifica</span><span class="sxs-lookup"><span data-stu-id="97b49-214">**Notification Id** – the unique id of the notification</span></span>

    -   <span data-ttu-id="97b49-215">Esempio: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="97b49-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="97b49-216">**ID richiesta client**: l'ID specifico della richiesta creato dal browser</span><span class="sxs-lookup"><span data-stu-id="97b49-216">**Client Request Id** – the specific request id made by your browser</span></span>

    -   <span data-ttu-id="97b49-217">Esempio: **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="97b49-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="97b49-218">**Timestamp (UTC)**: il timestamp in cui si è verificata la notifica, basato sul sistema UTC</span><span class="sxs-lookup"><span data-stu-id="97b49-218">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

    -   <span data-ttu-id="97b49-219">Esempio: **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="97b49-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="97b49-220">**ID transazione interna**: l'ID interno che è possibile usare per cercare l'errore nei sistemi</span><span class="sxs-lookup"><span data-stu-id="97b49-220">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

    -   <span data-ttu-id="97b49-221">Esempio: **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="97b49-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="97b49-222">**UPN** : l'utente che ha eseguito l'operazione</span><span class="sxs-lookup"><span data-stu-id="97b49-222">**UPN** – the user who performed the operation</span></span>

    -   <span data-ttu-id="97b49-223">Esempio: **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="97b49-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="97b49-224">**ID tenant**: l'ID univoco del tenant di cui è membro l'utente che ha eseguito l'operazione</span><span class="sxs-lookup"><span data-stu-id="97b49-224">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

    -   <span data-ttu-id="97b49-225">Esempio: **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="97b49-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="97b49-226">**ID oggetto utente**: l'ID univoco dell'utente che ha eseguito l'operazione</span><span class="sxs-lookup"><span data-stu-id="97b49-226">**User object Id** – the unique ID of the user who performed the operation</span></span>

    -   <span data-ttu-id="97b49-227">Esempio: **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="97b49-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="97b49-228">Elementi della notifica dettagliati</span><span class="sxs-lookup"><span data-stu-id="97b49-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="97b49-229">**Nome visualizzato**: **(può essere vuoto)** un nome visualizzato più dettagliato per l'errore</span><span class="sxs-lookup"><span data-stu-id="97b49-229">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

    -   <span data-ttu-id="97b49-230">Esempio*: **impostazioni del proxy di applicazione**</span><span class="sxs-lookup"><span data-stu-id="97b49-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="97b49-231">**Stato**: lo stato specifico della notifica</span><span class="sxs-lookup"><span data-stu-id="97b49-231">**Status** – the specific status of the notification</span></span>

    -   <span data-ttu-id="97b49-232">Esempio*: **Operazione non riuscita**</span><span class="sxs-lookup"><span data-stu-id="97b49-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="97b49-233">**ID oggetto**: **(può essere vuoto)** l'ID dell'oggetto su cui è stata eseguita l'operazione</span><span class="sxs-lookup"><span data-stu-id="97b49-233">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

    -   <span data-ttu-id="97b49-234">Esempio: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="97b49-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="97b49-235">**Dettagli**: la descrizione dettagliata di ciò che si è verificato come conseguenza dell'operazione</span><span class="sxs-lookup"><span data-stu-id="97b49-235">**Details** – the detailed description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="97b49-236">Esempio: **L'URL interno "http://bing.com/" non è valido perché è già in uso**</span><span class="sxs-lookup"><span data-stu-id="97b49-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="97b49-237">**Copia errore**: fare clic sull'**icona Copia** a destra della casella di testo **Copia errore** per copiare tutti i dettagli di notifica da condividere con un tecnico di supporto o con il gruppo del prodotto</span><span class="sxs-lookup"><span data-stu-id="97b49-237">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

    -   <span data-ttu-id="97b49-238">Esempio: ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="97b49-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="97b49-239">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="97b49-239">Next steps</span></span>
[<span data-ttu-id="97b49-240">Fornire l'accesso Single Sign-On alle app con il proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="97b49-240">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

