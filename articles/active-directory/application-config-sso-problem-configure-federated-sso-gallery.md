---
title: la configurazione di single sign-on federato per un'applicazione Azure AD raccolta aaaProblem | Documenti Microsoft
description: "Risolvere alcuni dei problemi più comuni di hello che si verifichino quando configurazione federata single sign-on tramite SAML per le applicazioni che sono elencate nella raccolta di applicazioni Azure AD hello"
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
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="60839-103">Problema nella configurazione dell'accesso Single Sign-On federato per un'applicazione nella raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="60839-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="60839-104">Se si verifica un problema durante la configurazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="60839-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="60839-105">Verificare di che aver seguito tutti i passaggi di hello in esercitazione hello per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="60839-105">Verify you have followed all hello steps in hello tutorial for hello application.</span></span> <span data-ttu-id="60839-106">Nella configurazione dell'applicazione hello, si dispone della documentazione in linea in modalità tooconfigure hello applicazione.</span><span class="sxs-lookup"><span data-stu-id="60839-106">In hello application’s configuration, you have inline documentation on how tooconfigure hello application.</span></span> <span data-ttu-id="60839-107">Inoltre, è possibile accedere hello [elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) per una Guida di dettaglio.</span><span class="sxs-lookup"><span data-stu-id="60839-107">Also, you can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="60839-108">Non è possibile aggiungere un'altra istanza di un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="60839-108">Can’t add another instance of hello application</span></span>

<span data-ttu-id="60839-109">tooadd una seconda istanza di un'applicazione, è necessario poter toobe:</span><span class="sxs-lookup"><span data-stu-id="60839-109">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="60839-110">Configurare un identificatore univoco per la seconda istanza hello.</span><span class="sxs-lookup"><span data-stu-id="60839-110">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="60839-111">Non sarà in grado di tooconfigure hello stesso identificatore utilizzato per la prima istanza hello.</span><span class="sxs-lookup"><span data-stu-id="60839-111">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="60839-112">Configurare un certificato diverso da hello di hello prima istanza.</span><span class="sxs-lookup"><span data-stu-id="60839-112">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="60839-113">Se hello applicazione non supporta i hello precedente.</span><span class="sxs-lookup"><span data-stu-id="60839-113">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="60839-114">Quindi, non sarà in grado di tooconfigure una seconda istanza.</span><span class="sxs-lookup"><span data-stu-id="60839-114">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a><span data-ttu-id="60839-115">Non è possibile aggiungere l'identificatore hello o hello URL di risposta</span><span class="sxs-lookup"><span data-stu-id="60839-115">Can’t add hello Identifier or hello Reply URL</span></span>

<span data-ttu-id="60839-116">Se non si è in grado di tooconfigure hello identificatore o URL di risposta hello, confermare l'identificatore hello e valori di URL di risposta corrispondono a criteri di hello preconfigurati per l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="60839-116">If you’re not able tooconfigure hello Identifier or hello Reply URL, confirm hello Identifier and Reply URL values match hello patterns pre-configured for hello application.</span></span>

<span data-ttu-id="60839-117">modelli di hello tooknow preconfigurati per l'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="60839-117">tooknow hello patterns pre-configured for hello application:</span></span>

1.  <span data-ttu-id="60839-118">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.** Passare toostep 7.</span><span class="sxs-lookup"><span data-stu-id="60839-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.** Go toostep 7.</span></span> <span data-ttu-id="60839-119">Se già presenti nel Pannello di configurazione dell'applicazione hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60839-119">If you are already in hello application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="60839-120">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="60839-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="60839-121">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="60839-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="60839-122">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="60839-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="60839-123">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="60839-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="60839-124">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="60839-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="60839-125">Selezionare l'applicazione hello tooconfigure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="60839-125">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="60839-126">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="60839-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="60839-127">Selezionare **basato su SAML Sign-on** da hello **modalità** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="60839-127">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="60839-128">Passare toohello **identificatore** o **URL di risposta** casella di testo, in hello **sezione URL e di dominio.**</span><span class="sxs-lookup"><span data-stu-id="60839-128">Go toohello **Identifier** or **Reply URL** textbox, under hello **Domain and URLs section.**</span></span>

