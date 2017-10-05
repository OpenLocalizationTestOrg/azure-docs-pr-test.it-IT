---
title: Problemi di accesso a un'applicazione non nella raccolta configurata per il Single Sign-On federato | Microsoft Docs
description: Linee guida per i problemi specifici che possono verificarsi durante l'accesso a un'applicazione configurata per il Single Sign-On federato basato su SAML con Azure AD
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
ms.openlocfilehash: 3afc7bca878caef424d3fa3c64aa17df0fda7de5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-a-non-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="8c561-103">Problemi di accesso a un'applicazione non nella raccolta configurata per il Single Sign-On federato</span><span class="sxs-lookup"><span data-stu-id="8c561-103">Problems signing in to a non-gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="8c561-104">Per risolvere il problema, è necessario verificare la configurazione dell'applicazione in Azure AD come segue:</span><span class="sxs-lookup"><span data-stu-id="8c561-104">To troubleshoot your problem, you need to verify the application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="8c561-105">Assicurarsi di aver seguito tutti i passaggi di configurazione per l'applicazione nella raccolta di AD Azure.</span><span class="sxs-lookup"><span data-stu-id="8c561-105">You have followed all the configuration steps for the Azure AD gallery application.</span></span>

-   <span data-ttu-id="8c561-106">Controllare che l'identificatore e l'URL di risposta configurati in AAD corrispondano ai valori previsti nell'applicazione</span><span class="sxs-lookup"><span data-stu-id="8c561-106">The Identifier and Reply URL configured in AAD match they expected values in the application</span></span>

-   <span data-ttu-id="8c561-107">Verificare che siano stati assegnati utenti all'applicazione</span><span class="sxs-lookup"><span data-stu-id="8c561-107">You have assigned users to the application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="8c561-108">Applicazione non trovata nella directory</span><span class="sxs-lookup"><span data-stu-id="8c561-108">Application not found in directory</span></span>

<span data-ttu-id="8c561-109">*Errore AADSTS70001: applicazione con identificatore 'https://contoso.com' non trovata nella directory*.</span><span class="sxs-lookup"><span data-stu-id="8c561-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in the directory*.</span></span>

<span data-ttu-id="8c561-110">**Causa possibile**</span><span class="sxs-lookup"><span data-stu-id="8c561-110">**Possible cause**</span></span>

<span data-ttu-id="8c561-111">L'attributo Issuer inviato dall'applicazione ad Azure AD nella richiesta SAML non corrisponde al valore di identificatore configurato nell'applicazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c561-111">The Issuer attribute sends from the application to Azure AD in the SAML request doesn’t match the Identifier value configured in the application Azure AD.</span></span>

<span data-ttu-id="8c561-112">**Risoluzione**</span><span class="sxs-lookup"><span data-stu-id="8c561-112">**Resolution**</span></span>

<span data-ttu-id="8c561-113">Assicurarsi che l'attributo Issuer nella richiesta SAML corrisponda al valore di identificatore configurato in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="8c561-113">Ensure that the Issuer attribute in the SAML request it’s matching the Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="8c561-114">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="8c561-114">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="8c561-115">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8c561-115">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8c561-116">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8c561-116">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8c561-117">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8c561-117">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8c561-118">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8c561-118">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="8c561-119">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8c561-119">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="8c561-120">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8c561-120">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="8c561-121">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c561-121">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="8c561-122"><span id="_Hlk477190042" class="anchor"></span>Passare alla sezione **URL e dominio**.</span><span class="sxs-lookup"><span data-stu-id="8c561-122"><span id="_Hlk477190042" class="anchor"></span>Go to **Domain and URLs** section.</span></span> <span data-ttu-id="8c561-123">Verificare che il valore nella casella di testo dell'identificatore corrisponda al valore dell'identificatore visualizzato nel messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="8c561-123">Verify that the value in the Identifier textbox is matching the value for the identifier value displayed in the error.</span></span>

