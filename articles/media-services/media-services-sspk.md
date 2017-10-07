---
title: "Microsoft® Smooth Streaming Client Porting Kit aaaLicensing"
description: "Informazioni su come toolicensing hello Microsoft® Smooth Streaming Client Porting Kit."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="ed766-103">Licenza per Microsoft® Smooth Streaming Client Porting Kit</span><span class="sxs-lookup"><span data-stu-id="ed766-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="ed766-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ed766-104">Overview</span></span>
<span data-ttu-id="ed766-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** breve) è un'implementazione client Smooth Streaming ottimizzata toohelp incorporato produttori di dispositivi, via cavo e operatori di telefonia mobile, i provider di servizi di contenuto, palmari produttori di fornitori di software indipendenti (ISV) e i prodotti toocreate di provider di soluzioni e servizi per la trasmissione di flussi adattivi in formato Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="ed766-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized toohelp embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers toocreate products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="ed766-106">SSPK è un'implementazione indipendente dal dispositivo e piattaforma del client Smooth Streaming che possono essere trasferite dalla piattaforma e hello Licenziatario tooany dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ed766-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by hello licensee tooany device and platform.</span></span> 

<span data-ttu-id="ed766-107">Incluso di seguito è un'architettura di alto livello e consente di IIS Smooth Streaming Porting Kit è hello Smooth Streaming Client implementazione fornita da Microsoft e di includere tutta la logica hello core per la riproduzione del contenuto Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="ed766-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is hello Smooth Streaming Client implementation provided by Microsoft and includes all hello core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="ed766-108">Questa implementazione viene quindi applicata dai partner a una piattaforma o un dispositivo specifico mediante l'implementazione di interfacce appropriate.</span><span class="sxs-lookup"><span data-stu-id="ed766-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="ed766-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ed766-110">Description</span></span>
<span data-ttu-id="ed766-111">SSPK è concesso in licenza a condizioni che offrono un valore aziendale eccellente.</span><span class="sxs-lookup"><span data-stu-id="ed766-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="ed766-112">Licenza SSPK fornisce settore hello con:</span><span class="sxs-lookup"><span data-stu-id="ed766-112">SSPK license provides hello industry with:</span></span>

* <span data-ttu-id="ed766-113">Codice sorgente di Smooth Streaming Porting Kit in C++</span><span class="sxs-lookup"><span data-stu-id="ed766-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="ed766-114">implementa la funzionalità client di Smooth Streaming Client</span><span class="sxs-lookup"><span data-stu-id="ed766-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="ed766-115">aggiunge analisi del formato, euristica, logica di buffering e così via.</span><span class="sxs-lookup"><span data-stu-id="ed766-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="ed766-116">API dell'applicazione lettore</span><span class="sxs-lookup"><span data-stu-id="ed766-116">Player application APIs</span></span> 
  * <span data-ttu-id="ed766-117">interfacce di programmazione per l'interazione con un'applicazione lettore multimediale</span><span class="sxs-lookup"><span data-stu-id="ed766-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="ed766-118">Interfaccia Platform Abstraction Layer (PAL)</span><span class="sxs-lookup"><span data-stu-id="ed766-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="ed766-119">interfacce di programmazione per l'interazione con il sistema operativo hello (thread, socket)</span><span class="sxs-lookup"><span data-stu-id="ed766-119">programming interfaces for interaction with hello operating system (threads, sockets)</span></span>