10. <span data-ttu-id="60839-129">Esistono tre modi diversi modelli di tooknow hello è supportato per un'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="60839-129">There are three ways tooknow hello supported patterns for hello application:</span></span>

   * <span data-ttu-id="60839-130">Nella casella di testo hello hello supportato criteri viene visualizzato come segnaposto *esempio:* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="60839-130">In hello textbox, you see hello supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="60839-131">Se hello pattern non è supportato, viene visualizzato un punto esclamativo rosso quando si tenta di valore hello tooenter nella casella di testo hello.</span><span class="sxs-lookup"><span data-stu-id="60839-131">if hello pattern is not supported, you see a red exclamation mark when you try tooenter hello value in hello textbox.</span></span> <span data-ttu-id="60839-132">Se si posiziona il puntatore del mouse sul punto esclamativo rosso hello, visualizzare i modelli di hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="60839-132">If you hover your mouse over hello red exclamation mark, you see hello supported patterns.</span></span>

   * <span data-ttu-id="60839-133">Nell'esercitazione di hello per un'applicazione hello, è anche possibile ottenere informazioni sui pattern di hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="60839-133">In hello tutorial for hello application, you can also get information about hello supported patterns.</span></span> <span data-ttu-id="60839-134">In hello **Configura Azure AD single sign-on** sezione.</span><span class="sxs-lookup"><span data-stu-id="60839-134">Under hello **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="60839-135">Passaggio toohello passare i valori hello configurata in hello **dominio e gli URL** sezione.</span><span class="sxs-lookup"><span data-stu-id="60839-135">Go toohello step for configured hello values under hello **Domain and URLs** section.</span></span>

<span data-ttu-id="60839-136">Se i valori hello non corrispondano con i modelli di hello preconfigurati in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60839-136">If hello values don’t match with hello patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="60839-137">È possibile:</span><span class="sxs-lookup"><span data-stu-id="60839-137">You can:</span></span>

-   <span data-ttu-id="60839-138">Lavorare con i valori tooget fornitore dell'applicazione hello che corrispondono a criterio hello preconfigurato in Azure AD</span><span class="sxs-lookup"><span data-stu-id="60839-138">Work with hello application vendor tooget values that match hello pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="60839-139">In alternativa, è possibile contattare il team di Azure AD < aadapprequest@microsoft.com > o lasciare un commento nell'aggiornamento di hello toorequest esercitazione hello dei modelli di hello è supportato per un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="60839-139">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in hello tutorial toorequest hello update of hello supported patterns for hello application</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="60839-140">In cui è possibile impostare il formato di EntityID (ID utente) hello</span><span class="sxs-lookup"><span data-stu-id="60839-140">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="60839-141">Sarà formato EntityID (ID utente) di hello tooselect in grado di Azure AD invia toohello applicazione in risposta hello dopo l'autenticazione utente.</span><span class="sxs-lookup"><span data-stu-id="60839-141">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="60839-142">Azure AD selezionare hello formato attributo NameID hello (ID utente) in base al valore di hello selezionato o per hello formato richiesto da un'applicazione hello in hello AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="60839-142">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="60839-143">Per ulteriori informazioni visitare articolo hello [protocollo Single Sign-On SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) nella sezione hello NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="60839-143">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a><span data-ttu-id="60839-144">Impossibile trovare la configurazione hello Azure AD metadati toocomplete hello con un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="60839-144">Can’t find hello Azure AD metadata toocomplete hello configuration with hello application</span></span>

<span data-ttu-id="60839-145">i metadati dell'applicazione hello toodownload o un certificato da Azure AD, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="60839-145">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="60839-146">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="60839-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="60839-147">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="60839-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="60839-148">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="60839-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="60839-149">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="60839-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="60839-150">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="60839-150">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="60839-151">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="60839-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="60839-152">Selezionare un'applicazione hello è stato configurato single sign-on.</span><span class="sxs-lookup"><span data-stu-id="60839-152">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="60839-153">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="60839-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="60839-154">Andare troppo**certificato di firma SAML** sezione, quindi fare clic su **scaricare** valore della colonna.</span><span class="sxs-lookup"><span data-stu-id="60839-154">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="60839-155">A seconda di quale applicazione hello richiede la configurazione di single sign-on, vedere uno toodownload opzione hello hello Metadata XML o hello certificato.</span><span class="sxs-lookup"><span data-stu-id="60839-155">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="60839-156">Azure AD non fornisce i metadati hello tooget URL.</span><span class="sxs-lookup"><span data-stu-id="60839-156">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="60839-157">Hello metadati possono essere recuperati solo come un file XML.</span><span class="sxs-lookup"><span data-stu-id="60839-157">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="60839-158">Non conosce la modalità di invio applicazione tooan attestazioni SAML toocustomize</span><span class="sxs-lookup"><span data-stu-id="60839-158">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="60839-159">toolearn come le attestazioni degli attributi toocustomize hello SAML inviato tooyour applicazione, vedere [attestazioni mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="60839-159">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60839-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="60839-160">Next steps</span></span>
[<span data-ttu-id="60839-161">Gestione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60839-161">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
