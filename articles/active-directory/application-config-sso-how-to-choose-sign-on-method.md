---
title: Come determinare il metodo Single Sign-On da usare | Microsoft Docs
description: "Comprendere le modalità Single Sign-On supportate da Azure AD e come sceglierne una per l'applicazione d'interesse."
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
ms.openlocfilehash: 80f4a965920fec9cb578c1bee235c7857f37431e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-determine-what-single-sign-on-method-to-use"></a><span data-ttu-id="df496-103">Come determinare il metodo Single Sign-On da usare</span><span class="sxs-lookup"><span data-stu-id="df496-103">How to determine what single-sign on method to use</span></span>

<span data-ttu-id="df496-104">Questo articolo consente di comprendere le modalità Single Sign-On supportate da Azure AD e come sceglierne una per l'applicazione d'interesse.</span><span class="sxs-lookup"><span data-stu-id="df496-104">This article help you to understand the single sign-on modes supported by Azure AD and how to pick which one to choose for the application you are interested in.</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="df496-105">Modalità Single Sign-On e di provisioning supportate da tipi di applicazione specifici</span><span class="sxs-lookup"><span data-stu-id="df496-105">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="df496-106">La tabella seguente descrive le modalità Single Sign-On e di provisioning supportate da ognuno dei tipi di applicazione precedenti.</span><span class="sxs-lookup"><span data-stu-id="df496-106">The table below describes the different single sign-on and provisioning modes supported by each of the above application types.</span></span> <span data-ttu-id="df496-107">È possibile usare questa tabella per comprendere quale applicazione è necessario aggiungere per supportare un obiettivo specifico.</span><span class="sxs-lookup"><span data-stu-id="df496-107">You can use this table to help you to understand which application you need to add to support a specific goal.</span></span>

  ![Tabella tipi di app](./media/application-tables/table1.png)

## <a name="how-to-choose-a-single-sign-on-mode"></a><span data-ttu-id="df496-109">Come scegliere una modalità Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="df496-109">How to choose a single sign-on mode</span></span>

<span data-ttu-id="df496-110">Le modalità **Single Sign-On** supportate per le applicazioni Azure AD sono elencate di seguito.</span><span class="sxs-lookup"><span data-stu-id="df496-110">The supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="df496-111">**Single Sign-On di Azure AD disabilitato**: scegliere la **modalità Single Sign-On di Azure AD disabilitato** se non si è ancora pronti per integrare questa applicazione con Single Sign-On con Azure AD o semplicemente testandola</span><span class="sxs-lookup"><span data-stu-id="df496-111">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="df496-112">**Accesso collegato**: scegliere la **modalità Single Sing-On** [Accesso collegato](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) se si dispone di un'applicazione che è già connessa con una soluzione Single Sign-On esistente o se si desidera pubblicare un semplice collegamento per gli utenti nel [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) o nell'[utilità di avvio applicazioni di Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="df496-112">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="df496-113">**Accesso basato su password**: scegliere la **modalità Single Sign-On** [Accesso basato su password](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) se l'applicazione esegue il rendering di un campo di nome utente e password HTML e si desidera archiviare il nome utente e la password in modo sicuro per essere riprodotti all'applicazione in un secondo momento</span><span class="sxs-lookup"><span data-stu-id="df496-113">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span></span>

-   <span data-ttu-id="df496-114">**Accesso basato su SAML**: scegliere la modalità Single Sign-On [Accesso basato su SAML](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) se l'applicazione supporta i protocolli SAML o OpenID Connect o se si desidera poter eseguire il mapping degli utenti a ruoli specifici dell'applicazione in base alle regole definite nelle attestazioni SAML *(**Nota:** questa opzione non è disponibile quando il proxy dell'applicazione è configurato per un'applicazione)*</span><span class="sxs-lookup"><span data-stu-id="df496-114">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims *(**Note:** this option is not available when the application proxy is configured for an application)*</span></span>

-   <span data-ttu-id="df496-115">**Accesso basato su intestazione**: scegliere la modalità Single Sign-On [Accesso basato su intestazione](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) se si dispone di un'applicazione che usa PingAccess che supporta l'autenticazione basata sull'intestazione HTTP per la quale si desidera che esegua l'accesso Single Sign-On *(**Nota:** questa opzione è disponibile solo quando il proxy dell'applicazione e PingAccess sono configurati per un'applicazione)*</span><span class="sxs-lookup"><span data-stu-id="df496-115">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish to perform single-sign on to *(**Note:** this option is only available when the application proxy and PingAccess is configured for an application)*</span></span>

-   <span data-ttu-id="df496-116">**Autenticazione integrata di Windows**: scegliere la modalità Single Sign-On [Autenticazione integrata di Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) quando si espone un'applicazione WIA locale per la quale si desidera eseguire l'accesso Single Sign-On *(**Nota:** questa opzione è disponibile solo quando il proxy dell'applicazione è configurato per un'applicazione)*</span><span class="sxs-lookup"><span data-stu-id="df496-116">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to *(**Note:** this option is only available when the application proxy is configured for an application)*</span></span>

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="df496-117">Modalità Single Sign-On per le applicazioni personalizzate</span><span class="sxs-lookup"><span data-stu-id="df496-117">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="df496-118">Le applicazioni personalizzate sviluppate tramite l'esperienza [Applicazione personalizzata](#_Custom-Developed_Applications) supportano modalità Single Sign-On aggiuntive non elencate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df496-118">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="df496-119">inclusi i seguenti:</span><span class="sxs-lookup"><span data-stu-id="df496-119">These include:</span></span>

-   <span data-ttu-id="df496-120">Accesso basato su [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code)</span><span class="sxs-lookup"><span data-stu-id="df496-120">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="df496-121">Accesso basato su [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code)</span><span class="sxs-lookup"><span data-stu-id="df496-121">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="df496-122">Accesso basato su [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html)</span><span class="sxs-lookup"><span data-stu-id="df496-122">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="df496-123">Accesso basato su [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference)</span><span class="sxs-lookup"><span data-stu-id="df496-123">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="df496-124">Leggere [Guida per gli sviluppatori di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) per ulteriori informazioni su come creare un'applicazione personalizzata che supporta queste modalità Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="df496-124">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-to-set-an-applications-single-sign-on-mode"></a><span data-ttu-id="df496-125">Come impostare la modalità Single Sign-On di un'applicazione</span><span class="sxs-lookup"><span data-stu-id="df496-125">How to set an application’s single sign-on mode</span></span>

<span data-ttu-id="df496-126">Per impostare la modalità **Single Sign-On** di un'applicazione, seguire queste istruzioni:</span><span class="sxs-lookup"><span data-stu-id="df496-126">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="df496-127">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="df496-127">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="df496-128">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="df496-128">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="df496-129">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="df496-129">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="df496-130">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="df496-130">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="df496-131">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="df496-131">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="df496-132">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'**elenco di tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="df496-132">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="df496-133">Selezionare l'applicazione per cui si desidera configurare l'accesso Single Sign-on</span><span class="sxs-lookup"><span data-stu-id="df496-133">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="df496-134">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="df496-134">Once the application loads, click **Single sign-on** from the application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df496-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="df496-135">Next steps</span></span>
[<span data-ttu-id="df496-136">Fornire l'accesso Single Sign-On alle app con il proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="df496-136">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

