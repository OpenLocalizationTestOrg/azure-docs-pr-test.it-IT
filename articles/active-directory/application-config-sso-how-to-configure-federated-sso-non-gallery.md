---
title: Come configurare l'accesso Single Sign-On federato per un'applicazione non inclusa nella raccolta | Microsoft Docs
description: Informazioni su come configurare l'accesso Single Sign-On federato per un'applicazione personalizzata non inclusa nella raccolta e che si intende integrare con Azure AD
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
ms.openlocfilehash: da7bc05c6452cde4d0236806f249559f178dd4e1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="1b9fe-103">Come configurare l'accesso Single Sign-On federato per un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="1b9fe-103">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="1b9fe-104">Per configurare un'applicazione non inclusa nella raccolta, è necessario disporre di Azure AD Premium e l'applicazione deve supportare SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-104">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="1b9fe-105">Per altre informazioni sulle versioni di Azure AD, vedere [Prezzi di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="1b9fe-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="1b9fe-106">Panoramica dei passaggi necessari</span><span class="sxs-lookup"><span data-stu-id="1b9fe-106">Overview of steps required</span></span>
<span data-ttu-id="1b9fe-107">La panoramica di alto livello che segue mostra i passaggi necessari per configurare l'accesso Single Sign-On federato per un'applicazione non inclusa nella raccolta, ad esempio perché personalizzata.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-107">Below is a high level overview of the steps required to configure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="1b9fe-108">Configurare i valori dei metadati dell'applicazione in Azure AD (URL di accesso, identificatore, URL di risposta)</span><span class="sxs-lookup"><span data-stu-id="1b9fe-108">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="1b9fe-109">Selezionare l'identificatore utente e aggiungere gli attributi utente da inviare all'applicazione</span><span class="sxs-lookup"><span data-stu-id="1b9fe-109">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="1b9fe-110">Recuperare il certificato e i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b9fe-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="1b9fe-111">Configurare i valori dei metadati di Azure AD nell'applicazione (URL di accesso, autorità emittente, URL di disconnessione e certificato)</span><span class="sxs-lookup"><span data-stu-id="1b9fe-111">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="1b9fe-112">Assegnare utenti all'applicazione</span><span class="sxs-lookup"><span data-stu-id="1b9fe-112">Assign users to the application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-to-non-gallery-applications"></a><span data-ttu-id="1b9fe-113">Configurazione dell'accesso Single Sign-On per le applicazioni non incluse nella raccolta</span><span class="sxs-lookup"><span data-stu-id="1b9fe-113">Configuring single sign-on to non-gallery applications</span></span>

<span data-ttu-id="1b9fe-114">Per configurare l'accesso Single Sign-On per un'applicazione non inclusa nella raccolta di Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1b9fe-114">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="1b9fe-115">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-115">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1b9fe-116">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-116">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1b9fe-117">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-117">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1b9fe-118">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-118">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1b9fe-119">Fare clic sul pulsante **Aggiungi** nell'angolo superiore destro del pannello **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-119">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="1b9fe-120">Fare clic su **Applicazione non nella raccolta** nella sezione **Aggiungi app personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-120">click **Non-gallery application** in the **Add your own app** section</span></span>

7.  <span data-ttu-id="1b9fe-121">Immettere il nome dell'applicazione nella casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-121">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="1b9fe-122">Fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-122">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="1b9fe-123">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-123">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="1b9fe-124">Selezionare **Accesso basato su SAML** dal menu a discesa **Modalità**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-124">Select **SAML-based Sign-on** in the **Mode** dropdown.</span></span>

