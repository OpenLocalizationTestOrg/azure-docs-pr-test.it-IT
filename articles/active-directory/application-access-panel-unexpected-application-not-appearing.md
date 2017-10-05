---
title: Un'applicazione assegnata non viene visualizzata nel pannello di accesso | Microsoft Docs
description: Risolvere il problema relativo alla mancata visualizzazione di un'applicazione nel pannello di accesso
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
ms.reviwer: japere
ms.openlocfilehash: 9ea5744d77b90929598ea5feb80c7bbdff3772fc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="an-assigned-application-is-not-appearing-on-the-access-panel"></a><span data-ttu-id="405f8-103">Un'applicazione assegnata non viene visualizzata nel pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="405f8-103">An assigned application is not appearing on the access panel</span></span>

<span data-ttu-id="405f8-104">Il pannello di accesso è un portale basato sul Web che consente a un utente con account aziendale o di istituto di istruzione in Azure Active Directory (Azure AD) di visualizzare e avviare applicazioni basate sul cloud a cui l'amministratore di Azure AD ha concesso l'accesso.</span><span class="sxs-lookup"><span data-stu-id="405f8-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="405f8-105">Queste applicazioni sono configurate per conto dell'utente nel portale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="405f8-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="405f8-106">Perché l'applicazione sia visibile nel pannello di accesso, è necessario che sia configurata correttamente e assegnata all'utente o a un gruppo di cui l'utente è membro.</span><span class="sxs-lookup"><span data-stu-id="405f8-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="405f8-107">Il tipo di app che l'utente può visualizzare rientra nelle categorie seguenti:</span><span class="sxs-lookup"><span data-stu-id="405f8-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="405f8-108">Applicazioni di Office 365</span><span class="sxs-lookup"><span data-stu-id="405f8-108">Office 365 Applications</span></span>

-   <span data-ttu-id="405f8-109">Applicazioni Microsoft e di terze parti configurate con il servizio Single Sign-On basato su federazione</span><span class="sxs-lookup"><span data-stu-id="405f8-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="405f8-110">Applicazioni SSO basate su password</span><span class="sxs-lookup"><span data-stu-id="405f8-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="405f8-111">Applicazioni con soluzioni SSO esistenti</span><span class="sxs-lookup"><span data-stu-id="405f8-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="405f8-112">Problemi generali da verificare per primi</span><span class="sxs-lookup"><span data-stu-id="405f8-112">General issues to check first</span></span>

-   <span data-ttu-id="405f8-113">Se un'applicazione è stata appena aggiunta a un utente, provare ad accedere, a disconnettersi e ad accedere nuovamente al pannello di accesso dell'utente dopo alcuni minuti per vedere se l'applicazione è stata aggiunta.</span><span class="sxs-lookup"><span data-stu-id="405f8-113">If an application was just added to a user, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is added.</span></span>

-   <span data-ttu-id="405f8-114">Se è stata appena rimossa una licenza da un utente o da un gruppo di cui l'utente è membro, l'aggiornamento della visualizzazione potrebbe richiedere molto tempo a seconda delle dimensioni e della complessità del gruppo.</span><span class="sxs-lookup"><span data-stu-id="405f8-114">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="405f8-115">Attendere un tempo più lungo prima di accedere al pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="405f8-115">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-application-configuration"></a><span data-ttu-id="405f8-116">Problemi relativi alla configurazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="405f8-116">Problems related to application configuration</span></span>

<span data-ttu-id="405f8-117">È possibile che un'applicazione non venga visualizzata nel pannello di accesso dell'utente a causa di un'errata configurazione della stessa.</span><span class="sxs-lookup"><span data-stu-id="405f8-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="405f8-118">L'articolo illustra alcuni modi per risolvere i problemi correlati alla configurazione dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="405f8-118">Below are some ways you can troubleshoot issues related to application configuration:</span></span>

