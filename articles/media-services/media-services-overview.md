---
title: Panoramica di Servizi multimediali di Azure | Microsoft Docs
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
ms.openlocfilehash: 2a175aed40b9775d9a4de6877eb3467b43819568
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-media-services-overview"></a><span data-ttu-id="1946c-103">Panoramica di Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="1946c-103">Azure Media Services overview</span></span> 

<span data-ttu-id="1946c-104">Servizi multimediali di Microsoft Azure costituisce una piattaforma estensibile basata sul cloud che consente agli sviluppatori di creare applicazioni di distribuzione e gestione di contenuti multimediali altamente scalabili.</span><span class="sxs-lookup"><span data-stu-id="1946c-104">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers to build scalable media management and delivery applications.</span></span> <span data-ttu-id="1946c-105">Servizi multimediali si basa su API REST che consentono di caricare, archiviare e codificare contenuti video o audio in modo sicuro, nonché creare pacchetti di tali contenuti per la distribuzione in streaming live e on demand a vari client (ad esempio, TV, PC e dispositivi mobili).</span><span class="sxs-lookup"><span data-stu-id="1946c-105">Media Services is based on REST APIs that enable you to securely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery to various clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="1946c-106">È possibile creare flussi di lavoro end-to-end usando unicamente Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="1946c-106">You can build end-to-end workflows using entirely Media Services.</span></span> <span data-ttu-id="1946c-107">È anche possibile usare componenti di terze parti per alcune parti del flusso di lavoro,</span><span class="sxs-lookup"><span data-stu-id="1946c-107">You can also choose to use third-party components for some parts of your workflow.</span></span> <span data-ttu-id="1946c-108">ad esempio, la codifica con un codificatore di terze parti.</span><span class="sxs-lookup"><span data-stu-id="1946c-108">For example, encode using a third-party encoder.</span></span> <span data-ttu-id="1946c-109">Inoltre, sono possibili operazioni di caricamento, protezione, creazione di pacchetti e invio tramite Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="1946c-109">Then, upload, protect, package, deliver using Media Services.</span></span>

<span data-ttu-id="1946c-110">È possibile optare per lo streaming dei contenuti live o on demand.</span><span class="sxs-lookup"><span data-stu-id="1946c-110">You can choose to stream your content live or deliver content on-demand.</span></span> <span data-ttu-id="1946c-111">L'argomento contiene inoltre collegamenti ad altri argomenti rilevanti.</span><span class="sxs-lookup"><span data-stu-id="1946c-111">The topic also links to other relevant topics.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="1946c-112">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1946c-112">Media Services learning paths</span></span>
<span data-ttu-id="1946c-113">È possibile visualizzare i percorsi di apprendimento AMS qui:</span><span class="sxs-lookup"><span data-stu-id="1946c-113">You can view AMS learning paths here:</span></span>

