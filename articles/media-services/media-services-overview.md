---
title: Panoramica di servizi multimediali aaaAzure | Documenti Microsoft
description: Questo argomento fornisce informazioni generali su Servizi multimediali di Azure
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a><span data-ttu-id="ad170-103">Panoramica di Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="ad170-103">Azure Media Services overview</span></span> 

<span data-ttu-id="ad170-104">Servizi multimediali di Microsoft Azure è una piattaforma estendibile basato su cloud che consente agli sviluppatori toobuild contenuti multimediali altamente scalabili distribuzione e gestione delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ad170-104">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers toobuild scalable media management and delivery applications.</span></span> <span data-ttu-id="ad170-105">Servizi multimediali è basato sulle API REST che consentono di caricamento toosecurely, archiviare, codificare e creare il pacchetto di contenuto video o audio per su richiesta e live streaming toovarious client di recapito (ad esempio, TV, PC e dispositivi mobili).</span><span class="sxs-lookup"><span data-stu-id="ad170-105">Media Services is based on REST APIs that enable you toosecurely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery toovarious clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="ad170-106">È possibile creare flussi di lavoro end-to-end usando unicamente Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="ad170-106">You can build end-to-end workflows using entirely Media Services.</span></span> <span data-ttu-id="ad170-107">È anche possibile scegliere toouse componenti di terze parti per alcune parti del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ad170-107">You can also choose toouse third-party components for some parts of your workflow.</span></span> <span data-ttu-id="ad170-108">ad esempio, la codifica con un codificatore di terze parti.</span><span class="sxs-lookup"><span data-stu-id="ad170-108">For example, encode using a third-party encoder.</span></span> <span data-ttu-id="ad170-109">Inoltre, sono possibili operazioni di caricamento, protezione, creazione di pacchetti e invio tramite Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="ad170-109">Then, upload, protect, package, deliver using Media Services.</span></span>

<span data-ttu-id="ad170-110">È possibile scegliere toostream il contenuto in tempo reale o fornire contenuto su richiesta.</span><span class="sxs-lookup"><span data-stu-id="ad170-110">You can choose toostream your content live or deliver content on-demand.</span></span> <span data-ttu-id="ad170-111">argomento Hello è anche possibile collegare tooother relativi argomenti.</span><span class="sxs-lookup"><span data-stu-id="ad170-111">hello topic also links tooother relevant topics.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ad170-112">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="ad170-112">Media Services learning paths</span></span>
<span data-ttu-id="ad170-113">È possibile visualizzare i percorsi di apprendimento AMS qui:</span><span class="sxs-lookup"><span data-stu-id="ad170-113">You can view AMS learning paths here:</span></span>

