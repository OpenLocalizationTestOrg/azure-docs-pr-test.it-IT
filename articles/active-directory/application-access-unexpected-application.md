---
title: Applicazione non prevista nell'elenco delle applicazioni | Microsoft Docs
description: Come visualizzare tutte le applicazioni nel tenant e capire come le applicazioni vengono visualizzate nell'elenco Tutte le applicazioni in Applicazioni aziendali
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
ms.openlocfilehash: 0f8136cb066fa6e3e4a8dd06e34b9f866e3916f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="919e7-103">Applicazione non prevista nell'elenco delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="919e7-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="919e7-104">Questo articolo illustra come vengono visualizzate le applicazioni nell'elenco **Tutte le applicazioni** in **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="919e7-104">This article help you to understand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-to-see-all-applications-in-your-tenant"></a><span data-ttu-id="919e7-105">Come visualizzare tutte le applicazioni nel tenant</span><span class="sxs-lookup"><span data-stu-id="919e7-105">How to see all applications in your tenant</span></span>

<span data-ttu-id="919e7-106">Per visualizzare tutte le applicazioni nel tenant, è necessario usare il controllo **Filtro** per visualizzare **Tutte le applicazioni** nell'elenco **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="919e7-106">To see all the applications in your tenant, you need to use the **Filter** control to show **All Applications** under the **All Applications** list.</span></span> <span data-ttu-id="919e7-107">A questo scopo, eseguire la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="919e7-107">To do this, follow the steps below:</span></span>

1.  <span data-ttu-id="919e7-108">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **coamministratore.**</span><span class="sxs-lookup"><span data-stu-id="919e7-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="919e7-109">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="919e7-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="919e7-110">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="919e7-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="919e7-111">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="919e7-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="919e7-112">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="919e7-112">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="919e7-113">Fare clic sul controllo **Filtro** all'inizio dell'**elenco Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="919e7-113">click the use the **Filter** control at the top of the **All Applications List**.</span></span>

