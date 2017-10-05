---
title: Problema nella configurazione dell'accesso Single Sign-On federato per un'applicazione nella raccolta di Azure AD | Microsoft Docs
description: Informazioni sui problemi comuni che si possono incontrare durante la configurazione dell'accesso Single Sign-On federato per applicazioni SAML incluse nella raccolta delle applicazioni di Azure AD
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
ms.openlocfilehash: 290ca66048281de5e031b0404919bed84ab19ffa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="4a5d2-103">Problema nella configurazione dell'accesso Single Sign-On federato per un'applicazione nella raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a5d2-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="4a5d2-104">Se si verifica un problema durante la configurazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="4a5d2-105">Verificare di aver seguito tutti i passaggi dell'esercitazione per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-105">Verify you have followed all the steps in the tutorial for the application.</span></span> <span data-ttu-id="4a5d2-106">Durante la configurazione dell'applicazione è disponibile la documentazione in linea relativa a come configurare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-106">In the application’s configuration, you have inline documentation on how to configure the application.</span></span> <span data-ttu-id="4a5d2-107">Per le istruzioni dettagliate, è possibile accedere all'[Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/).</span><span class="sxs-lookup"><span data-stu-id="4a5d2-107">Also, you can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="4a5d2-108">Impossibile aggiungere un'altra istanza dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="4a5d2-108">Can’t add another instance of the application</span></span>

<span data-ttu-id="4a5d2-109">Per aggiungere una seconda istanza di un'applicazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="4a5d2-109">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="4a5d2-110">Configurare un identificatore univoco per la seconda istanza.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-110">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="4a5d2-111">Non è possibile configurare lo stesso identificatore usato per la prima istanza.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-111">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="4a5d2-112">Configurare un certificato diverso da quello usato per la prima istanza.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-112">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="4a5d2-113">Se l'applicazione non supporta alcuna delle operazioni sopra indicate,</span><span class="sxs-lookup"><span data-stu-id="4a5d2-113">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="4a5d2-114">non è possibile configurare una seconda istanza.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-114">Then, you won’t be able to configure a second instance.</span></span>

## <a name="cant-add-the-identifier-or-the-reply-url"></a><span data-ttu-id="4a5d2-115">Impossibile aggiungere l'identificatore o l'URL di risposta</span><span class="sxs-lookup"><span data-stu-id="4a5d2-115">Can’t add the Identifier or the Reply URL</span></span>

<span data-ttu-id="4a5d2-116">Se non è possibile configurare l'identificatore o l'URL di risposta, verificare che i valori dell'identificatore e dell'URL di risposta corrispondano ai modelli preconfigurati per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-116">If you’re not able to configure the Identifier or the Reply URL, confirm the Identifier and Reply URL values match the patterns pre-configured for the application.</span></span>

<span data-ttu-id="4a5d2-117">Per conoscere i modelli preconfigurati per l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="4a5d2-117">To know the patterns pre-configured for the application:</span></span>

1.  <span data-ttu-id="4a5d2-118">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> <span data-ttu-id="4a5d2-119">Andare al passaggio 7.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-119">Go to step 7.</span></span> <span data-ttu-id="4a5d2-120">Se si è già nel pannello di configurazione dell'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-120">If you are already in the application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="4a5d2-121">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-121">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4a5d2-122">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-122">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4a5d2-123">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-123">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4a5d2-124">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-124">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="4a5d2-125">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-125">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4a5d2-126">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-126">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4a5d2-127">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-127">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4a5d2-128">Selezionare **Accesso basato su SAML** dal menu a discesa **Modalità**.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-128">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="4a5d2-129">Passare alla casella di testo **Identificatore** o **URL di risposta** nella sezione **URL e dominio**.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-129">Go to the **Identifier** or **Reply URL** textbox, under the **Domain and URLs section.**</span></span>

