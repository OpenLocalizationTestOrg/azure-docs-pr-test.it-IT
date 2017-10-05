---
title: Errore nella pagina di un'applicazione dopo l'accesso | Microsoft Docs
description: Come risolvere i problemi di accesso ad Azure AD quando l'applicazione stessa genera un errore
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
ms.openlocfilehash: a8cd93256f79ece268ec3411dfbdf590f4b24447
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="45f35-103">Errore nella pagina di un'applicazione dopo l'accesso</span><span class="sxs-lookup"><span data-stu-id="45f35-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="45f35-104">In questo scenario l'utente ha eseguito l'accesso ad Azure AD, ma l'applicazione visualizza un errore che non consente all'utente di completare correttamente il flusso di accesso.</span><span class="sxs-lookup"><span data-stu-id="45f35-104">In this scenario, Azure AD has signed the user in, but the application is displaying an error not allowing the user to successfully finish the sign in flow.</span></span> <span data-ttu-id="45f35-105">In questo scenario l'applicazione non accetta la risposta di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45f35-105">In this scenario, the application is not accepting the response issue by Azure AD.</span></span>

<span data-ttu-id="45f35-106">Ci sono diversi motivi per cui l'applicazione non ha accettato la risposta di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45f35-106">There are some possible reasons why the application didn’t accept the response from Azure AD.</span></span> <span data-ttu-id="45f35-107">Se l'errore nell'applicazione non è sufficientemente chiaro per capire cosa manca nella risposta, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="45f35-107">If the error in the application is not clear enough to know what is missing in the response, then:</span></span>

