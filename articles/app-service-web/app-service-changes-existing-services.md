---
title: aaaAzure servizio App e sul suo impatto sui servizi di Azure esistenti
description: "Viene illustrato come hello nuovo servizio App di Azure e le funzionalità di influire sulle servizi esistenti in Azure."
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
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="91e96-103">Servizio app di Azure e i servizi di Azure esistenti</span><span class="sxs-lookup"><span data-stu-id="91e96-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="91e96-104">Questo articolo vengono illustrati hello modifiche tooexisting servizi di Azure come parte dell'insieme di hello modifica toobring diversi servizi di Azure in [Azure App Service](https://azure.microsoft.com/services/app-service/), una nuova offerta integrata.</span><span class="sxs-lookup"><span data-stu-id="91e96-104">This article outlines hello changes tooexisting Azure services as part of hello change toobring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="91e96-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="91e96-105">Overview</span></span>
<span data-ttu-id="91e96-106">[Servizio App di Azure](https://azure.microsoft.com/services/app-service/) è un servizio cloud nuovi ed esclusivi che consente agli sviluppatori toocreate App web e dispositivi mobili per qualsiasi piattaforma e con qualsiasi dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91e96-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers toocreate web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="91e96-107">Servizio App è che toostreamline una soluzione integrata progettata ripetuto funzioni codifica, integrazione con sistemi di SaaS ed enterprise e automatizzare i processi di business mentre soddisfa le esigenze di sicurezza, affidabilità e la scalabilità.</span><span class="sxs-lookup"><span data-stu-id="91e96-107">App Service is an integrated solution designed toostreamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="91e96-108">Servizio App riunisce hello Azure esistenti seguenti servizi - [siti Web](https://azure.microsoft.com/services/websites/), [servizi mobili](https://azure.microsoft.com/services/mobile-services/), e [servizi Biztalk](https://azure.microsoft.com/services/biztalk-services/) in un'unica combinazione servizio, mentre aggiunta di nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="91e96-108">App Service brings together hello following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="91e96-109">Servizio App consente hello toohost seguenti tipi di app:</span><span class="sxs-lookup"><span data-stu-id="91e96-109">App Service allows you toohost hello following app types:</span></span>

* <span data-ttu-id="91e96-110">App Web</span><span class="sxs-lookup"><span data-stu-id="91e96-110">Web Apps</span></span>
* <span data-ttu-id="91e96-111">App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="91e96-111">Mobile Apps</span></span>
* <span data-ttu-id="91e96-112">App per le API</span><span class="sxs-lookup"><span data-stu-id="91e96-112">API Apps</span></span>
* <span data-ttu-id="91e96-113">App per la logica</span><span class="sxs-lookup"><span data-stu-id="91e96-113">Logic Apps</span></span>

<span data-ttu-id="91e96-114">Hello nella tabella seguente vengono illustrati Azure esistenti come servizi mapping tooApp hello e servizio app tipi disponibili in esso contenuti.</span><span class="sxs-lookup"><span data-stu-id="91e96-114">hello following table explains how existing Azure services map tooApp Service and hello app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="91e96-115">Servizio di Azure esistente</span><span class="sxs-lookup"><span data-stu-id="91e96-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="91e96-116">Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="91e96-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="91e96-117">Cosa è cambiato</span><span class="sxs-lookup"><span data-stu-id="91e96-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="91e96-118">Siti Web di Azure</span><span class="sxs-lookup"><span data-stu-id="91e96-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="91e96-119">App Web</span><span class="sxs-lookup"><span data-stu-id="91e96-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="91e96-120">Per i siti Web di Azure, servizio App è limitato esclusivamente toochanging hello Nome siti Web tooWeb app.</span><span class="sxs-lookup"><span data-stu-id="91e96-120">For Azure Websites, App Service is strictly limited toochanging hello name  Websites tooWeb Apps.</span></span>
<p><li><span data-ttu-id="91e96-121">Tutte le istanze esistenti di Siti Web sono ora app Web nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="91e96-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="91e96-122">È possibile accedere ai siti Web inclusi esistenti tramite hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">portale Azure</a>, quale è possibile trovare tutti i siti esistenti in <em>App Web</em>.</span><span class="sxs-lookup"><span data-stu-id="91e96-122">You can access your existing websites via hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="91e96-123"><em>Web piano di Hosting</em> è ora <em>piano di servizio App</em>.</span><span class="sxs-lookup"><span data-stu-id="91e96-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="91e96-124">Un <em>piano di servizio app</em> può ospitare qualsiasi tipo di servizio app, ad esempio app Web, per dispositivi mobili, per la logica o per le API.</span><span class="sxs-lookup"><span data-stu-id="91e96-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="91e96-125">App Web del servizio app di Azure si trova ora in stato di disponibilità generale.</span><span class="sxs-lookup"><span data-stu-id="91e96-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="91e96-126"><a href="http://azure.microsoft.com/services/app-service/web/">Altre informazioni sulle App Web</a>.</span><span class="sxs-lookup"><span data-stu-id="91e96-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="91e96-127">Servizi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="91e96-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="91e96-128">App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="91e96-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="91e96-129">Servizi mobili continuare toobe disponibile come servizio autonomo e rimangono completamente supportati.</span><span class="sxs-lookup"><span data-stu-id="91e96-129">Mobile Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="91e96-130">App per dispositivi mobili è un tipo di app nel servizio App, che integra le funzionalità di hello di servizi mobili e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="91e96-130">Mobile Apps is an app type in App Service, which integrates all of hello functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="91e96-131">È facile troppo<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">esegue la migrazione da servizi mobili tooMobile app</a>.</span><span class="sxs-lookup"><span data-stu-id="91e96-131">It is easy too<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services tooMobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="91e96-132">Come parte del servizio app, App per dispositivi mobili offre nuove funzionalità oltre a quelle di Servizi mobili, come l'integrazione con sistemi locali e SaaS, slot di gestione temporanea, Processi Web, opzioni di scalabilità migliorate e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="91e96-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="91e96-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Altre informazioni sulle App per dispositivi mobili</a>.</span><span class="sxs-lookup"><span data-stu-id="91e96-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="91e96-134">App per le API</span><span class="sxs-lookup"><span data-stu-id="91e96-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="91e96-135">App per le API è un nuovo tipo di app nel servizio App che consente di compilare facilmente e utilizzare le API in cloud hello.</span><span class="sxs-lookup"><span data-stu-id="91e96-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in hello cloud.</span></span></p>
<p><li><span data-ttu-id="91e96-136"><a href="http://azure.microsoft.com/services/app-service/api/">Altre informazioni sulle API app</a>.</span><span class="sxs-lookup"><span data-stu-id="91e96-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="91e96-137">App per la logica</span><span class="sxs-lookup"><span data-stu-id="91e96-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="91e96-138">App per la logica è un nuovo tipo di app nel servizio app, che consente di automatizzare i processi aziendali con estrema facilità.</span><span class="sxs-lookup"><span data-stu-id="91e96-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="91e96-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Altre informazioni sulle App logica</a>.</span><span class="sxs-lookup"><span data-stu-id="91e96-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="91e96-140">Servizi BizTalk di Azure</span><span class="sxs-lookup"><span data-stu-id="91e96-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="91e96-141">App per le API di BizTalk</span><span class="sxs-lookup"><span data-stu-id="91e96-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="91e96-142">Servizi BizTalk continuare toobe disponibile come servizio autonomo e rimangono completamente supportati.</span><span class="sxs-lookup"><span data-stu-id="91e96-142">BizTalk Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="91e96-143">Tutte le funzionalità di hello dei servizi BizTalk vengono integrate nel servizio App come App per le API abilitazione utenti tooperform enterprise application integration e scenari di integrazione B2B con uno qualsiasi dei tipi di app hello nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="91e96-143">All hello capabilities of BizTalk Services are integrated into App Service as API Apps enabling users tooperform enterprise application integration and B2B integration scenarios with any of hello app types in App Service.</span></span></p>
<li><p><span data-ttu-id="91e96-144">Logica App consentono di automatizzare i processi di business utilizzando un flussi di lavoro di progettazione visiva esperienza toocreate.</span><span class="sxs-lookup"><span data-stu-id="91e96-144">With Logic Apps, you can now automate business processes using a visual design experience toocreate workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="91e96-145">toolearn, visitare [documentazione del servizio App](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="91e96-145">toolearn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