* [<span data-ttu-id="ad170-114">Flusso di lavoro AMS Live Streaming</span><span class="sxs-lookup"><span data-stu-id="ad170-114">AMS Live Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [<span data-ttu-id="ad170-115">Flusso di lavoro dello streaming on demand di AMS</span><span class="sxs-lookup"><span data-stu-id="ad170-115">AMS on-Demand Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a><span data-ttu-id="ad170-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ad170-116">Prerequisites</span></span>

<span data-ttu-id="ad170-117">toostart tramite servizi multimediali di Azure, è necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="ad170-117">toostart using Azure Media Services, you should have hello following:</span></span>

* <span data-ttu-id="ad170-118">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="ad170-118">An Azure account.</span></span> <span data-ttu-id="ad170-119">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="ad170-119">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ad170-120">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ad170-120">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="ad170-121">Un account di Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="ad170-121">An Azure Media Services account.</span></span> <span data-ttu-id="ad170-122">Per altre informazioni, vedere [Creare un account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="ad170-122">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="ad170-123">(Facoltativo) Configurare l'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="ad170-123">(Optional) Set up development environment.</span></span> <span data-ttu-id="ad170-124">Scegliere .NET o API REST per l'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="ad170-124">Choose .NET or REST API for your development environment.</span></span> <span data-ttu-id="ad170-125">Per altre informazioni, vedere [Configurare l'ambiente](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="ad170-125">For more information, see [Set up environment](media-services-dotnet-how-to-use.md).</span></span>

    <span data-ttu-id="ad170-126">Inoltre, informazioni su come troppo[connettersi a livello di programmazione tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="ad170-126">Also, learn how too[connect  programmatically tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
* <span data-ttu-id="ad170-127">Un endpoint di streaming Standard o Premium con stato avviato.</span><span class="sxs-lookup"><span data-stu-id="ad170-127">A standard or premium streaming endpoint in started state.</span></span>  <span data-ttu-id="ad170-128">Per altre informazioni, vedere [Gestione degli endpoint di streaming](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="ad170-128">For more information, see [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md)</span></span>

## <a name="sdks-and-tools"></a><span data-ttu-id="ad170-129">SDK e strumenti</span><span class="sxs-lookup"><span data-stu-id="ad170-129">SDKs and tools</span></span>

<span data-ttu-id="ad170-130">soluzioni di servizi multimediali toobuild, è possibile utilizzare:</span><span class="sxs-lookup"><span data-stu-id="ad170-130">toobuild Media Services solutions, you can use:</span></span>

* [<span data-ttu-id="ad170-131">API REST di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="ad170-131">Media Services REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* <span data-ttu-id="ad170-132">Uno dei client disponibili hello SDK:</span><span class="sxs-lookup"><span data-stu-id="ad170-132">One of hello available client SDKs:</span></span>
    * <span data-ttu-id="ad170-133">[Azure Media Services SDK per .NET](https://github.com/Azure/azure-sdk-for-media-services)</span><span class="sxs-lookup"><span data-stu-id="ad170-133">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services),</span></span>
    * <span data-ttu-id="ad170-134">[Azure SDK per Java](https://github.com/Azure/azure-sdk-for-java),</span><span class="sxs-lookup"><span data-stu-id="ad170-134">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java),</span></span>
    * <span data-ttu-id="ad170-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span><span class="sxs-lookup"><span data-stu-id="ad170-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span></span>
    * <span data-ttu-id="ad170-136">[Servizi multimediali di Azure per Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js). Questa è una versione non Microsoft di Node.js SDK.</span><span class="sxs-lookup"><span data-stu-id="ad170-136">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (This is a non-Microsoft version of a Node.js SDK.</span></span> <span data-ttu-id="ad170-137">Viene mantenuto da una community e non sono attualmente una copertura del 100% di hello AMS APIs).</span><span class="sxs-lookup"><span data-stu-id="ad170-137">It is maintained by a community and currently does not have a 100% coverage of hello AMS APIs).</span></span>
* <span data-ttu-id="ad170-138">Strumenti esistenti:</span><span class="sxs-lookup"><span data-stu-id="ad170-138">Existing tools:</span></span>
    * [<span data-ttu-id="ad170-139">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ad170-139">Azure portal</span></span>](https://portal.azure.com/)
    * <span data-ttu-id="ad170-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) è un'applicazione Winforms/C# per Windows)</span><span class="sxs-lookup"><span data-stu-id="ad170-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is a Winforms/C# application for Windows)</span></span>

## <a name="concepts-and-overview"></a><span data-ttu-id="ad170-141">Panoramica e concetti</span><span class="sxs-lookup"><span data-stu-id="ad170-141">Concepts and overview</span></span>
<span data-ttu-id="ad170-142">Per i concetti relativi ai Servizi multimediali di Azure, vedere [Concetti su Servizi multimediali di Azure](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="ad170-142">For Azure Media Services concepts, see [Concepts](media-services-concepts.md).</span></span>

<span data-ttu-id="ad170-143">Per una procedura-tooseries che presentano le componenti principali di hello tooall di servizi multimediali di Azure, vedere [esercitazioni di Azure Media Services dettagliata](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span><span class="sxs-lookup"><span data-stu-id="ad170-143">For a how-tooseries that introduces you tooall hello main components of Azure Media Services, see [Azure Media Services Step-by-Step tutorials](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span></span> <span data-ttu-id="ad170-144">Questa serie contiene una panoramica dei concetti e utilizza le attività di hello AMSE strumento toodemonstrate AMS.</span><span class="sxs-lookup"><span data-stu-id="ad170-144">This series has a great overview of concepts and it uses hello AMSE tool toodemonstrate AMS tasks.</span></span> <span data-ttu-id="ad170-145">AMSE è uno strumento Windows.</span><span class="sxs-lookup"><span data-stu-id="ad170-145">AMSE tool is a Windows tool.</span></span> <span data-ttu-id="ad170-146">Questo strumento supporta la maggior parte delle attività hello è possibile ottenere a livello di codice con [AMS SDK per .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK per Java](https://github.com/Azure/azure-sdk-for-java), o [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span><span class="sxs-lookup"><span data-stu-id="ad170-146">This tool supports most of hello tasks you can achieve programmatically with [AMS SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java), or  [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span></span>

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a><span data-ttu-id="ad170-147">Scenari supportati e disponibilità di Servizi multimediali nei data center</span><span class="sxs-lookup"><span data-stu-id="ad170-147">Supported scenarios and availability of Media Services across data centers</span></span>

<span data-ttu-id="ad170-148">Per informazioni dettagliate, vedere [Scenari supportati e disponibilità di Servizi multimediali nei data center](scenarios-and-availability.md).</span><span class="sxs-lookup"><span data-stu-id="ad170-148">For detailed information, see [AMS scenarios and availability of features and services across data centers](scenarios-and-availability.md).</span></span>

## <a name="service-level-agreement-sla"></a><span data-ttu-id="ad170-149">Contratto di servizio (SLA)</span><span class="sxs-lookup"><span data-stu-id="ad170-149">Service Level Agreement (SLA)</span></span>

* <span data-ttu-id="ad170-150">Per il servizio di codifica di Servizi multimediali, è garantita una disponibilità al 99,9% delle transazioni delle API REST.</span><span class="sxs-lookup"><span data-stu-id="ad170-150">For Media Services Encoding, we guarantee 99.9% availability of REST API transactions.</span></span>
* <span data-ttu-id="ad170-151">Con l'acquisto di un endpoint di streaming Standard o Premium, per il servizio di streaming, è garantita una disponibilità al 99,9% per i contenuti multimediali esistenti.</span><span class="sxs-lookup"><span data-stu-id="ad170-151">For Streaming, we will successfully service requests with a 99.9% availability guarantee for existing media content when a standard or premium streaming endpoint is purchased.</span></span>
* <span data-ttu-id="ad170-152">Per i canali Live, si garantisce che l'esecuzione di canali connettività esterna almeno il 99,9% del tempo di hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-152">For Live Channels, we guarantee that running Channels will have external connectivity at least 99.9% of hello time.</span></span>
* <span data-ttu-id="ad170-153">Per la protezione del contenuto, è garantito che è verrà correttamente soddisfare richieste di chiavi almeno il 99,9% del tempo di hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-153">For Content Protection, we guarantee that we will successfully fulfill key requests at least 99.9% of hello time.</span></span>
* <span data-ttu-id="ad170-154">Per un indicizzatore, è, il servizio indicizzatore attività elaborata con una codifica di riservato unità 99,9% del tempo di hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-154">For Indexer, we will successfully service Indexer Task requests processed with an Encoding Reserved Unit 99.9% of hello time.</span></span>

<span data-ttu-id="ad170-155">Per altre informazioni, vedere [Contratto di servizio di Microsoft Azure](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="ad170-155">For more information, see [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="ad170-156">Per informazioni sulla disponibilità in Data Center, vedere hello [Avaiability](scenarios-and-availability.md#availability) sezione.</span><span class="sxs-lookup"><span data-stu-id="ad170-156">For information about availability in datacenters, see hello [Avaiability](scenarios-and-availability.md#availability) section.</span></span>

## <a name="support"></a><span data-ttu-id="ad170-157">Supporto</span><span class="sxs-lookup"><span data-stu-id="ad170-157">Support</span></span>

<span data-ttu-id="ad170-158">[supporto tecnico di Azure](https://azure.microsoft.com/support/options/) fornisce opzioni di supporto per Azure, compreso Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="ad170-158">[Azure Support](https://azure.microsoft.com/support/options/) provides support options for Azure, including Media Services.</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="ad170-159">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="ad170-159">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
