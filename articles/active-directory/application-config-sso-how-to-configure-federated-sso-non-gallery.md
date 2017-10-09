---
title: aaaHow tooconfigure federata single sign-on per un'applicazione non raccolta | Documenti Microsoft
description: Come tooconfigure federata single sign-on per un'applicazione non raccolta personalizzata che si desidera toointegrate con Azure AD
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
ms.openlocfilehash: f4a37cb500c075d0ce917ad8f13411f2ce208c56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="3e216-103">Come tooconfigure federata single sign-on per un'applicazione non-raccolta</span><span class="sxs-lookup"><span data-stu-id="3e216-103">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="3e216-104">un'applicazione non raccolta tooconfigure, è necessario toohave Azure AD premium e un'applicazione hello supporta SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="3e216-104">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="3e216-105">Per altre informazioni sulle versioni di Azure AD, vedere [Prezzi di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="3e216-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="3e216-106">Panoramica dei passaggi necessari</span><span class="sxs-lookup"><span data-stu-id="3e216-106">Overview of steps required</span></span>
<span data-ttu-id="3e216-107">Di seguito viene fornita una panoramica ad alto livello di hello passaggi necessari tooconfigure federata single sign-on per un non-raccolta (ad esempio, personalizzata) dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3e216-107">Below is a high level overview of hello steps required tooconfigure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="3e216-108">Configurare i valori dei metadati dell'applicazione hello in Azure AD (accesso URL, identificatore, l'URL di risposta)</span><span class="sxs-lookup"><span data-stu-id="3e216-108">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="3e216-109">Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente</span><span class="sxs-lookup"><span data-stu-id="3e216-109">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="3e216-110">Recuperare il certificato e i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e216-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="3e216-111">Configurare i valori dei metadati di Azure AD in un'applicazione hello (accesso URL, autorità emittente, Logout URL e certificato)</span><span class="sxs-lookup"><span data-stu-id="3e216-111">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="3e216-112">Assegnare gli utenti dell'applicazione toohello</span><span class="sxs-lookup"><span data-stu-id="3e216-112">Assign users toohello application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-toonon-gallery-applications"></a><span data-ttu-id="3e216-113">Configurazione di applicazioni single sign-on toonon-raccolta</span><span class="sxs-lookup"><span data-stu-id="3e216-113">Configuring single sign-on toonon-gallery applications</span></span>

<span data-ttu-id="3e216-114">tooconfigure single sign-on per un'applicazione che non si trova nella raccolta di Azure AD hello, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="3e216-114">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="3e216-115">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="3e216-115">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3e216-116">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-116">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3e216-117">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3e216-117">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3e216-118">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3e216-118">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3e216-119">Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** blade.</span><span class="sxs-lookup"><span data-stu-id="3e216-119">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="3e216-120">Fare clic su **applicazione Non raccolta** in hello **aggiungere la propria app** sezione</span><span class="sxs-lookup"><span data-stu-id="3e216-120">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="3e216-121">Immettere il nome di hello dell'applicazione hello in hello **nome** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="3e216-121">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="3e216-122">Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="3e216-122">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="3e216-123">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-123">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="3e216-124">Selezionare **basato su SAML Sign-on** in hello **modalità** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="3e216-124">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="3e216-125">Immettere i valori hello necessarie nelle **dominio e gli URL.**</span><span class="sxs-lookup"><span data-stu-id="3e216-125">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="3e216-126">È necessario ottenere questi valori dal fornitore dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-126">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="3e216-127">un'applicazione hello tooconfigure come avviata da IdP SSO, immettere hello URL di risposta e l'identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-127">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2. <span data-ttu-id="3e216-128">**Facoltativo:** tooconfigure un'applicazione hello come SSO avviato da SP, hello Sign in URL è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="3e216-128">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="3e216-129">In hello **gli attributi utente**, selezionare hello identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="3e216-129">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="3e216-130">**Facoltativo:** fare clic su **visualizzare e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.</span><span class="sxs-lookup"><span data-stu-id="3e216-130">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="3e216-131">un attributo tooadd:</span><span class="sxs-lookup"><span data-stu-id="3e216-131">tooadd an attribute:</span></span>

   1. <span data-ttu-id="3e216-132">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="3e216-132">click **Add attribute**.</span></span> <span data-ttu-id="3e216-133">Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-133">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="3e216-134">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3e216-134">Click **Save.**</span></span> <span data-ttu-id="3e216-135">Vedrai hello nuovo attributo tabella hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-135">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="3e216-136">Fare clic su **configura &lt;nome applicazione&gt;**  tooaccess documentazione sulla tooconfigure single sign-on nell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-136">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="3e216-137">È inoltre URL AD Azure e certificato richiesto per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-137">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