<span data-ttu-id="8c561-124">Dopo aver aggiornato il valore dell'identificatore in Azure AD in modo che corrisponda al valore inviato dall'applicazione nella richiesta SAML, dovrebbe essere possibile accedere all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c561-124">After you have updated the Identifier value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="the-reply-address-does-not-match-the-reply-addresses-configured-for-the-application"></a><span data-ttu-id="8c561-125">L'indirizzo di risposta non corrisponde agli indirizzi di risposta configurati per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c561-125">The reply address does not match the reply addresses configured for the application.</span></span> 

<span data-ttu-id="8c561-126">*Errore AADSTS50011: l'indirizzo di risposta 'https://contoso.com' non corrisponde agli indirizzi risposta configurati per l'applicazione*</span><span class="sxs-lookup"><span data-stu-id="8c561-126">*Error AADSTS50011: The reply address ‘https://contoso.com’ does not match the reply addresses configured for the application*</span></span> 

<span data-ttu-id="8c561-127">**Causa possibile**</span><span class="sxs-lookup"><span data-stu-id="8c561-127">**Possible cause**</span></span> 

<span data-ttu-id="8c561-128">Il valore AssertionConsumerServiceURL nella richiesta SAML non corrisponde al valore o al modello dell'URL di risposta configurato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c561-128">The AssertionConsumerServiceURL value in the SAML request doesn't match the Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="8c561-129">Il valore AssertionConsumerServiceURL nella richiesta SAML è l'URL visualizzato nel messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="8c561-129">The AssertionConsumerServiceURL value in the SAML request is the URL you see in the error.</span></span> 

<span data-ttu-id="8c561-130">**Risoluzione**</span><span class="sxs-lookup"><span data-stu-id="8c561-130">**Resolution**</span></span> 

<span data-ttu-id="8c561-131">Assicurare che il valore AssertionConsumerServiceURL nella richiesta SAML corrisponda al valore dell'URL di risposta configurato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c561-131">Ensure that the AssertionConsumerServiceURL value in the SAML request it's matching the Reply URL value configured in Azure AD.</span></span> 
 
1.  <span data-ttu-id="8c561-132">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="8c561-132">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> 

2.  <span data-ttu-id="8c561-133">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8c561-133">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span> 

3.  <span data-ttu-id="8c561-134">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8c561-134">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span> 

4.  <span data-ttu-id="8c561-135">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8c561-135">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span> 

5.  <span data-ttu-id="8c561-136">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8c561-136">click **All Applications** to view a list of all your applications.</span></span> 

  * <span data-ttu-id="8c561-137">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e      impostare l'opzione **Mostra** su **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="8c561-137">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and       set the **Show** option to **All Applications.**</span></span>
  
6.  <span data-ttu-id="8c561-138">Selezionare l'applicazione per cui si vuole configurare un accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8c561-138">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="8c561-139">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c561-139">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="8c561-140">Passare alla sezione **URL e dominio**.</span><span class="sxs-lookup"><span data-stu-id="8c561-140">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="8c561-141">Verificare o aggiornare il valore nella casella di testo URL di risposta in modo che corrisponda al valore AssertionConsumerServiceURL nella richiesta SAML.</span><span class="sxs-lookup"><span data-stu-id="8c561-141">Verify or update the value in the Reply URL textbox to match the AssertionConsumerServiceURL value in the SAML request.</span></span>

  * <span data-ttu-id="8c561-142">Se non viene visualizzata la casella di testo URL di risposta, selezionare la casella **Mostra impostazioni URL avanzate**.</span><span class="sxs-lookup"><span data-stu-id="8c561-142">If you don't see the Reply URL textbox, select the **Show advanced URL settings** checkbox.</span></span> 

<span data-ttu-id="8c561-143">Dopo aver aggiornato il valore dell'URL di risposta in Azure AD in modo che corrisponda al valore inviato dall'applicazione nella richiesta SAML, dovrebbe essere possibile accedere all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c561-143">After you have updated the Reply URL value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="8c561-144">All'utente non è stato assegnato un ruolo</span><span class="sxs-lookup"><span data-stu-id="8c561-144">User not assigned a role</span></span>

