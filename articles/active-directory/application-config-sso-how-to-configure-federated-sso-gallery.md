---
title: aaaHow tooconfigure federata single sign-on per un'applicazione Azure AD raccolta | Documenti Microsoft
description: Come tooconfigure federata single sign-on per un esistente raccolta di Azure AD applicazione e usare esercitazioni tooget lavorare rapidamente
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
ms.openlocfilehash: a93de021fddd253e4fe663c221b822d12625fd54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="b91cf-103">Come tooconfigure federata single sign-on per un'applicazione di raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b91cf-103">How tooconfigure federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="b91cf-104">Tutte le applicazioni nella raccolta di Azure AD hello abilitata con funzionalità Enterprise single sign-on con un'esercitazione dettagliata disponibile.</span><span class="sxs-lookup"><span data-stu-id="b91cf-104">All applications in hello Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="b91cf-105">È possibile accedere hello [elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) per istruzioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="b91cf-105">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="b91cf-106">Panoramica dei passaggi necessari</span><span class="sxs-lookup"><span data-stu-id="b91cf-106">Overview of steps required</span></span>
<span data-ttu-id="b91cf-107">un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:</span><span class="sxs-lookup"><span data-stu-id="b91cf-107">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="b91cf-108">Aggiungere un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b91cf-108">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="b91cf-109">Configurare i valori dei metadati dell'applicazione hello in Azure AD (accesso URL, identificatore, l'URL di risposta)</span><span class="sxs-lookup"><span data-stu-id="b91cf-109">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="b91cf-110">Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente</span><span class="sxs-lookup"><span data-stu-id="b91cf-110">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="b91cf-111">Recuperare il certificato e i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b91cf-111">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="b91cf-112">Configurare i valori dei metadati di Azure AD in un'applicazione hello (accesso URL, autorità emittente, Logout URL e certificato)</span><span class="sxs-lookup"><span data-stu-id="b91cf-112">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="b91cf-113">Assegnare gli utenti dell'applicazione toohello</span><span class="sxs-lookup"><span data-stu-id="b91cf-113">Assign users toohello application</span></span>](#assign-users-to-the-application)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="b91cf-114">Aggiungere un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b91cf-114">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="b91cf-115">un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="b91cf-115">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="b91cf-116">Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**</span><span class="sxs-lookup"><span data-stu-id="b91cf-116">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="b91cf-117">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b91cf-118">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="b91cf-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b91cf-119">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b91cf-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b91cf-120">Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** blade.</span><span class="sxs-lookup"><span data-stu-id="b91cf-120">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="b91cf-121">In hello **immettere un nome** casella di testo da hello **Aggiungi dalla raccolta hello** sezione, il nome del tipo hello di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-121">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="b91cf-122">Selezionare l'applicazione hello da tooconfigure per single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b91cf-122">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="b91cf-123">Prima di aggiungere un'applicazione hello, è possibile modificarne il nome da hello **nome** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="b91cf-123">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="b91cf-124">Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b91cf-124">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="b91cf-125">Dopo un breve periodo di tempo, è il pannello di configurazione dell'applicazione in grado di toosee hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-125">After a short period of time, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="b91cf-126">Configurare single sign-on per un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b91cf-126">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="b91cf-127">tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="b91cf-127">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="b91cf-128">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore**.</span><span class="sxs-lookup"><span data-stu-id="b91cf-128">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="b91cf-129">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-129">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b91cf-130">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="b91cf-130">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b91cf-131">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b91cf-131">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b91cf-132">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b91cf-132">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="b91cf-133">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="b91cf-133">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b91cf-134">Selezionare l'applicazione hello tooconfigure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b91cf-134">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="b91cf-135">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-135">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b91cf-136">Selezionare **basato su SAML Sign-on** da hello **modalità** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="b91cf-136">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="b91cf-137">Immettere i valori hello necessarie nelle **dominio e gli URL.**</span><span class="sxs-lookup"><span data-stu-id="b91cf-137">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="b91cf-138">È necessario ottenere questi valori dal fornitore dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-138">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="b91cf-139">un'applicazione hello tooconfigure come SSO avviato da SP, hello Sign in URL è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b91cf-139">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="b91cf-140">Per alcune applicazioni, identificatore hello è anche un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b91cf-140">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="b91cf-141">applicazione hello tooconfigure come avviata da IdP SSO, hello URL di risposta è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b91cf-141">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="b91cf-142">Per alcune applicazioni, identificatore hello è anche un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b91cf-142">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="b91cf-143">**Facoltativo:** fare clic su **Mostra URL impostazioni avanzate** se si desidera toosee hello non obbligatori valori.</span><span class="sxs-lookup"><span data-stu-id="b91cf-143">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="b91cf-144">In hello **gli attributi utente**, selezionare hello identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="b91cf-144">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="b91cf-145">**Facoltativo:** fare clic su **visualizzare e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.</span><span class="sxs-lookup"><span data-stu-id="b91cf-145">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

  <span data-ttu-id="b91cf-146">un attributo tooadd:</span><span class="sxs-lookup"><span data-stu-id="b91cf-146">tooadd an attribute:</span></span>
   
   1. <span data-ttu-id="b91cf-147">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="b91cf-147">click **Add attribute**.</span></span> <span data-ttu-id="b91cf-148">Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-148">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   1. <span data-ttu-id="b91cf-149">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b91cf-149">Click **Save.**</span></span> <span data-ttu-id="b91cf-150">Vedrai hello nuovo attributo tabella hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-150">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="b91cf-151">Fare clic su **configura &lt;nome applicazione&gt;**  tooaccess documentazione sulla tooconfigure single sign-on nell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-151">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="b91cf-152">È inoltre gli URL dei metadati di hello e certificato richiesto toosetup SSO con un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-152">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="b91cf-153">Fare clic su **salvare** configurazione hello toosave.</span><span class="sxs-lookup"><span data-stu-id="b91cf-153">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="b91cf-154">Assegnare gli utenti dell'applicazione toohello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-154">Assign users toohello application.</span></span>

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="b91cf-155">Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente</span><span class="sxs-lookup"><span data-stu-id="b91cf-155">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="b91cf-156">tooselect hello identificatore utente o aggiungere gli attributi utente, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="b91cf-156">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="b91cf-157">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="b91cf-157">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b91cf-158">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b91cf-159">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="b91cf-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b91cf-160">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b91cf-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b91cf-161">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b91cf-161">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="b91cf-162">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="b91cf-162">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b91cf-163">Selezionare un'applicazione hello è stato configurato single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b91cf-163">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b91cf-164">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-164">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b91cf-165">In hello **gli attributi utente** hello di sezione, selezionare un identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="b91cf-165">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="b91cf-166">Hello opzione selezionata deve toomatch hello previsto valore utente hello tooauthenticate dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-166">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

  >[!NOTE] 
  ><span data-ttu-id="b91cf-167">Azure AD selezionare hello formato attributo NameID hello (ID utente) in base al valore di hello selezionato o per hello formato richiesto da un'applicazione hello in hello AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="b91cf-167">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="b91cf-168">Per ulteriori informazioni visitare articolo hello [protocollo Single Sign-On SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) in hello sezione NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="b91cf-168">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
  >
  >

9.  <span data-ttu-id="b91cf-169">Fare clic su attributi utente tooadd, **visualizzazione e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.</span><span class="sxs-lookup"><span data-stu-id="b91cf-169">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="b91cf-170">un attributo tooadd:</span><span class="sxs-lookup"><span data-stu-id="b91cf-170">tooadd an attribute:</span></span>
  
   1. <span data-ttu-id="b91cf-171">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="b91cf-171">click **Add attribute**.</span></span> <span data-ttu-id="b91cf-172">Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-172">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="b91cf-173">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b91cf-173">Click **Save**.</span></span> <span data-ttu-id="b91cf-174">Vedrai hello nuovo attributo tabella hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-174">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="b91cf-175">Scaricare i metadati di Azure AD hello o certificato</span><span class="sxs-lookup"><span data-stu-id="b91cf-175">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="b91cf-176">i metadati dell'applicazione hello toodownload o un certificato da Azure AD, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="b91cf-176">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="b91cf-177">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="b91cf-177">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b91cf-178">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-178">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b91cf-179">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="b91cf-179">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b91cf-180">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b91cf-180">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b91cf-181">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b91cf-181">click **All Applications** tooview a list of all your applications.</span></span>

  *  <span data-ttu-id="b91cf-182">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b91cf-182">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications**.</span></span>

6.  <span data-ttu-id="b91cf-183">Selezionare un'applicazione hello è stato configurato single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b91cf-183">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b91cf-184">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-184">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b91cf-185">Andare troppo**certificato di firma SAML** sezione, quindi fare clic su **scaricare** valore della colonna.</span><span class="sxs-lookup"><span data-stu-id="b91cf-185">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="b91cf-186">A seconda di quale applicazione hello richiede la configurazione di single sign-on, vedere uno toodownload opzione hello hello Metadata XML o hello certificato.</span><span class="sxs-lookup"><span data-stu-id="b91cf-186">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="b91cf-187">Azure AD non fornisce i metadati hello tooget URL.</span><span class="sxs-lookup"><span data-stu-id="b91cf-187">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="b91cf-188">Hello metadati possono essere recuperati solo come un file XML.</span><span class="sxs-lookup"><span data-stu-id="b91cf-188">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="b91cf-189">Assegnare gli utenti dell'applicazione toohello</span><span class="sxs-lookup"><span data-stu-id="b91cf-189">Assign users toohello application</span></span>

<span data-ttu-id="b91cf-190">tooassign uno o più applicazioni tooan utenti direttamente, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="b91cf-190">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="b91cf-191">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="b91cf-191">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b91cf-192">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-192">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b91cf-193">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="b91cf-193">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b91cf-194">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b91cf-194">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b91cf-195">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b91cf-195">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="b91cf-196">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="b91cf-196">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b91cf-197">Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="b91cf-197">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="b91cf-198">Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-198">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b91cf-199">Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="b91cf-199">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="b91cf-200">Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="b91cf-200">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="b91cf-201">Tipo di hello **nome completo** o **indirizzo di posta elettronica** dell'utente hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="b91cf-201">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="b91cf-202">Passare il mouse su hello **utente** in hello elenco tooreveal un **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="b91cf-202">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="b91cf-203">Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello dell'utente il toohello utente **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="b91cf-203">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="b91cf-204">**Facoltativo:** se si desidera troppo**aggiungere più di un utente**, in un altro tipo di **nome completo** o **indirizzo di posta elettronica** in hello **Cerca per nome o l'indirizzo di posta elettronica** casella di ricerca e fare clic su questo toohello utente hello casella di controllo tooadd **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="b91cf-204">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="b91cf-205">Al termine della selezione utenti, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="b91cf-205">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="b91cf-206">**Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un ruolo tooassign toohello utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="b91cf-206">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="b91cf-207">Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="b91cf-207">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="b91cf-208">Dopo un breve periodo di tempo, gli utenti di hello selezionato in toolaunch in grado di queste applicazioni utilizzano hello metodi descritti nella sezione Descrizione della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="b91cf-208">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="b91cf-209">Personalizzazione di attestazioni SAML hello inviati tooan applicazione</span><span class="sxs-lookup"><span data-stu-id="b91cf-209">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="b91cf-210">toolearn come le attestazioni degli attributi toocustomize hello SAML inviato tooyour applicazione, vedere [attestazioni mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="b91cf-210">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b91cf-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b91cf-211">Next steps</span></span>
[<span data-ttu-id="b91cf-212">Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="b91cf-212">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)



