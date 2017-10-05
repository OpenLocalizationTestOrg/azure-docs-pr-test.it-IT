---
title: Come configurare l'accesso Single Sign-On federato per un'applicazione della raccolta di Azure AD | Microsoft Docs
description: Informazioni su come configurare l'accesso Single Sign-On federato per un'applicazione nella raccolta di Azure AD e usare le esercitazioni per eseguire l'operazione rapidamente
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
ms.openlocfilehash: 1b1d00718981b2c7d11f5b88428d02e16dd0b34d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="b88f2-103">Come configurare l'accesso Single Sign-On federato per un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b88f2-103">How to configure federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="b88f2-104">Per tutte le applicazioni nella raccolta di Azure AD con funzionalità Enterprise Single Sign-On abilitata è disponibile un'esercitazione dettagliata.</span><span class="sxs-lookup"><span data-stu-id="b88f2-104">All applications in the Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="b88f2-105">Per le istruzioni dettagliate, è possibile accedere all'[Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/).</span><span class="sxs-lookup"><span data-stu-id="b88f2-105">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="b88f2-106">Panoramica dei passaggi necessari</span><span class="sxs-lookup"><span data-stu-id="b88f2-106">Overview of steps required</span></span>
<span data-ttu-id="b88f2-107">Per configurare un'applicazione della raccolta di Azure AD è necessario:</span><span class="sxs-lookup"><span data-stu-id="b88f2-107">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="b88f2-108">Aggiungere un'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b88f2-108">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="b88f2-109">Configurare i valori dei metadati dell'applicazione in Azure AD (URL di accesso, identificatore, URL di risposta)</span><span class="sxs-lookup"><span data-stu-id="b88f2-109">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="b88f2-110">Selezionare l'identificatore utente e aggiungere gli attributi utente da inviare all'applicazione</span><span class="sxs-lookup"><span data-stu-id="b88f2-110">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="b88f2-111">Recuperare il certificato e i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b88f2-111">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="b88f2-112">Configurare i valori dei metadati di Azure AD nell'applicazione (URL di accesso, autorità emittente, URL di disconnessione e certificato)</span><span class="sxs-lookup"><span data-stu-id="b88f2-112">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="b88f2-113">Assegnare utenti all'applicazione</span><span class="sxs-lookup"><span data-stu-id="b88f2-113">Assign users to the application</span></span>](#assign-users-to-the-application)

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="b88f2-114">Aggiungere un'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b88f2-114">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="b88f2-115">Per aggiungere un'applicazione dalla raccolta di Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b88f2-115">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="b88f2-116">Aprire il [portale di Azure](https://portal.azure.com) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-116">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="b88f2-117">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b88f2-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b88f2-118">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b88f2-119">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b88f2-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b88f2-120">Fare clic sul pulsante **Aggiungi** nell'angolo superiore destro del pannello **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-120">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="b88f2-121">Nella casella di testo **Immettere un nome** della sezione **Aggiungi dalla raccolta** digitare il nome dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b88f2-121">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="b88f2-122">Selezionare l'applicazione che si vuole configurare con l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b88f2-122">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="b88f2-123">Prima di aggiungere l'applicazione, è possibile modificarne il nome usando la casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-123">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="b88f2-124">Fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b88f2-124">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="b88f2-125">Dopo un breve periodo di tempo sarà possibile visualizzare il pannello di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b88f2-125">After a short period of time, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="b88f2-126">Configurare l'accesso Single Sign-On per un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b88f2-126">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="b88f2-127">Per configurare l'accesso Single Sign-On per un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b88f2-127">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="b88f2-128">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-128">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="b88f2-129">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b88f2-129">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b88f2-130">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-130">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b88f2-131">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b88f2-131">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b88f2-132">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b88f2-132">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="b88f2-133">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-133">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b88f2-134">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b88f2-134">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="b88f2-135">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b88f2-135">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b88f2-136">Selezionare **Accesso basato su SAML** dal menu a discesa **Modalità**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-136">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="b88f2-137">Immettere i valori necessari in **URL e dominio**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-137">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="b88f2-138">È necessario ottenere questi valori dal fornitore dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b88f2-138">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="b88f2-139">Per configurare l'applicazione come SSO avviato da provider di servizi, l'URL di accesso è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b88f2-139">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="b88f2-140">Per alcune applicazioni, anche l'identificatore è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b88f2-140">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="b88f2-141">Per configurare l'applicazione come SSO avviato da IdP, l'URL di risposta è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b88f2-141">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="b88f2-142">Per alcune applicazioni, anche l'identificatore è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b88f2-142">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="b88f2-143">**Facoltativo:** fare clic su **Mostra impostazioni URL avanzate** se si vuole vedere i valori non obbligatori.</span><span class="sxs-lookup"><span data-stu-id="b88f2-143">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="b88f2-144">In **Attributi utente** selezionare l'identificatore univoco per gli utenti nel menu a discesa **Identificatore utente**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-144">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="b88f2-145">**Facoltativo:** fare clic su **Visualizza e modifica tutti gli altri attributi utente** per modificare gli attributi da inviare all'applicazione nel token SAML quando l'utente effettua l'accesso.</span><span class="sxs-lookup"><span data-stu-id="b88f2-145">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

  <span data-ttu-id="b88f2-146">Per aggiungere un attributo:</span><span class="sxs-lookup"><span data-stu-id="b88f2-146">To add an attribute:</span></span>
   
   1. <span data-ttu-id="b88f2-147">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-147">click **Add attribute**.</span></span> <span data-ttu-id="b88f2-148">Immettere il **Nome** e selezionare il **Valore** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="b88f2-148">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   1. <span data-ttu-id="b88f2-149">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-149">Click **Save.**</span></span> <span data-ttu-id="b88f2-150">Il nuovo attributo verrà visualizzato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="b88f2-150">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="b88f2-151">Fare clic su **Configura &lt;nome applicazione&gt;** per accedere alla documentazione che illustra come configurare l'accesso Single Sign-On nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b88f2-151">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="b88f2-152">Sono inoltre disponibili il certificato e gli URL dei metadati richiesti per configurare l'accesso SSO con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b88f2-152">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="b88f2-153">Fare clic su **Salva** per salvare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="b88f2-153">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="b88f2-154">Assegnare utenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b88f2-154">Assign users to the application.</span></span>

## <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="b88f2-155">Selezionare l'identificatore utente e aggiungere gli attributi utente da inviare all'applicazione</span><span class="sxs-lookup"><span data-stu-id="b88f2-155">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="b88f2-156">Per selezionare l'identificatore utente o aggiungere gli attributi dell'utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b88f2-156">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="b88f2-157">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-157">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b88f2-158">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b88f2-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b88f2-159">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b88f2-160">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b88f2-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b88f2-161">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b88f2-161">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="b88f2-162">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-162">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b88f2-163">Selezionare l'applicazione per cui è stato configurato l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b88f2-163">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b88f2-164">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b88f2-164">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b88f2-165">Nella sezione **Attributi utente** selezionare l'identificatore univoco per gli utenti nel menu a discesa **Identificatore utente**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-165">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="b88f2-166">L'opzione selezionata deve corrispondere al valore previsto nell'applicazione per autenticare l'utente.</span><span class="sxs-lookup"><span data-stu-id="b88f2-166">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

  >[!NOTE] 
  ><span data-ttu-id="b88f2-167">Azure AD seleziona il formato per l'attributo NameID (identificatore utente) in base al valore selezionato o al formato richiesto dall'applicazione nell'oggetto AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="b88f2-167">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="b88f2-168">Per altre informazioni, vedere l'articolo relativo al [protocollo SAML per Single Sign-On](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sotto la sezione NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="b88f2-168">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
  >
  >

9.  <span data-ttu-id="b88f2-169">Per aggiungere gli attributi utente, fare clic su **Visualizza e modifica tutti gli altri attributi utente** per modificare gli attributi da inviare all'applicazione nel token SAML quando l'utente effettua l'accesso.</span><span class="sxs-lookup"><span data-stu-id="b88f2-169">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="b88f2-170">Per aggiungere un attributo:</span><span class="sxs-lookup"><span data-stu-id="b88f2-170">To add an attribute:</span></span>
  
   1. <span data-ttu-id="b88f2-171">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-171">click **Add attribute**.</span></span> <span data-ttu-id="b88f2-172">Immettere il **Nome** e selezionare il **Valore** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="b88f2-172">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="b88f2-173">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-173">Click **Save**.</span></span> <span data-ttu-id="b88f2-174">Il nuovo attributo verrà visualizzato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="b88f2-174">You see the new attribute in the table.</span></span>

## <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="b88f2-175">Scaricare il certificato o i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b88f2-175">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="b88f2-176">Per scaricare il certificato o i metadati dell'applicazione da Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b88f2-176">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="b88f2-177">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-177">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b88f2-178">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b88f2-178">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b88f2-179">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-179">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b88f2-180">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b88f2-180">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b88f2-181">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b88f2-181">click **All Applications** to view a list of all your applications.</span></span>

  *  <span data-ttu-id="b88f2-182">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-182">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications**.</span></span>

6.  <span data-ttu-id="b88f2-183">Selezionare l'applicazione per cui è stato configurato l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b88f2-183">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b88f2-184">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b88f2-184">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b88f2-185">Passare alla sezione **Certificato di firma SAML** e quindi fare clic sul valore della colonna **Download**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-185">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="b88f2-186">A seconda di quale applicazione richiede la configurazione dell'accesso Single Sign-On, è visibile l'opzione per scaricare il codice XML dei metadati o l'opzione per scaricare il certificato.</span><span class="sxs-lookup"><span data-stu-id="b88f2-186">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="b88f2-187">Azure AD non fornisce URL per ottenere i metadati.</span><span class="sxs-lookup"><span data-stu-id="b88f2-187">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="b88f2-188">I metadati possono essere recuperati solo come file XML.</span><span class="sxs-lookup"><span data-stu-id="b88f2-188">The metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-to-the-application"></a><span data-ttu-id="b88f2-189">Assegnare utenti all'applicazione</span><span class="sxs-lookup"><span data-stu-id="b88f2-189">Assign users to the application</span></span>

<span data-ttu-id="b88f2-190">Per assegnare uno o più utenti direttamente a un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b88f2-190">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="b88f2-191">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-191">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b88f2-192">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b88f2-192">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b88f2-193">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-193">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b88f2-194">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b88f2-194">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b88f2-195">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b88f2-195">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="b88f2-196">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-196">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b88f2-197">Selezionare nell'elenco l'applicazione che si vuole assegnare a un utente.</span><span class="sxs-lookup"><span data-stu-id="b88f2-197">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="b88f2-198">Dopo il caricamento dell'applicazione, fare clic su **Utenti e gruppi** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b88f2-198">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b88f2-199">Fare clic sul pulsante **Aggiungi** nella parte superiore dell'elenco **Utenti e gruppi** per aprire il pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-199">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="b88f2-200">Fare clic sul selettore **Utenti e gruppi** nel pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-200">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="b88f2-201">Nella casella di ricerca **Cerca per nome o indirizzo di posta** digitare il **nome completo**  o l'**indirizzo di posta elettronica** dell'utente oggetto dell'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="b88f2-201">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="b88f2-202">Passare il puntatore sull'**utente** nell'elenco per visualizzare una **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-202">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="b88f2-203">Fare clic sulla casella di controllo accanto alla foto o al logo del profilo dell'utente per aggiungere l'utente all'elenco **Selezionato**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-203">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="b88f2-204">**Facoltativo:** se si vuole **aggiungere più di un utente**, digitare un altro **nome completo** o **indirizzo di posta elettronica** nella casella di ricerca **Cerca per nome o indirizzo di posta** e fare clic sulla casella di controllo per aggiungere l'utente all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="b88f2-204">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="b88f2-205">Dopo avere selezionato gli utenti, fare clic sul pulsante **Seleziona** per aggiungerli all'elenco di utenti e gruppi da assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b88f2-205">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="b88f2-206">**Facoltativo:** fare clic sul selettore **Seleziona ruolo** nel pannello **Aggiungi assegnazione** per scegliere un ruolo da assegnare agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="b88f2-206">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="b88f2-207">Fare clic sul pulsante **Assegna** per assegnare l'applicazione agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="b88f2-207">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="b88f2-208">Dopo un breve periodo di tempo, gli utenti selezionati potranno avviare queste applicazioni usando i metodi illustrati nella sezione Descrizione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="b88f2-208">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="b88f2-209">Personalizzazione delle attestazioni SAML inviate a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="b88f2-209">Customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="b88f2-210">Per informazioni su come personalizzare le attestazioni degli attributi SAML inviate all'applicazione, vedere [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) (Mapping di attestazioni in Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="b88f2-210">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b88f2-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b88f2-211">Next steps</span></span>
[<span data-ttu-id="b88f2-212">Fornire l'accesso Single Sign-On alle app con il proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="b88f2-212">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)