<span data-ttu-id="8c561-145">*Error AADSTS50105: The signed in user 'brian@contoso.com' is not assigned to a role for the application (Errore AADSTS50105: nessun ruolo assegnato all'utente che ha eseguito l'accesso "brian@contoso.com" per l'applicazione)*</span><span class="sxs-lookup"><span data-stu-id="8c561-145">*Error AADSTS50105: The signed in user 'brian@contoso.com' is not assigned to a role for the application*</span></span>

<span data-ttu-id="8c561-146">**Causa possibile**</span><span class="sxs-lookup"><span data-stu-id="8c561-146">**Possible cause**</span></span>

<span data-ttu-id="8c561-147">L'utente non ha ottenuto l'accesso all'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c561-147">The user has not been granted access to the application in Azure AD.</span></span>

<span data-ttu-id="8c561-148">**Risoluzione**</span><span class="sxs-lookup"><span data-stu-id="8c561-148">**Resolution**</span></span>

<span data-ttu-id="8c561-149">Per assegnare uno o più utenti direttamente a un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8c561-149">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="8c561-150">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="8c561-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="8c561-151">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8c561-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8c561-152">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8c561-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8c561-153">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8c561-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8c561-154">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8c561-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="8c561-155">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8c561-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="8c561-156">Selezionare nell'elenco l'applicazione che si vuole assegnare a un utente.</span><span class="sxs-lookup"><span data-stu-id="8c561-156">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="8c561-157">Dopo il caricamento dell'applicazione, fare clic su **Utenti e gruppi** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c561-157">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="8c561-158">Fare clic sul pulsante **Aggiungi** nella parte superiore dell'elenco **Utenti e gruppi** per aprire il pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8c561-158">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="8c561-159">Fare clic sul selettore **Utenti e gruppi** nel pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8c561-159">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="8c561-160">Nella casella di ricerca **Cerca per nome o indirizzo di posta** digitare il **nome completo**  o l'**indirizzo di posta elettronica** dell'utente oggetto dell'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="8c561-160">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="8c561-161">Passare il puntatore sull'**utente** nell'elenco per visualizzare una **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="8c561-161">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="8c561-162">Fare clic sulla casella di controllo accanto alla foto o al logo del profilo dell'utente per aggiungere l'utente all'elenco **Selezionato**.</span><span class="sxs-lookup"><span data-stu-id="8c561-162">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="8c561-163">**Facoltativo:** se si vuole **aggiungere più di un utente**, digitare un altro **nome completo** o **indirizzo di posta elettronica** nella casella di ricerca **Cerca per nome o indirizzo di posta** e fare clic sulla casella di controllo per aggiungere l'utente all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="8c561-163">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="8c561-164">Dopo avere selezionato gli utenti, fare clic sul pulsante **Seleziona** per aggiungerli all'elenco di utenti e gruppi da assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c561-164">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="8c561-165">**Facoltativo:** fare clic sul selettore **Seleziona ruolo** nel pannello **Aggiungi assegnazione** per scegliere un ruolo da assegnare agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="8c561-165">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="8c561-166">Fare clic sul pulsante **Assegna** per assegnare l'applicazione agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="8c561-166">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="8c561-167">Dopo un breve periodo di tempo, gli utenti selezionati potranno avviare queste applicazioni usando i metodi illustrati nella sezione Descrizione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="8c561-167">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="8c561-168">La richiesta non è un messaggio SAML valido</span><span class="sxs-lookup"><span data-stu-id="8c561-168">Not a valid SAML Request</span></span>

<span data-ttu-id="8c561-169">*Error AADSTS75005: The request is not a valid Saml2 protocol message.*(Errore AADSTS75005: la richiesta non è un messaggio del protocollo Saml2 valido).</span><span class="sxs-lookup"><span data-stu-id="8c561-169">*Error AADSTS75005: The request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="8c561-170">**Causa possibile**</span><span class="sxs-lookup"><span data-stu-id="8c561-170">**Possible cause**</span></span>

<span data-ttu-id="8c561-171">Azure AD non supporta la richiesta di SAML inviata dall'applicazione per il Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8c561-171">Azure AD doesn’t support the SAML Request sent by the application for Single Sign-on.</span></span> <span data-ttu-id="8c561-172">Alcuni problemi comuni sono:</span><span class="sxs-lookup"><span data-stu-id="8c561-172">Some common issues are:</span></span>

-   <span data-ttu-id="8c561-173">Campi obbligatori mancanti nella richiesta SAML</span><span class="sxs-lookup"><span data-stu-id="8c561-173">Missing required fields in the SAML request</span></span>

-   <span data-ttu-id="8c561-174">Metodo codificato della richiesta SAML</span><span class="sxs-lookup"><span data-stu-id="8c561-174">SAML request encoded method</span></span>

<span data-ttu-id="8c561-175">**Risoluzione**</span><span class="sxs-lookup"><span data-stu-id="8c561-175">**Resolution**</span></span>

1.  <span data-ttu-id="8c561-176">Acquisire la richiesta SAML.</span><span class="sxs-lookup"><span data-stu-id="8c561-176">Capture SAML request.</span></span> <span data-ttu-id="8c561-177">Per informazioni su come acquisire la richiesta SAML, seguire l'esercitazione [Come eseguire il debug di single sign-on basato su SAML per applicazioni in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="8c561-177">follow the tutorial on [how to debug SAML-based single sign-on to applications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) to learn how to capture the SAML request.</span></span>

2.  <span data-ttu-id="8c561-178">Contattare il fornitore dell'applicazione e condividere:</span><span class="sxs-lookup"><span data-stu-id="8c561-178">Contact the application vendor and share:</span></span>

    -   <span data-ttu-id="8c561-179">Richiesta SAML</span><span class="sxs-lookup"><span data-stu-id="8c561-179">SAML request</span></span>

    -   [<span data-ttu-id="8c561-180">Requisiti del protocollo SAML per Single Sign-On di Azure</span><span class="sxs-lookup"><span data-stu-id="8c561-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="8c561-181">Il fornitore dovrebbe confermare di supportare l'implementazione del protocollo SAML di Azure AD SAML per il Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="8c561-181">They should validate they support the Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="8c561-182">Nessuna risorsa nell'elenco requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="8c561-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="8c561-183">*Error AADSTS65005: The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list. (Errore: l'applicazione client ha richiesto l'accesso alla risorsa '00000002-0000-0000-c000-000000000000'. La richiesta ha avuto esito negativo perché il client non ha specificato questa risorsa nell'elenco requiredResourceAccess)*.</span><span class="sxs-lookup"><span data-stu-id="8c561-183">*Error AADSTS65005: The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="8c561-184">**Causa possibile**</span><span class="sxs-lookup"><span data-stu-id="8c561-184">**Possible cause**</span></span>

<span data-ttu-id="8c561-185">L'oggetto applicazione è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="8c561-185">The application object is corrupted.</span></span>

<span data-ttu-id="8c561-186">**Risoluzione**</span><span class="sxs-lookup"><span data-stu-id="8c561-186">**Resolution**</span></span>

<span data-ttu-id="8c561-187">Per risolvere il problema, rimuovere l'applicazione dalla directory</span><span class="sxs-lookup"><span data-stu-id="8c561-187">To solve the problem, remove the application from the directory.</span></span> <span data-ttu-id="8c561-188">e quindi aggiungerla e riconfigurarla seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8c561-188">Then, add and reconfigure the application, follow the steps below:</span></span>

1.  <span data-ttu-id="8c561-189">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="8c561-189">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="8c561-190">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8c561-190">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8c561-191">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8c561-191">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8c561-192">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8c561-192">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8c561-193">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8c561-193">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="8c561-194">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8c561-194">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="8c561-195">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8c561-195">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="8c561-196">Fare clic su **Elimina** in alto a sinistra del pannello **Panoramica** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c561-196">Click **Delete** at the top-left of the application **Overview** blade.</span></span>

8.  <span data-ttu-id="8c561-197">Aggiornare Azure AD, aggiungere l'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c561-197">Refresh Azure AD and Add the application from the Azure AD gallery.</span></span> <span data-ttu-id="8c561-198">e quindi configurarla di nuovo.</span><span class="sxs-lookup"><span data-stu-id="8c561-198">Then, Configure the application again.</span></span>

<span data-ttu-id="8c561-199">Dopo la riconfigurazione dell'applicazione, dovrebbe essere possibile accedere all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c561-199">After reconfiguring the application, you should be able to sign in to the application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="8c561-200">Chiave o certificato non configurato</span><span class="sxs-lookup"><span data-stu-id="8c561-200">Certificate or key not configured</span></span>

<span data-ttu-id="8c561-201">Error AADSTS50003: No signing key configured (Errore AADSTS50003: nessuna chiave di firma configurata).</span><span class="sxs-lookup"><span data-stu-id="8c561-201">Error AADSTS50003: No signing key configured.</span></span>

<span data-ttu-id="8c561-202">**Causa possibile**</span><span class="sxs-lookup"><span data-stu-id="8c561-202">**Possible cause**</span></span>

<span data-ttu-id="8c561-203">L'oggetto applicazione è danneggiato e Azure AD non riconosce il certificato configurato per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c561-203">The application object is corrupted and Azure AD doesn’t recognize the certificate configured for the application.</span></span>

<span data-ttu-id="8c561-204">**Risoluzione**</span><span class="sxs-lookup"><span data-stu-id="8c561-204">**Resolution**</span></span>

<span data-ttu-id="8c561-205">Per eliminare e creare un nuovo certificato, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8c561-205">To delete and create a new certificate, follow the steps below:</span></span>

1.  <span data-ttu-id="8c561-206">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="8c561-206">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="8c561-207">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8c561-207">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8c561-208">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8c561-208">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8c561-209">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8c561-209">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8c561-210">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8c561-210">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="8c561-211">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8c561-211">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="8c561-212">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8c561-212">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="8c561-213">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8c561-213">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="8c561-214">Nella sezione **Certificato di firma SAML** fare clic su **Crea nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="8c561-214">click **Create new certificate** under the **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="8c561-215">Selezionare la data di scadenza.</span><span class="sxs-lookup"><span data-stu-id="8c561-215">Select Expiration date.</span></span> <span data-ttu-id="8c561-216">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8c561-216">Then, click **Save.**</span></span>

10. <span data-ttu-id="8c561-217">Selezionare l'opzione per **attivare il nuovo certificato** in modo da sostituire il certificato attivo.</span><span class="sxs-lookup"><span data-stu-id="8c561-217">Check **Make new certificate active** to override the active certificate.</span></span> <span data-ttu-id="8c561-218">Fare quindi clic su **Salva** nella parte superiore del pannello e accettare di attivare il certificato di rollover.</span><span class="sxs-lookup"><span data-stu-id="8c561-218">Then, click **Save** at the top of the blade and accept to activate the rollover certificate.</span></span>

11. <span data-ttu-id="8c561-219">Nella sezione **Certificato di firma SAML** selezionare **Rimuovi** per rimuovere il certificato **Inutilizzato**.</span><span class="sxs-lookup"><span data-stu-id="8c561-219">Under the **SAML Signing Certificate** section, click **remove** to remove the **Unused** certificate.</span></span>

## <a name="problem-when-customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="8c561-220">Problema di personalizzazione delle attestazioni SAML inviate a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="8c561-220">Problem when customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="8c561-221">Per informazioni su come personalizzare le attestazioni degli attributi SAML inviate all'applicazione, vedere [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) (Mapping di attestazioni in Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="8c561-221">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c561-222">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8c561-222">Next steps</span></span>
[<span data-ttu-id="8c561-223">Requisiti del protocollo SAML per Single Sign-On di Azure</span><span class="sxs-lookup"><span data-stu-id="8c561-223">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
