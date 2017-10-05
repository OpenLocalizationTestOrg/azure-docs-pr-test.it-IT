---
title: Come aggiungere un'applicazione multi-tenant alla raccolta di applicazioni di Azure AD | Microsoft Docs
description: Viene illustrato come inserire l'applicazione multi-tenant sviluppata personalizzata nella raccolta di applicazioni di AD Azure
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
ms.openlocfilehash: 208f0d40bd7a8e8f35f16e1fcb09c305d833dbb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-add-a-multi-tenant-application-to-the-azure-ad-application-gallery"></a><span data-ttu-id="26622-103">Come aggiungere un'applicazione multi-tenant alla raccolta di applicazioni di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26622-103">How to add a multi-tenant application to the Azure AD application gallery</span></span>

## <a name="what-is-the-azure-ad-application-gallery"></a><span data-ttu-id="26622-104">Definizione della raccolta di applicazioni di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26622-104">What is the Azure AD Application Gallery?</span></span>

<span data-ttu-id="26622-105">La raccolta di applicazioni di Azure AD è un ottimo modo per esporre l'applicazione a milioni di clienti di Azure Active Directory per ampliare l'impatto e la portata dell'applicazione nel marketplace.</span><span class="sxs-lookup"><span data-stu-id="26622-105">The Azure AD Application Gallery is a great way to get your application in front of all the millions of Azure Active Directory customers to broaden the impact and reach of your application in the marketplace.</span></span> <span data-ttu-id="26622-106">I passaggi seguenti illustrano come inserire l'applicazione nella raccolta di applicazioni di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26622-106">The below steps explain how you can list your application in the Azure AD Application Gallery.</span></span>

## <a name="if-your-application-supports-saml-or-openidconnect"></a><span data-ttu-id="26622-107">Se l'applicazione supporta SAML o OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="26622-107">If your application supports SAML or OpenIDConnect</span></span>
<span data-ttu-id="26622-108">Se si dispone di un'applicazione multi-tenant che si vuole inserire nella raccolta di applicazioni di Azure AD, è prima necessario assicurarsi che l'applicazione supporti una delle tecnologie seguenti Single Sign-On:</span><span class="sxs-lookup"><span data-stu-id="26622-108">If you have a multi-tenant application you'd like to list in the Azure AD Application Gallery, you must first make sure that your application supports one of the following single sign-on technologies:</span></span>

1. <span data-ttu-id="26622-109">**OpenID Connect** : integrazione diretta con Azure AD usando OpenID Connect per l'autenticazione e l'API di consenso di Azure AD per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="26622-109">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="26622-110">Se si sta iniziando un'integrazione e l'applicazione non supporta SAML, questa è la modalità consigliata.</span><span class="sxs-lookup"><span data-stu-id="26622-110">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
2. <span data-ttu-id="26622-111">**SAML** : l'applicazione può già configurare i provider di identità di terze parti tramite il protocollo SAML.</span><span class="sxs-lookup"><span data-stu-id="26622-111">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="26622-112">Se l'applicazione supporta una di queste modalità Single Sign-On e si intende inserirla nella raccolta di applicazioni multi-tenant di Azure AD, è possibile seguire la procedura indicata di seguito nel documento.</span><span class="sxs-lookup"><span data-stu-id="26622-112">If your application supports one of these single sign-on modes and you'd like to list your multi-tenant application in the Azure AD Application Gallery, you can follow the steps in the document below.</span></span> <span data-ttu-id="26622-113">Per iniziare rapidamente, inviare un messaggio di posta elettronica a **waadpartners@microsoft.com**.</span><span class="sxs-lookup"><span data-stu-id="26622-113">To get started quickly send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="if-your-application-does-not-support-saml-or-openidconnect"></a><span data-ttu-id="26622-114">Se l'applicazione non supporta SAML o OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="26622-114">If your application does not support SAML or OpenIDConnect</span></span>
<span data-ttu-id="26622-115">Anche se l'applicazione non supporta una di queste modalità, è comunque possibile integrarla nella raccolta usando la tecnologia Single Sign-On tramite password.</span><span class="sxs-lookup"><span data-stu-id="26622-115">Even if your application does not support one of these modes, we can still integrate it into our gallery using our Password Single Sign-on technology.</span></span> <span data-ttu-id="26622-116">Se si vuole esplorare questa opzione, è possibile inviare un messaggio di posta elettronica a **waadpartners@microsoft.com**.</span><span class="sxs-lookup"><span data-stu-id="26622-116">If you'd like to explore this option, you can send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26622-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="26622-117">Next steps</span></span>
[<span data-ttu-id="26622-118">Inserimento dell'applicazione nella raccolta di applicazioni Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26622-118">How to list your application in the Azure Active Directory application gallery</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)