11. <span data-ttu-id="1b9fe-125">Immettere i valori necessari in **URL e dominio**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-125">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="1b9fe-126">È necessario ottenere questi valori dal fornitore dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-126">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="1b9fe-127">Per configurare l'applicazione come SSO avviato da IdP, immettere l'URL di risposta e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-127">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

   2. <span data-ttu-id="1b9fe-128">**Facoltativo:** per configurare l'applicazione come SSO avviato da provider di servizi, l'URL di accesso è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-128">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="1b9fe-129">In **Attributi utente** selezionare l'identificatore univoco per gli utenti nel menu a discesa **Identificatore utente**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-129">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="1b9fe-130">**Facoltativo:** fare clic su **Visualizza e modifica tutti gli altri attributi utente** per modificare gli attributi da inviare all'applicazione nel token SAML quando l'utente effettua l'accesso.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-130">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="1b9fe-131">Per aggiungere un attributo:</span><span class="sxs-lookup"><span data-stu-id="1b9fe-131">To add an attribute:</span></span>

   1. <span data-ttu-id="1b9fe-132">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-132">click **Add attribute**.</span></span> <span data-ttu-id="1b9fe-133">Immettere il **Nome** e selezionare il **Valore** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-133">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="1b9fe-134">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-134">Click **Save.**</span></span> <span data-ttu-id="1b9fe-135">Il nuovo attributo verrà visualizzato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-135">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="1b9fe-136">Fare clic su **Configura &lt;nome applicazione&gt;** per accedere alla documentazione che illustra come configurare l'accesso Single Sign-On nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-136">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="1b9fe-137">Sono inoltre disponibili il certificato e gli URL di Azure AD richiesti per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-137">Also, you has Azure AD URLs and certificate required for the application.</span></span>

