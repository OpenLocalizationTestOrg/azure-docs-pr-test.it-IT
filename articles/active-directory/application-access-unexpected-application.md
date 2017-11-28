---
title: applicazione aaaUnexpected in un elenco di applicazioni | Documenti Microsoft
description: Come toosee nel tenant di tutte le applicazioni e comprendere come le applicazioni vengono visualizzate nell'elenco di tutte le applicazioni in applicazioni aziendali
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
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="13027-103">Applicazione non prevista nell'elenco delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="13027-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="13027-104">Questo articolo è utile toounderstand modalità di visualizzazione in applicazioni il **tutte le applicazioni** elenco sotto **applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="13027-104">This article help you toounderstand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-toosee-all-applications-in-your-tenant"></a><span data-ttu-id="13027-105">Come toosee tutte le applicazioni nel tenant</span><span class="sxs-lookup"><span data-stu-id="13027-105">How toosee all applications in your tenant</span></span>

<span data-ttu-id="13027-106">toosee tutti hello applicazioni nel tenant, è necessario hello toouse **filtro** controllare tooshow **tutte le applicazioni** in hello **tutte le applicazioni** elenco.</span><span class="sxs-lookup"><span data-stu-id="13027-106">toosee all hello applications in your tenant, you need toouse hello **Filter** control tooshow **All Applications** under hello **All Applications** list.</span></span> <span data-ttu-id="13027-107">toodo, questa procedura hello seguire seguente:</span><span class="sxs-lookup"><span data-stu-id="13027-107">toodo this, follow hello steps below:</span></span>

1.  <span data-ttu-id="13027-108">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="13027-108">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="13027-109">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="13027-109">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="13027-110">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="13027-110">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="13027-111">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="13027-111">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="13027-112">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="13027-112">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="13027-113">Fare clic su hello utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="13027-113">click hello use hello **Filter** control at hello top of hello **All Applications List**.</span></span>