-   [<span data-ttu-id="405f8-119">Come configurare l'accesso Single Sign-On federato per un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="405f8-119">How to configure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="405f8-120">Come configurare l'accesso Single Sign-On federato per un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="405f8-120">How to configure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="405f8-121">Come configurare un'applicazione Single Sign-On basato su password per un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="405f8-121">How to configure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="405f8-122">Come configurare un'applicazione Single Sign-On basato password per un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="405f8-122">How to configure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="405f8-123">Come configurare l'accesso Single Sign-On federato per un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="405f8-123">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="405f8-124">Per tutte le applicazioni nella raccolta di Azure AD con funzionalità Enterprise Single Sign-On abilitata è disponibile un'esercitazione dettagliata.</span><span class="sxs-lookup"><span data-stu-id="405f8-124">All applications in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="405f8-125">Per le istruzioni dettagliate, è possibile accedere all'[Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/).</span><span class="sxs-lookup"><span data-stu-id="405f8-125">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="405f8-126">Per configurare un'applicazione della raccolta di Azure AD è necessario:</span><span class="sxs-lookup"><span data-stu-id="405f8-126">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="405f8-127">Aggiungere un'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="405f8-127">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="405f8-128">Configurare i valori dei metadati dell'applicazione in Azure AD (URL di accesso, identificatore, URL di risposta)</span><span class="sxs-lookup"><span data-stu-id="405f8-128">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="405f8-129">Selezionare l'identificatore utente e aggiungere gli attributi utente da inviare all'applicazione</span><span class="sxs-lookup"><span data-stu-id="405f8-129">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="405f8-130">Recuperare il certificato e i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="405f8-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="405f8-131">Configurare i valori dei metadati di Azure AD nell'applicazione (URL di accesso, autorità emittente, URL di disconnessione e certificato)</span><span class="sxs-lookup"><span data-stu-id="405f8-131">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="405f8-132">Aggiungere un'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="405f8-132">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="405f8-133">Per aggiungere un'applicazione dalla raccolta di Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="405f8-133">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-134">Aprire il [portale di Azure](https://portal.azure.com) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="405f8-134">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="405f8-135">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-135">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-136">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-136">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-137">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="405f8-137">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="405f8-138">Fare clic sul pulsante **Aggiungi** nell'angolo superiore destro del pannello **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="405f8-138">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="405f8-139">Nella casella di testo **Immettere un nome** della sezione **Aggiungi dalla raccolta** digitare il nome dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-139">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="405f8-140">Selezionare l'applicazione che si vuole configurare con l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="405f8-140">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="405f8-141">Prima di aggiungere l'applicazione, è possibile modificarne il nome usando la casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="405f8-141">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="405f8-142">Fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-142">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="405f8-143">Dopo un breve periodo di tempo sarà possibile visualizzare il pannello di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-143">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="405f8-144">Configurare l'accesso Single Sign-On per un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="405f8-144">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="405f8-145">Per configurare l'accesso Single Sign-On per un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="405f8-145">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-146">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="405f8-146">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="405f8-147">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-147">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-148">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-148">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-149">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="405f8-149">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="405f8-150">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="405f8-150">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="405f8-151">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="405f8-151">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="405f8-152">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="405f8-152">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="405f8-153">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-153">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="405f8-154">Selezionare **Accesso basato su SAML** dal menu a discesa **Modalità**.</span><span class="sxs-lookup"><span data-stu-id="405f8-154">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="405f8-155">Immettere i valori necessari in **URL e dominio**.</span><span class="sxs-lookup"><span data-stu-id="405f8-155">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="405f8-156">È necessario ottenere questi valori dal fornitore dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-156">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="405f8-157">Per configurare l'applicazione come SSO avviato da provider di servizi, l'URL di accesso è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="405f8-157">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="405f8-158">Per alcune applicazioni, anche l'identificatore è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="405f8-158">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="405f8-159">Per configurare l'applicazione come SSO avviato da IdP, l'URL di risposta è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="405f8-159">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="405f8-160">Per alcune applicazioni, anche l'identificatore è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="405f8-160">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="405f8-161">**Facoltativo:** fare clic su **Mostra impostazioni URL avanzate** se si vuole vedere i valori non obbligatori.</span><span class="sxs-lookup"><span data-stu-id="405f8-161">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="405f8-162">In **Attributi utente** selezionare l'identificatore univoco per gli utenti nel menu a discesa **Identificatore utente**.</span><span class="sxs-lookup"><span data-stu-id="405f8-162">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="405f8-163">**Facoltativo:** fare clic su **Visualizza e modifica tutti gli altri attributi utente** per modificare gli attributi da inviare all'applicazione nel token SAML quando l'utente effettua l'accesso.</span><span class="sxs-lookup"><span data-stu-id="405f8-163">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="405f8-164">Per aggiungere un attributo:</span><span class="sxs-lookup"><span data-stu-id="405f8-164">To add an attribute:</span></span>

   1. <span data-ttu-id="405f8-165">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="405f8-165">click **Add attribute**.</span></span> <span data-ttu-id="405f8-166">Immettere il **Nome** e selezionare il **Valore** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="405f8-166">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="405f8-167">fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="405f8-167">click **Save.**</span></span> <span data-ttu-id="405f8-168">Il nuovo attributo verrà visualizzato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="405f8-168">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="405f8-169">Fare clic su **Configura &lt;nome applicazione&gt;** per accedere alla documentazione che illustra come configurare l'accesso Single Sign-On nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-169">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="405f8-170">Sono inoltre disponibili il certificato e gli URL dei metadati richiesti per configurare l'accesso SSO con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-170">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="405f8-171">fare clic su **Salva** per salvare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-171">click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="405f8-172">Assegnare utenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-172">Assign users to the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="405f8-173">Selezionare l'identificatore utente e aggiungere gli attributi utente da inviare all'applicazione</span><span class="sxs-lookup"><span data-stu-id="405f8-173">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="405f8-174">Per selezionare l'identificatore utente o aggiungere gli attributi dell'utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="405f8-174">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-175">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="405f8-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="405f8-176">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-177">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-178">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="405f8-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="405f8-179">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="405f8-179">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="405f8-180">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="405f8-180">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="405f8-181">Selezionare l'applicazione per cui è stato configurato l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="405f8-181">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="405f8-182">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-182">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="405f8-183">Nella sezione **Attributi utente** selezionare l'identificatore univoco per gli utenti nel menu a discesa **Identificatore utente**.</span><span class="sxs-lookup"><span data-stu-id="405f8-183">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="405f8-184">L'opzione selezionata deve corrispondere al valore previsto nell'applicazione per autenticare l'utente.</span><span class="sxs-lookup"><span data-stu-id="405f8-184">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="405f8-185">Azure AD seleziona il formato per l'attributo NameID (identificatore utente) in base al valore selezionato o al formato richiesto dall'applicazione nell'oggetto AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="405f8-185">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="405f8-186">Per altre informazioni, vedere l'articolo relativo al [protocollo SAML per Single Sign-On](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sotto la sezione NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="405f8-186">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="405f8-187">Per aggiungere gli attributi utente, fare clic su **Visualizza e modifica tutti gli altri attributi utente** per modificare gli attributi da inviare all'applicazione nel token SAML quando l'utente effettua l'accesso.</span><span class="sxs-lookup"><span data-stu-id="405f8-187">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="405f8-188">Per aggiungere un attributo:</span><span class="sxs-lookup"><span data-stu-id="405f8-188">To add an attribute:</span></span>

   1. <span data-ttu-id="405f8-189">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="405f8-189">click **Add attribute**.</span></span> <span data-ttu-id="405f8-190">Immettere il **Nome** e selezionare il **Valore** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="405f8-190">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="405f8-191">fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="405f8-191">click **Save.**</span></span> <span data-ttu-id="405f8-192">Il nuovo attributo è visualizzato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="405f8-192">You will see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="405f8-193">Scaricare il certificato o i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="405f8-193">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="405f8-194">Per scaricare il certificato o i metadati dell'applicazione da Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="405f8-194">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-195">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="405f8-195">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="405f8-196">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-196">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-197">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-197">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-198">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="405f8-198">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="405f8-199">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="405f8-199">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="405f8-200">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="405f8-200">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="405f8-201">Selezionare l'applicazione per cui è stato configurato l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="405f8-201">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="405f8-202">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-202">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="405f8-203">Passare alla sezione **Certificato di firma SAML** e quindi fare clic sul valore della colonna **Download**.</span><span class="sxs-lookup"><span data-stu-id="405f8-203">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="405f8-204">A seconda di quale applicazione richiede la configurazione dell'accesso Single Sign-On, è visibile l'opzione per scaricare il codice XML dei metadati o l'opzione per scaricare il certificato.</span><span class="sxs-lookup"><span data-stu-id="405f8-204">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="405f8-205">Azure AD non fornisce URL per ottenere i metadati.</span><span class="sxs-lookup"><span data-stu-id="405f8-205">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="405f8-206">I metadati possono essere recuperati solo come file XML.</span><span class="sxs-lookup"><span data-stu-id="405f8-206">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="405f8-207">Come configurare l'accesso Single Sign-On federato per un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="405f8-207">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="405f8-208">Per configurare un'applicazione non inclusa nella raccolta, è necessario disporre di Azure AD Premium e l'applicazione deve supportare SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="405f8-208">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="405f8-209">Per altre informazioni sulle versioni di Azure AD, vedere [Prezzi di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="405f8-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="405f8-210">Configurare i valori dei metadati dell'applicazione in Azure AD (URL di accesso, identificatore, URL di risposta)</span><span class="sxs-lookup"><span data-stu-id="405f8-210">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="405f8-211">Selezionare l'identificatore utente e aggiungere gli attributi utente da inviare all'applicazione</span><span class="sxs-lookup"><span data-stu-id="405f8-211">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="405f8-212">Recuperare il certificato e i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="405f8-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="405f8-213">Configurare i valori dei metadati di Azure AD nell'applicazione (URL di accesso, autorità emittente, URL di disconnessione e certificato)</span><span class="sxs-lookup"><span data-stu-id="405f8-213">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="405f8-214">Configurare i valori dei metadati dell'applicazione in Azure AD (URL di accesso, identificatore, URL di risposta)</span><span class="sxs-lookup"><span data-stu-id="405f8-214">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="405f8-215">Per configurare l'accesso Single Sign-On per un'applicazione non inclusa nella raccolta di Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="405f8-215">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-216">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="405f8-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="405f8-217">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-218">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-219">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="405f8-219">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="405f8-220">Fare clic sul pulsante **Aggiungi** nell'angolo superiore destro del pannello **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="405f8-220">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="405f8-221">Fare clic su **Applicazione non nella raccolta** nella sezione **Aggiungi app personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="405f8-221">click **Non-gallery application** in the **Add your own app** section.</span></span>

7.  <span data-ttu-id="405f8-222">Immettere il nome dell'applicazione nella casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="405f8-222">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="405f8-223">Fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-223">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="405f8-224">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-224">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="405f8-225">Selezionare **Accesso basato su SAML** dal menu a discesa **Modalità**.</span><span class="sxs-lookup"><span data-stu-id="405f8-225">Select **SAML-based Sign-on** in the **Mode** dropdown.</span></span>

11. <span data-ttu-id="405f8-226">Immettere i valori necessari in **URL e dominio**.</span><span class="sxs-lookup"><span data-stu-id="405f8-226">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="405f8-227">È necessario ottenere questi valori dal fornitore dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-227">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="405f8-228">Per configurare l'applicazione come SSO avviato da IdP, immettere l'URL di risposta e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="405f8-228">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

   2.  <span data-ttu-id="405f8-229">**Facoltativo:** per configurare l'applicazione come SSO avviato da provider di servizi, l'URL di accesso è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="405f8-229">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="405f8-230">In **Attributi utente** selezionare l'identificatore univoco per gli utenti nel menu a discesa **Identificatore utente**.</span><span class="sxs-lookup"><span data-stu-id="405f8-230">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="405f8-231">**Facoltativo:** fare clic su **Visualizza e modifica tutti gli altri attributi utente** per modificare gli attributi da inviare all'applicazione nel token SAML quando l'utente effettua l'accesso.</span><span class="sxs-lookup"><span data-stu-id="405f8-231">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="405f8-232">Per aggiungere un attributo:</span><span class="sxs-lookup"><span data-stu-id="405f8-232">To add an attribute:</span></span>

   1. <span data-ttu-id="405f8-233">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="405f8-233">click **Add attribute**.</span></span> <span data-ttu-id="405f8-234">Immettere il **Nome** e selezionare il **Valore** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="405f8-234">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="405f8-235">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="405f8-235">Click **Save.**</span></span> <span data-ttu-id="405f8-236">Il nuovo attributo verrà visualizzato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="405f8-236">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="405f8-237">Fare clic su **Configura &lt;nome applicazione&gt;** per accedere alla documentazione che illustra come configurare l'accesso Single Sign-On nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-237">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="405f8-238">Sono inoltre disponibili il certificato e gli URL di Azure AD richiesti per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-238">Also, you has Azure AD URLs and certificate required for the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="405f8-239">Selezionare l'identificatore utente e aggiungere gli attributi utente da inviare all'applicazione</span><span class="sxs-lookup"><span data-stu-id="405f8-239">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="405f8-240">Per selezionare l'identificatore utente o aggiungere gli attributi dell'utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="405f8-240">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-241">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="405f8-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="405f8-242">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-243">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-244">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="405f8-244">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="405f8-245">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="405f8-245">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="405f8-246">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="405f8-246">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="405f8-247">Selezionare l'applicazione per cui è stato configurato l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="405f8-247">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="405f8-248">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-248">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="405f8-249">Nella sezione **Attributi utente** selezionare l'identificatore univoco per gli utenti nel menu a discesa **Identificatore utente**.</span><span class="sxs-lookup"><span data-stu-id="405f8-249">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="405f8-250">L'opzione selezionata deve corrispondere al valore previsto nell'applicazione per autenticare l'utente.</span><span class="sxs-lookup"><span data-stu-id="405f8-250">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="405f8-251">Azure AD seleziona il formato per l'attributo NameID (identificatore utente) in base al valore selezionato o al formato richiesto dall'applicazione nell'oggetto AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="405f8-251">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="405f8-252">Per altre informazioni, vedere l'articolo relativo al [protocollo SAML per Single Sign-On](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sotto la sezione NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="405f8-252">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="405f8-253">Per aggiungere gli attributi utente, fare clic su **Visualizza e modifica tutti gli altri attributi utente** per modificare gli attributi da inviare all'applicazione nel token SAML quando l'utente effettua l'accesso.</span><span class="sxs-lookup"><span data-stu-id="405f8-253">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="405f8-254">Per aggiungere un attributo:</span><span class="sxs-lookup"><span data-stu-id="405f8-254">To add an attribute:</span></span>

   1. <span data-ttu-id="405f8-255">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="405f8-255">click **Add attribute**.</span></span> <span data-ttu-id="405f8-256">Immettere il **Nome** e selezionare il **Valore** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="405f8-256">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="405f8-257">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="405f8-257">Click **Save.**</span></span> <span data-ttu-id="405f8-258">Il nuovo attributo verrà visualizzato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="405f8-258">You see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="405f8-259">Scaricare il certificato o i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="405f8-259">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="405f8-260">Per scaricare il certificato o i metadati dell'applicazione da Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="405f8-260">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-261">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="405f8-261">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="405f8-262">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-262">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-263">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-263">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-264">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="405f8-264">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="405f8-265">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="405f8-265">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="405f8-266">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="405f8-266">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="405f8-267">Selezionare l'applicazione per cui è stato configurato l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="405f8-267">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="405f8-268">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-268">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="405f8-269">Passare alla sezione **Certificato di firma SAML** e quindi fare clic sul valore della colonna **Download**.</span><span class="sxs-lookup"><span data-stu-id="405f8-269">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="405f8-270">A seconda di quale applicazione richiede la configurazione dell'accesso Single Sign-On, è visibile l'opzione per scaricare il codice XML dei metadati o l'opzione per scaricare il certificato.</span><span class="sxs-lookup"><span data-stu-id="405f8-270">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="405f8-271">Azure AD non fornisce URL per ottenere i metadati.</span><span class="sxs-lookup"><span data-stu-id="405f8-271">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="405f8-272">I metadati possono essere recuperati solo come file XML.</span><span class="sxs-lookup"><span data-stu-id="405f8-272">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="405f8-273">Come configurare l'accesso Single Sign-On basato su password per un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="405f8-273">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="405f8-274">Per configurare un'applicazione della raccolta di Azure AD è necessario:</span><span class="sxs-lookup"><span data-stu-id="405f8-274">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="405f8-275">Aggiungere un'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="405f8-275">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="405f8-276">Configurare l'applicazione con l'accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="405f8-276">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="405f8-277">Aggiungere un'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="405f8-277">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="405f8-278">Per aggiungere un'applicazione dalla raccolta di Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="405f8-278">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-279">Aprire il [portale di Azure](https://portal.azure.com) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="405f8-279">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="405f8-280">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-280">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-281">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-281">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-282">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="405f8-282">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="405f8-283">Fare clic sul pulsante **Aggiungi** nell'angolo superiore destro del pannello **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="405f8-283">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="405f8-284">Nella casella di testo **Immettere un nome** della sezione **Aggiungi dalla raccolta** digitare il nome dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-284">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="405f8-285">Selezionare l'applicazione che si vuole configurare con l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="405f8-285">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="405f8-286">Prima di aggiungere l'applicazione, è possibile modificarne il nome usando la casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="405f8-286">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="405f8-287">Fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-287">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="405f8-288">Dopo un breve periodo di tempo sarà possibile visualizzare il pannello di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-288">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="405f8-289">Configurare l'applicazione per un accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="405f8-289">Configure the application for password single sign-on</span></span>

<span data-ttu-id="405f8-290">Per configurare un accesso Single Sign-On per un'applicazione, seguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="405f8-290">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-291">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="405f8-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="405f8-292">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-293">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-294">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="405f8-294">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="405f8-295">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="405f8-295">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="405f8-296">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="405f8-296">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="405f8-297">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="405f8-297">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="405f8-298">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-298">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="405f8-299">Selezionare la modalità **Accesso basato su password**.</span><span class="sxs-lookup"><span data-stu-id="405f8-299">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="405f8-300">[Assegnare gli utenti all'applicazione](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="405f8-300">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="405f8-301">È anche possibile specificare le credenziali per conto dell'utente selezionando le righe degli utenti e facendo clic su **Aggiorna credenziali**, quindi immettendo il nome utente e la password per conto degli utenti.</span><span class="sxs-lookup"><span data-stu-id="405f8-301">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="405f8-302">In caso contrario, verrà richiesto agli utenti di immettere le credenziali all'avvio.</span><span class="sxs-lookup"><span data-stu-id="405f8-302">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="405f8-303">Come configurare l'accesso Single Sign-On basato su password per un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="405f8-303">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="405f8-304">Per configurare un'applicazione della raccolta di Azure AD è necessario:</span><span class="sxs-lookup"><span data-stu-id="405f8-304">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="405f8-305">Aggiungere un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="405f8-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="405f8-306">Configurare l'applicazione per un accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="405f8-306">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="405f8-307">Aggiungere un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="405f8-307">Add a non-gallery application</span></span>

<span data-ttu-id="405f8-308">Per aggiungere un'applicazione dalla raccolta di Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="405f8-308">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-309">Aprire il [portale di Azure](https://portal.azure.com) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="405f8-309">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="405f8-310">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-310">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-311">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-311">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-312">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="405f8-312">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="405f8-313">Fare clic sul pulsante **Aggiungi** nell'angolo superiore destro del pannello **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="405f8-313">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="405f8-314">Fare clic su**Applicazione non nella raccolta**.</span><span class="sxs-lookup"><span data-stu-id="405f8-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="405f8-315">Immettere il nome dell'applicazione nella casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="405f8-315">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="405f8-316">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="405f8-316">Select **Add.**</span></span>

<span data-ttu-id="405f8-317">Dopo un breve periodo di tempo, sarà possibile visualizzare il pannello di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-317">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="405f8-318">Configurare l'applicazione per un accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="405f8-318">Configure the application for password single sign-on</span></span>

<span data-ttu-id="405f8-319">Per configurare un accesso Single Sign-On per un'applicazione, seguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="405f8-319">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-320">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="405f8-320">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="405f8-321">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-321">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-322">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-322">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-323">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="405f8-323">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="405f8-324">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="405f8-324">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="405f8-325">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="405f8-325">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="405f8-326">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="405f8-326">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="405f8-327">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-327">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="405f8-328">Selezionare la modalità **Accesso basato su password**.</span><span class="sxs-lookup"><span data-stu-id="405f8-328">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="405f8-329">Immettere l'**URL di accesso**.</span><span class="sxs-lookup"><span data-stu-id="405f8-329">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="405f8-330">Questo è l'URL in cui gli utenti immettono il nome utente e la password per accedere.</span><span class="sxs-lookup"><span data-stu-id="405f8-330">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="405f8-331">Verificare che i campi di accesso siano visibili nell'URL.</span><span class="sxs-lookup"><span data-stu-id="405f8-331">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="405f8-332">[Assegnare gli utenti all'applicazione](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="405f8-332">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="405f8-333">È anche possibile specificare le credenziali per conto dell'utente selezionando le righe degli utenti e facendo clic su **Aggiorna credenziali**, quindi immettendo il nome utente e la password per conto degli utenti.</span><span class="sxs-lookup"><span data-stu-id="405f8-333">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="405f8-334">In caso contrario, verrà richiesto agli utenti di immettere le credenziali all'avvio.</span><span class="sxs-lookup"><span data-stu-id="405f8-334">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="405f8-335">Problemi relativi all'assegnazione di applicazioni agli utenti</span><span class="sxs-lookup"><span data-stu-id="405f8-335">Problems related to assigning applications to users</span></span>

<span data-ttu-id="405f8-336">Un utente potrebbe non vedere un'applicazione nel pannello di accesso perché non è stato assegnato all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-336">A user may not be seeing an application on their Access Panel because they are not assigned to the application.</span></span> <span data-ttu-id="405f8-337">Alcune procedure per verificare questa situazione sono elencate di seguito:</span><span class="sxs-lookup"><span data-stu-id="405f8-337">Below are some ways to check:</span></span>

-   [<span data-ttu-id="405f8-338">Controllare se un utente è assegnato all'applicazione</span><span class="sxs-lookup"><span data-stu-id="405f8-338">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="405f8-339">Come assegnare un utente direttamente a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="405f8-339">How to assign a user to an application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="405f8-340">Controllare se a un utente è stata assegnata una licenza relativa all'applicazione</span><span class="sxs-lookup"><span data-stu-id="405f8-340">Check if a user is assigned to a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="405f8-341">Come assegnare una licenza a un utente</span><span class="sxs-lookup"><span data-stu-id="405f8-341">How to assign a license to a user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="405f8-342">Controllare se un utente è assegnato all'applicazione</span><span class="sxs-lookup"><span data-stu-id="405f8-342">Check if a user is assigned to the application</span></span>

<span data-ttu-id="405f8-343">Per controllare se un utente è assegnato all'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="405f8-343">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-344">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="405f8-344">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="405f8-345">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-345">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-346">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-346">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-347">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="405f8-347">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="405f8-348">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="405f8-348">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="405f8-349">**Cercare** il nome dell'applicazione in questione.</span><span class="sxs-lookup"><span data-stu-id="405f8-349">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="405f8-350">Fare clic su **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="405f8-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="405f8-351">Controllare se un utente è assegnato all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-351">Check to see if your user is assigned to the application.</span></span>

   * <span data-ttu-id="405f8-352">In caso contrario, seguire la procedura descritta in "Come assegnare un utente direttamente a un'applicazione".</span><span class="sxs-lookup"><span data-stu-id="405f8-352">If not follow the steps in “How to assign a user to an application directly” to do so.</span></span>

### <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="405f8-353">Come assegnare un utente direttamente a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="405f8-353">How to assign a user to an application directly</span></span>

<span data-ttu-id="405f8-354">Per assegnare uno o più utenti direttamente a un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="405f8-354">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-355">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="405f8-355">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="405f8-356">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-356">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-357">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-357">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-358">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="405f8-358">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="405f8-359">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="405f8-359">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="405f8-360">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="405f8-360">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="405f8-361">Selezionare nell'elenco l'applicazione che si vuole assegnare a un utente.</span><span class="sxs-lookup"><span data-stu-id="405f8-361">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="405f8-362">Dopo il caricamento dell'applicazione, fare clic su **Utenti e gruppi** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-362">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="405f8-363">Fare clic sul pulsante **Aggiungi** nella parte superiore dell'elenco **Utenti e gruppi** per aprire il pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="405f8-363">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="405f8-364">Fare clic sul selettore **Utenti e gruppi** nel pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="405f8-364">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="405f8-365">Nella casella di ricerca **Cerca per nome o indirizzo di posta** digitare il **nome completo**  o l'**indirizzo di posta elettronica** dell'utente oggetto dell'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-365">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="405f8-366">Passare il puntatore sull'**utente** nell'elenco per visualizzare una **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="405f8-366">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="405f8-367">Fare clic sulla casella di controllo accanto alla foto o al logo del profilo dell'utente per aggiungere l'utente all'elenco **Selezionato**.</span><span class="sxs-lookup"><span data-stu-id="405f8-367">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="405f8-368">**Facoltativo:** se si vuole **aggiungere più di un utente**, digitare un altro **nome completo** o **indirizzo di posta elettronica** nella casella di ricerca **Cerca per nome o indirizzo di posta** e fare clic sulla casella di controllo per aggiungere l'utente all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="405f8-368">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="405f8-369">Dopo avere selezionato gli utenti, fare clic sul pulsante **Seleziona** per aggiungerli all'elenco di utenti e gruppi da assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-369">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="405f8-370">**Facoltativo:** fare clic sul selettore **Seleziona ruolo** nel pannello **Aggiungi assegnazione** per scegliere un ruolo da assegnare agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="405f8-370">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="405f8-371">Fare clic sul pulsante **Assegna** per assegnare l'applicazione agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="405f8-371">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="405f8-372">Dopo un breve periodo di tempo gli utenti selezionati saranno in grado di avviare queste applicazioni nel pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="405f8-372">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="405f8-373">Controllare se un utente è incluso nella licenza relativa all'applicazione</span><span class="sxs-lookup"><span data-stu-id="405f8-373">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="405f8-374">Per controllare le licenze assegnate a un utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="405f8-374">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-375">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="405f8-375">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="405f8-376">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-376">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-377">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-377">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-378">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-378">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="405f8-379">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="405f8-379">click **All users**.</span></span>

6.  <span data-ttu-id="405f8-380">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="405f8-380">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="405f8-381">Fare clic su **Licenze** per verificare quali licenze sono assegnate all'utente.</span><span class="sxs-lookup"><span data-stu-id="405f8-381">click **Licenses** to see which licenses the user currently has assigned.</span></span>

  * <span data-ttu-id="405f8-382">Se l'utente è assegnato a una licenza Office, le applicazioni Office di Microsoft sono visibili nel pannello di accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="405f8-382">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-user-a-license"></a><span data-ttu-id="405f8-383">Come assegnare una licenza a un utente</span><span class="sxs-lookup"><span data-stu-id="405f8-383">How to assign a user a license</span></span> 

<span data-ttu-id="405f8-384">Per assegnare una licenza a un utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="405f8-384">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-385">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="405f8-385">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="405f8-386">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-386">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-387">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-387">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-388">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-388">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="405f8-389">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="405f8-389">click **All users**.</span></span>

6.  <span data-ttu-id="405f8-390">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="405f8-390">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="405f8-391">Fare clic su **Licenze** per visualizzare le licenze attualmente assegnate all'utente.</span><span class="sxs-lookup"><span data-stu-id="405f8-391">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="405f8-392">Fare clic sul pulsante **Assegna** .</span><span class="sxs-lookup"><span data-stu-id="405f8-392">click the **Assign** button.</span></span>

9.  <span data-ttu-id="405f8-393">Selezionare **uno o più prodotti** nell'elenco dei prodotti disponibili.</span><span class="sxs-lookup"><span data-stu-id="405f8-393">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="405f8-394">**Facoltativo**: fare clic sulla voce **Opzioni di assegnazione** per assegnare in modo granulare i prodotti.</span><span class="sxs-lookup"><span data-stu-id="405f8-394">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="405f8-395">Fare clic su **OK** al termine.</span><span class="sxs-lookup"><span data-stu-id="405f8-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="405f8-396">Fare clic sul pulsante **Assegna** per assegnare queste licenze all'utente.</span><span class="sxs-lookup"><span data-stu-id="405f8-396">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="405f8-397">Problemi relativi all'assegnazione di applicazioni a gruppi</span><span class="sxs-lookup"><span data-stu-id="405f8-397">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="405f8-398">Un utente può visualizzare un'applicazione nel pannello di accesso perché è membro di un gruppo assegnato all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="405f8-399">Alcune procedure per verificare questa situazione sono elencate di seguito:</span><span class="sxs-lookup"><span data-stu-id="405f8-399">Below are some ways to check:</span></span>

-   [<span data-ttu-id="405f8-400">Controllare l'appartenenza a gruppi da parte di un utente</span><span class="sxs-lookup"><span data-stu-id="405f8-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="405f8-401">Come assegnare un'applicazione direttamente a un gruppo</span><span class="sxs-lookup"><span data-stu-id="405f8-401">How to assign an application to a group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="405f8-402">Controllare se un utente è membro di un gruppo assegnato a una licenza</span><span class="sxs-lookup"><span data-stu-id="405f8-402">Check if a user is part of group assigned to a license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="405f8-403">Come assegnare una licenza a un gruppo</span><span class="sxs-lookup"><span data-stu-id="405f8-403">How to assign a license to a group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="405f8-404">Controllare l'appartenenza a gruppi da parte di un utente</span><span class="sxs-lookup"><span data-stu-id="405f8-404">Check a user’s group memberships</span></span>

<span data-ttu-id="405f8-405">Per controllare l'appartenenza a un gruppo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="405f8-405">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-406">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="405f8-406">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="405f8-407">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-407">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-408">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-408">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-409">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-409">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="405f8-410">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="405f8-410">click **All users**.</span></span>

6.  <span data-ttu-id="405f8-411">**Cercare** l'utente interessato e **fare clic sulla relativa riga** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="405f8-411">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="405f8-412">Fare clic su **Gruppi**.</span><span class="sxs-lookup"><span data-stu-id="405f8-412">click **Groups**.</span></span>

8.  <span data-ttu-id="405f8-413">Controllare se un utente è membro di un gruppo assegnato all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-413">Check to see if your user is part of a Group assigned to the application.</span></span>

  * <span data-ttu-id="405f8-414">Se si vuole rimuovere l'utente dal gruppo, **fare clic sulla riga** del gruppo e selezionare Elimina.</span><span class="sxs-lookup"><span data-stu-id="405f8-414">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="how-to-assign-an-application-to-a-group-directly"></a><span data-ttu-id="405f8-415">Come assegnare un'applicazione direttamente a un gruppo</span><span class="sxs-lookup"><span data-stu-id="405f8-415">How to assign an application to a group directly</span></span>

<span data-ttu-id="405f8-416">Per assegnare uno o più gruppi direttamente a un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="405f8-416">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-417">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="405f8-417">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="405f8-418">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-418">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-419">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-419">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-420">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="405f8-420">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="405f8-421">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="405f8-421">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="405f8-422">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="405f8-422">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="405f8-423">Selezionare nell'elenco l'applicazione che si vuole assegnare a un utente.</span><span class="sxs-lookup"><span data-stu-id="405f8-423">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="405f8-424">Dopo il caricamento dell'applicazione, fare clic su **Utenti e gruppi** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-424">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="405f8-425">Fare clic sul pulsante **Aggiungi** nella parte superiore dell'elenco **Utenti e gruppi** per aprire il pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="405f8-425">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="405f8-426">Fare clic sul selettore **Utenti e gruppi** nel pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="405f8-426">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="405f8-427">Nella casella di ricerca **Cerca per nome o indirizzo di posta** digitare il **nome completo del gruppo** a cui si vuole eseguire l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-427">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="405f8-428">Posizionare il puntatore sul **gruppo** nell'elenco per visualizzare una **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="405f8-428">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="405f8-429">Fare clic sulla casella di controllo accanto alla foto o al logo del profilo del gruppo per aggiungere il gruppo all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="405f8-429">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="405f8-430">**Facoltativo:** se si vuole **aggiungere più di un gruppo**, digitare un altro **nome completo di gruppo** nella casella di ricerca **Cerca per nome o indirizzo di posta** e fare clic sulla casella di controllo per aggiungere il gruppo all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="405f8-430">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="405f8-431">Dopo avere selezionato i gruppi, fare clic sul pulsante **Seleziona** per aggiungerli all'elenco di utenti e gruppi da assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-431">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="405f8-432">**Facoltativo:** fare clic sul selettore **Seleziona ruolo** nel pannello **Aggiungi assegnazione** per scegliere un ruolo da assegnare ai gruppi selezionati.</span><span class="sxs-lookup"><span data-stu-id="405f8-432">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="405f8-433">Fare clic sul pulsante **Assegna** per assegnare l'applicazione ai gruppi selezionati.</span><span class="sxs-lookup"><span data-stu-id="405f8-433">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="405f8-434">Dopo un breve periodo di tempo gli utenti selezionati saranno in grado di avviare queste applicazioni nel pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="405f8-434">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-to-a-license"></a><span data-ttu-id="405f8-435">Controllare se un utente è membro di un gruppo assegnato a una licenza</span><span class="sxs-lookup"><span data-stu-id="405f8-435">Check if a user is part of group assigned to a license</span></span>

1.  <span data-ttu-id="405f8-436">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="405f8-436">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="405f8-437">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-437">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-438">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-438">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-439">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-439">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="405f8-440">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="405f8-440">click **All users**.</span></span>

6.  <span data-ttu-id="405f8-441">**Cercare** l'utente interessato e **fare clic sulla relativa riga** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="405f8-441">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="405f8-442">Fare clic su **Gruppi**.</span><span class="sxs-lookup"><span data-stu-id="405f8-442">click **Groups**.</span></span>

8.  <span data-ttu-id="405f8-443">Fare clic sulla riga di un gruppo specifico.</span><span class="sxs-lookup"><span data-stu-id="405f8-443">click the row of a specific group.</span></span>

9.  <span data-ttu-id="405f8-444">Fare clic su **Licenze** per vedere le licenze assegnate al gruppo.</span><span class="sxs-lookup"><span data-stu-id="405f8-444">click **Licenses** to see which licenses the group has assigned to it.</span></span>

   * <span data-ttu-id="405f8-445">Se il gruppo è assegnato a una licenza Office, le applicazioni Office di Microsoft sono visibili nel pannello di accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="405f8-445">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-license-to-a-group"></a><span data-ttu-id="405f8-446">Come assegnare una licenza a un gruppo</span><span class="sxs-lookup"><span data-stu-id="405f8-446">How to assign a license to a group</span></span>

<span data-ttu-id="405f8-447">Per assegnare una licenza a un gruppo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="405f8-447">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="405f8-448">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="405f8-448">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="405f8-449">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="405f8-449">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="405f8-450">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="405f8-450">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="405f8-451">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="405f8-451">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="405f8-452">Fare clic su **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="405f8-452">click **All groups**.</span></span>

6.  <span data-ttu-id="405f8-453">**Cercare** il gruppo desiderato e **fare clic sulla relativa riga** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="405f8-453">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="405f8-454">Fare clic su **Licenze** per visualizzare le licenze attualmente assegnate al gruppo.</span><span class="sxs-lookup"><span data-stu-id="405f8-454">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="405f8-455">Fare clic sul pulsante **Assegna** .</span><span class="sxs-lookup"><span data-stu-id="405f8-455">click the **Assign** button.</span></span>

9.  <span data-ttu-id="405f8-456">Selezionare **uno o più prodotti** nell'elenco dei prodotti disponibili.</span><span class="sxs-lookup"><span data-stu-id="405f8-456">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="405f8-457">**Facoltativo**: fare clic sulla voce **Opzioni di assegnazione** per assegnare in modo granulare i prodotti.</span><span class="sxs-lookup"><span data-stu-id="405f8-457">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="405f8-458">Fare clic su **OK** al termine.</span><span class="sxs-lookup"><span data-stu-id="405f8-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="405f8-459">Fare clic sul pulsante **Assegna** per assegnare queste licenze al gruppo.</span><span class="sxs-lookup"><span data-stu-id="405f8-459">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="405f8-460">L'operazione potrebbe richiedere molto tempo a seconda della dimensione e della complessità del gruppo.</span><span class="sxs-lookup"><span data-stu-id="405f8-460">This may take a long time, depending on the size and complexity of the group.</span></span>

>[!NOTE]
><span data-ttu-id="405f8-461">Per eseguire l'operazione più velocemente, è consigliabile assegnare temporaneamente una licenza direttamente all'utente.</span><span class="sxs-lookup"><span data-stu-id="405f8-461">To do this faster, consider temporarily assigning a license to the user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="405f8-462">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="405f8-462">Next steps</span></span>
[<span data-ttu-id="405f8-463">Aggiungere o modificare utenti in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="405f8-463">Add new users to Azure Active Directory</span></span>](active-directory-users-create-azure-portal.md)