15. [<span data-ttu-id="1b9fe-138">Assegnare utenti all'applicazione</span><span class="sxs-lookup"><span data-stu-id="1b9fe-138">Assign users to the application.</span></span>](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="1b9fe-139">Selezionare l'identificatore utente e aggiungere gli attributi utente da inviare all'applicazione</span><span class="sxs-lookup"><span data-stu-id="1b9fe-139">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="1b9fe-140">Per selezionare l'identificatore utente o aggiungere gli attributi dell'utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1b9fe-140">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="1b9fe-141">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-141">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1b9fe-142">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-142">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1b9fe-143">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-143">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1b9fe-144">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-144">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1b9fe-145">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-145">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="1b9fe-146">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-146">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1b9fe-147">Selezionare l'applicazione per cui è stato configurato l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-147">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="1b9fe-148">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-148">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1b9fe-149">Nella sezione **Attributi utente** selezionare l'identificatore univoco per gli utenti nel menu a discesa **Identificatore utente**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-149">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="1b9fe-150">L'opzione selezionata deve corrispondere al valore previsto nell'applicazione per autenticare l'utente.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-150">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

 ><span data-ttu-id="1b9fe-151">[!NOTA} Azure AD seleziona il formato per l'attributo NameID (identificatore utente) in base al valore selezionato o al formato richiesto dall'applicazione nell'oggetto AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-151">[!NOTE} Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="1b9fe-152">Per altre informazioni, vedere l'articolo relativo al [protocollo SAML per Single Sign-On](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sotto la sezione NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-152">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="1b9fe-153">Per aggiungere gli attributi utente, fare clic su **Visualizza e modifica tutti gli altri attributi utente** per modificare gli attributi da inviare all'applicazione nel token SAML quando l'utente effettua l'accesso.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-153">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="1b9fe-154">Per aggiungere un attributo:</span><span class="sxs-lookup"><span data-stu-id="1b9fe-154">To add an attribute:</span></span>

   1. <span data-ttu-id="1b9fe-155">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-155">click **Add attribute**.</span></span> <span data-ttu-id="1b9fe-156">Immettere il **Nome** e selezionare il **Valore** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-156">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="1b9fe-157">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-157">Click **Save.**</span></span> <span data-ttu-id="1b9fe-158">Il nuovo attributo verrà visualizzato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-158">You see the new attribute in the table.</span></span>

## <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="1b9fe-159">Scaricare il certificato o i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b9fe-159">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="1b9fe-160">Per scaricare il certificato o i metadati dell'applicazione da Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1b9fe-160">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="1b9fe-161">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-161">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1b9fe-162">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-162">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1b9fe-163">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-163">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1b9fe-164">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-164">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1b9fe-165">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-165">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="1b9fe-166">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-166">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1b9fe-167">Selezionare l'applicazione per cui è stato configurato l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-167">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="1b9fe-168">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-168">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1b9fe-169">Passare alla sezione **Certificato di firma SAML** e quindi fare clic sul valore della colonna **Download**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-169">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="1b9fe-170">A seconda di quale applicazione richiede la configurazione dell'accesso Single Sign-On, è visibile l'opzione per scaricare il codice XML dei metadati o l'opzione per scaricare il certificato.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-170">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="1b9fe-171">Azure AD non fornisce URL per ottenere i metadati.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-171">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="1b9fe-172">I metadati possono essere recuperati solo come file XML.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-172">The metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-to-the-application"></a><span data-ttu-id="1b9fe-173">Assegnare utenti all'applicazione</span><span class="sxs-lookup"><span data-stu-id="1b9fe-173">Assign users to the application</span></span>

<span data-ttu-id="1b9fe-174">Per assegnare uno o più utenti direttamente a un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1b9fe-174">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="1b9fe-175">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1b9fe-176">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1b9fe-177">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1b9fe-178">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1b9fe-179">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-179">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="1b9fe-180">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-180">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1b9fe-181">Selezionare nell'elenco l'applicazione che si vuole assegnare a un utente.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-181">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="1b9fe-182">Dopo il caricamento dell'applicazione, fare clic su **Utenti e gruppi** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-182">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1b9fe-183">Fare clic sul pulsante **Aggiungi** nella parte superiore dell'elenco **Utenti e gruppi** per aprire il pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-183">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="1b9fe-184">Fare clic sul selettore **Utenti e gruppi** nel pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-184">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="1b9fe-185">Nella casella di ricerca **Cerca per nome o indirizzo di posta** digitare il **nome completo**  o l'**indirizzo di posta elettronica** dell'utente oggetto dell'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-185">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="1b9fe-186">Passare il puntatore sull'**utente** nell'elenco per visualizzare una **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-186">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="1b9fe-187">Fare clic sulla casella di controllo accanto alla foto o al logo del profilo dell'utente per aggiungere l'utente all'elenco **Selezionato**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-187">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="1b9fe-188">**Facoltativo:** se si vuole **aggiungere più di un utente**, digitare un altro **nome completo** o **indirizzo di posta elettronica** nella casella di ricerca **Cerca per nome o indirizzo di posta** e fare clic sulla casella di controllo per aggiungere l'utente all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-188">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="1b9fe-189">Dopo avere selezionato gli utenti, fare clic sul pulsante **Seleziona** per aggiungerli all'elenco di utenti e gruppi da assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-189">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="1b9fe-190">**Facoltativo:** fare clic sul selettore **Seleziona ruolo** nel pannello **Aggiungi assegnazione** per scegliere un ruolo da assegnare agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-190">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="1b9fe-191">Fare clic sul pulsante **Assegna** per assegnare l'applicazione agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-191">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="1b9fe-192">Dopo un breve periodo di tempo, gli utenti selezionati potranno avviare queste applicazioni usando i metodi illustrati nella sezione Descrizione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="1b9fe-192">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="1b9fe-193">Personalizzazione delle attestazioni SAML inviate a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="1b9fe-193">Customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="1b9fe-194">Per informazioni su come personalizzare le attestazioni degli attributi SAML inviate all'applicazione, vedere [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) (Mapping di attestazioni in Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1b9fe-194">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b9fe-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1b9fe-195">Next steps</span></span>
[<span data-ttu-id="1b9fe-196">Fornire l'accesso Single Sign-On alle app con il proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="1b9fe-196">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
