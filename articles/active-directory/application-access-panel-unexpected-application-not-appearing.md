---
title: applicazione aaaAn assegnato non viene visualizzato nel Pannello di accesso hello | Documenti Microsoft
description: "Risoluzione dei problemi perché un'applicazione non viene visualizzato nel Pannello di accesso hello"
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
ms.openlocfilehash: 089883f406267df4552c7fc991883f335ad49fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="an-assigned-application-is-not-appearing-on-hello-access-panel"></a><span data-ttu-id="db07d-103">Un'applicazione assegnata non viene visualizzato nel Pannello di accesso hello</span><span class="sxs-lookup"><span data-stu-id="db07d-103">An assigned application is not appearing on hello access panel</span></span>

<span data-ttu-id="db07d-104">Hello Pannello di accesso è un portale basato sul web che consente a un utente con un lavoro o account Azure Active Directory (Azure AD) tooview avvio basato su cloud le applicazioni e dell'istituto di istruzione che hello amministratore di Azure AD ha concesso l'accesso a.</span><span class="sxs-lookup"><span data-stu-id="db07d-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="db07d-105">Queste applicazioni sono configurate per conto di utente hello nel portale di Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="db07d-106">un'applicazione Hello deve essere configurata correttamente e toohello assegnato utente o un utente di hello gruppo è un membro di un'applicazione hello toosee in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="db07d-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="db07d-107">tipo Hello delle App, potrebbe essere visualizzato un utente rientrano nelle seguenti categorie di hello:</span><span class="sxs-lookup"><span data-stu-id="db07d-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="db07d-108">Applicazioni di Office 365</span><span class="sxs-lookup"><span data-stu-id="db07d-108">Office 365 Applications</span></span>

-   <span data-ttu-id="db07d-109">Applicazioni Microsoft e di terze parti configurate con il servizio Single Sign-On basato su federazione</span><span class="sxs-lookup"><span data-stu-id="db07d-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="db07d-110">Applicazioni SSO basate su password</span><span class="sxs-lookup"><span data-stu-id="db07d-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="db07d-111">Applicazioni con soluzioni SSO esistenti</span><span class="sxs-lookup"><span data-stu-id="db07d-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="db07d-112">Generale problemi toocheck prima</span><span class="sxs-lookup"><span data-stu-id="db07d-112">General issues toocheck first</span></span>

-   <span data-ttu-id="db07d-113">Se un'applicazione è stata appena aggiunta utente tooa, riprovare toosign avanti e indietro nel Pannello di accesso dell'utente hello dopo pochi minuti toosee se viene aggiunta un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-113">If an application was just added tooa user, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is added.</span></span>

-   <span data-ttu-id="db07d-114">Se una licenza è stata rimossa solo da un utente o gruppo utente hello è che un membro di questo potrebbe richiedere molto tempo, a seconda delle dimensioni di hello e la complessità del gruppo di hello per toobe le modifiche apportate.</span><span class="sxs-lookup"><span data-stu-id="db07d-114">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="db07d-115">Consentire del tempo aggiuntivo prima della firma in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="db07d-115">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooapplication-configuration"></a><span data-ttu-id="db07d-116">Configurazione di problemi correlati tooapplication</span><span class="sxs-lookup"><span data-stu-id="db07d-116">Problems related tooapplication configuration</span></span>

<span data-ttu-id="db07d-117">È possibile che un'applicazione non venga visualizzata nel pannello di accesso dell'utente a causa di un'errata configurazione della stessa.</span><span class="sxs-lookup"><span data-stu-id="db07d-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="db07d-118">Ecco alcuni modi in cui che è possibile risolvere problemi di configurazione correlati tooapplication problemi:</span><span class="sxs-lookup"><span data-stu-id="db07d-118">Below are some ways you can troubleshoot issues related tooapplication configuration:</span></span>