10. <span data-ttu-id="4a5d2-130">Esistono tre modi per conoscere i modelli supportati per l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="4a5d2-130">There are three ways to know the supported patterns for the application:</span></span>

   * <span data-ttu-id="4a5d2-131">Nella casella di testo è presente il modello supportato come segnaposto, *esempio:* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-131">In the textbox, you see the supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="4a5d2-132">Se il modello non è supportato, viene visualizzato un punto esclamativo rosso quando si tenta di immettere il valore nella casella di testo.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-132">if the pattern is not supported, you see a red exclamation mark when you try to enter the value in the textbox.</span></span> <span data-ttu-id="4a5d2-133">Se si posiziona il mouse sul punto esclamativo rosso, vengono visualizzati i modelli supportati.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-133">If you hover your mouse over the red exclamation mark, you see the supported patterns.</span></span>

   * <span data-ttu-id="4a5d2-134">Nell'esercitazione per l'applicazione sono disponibili anche informazioni sui modelli supportati.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-134">In the tutorial for the application, you can also get information about the supported patterns.</span></span> <span data-ttu-id="4a5d2-135">Nella sezione **Configurare il Single Sign-On di Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-135">Under the **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="4a5d2-136">Andare al passaggio per configurare i valori nella sezione **URL e dominio**.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-136">Go to the step for configured the values under the **Domain and URLs** section.</span></span>

<span data-ttu-id="4a5d2-137">Se i valori non corrispondono ai modelli preconfigurati in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-137">If the values don’t match with the patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="4a5d2-138">È possibile:</span><span class="sxs-lookup"><span data-stu-id="4a5d2-138">You can:</span></span>

-   <span data-ttu-id="4a5d2-139">Chiedere al fornitore dell'applicazione valori che corrispondono al modello preconfigurato in Azure AD</span><span class="sxs-lookup"><span data-stu-id="4a5d2-139">Work with the application vendor to get values that match the pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="4a5d2-140">Contattare, in alternativa, il team di Azure AD all'indirizzo <aadapprequest@microsoft.com> o lasciare un commento nell'esercitazione per richiedere l'aggiornamento dei modelli supportati per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="4a5d2-140">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in the tutorial to request the update of the supported patterns for the application</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="4a5d2-141">Dove impostare il formato di EntityID (identificatore utente)</span><span class="sxs-lookup"><span data-stu-id="4a5d2-141">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="4a5d2-142">Non è possibile selezionare il formato di EntityID (identificatore utente) che Azure AD invia all'applicazione in risposta all'autenticazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-142">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="4a5d2-143">Azure AD seleziona il formato per l'attributo NameID (identificatore utente) in base al valore selezionato o al formato richiesto dall'applicazione nell'oggetto AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-143">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="4a5d2-144">Per altre informazioni, vedere l'articolo relativo al [protocollo SAML per Single Sign-On](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sotto la sezione NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-144">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="cant-find-the-azure-ad-metadata-to-complete-the-configuration-with-the-application"></a><span data-ttu-id="4a5d2-145">Impossibile trovare i metadati di Azure AD per completare la configurazione con l'applicazione</span><span class="sxs-lookup"><span data-stu-id="4a5d2-145">Can’t find the Azure AD metadata to complete the configuration with the application</span></span>

<span data-ttu-id="4a5d2-146">Per scaricare il certificato o i metadati dell'applicazione da Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4a5d2-146">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="4a5d2-147">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4a5d2-148">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4a5d2-149">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4a5d2-150">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-150">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4a5d2-151">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-151">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="4a5d2-152">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-152">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4a5d2-153">Selezionare l'applicazione per cui è stato configurato l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-153">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="4a5d2-154">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-154">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4a5d2-155">Passare alla sezione **Certificato di firma SAML** e quindi fare clic sul valore della colonna **Download**.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-155">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="4a5d2-156">A seconda di quale applicazione richiede la configurazione dell'accesso Single Sign-On, è visibile l'opzione per scaricare il codice XML dei metadati o l'opzione per scaricare il certificato.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-156">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="4a5d2-157">Azure AD non fornisce URL per ottenere i metadati.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-157">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="4a5d2-158">I metadati possono essere recuperati solo come file XML.</span><span class="sxs-lookup"><span data-stu-id="4a5d2-158">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="4a5d2-159">Informazioni sulla personalizzazione delle attestazioni SAML inviate a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="4a5d2-159">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="4a5d2-160">Per informazioni su come personalizzare le attestazioni degli attributi SAML inviate all'applicazione, vedere [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) (Mapping di attestazioni in Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4a5d2-160">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a5d2-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4a5d2-161">Next steps</span></span>
[<span data-ttu-id="4a5d2-162">Gestione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a5d2-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
