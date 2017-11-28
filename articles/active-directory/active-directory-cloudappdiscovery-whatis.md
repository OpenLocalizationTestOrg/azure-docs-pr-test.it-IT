---
title: le applicazioni cloud a Cloud App Discovery non gestita di aaaFinding | Documenti Microsoft
description: Fornisce informazioni sulla ricerca e la gestione delle applicazioni con Cloud App Discovery, quali sono i vantaggi di hello e sul relativo funzionamento.
services: active-directory
keywords: cloud app discovery, gestione delle applicazioni
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="18928-104">Ricerca di applicazioni cloud non gestite con Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="18928-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="18928-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="18928-105">Overview</span></span>
<span data-ttu-id="18928-106">Nelle aziende moderne i reparti IT spesso non sono a conoscenza di tutte le applicazioni cloud hello che i membri dell'organizzazione di utilizzare toodo il proprio lavoro.</span><span class="sxs-lookup"><span data-stu-id="18928-106">In modern enterprises, IT departments are often not aware of all hello cloud applications that members of their organization use toodo their work.</span></span> <span data-ttu-id="18928-107">È facile toosee perché gli amministratori avranno preoccupazioni dati toocorporate di accesso non autorizzato, perdita di dati e altri rischi di protezione.</span><span class="sxs-lookup"><span data-stu-id="18928-107">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="18928-108">A causa di questa mancanza di consapevolezza, la creazione di un piano per la gestione dei rischi per la sicurezza potrebbe sembrare complicata.</span><span class="sxs-lookup"><span data-stu-id="18928-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="18928-109">Cloud App Discovery è una funzionalità Premium di Azure Active Directory (AD) che consente applicazioni cloud toodiscover in uso da parte di persone hello all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="18928-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you toodiscover cloud applications being used by hello people in your organization.</span></span>

<span data-ttu-id="18928-110">**Cloud App Discovery consente di:**</span><span class="sxs-lookup"><span data-stu-id="18928-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="18928-111">Trovare le applicazioni cloud hello in uso e misurarne dal numero di utenti, volume di traffico o un numero di applicazione toohello di richieste web.</span><span class="sxs-lookup"><span data-stu-id="18928-111">Find hello cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests toohello application.</span></span>
* <span data-ttu-id="18928-112">Identificare gli utenti di hello che usano un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="18928-112">Identify hello users that are using an application.</span></span>
* <span data-ttu-id="18928-113">Esportare i dati per analisi offline.</span><span class="sxs-lookup"><span data-stu-id="18928-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="18928-114">Portare le applicazioni sotto il controllo IT e abilitare la funzionalità Single Sign-On per la gestione degli utenti.</span><span class="sxs-lookup"><span data-stu-id="18928-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="18928-115">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="18928-115">How it works</span></span>
1. <span data-ttu-id="18928-116">Gli agenti di utilizzo dell'applicazione vengono installati nei computer dell'utente.</span><span class="sxs-lookup"><span data-stu-id="18928-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="18928-117">informazioni sull'utilizzo di applicazione Hello acquisite dagli agenti hello viene inviate tramite un servizio cloud app discovery di canale crittografato protetto toohello.</span><span class="sxs-lookup"><span data-stu-id="18928-117">hello application usage information captured by hello agents is sent over a secure, encrypted channel toohello cloud app discovery service.</span></span>
3. <span data-ttu-id="18928-118">Hello servizio Cloud App Discovery valuta dati hello e genera i report.</span><span class="sxs-lookup"><span data-stu-id="18928-118">hello Cloud App Discovery service evaluates hello data and generates reports.</span></span>

![Diagramma di Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="18928-120">tooget a usare Cloud App Discovery, vedere [Guida introduttiva a Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="18928-120">tooget started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="18928-121">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="18928-121">Related articles</span></span>
* [<span data-ttu-id="18928-122">Considerazioni sulla sicurezza e sulla privacy in Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="18928-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="18928-123">Guida alla distribuzione di criteri di gruppo di Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="18928-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="18928-124">Guida alla distribuzione di Cloud App Discovery System Center</span><span class="sxs-lookup"><span data-stu-id="18928-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="18928-125">Impostazioni del Registro di sistema di Cloud App Discovery per servizi proxy con porte personalizzate</span><span class="sxs-lookup"><span data-stu-id="18928-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="18928-126">Log modifiche dell'agente di Cloud App Discovery </span><span class="sxs-lookup"><span data-stu-id="18928-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="18928-127">Domande frequenti di Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="18928-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [<span data-ttu-id="18928-128">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="18928-128">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