-   [<span data-ttu-id="db07d-119">Come tooconfigure federata single sign-on per un'applicazione di raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="db07d-119">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="db07d-120">Come tooconfigure federata single sign-on per un'applicazione non-raccolta</span><span class="sxs-lookup"><span data-stu-id="db07d-120">How tooconfigure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="db07d-121">Come tooconfigure una password single sign-on dell'applicazione per un'applicazione di raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="db07d-121">How tooconfigure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="db07d-122">Come tooconfigure una password single sign-on dell'applicazione per un'applicazione non-raccolta</span><span class="sxs-lookup"><span data-stu-id="db07d-122">How tooconfigure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="db07d-123">Come tooconfigure federata single sign-on per un'applicazione di raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="db07d-123">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="db07d-124">Tutte le applicazioni nella raccolta di Azure AD hello abilitata con funzionalità di Enterprise Single Sign-On con un'esercitazione dettagliata disponibile.</span><span class="sxs-lookup"><span data-stu-id="db07d-124">All applications in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="db07d-125">È possibile accedere hello [elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) per una Guida di dettaglio.</span><span class="sxs-lookup"><span data-stu-id="db07d-125">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="db07d-126">un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:</span><span class="sxs-lookup"><span data-stu-id="db07d-126">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="db07d-127">Aggiungere un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="db07d-127">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="db07d-128">Configurare i valori dei metadati dell'applicazione hello in Azure AD (accesso URL, identificatore, l'URL di risposta)</span><span class="sxs-lookup"><span data-stu-id="db07d-128">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="db07d-129">Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente</span><span class="sxs-lookup"><span data-stu-id="db07d-129">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="db07d-130">Recuperare il certificato e i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="db07d-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="db07d-131">Configurare i valori dei metadati di Azure AD in un'applicazione hello (accesso URL, autorità emittente, Logout URL e certificato)</span><span class="sxs-lookup"><span data-stu-id="db07d-131">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="db07d-132">Aggiungere un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="db07d-132">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="db07d-133">un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-133">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-134">Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**</span><span class="sxs-lookup"><span data-stu-id="db07d-134">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="db07d-135">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-135">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-136">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-136">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-137">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db07d-137">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="db07d-138">Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** blade.</span><span class="sxs-lookup"><span data-stu-id="db07d-138">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="db07d-139">In hello **immettere un nome** casella di testo da hello **Aggiungi dalla raccolta hello** sezione, il nome del tipo hello di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-139">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="db07d-140">Selezionare l'applicazione hello da tooconfigure per single sign-on.</span><span class="sxs-lookup"><span data-stu-id="db07d-140">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="db07d-141">Prima di aggiungere un'applicazione hello, è possibile modificarne il nome da hello **nome** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="db07d-141">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="db07d-142">Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="db07d-142">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="db07d-143">Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-143">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="db07d-144">Configurare single sign-on per un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="db07d-144">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="db07d-145">tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-145">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-146">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="db07d-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="db07d-147">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-148">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-149">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db07d-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="db07d-150">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="db07d-150">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="db07d-151">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="db07d-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="db07d-152">Selezionare l'applicazione hello tooconfigure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="db07d-152">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="db07d-153">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="db07d-154">Selezionare **basato su SAML Sign-on** da hello **modalità** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="db07d-154">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="db07d-155">Immettere i valori hello necessarie nelle **dominio e gli URL.**</span><span class="sxs-lookup"><span data-stu-id="db07d-155">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="db07d-156">È necessario ottenere questi valori dal fornitore dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-156">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="db07d-157">un'applicazione hello tooconfigure come SSO avviato da SP, hello Sign in URL è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="db07d-157">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="db07d-158">Per alcune applicazioni, identificatore hello è anche un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="db07d-158">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="db07d-159">applicazione hello tooconfigure come avviata da IdP SSO, hello URL di risposta è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="db07d-159">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="db07d-160">Per alcune applicazioni, identificatore hello è anche un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="db07d-160">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="db07d-161">**Facoltativo:** fare clic su **Mostra URL impostazioni avanzate** se si desidera toosee hello non obbligatori valori.</span><span class="sxs-lookup"><span data-stu-id="db07d-161">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="db07d-162">In hello **gli attributi utente**, selezionare hello identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="db07d-162">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="db07d-163">**Facoltativo:** fare clic su **visualizzare e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.</span><span class="sxs-lookup"><span data-stu-id="db07d-163">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="db07d-164">un attributo tooadd:</span><span class="sxs-lookup"><span data-stu-id="db07d-164">tooadd an attribute:</span></span>

   1. <span data-ttu-id="db07d-165">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="db07d-165">click **Add attribute**.</span></span> <span data-ttu-id="db07d-166">Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-166">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="db07d-167">fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="db07d-167">click **Save.**</span></span> <span data-ttu-id="db07d-168">Vedrai hello nuovo attributo tabella hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-168">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="db07d-169">Fare clic su **configura &lt;nome applicazione&gt;**  tooaccess documentazione sulla tooconfigure single sign-on nell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-169">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="db07d-170">È inoltre gli URL dei metadati di hello e certificato richiesto toosetup SSO con un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-170">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="db07d-171">Fare clic su **salvare** configurazione hello toosave.</span><span class="sxs-lookup"><span data-stu-id="db07d-171">click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="db07d-172">Assegnare gli utenti dell'applicazione toohello.</span><span class="sxs-lookup"><span data-stu-id="db07d-172">Assign users toohello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="db07d-173">Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente</span><span class="sxs-lookup"><span data-stu-id="db07d-173">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="db07d-174">tooselect hello identificatore utente o aggiungere gli attributi utente, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-174">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-175">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="db07d-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="db07d-176">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-177">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-178">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db07d-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="db07d-179">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="db07d-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="db07d-180">Se non viene visualizzata l'applicazione hello da tooshow qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="db07d-180">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="db07d-181">Selezionare un'applicazione hello è stato configurato single sign-on.</span><span class="sxs-lookup"><span data-stu-id="db07d-181">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="db07d-182">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-182">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="db07d-183">In hello **gli attributi utente** hello di sezione, selezionare un identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="db07d-183">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="db07d-184">Hello opzione selezionata deve toomatch hello previsto valore utente hello tooauthenticate dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-184">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="db07d-185">Azure AD selezionare hello formato attributo NameID hello (ID utente) in base al valore di hello selezionato o per hello formato richiesto da un'applicazione hello in hello AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="db07d-185">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="db07d-186">Per ulteriori informazioni visitare articolo hello [protocollo Single Sign-On SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) in hello sezione NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="db07d-186">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="db07d-187">Fare clic su attributi utente tooadd, **visualizzazione e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.</span><span class="sxs-lookup"><span data-stu-id="db07d-187">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="db07d-188">un attributo tooadd:</span><span class="sxs-lookup"><span data-stu-id="db07d-188">tooadd an attribute:</span></span>

   1. <span data-ttu-id="db07d-189">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="db07d-189">click **Add attribute**.</span></span> <span data-ttu-id="db07d-190">Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-190">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="db07d-191">fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="db07d-191">click **Save.**</span></span> <span data-ttu-id="db07d-192">Si noterà hello nuovo attributo tabella hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-192">You will see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="db07d-193">Scaricare i metadati di Azure AD hello o certificato</span><span class="sxs-lookup"><span data-stu-id="db07d-193">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="db07d-194">i metadati dell'applicazione hello toodownload o un certificato da Azure AD, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-194">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-195">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="db07d-195">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="db07d-196">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-196">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-197">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-197">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-198">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db07d-198">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="db07d-199">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="db07d-199">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="db07d-200">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="db07d-200">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="db07d-201">Selezionare un'applicazione hello è stato configurato single sign-on.</span><span class="sxs-lookup"><span data-stu-id="db07d-201">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="db07d-202">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-202">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="db07d-203">Andare troppo**certificato di firma SAML** sezione, quindi fare clic su **scaricare** valore della colonna.</span><span class="sxs-lookup"><span data-stu-id="db07d-203">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="db07d-204">A seconda di quale applicazione hello richiede la configurazione di single sign-on, vedere uno toodownload opzione hello hello Metadata XML o hello certificato.</span><span class="sxs-lookup"><span data-stu-id="db07d-204">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="db07d-205">Azure AD non fornisce i metadati hello tooget URL.</span><span class="sxs-lookup"><span data-stu-id="db07d-205">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="db07d-206">Hello metadati possono essere recuperati solo come un file XML.</span><span class="sxs-lookup"><span data-stu-id="db07d-206">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="db07d-207">Come tooconfigure federata single sign-on per un'applicazione non-raccolta</span><span class="sxs-lookup"><span data-stu-id="db07d-207">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="db07d-208">un'applicazione non raccolta tooconfigure, è necessario toohave Azure AD premium e un'applicazione hello supporta SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="db07d-208">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="db07d-209">Per altre informazioni sulle versioni di Azure AD, vedere [Prezzi di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="db07d-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="db07d-210">Configurare i valori dei metadati dell'applicazione hello in Azure AD (accesso URL, identificatore, l'URL di risposta)</span><span class="sxs-lookup"><span data-stu-id="db07d-210">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="db07d-211">Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente</span><span class="sxs-lookup"><span data-stu-id="db07d-211">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="db07d-212">Recuperare il certificato e i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="db07d-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="db07d-213">Configurare i valori dei metadati di Azure AD in un'applicazione hello (accesso URL, autorità emittente, Logout URL e certificato)</span><span class="sxs-lookup"><span data-stu-id="db07d-213">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="db07d-214">Configurare i valori dei metadati dell'applicazione hello in Azure AD (accesso URL, identificatore, l'URL di risposta)</span><span class="sxs-lookup"><span data-stu-id="db07d-214">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="db07d-215">tooconfigure single sign-on per un'applicazione che non si trova nella raccolta di Azure AD hello, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-215">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-216">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="db07d-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="db07d-217">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-218">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-219">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db07d-219">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="db07d-220">Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** blade.</span><span class="sxs-lookup"><span data-stu-id="db07d-220">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="db07d-221">Fare clic su **applicazione Non raccolta** in hello **aggiungere la propria app** sezione.</span><span class="sxs-lookup"><span data-stu-id="db07d-221">click **Non-gallery application** in hello **Add your own app** section.</span></span>