* <span data-ttu-id="ed766-120">Interfaccia Hardware Abstraction Layer (HAL)</span><span class="sxs-lookup"><span data-stu-id="ed766-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="ed766-121">interfacce di programmazione per l'interazione con un decodificatore A/V hardware (decodifica, rendering)</span><span class="sxs-lookup"><span data-stu-id="ed766-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="ed766-122">Interfaccia Digital Rights Management (DRM)</span><span class="sxs-lookup"><span data-stu-id="ed766-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="ed766-123">interfacce di programmazione per la gestione di DRM tramite hello DRM Abstraction Layer (DAL)</span><span class="sxs-lookup"><span data-stu-id="ed766-123">programming interfaces for handling DRM through hello DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="ed766-124">Microsoft PlayReady Porting Kit viene fornito separatamente, ma si integra tramite questa interfaccia.</span><span class="sxs-lookup"><span data-stu-id="ed766-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="ed766-125">Per altri dettagli sulle licenze Microsoft PlayReady Device, fare clic [qui](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span><span class="sxs-lookup"><span data-stu-id="ed766-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="ed766-126">Esempi di implementazione</span><span class="sxs-lookup"><span data-stu-id="ed766-126">Implementation samples</span></span> 
  * <span data-ttu-id="ed766-127">implementazione PAL di esempio per Linux</span><span class="sxs-lookup"><span data-stu-id="ed766-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="ed766-128">implementazione HAL di esempio per GStreamer</span><span class="sxs-lookup"><span data-stu-id="ed766-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="ed766-129">Opzioni di licenza</span><span class="sxs-lookup"><span data-stu-id="ed766-129">Licensing Options</span></span>
<span data-ttu-id="ed766-130">Microsoft Smooth Streaming Client Porting Kit viene effettuata toolicensees disponibile in due contratti di licenza distinte: una per lo sviluppo di Smooth Streaming Client provvisorio prodotti e un altro per la distribuzione agli utenti di tooend Smooth Streaming Client prodotto finale.</span><span class="sxs-lookup"><span data-stu-id="ed766-130">Microsoft Smooth Streaming Client Porting Kit is made available toolicensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products tooend users.</span></span>

* <span data-ttu-id="ed766-131">Per produttori chipset, integratori di sistema o software indipendenti (Vendor) che richiedono un codice di origine porting kit toodevelop provvisorio prodotti, una Microsoft Smooth Streaming Client Porting Kit **licenza del prodotto provvisorio** deve essere eseguito.</span><span class="sxs-lookup"><span data-stu-id="ed766-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit toodevelop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="ed766-132">Per i produttori di dispositivi o gli ISV che necessitano di diritti di distribuzione per gli utenti tooend Smooth Streaming Client finale prodotti, hello Microsoft Smooth Streaming Client Porting Kit **licenza del prodotto finale** deve essere eseguito.</span><span class="sxs-lookup"><span data-stu-id="ed766-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products tooend users, hello Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="ed766-133">Interim Product License di Microsoft Smooth Streaming Client Porting Kit</span><span class="sxs-lookup"><span data-stu-id="ed766-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="ed766-134">Con questa licenza, Microsoft offre un Smooth Streaming Client Porting Kit e hello toodevelop diritti di proprietà intellettuale necessari e distribuire Smooth Streaming Client provvisorio prodotti tooother Smooth Streaming Client Porting Kit dispositivo i titolari di licenze che distribuire Smooth Streaming Client prodotto finale.</span><span class="sxs-lookup"><span data-stu-id="ed766-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and hello necessary intellectual property rights toodevelop and distribute Smooth Streaming Client Interim Products tooother Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="ed766-135">Struttura tariffaria</span><span class="sxs-lookup"><span data-stu-id="ed766-135">Fee structure</span></span>
<span data-ttu-id="ed766-136">Una quota di licenza monouso 50.000 dollari fornisce accesso toohello Smooth Streaming Client Porting Kit.</span><span class="sxs-lookup"><span data-stu-id="ed766-136">A U.S. $50,000 one-time license fee provides access toohello Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="ed766-137">Final Product License di Microsoft Smooth Streaming Client Porting Kit</span><span class="sxs-lookup"><span data-stu-id="ed766-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="ed766-138">In questo tipo di licenza, Microsoft offre tutte le necessarie tooreceive di diritti di proprietà intellettuale Smooth Streaming Client provvisorio prodotti da altri licenziatari Smooth Streaming Client Porting Kit e toodistribute aziendale personalizzata Smooth Streaming Client finale Utenti tooend di prodotti.</span><span class="sxs-lookup"><span data-stu-id="ed766-138">Under this license, Microsoft offers all necessary intellectual property rights tooreceive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and toodistribute company-branded Smooth Streaming Client Final Products tooend users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="ed766-139">Struttura tariffaria</span><span class="sxs-lookup"><span data-stu-id="ed766-139">Fee structure</span></span>
<span data-ttu-id="ed766-140">Hello Smooth Streaming Client finale del prodotto è disponibile in un modello di royalty come in:</span><span class="sxs-lookup"><span data-stu-id="ed766-140">hello Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="ed766-141">USD 0,10 per ogni implementazione di dispositivo fornita</span><span class="sxs-lookup"><span data-stu-id="ed766-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="ed766-142">royalty Hello è limitato a 50.000 ogni anno</span><span class="sxs-lookup"><span data-stu-id="ed766-142">hello royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="ed766-143">Nessun diritto per le prime 10.000 implementazioni di dispositivi ogni anno</span><span class="sxs-lookup"><span data-stu-id="ed766-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="ed766-144">Procedura di gestione delle licenze e accesso a SSPK</span><span class="sxs-lookup"><span data-stu-id="ed766-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="ed766-145">Per domande relative alla gestione delle licenze, inviare un messaggio di posta elettronica a [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) .</span><span class="sxs-lookup"><span data-stu-id="ed766-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="ed766-146">Hello [portale distribuzione SSPK](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) è accessibile tooregistered licenziatari provvisorio.</span><span class="sxs-lookup"><span data-stu-id="ed766-146">hello [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible tooregistered Interim licensees.</span></span>

<span data-ttu-id="ed766-147">I titolari di licenze provvisorio e SSPK finale possono inviare domande tecniche troppo[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ed766-147">Interim and Final SSPK licensees can submit technical questions too[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="ed766-148">Licenziatari di contratti Microsoft Smooth Streaming Client Interim Product</span><span class="sxs-lookup"><span data-stu-id="ed766-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="ed766-149">Adroit Business Solutions, Inc</span><span class="sxs-lookup"><span data-stu-id="ed766-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="ed766-150">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="ed766-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="ed766-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="ed766-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="ed766-152">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="ed766-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="ed766-153">Alticast Corporation</span></span>
* <span data-ttu-id="ed766-154">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="ed766-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="ed766-155">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="ed766-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="ed766-156">AVC Multimedia Software Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="ed766-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="ed766-157">Cavium, Inc.</span></span>
* <span data-ttu-id="ed766-158">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="ed766-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="ed766-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="ed766-159">Enseo, Inc.</span></span>
* <span data-ttu-id="ed766-160">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="ed766-160">Fluendo S.A.</span></span>
* <span data-ttu-id="ed766-161">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="ed766-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="ed766-162">Infomir GMBH</span></span>
* <span data-ttu-id="ed766-163">Irdeto USA Inc.</span><span class="sxs-lookup"><span data-stu-id="ed766-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="ed766-164">iWEDIA S.A.</span><span class="sxs-lookup"><span data-stu-id="ed766-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="ed766-165">Liberty Global Services BV</span><span class="sxs-lookup"><span data-stu-id="ed766-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="ed766-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="ed766-166">MediaTek Inc.</span></span>
* <span data-ttu-id="ed766-167">MStar Co, Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="ed766-168">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="ed766-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="ed766-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="ed766-170">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="ed766-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="ed766-171">Sichuan Changhong Electric Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="ed766-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="ed766-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="ed766-172">SoftAtHome</span></span>
* <span data-ttu-id="ed766-173">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="ed766-173">Sony Corporation</span></span>
* <span data-ttu-id="ed766-174">Tatung Technology Inc.</span><span class="sxs-lookup"><span data-stu-id="ed766-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="ed766-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="ed766-176">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="ed766-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="ed766-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="ed766-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="ed766-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="ed766-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="ed766-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="ed766-180">Licenziatari di contratti Microsoft Smooth Streaming Client Final Product</span><span class="sxs-lookup"><span data-stu-id="ed766-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="ed766-181">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="ed766-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="ed766-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="ed766-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="ed766-183">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="ed766-184">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="ed766-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="ed766-185">AmTRAN Technology Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="ed766-186">Arcadyan Technology Corporation</span><span class="sxs-lookup"><span data-stu-id="ed766-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="ed766-187">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="ed766-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="ed766-188">ATMACA ELEKTRONİK SAN.</span><span class="sxs-lookup"><span data-stu-id="ed766-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="ed766-189">VE TİC.</span><span class="sxs-lookup"><span data-stu-id="ed766-189">VE TİC.</span></span> <span data-ttu-id="ed766-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="ed766-190">A.Ş</span></span>
* <span data-ttu-id="ed766-191">British Sky Broadcasting Limited</span><span class="sxs-lookup"><span data-stu-id="ed766-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="ed766-192">CastPal Technology Inc., Shenzhen</span><span class="sxs-lookup"><span data-stu-id="ed766-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="ed766-193">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="ed766-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="ed766-194">Dongguan Digital AV Technology Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="ed766-195">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="ed766-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="ed766-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="ed766-196">Enseo, Inc.</span></span>
* <span data-ttu-id="ed766-197">Filmflex Movies Limited</span><span class="sxs-lookup"><span data-stu-id="ed766-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="ed766-198">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="ed766-198">Fluendo S.A.</span></span>
* <span data-ttu-id="ed766-199">Gibson Innovations Limited</span><span class="sxs-lookup"><span data-stu-id="ed766-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="ed766-200">Haier Information Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="ed766-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="ed766-201">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="ed766-202">Hisense International Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="ed766-203">Homecast Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="ed766-203">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="ed766-204">Hon Hai Precision Industry Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="ed766-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="ed766-205">Infomir GMBH</span></span>
* <span data-ttu-id="ed766-206">Kaonmedia Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="ed766-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="ed766-207">KDDI Corporation</span></span>
* <span data-ttu-id="ed766-208">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="ed766-209">Orange SA</span><span class="sxs-lookup"><span data-stu-id="ed766-209">Orange SA</span></span>
* <span data-ttu-id="ed766-210">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="ed766-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="ed766-211">Sagemcom Broadband SAS</span><span class="sxs-lookup"><span data-stu-id="ed766-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="ed766-212">Shenzhen Coship Electronics CO., LTD</span><span class="sxs-lookup"><span data-stu-id="ed766-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="ed766-213">Shenzhen Jiuzhou Electric Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="ed766-213">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="ed766-214">Shenzhen Skyworth Digital Technology Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="ed766-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="ed766-215">Sichuan Changhong Electric Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="ed766-216">Skardin Industrial Corp.</span><span class="sxs-lookup"><span data-stu-id="ed766-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="ed766-217">Sky Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="ed766-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="ed766-218">SmarDTV S.A.</span><span class="sxs-lookup"><span data-stu-id="ed766-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="ed766-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="ed766-219">SoftAtHome</span></span>
* <span data-ttu-id="ed766-220">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="ed766-220">Sony Corporation</span></span>
* <span data-ttu-id="ed766-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span><span class="sxs-lookup"><span data-stu-id="ed766-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="ed766-222">Technicolor Delivery Technologies, SAS</span><span class="sxs-lookup"><span data-stu-id="ed766-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="ed766-223">Tongfang Global Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="ed766-224">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="ed766-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="ed766-225">Toshiba Lifestyle Products & Services Corporation</span><span class="sxs-lookup"><span data-stu-id="ed766-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="ed766-226">Universal Media Corporation /Slovakia/ s.r.o.</span><span class="sxs-lookup"><span data-stu-id="ed766-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="ed766-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="ed766-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="ed766-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="ed766-228">Wistron Corporation</span></span>
* <span data-ttu-id="ed766-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="ed766-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="ed766-230">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="ed766-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ed766-231">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="ed766-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

