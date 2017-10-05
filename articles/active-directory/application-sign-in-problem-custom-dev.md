---
title: Problemi di accesso a un'applicazione personalizzata | Microsoft Docs
description: Errori comuni che potrebbero impedire l'accesso a un'applicazione sviluppata con Azure AD
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
ms.openlocfilehash: b0df23e040a73d18968f547eef7347f14cc577c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-custom-developed-application"></a><span data-ttu-id="d15de-103">Problemi di accesso a un'applicazione personalizzata</span><span class="sxs-lookup"><span data-stu-id="d15de-103">Problems signing in to an custom-developed application</span></span>

<span data-ttu-id="d15de-104">Ci sono diversi errori che potrebbero impedire l'accesso a un'app.</span><span class="sxs-lookup"><span data-stu-id="d15de-104">There are several errors that could be causing you to not be able to sign into an app.</span></span> <span data-ttu-id="d15de-105">Il motivo più frequente che causa questo problema è l'errata configurazione delle app.</span><span class="sxs-lookup"><span data-stu-id="d15de-105">The biggest reason people encounter this problem is misconfigured apps.</span></span>

## <a name="errors-related-to--misconfigured-apps"></a><span data-ttu-id="d15de-106">Errori correlati alle app configurate in modo errato</span><span class="sxs-lookup"><span data-stu-id="d15de-106">Errors related to  misconfigured apps</span></span>

* <span data-ttu-id="d15de-107">Verificare che le configurazioni nel portale corrispondano a quelle nell'app.</span><span class="sxs-lookup"><span data-stu-id="d15de-107">Verify both the configurations in the portal match what you have in your app.</span></span> <span data-ttu-id="d15de-108">In particolare, confrontare ID applicazione/client, URL di risposta, chiavi/segreti client e URI ID app.</span><span class="sxs-lookup"><span data-stu-id="d15de-108">Specifically, compare Client/Application ID, Reply URLs, Client Secrets/Keys, and App ID URI.</span></span>

* <span data-ttu-id="d15de-109">Confrontare la risorsa a cui si richiede l'accesso nel codice con le autorizzazioni configurate nella scheda **Risorse necessarie** per assicurarsi di richiedere solo le risorse configurate.</span><span class="sxs-lookup"><span data-stu-id="d15de-109">Compare the resource you’re requesting access to in code with the configured permissions in the **Required Resources** tab to make sure you only request resources you’ve configured.</span></span>

* <span data-ttu-id="d15de-110">Vedere [Azure AD in StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) per errori o problemi simili.</span><span class="sxs-lookup"><span data-stu-id="d15de-110">See [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) for any similar errors or problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d15de-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d15de-111">Next steps</span></span>

[<span data-ttu-id="d15de-112">Guida per gli sviluppatori di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d15de-112">Azure AD Developer Guide</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)<br>

[<span data-ttu-id="d15de-113">Integrazione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d15de-113">Consent and Integrating Apps to Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications>)<br>

[<span data-ttu-id="d15de-114">Consenso e concessione delle autorizzazioni per le app con convergenza di Azure Active Directory v2.0</span><span class="sxs-lookup"><span data-stu-id="d15de-114">Consent and Permissioning for Azure AD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="d15de-115">Azure AD in Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="d15de-115">Azure AD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory>)