* [<span data-ttu-id="1946c-114">Flusso di lavoro AMS Live Streaming</span><span class="sxs-lookup"><span data-stu-id="1946c-114">AMS Live Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [<span data-ttu-id="1946c-115">Flusso di lavoro dello streaming on demand di AMS</span><span class="sxs-lookup"><span data-stu-id="1946c-115">AMS on-Demand Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a><span data-ttu-id="1946c-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1946c-116">Prerequisites</span></span>

<span data-ttu-id="1946c-117">Per iniziare a utilizzare Servizi multimediali di Azure, è necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="1946c-117">To start using Azure Media Services, you should have the following:</span></span>

* <span data-ttu-id="1946c-118">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="1946c-118">An Azure account.</span></span> <span data-ttu-id="1946c-119">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="1946c-119">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1946c-120">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="1946c-120">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="1946c-121">Un account di Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="1946c-121">An Azure Media Services account.</span></span> <span data-ttu-id="1946c-122">Per altre informazioni, vedere [Creare un account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="1946c-122">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="1946c-123">(Facoltativo) Configurare l'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="1946c-123">(Optional) Set up development environment.</span></span> <span data-ttu-id="1946c-124">Scegliere .NET o API REST per l'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="1946c-124">Choose .NET or REST API for your development environment.</span></span> <span data-ttu-id="1946c-125">Per altre informazioni, vedere [Configurare l'ambiente](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="1946c-125">For more information, see [Set up environment](media-services-dotnet-how-to-use.md).</span></span>

    <span data-ttu-id="1946c-126">Sono anche disponibili informazioni su come [connettersi all'API AMS a livello di codice](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="1946c-126">Also, learn how to [connect  programmatically to AMS API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
* <span data-ttu-id="1946c-127">Un endpoint di streaming Standard o Premium con stato avviato.</span><span class="sxs-lookup"><span data-stu-id="1946c-127">A standard or premium streaming endpoint in started state.</span></span>  <span data-ttu-id="1946c-128">Per altre informazioni, vedere [Gestione degli endpoint di streaming](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="1946c-128">For more information, see [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md)</span></span>

## <a name="sdks-and-tools"></a><span data-ttu-id="1946c-129">SDK e strumenti</span><span class="sxs-lookup"><span data-stu-id="1946c-129">SDKs and tools</span></span>

<span data-ttu-id="1946c-130">Per creare soluzioni di Servizi multimediali, è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="1946c-130">To build Media Services solutions, you can use:</span></span>

* [<span data-ttu-id="1946c-131">API REST di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1946c-131">Media Services REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* <span data-ttu-id="1946c-132">Uno dei client SDK disponibili:</span><span class="sxs-lookup"><span data-stu-id="1946c-132">One of the available client SDKs:</span></span>
    * <span data-ttu-id="1946c-133">[Azure Media Services SDK per .NET](https://github.com/Azure/azure-sdk-for-media-services)</span><span class="sxs-lookup"><span data-stu-id="1946c-133">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services),</span></span>
    * <span data-ttu-id="1946c-134">[Azure SDK per Java](https://github.com/Azure/azure-sdk-for-java),</span><span class="sxs-lookup"><span data-stu-id="1946c-134">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java),</span></span>
    * <span data-ttu-id="1946c-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span><span class="sxs-lookup"><span data-stu-id="1946c-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span></span>
    * <span data-ttu-id="1946c-136">[Servizi multimediali di Azure per Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js). Questa è una versione non Microsoft di Node.js SDK.</span><span class="sxs-lookup"><span data-stu-id="1946c-136">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (This is a non-Microsoft version of a Node.js SDK.</span></span> <span data-ttu-id="1946c-137">È gestita da una community e attualmente non copre al 100% le API AMS.</span><span class="sxs-lookup"><span data-stu-id="1946c-137">It is maintained by a community and currently does not have a 100% coverage of the AMS APIs).</span></span>
* <span data-ttu-id="1946c-138">Strumenti esistenti:</span><span class="sxs-lookup"><span data-stu-id="1946c-138">Existing tools:</span></span>
    * [<span data-ttu-id="1946c-139">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1946c-139">Azure portal</span></span>](https://portal.azure.com/)
    * <span data-ttu-id="1946c-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) è un'applicazione Winforms/C# per Windows)</span><span class="sxs-lookup"><span data-stu-id="1946c-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is a Winforms/C# application for Windows)</span></span>

## <a name="concepts-and-overview"></a><span data-ttu-id="1946c-141">Panoramica e concetti</span><span class="sxs-lookup"><span data-stu-id="1946c-141">Concepts and overview</span></span>
<span data-ttu-id="1946c-142">Per i concetti relativi ai Servizi multimediali di Azure, vedere [Concetti su Servizi multimediali di Azure](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="1946c-142">For Azure Media Services concepts, see [Concepts](media-services-concepts.md).</span></span>

<span data-ttu-id="1946c-143">Per una serie di procedure che illustra tutti i componenti principali di Servizi multimediali di Azure, vedere la pagina relativa alle [esercitazioni dettagliate sui Servizi multimediali di Azure](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span><span class="sxs-lookup"><span data-stu-id="1946c-143">For a how-to series that introduces you to all the main components of Azure Media Services, see [Azure Media Services Step-by-Step tutorials](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span></span> <span data-ttu-id="1946c-144">Questa serie offre un'ottima panoramica dei concetti e usa lo strumento AMSE per illustrare le attività AMS.</span><span class="sxs-lookup"><span data-stu-id="1946c-144">This series has a great overview of concepts and it uses the AMSE tool to demonstrate AMS tasks.</span></span> <span data-ttu-id="1946c-145">AMSE è uno strumento Windows.</span><span class="sxs-lookup"><span data-stu-id="1946c-145">AMSE tool is a Windows tool.</span></span> <span data-ttu-id="1946c-146">Supporta la maggior parte delle attività che è possibile eseguire a livello di codice con [AMS SDK per .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK per Java](https://github.com/Azure/azure-sdk-for-java) o [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span><span class="sxs-lookup"><span data-stu-id="1946c-146">This tool supports most of the tasks you can achieve programmatically with [AMS SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java), or  [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span></span>

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a><span data-ttu-id="1946c-147">Scenari supportati e disponibilità di Servizi multimediali nei data center</span><span class="sxs-lookup"><span data-stu-id="1946c-147">Supported scenarios and availability of Media Services across data centers</span></span>

<span data-ttu-id="1946c-148">Per informazioni dettagliate, vedere [Scenari supportati e disponibilità di Servizi multimediali nei data center](scenarios-and-availability.md).</span><span class="sxs-lookup"><span data-stu-id="1946c-148">For detailed information, see [AMS scenarios and availability of features and services across data centers](scenarios-and-availability.md).</span></span>

## <a name="service-level-agreement-sla"></a><span data-ttu-id="1946c-149">Contratto di servizio (SLA)</span><span class="sxs-lookup"><span data-stu-id="1946c-149">Service Level Agreement (SLA)</span></span>

* <span data-ttu-id="1946c-150">Per il servizio di codifica di Servizi multimediali, è garantita una disponibilità al 99,9% delle transazioni delle API REST.</span><span class="sxs-lookup"><span data-stu-id="1946c-150">For Media Services Encoding, we guarantee 99.9% availability of REST API transactions.</span></span>
* <span data-ttu-id="1946c-151">Con l'acquisto di un endpoint di streaming Standard o Premium, per il servizio di streaming, è garantita una disponibilità al 99,9% per i contenuti multimediali esistenti.</span><span class="sxs-lookup"><span data-stu-id="1946c-151">For Streaming, we will successfully service requests with a 99.9% availability guarantee for existing media content when a standard or premium streaming endpoint is purchased.</span></span>
* <span data-ttu-id="1946c-152">Per i canali live, è garantito che i canali in esecuzione avranno connettività esterna per almeno il 99,9% del tempo.</span><span class="sxs-lookup"><span data-stu-id="1946c-152">For Live Channels, we guarantee that running Channels will have external connectivity at least 99.9% of the time.</span></span>
* <span data-ttu-id="1946c-153">Per la protezione del contenuto, è garantita l'evasione delle richieste di chiavi per almeno il 99,9% del tempo.</span><span class="sxs-lookup"><span data-stu-id="1946c-153">For Content Protection, we guarantee that we will successfully fulfill key requests at least 99.9% of the time.</span></span>
* <span data-ttu-id="1946c-154">Per l'indicizzatore, è garantito che verranno soddisfatte le richieste di attività dell'indicizzatore elaborate con un'unità riservata di codifica per il 99,9% del tempo.</span><span class="sxs-lookup"><span data-stu-id="1946c-154">For Indexer, we will successfully service Indexer Task requests processed with an Encoding Reserved Unit 99.9% of the time.</span></span>

<span data-ttu-id="1946c-155">Per altre informazioni, vedere [Contratto di servizio di Microsoft Azure](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="1946c-155">For more information, see [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="1946c-156">Per informazioni sulla disponibilità nei data center, vedere la sezione relativa alla [disponibilità](scenarios-and-availability.md#availability).</span><span class="sxs-lookup"><span data-stu-id="1946c-156">For information about availability in datacenters, see the [Avaiability](scenarios-and-availability.md#availability) section.</span></span>

## <a name="support"></a><span data-ttu-id="1946c-157">Supporto</span><span class="sxs-lookup"><span data-stu-id="1946c-157">Support</span></span>

<span data-ttu-id="1946c-158">[supporto tecnico di Azure](https://azure.microsoft.com/support/options/) fornisce opzioni di supporto per Azure, compreso Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="1946c-158">[Azure Support](https://azure.microsoft.com/support/options/) provides support options for Azure, including Media Services.</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="1946c-159">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="1946c-159">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