-   <span data-ttu-id="45f35-108">Se l'applicazione è la raccolta di Azure AD, verificare di aver seguito tutti i passaggi nell'articolo [Come eseguire il debug di single sign-on basato su SAML per applicazioni in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="45f35-108">If the application is the Azure AD Gallery, verify you have followed all the steps in the article [How to debug SAML-based single sign-on to applications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="45f35-109">Usare uno strumento come [Fiddler](http://www.telerik.com/fiddler) per acquisire la richiesta SAML, la risposta SAML e il token SAML.</span><span class="sxs-lookup"><span data-stu-id="45f35-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) to capture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="45f35-110">Condividere la risposta SAML con il fornitore dell'applicazione per capire cosa manca.</span><span class="sxs-lookup"><span data-stu-id="45f35-110">Share the SAML response with the application vendor to know what is missing.</span></span>

## <a name="missing-attributes-in-the-saml-response"></a><span data-ttu-id="45f35-111">Attributi mancanti nella risposta SAML</span><span class="sxs-lookup"><span data-stu-id="45f35-111">Missing attributes in the SAML response</span></span>

<span data-ttu-id="45f35-112">Per aggiungere un attributo nella configurazione di Azure AD da inviare nella risposta di Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="45f35-112">To add an attribute in the Azure AD configuration to be sent in the Azure AD response, follow the steps below:</span></span>

1.  <span data-ttu-id="45f35-113">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="45f35-113">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="45f35-114">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="45f35-114">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="45f35-115">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="45f35-115">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="45f35-116">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="45f35-116">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="45f35-117">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="45f35-117">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="45f35-118">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="45f35-118">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="45f35-119">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="45f35-119">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="45f35-120">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="45f35-120">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="45f35-121">Fare clic su **Visualizza e modifica tutti gli altri attributi utente** nella sezione **Attributi utente** per modificare gli attributi da inviare all'applicazione nel token SAML quando l'utente esegue l'accesso.</span><span class="sxs-lookup"><span data-stu-id="45f35-121">click **View and edit all other user attributes under** the **User Attributes** section to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="45f35-122">Per aggiungere un attributo:</span><span class="sxs-lookup"><span data-stu-id="45f35-122">To add an attribute:</span></span>

   * <span data-ttu-id="45f35-123">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="45f35-123">click **Add attribute**.</span></span> <span data-ttu-id="45f35-124">Immettere il **Nome** e selezionare il **Valore** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="45f35-124">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   * <span data-ttu-id="45f35-125">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="45f35-125">Click **Save.**</span></span> <span data-ttu-id="45f35-126">Il nuovo attributo verrà visualizzato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="45f35-126">You see the new attribute in the table.</span></span>

9.  <span data-ttu-id="45f35-127">Salvare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="45f35-127">Save the configuration.</span></span>

<span data-ttu-id="45f35-128">Al successivo accesso dell'utente all'applicazione, Azure AD invia il nuovo attributo nella risposta SAML.</span><span class="sxs-lookup"><span data-stu-id="45f35-128">Next time the user signs in to the application, Azure AD send the new attribute in the SAML response.</span></span>

## <a name="the-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="45f35-129">L'applicazione prevede un formato o un valore dell'ID utente diverso</span><span class="sxs-lookup"><span data-stu-id="45f35-129">The application expects a different User Identifier value or format</span></span>

<span data-ttu-id="45f35-130">L'accesso all'applicazione non riesce perché nella risposta SAML mancano attributi come i ruoli o perché l'applicazione prevede un formato diverso per l'attributo EntityID.</span><span class="sxs-lookup"><span data-stu-id="45f35-130">The sign-in to the application is failing because the SAML response is missing attributes such as roles or because the application is expecting a different format for the EntityID attribute.</span></span>

## <a name="add-an-attribute-in-the-azure-ad-application-configuration"></a><span data-ttu-id="45f35-131">Aggiungere un attributo nella configurazione dell'applicazione Azure AD:</span><span class="sxs-lookup"><span data-stu-id="45f35-131">Add an attribute in the Azure AD application configuration:</span></span>

<span data-ttu-id="45f35-132">Per modificare il valore dell'ID utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="45f35-132">To change the User Identifier value, follow the steps below:</span></span>

1.  <span data-ttu-id="45f35-133">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="45f35-133">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="45f35-134">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="45f35-134">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="45f35-135">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="45f35-135">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="45f35-136">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="45f35-136">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="45f35-137">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="45f35-137">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="45f35-138">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="45f35-138">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="45f35-139">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="45f35-139">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="45f35-140">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="45f35-140">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="45f35-141">In **Attributi utente** selezionare l'identificatore univoco per gli utenti nel menu a discesa **Identificatore utente**.</span><span class="sxs-lookup"><span data-stu-id="45f35-141">Under the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="45f35-142">Modificare il formato di EntityID (ID utente)</span><span class="sxs-lookup"><span data-stu-id="45f35-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="45f35-143">Se l'applicazione prevede un altro formato per l'attributo EntityID,</span><span class="sxs-lookup"><span data-stu-id="45f35-143">If the application expects another format for the EntityID attribute.</span></span> <span data-ttu-id="45f35-144">non sarà possibile selezionare il formato di EntityID (ID utente) che Azure AD invia all'applicazione nella risposta dopo l'autenticazione utente.</span><span class="sxs-lookup"><span data-stu-id="45f35-144">Then, you won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="45f35-145">Azure AD seleziona il formato per l'attributo NameID (ID utente) in base al valore selezionato o al formato richiesto dall'applicazione nell'oggetto AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="45f35-145">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="45f35-146">Per altre informazioni, vedere la sezione NameIDPolicy dell'articolo [Protocollo SAML per Single Sign-On](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest).</span><span class="sxs-lookup"><span data-stu-id="45f35-146">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>

## <a name="the-application-expects-a-different-signature-method-for-the-saml-response"></a><span data-ttu-id="45f35-147">L'applicazione prevede un metodo di firma diverso per la risposta SAML</span><span class="sxs-lookup"><span data-stu-id="45f35-147">The application expects a different signature method for the SAML response</span></span>

<span data-ttu-id="45f35-148">Per modificare le parti del token SAML con firma digitale di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="45f35-148">To change what parts of the SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="45f35-149">Attenersi ai passaggi indicati di seguito:</span><span class="sxs-lookup"><span data-stu-id="45f35-149">Follow the steps below:</span></span>

1.  <span data-ttu-id="45f35-150">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="45f35-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="45f35-151">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="45f35-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="45f35-152">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="45f35-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="45f35-153">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="45f35-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="45f35-154">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="45f35-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="45f35-155">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="45f35-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="45f35-156">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="45f35-156">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="45f35-157">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="45f35-157">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="45f35-158">Fare clic su **Mostra impostazioni avanzate per la firma di certificati** nella sezione **Certificato di firma SAML**.</span><span class="sxs-lookup"><span data-stu-id="45f35-158">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="45f35-159">Selezionare un valore appropriato per **Opzione di firma** in base a quanto previsto dall'applicazione:</span><span class="sxs-lookup"><span data-stu-id="45f35-159">Select the appropriate **Signing Option** expected by the application:</span></span>

  * <span data-ttu-id="45f35-160">Firma risposta SAML</span><span class="sxs-lookup"><span data-stu-id="45f35-160">Sign SAML response</span></span>

  * <span data-ttu-id="45f35-161">Firma asserzione e risposta SAML</span><span class="sxs-lookup"><span data-stu-id="45f35-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="45f35-162">Firma asserzione SAML</span><span class="sxs-lookup"><span data-stu-id="45f35-162">Sign SAML assertion</span></span>

<span data-ttu-id="45f35-163">Al successivo accesso dell'utente all'applicazione, Azure AD firma la parte della risposta SAML selezionata.</span><span class="sxs-lookup"><span data-stu-id="45f35-163">Next time the user signs in to the application, Azure AD sign the part of the SAML response selected.</span></span>

## <a name="the-application-expects-the-signing-algorithm-to-be-sha-1"></a><span data-ttu-id="45f35-164">L'applicazione prevede che l'algoritmo di firma sia SHA-1</span><span class="sxs-lookup"><span data-stu-id="45f35-164">The application expects the signing algorithm to be SHA-1</span></span>

<span data-ttu-id="45f35-165">Per impostazione predefinita, Azure AD firma il token SAML usando l'algoritmo più sicuro.</span><span class="sxs-lookup"><span data-stu-id="45f35-165">By default, Azure AD signs the SAML token using the most security algorithm.</span></span> <span data-ttu-id="45f35-166">Non è consigliabile modificare l'algoritmo di firma scegliendo SHA-1, a meno che non sia richiesto dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="45f35-166">Changing the sign algorithm to SHA-1 is not recommended unless required by the application.</span></span>

<span data-ttu-id="45f35-167">Per modificare l'algoritmo di firma, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="45f35-167">To change the signing algorithm, follow the steps below:</span></span>

1.  <span data-ttu-id="45f35-168">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="45f35-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="45f35-169">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="45f35-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="45f35-170">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="45f35-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="45f35-171">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="45f35-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="45f35-172">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="45f35-172">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="45f35-173">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="45f35-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="45f35-174">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="45f35-174">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="45f35-175">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="45f35-175">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="45f35-176">Fare clic su **Mostra impostazioni avanzate per la firma di certificati** nella sezione **Certificato di firma SAML**.</span><span class="sxs-lookup"><span data-stu-id="45f35-176">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="45f35-177">Selezionare SHA-1 in **Algoritmo di firma**.</span><span class="sxs-lookup"><span data-stu-id="45f35-177">Select SHA-1, in the **Signing Algorithm**.</span></span>

<span data-ttu-id="45f35-178">Al successivo accesso dell'utente all'applicazione, Azure AD firma il token SAML usando l'algoritmo SHA-1.</span><span class="sxs-lookup"><span data-stu-id="45f35-178">Next time the user signs in to the application, Azure AD sign the SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45f35-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45f35-179">Next steps</span></span>
[<span data-ttu-id="45f35-180">Come eseguire il debug di single sign-on basato su SAML per applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="45f35-180">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
