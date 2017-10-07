---
title: aaaGetting avviato con l'API di creazione report hello Azure AD | Documenti Microsoft
description: "Modalità di avvio tooget con hello reporting API Azure Active Directory"
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
ms.openlocfilehash: bb7d72ba445daa367d7502889c38a605a16f26d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api"></a><span data-ttu-id="fdae3-103">Introduzione a hello reporting API Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fdae3-103">Getting started with hello Azure Active Directory reporting API</span></span>

<span data-ttu-id="fdae3-104">Azure Active Directory fornisce una serie di report.</span><span class="sxs-lookup"><span data-stu-id="fdae3-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="fdae3-105">dati di Hello di questi report possono essere molto utile tooyour applicazioni, ad esempio i sistemi SIEM, controllo e strumenti di business intelligence.</span><span class="sxs-lookup"><span data-stu-id="fdae3-105">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="fdae3-106">Hello Azure AD reporting che API forniscono dati toohello accesso a livello di codice tramite un set di API basata su REST.</span><span class="sxs-lookup"><span data-stu-id="fdae3-106">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="fdae3-107">È possibile chiamare le API da numerosi linguaggi di programmazione e strumenti.</span><span class="sxs-lookup"><span data-stu-id="fdae3-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="fdae3-108">In questo articolo vengono fornite informazioni di hello è necessario tooget introduttiva hello Azure AD reporting API.</span><span class="sxs-lookup"><span data-stu-id="fdae3-108">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="fdae3-109">Nella sezione successiva hello, disponibili ulteriori informazioni sull'utilizzo di hello audit e accesso API.</span><span class="sxs-lookup"><span data-stu-id="fdae3-109">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> 

<span data-ttu-id="fdae3-110">Per le domande frequenti, fare clic [qui](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span><span class="sxs-lookup"><span data-stu-id="fdae3-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="fdae3-111">In caso di problemi, [inviare un ticket di supporto](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span><span class="sxs-lookup"><span data-stu-id="fdae3-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="fdae3-112">Percorso di formazione</span><span class="sxs-lookup"><span data-stu-id="fdae3-112">Learning map</span></span>
1. <span data-ttu-id="fdae3-113">**Preparare** -prima di poter testare gli esempi di API, è necessario hello toocomplete [prerequisiti tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fdae3-113">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="fdae3-114">**Esplorare** -ottenere una visione prima di hello reporting API:</span><span class="sxs-lookup"><span data-stu-id="fdae3-114">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="fdae3-115">Utilizzo di esempi di hello per il controllo di hello API</span><span class="sxs-lookup"><span data-stu-id="fdae3-115">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="fdae3-116">Utilizzo di esempi di hello per API report attività di accesso di hello</span><span class="sxs-lookup"><span data-stu-id="fdae3-116">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="fdae3-117">**Personalizzazione** - Creare una soluzione personalizzata:</span><span class="sxs-lookup"><span data-stu-id="fdae3-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="fdae3-118">Utilizzo di riferimenti alle API di controllo hello</span><span class="sxs-lookup"><span data-stu-id="fdae3-118">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="fdae3-119">Utilizzando i report di attività di accesso hello riferimento API</span><span class="sxs-lookup"><span data-stu-id="fdae3-119">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="fdae3-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fdae3-120">Next Steps</span></span>
<span data-ttu-id="fdae3-121">Se si desidera toosee tutti gli endpoint API Graph di Azure AD disponibili, utilizzare questo collegamento: [https://graph.windows.net/tenant-name/activities/$ metadata? api-version = beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="fdae3-121">If you are curious toosee all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