15. [<span data-ttu-id="3e216-138">Assegnare gli utenti dell'applicazione toohello.</span><span class="sxs-lookup"><span data-stu-id="3e216-138">Assign users toohello application.</span></span>](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="3e216-139">Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente</span><span class="sxs-lookup"><span data-stu-id="3e216-139">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="3e216-140">tooselect hello identificatore utente o aggiungere gli attributi utente, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="3e216-140">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="3e216-141">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="3e216-141">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3e216-142">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-142">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3e216-143">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3e216-143">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3e216-144">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3e216-144">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3e216-145">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="3e216-145">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3e216-146">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="3e216-146">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3e216-147">Selezionare un'applicazione hello è stato configurato single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3e216-147">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="3e216-148">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-148">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3e216-149">In hello **gli attributi utente** hello di sezione, selezionare un identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="3e216-149">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="3e216-150">Hello opzione selezionata deve toomatch hello previsto valore utente hello tooauthenticate dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-150">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

 ><span data-ttu-id="3e216-151">[! Nota} di Azure Active Directory, selezionare il formato di hello per hello NameID identificatore dell'attributo (utente) in base al valore di hello selezionato o hello formato richiesto da un'applicazione hello in hello AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="3e216-151">[!NOTE} Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="3e216-152">Per ulteriori informazioni visitare articolo hello [protocollo Single Sign-On SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) in hello sezione NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="3e216-152">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="3e216-153">Fare clic su attributi utente tooadd, **visualizzazione e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.</span><span class="sxs-lookup"><span data-stu-id="3e216-153">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="3e216-154">un attributo tooadd:</span><span class="sxs-lookup"><span data-stu-id="3e216-154">tooadd an attribute:</span></span>

   1. <span data-ttu-id="3e216-155">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="3e216-155">click **Add attribute**.</span></span> <span data-ttu-id="3e216-156">Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-156">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="3e216-157">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3e216-157">Click **Save.**</span></span> <span data-ttu-id="3e216-158">Vedrai hello nuovo attributo tabella hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-158">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="3e216-159">Scaricare i metadati di Azure AD hello o certificato</span><span class="sxs-lookup"><span data-stu-id="3e216-159">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="3e216-160">i metadati dell'applicazione hello toodownload o un certificato da Azure AD, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="3e216-160">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="3e216-161">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="3e216-161">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3e216-162">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-162">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3e216-163">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3e216-163">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3e216-164">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3e216-164">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3e216-165">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="3e216-165">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="3e216-166">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="3e216-166">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3e216-167">Selezionare un'applicazione hello è stato configurato single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3e216-167">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="3e216-168">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-168">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3e216-169">Andare troppo**certificato di firma SAML** sezione, quindi fare clic su **scaricare** valore della colonna.</span><span class="sxs-lookup"><span data-stu-id="3e216-169">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="3e216-170">A seconda di quale applicazione hello richiede la configurazione di single sign-on, vedere uno toodownload opzione hello hello Metadata XML o hello certificato.</span><span class="sxs-lookup"><span data-stu-id="3e216-170">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="3e216-171">Azure AD non fornisce i metadati hello tooget URL.</span><span class="sxs-lookup"><span data-stu-id="3e216-171">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="3e216-172">Hello metadati possono essere recuperati solo come un file XML.</span><span class="sxs-lookup"><span data-stu-id="3e216-172">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="3e216-173">Assegnare gli utenti dell'applicazione toohello</span><span class="sxs-lookup"><span data-stu-id="3e216-173">Assign users toohello application</span></span>

<span data-ttu-id="3e216-174">tooassign uno o più applicazioni tooan utenti direttamente, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="3e216-174">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="3e216-175">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="3e216-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3e216-176">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3e216-177">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3e216-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3e216-178">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3e216-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3e216-179">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="3e216-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3e216-180">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="3e216-180">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3e216-181">Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="3e216-181">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="3e216-182">Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-182">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3e216-183">Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="3e216-183">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="3e216-184">Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="3e216-184">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="3e216-185">Tipo di hello **nome completo** o **indirizzo di posta elettronica** dell'utente hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="3e216-185">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="3e216-186">Passare il mouse su hello **utente** in hello elenco tooreveal un **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="3e216-186">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="3e216-187">Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello dell'utente il toohello utente **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="3e216-187">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="3e216-188">**Facoltativo:** se si desidera troppo**aggiungere più di un utente**, in un altro tipo di **nome completo** o **indirizzo di posta elettronica** in hello **Cerca per nome o l'indirizzo di posta elettronica** casella di ricerca e fare clic su questo toohello utente hello casella di controllo tooadd **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="3e216-188">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="3e216-189">Al termine della selezione utenti, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="3e216-189">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="3e216-190">**Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un ruolo tooassign toohello utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="3e216-190">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="3e216-191">Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="3e216-191">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="3e216-192">Dopo un breve periodo di tempo, gli utenti di hello selezionato in toolaunch in grado di queste applicazioni utilizzano hello metodi descritti nella sezione Descrizione della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="3e216-192">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="3e216-193">Personalizzazione di attestazioni SAML hello inviati tooan applicazione</span><span class="sxs-lookup"><span data-stu-id="3e216-193">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="3e216-194">toolearn come le attestazioni degli attributi toocustomize hello SAML inviato tooyour applicazione, vedere [attestazioni mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="3e216-194">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e216-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3e216-195">Next steps</span></span>
[<span data-ttu-id="3e216-196">Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="3e216-196">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
