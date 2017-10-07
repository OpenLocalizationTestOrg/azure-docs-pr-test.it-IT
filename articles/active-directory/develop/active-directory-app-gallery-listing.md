---
title: aaaListing l'applicazione nella raccolta di hello Azure Active Directory dell'applicazione
description: Come un'applicazione che supporta single sign-on in toolist hello raccolta di Azure Active Directory | Microsoft Azure
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
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a><span data-ttu-id="5143b-103">Elenca l'applicazione nella raccolta di hello Azure Active Directory dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5143b-103">Listing your application in hello Azure Active Directory application gallery</span></span>
<span data-ttu-id="5143b-104">un'applicazione che supporta single sign-on con Azure Active Directory in hello toolist [raccolta di Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), un'applicazione hello deve prima esigenze tooimplement di hello seguenti modalità di integrazione:</span><span class="sxs-lookup"><span data-stu-id="5143b-104">toolist an application that supports single sign-on with Azure Active Directory in hello [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), hello application first needs tooimplement one of hello following integration modes:</span></span>

* <span data-ttu-id="5143b-105">**OpenID Connect** : integrazione diretta con Azure AD Usa OpenID Connect per l'autenticazione e hello consenso di Azure AD API per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="5143b-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and hello Azure AD consent API for configuration.</span></span> <span data-ttu-id="5143b-106">Se si avvia solo un'integrazione e l'applicazione non supporta SAML, questo è la modalità consigliata hello.</span><span class="sxs-lookup"><span data-stu-id="5143b-106">If you are just starting an integration and your application does not support SAML, then this is hello recommend mode.</span></span>
* <span data-ttu-id="5143b-107">**SAML** : l'applicazione contiene già hello possibilità tooconfigure terze parti i provider di identità tramite protocollo SAML hello.</span><span class="sxs-lookup"><span data-stu-id="5143b-107">**SAML** – Your application already has hello ability tooconfigure third-party identity providers using hello SAML protocol.</span></span>

<span data-ttu-id="5143b-108">Di seguito è riportato un elenco dei requisiti di ogni modalità.</span><span class="sxs-lookup"><span data-stu-id="5143b-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="5143b-109">Integrazione di OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="5143b-109">OpenID Connect Integration</span></span>
<span data-ttu-id="5143b-110">toointegrate l'applicazione con Azure AD, hello seguente [le istruzioni per sviluppatori](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="5143b-110">toointegrate your application with Azure AD, following hello [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="5143b-111">Quindi completare alle seguenti domande hello e inviare toowaadpartners@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="5143b-111">Then complete hello questions below and send toowaadpartners@microsoft.com.</span></span>

