---
title: Problema nell'installazione dell'estensione del browser per il pannello di accesso dell'applicazione | Microsoft Docs
description: Informazioni su come correggere gli errori comuni riscontrabili durante l'installazione dell'estensione del browser per il pannello di accesso
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
ms.reviewer: japere
ms.openlocfilehash: 8b7327508633e33917d1fa9c1f35ed1bde5a26e1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="problem-installing-the-application-access-panel-browser-extension"></a><span data-ttu-id="9fb1c-103">Problema nell'installazione dell'estensione del browser per il pannello di accesso dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="9fb1c-103">Problem installing the application access panel browser extension</span></span>

<span data-ttu-id="9fb1c-104">Il pannello di accesso è un portale basato sul Web che permette a un utente che ha un account aziendale o di istituto di istruzione in Azure Active Directory (Azure AD) di visualizzare e avviare applicazioni basate sul cloud a cui l'amministratore di Azure AD ha concesso l'accesso.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="9fb1c-105">Un utente dotato di edizioni di Azure AD può anche usare le funzionalità di gestione self-service di gruppi e app tramite il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="9fb1c-106">Il pannello di accesso è separato dal portale di Azure e non richiede una sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="9fb1c-107">Per usare il servizio Single Sign-On (SSO) basato su password nel pannello di accesso, è necessario installare l'estensione del pannello di accesso nel browser dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="9fb1c-108">Questa estensione viene scaricata automaticamente quando un utente seleziona un'applicazione configurata per il servizio Single Sign-On basato su password.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="9fb1c-109">Applicazione dei requisiti del browser per il pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="9fb1c-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="9fb1c-110">Per il pannello di accesso è necessario un browser che supporti JavaScript e in cui sia abilitato CSS.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="9fb1c-111">Per usare il servizio Single Sign-On (SSO) basato su password nel pannello di accesso, è necessario installare l'estensione del pannello di accesso nel browser dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="9fb1c-112">Questa estensione viene scaricata automaticamente quando un utente seleziona un'applicazione configurata per il servizio Single Sign-On basato su password.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="9fb1c-113">Per l'accesso Single Sign-On basato su password il browser dell'utente finale può essere uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="9fb1c-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="9fb1c-114">Internet Explorer 8, 9, 10, 11 su Windows 7 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="9fb1c-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="9fb1c-115">Edge su Windows 10 Anniversary Edition o versioni successive</span><span class="sxs-lookup"><span data-stu-id="9fb1c-115">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="9fb1c-116">Chrome in Windows 7 o versione successiva e MacOS X o versione successiva</span><span class="sxs-lookup"><span data-stu-id="9fb1c-116">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="9fb1c-117">Firefox 26.0 o versione successiva in Windows XP SP2 o versione successiva e in Mac OS X 10.6 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="9fb1c-117">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="9fb1c-118">Come installare l'estensione del browser per il pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="9fb1c-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="9fb1c-119">Per installare l'estensione del browser per il pannello di accesso, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9fb1c-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="9fb1c-120">Aprire il [pannello di accesso](https://myapps.microsoft.com) in uno dei browser supportati e accedere come **utente** ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="9fb1c-121">Fare clic su un'**applicazione con accesso SSO basato su password** nel pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-121">Click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="9fb1c-122">Quando viene richiesto di installare il software, selezionare **Installa ora**.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="9fb1c-123">A seconda del browser in uso, si verrà indirizzati al collegamento per il download.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="9fb1c-124">**Aggiungere** l'estensione al browser.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="9fb1c-125">Se richiesto dal browser, scegliere se **abilitare** o **consentire** l'uso dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="9fb1c-126">Al termine dell'installazione, **riavviare** la sessione del browser.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="9fb1c-127">Accedere al pannello di accesso e verificare se è possibile **avviare** le applicazioni con accesso SSO basato su password.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="9fb1c-128">È anche possibile scaricare l'estensione per Chrome ed Edge dai collegamenti diretti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9fb1c-128">You may also download the extension for Chrome and Edge from the direct links below:</span></span>

