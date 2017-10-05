---
title: Inserimento dell'applicazione nella raccolta di applicazioni Azure Active Directory
description: Come elencare un'applicazione che supporta l'accesso Single Sign-On nella raccolta di Azure Active Directory | Microsoft Azure
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: cf25772bd9d92b59401aa5da76e6bbd5fa5ee3e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="listing-your-application-in-the-azure-active-directory-application-gallery"></a><span data-ttu-id="08d1a-103">Inserimento dell'applicazione nella raccolta di applicazioni Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08d1a-103">Listing your application in the Azure Active Directory application gallery</span></span>
<span data-ttu-id="08d1a-104">Per inserire un'applicazione che supporta Single Sign-On con Azure Active Directory nella [raccolta di Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), l'applicazione deve innanzitutto implementare una delle modalità di integrazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="08d1a-104">To list an application that supports single sign-on with Azure Active Directory in the [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), the application first needs to implement one of the following integration modes:</span></span>

* <span data-ttu-id="08d1a-105">**OpenID Connect** : integrazione diretta con Azure AD usando OpenID Connect per l'autenticazione e l'API di consenso di Azure AD per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="08d1a-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="08d1a-106">Se si sta iniziando un'integrazione e l'applicazione non supporta SAML, questa è la modalità consigliata.</span><span class="sxs-lookup"><span data-stu-id="08d1a-106">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
* <span data-ttu-id="08d1a-107">**SAML** : l'applicazione può già configurare i provider di identità di terze parti tramite il protocollo SAML.</span><span class="sxs-lookup"><span data-stu-id="08d1a-107">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="08d1a-108">Di seguito è riportato un elenco dei requisiti di ogni modalità.</span><span class="sxs-lookup"><span data-stu-id="08d1a-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="08d1a-109">Integrazione di OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="08d1a-109">OpenID Connect Integration</span></span>
<span data-ttu-id="08d1a-110">Per integrare l'applicazione con Azure AD, seguire [le istruzioni per sviluppatori](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="08d1a-110">To integrate your application with Azure AD, following the [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="08d1a-111">Completare quindi i dati seguenti e inviare all'indirizzo waadpartners@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="08d1a-111">Then complete the questions below and send to waadpartners@microsoft.com.</span></span>

