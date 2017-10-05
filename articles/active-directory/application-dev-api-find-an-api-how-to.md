---
title: Come trovare un'API specifica necessaria per un'applicazione personalizzata | Microsoft Docs
description: Informazioni su come configurare le autorizzazioni necessarie per accedere a un'API specifica nell'applicazione Azure AD personalizzata
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
ms.openlocfilehash: e0c07fd030339d025894520500d2cd948d31af45
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-find-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="f509c-103">Come trovare un'API specifica necessaria per un'applicazione personalizzata</span><span class="sxs-lookup"><span data-stu-id="f509c-103">How to find a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="f509c-104">L'accesso alle API richiede la configurazione di ruoli e ambiti di accesso.</span><span class="sxs-lookup"><span data-stu-id="f509c-104">Access to APIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="f509c-105">Se si desidera esporre le API Web dell'applicazione della risorsa alle applicazioni client, è necessario configurare gli ambiti e i ruoli di accesso per l'API.</span><span class="sxs-lookup"><span data-stu-id="f509c-105">If you want to expose your resource application web APIs to client applications, you need to configure access scopes and roles for the API.</span></span> <span data-ttu-id="f509c-106">Se si desidera che un'applicazione client acceda a un'API Web, è necessario configurare le autorizzazioni per accedere all'API nella registrazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="f509c-106">If you want a client application to access a web API, you need to configure permissions to access the API in the app registration.</span></span>

## <a name="configuring-a-resource-application-to-expose-web-apis"></a><span data-ttu-id="f509c-107">Configurazione di un'applicazione della risorsa per esporre le API Web</span><span class="sxs-lookup"><span data-stu-id="f509c-107">Configuring a resource application to expose web APIs</span></span>

<span data-ttu-id="f509c-108">Quando si espone l'API Web, l'API viene visualizzata nell'elenco **Selezionare un'API** quando si aggiungono le autorizzazioni alla registrazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f509c-108">When you expose your web API, the API be displayed in the **Select an API** list when adding permissions to an app registration.</span></span> <span data-ttu-id="f509c-109">Per aggiungere gli ambiti di accesso, seguire la procedura descritta in [Aggiunta di ambiti di accesso all'applicazione della risorsa](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span><span class="sxs-lookup"><span data-stu-id="f509c-109">To add access scopes, follow the steps outlined in [adding access scopes to your resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-to-access-web-apis"></a><span data-ttu-id="f509c-110">Configurazione di un'applicazione client per accedere alle API Web</span><span class="sxs-lookup"><span data-stu-id="f509c-110">Configuring a client application to access web APIs</span></span>

<span data-ttu-id="f509c-111">Quando si aggiungono le autorizzazioni per la registrazione dell'app, è possibile **aggiungere l'accesso all'API** per esporre le API Web.</span><span class="sxs-lookup"><span data-stu-id="f509c-111">When you add permissions to your app registration, you can **add API access** to exposed web APIs.</span></span> <span data-ttu-id="f509c-112">Per accedere alle API Web, seguire la procedura descritta nella sezione [Per aggiungere credenziali o autorizzazioni per accedere alle API Web](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span><span class="sxs-lookup"><span data-stu-id="f509c-112">To access web APIs, follow the steps outlined in [add credentials or permissions to access web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f509c-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f509c-113">Next steps</span></span>

-   [<span data-ttu-id="f509c-114">Integrazione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f509c-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="f509c-115">Informazioni sul manifesto dell'applicazione in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f509c-115">Understanding the Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