-   [<span data-ttu-id="9fb1c-129">Estensione Pannello di accesso per Chrome</span><span class="sxs-lookup"><span data-stu-id="9fb1c-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="9fb1c-130">Estensione Pannello di accesso per Edge</span><span class="sxs-lookup"><span data-stu-id="9fb1c-130">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="9fb1c-131">Impostazione dei Criteri di gruppo per Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="9fb1c-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="9fb1c-132">È possibile impostare Criteri di gruppo che consentono di installare l'estensione del pannello di accesso per Internet Explorer nei computer degli utenti in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="9fb1c-133">I prerequisiti includono:</span><span class="sxs-lookup"><span data-stu-id="9fb1c-133">The prerequisites include:</span></span>

-   <span data-ttu-id="9fb1c-134">[Servizi di dominio Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)è già stato configurato e i computer degli utenti sono stati aggiunti al dominio.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="9fb1c-135">Per modificare l'oggetto Criteri di gruppo è necessaria l'autorizzazione "Modifica impostazione".</span><span class="sxs-lookup"><span data-stu-id="9fb1c-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="9fb1c-136">Questa autorizzazione è assegnata per impostazione predefinita ai membri dei gruppi di sicurezza seguenti: Domain Administrators, Enterprise Administrators e Group Policy Creator Owners.</span><span class="sxs-lookup"><span data-stu-id="9fb1c-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="9fb1c-137">[Altre informazioni](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9fb1c-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="9fb1c-138">Per istruzioni passo passo su come configurare i Criteri di gruppo e distribuirli agli utenti, seguire l'esercitazione [Come distribuire l'estensione Pannello di accesso per Internet Explorer con Criteri di gruppo](active-directory-saas-ie-group-policy.md).</span><span class="sxs-lookup"><span data-stu-id="9fb1c-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="9fb1c-139">Risoluzione dei problemi del pannello di accesso in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="9fb1c-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="9fb1c-140">Per accedere a uno strumento diagnostico e per istruzioni passo passo sulla configurazione dell'estensione per Internet Explorer, seguire la procedura nella sezione sulla [risoluzione dei problemi relativi all'estensione del pannello di accesso per Internet Explorer](active-directory-saas-ie-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="9fb1c-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](active-directory-saas-ie-troubleshooting.md) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="9fb1c-141">Se questi passaggi per la risoluzione dei problemi non risolvono il problema</span><span class="sxs-lookup"><span data-stu-id="9fb1c-141">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="9fb1c-142">Aprire un ticket di supporto con le informazioni seguenti, se disponibili:</span><span class="sxs-lookup"><span data-stu-id="9fb1c-142">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="9fb1c-143">ID errore di correlazione</span><span class="sxs-lookup"><span data-stu-id="9fb1c-143">Correlation error ID</span></span>

-   <span data-ttu-id="9fb1c-144">UPN (indirizzo di posta elettronica dell'utente)</span><span class="sxs-lookup"><span data-stu-id="9fb1c-144">UPN (user email address)</span></span>

-   <span data-ttu-id="9fb1c-145">ID tenant</span><span class="sxs-lookup"><span data-stu-id="9fb1c-145">TenantID</span></span>

-   <span data-ttu-id="9fb1c-146">Tipo di browser</span><span class="sxs-lookup"><span data-stu-id="9fb1c-146">Browser type</span></span>

-   <span data-ttu-id="9fb1c-147">Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore</span><span class="sxs-lookup"><span data-stu-id="9fb1c-147">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="9fb1c-148">Tracce Fiddler</span><span class="sxs-lookup"><span data-stu-id="9fb1c-148">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fb1c-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9fb1c-149">Next steps</span></span>
[<span data-ttu-id="9fb1c-150">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9fb1c-150">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
