---
title: Come scegliere il tipo di applicazione da usare durante l'aggiunta di un'applicazione | Microsoft Docs
description: "Informazioni sui tipi di applicazioni supportate che è possibile integrare in Azure AD e sulle opzioni di configurazione correlate"
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
ms.openlocfilehash: e0d41d1933531c2c633613bcbc1bbcbf075d6a69
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-choose-which-application-type-to-use-when-adding-an-application"></a><span data-ttu-id="4c554-103">Come scegliere il tipo di applicazione da usare durante l'aggiunta di un'applicazione</span><span class="sxs-lookup"><span data-stu-id="4c554-103">How to choose which application type to use when adding an application</span></span>

<span data-ttu-id="4c554-104">Questo articolo consente di comprendere i quattro principali tipi di applicazioni che è possibile integrare con Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4c554-104">This article help you to understand the four main types of applications you can integrate with Azure AD:</span></span>

* <span data-ttu-id="4c554-105">Applicazioni supportate da ciascuno di essi</span><span class="sxs-lookup"><span data-stu-id="4c554-105">What is supported by each of them</span></span>
* <span data-ttu-id="4c554-106">Motivo per cui scegliere una determinata applicazione</span><span class="sxs-lookup"><span data-stu-id="4c554-106">Why you might choose which application</span></span>
* <span data-ttu-id="4c554-107">Come configurare le proprietà di base di tali dell'applicazione, ad esempio in che modo si esegue il **provisioning** dell'utente o quale tecnologia **Single Sign-On** usare.</span><span class="sxs-lookup"><span data-stu-id="4c554-107">How to configure those application’s core properties, like how users are **provisioned**, or what **single sign-on** technology to use.</span></span>

## <a name="supported-application-types-in-azure-ad"></a><span data-ttu-id="4c554-108">Tipi di applicazioni supportate in Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c554-108">Supported application types in Azure AD</span></span>

<span data-ttu-id="4c554-109">Azure AD supporta quattro principali tipi di applicazione che è possibile aggiungere tramite la funzionalità **Aggiungi** disponibile in **Applicazioni Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="4c554-109">Azure AD supports four main application types that you can add using the **Add** feature found under **Enterprise Applications**.</span></span> <span data-ttu-id="4c554-110">inclusi i seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c554-110">These include:</span></span>

-   <span data-ttu-id="4c554-111">**Applicazioni della raccolta di Azure AD**: un'applicazione che è già stata integrata per un accesso Single Sign-On con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c554-111">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

-   <span data-ttu-id="4c554-112">**Applicazioni del proxy applicazioni**: un'applicazione in esecuzione nell'ambiente locale per cui si vuole specificare un punto di accesso singolo esterno.</span><span class="sxs-lookup"><span data-stu-id="4c554-112">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

-   <span data-ttu-id="4c554-113">**Applicazioni personalizzate**: un'applicazione che l'organizzazione vuole sviluppare nella piattaforma di sviluppo delle applicazioni di Azure AD, ma che non è ancora disponibile.</span><span class="sxs-lookup"><span data-stu-id="4c554-113">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

-   <span data-ttu-id="4c554-114">**Applicazioni non incluse nella raccolta**: tutte le altre applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4c554-114">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="4c554-115">Qualsiasi collegamento Web o qualsiasi applicazione che usa un campo di nome utente e password supporta i protocolli SAML o OpenID Connect o supporta SCIM che può essere integrato per un accesso Single Sign-On con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c554-115">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

## <a name="features-and-capabilities-supported-by-all-the-above-application-types"></a><span data-ttu-id="4c554-116">Funzionalità e capacità supportate dai tipi di applicazione precedente</span><span class="sxs-lookup"><span data-stu-id="4c554-116">Features and capabilities supported by all the above application types</span></span>

<span data-ttu-id="4c554-117">Le seguenti funzionalità sono supportate dai quattro tipi di applicazione indicati in precedenza in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4c554-117">The following features are supported by any of the above 4 application types in Azure AD:</span></span>