* <span data-ttu-id="08d1a-112">Fornire le credenziali per un tenant o un account di prova con l'applicazione che possono essere usate dal team di Azure AD per testare l'integrazione.</span><span class="sxs-lookup"><span data-stu-id="08d1a-112">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="08d1a-113">Fornire istruzioni su come il team di Azure AD può accedere e connettere un'istanza di Azure AD all'applicazione usando il [framework di consenso di Azure AD](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="08d1a-113">Provide instructions on how the Azure AD team can sign in and connect an instance of Azure AD to your application using the [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="08d1a-114">Fornire eventuali istruzioni aggiuntive necessarie per il team di Azure AD per testare l'accesso Single Sign-On con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="08d1a-114">Provide any further instructions required for the Azure AD team to test single sign-on with your application.</span></span> 
* <span data-ttu-id="08d1a-115">Specificare le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="08d1a-115">Provide the info below:</span></span>

> <span data-ttu-id="08d1a-116">Nome società:</span><span class="sxs-lookup"><span data-stu-id="08d1a-116">Company Name:</span></span>
> 
> <span data-ttu-id="08d1a-117">Sito Web società:</span><span class="sxs-lookup"><span data-stu-id="08d1a-117">Company Website:</span></span>
> 
> <span data-ttu-id="08d1a-118">Nome dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="08d1a-118">Application Name:</span></span>
> 
> <span data-ttu-id="08d1a-119">Descrizione dell'applicazione (max 200 caratteri):</span><span class="sxs-lookup"><span data-stu-id="08d1a-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="08d1a-120">Sito Web dell'applicazione (informazioni):</span><span class="sxs-lookup"><span data-stu-id="08d1a-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="08d1a-121">Sito Web del supporto tecnico dell'applicazione o informazioni di contatto:</span><span class="sxs-lookup"><span data-stu-id="08d1a-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="08d1a-122">ID applicazione dell'applicazione, indicato nei dettagli dell'applicazione all'indirizzo https://portal.azure.com:</span><span class="sxs-lookup"><span data-stu-id="08d1a-122">Application  ID of the application, as shown in the application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="08d1a-123">URL di iscrizione dell'applicazione, cui i clienti accedono per iscriversi e/o acquistare l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="08d1a-123">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="08d1a-124">Scegliere fino a tre categorie a cui associare l'applicazione. Per informazioni sulle categorie disponibili, vedere il Marketplace di Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="08d1a-124">Choose up to three categories for your application to be listed under (for available categories see the Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="08d1a-125">Allegare l'icona piccola dell'applicazione (file PNG, 45x45 pixel, colore di sfondo a tinta unita):</span><span class="sxs-lookup"><span data-stu-id="08d1a-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="08d1a-126">Allegare l'icona grande dell'applicazione (file PNG, 215x215 pixel, colore di sfondo a tinta unita):</span><span class="sxs-lookup"><span data-stu-id="08d1a-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="08d1a-127">Allegare il logo dell'applicazione (file PNG, 150x122 pixel, colore di sfondo a tinta unita):</span><span class="sxs-lookup"><span data-stu-id="08d1a-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="08d1a-128">Integrazione di SAML</span><span class="sxs-lookup"><span data-stu-id="08d1a-128">SAML Integration</span></span>
<span data-ttu-id="08d1a-129">Qualsiasi app che supporta SAML 2.0 può essere integrata direttamente con un tenant di Azure AD usando [queste istruzioni per l'aggiunta di un'applicazione personalizzata](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="08d1a-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions to add a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="08d1a-130">Dopo aver verificato che l'integrazione dell'applicazione funziona con Azure AD, inviare le informazioni seguenti a <mailto:waadpartners@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="08d1a-130">Once you have tested that your application integration works with Azure AD, send the following information to <mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="08d1a-131">Fornire le credenziali per un tenant o un account di prova con l'applicazione che possono essere usate dal team di Azure AD per testare l'integrazione.</span><span class="sxs-lookup"><span data-stu-id="08d1a-131">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="08d1a-132">Fornire l'URL Single Sign-On SAML, l'URL dell'autorità di certificazione (ID entità) e i valori dell'URL di risposta (servizio consumer di asserzione) per l'applicazione, come descritto [qui](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="08d1a-132">Provide the SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="08d1a-133">Se si forniscono in genere questi valori come parte di un file di metadati SAML, inviare anche quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="08d1a-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="08d1a-134">Fornire una breve descrizione di come configurare Azure AD come provider di identità nell'applicazione usando SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="08d1a-134">Provide a brief description of how to configure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="08d1a-135">Se l'applicazione supporta la configurazione di Azure AD come provider di identità attraverso un portale di amministrazione self-service, assicurarsi che le credenziali specificate in precedenza includano la possibilità di impostare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="08d1a-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure the credentials provided above include the ability to set this up.</span></span>
* <span data-ttu-id="08d1a-136">Specificare le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="08d1a-136">Provide the info below:</span></span>

> <span data-ttu-id="08d1a-137">Nome società:</span><span class="sxs-lookup"><span data-stu-id="08d1a-137">Company Name:</span></span>
> 
> <span data-ttu-id="08d1a-138">Sito Web società:</span><span class="sxs-lookup"><span data-stu-id="08d1a-138">Company Website:</span></span>
> 
> <span data-ttu-id="08d1a-139">Nome dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="08d1a-139">Application Name:</span></span>
> 
> <span data-ttu-id="08d1a-140">Descrizione dell'applicazione (max 200 caratteri):</span><span class="sxs-lookup"><span data-stu-id="08d1a-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="08d1a-141">Sito Web dell'applicazione (informazioni):</span><span class="sxs-lookup"><span data-stu-id="08d1a-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="08d1a-142">Sito Web del supporto tecnico dell'applicazione o informazioni di contatto:</span><span class="sxs-lookup"><span data-stu-id="08d1a-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="08d1a-143">URL di iscrizione dell'applicazione, cui i clienti accedono per iscriversi e/o acquistare l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="08d1a-143">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="08d1a-144">Scegliere fino a tre categorie a cui associare l'applicazione. Per informazioni sulle categorie disponibili, vedere il [Marketplace di Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/):</span><span class="sxs-lookup"><span data-stu-id="08d1a-144">Choose up to three categories for your application to be listed under (for available categories see the [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="08d1a-145">Allegare l'icona piccola dell'applicazione (file PNG, 45x45 pixel, colore di sfondo a tinta unita):</span><span class="sxs-lookup"><span data-stu-id="08d1a-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="08d1a-146">Allegare l'icona grande dell'applicazione (file PNG, 215x215 pixel, colore di sfondo a tinta unita):</span><span class="sxs-lookup"><span data-stu-id="08d1a-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="08d1a-147">Allegare il logo dell'applicazione (file PNG, 150x122 pixel, colore di sfondo a tinta unita):</span><span class="sxs-lookup"><span data-stu-id="08d1a-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

