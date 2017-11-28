---
title: aaaUsing New Relic con Azure | Documenti Microsoft
description: Informazioni su come toouse hello toomanage servizio New Relic e monitorare l'applicazione Azure.
services: 
documentationcenter: .net
author: nickfloyd
manager: timlt
editor: 
ms.assetid: b01011be-c344-4e33-987d-c93dac1971fb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2016
ms.author: nickfloyd@newrelic.com
ms.openlocfilehash: 81e5f1b694264e3586ac75d40edd8afe185493d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="913ef-103">Gestione delle prestazioni delle applicazioni con New Relic in Siti Web di Azure</span><span class="sxs-lookup"><span data-stu-id="913ef-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="913ef-104">È possibile aggiungere le prestazioni di qualità elevata del New Relic monitoraggio tooyour applicazioni ospitate di Azure.</span><span class="sxs-lookup"><span data-stu-id="913ef-104">You can add New Relic's world-class performance monitoring tooyour Azure hosted applications.</span></span> <span data-ttu-id="913ef-105">Insieme a funzionalità complete di monitoraggio, risoluzione dei problemi e ottimizzazione delle app di Azure, usando Azure si ha anche diritto a un prezzo scontato per i prodotti di New Relic.</span><span class="sxs-lookup"><span data-stu-id="913ef-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="913ef-106">Informazioni su New Relic</span><span class="sxs-lookup"><span data-stu-id="913ef-106">What is New Relic?</span></span>
<span data-ttu-id="913ef-107">Con [prodotti New Relic](https://newrelic.com/products), è possibile risolvere gli errori di app, anticipare i problemi potenziali e informazioni sulle prestazioni di hello dell'intero ambiente.</span><span class="sxs-lookup"><span data-stu-id="913ef-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand hello performance of your entire environment.</span></span> <span data-ttu-id="913ef-108">È progettato toosave tempo durante l'identificazione e la diagnosi dei problemi di prestazioni, e tale client inserisce informazioni hello necessarie toosolve questi problemi a portata di mano.</span><span class="sxs-lookup"><span data-stu-id="913ef-108">It is designed toosave you time when identifying and diagnosing performance issues, and it puts hello information you need toosolve these issues at your fingertips.</span></span>

<span data-ttu-id="913ef-109">Nuovo Relic tracce hello caricare ora e la velocità effettiva per le transazioni web, server hello e browser degli utenti.</span><span class="sxs-lookup"><span data-stu-id="913ef-109">New Relic tracks hello load time and throughput for your web transactions, both from hello server and your users' browsers.</span></span> <span data-ttu-id="913ef-110">Mostra il tempo speso per database hello, consente di analizzare le query lente e richieste web, fornisce il monitoraggio dei tempi di attività e avvisi, tiene traccia delle eccezioni dell'applicazione e molto più.</span><span class="sxs-lookup"><span data-stu-id="913ef-110">It shows how much time you spend in hello database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="913ef-111">Prezzo speciale</span><span class="sxs-lookup"><span data-stu-id="913ef-111">Special pricing</span></span>
<span data-ttu-id="913ef-112">Nuovo Relic Standard è disponibile tooAzure utenti.</span><span class="sxs-lookup"><span data-stu-id="913ef-112">New Relic Standard is free tooAzure users.</span></span> <span data-ttu-id="913ef-113">New Relic Pro viene offerto in base alle dimensioni delle istanze per i servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="913ef-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="913ef-114">Per informazioni sui prezzi, vedere hello [pagina New Relic](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in hello Azure Marketplace o contattare New Relic (sales@newrelic.com) per la determinazione dei prezzi di livello aziendale.</span><span class="sxs-lookup"><span data-stu-id="913ef-114">For pricing information, see hello [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in hello Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="913ef-115">I clienti Azure ricevono una sottoscrizione di valutazione di due settimane di nuovo Relic Pro durante la distribuzione dell'agente di New Relic hello.</span><span class="sxs-lookup"><span data-stu-id="913ef-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy hello New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-hello-azure-store"></a><span data-ttu-id="913ef-116">Iscriversi a New Relic utilizzando hello Azure Store</span><span class="sxs-lookup"><span data-stu-id="913ef-116">Sign up for New Relic using hello Azure Store</span></span>
<span data-ttu-id="913ef-117">New Relic si integra facilmente con i ruoli Web e di lavoro di Azure.</span><span class="sxs-lookup"><span data-stu-id="913ef-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="913ef-118">È possibile rapidamente e facilmente iscriversi a New Relic direttamente da hello Azure Store.</span><span class="sxs-lookup"><span data-stu-id="913ef-118">You can quickly and easily sign up for New Relic directly from hello Azure Store.</span></span> <span data-ttu-id="913ef-119">Per istruzioni, vedere hello [Azure archiviano le istruzioni per l'abbonamento](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) da New Relic.</span><span class="sxs-lookup"><span data-stu-id="913ef-119">For instructions, see hello [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="913ef-120">Visualizzare i dati</span><span class="sxs-lookup"><span data-stu-id="913ef-120">View your data</span></span>
<span data-ttu-id="913ef-121">Dopo aver effettuato l'iscrizione, è possibile sfruttare le sorprendenti funzionalità di New Relic per il monitoraggio delle applicazioni e l'analisi basata sui dati .</span><span class="sxs-lookup"><span data-stu-id="913ef-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="913ef-122">toocheck le prestazioni dell'app in New Relic:</span><span class="sxs-lookup"><span data-stu-id="913ef-122">toocheck your app's performance in New Relic:</span></span>

1. <span data-ttu-id="913ef-123">Hello portale di Azure, selezionare Gestisci.</span><span class="sxs-lookup"><span data-stu-id="913ef-123">From hello Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="913ef-124">Accedere con l'account di New Relic sotto forma di indirizzo di posta elettronica e password.</span><span class="sxs-lookup"><span data-stu-id="913ef-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="913ef-125">Selezionare l'applicazione da hello applicazione indice tooview tutti i dati dell'applicazione in hello [pagina Panoramica APM](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span><span class="sxs-lookup"><span data-stu-id="913ef-125">Select your app from hello Application index tooview all your app's data in hello [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="913ef-126">Uso di New Relic con Azure</span><span class="sxs-lookup"><span data-stu-id="913ef-126">Using New Relic with Azure</span></span>
<span data-ttu-id="913ef-127">Per altre informazioni sull'uso di New Relic e Azure, vedere il [sito della documentazione di New Relic](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), ad esempio:</span><span class="sxs-lookup"><span data-stu-id="913ef-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="913ef-128">New Relic for .NET</span><span class="sxs-lookup"><span data-stu-id="913ef-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="913ef-129">Instrument a .NET Worker Role on Azure Cloud Service</span><span class="sxs-lookup"><span data-stu-id="913ef-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="913ef-130">New Relic per la piattaforma Microsoft Azure Cloud hello</span><span class="sxs-lookup"><span data-stu-id="913ef-130">New Relic for hello Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="913ef-131">New Relic per hello servizi App di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="913ef-131">New Relic for hello Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="913ef-132">New Relic/Azure troubleshooting</span><span class="sxs-lookup"><span data-stu-id="913ef-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

