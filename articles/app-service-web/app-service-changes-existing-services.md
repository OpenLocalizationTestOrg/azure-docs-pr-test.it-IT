---
title: Servizio app di Azure e impatto sui servizi di Azure esistenti
description: "Viene illustrato come il nuovo servizio app di Azure e le relative funzionalità influiscono sui servizi esistenti in Azure."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: ed967fda7a216ed49532be54228ebe888cf16b6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="58892-103">Servizio app di Azure e i servizi di Azure esistenti</span><span class="sxs-lookup"><span data-stu-id="58892-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="58892-104">Questo articolo illustra le modifiche ai servizi di Azure esistenti come parte delle modifiche introdotte al fine di raggruppare vari servizi di Azure nel [servizio app di Azure](https://azure.microsoft.com/services/app-service/), una nuova offerta integrata.</span><span class="sxs-lookup"><span data-stu-id="58892-104">This article outlines the changes to existing Azure services as part of the change to bring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="58892-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="58892-105">Overview</span></span>
<span data-ttu-id="58892-106">[servizio app di Azure](https://azure.microsoft.com/services/app-service/) è un servizio cloud nuovo ed esclusivo che consente agli sviluppatori di creare app per dispositivi mobili e Web per qualsiasi piattaforma e dispositivo.</span><span class="sxs-lookup"><span data-stu-id="58892-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers to create web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="58892-107">Il servizio app viene offerto come soluzione integrata progettata per snellire le ripetitive procedure di scrittura del codice, integrarsi con i sistemi aziendali e SaaS e automatizzare i processi aziendali, adattandosi al contempo alle esigenze di sicurezza, affidabilità e scalabilità.</span><span class="sxs-lookup"><span data-stu-id="58892-107">App Service is an integrated solution designed to streamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="58892-108">Il servizio app riunisce i servizi di Azure esistenti [Siti Web](https://azure.microsoft.com/services/websites/), [Servizi mobili](https://azure.microsoft.com/services/mobile-services/) e [Servizi Biztalk](https://azure.microsoft.com/services/biztalk-services/) in un unico servizio combinato a cui sono state aggiunte nuove funzionalità avanzate.</span><span class="sxs-lookup"><span data-stu-id="58892-108">App Service brings together the following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="58892-109">Il servizio app consente di ospitare i seguenti tipi di app:</span><span class="sxs-lookup"><span data-stu-id="58892-109">App Service allows you to host the following app types:</span></span>

* <span data-ttu-id="58892-110">App Web</span><span class="sxs-lookup"><span data-stu-id="58892-110">Web Apps</span></span>
* <span data-ttu-id="58892-111">App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="58892-111">Mobile Apps</span></span>
* <span data-ttu-id="58892-112">App per le API</span><span class="sxs-lookup"><span data-stu-id="58892-112">API Apps</span></span>
* <span data-ttu-id="58892-113">App per la logica</span><span class="sxs-lookup"><span data-stu-id="58892-113">Logic Apps</span></span>

<span data-ttu-id="58892-114">La tabella seguente illustra la corrispondenza tra i servizi di Azure esistenti e il nuovo servizio app, nonché i tipi di app disponibili al suo interno.</span><span class="sxs-lookup"><span data-stu-id="58892-114">The following table explains how existing Azure services map to App Service and the app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="58892-115">Servizio di Azure esistente</span><span class="sxs-lookup"><span data-stu-id="58892-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="58892-116">Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="58892-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="58892-117">Cosa è cambiato</span><span class="sxs-lookup"><span data-stu-id="58892-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="58892-118">Siti Web di Azure</span><span class="sxs-lookup"><span data-stu-id="58892-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="58892-119">App Web</span><span class="sxs-lookup"><span data-stu-id="58892-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="58892-120">Per quanto riguarda Siti Web di Azure, le modifiche si riducono esclusivamente al cambio di nome da Siti Web ad App Web.</span><span class="sxs-lookup"><span data-stu-id="58892-120">For Azure Websites, App Service is strictly limited to changing the name  Websites to Web Apps.</span></span>
<p><li><span data-ttu-id="58892-121">Tutte le istanze esistenti di Siti Web sono ora app Web nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="58892-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="58892-122">È possibile accedere ai siti web esistenti tramite il <a href="http://go.microsoft.com/fwlink/?LinkId=529715">portale di Azure</a>, in cui tutti i siti Web esistenti saranno visualizzati sotto <em>App Web</em>.</span><span class="sxs-lookup"><span data-stu-id="58892-122">You can access your existing websites via the <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="58892-123"><em>Web piano di Hosting</em> è ora <em>piano di servizio App</em>.</span><span class="sxs-lookup"><span data-stu-id="58892-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="58892-124">Un <em>piano di servizio app</em> può ospitare qualsiasi tipo di servizio app, ad esempio app Web, per dispositivi mobili, per la logica o per le API.</span><span class="sxs-lookup"><span data-stu-id="58892-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="58892-125">App Web del servizio app di Azure si trova ora in stato di disponibilità generale.</span><span class="sxs-lookup"><span data-stu-id="58892-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="58892-126"><a href="http://azure.microsoft.com/services/app-service/web/">Altre informazioni sulle App Web</a>.</span><span class="sxs-lookup"><span data-stu-id="58892-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="58892-127">Servizi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="58892-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="58892-128">App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="58892-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="58892-129">Servizi mobili continua ad essere disponibile come servizio autonomo e rimane completamente supportato.</span><span class="sxs-lookup"><span data-stu-id="58892-129">Mobile Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="58892-130">App per dispositivi mobili è un tipo di app nel servizio app che integra tutte le funzionalità di Servizi mobili e altre.</span><span class="sxs-lookup"><span data-stu-id="58892-130">Mobile Apps is an app type in App Service, which integrates all of the functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="58892-131">La <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrazione da Servizi mobili ad App per dispositivi mobili</a> è molto semplice.</span><span class="sxs-lookup"><span data-stu-id="58892-131">It is easy to <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services to Mobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="58892-132">Come parte del servizio app, App per dispositivi mobili offre nuove funzionalità oltre a quelle di Servizi mobili, come l'integrazione con sistemi locali e SaaS, slot di gestione temporanea, Processi Web, opzioni di scalabilità migliorate e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="58892-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="58892-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Altre informazioni sulle App per dispositivi mobili</a>.</span><span class="sxs-lookup"><span data-stu-id="58892-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="58892-134">App per le API</span><span class="sxs-lookup"><span data-stu-id="58892-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="58892-135">App per le API è un nuovo tipo di app nel servizio app, che consente di creare e usare API nel cloud con estrema facilità.</span><span class="sxs-lookup"><span data-stu-id="58892-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in the cloud.</span></span></p>
<p><li><span data-ttu-id="58892-136"><a href="http://azure.microsoft.com/services/app-service/api/">Altre informazioni sulle API app</a>.</span><span class="sxs-lookup"><span data-stu-id="58892-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="58892-137">App per la logica</span><span class="sxs-lookup"><span data-stu-id="58892-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="58892-138">App per la logica è un nuovo tipo di app nel servizio app, che consente di automatizzare i processi aziendali con estrema facilità.</span><span class="sxs-lookup"><span data-stu-id="58892-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="58892-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Altre informazioni sulle App logica</a>.</span><span class="sxs-lookup"><span data-stu-id="58892-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="58892-140">Servizi BizTalk di Azure</span><span class="sxs-lookup"><span data-stu-id="58892-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="58892-141">App per le API di BizTalk</span><span class="sxs-lookup"><span data-stu-id="58892-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="58892-142">Servizi BizTalk continua a essere disponibile come servizio autonomo e rimane completamente supportato.</span><span class="sxs-lookup"><span data-stu-id="58892-142">BizTalk Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="58892-143">Tutte le funzionalità di Servizi BizTalk sono integrate nel servizio app come app per le API, consentendo agli utenti di eseguire l'integrazione di applicazioni aziendali e di scenari B2B con qualsiasi tipo di app del servizio app.</span><span class="sxs-lookup"><span data-stu-id="58892-143">All the capabilities of BizTalk Services are integrated into App Service as API Apps enabling users to perform enterprise application integration and B2B integration scenarios with any of the app types in App Service.</span></span></p>
<li><p><span data-ttu-id="58892-144">Con App per la logica è ora possibile automatizzare i processi aziendali usando un'esperienza di progettazione visiva per la creazione di flussi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="58892-144">With Logic Apps, you can now automate business processes using a visual design experience to create workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="58892-145">Per altre informazioni, vedere la [documentazione relativa al servizio app](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="58892-145">To learn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

