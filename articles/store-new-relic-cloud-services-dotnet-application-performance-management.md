---
title: Uso di New Relic con Azure | Microsoft Docs
description: Informazioni sull'uso del servizio New Relic per gestire e monitorare l'applicazione Azure.
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
ms.openlocfilehash: f4f13c909a6ff640d403f5264004176c087925dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="a67bc-103">Gestione delle prestazioni delle applicazioni con New Relic in Siti Web di Azure</span><span class="sxs-lookup"><span data-stu-id="a67bc-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="a67bc-104">È possibile aggiungere New Relic per un monitoraggio di qualità superiore delle prestazioni delle applicazioni ospitate in Azure.</span><span class="sxs-lookup"><span data-stu-id="a67bc-104">You can add New Relic's world-class performance monitoring to your Azure hosted applications.</span></span> <span data-ttu-id="a67bc-105">Insieme a funzionalità complete di monitoraggio, risoluzione dei problemi e ottimizzazione delle app di Azure, usando Azure si ha anche diritto a un prezzo scontato per i prodotti di New Relic.</span><span class="sxs-lookup"><span data-stu-id="a67bc-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="a67bc-106">Informazioni su New Relic</span><span class="sxs-lookup"><span data-stu-id="a67bc-106">What is New Relic?</span></span>
<span data-ttu-id="a67bc-107">Con i [prodotti New Relic](https://newrelic.com/products)è possibile risolvere gli errori delle app, prevenire i problemi potenziali e comprendere le prestazioni dell'intero ambiente.</span><span class="sxs-lookup"><span data-stu-id="a67bc-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand the performance of your entire environment.</span></span> <span data-ttu-id="a67bc-108">Lo strumento è progettato per consentire di risparmiare tempo quando si identificano o si diagnosticano problemi di prestazioni ed è in grado di mettere alla portata dell'utente tutte le informazioni necessarie per la risoluzione di tali problemi.</span><span class="sxs-lookup"><span data-stu-id="a67bc-108">It is designed to save you time when identifying and diagnosing performance issues, and it puts the information you need to solve these issues at your fingertips.</span></span>

<span data-ttu-id="a67bc-109">New Relic tiene traccia del tempo di caricamento e della velocità effettiva delle transazioni Web, sia dal server che dai browser degli utenti.</span><span class="sxs-lookup"><span data-stu-id="a67bc-109">New Relic tracks the load time and throughput for your web transactions, both from the server and your users' browsers.</span></span> <span data-ttu-id="a67bc-110">Visualizza il tempo trascorso nel database, analizza le query e le richieste Web più lente, fornisce il monitoraggio del tempo di attività e l'invio di avvisi, tiene traccia delle eccezioni delle applicazioni e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="a67bc-110">It shows how much time you spend in the database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="a67bc-111">Prezzo speciale</span><span class="sxs-lookup"><span data-stu-id="a67bc-111">Special pricing</span></span>
<span data-ttu-id="a67bc-112">New Relic Standard è gratuito per gli utenti di Azure.</span><span class="sxs-lookup"><span data-stu-id="a67bc-112">New Relic Standard is free to Azure users.</span></span> <span data-ttu-id="a67bc-113">New Relic Pro viene offerto in base alle dimensioni delle istanze per i servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="a67bc-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="a67bc-114">Per informazioni sui prezzi, vedere il [pagina New Relic](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in Azure Marketplace o il contatto New Relic (sales@newrelic.com) per la determinazione dei prezzi di livello aziendale.</span><span class="sxs-lookup"><span data-stu-id="a67bc-114">For pricing information, see the [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in the Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="a67bc-115">I clienti di Azure che distribuiscono l'agente New Relic hanno diritto a una sottoscrizione di valutazione di New Relic Pro della durata di due settimane.</span><span class="sxs-lookup"><span data-stu-id="a67bc-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy the New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-the-azure-store"></a><span data-ttu-id="a67bc-116">Iscrizione a New Relic utilizzando Azure Store</span><span class="sxs-lookup"><span data-stu-id="a67bc-116">Sign up for New Relic using the Azure Store</span></span>
<span data-ttu-id="a67bc-117">New Relic si integra facilmente con i ruoli Web e di lavoro di Azure.</span><span class="sxs-lookup"><span data-stu-id="a67bc-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="a67bc-118">È possibile iscriversi facilmente e rapidamente a New Relic direttamente da Azure Store.</span><span class="sxs-lookup"><span data-stu-id="a67bc-118">You can quickly and easily sign up for New Relic directly from the Azure Store.</span></span> <span data-ttu-id="a67bc-119">Per istruzioni, vedere le [istruzioni per l'iscrizione tramite Azure Store](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) di New Relic.</span><span class="sxs-lookup"><span data-stu-id="a67bc-119">For instructions, see the [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="a67bc-120">Visualizzare i dati</span><span class="sxs-lookup"><span data-stu-id="a67bc-120">View your data</span></span>
<span data-ttu-id="a67bc-121">Dopo aver effettuato l'iscrizione, è possibile sfruttare le sorprendenti funzionalità di New Relic per il monitoraggio delle applicazioni e l'analisi basata sui dati .</span><span class="sxs-lookup"><span data-stu-id="a67bc-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="a67bc-122">Per controllare le prestazioni dell'applicazione in New Relic:</span><span class="sxs-lookup"><span data-stu-id="a67bc-122">To check your app's performance in New Relic:</span></span>

1. <span data-ttu-id="a67bc-123">Nel portale di Azure selezionare Gestisci.</span><span class="sxs-lookup"><span data-stu-id="a67bc-123">From the Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="a67bc-124">Accedere con l'account di New Relic sotto forma di indirizzo di posta elettronica e password.</span><span class="sxs-lookup"><span data-stu-id="a67bc-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="a67bc-125">Selezionare l'app nell'indice delle applicazioni per visualizzare tutti i dati nella [APM Overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page)(pagina della panoramica di APM).</span><span class="sxs-lookup"><span data-stu-id="a67bc-125">Select your app from the Application index to view all your app's data in the [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="a67bc-126">Uso di New Relic con Azure</span><span class="sxs-lookup"><span data-stu-id="a67bc-126">Using New Relic with Azure</span></span>
<span data-ttu-id="a67bc-127">Per altre informazioni sull'uso di New Relic e Azure, vedere il [sito della documentazione di New Relic](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a67bc-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="a67bc-128">New Relic for .NET</span><span class="sxs-lookup"><span data-stu-id="a67bc-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="a67bc-129">Instrument a .NET Worker Role on Azure Cloud Service</span><span class="sxs-lookup"><span data-stu-id="a67bc-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="a67bc-130">New Relic for the Microsoft Azure Cloud platform</span><span class="sxs-lookup"><span data-stu-id="a67bc-130">New Relic for the Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="a67bc-131">New Relic for the Microsoft Azure App Services</span><span class="sxs-lookup"><span data-stu-id="a67bc-131">New Relic for the Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="a67bc-132">New Relic/Azure troubleshooting</span><span class="sxs-lookup"><span data-stu-id="a67bc-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