* <span data-ttu-id="5143b-112">Fornire le credenziali per un tenant di prova o di un account con l'applicazione che può essere utilizzato da hello integrazione hello tootest team di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5143b-112">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="5143b-113">Vengono fornite istruzioni su come hello Azure AD può accedere e connettersi a un'istanza di applicazione di tooyour di Azure AD con hello [framework di consenso di Azure AD](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="5143b-113">Provide instructions on how hello Azure AD team can sign in and connect an instance of Azure AD tooyour application using hello [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="5143b-114">Fornire eventuali altre istruzioni necessarie per hello Azure AD team tootest single sign-on con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5143b-114">Provide any further instructions required for hello Azure AD team tootest single sign-on with your application.</span></span> 
* <span data-ttu-id="5143b-115">Fornire informazioni hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="5143b-115">Provide hello info below:</span></span>

> <span data-ttu-id="5143b-116">Nome società:</span><span class="sxs-lookup"><span data-stu-id="5143b-116">Company Name:</span></span>
> 
> <span data-ttu-id="5143b-117">Sito Web società:</span><span class="sxs-lookup"><span data-stu-id="5143b-117">Company Website:</span></span>
> 
> <span data-ttu-id="5143b-118">Nome dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="5143b-118">Application Name:</span></span>
> 
> <span data-ttu-id="5143b-119">Descrizione dell'applicazione (max 200 caratteri):</span><span class="sxs-lookup"><span data-stu-id="5143b-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="5143b-120">Sito Web dell'applicazione (informazioni):</span><span class="sxs-lookup"><span data-stu-id="5143b-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="5143b-121">Sito Web del supporto tecnico dell'applicazione o informazioni di contatto:</span><span class="sxs-lookup"><span data-stu-id="5143b-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="5143b-122">ID dell'applicazione hello, come illustrato nei dettagli dell'applicazione hello in https://portal.azure.com:</span><span class="sxs-lookup"><span data-stu-id="5143b-122">Application  ID of hello application, as shown in hello application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="5143b-123">URL di iscrizione dell'applicazione esiti di toosign per i clienti e/o acquistare un'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="5143b-123">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="5143b-124">Scegliere le categorie di toothree per l'applicazione di toobe elencati sotto (per le categorie disponibili, vedere hello Azure Active Directory Marketplace):</span><span class="sxs-lookup"><span data-stu-id="5143b-124">Choose up toothree categories for your application toobe listed under (for available categories see hello Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="5143b-125">Allegare l'icona piccola dell'applicazione (file PNG, 45x45 pixel, colore di sfondo a tinta unita):</span><span class="sxs-lookup"><span data-stu-id="5143b-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="5143b-126">Allegare l'icona grande dell'applicazione (file PNG, 215x215 pixel, colore di sfondo a tinta unita):</span><span class="sxs-lookup"><span data-stu-id="5143b-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="5143b-127">Allegare il logo dell'applicazione (file PNG, 150x122 pixel, colore di sfondo a tinta unita):</span><span class="sxs-lookup"><span data-stu-id="5143b-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="5143b-128">Integrazione di SAML</span><span class="sxs-lookup"><span data-stu-id="5143b-128">SAML Integration</span></span>
<span data-ttu-id="5143b-129">Qualsiasi app che supporta SAML 2.0 può integrarsi direttamente con un tenant di Azure AD usando [questi tooadd istruzioni un'applicazione personalizzata](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="5143b-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions tooadd a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="5143b-130">Dopo aver verificato che l'integrazione dell'applicazione funziona con Azure AD, inviare le seguenti informazioni troppo hello<mailto:waadpartners@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="5143b-130">Once you have tested that your application integration works with Azure AD, send hello following information too<mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="5143b-131">Fornire le credenziali per un tenant di prova o di un account con l'applicazione che può essere utilizzato da hello integrazione hello tootest team di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5143b-131">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="5143b-132">Fornire hello SAML URL Sign-On, URL autorità di certificazione (ID entità), e l'URL di risposta (servizio consumer di asserzione) i valori per l'applicazione, come descritto [qui](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="5143b-132">Provide hello SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="5143b-133">Se si forniscono in genere questi valori come parte di un file di metadati SAML, inviare anche quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="5143b-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="5143b-134">Fornire una breve descrizione di come tooconfigure Azure AD come provider di identità dell'applicazione tramite SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="5143b-134">Provide a brief description of how tooconfigure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="5143b-135">Se l'applicazione supporta la configurazione di Azure AD come provider di identità tramite un portale amministrativo self-service, quindi verificare le credenziali di hello fornite in precedenza includono hello possibilità tooset questo backup.</span><span class="sxs-lookup"><span data-stu-id="5143b-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure hello credentials provided above include hello ability tooset this up.</span></span>
* <span data-ttu-id="5143b-136">Fornire informazioni hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="5143b-136">Provide hello info below:</span></span>

> <span data-ttu-id="5143b-137">Nome società:</span><span class="sxs-lookup"><span data-stu-id="5143b-137">Company Name:</span></span>
> 
> <span data-ttu-id="5143b-138">Sito Web società:</span><span class="sxs-lookup"><span data-stu-id="5143b-138">Company Website:</span></span>
> 
> <span data-ttu-id="5143b-139">Nome dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="5143b-139">Application Name:</span></span>
> 
> <span data-ttu-id="5143b-140">Descrizione dell'applicazione (max 200 caratteri):</span><span class="sxs-lookup"><span data-stu-id="5143b-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="5143b-141">Sito Web dell'applicazione (informazioni):</span><span class="sxs-lookup"><span data-stu-id="5143b-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="5143b-142">Sito Web del supporto tecnico dell'applicazione o informazioni di contatto:</span><span class="sxs-lookup"><span data-stu-id="5143b-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="5143b-143">URL di iscrizione dell'applicazione esiti di toosign per i clienti e/o acquistare un'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="5143b-143">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="5143b-144">Scegliere le categorie di toothree per toobe l'applicazione elencati sotto (per le categorie disponibili, vedere hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span><span class="sxs-lookup"><span data-stu-id="5143b-144">Choose up toothree categories for your application toobe listed under (for available categories see hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="5143b-145">Allegare l'icona piccola dell'applicazione (file PNG, 45x45 pixel, colore di sfondo a tinta unita):</span><span class="sxs-lookup"><span data-stu-id="5143b-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="5143b-146">Allegare l'icona grande dell'applicazione (file PNG, 215x215 pixel, colore di sfondo a tinta unita):</span><span class="sxs-lookup"><span data-stu-id="5143b-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="5143b-147">Allegare il logo dell'applicazione (file PNG, 150x122 pixel, colore di sfondo a tinta unita):</span><span class="sxs-lookup"><span data-stu-id="5143b-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