-   <span data-ttu-id="4c554-118">**Avvio rapido**: consente l'uso rapido di un'applicazione tramite una [semplice procedura di distribuzione](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span><span class="sxs-lookup"><span data-stu-id="4c554-118">**Quick start** – get going with an application quickly by following [simple deployment steps](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span></span>

-   <span data-ttu-id="4c554-119">**Gestione generale delle proprietà**: consente di ottenere un [collegamento diretto](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) a un'applicazione, [la personalizzazione del marchio](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) di un'applicazione o di [disabilitare l'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) per tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="4c554-119">**General properties management** – get a [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) to an application, [customize the branding](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) of an application, or [disable the application](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) for all users.</span></span>

-   <span data-ttu-id="4c554-120">**Gestione utenti e gruppi**: consente di [assegnare](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) o [rimuovere](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) utenti e gruppi da un'applicazione e, facoltativamente, assegnare i ruoli specifici dell'applicazione a cui gli utenti e i gruppi hanno accesso</span><span class="sxs-lookup"><span data-stu-id="4c554-120">**User and group management** – [assign](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) or [remove](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) users and groups to an application, and optionally assign the specific application roles these users and groups have access to</span></span>

-   <span data-ttu-id="4c554-121">**Accesso alle applicazioni self-service**: consente agli utenti di richiedere l'[accesso alle applicazioni self-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) per un'applicazione dai pannelli di accesso dell'applicazione aggiungendo direttamente un'applicazione o, facoltativamente, [aggiungendola a un gruppo abilitato al self-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) che richiede l'approvazione business lungo il percorso</span><span class="sxs-lookup"><span data-stu-id="4c554-121">**Self-service application access** – enable your users to request [self-service application access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to an application from their Application Access Panels either by adding an application directly or [joining a self-service enabled group](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), optionally requiring business approval along the way</span></span>

-   <span data-ttu-id="4c554-122">**Log di accesso**: consentono di vedere [tutti gli accessi a un'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) o tutte le applicazioni</span><span class="sxs-lookup"><span data-stu-id="4c554-122">**Sign-in logs** – see [all the sign-ins to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), or all your applications</span></span>

-   <span data-ttu-id="4c554-123">**Registri di controllo**: consentono di vedere i [registri di controllo dettagliati sulle modifiche a un'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) o per tutte le applicazioni</span><span class="sxs-lookup"><span data-stu-id="4c554-123">**Audit logs** – see [detailed audit logs about modifications to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), or to all your applications</span></span>

-   <span data-ttu-id="4c554-124">**Accesso condizionale e basato sui rischi**: consente di impostare potenti [regole di accesso basate sulle condizioni](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) che vengono applicate quando gli utenti tentano di accedere a un'applicazione specifica</span><span class="sxs-lookup"><span data-stu-id="4c554-124">**Conditional and risk-based access** – set powerful [condition-based access rules](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) that are enforced when users attempt to sign in to a specific application</span></span>

-   <span data-ttu-id="4c554-125">**Visualizzazione autorizzazioni** : consente di visualizzare le [autorizzazioni OAuth2](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) a cui ha accesso un'applicazione nella directory da un unico punto</span><span class="sxs-lookup"><span data-stu-id="4c554-125">**Permissions view** – view any of the [OAuth2 permissions](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) an application has access to in your directory from a single place</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="4c554-126">Modalità Single Sign-On e di provisioning supportate da tipi di applicazione specifici</span><span class="sxs-lookup"><span data-stu-id="4c554-126">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="4c554-127">La tabella seguente descrive le modalità Single Sign-On e di provisioning supportate da ognuno dei tipi di applicazione precedenti.</span><span class="sxs-lookup"><span data-stu-id="4c554-127">The table below describes the different single sign-on and provisioning modes supported by each of the above application types.</span></span> <span data-ttu-id="4c554-128">È possibile usare questa tabella per comprendere quale applicazione è necessario aggiungere per supportare un obiettivo specifico.</span><span class="sxs-lookup"><span data-stu-id="4c554-128">You can use this table to help you to understand which application you need to add to support a specific goal.</span></span>

  ![Tabella tipi di app](./media/application-tables/table1.png)

## <a name="how-to-choose-a-single-sign-on-mode"></a><span data-ttu-id="4c554-130">Come scegliere una modalità Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4c554-130">How to choose a single sign-on mode</span></span>

<span data-ttu-id="4c554-131">Le modalità **Single Sign-On** supportate per le applicazioni Azure AD sono elencate di seguito.</span><span class="sxs-lookup"><span data-stu-id="4c554-131">The supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="4c554-132">**Single Sign-On di Azure AD disabilitato**: scegliere la **modalità Single Sign-On di Azure AD disabilitato** se non si è ancora pronti per integrare questa applicazione con Single Sign-On con Azure AD o semplicemente testandola</span><span class="sxs-lookup"><span data-stu-id="4c554-132">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="4c554-133">**Accesso collegato**: scegliere la **modalità Single Sing-On** [Accesso collegato](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) se si dispone di un'applicazione che è già connessa con una soluzione Single Sign-On esistente o se si desidera pubblicare un semplice collegamento per gli utenti nel [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) o nell'[utilità di avvio applicazioni di Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="4c554-133">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="4c554-134">**Accesso basato su password**: scegliere la **modalità Single Sign-On** [Accesso basato su password](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) se l'applicazione esegue il rendering di un campo di nome utente e password HTML e si desidera archiviare il nome utente e la password in modo sicuro per essere riprodotti all'applicazione in un secondo momento</span><span class="sxs-lookup"><span data-stu-id="4c554-134">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span></span>

-   <span data-ttu-id="4c554-135">**Accesso basato su SAML**: scegliere la modalità Single Sign-On [Accesso basato su SAML](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) se l'applicazione supporta i protocolli SAML oppure OpenID Connect o se si desidera poter eseguire il mapping degli utenti a ruoli specifici dell'applicazione in base alle regole definite nelle attestazioni SAML *</span><span class="sxs-lookup"><span data-stu-id="4c554-135">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims *</span></span>

   >[!NOTE]
   ><span data-ttu-id="4c554-136">Questa opzione non è disponibile quando il proxy dell'applicazione è configurato per un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4c554-136">This option is not available when the application proxy is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="4c554-137">**Accesso basato su intestazione**: scegliere la modalità Single Sign-On [Accesso basato su intestazione](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) se si dispone di un'applicazione che usa PingAccess che supporta l'autenticazione basata sull'intestazione HTTP per la quale si desidera eseguire l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4c554-137">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish to perform single-sign on to</span></span> 

   >[!NOTE]
   ><span data-ttu-id="4c554-138">Questa opzione è disponibile solo quando il proxy dell'applicazione e PingAccess sono configurati per un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4c554-138">This option is only available when the application proxy and PingAccess is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="4c554-139">**Autenticazione integrata di Windows**: scegliere la modalità Single Sign-On [Autenticazione integrata di Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) quando si espone un'applicazione WIA locale per la quale si desidera eseguire l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4c554-139">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to</span></span> 

   >[!NOTE]
   ><span data-ttu-id="4c554-140">Questa opzione è disponibile solo quando il proxy dell'applicazione è configurato per un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4c554-140">This option is only available when the application proxy is configured for an application.</span></span>
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="4c554-141">Modalità Single Sign-On per le applicazioni personalizzate</span><span class="sxs-lookup"><span data-stu-id="4c554-141">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="4c554-142">Le applicazioni personalizzate sviluppate tramite l'esperienza [Applicazione personalizzata](#_Custom-Developed_Applications) supportano modalità Single Sign-On aggiuntive non elencate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4c554-142">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="4c554-143">inclusi i seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c554-143">These include:</span></span>

-   <span data-ttu-id="4c554-144">Accesso basato su [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code)</span><span class="sxs-lookup"><span data-stu-id="4c554-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="4c554-145">Accesso basato su [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code)</span><span class="sxs-lookup"><span data-stu-id="4c554-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="4c554-146">Accesso basato su [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html)</span><span class="sxs-lookup"><span data-stu-id="4c554-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="4c554-147">Accesso basato su [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference)</span><span class="sxs-lookup"><span data-stu-id="4c554-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="4c554-148">Leggere [Guida per gli sviluppatori di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) per ulteriori informazioni su come creare un'applicazione personalizzata che supporta queste modalità Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="4c554-148">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-to-set-an-applications-single-sign-on-mode"></a><span data-ttu-id="4c554-149">Come impostare la modalità Single Sign-On di un'applicazione</span><span class="sxs-lookup"><span data-stu-id="4c554-149">How to set an application’s single sign-on mode</span></span>

<span data-ttu-id="4c554-150">Per impostare la modalità **Single Sign-On** di un'applicazione, seguire queste istruzioni:</span><span class="sxs-lookup"><span data-stu-id="4c554-150">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="4c554-151">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="4c554-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4c554-152">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="4c554-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4c554-153">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c554-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4c554-154">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4c554-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4c554-155">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4c554-155">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4c554-156">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'**elenco di tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4c554-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4c554-157">Selezionare l'applicazione per cui si desidera configurare l'accesso Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="4c554-157">Select the application for which you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4c554-158">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4c554-158">Once the application loads, click **Single sign-on** from the application’s left hand navigation menu.</span></span>

## <a name="how-to-choose-a-provisioning-mode"></a><span data-ttu-id="4c554-159">Come scegliere una modalità di provisioning</span><span class="sxs-lookup"><span data-stu-id="4c554-159">How to choose a provisioning mode</span></span>

-   <span data-ttu-id="4c554-160">**Provisioning manuale**: scegliere la modalità di provisioning [manuale](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) se si dispone di account esistenti o si desidera gestire gli account per l'applicazione all'esterno di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c554-160">**Manual Provisioning** – choose the [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) provisioning mode if you have existing accounts, or wish to manage accounts for this application outside of Azure AD.</span></span>

-   <span data-ttu-id="4c554-161">**Provisioning automatico**: scegliere la **modalità di provisioning** [automatica](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning)se si desidera abilitare il provisioning automatico basato su API e/o il deprovisioning degli account utente per questa applicazione</span><span class="sxs-lookup"><span data-stu-id="4c554-161">**Automatic Provisioning** – choose the [Automatic](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **provisioning mode** if you want to enable automatic API-based provisioning and/or de-provisioning of user accounts to this application</span></span> 

   >[!NOTE]
   ><span data-ttu-id="4c554-162">Questa opzione è disponibile solo per le applicazioni all'interno della categoria **in primo piano** della [Raccolta di applicazioni di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="4c554-162">This option is available only for applications within the **featured** category of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span></span>
   >
   >

-   <span data-ttu-id="4c554-163">**Provisioning automatico basato su SCIM**: usare il [provisioning automatico basato su SCIM](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) se un'applicazione supporta il protocollo SCIM per il rilevamento di modifiche a utenti e gruppi, emessi automaticamente per le modifiche a tutte le applicazioni integrate in Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c554-163">**SCIM-based Automatic Provisioning** – use [SCIM-based Automatic Provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) if your application supports the SCIM protocol for detecting changes to users and groups, which are automatically emitted for changes to any application integrated with Azure AD</span></span> 

   >[!NOTE]
   ><span data-ttu-id="4c554-164">Questa opzione non è elencata come una modalità specifica di provisioning, ma è abilitata per impostazione predefinita per tutte le applicazioni integrate in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c554-164">This option is not listed as a specific provisioning mode, but is enabled by default for all applications that are integrated with Azure AD.</span></span>
   >
   >

## <a name="how-to-set-an-applications-provisioning-mode"></a><span data-ttu-id="4c554-165">Come impostare la modalità di provisioning di un'applicazione</span><span class="sxs-lookup"><span data-stu-id="4c554-165">How to set an application’s provisioning mode</span></span>

<span data-ttu-id="4c554-166">Per impostare la modalità di **provisioning** di un'applicazione, seguire queste istruzioni:</span><span class="sxs-lookup"><span data-stu-id="4c554-166">To set an application’s **provisioning** mode, follow the instructions below:</span></span>

<span data-ttu-id="4c554-167">Per impostare la modalità **Single Sign-On** di un'applicazione, seguire queste istruzioni:</span><span class="sxs-lookup"><span data-stu-id="4c554-167">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="4c554-168">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="4c554-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4c554-169">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="4c554-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4c554-170">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c554-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4c554-171">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4c554-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4c554-172">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4c554-172">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4c554-173">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'**elenco di tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4c554-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4c554-174">Selezionare l'applicazione per cui si desidera configurare il provisioning.</span><span class="sxs-lookup"><span data-stu-id="4c554-174">Select the application for which you want to configure provisioning.</span></span>

7.  <span data-ttu-id="4c554-175">Dopo il caricamento dell'applicazione, fare clic su **Provisioning** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4c554-175">Once the application loads, click **Provisioning** from the application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c554-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4c554-176">Next steps</span></span>
[<span data-ttu-id="4c554-177">Gestione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c554-177">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