7.  <span data-ttu-id="db07d-222">Immettere il nome di hello dell'applicazione hello in hello **nome** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="db07d-222">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="db07d-223">Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="db07d-223">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="db07d-224">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-224">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="db07d-225">Selezionare **basato su SAML Sign-on** in hello **modalità** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="db07d-225">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="db07d-226">Immettere i valori hello necessarie nelle **dominio e gli URL.**</span><span class="sxs-lookup"><span data-stu-id="db07d-226">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="db07d-227">È necessario ottenere questi valori dal fornitore dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-227">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="db07d-228">un'applicazione hello tooconfigure come avviata da IdP SSO, immettere hello URL di risposta e l'identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-228">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2.  <span data-ttu-id="db07d-229">**Facoltativo:** tooconfigure un'applicazione hello come SSO avviato da SP, hello Sign in URL è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="db07d-229">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="db07d-230">In hello **gli attributi utente**, selezionare hello identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="db07d-230">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="db07d-231">**Facoltativo:** fare clic su **visualizzare e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.</span><span class="sxs-lookup"><span data-stu-id="db07d-231">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="db07d-232">un attributo tooadd:</span><span class="sxs-lookup"><span data-stu-id="db07d-232">tooadd an attribute:</span></span>

   1. <span data-ttu-id="db07d-233">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="db07d-233">click **Add attribute**.</span></span> <span data-ttu-id="db07d-234">Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-234">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="db07d-235">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="db07d-235">Click **Save.**</span></span> <span data-ttu-id="db07d-236">Vedrai hello nuovo attributo tabella hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-236">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="db07d-237">Fare clic su **configura &lt;nome applicazione&gt;**  tooaccess documentazione sulla tooconfigure single sign-on nell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-237">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="db07d-238">È inoltre URL AD Azure e certificato richiesto per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-238">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="db07d-239">Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente</span><span class="sxs-lookup"><span data-stu-id="db07d-239">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="db07d-240">tooselect hello identificatore utente o aggiungere gli attributi utente, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-240">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-241">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="db07d-241">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="db07d-242">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-242">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-243">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-243">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-244">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db07d-244">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="db07d-245">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="db07d-245">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="db07d-246">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="db07d-246">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="db07d-247">Selezionare un'applicazione hello è stato configurato single sign-on.</span><span class="sxs-lookup"><span data-stu-id="db07d-247">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="db07d-248">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-248">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="db07d-249">In hello **gli attributi utente** hello di sezione, selezionare un identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="db07d-249">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="db07d-250">Hello opzione selezionata deve toomatch hello previsto valore utente hello tooauthenticate dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-250">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="db07d-251">Azure AD selezionare hello formato attributo NameID hello (ID utente) in base al valore di hello selezionato o per hello formato richiesto da un'applicazione hello in hello AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="db07d-251">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="db07d-252">Per ulteriori informazioni visitare articolo hello [protocollo Single Sign-On SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) in hello sezione NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="db07d-252">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="db07d-253">Fare clic su attributi utente tooadd, **visualizzazione e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.</span><span class="sxs-lookup"><span data-stu-id="db07d-253">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="db07d-254">un attributo tooadd:</span><span class="sxs-lookup"><span data-stu-id="db07d-254">tooadd an attribute:</span></span>

   1. <span data-ttu-id="db07d-255">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="db07d-255">click **Add attribute**.</span></span> <span data-ttu-id="db07d-256">Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-256">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="db07d-257">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="db07d-257">Click **Save.**</span></span> <span data-ttu-id="db07d-258">Vedrai hello nuovo attributo tabella hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-258">You see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="db07d-259">Scaricare i metadati di Azure AD hello o certificato</span><span class="sxs-lookup"><span data-stu-id="db07d-259">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="db07d-260">i metadati dell'applicazione hello toodownload o un certificato da Azure AD, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-260">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-261">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="db07d-261">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="db07d-262">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-262">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-263">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-263">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-264">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db07d-264">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="db07d-265">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="db07d-265">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="db07d-266">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="db07d-266">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="db07d-267">Selezionare un'applicazione hello è stato configurato single sign-on.</span><span class="sxs-lookup"><span data-stu-id="db07d-267">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="db07d-268">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-268">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="db07d-269">Andare troppo**certificato di firma SAML** sezione, quindi fare clic su **scaricare** valore della colonna.</span><span class="sxs-lookup"><span data-stu-id="db07d-269">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="db07d-270">A seconda di quale applicazione hello richiede la configurazione di single sign-on, vedere uno toodownload opzione hello hello Metadata XML o hello certificato.</span><span class="sxs-lookup"><span data-stu-id="db07d-270">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="db07d-271">Azure AD non fornisce i metadati hello tooget URL.</span><span class="sxs-lookup"><span data-stu-id="db07d-271">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="db07d-272">Hello metadati possono essere recuperati solo come un file XML.</span><span class="sxs-lookup"><span data-stu-id="db07d-272">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="db07d-273">Come password tooconfigure single sign-on per un'applicazione di raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="db07d-273">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="db07d-274">un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:</span><span class="sxs-lookup"><span data-stu-id="db07d-274">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="db07d-275">Aggiungere un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="db07d-275">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="db07d-276">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="db07d-276">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="db07d-277">Aggiungere un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="db07d-277">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="db07d-278">un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-278">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-279">Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**</span><span class="sxs-lookup"><span data-stu-id="db07d-279">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="db07d-280">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-280">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-281">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-281">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-282">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db07d-282">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="db07d-283">Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** blade.</span><span class="sxs-lookup"><span data-stu-id="db07d-283">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="db07d-284">In hello **immettere un nome** casella di testo da hello **Aggiungi dalla raccolta hello** sezione, il nome del tipo hello di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-284">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="db07d-285">Selezionare l'applicazione hello da tooconfigure per single sign-on.</span><span class="sxs-lookup"><span data-stu-id="db07d-285">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="db07d-286">Prima di aggiungere un'applicazione hello, è possibile modificarne il nome da hello **nome** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="db07d-286">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="db07d-287">Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="db07d-287">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="db07d-288">Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-288">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="db07d-289">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="db07d-289">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="db07d-290">tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-290">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-291">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="db07d-291">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="db07d-292">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-292">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-293">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-293">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-294">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db07d-294">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="db07d-295">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="db07d-295">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="db07d-296">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="db07d-296">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="db07d-297">Selezionare l'applicazione hello tooconfigure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="db07d-297">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="db07d-298">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-298">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="db07d-299">Modalità di selezione hello **basato su Password Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="db07d-299">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="db07d-300">[Assegnare gli utenti dell'applicazione toohello](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="db07d-300">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="db07d-301">Inoltre, è anche possibile fornire credenziali per conto dell'utente hello selezionando le righe di hello di utenti hello e facendo clic su **credenziali di aggiornamento** e l'immissione di nome utente hello e una password per conto degli utenti hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-301">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="db07d-302">In caso contrario, gli utenti in tooenter richiesta hello credenziali stessi all'avvio.</span><span class="sxs-lookup"><span data-stu-id="db07d-302">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="db07d-303">Come password tooconfigure single sign-on per un'applicazione non-raccolta</span><span class="sxs-lookup"><span data-stu-id="db07d-303">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="db07d-304">un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:</span><span class="sxs-lookup"><span data-stu-id="db07d-304">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="db07d-305">Aggiungere un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="db07d-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="db07d-306">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="db07d-306">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="db07d-307">Aggiungere un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="db07d-307">Add a non-gallery application</span></span>

<span data-ttu-id="db07d-308">un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-308">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-309">Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**.</span><span class="sxs-lookup"><span data-stu-id="db07d-309">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="db07d-310">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-310">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-311">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-311">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-312">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db07d-312">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="db07d-313">Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** blade.</span><span class="sxs-lookup"><span data-stu-id="db07d-313">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="db07d-314">Fare clic su**Applicazione non nella raccolta**.</span><span class="sxs-lookup"><span data-stu-id="db07d-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="db07d-315">Immettere il nome di hello dell'applicazione in hello **nome** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="db07d-315">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="db07d-316">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="db07d-316">Select **Add.**</span></span>

<span data-ttu-id="db07d-317">Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-317">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="db07d-318">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="db07d-318">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="db07d-319">tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-319">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-320">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="db07d-320">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="db07d-321">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-321">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-322">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-322">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-323">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db07d-323">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="db07d-324">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="db07d-324">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="db07d-325">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="db07d-325">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="db07d-326">Selezionare l'applicazione hello tooconfigure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="db07d-326">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="db07d-327">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-327">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="db07d-328">Modalità di selezione hello **basato su Password Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="db07d-328">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="db07d-329">Immettere hello **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="db07d-329">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="db07d-330">Si tratta hello URL in cui gli utenti immettono il nome utente e password toosign in a.</span><span class="sxs-lookup"><span data-stu-id="db07d-330">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="db07d-331">Verificare i campi di accesso hello sono visibili nell'URL hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-331">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="db07d-332">[Assegnare gli utenti dell'applicazione toohello](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="db07d-332">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="db07d-333">Inoltre, è anche possibile fornire credenziali per conto dell'utente hello selezionando le righe di hello di utenti hello e facendo clic su **credenziali di aggiornamento** e l'immissione di nome utente hello e una password per conto degli utenti hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-333">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="db07d-334">In caso contrario, gli utenti in tooenter richiesta hello credenziali stessi all'avvio.</span><span class="sxs-lookup"><span data-stu-id="db07d-334">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="db07d-335">Problemi correlati tooassigning applicazioni toousers</span><span class="sxs-lookup"><span data-stu-id="db07d-335">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="db07d-336">Un utente potrebbe non contenere un'applicazione nel proprio pannello di accesso perché non sono assegnati toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="db07d-336">A user may not be seeing an application on their Access Panel because they are not assigned toohello application.</span></span> <span data-ttu-id="db07d-337">Di seguito sono toocheck alcuni modi:</span><span class="sxs-lookup"><span data-stu-id="db07d-337">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="db07d-338">Verificare se un utente è assegnato toohello applicazione</span><span class="sxs-lookup"><span data-stu-id="db07d-338">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="db07d-339">Come tooassign direttamente un'applicazione utente tooan</span><span class="sxs-lookup"><span data-stu-id="db07d-339">How tooassign a user tooan application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="db07d-340">Verificare se un utente viene assegnata una licenza tooa correlati toohello applicazione</span><span class="sxs-lookup"><span data-stu-id="db07d-340">Check if a user is assigned tooa license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="db07d-341">Come un utente tooa licenza tooassign</span><span class="sxs-lookup"><span data-stu-id="db07d-341">How tooassign a license tooa user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="db07d-342">Verificare se un utente è assegnato toohello applicazione</span><span class="sxs-lookup"><span data-stu-id="db07d-342">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="db07d-343">toocheck se un utente è assegnato toohello applicazione, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-343">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-344">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="db07d-344">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="db07d-345">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-345">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-346">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-346">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-347">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db07d-347">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="db07d-348">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="db07d-348">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="db07d-349">**Ricerca** per nome hello dell'applicazione hello in questione.</span><span class="sxs-lookup"><span data-stu-id="db07d-349">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="db07d-350">Fare clic su **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="db07d-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="db07d-351">Controllare toosee se l'utente è assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="db07d-351">Check toosee if your user is assigned toohello application.</span></span>

   * <span data-ttu-id="db07d-352">In caso contrario, seguire i passaggi di hello in "modalità tooassign direttamente un'applicazione utente tooan" toodo in modo.</span><span class="sxs-lookup"><span data-stu-id="db07d-352">If not follow hello steps in “How tooassign a user tooan application directly” toodo so.</span></span>

### <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="db07d-353">Come tooassign direttamente un'applicazione utente tooan</span><span class="sxs-lookup"><span data-stu-id="db07d-353">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="db07d-354">tooassign uno o più applicazioni tooan utenti direttamente, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-354">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-355">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="db07d-355">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="db07d-356">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-356">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-357">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-357">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-358">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db07d-358">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="db07d-359">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="db07d-359">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="db07d-360">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="db07d-360">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="db07d-361">Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="db07d-361">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="db07d-362">Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-362">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="db07d-363">Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="db07d-363">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="db07d-364">Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="db07d-364">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="db07d-365">Tipo di hello **nome completo** o **indirizzo di posta elettronica** dell'utente hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="db07d-365">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="db07d-366">Passare il mouse su hello **utente** in hello elenco tooreveal un **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="db07d-366">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="db07d-367">Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello dell'utente il toohello utente **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="db07d-367">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="db07d-368">**Facoltativo:** se si desidera troppo**aggiungere più di un utente**, in un altro tipo di **nome completo** o **indirizzo di posta elettronica** in hello **Cerca per nome o l'indirizzo di posta elettronica** casella di ricerca e fare clic su questo toohello utente hello casella di controllo tooadd **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="db07d-368">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="db07d-369">Al termine della selezione utenti, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="db07d-369">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="db07d-370">**Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un ruolo tooassign toohello utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="db07d-370">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="db07d-371">Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="db07d-371">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="db07d-372">Dopo un breve periodo, gli utenti di hello selezionato toolaunch in grado di queste applicazioni in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="db07d-372">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="db07d-373">Controllare se un utente è in una licenza correlati toohello applicazione</span><span class="sxs-lookup"><span data-stu-id="db07d-373">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="db07d-374">toocheck un utente assegnate le licenze, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-374">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-375">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="db07d-375">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="db07d-376">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-376">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-377">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-377">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-378">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-378">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="db07d-379">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="db07d-379">click **All users**.</span></span>

6.  <span data-ttu-id="db07d-380">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="db07d-380">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="db07d-381">Fare clic su **licenze** toosee utente hello licenze è attualmente assegnato.</span><span class="sxs-lookup"><span data-stu-id="db07d-381">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

  * <span data-ttu-id="db07d-382">Se utente hello viene assegnata una licenza di Office tooan tooappear applicazioni di Office di terze parti prima in questo modo su hello nel Pannello di accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="db07d-382">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-user-a-license"></a><span data-ttu-id="db07d-383">Come tooassign una licenza utente</span><span class="sxs-lookup"><span data-stu-id="db07d-383">How tooassign a user a license</span></span> 

<span data-ttu-id="db07d-384">un utente, tooa licenza tooassign procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-384">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-385">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="db07d-385">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="db07d-386">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-386">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-387">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-387">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-388">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-388">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="db07d-389">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="db07d-389">click **All users**.</span></span>

6.  <span data-ttu-id="db07d-390">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="db07d-390">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="db07d-391">Fare clic su **licenze** toosee utente hello licenze è attualmente assegnato.</span><span class="sxs-lookup"><span data-stu-id="db07d-391">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="db07d-392">Fare clic su hello **assegnare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="db07d-392">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="db07d-393">Selezionare **uno o più prodotti** dall'elenco di hello dei prodotti disponibili.</span><span class="sxs-lookup"><span data-stu-id="db07d-393">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="db07d-394">**Parametro facoltativo** fare clic su hello **opzioni assegnazione** toogranularly elemento assegnare i prodotti.</span><span class="sxs-lookup"><span data-stu-id="db07d-394">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="db07d-395">Fare clic su **OK** al termine.</span><span class="sxs-lookup"><span data-stu-id="db07d-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="db07d-396">Fare clic su hello **assegnare** pulsante tooassign questi utente toothis licenze.</span><span class="sxs-lookup"><span data-stu-id="db07d-396">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="db07d-397">Problemi correlati tooassigning applicazioni toogroups</span><span class="sxs-lookup"><span data-stu-id="db07d-397">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="db07d-398">Un utente potrebbe contenere un'applicazione nel proprio pannello di accesso perché fanno parte di un gruppo che dispone di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="db07d-399">Di seguito sono toocheck alcuni modi:</span><span class="sxs-lookup"><span data-stu-id="db07d-399">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="db07d-400">Controllare le appartenenze ai gruppi di un utente </span><span class="sxs-lookup"><span data-stu-id="db07d-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="db07d-401">Come tooassign tooa un'applicazione di gruppo direttamente</span><span class="sxs-lookup"><span data-stu-id="db07d-401">How tooassign an application tooa group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="db07d-402">Controllare se un utente fa parte del gruppo assegnato tooa licenza</span><span class="sxs-lookup"><span data-stu-id="db07d-402">Check if a user is part of group assigned tooa license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="db07d-403">Come un gruppo di licenze tooa tooassign</span><span class="sxs-lookup"><span data-stu-id="db07d-403">How tooassign a license tooa group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="db07d-404">Controllare le appartenenze a gruppi dell'utente</span><span class="sxs-lookup"><span data-stu-id="db07d-404">Check a user’s group memberships</span></span>

<span data-ttu-id="db07d-405">toocheck appartenenza a un gruppo, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-405">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-406">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="db07d-406">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="db07d-407">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-407">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-408">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-408">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-409">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-409">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="db07d-410">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="db07d-410">click **All users**.</span></span>

6.  <span data-ttu-id="db07d-411">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="db07d-411">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="db07d-412">Fare clic su **Gruppi**.</span><span class="sxs-lookup"><span data-stu-id="db07d-412">click **Groups**.</span></span>

8.  <span data-ttu-id="db07d-413">Controllare toosee se l'utente fa parte di un'applicazione toohello gruppo assegnato.</span><span class="sxs-lookup"><span data-stu-id="db07d-413">Check toosee if your user is part of a Group assigned toohello application.</span></span>

  * <span data-ttu-id="db07d-414">Se si desidera tooremove hello utente dal gruppo di hello, **fare clic sulla riga hello** del gruppo di hello e seleziona Elimina.</span><span class="sxs-lookup"><span data-stu-id="db07d-414">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="how-tooassign-an-application-tooa-group-directly"></a><span data-ttu-id="db07d-415">Come tooassign tooa un'applicazione di gruppo direttamente</span><span class="sxs-lookup"><span data-stu-id="db07d-415">How tooassign an application tooa group directly</span></span>

<span data-ttu-id="db07d-416">tooassign uno o più gruppi di applicazioni tooan direttamente, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-416">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-417">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="db07d-417">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="db07d-418">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-418">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-419">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-419">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-420">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db07d-420">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="db07d-421">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="db07d-421">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="db07d-422">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="db07d-422">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="db07d-423">Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="db07d-423">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="db07d-424">Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-424">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="db07d-425">Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="db07d-425">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="db07d-426">Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="db07d-426">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="db07d-427">Tipo di hello **nome del gruppo completo** del gruppo di hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="db07d-427">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="db07d-428">Passare il mouse su hello **gruppo** in hello elenco tooreveal un **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="db07d-428">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="db07d-429">Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello del gruppo toohello l'utente **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="db07d-429">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="db07d-430">**Facoltativo:** se si desidera troppo**aggiungere più di un gruppo**, in un altro tipo di **nome del gruppo completo** in hello **ricerca per nome o indirizzo di posta** casella di ricerca Fare clic su hello casella di controllo tooadd toohello questo gruppo **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="db07d-430">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="db07d-431">Al termine della selezione gruppi, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="db07d-431">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="db07d-432">**Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un toohello tooassign ruolo gruppi di sicurezza selezionato.</span><span class="sxs-lookup"><span data-stu-id="db07d-432">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="db07d-433">Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gruppi selezionati.</span><span class="sxs-lookup"><span data-stu-id="db07d-433">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="db07d-434">Dopo un breve periodo, gli utenti di hello selezionato toolaunch in grado di queste applicazioni in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="db07d-434">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-tooa-license"></a><span data-ttu-id="db07d-435">Controllare se un utente fa parte del gruppo assegnato tooa licenza</span><span class="sxs-lookup"><span data-stu-id="db07d-435">Check if a user is part of group assigned tooa license</span></span>

1.  <span data-ttu-id="db07d-436">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="db07d-436">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="db07d-437">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-437">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-438">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-438">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-439">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-439">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="db07d-440">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="db07d-440">click **All users**.</span></span>

6.  <span data-ttu-id="db07d-441">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="db07d-441">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="db07d-442">Fare clic su **Gruppi**.</span><span class="sxs-lookup"><span data-stu-id="db07d-442">click **Groups**.</span></span>

8.  <span data-ttu-id="db07d-443">Fare clic sulla riga hello di un gruppo specifico.</span><span class="sxs-lookup"><span data-stu-id="db07d-443">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="db07d-444">Fare clic su **licenze** toosee quale gruppo di licenze hello è assegnato tooit.</span><span class="sxs-lookup"><span data-stu-id="db07d-444">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

   * <span data-ttu-id="db07d-445">Se gruppo hello viene assegnata una licenza di Office tooan in che questo potrebbe rendere determinati tooappear applicazioni di Office di terze parti prima hello nel Pannello di accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="db07d-445">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-license-tooa-group"></a><span data-ttu-id="db07d-446">Come un gruppo di licenze tooa tooassign</span><span class="sxs-lookup"><span data-stu-id="db07d-446">How tooassign a license tooa group</span></span>

<span data-ttu-id="db07d-447">un gruppo di licenze tooa tooassign procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="db07d-447">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="db07d-448">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="db07d-448">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="db07d-449">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-449">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="db07d-450">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="db07d-450">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="db07d-451">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-451">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="db07d-452">Fare clic su **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="db07d-452">click **All groups**.</span></span>

6.  <span data-ttu-id="db07d-453">**Ricerca** per gruppo hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="db07d-453">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="db07d-454">Fare clic su **licenze** toosee quale gruppo di licenze hello è attualmente assegnato.</span><span class="sxs-lookup"><span data-stu-id="db07d-454">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="db07d-455">Fare clic su hello **assegnare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="db07d-455">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="db07d-456">Selezionare **uno o più prodotti** dall'elenco di hello dei prodotti disponibili.</span><span class="sxs-lookup"><span data-stu-id="db07d-456">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="db07d-457">**Parametro facoltativo** fare clic su hello **opzioni assegnazione** toogranularly elemento assegnare i prodotti.</span><span class="sxs-lookup"><span data-stu-id="db07d-457">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="db07d-458">Fare clic su **OK** al termine.</span><span class="sxs-lookup"><span data-stu-id="db07d-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="db07d-459">Fare clic su hello **assegnare** pulsante tooassign questi toothis di gruppo di licenze.</span><span class="sxs-lookup"><span data-stu-id="db07d-459">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="db07d-460">L'operazione potrebbe richiedere molto tempo, a seconda delle dimensioni di hello e la complessità del gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="db07d-460">This may take a long time, depending on hello size and complexity of hello group.</span></span>

>[!NOTE]
><span data-ttu-id="db07d-461">toodo questo più velocemente, è consigliabile temporaneamente assegna una licenza toohello utente direttamente.</span><span class="sxs-lookup"><span data-stu-id="db07d-461">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="db07d-462">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="db07d-462">Next steps</span></span>
[<span data-ttu-id="db07d-463">Aggiungere nuovi utenti tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="db07d-463">Add new users tooAzure Active Directory</span></span>](active-directory-users-create-azure-portal.md)

