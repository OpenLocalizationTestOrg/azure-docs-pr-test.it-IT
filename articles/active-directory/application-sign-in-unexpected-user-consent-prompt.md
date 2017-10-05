---
title: Richiesta di consenso imprevista al momento dell'accesso a un'applicazione | Microsoft Docs
description: "Come risolvere il problema relativo a una richiesta di consenso imprevista visualizzata da un utente per un'applicazione che è stata integrata con Azure AD"
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
ms.openlocfilehash: e5b823e1251a7221f73efe6838d439f827f9665d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-to-an-application"></a><span data-ttu-id="eb206-103">Richiesta di consenso imprevista al momento dell'accesso a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="eb206-103">Unexpected consent prompt when signing in to an application</span></span>

<span data-ttu-id="eb206-104">Molte applicazioni integrate in Azure Active Directory richiedono autorizzazioni di accesso a varie risorse per funzionare.</span><span class="sxs-lookup"><span data-stu-id="eb206-104">Many applications that integrate with Azure Active Directory require permissions to various resources in order to run.</span></span> <span data-ttu-id="eb206-105">Quando anche queste risorse sono integrate in Azure Active Directory, le autorizzazioni per il relativo accesso vengono richieste tramite il framework di consenso di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb206-105">When these resources are also integrated with Azure Active Directory, permissions to access them is requested using the Azure AD consent framework.</span></span> 

<span data-ttu-id="eb206-106">Questo fa sì che venga visualizzata una richiesta di consenso al primo utilizzo dell'applicazione, in genere si tratta di un'operazione che viene eseguita una sola volta.</span><span class="sxs-lookup"><span data-stu-id="eb206-106">This results in a consent prompt being shown the first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="eb206-107">Scenari in cui gli utenti visualizzano richieste di consenso</span><span class="sxs-lookup"><span data-stu-id="eb206-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="eb206-108">Ulteriori richieste aggiuntive sono possibili in vari scenari:</span><span class="sxs-lookup"><span data-stu-id="eb206-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="eb206-109">L'insieme di autorizzazioni richiesto dall'applicazione è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="eb206-109">The set of permissions required by the application have changed.</span></span>

* <span data-ttu-id="eb206-110">L'utente che ha originariamente autorizzato l'applicazione non è un amministratore e ora un altro utente (non amministratore) sta utilizzando l'applicazione per la prima volta.</span><span class="sxs-lookup"><span data-stu-id="eb206-110">The user who originally consented to the application was not an administrator, and now a different (non-admin) User is using the application for the first time.</span></span>

* <span data-ttu-id="eb206-111">L'utente che ha originariamente autorizzato l'applicazione è un amministratore, ma non ha dato il consenso per conto dell'intera organizzazione.</span><span class="sxs-lookup"><span data-stu-id="eb206-111">The user who originally consented to the application was an administrator, but they did not consent on-behalf of the entire organization.</span></span>

* <span data-ttu-id="eb206-112">L'applicazione utilizza il [consenso incrementale e dinamico](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) per richiedere ulteriori autorizzazioni dopo che inizialmente è stato concesso il consenso.</span><span class="sxs-lookup"><span data-stu-id="eb206-112">The application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) to request additional permissions after consent was initially granted.</span></span> <span data-ttu-id="eb206-113">Questo tipo di consenso viene frequentemente usato quando funzionalità facoltative di un'applicazione richiedono autorizzazioni ulteriori a quelle richieste per la funzionalità di base.</span><span class="sxs-lookup"><span data-stu-id="eb206-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="eb206-114">Il consenso è stato revocato dopo essere stato inizialmente consentito.</span><span class="sxs-lookup"><span data-stu-id="eb206-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="eb206-115">Lo sviluppatore ha configurato l'applicazione in modo che visualizzi una richiesta di consenso ogni volta che viene usata (nota: non è una procedura consigliata).</span><span class="sxs-lookup"><span data-stu-id="eb206-115">The developer has configured the application to require a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb206-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eb206-116">Next steps</span></span>

-   [<span data-ttu-id="eb206-117">App, autorizzazioni e consenso in Azure Active Directory (endpoint v1.0)</span><span class="sxs-lookup"><span data-stu-id="eb206-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="eb206-118">Ambiti, autorizzazioni e consenso in Azure Active Directory (endpoint v2.0)</span><span class="sxs-lookup"><span data-stu-id="eb206-118">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


