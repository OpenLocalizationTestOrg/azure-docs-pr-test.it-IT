---
title: aaaGetting avviato con l'API di creazione report hello Azure AD nel portale classico hello Azure AD | Documenti Microsoft
description: "Modalità di avvio tooget con hello reporting API Azure Active Directory"
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
ms.openlocfilehash: 52e22d442650731fc6ed28991fc65f9182af0540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api-on-hello-azure-ad-classic-portal"></a><span data-ttu-id="84cbd-103">Introduzione a hello reporting API nel portale classico hello Azure AD Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="84cbd-103">Getting started with hello Azure Active Directory reporting API on hello Azure AD classic portal</span></span>
<span data-ttu-id="84cbd-104">*In questo argomento fa parte di hello [Azure Active Directory Reporting Guida](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="84cbd-104">*This topic is part of hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="84cbd-105">Azure Active Directory fornisce una serie di report.</span><span class="sxs-lookup"><span data-stu-id="84cbd-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="84cbd-106">dati di Hello di questi report possono essere molto utile tooyour applicazioni, ad esempio i sistemi SIEM, controllo e strumenti di business intelligence.</span><span class="sxs-lookup"><span data-stu-id="84cbd-106">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="84cbd-107">Hello Azure AD reporting che API forniscono dati toohello accesso a livello di codice tramite un set di API basata su REST.</span><span class="sxs-lookup"><span data-stu-id="84cbd-107">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="84cbd-108">È possibile chiamare le API da numerosi linguaggi di programmazione e strumenti.</span><span class="sxs-lookup"><span data-stu-id="84cbd-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="84cbd-109">In questo articolo vengono fornite informazioni di hello è necessario tooget introduttiva hello Azure AD reporting API.</span><span class="sxs-lookup"><span data-stu-id="84cbd-109">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="84cbd-110">Nella sezione successiva hello, disponibili ulteriori informazioni sull'utilizzo di hello audit e accesso API.</span><span class="sxs-lookup"><span data-stu-id="84cbd-110">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> <span data-ttu-id="84cbd-111">Per tutte le altre API, vedere hello [report di Azure AD ed events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) articolo.</span><span class="sxs-lookup"><span data-stu-id="84cbd-111">For all other APIs, see hello [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="84cbd-112">Per domande, problemi o suggerimenti, contattare la [Guida per la creazione di report AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="84cbd-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="84cbd-113">Percorso di formazione</span><span class="sxs-lookup"><span data-stu-id="84cbd-113">Learning map</span></span>
1. <span data-ttu-id="84cbd-114">**Preparare** -prima di poter testare gli esempi di API, è necessario hello toocomplete [prerequisiti tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="84cbd-114">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="84cbd-115">**Esplorare** -ottenere una visione prima di hello reporting API:</span><span class="sxs-lookup"><span data-stu-id="84cbd-115">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="84cbd-116">Utilizzo di esempi di hello per il controllo di hello API</span><span class="sxs-lookup"><span data-stu-id="84cbd-116">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="84cbd-117">Utilizzo di esempi di hello per API report attività di accesso di hello</span><span class="sxs-lookup"><span data-stu-id="84cbd-117">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="84cbd-118">**Personalizzazione** - Creare una soluzione personalizzata:</span><span class="sxs-lookup"><span data-stu-id="84cbd-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="84cbd-119">Utilizzo di riferimenti alle API di controllo hello</span><span class="sxs-lookup"><span data-stu-id="84cbd-119">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="84cbd-120">Utilizzando i report di attività di accesso hello riferimento API</span><span class="sxs-lookup"><span data-stu-id="84cbd-120">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="84cbd-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="84cbd-121">Next Steps</span></span>
<span data-ttu-id="84cbd-122">Se si desidera toosee tutti hello endpoint API Graph di Azure AD disponibili passando troppo[https://graph.windows.net/tenant-name/reports/$ metadata? api-version = beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="84cbd-122">If you are curious toosee all of hello available Azure AD Graph API endpoints by navigating too[https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