7.  <span data-ttu-id="919e7-114">Nel pannello del **filtro** impostare l'opzione **Mostra** su **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="919e7-114">On the **Filter** blade, set the **Show** option to **All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="919e7-115">Perché viene visualizzata un'applicazione specifica nell'elenco di tutte le applicazioni?</span><span class="sxs-lookup"><span data-stu-id="919e7-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="919e7-116">Quando si imposta il filtro su **Tutte le applicazioni**, l'**elenco** di **tutte le applicazioni** visualizza ogni oggetto entità servizio nel tenant.</span><span class="sxs-lookup"><span data-stu-id="919e7-116">When filtered to **All Applications**, the **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="919e7-117">Gli oggetti entità servizio possono essere visualizzati in questo elenco in diversi modi:</span><span class="sxs-lookup"><span data-stu-id="919e7-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="919e7-118">Quando si aggiunge un'applicazione dalla raccolta di applicazioni, incluse:</span><span class="sxs-lookup"><span data-stu-id="919e7-118">When you add any application from the application gallery, including:</span></span>

   1. <span data-ttu-id="919e7-119">**Applicazioni della raccolta di Azure AD**: un'applicazione che è già stata integrata per un accesso Single Sign-On con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="919e7-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="919e7-120">**Applicazioni del proxy applicazioni**: un'applicazione in esecuzione nell'ambiente locale per cui si vuole specificare un punto di accesso singolo esterno.</span><span class="sxs-lookup"><span data-stu-id="919e7-120">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

   3. <span data-ttu-id="919e7-121">**Applicazioni personalizzate**: un'applicazione che l'organizzazione vuole sviluppare nella piattaforma di sviluppo delle applicazioni di Azure AD, ma che non è ancora disponibile.</span><span class="sxs-lookup"><span data-stu-id="919e7-121">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="919e7-122">**Applicazioni non incluse nella raccolta**: tutte le altre applicazioni.</span><span class="sxs-lookup"><span data-stu-id="919e7-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="919e7-123">Qualsiasi collegamento Web o qualsiasi applicazione che usa un campo di nome utente e password supporta i protocolli SAML o OpenID Connect o supporta SCIM che può essere integrato per un accesso Single Sign-On con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="919e7-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="919e7-124">Quando si effettua l'iscrizione o si esegue l'accesso a un'applicazione di terze parti integrata con Azure Active Directory<sup></sup>,</span><span class="sxs-lookup"><span data-stu-id="919e7-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="919e7-125">ad esempio [Smartsheet](https://app.smartsheet.com/b/home) o [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span><span class="sxs-lookup"><span data-stu-id="919e7-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="919e7-126">Quando si esegue l'accesso o si aggiunge una licenza a un utente o gruppo per un'applicazione proprietaria, ad esempio [Microsoft Office 365](http://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="919e7-126">When signing up for, or adding a license to a user or a group to a first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="919e7-127">Quando si aggiunge una nuova registrazione di applicazione tramite la creazione di un'applicazione personalizzata usando [Registro applicazioni](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span><span class="sxs-lookup"><span data-stu-id="919e7-127">When you add a new application registration by creating a custom-developed application using the [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="919e7-128">Quando si aggiunge una nuova registrazione di applicazione tramite la creazione di un'applicazione personalizzata usando il [portale di registrazione delle applicazioni V2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span><span class="sxs-lookup"><span data-stu-id="919e7-128">When you add a new application registration by creating a custom-developed application using the [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="919e7-129">Quando si aggiunge un'applicazione sviluppata con i [metodi di autenticazione ASP.net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) o con i [Servizi connessi](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx) di Visual Studio .</span><span class="sxs-lookup"><span data-stu-id="919e7-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="919e7-130">Quando si crea un oggetto entità servizio usando il [modulo Azure AD PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="919e7-130">When you create a service principal object using the [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="919e7-131">Quando un amministratore [concede l'autorizzazione a un'applicazione](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) di usare i dati nel tenant.</span><span class="sxs-lookup"><span data-stu-id="919e7-131">When you [consent to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator to use data in your tenant.</span></span>

9.  <span data-ttu-id="919e7-132">Quando un [utente consente a un'applicazione](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) di usare i dati nel tenant.</span><span class="sxs-lookup"><span data-stu-id="919e7-132">When a [user consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to use data in your tenant.</span></span>

10. <span data-ttu-id="919e7-133">Quando si abilitano determinati servizi che archiviano dati nel tenant,</span><span class="sxs-lookup"><span data-stu-id="919e7-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="919e7-134">ad esempio la reimpostazione della password, basata su un modello di un'entità servizio per archiviare in modo sicuro i criteri di reimpostazione delle password.</span><span class="sxs-lookup"><span data-stu-id="919e7-134">One example of this is Password Reset, which is modeled as a service principal to store your password reset policy securely.</span></span>

<span data-ttu-id="919e7-135">Per ottenere altre informazioni dettagliate sull'aggiunta di app alla directory, vedere [Come vengono aggiunte le applicazioni in Azure AD e perché](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span><span class="sxs-lookup"><span data-stu-id="919e7-135">To get more details on how apps are added to your directory, read [How and why applications are added to Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="919e7-136">Si vuole rimuovere un'assegnazione specifica di un utente o gruppo a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="919e7-136">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="919e7-137">Per rimuovere un'assegnazione di un utente o di un gruppo da un'applicazione, seguire i passaggi elencati nell'articolo [Rimuovere l'assegnazione di un utente o un gruppo da un'app aziendale in anteprima di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="919e7-137">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-to-disable-all-access-to-an-application-for-every-user"></a><span data-ttu-id="919e7-138">Si vuole disabilitare tutti gli accessi a un'applicazione per tutti gli utenti</span><span class="sxs-lookup"><span data-stu-id="919e7-138">I want to disable all access to an application for every user</span></span>

<span data-ttu-id="919e7-139">Per disabilitare tutti gli accessi utente a un'applicazione, seguire i passaggi elencati nell'articolo [Disabilitare gli accessi utente per un'app aziendale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="919e7-139">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="919e7-140">Si vuole eliminare completamente un'applicazione</span><span class="sxs-lookup"><span data-stu-id="919e7-140">I want to delete an application entirely</span></span>

<span data-ttu-id="919e7-141">Per **eliminare un'applicazione**, seguire queste istruzioni:</span><span class="sxs-lookup"><span data-stu-id="919e7-141">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="919e7-142">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="919e7-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="919e7-143">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="919e7-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="919e7-144">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="919e7-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="919e7-145">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="919e7-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="919e7-146">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="919e7-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="919e7-147">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'**elenco di tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="919e7-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="919e7-148">Selezionare l'applicazione che si desidera eliminare.</span><span class="sxs-lookup"><span data-stu-id="919e7-148">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="919e7-149">Dopo il caricamento dell'applicazione, fare clic sull'icona **Elimina** che si trova nella parte superiore del pannello **Panoramica** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="919e7-149">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="919e7-150">Si vuole disabilitare tutte le operazioni future di consenso da parte dell'utente a tutte le applicazioni</span><span class="sxs-lookup"><span data-stu-id="919e7-150">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="919e7-151">La disabilitazione di consenso da parte dell'utente per l'intera directory impedisce agli utenti finali di consentire l'accesso a qualsiasi applicazione.</span><span class="sxs-lookup"><span data-stu-id="919e7-151">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="919e7-152">Gli amministratori possono sempre dare consenso per conto degli utenti.</span><span class="sxs-lookup"><span data-stu-id="919e7-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="919e7-153">Per informazioni sul consenso alle applicazioni e sui motivi per cui si desideri dare o meno consenso, leggere [Informazioni sul consenso dell'utente e dell'amministratore](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="919e7-153">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="919e7-154">Per **disabilitare tutte le operazioni future di consenso degli utenti nella directory intera**, seguire queste istruzioni:</span><span class="sxs-lookup"><span data-stu-id="919e7-154">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="919e7-155">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="919e7-155">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="919e7-156">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="919e7-156">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="919e7-157">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="919e7-157">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="919e7-158">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="919e7-158">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="919e7-159">Fare clic su **Impostazioni utente**.</span><span class="sxs-lookup"><span data-stu-id="919e7-159">click **User settings**.</span></span>

6.  <span data-ttu-id="919e7-160">Disabilitare tutte le future operazioni di consenso degli utenti impostando l'opzione **Gli utenti possono consentire alle app di accedere ai propri dati** su **No** e facendo clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="919e7-160">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="919e7-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="919e7-161">Next steps</span></span>
[<span data-ttu-id="919e7-162">Gestione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="919e7-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
