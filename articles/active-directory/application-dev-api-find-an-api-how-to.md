---
title: aaaHow toofind un'API specifica necessaria per un'applicazione sviluppata | Documenti Microsoft
description: "Autorizzazioni hello tooconfigure personalizzato non è presente un'API specifica tooaccess sviluppo di applicazioni Azure AD"
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
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="3eb8b-103">Come toofind un'API specifica necessaria per un'applicazione personalizzata</span><span class="sxs-lookup"><span data-stu-id="3eb8b-103">How toofind a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="3eb8b-104">Accesso tooAPIs richiedono la configurazione di ambiti di accesso e i ruoli.</span><span class="sxs-lookup"><span data-stu-id="3eb8b-104">Access tooAPIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="3eb8b-105">Se si desidera tooexpose tooclient applicazioni API web risorsa dell'applicazione, è necessario tooconfigure gli ambiti di accesso e i ruoli per hello API.</span><span class="sxs-lookup"><span data-stu-id="3eb8b-105">If you want tooexpose your resource application web APIs tooclient applications, you need tooconfigure access scopes and roles for hello API.</span></span> <span data-ttu-id="3eb8b-106">Se si desidera un tooaccess applicazione client un'API web, è necessario tooconfigure autorizzazioni tooaccess hello API nella registrazione dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="3eb8b-106">If you want a client application tooaccess a web API, you need tooconfigure permissions tooaccess hello API in hello app registration.</span></span>

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a><span data-ttu-id="3eb8b-107">Configurazione di una web tooexpose di risorse dell'applicazione API</span><span class="sxs-lookup"><span data-stu-id="3eb8b-107">Configuring a resource application tooexpose web APIs</span></span>

<span data-ttu-id="3eb8b-108">Quando si espone l'API web, hello API da visualizzare in hello **selezionare un'API** elenco durante l'aggiunta di registrazione dell'app tooan di autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="3eb8b-108">When you expose your web API, hello API be displayed in hello **Select an API** list when adding permissions tooan app registration.</span></span> <span data-ttu-id="3eb8b-109">gli ambiti di accesso tooadd, seguire i passaggi di hello illustrati in [aggiunta dell'accesso definisce l'ambito di applicazione della risorsa tooyour](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span><span class="sxs-lookup"><span data-stu-id="3eb8b-109">tooadd access scopes, follow hello steps outlined in [adding access scopes tooyour resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-tooaccess-web-apis"></a><span data-ttu-id="3eb8b-110">Configurazione dell'applicazione client tooaccess web API</span><span class="sxs-lookup"><span data-stu-id="3eb8b-110">Configuring a client application tooaccess web APIs</span></span>

<span data-ttu-id="3eb8b-111">Quando si aggiunge una registrazione dell'app tooyour autorizzazioni, è possibile **aggiungere l'accesso all'API** tooexposed web API.</span><span class="sxs-lookup"><span data-stu-id="3eb8b-111">When you add permissions tooyour app registration, you can **add API access** tooexposed web APIs.</span></span> <span data-ttu-id="3eb8b-112">tooaccess le API web, seguire i passaggi descritti nella procedura hello [aggiungere tooaccess credenziali o le autorizzazioni web API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span><span class="sxs-lookup"><span data-stu-id="3eb8b-112">tooaccess web APIs, follow hello steps outlined in [add credentials or permissions tooaccess web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3eb8b-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3eb8b-113">Next steps</span></span>

-   [<span data-ttu-id="3eb8b-114">Integrazione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3eb8b-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="3eb8b-115">Manifesto dell'applicazione di conoscenza hello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3eb8b-115">Understanding hello Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


