---
title: Introduzione all'API di creazione report di Azure AD | Microsoft Docs
description: Come iniziare a usare l'API di creazione report di Azure Active Directory
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/18/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 9944cbd2b1b7c4acb18d37da1394c0bbc170f77d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api"></a><span data-ttu-id="0922f-103">Introduzione all'API di creazione report di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0922f-103">Getting started with the Azure Active Directory reporting API</span></span>

<span data-ttu-id="0922f-104">Azure Active Directory fornisce una serie di report.</span><span class="sxs-lookup"><span data-stu-id="0922f-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="0922f-105">I dati di questi report possono essere molto utili per le applicazioni, ad esempio i sistemi SIEM e gli strumenti di controllo e business intelligence.</span><span class="sxs-lookup"><span data-stu-id="0922f-105">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="0922f-106">L'API di creazione report di Azure AD fornisce l'accesso ai dati dal codice tramite un set di API basate su REST.</span><span class="sxs-lookup"><span data-stu-id="0922f-106">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="0922f-107">È possibile chiamare le API da numerosi linguaggi di programmazione e strumenti.</span><span class="sxs-lookup"><span data-stu-id="0922f-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="0922f-108">Questo articolo riporta le informazioni necessarie per iniziare con le API di creazione report di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0922f-108">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="0922f-109">Nella sezione successiva sono riportate ulteriori informazioni sull'utilizzo delle API di controllo e di accesso.</span><span class="sxs-lookup"><span data-stu-id="0922f-109">In the next section, you find more details about using the audit and sign-in APIs.</span></span> 

<span data-ttu-id="0922f-110">Per le domande frequenti, fare clic [qui](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span><span class="sxs-lookup"><span data-stu-id="0922f-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="0922f-111">In caso di problemi, [inviare un ticket di supporto](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span><span class="sxs-lookup"><span data-stu-id="0922f-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="0922f-112">Percorso di formazione</span><span class="sxs-lookup"><span data-stu-id="0922f-112">Learning map</span></span>
1. <span data-ttu-id="0922f-113">**Preparazione** - Prima di poter usare gli esempi contenuti in questo argomento, è necessario completare i [prerequisiti di accesso all'API di creazione report di Azure AD](active-directory-reporting-api-prerequisites-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0922f-113">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="0922f-114">**Esplorazione** - Ottenere una prima impressione delle API di creazione report:</span><span class="sxs-lookup"><span data-stu-id="0922f-114">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="0922f-115">Utilizzo degli esempi dell'API di controllo</span><span class="sxs-lookup"><span data-stu-id="0922f-115">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="0922f-116">Utilizzo degli esempi dell'API di creazione report sull'attività di accesso</span><span class="sxs-lookup"><span data-stu-id="0922f-116">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="0922f-117">**Personalizzazione** - Creare una soluzione personalizzata:</span><span class="sxs-lookup"><span data-stu-id="0922f-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="0922f-118">Utilizzo delle informazioni di riferimento sull'API di controllo</span><span class="sxs-lookup"><span data-stu-id="0922f-118">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="0922f-119">Utilizzo delle informazioni di riferimento sull'API di creazione report sull'attività di accesso</span><span class="sxs-lookup"><span data-stu-id="0922f-119">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="0922f-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0922f-120">Next Steps</span></span>
<span data-ttu-id="0922f-121">Se si desidera vedere tutti gli endpoint disponibili dell'API Graph di Azure AD, usare questo link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="0922f-121">If you are curious to see all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