7.  <span data-ttu-id="13027-114">In hello **filtro** blade, hello set **Mostra** opzione troppo**tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="13027-114">On hello **Filter** blade, set hello **Show** option too**All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="13027-115">Perché viene visualizzata un'applicazione specifica nell'elenco di tutte le applicazioni?</span><span class="sxs-lookup"><span data-stu-id="13027-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="13027-116">Quando filtrata troppo**tutte le applicazioni**, hello **tutte le applicazioni** **elenco** Mostra tutti gli oggetti entità servizio nel tenant.</span><span class="sxs-lookup"><span data-stu-id="13027-116">When filtered too**All Applications**, hello **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="13027-117">Gli oggetti entità servizio possono essere visualizzati in questo elenco in diversi modi:</span><span class="sxs-lookup"><span data-stu-id="13027-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="13027-118">Quando si aggiunge un'applicazione dalla raccolta applicazione hello, tra cui:</span><span class="sxs-lookup"><span data-stu-id="13027-118">When you add any application from hello application gallery, including:</span></span>

   1. <span data-ttu-id="13027-119">**Applicazioni della raccolta di Azure AD**: un'applicazione che è già stata integrata per un accesso Single Sign-On con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13027-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="13027-120">**Le applicazioni di Proxy applicazione** : un'applicazione in esecuzione nell'ambiente locale che si desidera tooprovide protetta single-sign-on tooexternally.</span><span class="sxs-lookup"><span data-stu-id="13027-120">**Application Proxy Applications** – An application running in your on-premises environment that you want tooprovide secure single-sign on tooexternally.</span></span>

   3. <span data-ttu-id="13027-121">**Applicazioni sviluppate personalizzato** : hello di un'applicazione che l'organizzazione intende toodevelop nella piattaforma di sviluppo dell'applicazione AD Azure, ma che non esista ancora.</span><span class="sxs-lookup"><span data-stu-id="13027-121">**Custom-developed Applications** – An application that your organization wishes toodevelop on hello Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="13027-122">**Applicazioni non incluse nella raccolta**: tutte le altre applicazioni.</span><span class="sxs-lookup"><span data-stu-id="13027-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="13027-123">Qualsiasi collegamento web da o in qualsiasi applicazione che esegue il rendering di un campo di nome utente e password, supporta i protocolli SAML o OpenID Connect o supporti SCIM che si desidera toointegrate per single sign-on con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13027-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish toointegrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="13027-124">Quando si effettua l'iscrizione o si esegue l'accesso a un'applicazione di terze parti integrata con Azure Active Directory<sup></sup>,</span><span class="sxs-lookup"><span data-stu-id="13027-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="13027-125">ad esempio [Smartsheet](https://app.smartsheet.com/b/home) o [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span><span class="sxs-lookup"><span data-stu-id="13027-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="13027-126">Quando di iscriversi o aggiunta di un utente di tooa licenza o una gruppo tooa prima parte dell'applicazione, come [Microsoft Office 365](http://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="13027-126">When signing up for, or adding a license tooa user or a group tooa first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="13027-127">Quando si aggiunge una nuova registrazione di applicazione tramite la creazione di un'applicazione sviluppata utilizzando hello [Registro di sistema di](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span><span class="sxs-lookup"><span data-stu-id="13027-127">When you add a new application registration by creating a custom-developed application using hello [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="13027-128">Quando si aggiunge una nuova registrazione di applicazione tramite la creazione di un'applicazione sviluppata utilizzando hello [portale di registrazione applicazione v 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span><span class="sxs-lookup"><span data-stu-id="13027-128">When you add a new application registration by creating a custom-developed application using hello [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="13027-129">Quando si aggiunge un'applicazione sviluppata con i [metodi di autenticazione ASP.net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) o con i [Servizi connessi](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx) di Visual Studio .</span><span class="sxs-lookup"><span data-stu-id="13027-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="13027-130">Quando si crea un oggetto entità servizio utilizzando hello [modulo Azure AD PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="13027-130">When you create a service principal object using hello [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="13027-131">Quando si [consenso all'applicazione tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) come dati toouse amministratore nel tenant.</span><span class="sxs-lookup"><span data-stu-id="13027-131">When you [consent tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator toouse data in your tenant.</span></span>

9.  <span data-ttu-id="13027-132">Quando un [consenso dell'utente, applicazione tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse dati nel tenant.</span><span class="sxs-lookup"><span data-stu-id="13027-132">When a [user consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse data in your tenant.</span></span>

10. <span data-ttu-id="13027-133">Quando si abilitano determinati servizi che archiviano dati nel tenant,</span><span class="sxs-lookup"><span data-stu-id="13027-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="13027-134">Un esempio è la reimpostazione della Password, modellata come un toostore dell'entità servizio i criteri di reimpostazione password in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="13027-134">One example of this is Password Reset, which is modeled as a service principal toostore your password reset policy securely.</span></span>

<span data-ttu-id="13027-135">leggere ulteriori informazioni su come le app vengono aggiunti directory tooyour, tooget [come e perché le applicazioni vengono aggiunte AD tooAzure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span><span class="sxs-lookup"><span data-stu-id="13027-135">tooget more details on how apps are added tooyour directory, read [How and why applications are added tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a><span data-ttu-id="13027-136">Voglio tooremove dell'applicazione tooan di assegnazione di un utente specifico o del gruppo</span><span class="sxs-lookup"><span data-stu-id="13027-136">I want tooremove a specific user’s or group’s assignment tooan application</span></span>

<span data-ttu-id="13027-137">tooremove un'applicazione di tooan assegnazione utente o gruppo, seguire i passaggi di hello elencati in hello [rimuovere l'assegnazione di un utente o gruppo da un'applicazione aziendale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) articolo.</span><span class="sxs-lookup"><span data-stu-id="13027-137">tooremove a user or group assignment tooan application, follow hello steps listed in hello [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a><span data-ttu-id="13027-138">Voglio toodisable tutte le applicazioni di tooan di accesso per ogni utente</span><span class="sxs-lookup"><span data-stu-id="13027-138">I want toodisable all access tooan application for every user</span></span>

<span data-ttu-id="13027-139">toodisable tutti utente accessi tooan dell'applicazione, seguire la procedura seguente hello elencata in hello [disabilitare l'accesso degli utenti per un'applicazione aziendale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) articolo.</span><span class="sxs-lookup"><span data-stu-id="13027-139">toodisable all user sign-ins tooan application, follow hello steps listed in hello [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-toodelete-an-application-entirely"></a><span data-ttu-id="13027-140">Voglio toodelete un'applicazione completamente</span><span class="sxs-lookup"><span data-stu-id="13027-140">I want toodelete an application entirely</span></span>

<span data-ttu-id="13027-141">troppo**eliminare un'applicazione**, seguire le istruzioni di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="13027-141">too**delete an application**, follow hello instructions below:</span></span>

1.  <span data-ttu-id="13027-142">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="13027-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="13027-143">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="13027-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="13027-144">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="13027-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="13027-145">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="13027-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="13027-146">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="13027-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="13027-147">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="13027-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="13027-148">Selezionare l'applicazione hello da toodelete.</span><span class="sxs-lookup"><span data-stu-id="13027-148">Select hello application you want toodelete.</span></span>

7.  <span data-ttu-id="13027-149">Una volta che un'applicazione hello caricato, fare clic su **eliminare** icona dell'applicazione principale hello **Panoramica** blade.</span><span class="sxs-lookup"><span data-stu-id="13027-149">Once hello application loads, click **Delete** icon from hello top application’s **Overview** blade.</span></span>

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a><span data-ttu-id="13027-150">Voglio toodisable tutti i futuri consenso operazioni tooany dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="13027-150">I want toodisable all future user consent operations tooany application</span></span>

<span data-ttu-id="13027-151">La disabilitazione di consenso dell'utente per l'intera directory impedire agli utenti finali di consenso tooany applicazione.</span><span class="sxs-lookup"><span data-stu-id="13027-151">Disabling user consent for your entire directory prevent end users from consenting tooany application.</span></span> <span data-ttu-id="13027-152">Gli amministratori possono sempre dare consenso per conto degli utenti.</span><span class="sxs-lookup"><span data-stu-id="13027-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="13027-153">toolearn più sull'applicazione di consenso e motivi per cui è possibile o potrebbe non essere toodo, lettura [consenso dell'amministratore e utente di conoscenza](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="13027-153">toolearn more about application consent, and why you may or may not wish toodo this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="13027-154">troppo**disabilitare tutte le operazioni utente future consenso nella directory intera**, seguire le istruzioni di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="13027-154">too**disable all future user consent operations in your entire directory**, follow hello instructions below:</span></span>

1.  <span data-ttu-id="13027-155">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="13027-155">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="13027-156">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="13027-156">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="13027-157">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="13027-157">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="13027-158">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="13027-158">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="13027-159">Fare clic su **Impostazioni utente**.</span><span class="sxs-lookup"><span data-stu-id="13027-159">click **User settings**.</span></span>

6.  <span data-ttu-id="13027-160">Disabilitare tutte le operazioni di consenso utente future impostazione hello **gli utenti possono consentire App tooaccess i propri dati** attivare o disattivare troppo**n** e fare clic su hello **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="13027-160">Disable all future user consent operations by setting hello **Users can allow apps tooaccess their data** toggle too**No** and click hello **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13027-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="13027-161">Next steps</span></span>
[<span data-ttu-id="13027-162">Gestione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="13027-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
