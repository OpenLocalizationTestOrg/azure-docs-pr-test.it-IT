---
title: Introduzione all'API di creazione report di Azure AD nel portale di Azure AD classico | Microsoft Docs
description: Come iniziare a usare l'API di creazione report di Azure Active Directory
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/18/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5e98b660fe19bb8abebf1c3b996b6295a6c4e728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api-on-the-azure-ad-classic-portal"></a><span data-ttu-id="c432e-103">Introduzione all'API di creazione report di Azure Active Directory nel portale di Azure AD classico</span><span class="sxs-lookup"><span data-stu-id="c432e-103">Getting started with the Azure Active Directory reporting API on the Azure AD classic portal</span></span>
<span data-ttu-id="c432e-104">*Questo argomento fa parte della [Guida alla creazione di report in Azure Active Directory](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="c432e-104">*This topic is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="c432e-105">Azure Active Directory fornisce una serie di report.</span><span class="sxs-lookup"><span data-stu-id="c432e-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="c432e-106">I dati di questi report possono essere molto utili per le applicazioni, ad esempio i sistemi SIEM e gli strumenti di controllo e business intelligence.</span><span class="sxs-lookup"><span data-stu-id="c432e-106">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="c432e-107">L'API di creazione report di Azure AD fornisce l'accesso ai dati dal codice tramite un set di API basate su REST.</span><span class="sxs-lookup"><span data-stu-id="c432e-107">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="c432e-108">È possibile chiamare le API da numerosi linguaggi di programmazione e strumenti.</span><span class="sxs-lookup"><span data-stu-id="c432e-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="c432e-109">Questo articolo riporta le informazioni necessarie per iniziare con le API di creazione report di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c432e-109">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="c432e-110">Nella sezione successiva sono riportate ulteriori informazioni sull'utilizzo delle API di controllo e di accesso.</span><span class="sxs-lookup"><span data-stu-id="c432e-110">In the next section, you find more details about using the audit and sign-in APIs.</span></span> <span data-ttu-id="c432e-111">Per tutte le altre API, vedere l'articolo di [sui report e gli eventi di Azure AD (anteprima)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview).</span><span class="sxs-lookup"><span data-stu-id="c432e-111">For all other APIs, see the [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="c432e-112">Per domande, problemi o suggerimenti, contattare la [Guida per la creazione di report AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c432e-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="c432e-113">Percorso di formazione</span><span class="sxs-lookup"><span data-stu-id="c432e-113">Learning map</span></span>
1. <span data-ttu-id="c432e-114">**Preparazione** - Prima di poter usare gli esempi contenuti in questo argomento, è necessario completare i [prerequisiti di accesso all'API di creazione report di Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="c432e-114">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="c432e-115">**Esplorazione** - Ottenere una prima impressione delle API di creazione report:</span><span class="sxs-lookup"><span data-stu-id="c432e-115">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="c432e-116">Utilizzo degli esempi dell'API di controllo</span><span class="sxs-lookup"><span data-stu-id="c432e-116">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="c432e-117">Utilizzo degli esempi dell'API di creazione report sull'attività di accesso</span><span class="sxs-lookup"><span data-stu-id="c432e-117">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="c432e-118">**Personalizzazione** - Creare una soluzione personalizzata:</span><span class="sxs-lookup"><span data-stu-id="c432e-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="c432e-119">Utilizzo delle informazioni di riferimento sull'API di controllo</span><span class="sxs-lookup"><span data-stu-id="c432e-119">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="c432e-120">Utilizzo delle informazioni di riferimento sull'API di creazione report sull'attività di accesso</span><span class="sxs-lookup"><span data-stu-id="c432e-120">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="c432e-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c432e-121">Next Steps</span></span>
<span data-ttu-id="c432e-122">Se si è curiosi di vedere tutti gli endpoint disponibili dell'API Graph di Azure AD, passare ad [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="c432e-122">If you are curious to see all of the available Azure AD Graph API endpoints by navigating to [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

