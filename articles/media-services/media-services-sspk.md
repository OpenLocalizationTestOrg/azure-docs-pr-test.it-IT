---
title: "Licenza per Microsoft® Smooth Streaming Client Porting Kit"
description: "Informazioni su come ottenere la licenza per Microsoft® Smooth Streaming Client Porting Kit."
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
ms.openlocfilehash: b5a36ac6771bef220afe29446cd56c1b65a498d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="a0132-103">Licenza per Microsoft® Smooth Streaming Client Porting Kit</span><span class="sxs-lookup"><span data-stu-id="a0132-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="a0132-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a0132-104">Overview</span></span>
<span data-ttu-id="a0132-105">Microsoft Smooth Streaming Client Porting Kit,**SSPK** per brevità, è un'implementazione client di Smooth Streaming ottimizzata per aiutare i produttori di dispositivi integrati, operatori di telefonia via cavo e mobile, provider di servizi di gestione del contenuto, produttori di telefoni, fornitori di software indipendenti (ISV) e provider di soluzioni a creare prodotti e servizi per la trasmissione di flussi adattivi in formato Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="a0132-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized to help embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers to create products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="a0132-106">SSPK è un'implementazione indipendente dal dispositivo e dalla piattaforma del client Smooth Streaming che può essere applicata dal licenziatario a qualsiasi dispositivo e piattaforma.</span><span class="sxs-lookup"><span data-stu-id="a0132-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by the licensee to any device and platform.</span></span> 

<span data-ttu-id="a0132-107">Di seguito è riportata un'architettura di alto livello che include la casella IIS Smooth Streaming Porting Kit, ovvero l'implementazione client di Smooth Streaming fornita da Microsoft, e tutta la logica di base per la riproduzione di contenuto Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="a0132-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is the Smooth Streaming Client implementation provided by Microsoft and includes all the core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="a0132-108">Questa implementazione viene quindi applicata dai partner a una piattaforma o un dispositivo specifico mediante l'implementazione di interfacce appropriate.</span><span class="sxs-lookup"><span data-stu-id="a0132-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="a0132-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a0132-110">Description</span></span>
<span data-ttu-id="a0132-111">SSPK è concesso in licenza a condizioni che offrono un valore aziendale eccellente.</span><span class="sxs-lookup"><span data-stu-id="a0132-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="a0132-112">La licenza SSPK offre al settore:</span><span class="sxs-lookup"><span data-stu-id="a0132-112">SSPK license provides the industry with:</span></span>

* <span data-ttu-id="a0132-113">Codice sorgente di Smooth Streaming Porting Kit in C++</span><span class="sxs-lookup"><span data-stu-id="a0132-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="a0132-114">implementa la funzionalità client di Smooth Streaming Client</span><span class="sxs-lookup"><span data-stu-id="a0132-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="a0132-115">aggiunge analisi del formato, euristica, logica di buffering e così via.</span><span class="sxs-lookup"><span data-stu-id="a0132-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="a0132-116">API dell'applicazione lettore</span><span class="sxs-lookup"><span data-stu-id="a0132-116">Player application APIs</span></span> 
  * <span data-ttu-id="a0132-117">interfacce di programmazione per l'interazione con un'applicazione lettore multimediale</span><span class="sxs-lookup"><span data-stu-id="a0132-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="a0132-118">Interfaccia Platform Abstraction Layer (PAL)</span><span class="sxs-lookup"><span data-stu-id="a0132-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="a0132-119">interfacce di programmazione per l'interazione con il sistema operativo (thread, socket)</span><span class="sxs-lookup"><span data-stu-id="a0132-119">programming interfaces for interaction with the operating system (threads, sockets)</span></span>
* <span data-ttu-id="a0132-120">Interfaccia Hardware Abstraction Layer (HAL)</span><span class="sxs-lookup"><span data-stu-id="a0132-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="a0132-121">interfacce di programmazione per l'interazione con un decodificatore A/V hardware (decodifica, rendering)</span><span class="sxs-lookup"><span data-stu-id="a0132-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="a0132-122">Interfaccia Digital Rights Management (DRM)</span><span class="sxs-lookup"><span data-stu-id="a0132-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="a0132-123">interfacce di programmazione per la gestione di DRM tramite DRM Abstraction Layer (DAL)</span><span class="sxs-lookup"><span data-stu-id="a0132-123">programming interfaces for handling DRM through the DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="a0132-124">Microsoft PlayReady Porting Kit viene fornito separatamente, ma si integra tramite questa interfaccia.</span><span class="sxs-lookup"><span data-stu-id="a0132-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="a0132-125">Per altri dettagli sulle licenze Microsoft PlayReady Device, fare clic [qui](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span><span class="sxs-lookup"><span data-stu-id="a0132-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="a0132-126">Esempi di implementazione</span><span class="sxs-lookup"><span data-stu-id="a0132-126">Implementation samples</span></span> 
  * <span data-ttu-id="a0132-127">implementazione PAL di esempio per Linux</span><span class="sxs-lookup"><span data-stu-id="a0132-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="a0132-128">implementazione HAL di esempio per GStreamer</span><span class="sxs-lookup"><span data-stu-id="a0132-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="a0132-129">Opzioni di licenza</span><span class="sxs-lookup"><span data-stu-id="a0132-129">Licensing Options</span></span>
<span data-ttu-id="a0132-130">Microsoft Smooth Streaming Client Porting Kit è disponibile per i licenziatari con due contratti di licenza distinti: uno per lo sviluppo di prodotti provvisori per il client Smooth Streaming e un altro per la distribuzione di prodotti finali per il client Smooth Streaming agli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="a0132-130">Microsoft Smooth Streaming Client Porting Kit is made available to licensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products to end users.</span></span>

* <span data-ttu-id="a0132-131">Per i produttori di chipset, gli integratori di sistema o i fornitori di software indipendenti (ISV) che necessitano di un kit per il porting del codice sorgente per sviluppare prodotti provvisori, è consigliabile usare una **Interim Product License** di Microsoft Smooth Streaming Client Porting Kit.</span><span class="sxs-lookup"><span data-stu-id="a0132-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit to develop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="a0132-132">Per i produttori di dispositivi o gli ISV che necessitano di diritti di distribuzione di prodotti finali per il client Smooth Streaming agli utenti finali, è consigliabile usare una **Final Product License** di Microsoft Smooth Streaming Client Porting Kit.</span><span class="sxs-lookup"><span data-stu-id="a0132-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products to end users, the Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="a0132-133">Interim Product License di Microsoft Smooth Streaming Client Porting Kit</span><span class="sxs-lookup"><span data-stu-id="a0132-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="a0132-134">In base alle condizioni di questa licenza, Microsoft offre Smooth Streaming Client Porting Kit e i diritti di proprietà intellettuale necessari per sviluppare e distribuire prodotti provvisori per il client Smooth Streaming ad altri licenziatari di dispositivi Smooth Streaming Client Porting Kit che distribuiscono prodotti finali per il client Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="a0132-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and the necessary intellectual property rights to develop and distribute Smooth Streaming Client Interim Products to other Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="a0132-135">Struttura tariffaria</span><span class="sxs-lookup"><span data-stu-id="a0132-135">Fee structure</span></span>
<span data-ttu-id="a0132-136">Una tariffa di licenza unica di USD 50.000 fornisce l'accesso a Smooth Streaming Client Porting Kit.</span><span class="sxs-lookup"><span data-stu-id="a0132-136">A U.S. $50,000 one-time license fee provides access to the Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="a0132-137">Final Product License di Microsoft Smooth Streaming Client Porting Kit</span><span class="sxs-lookup"><span data-stu-id="a0132-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="a0132-138">In base alle condizioni di questa licenza, Microsoft offre tutti i diritti di proprietà intellettuale necessari per ricevere prodotti provvisori per il client Smooth Streaming da altri licenziatari di Smooth Streaming Client Porting Kit e per distribuire prodotti finali con personalizzazione della società per il client Smooth Streaming agli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="a0132-138">Under this license, Microsoft offers all necessary intellectual property rights to receive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and to distribute company-branded Smooth Streaming Client Final Products to end users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="a0132-139">Struttura tariffaria</span><span class="sxs-lookup"><span data-stu-id="a0132-139">Fee structure</span></span>
<span data-ttu-id="a0132-140">Smooth Streaming Client Final Product è disponibile in un modello a pagamento come segue:</span><span class="sxs-lookup"><span data-stu-id="a0132-140">The Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="a0132-141">USD 0,10 per ogni implementazione di dispositivo fornita</span><span class="sxs-lookup"><span data-stu-id="a0132-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="a0132-142">I diritti sono limitati a un massimo di USD 50.000 all'anno</span><span class="sxs-lookup"><span data-stu-id="a0132-142">The royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="a0132-143">Nessun diritto per le prime 10.000 implementazioni di dispositivi ogni anno</span><span class="sxs-lookup"><span data-stu-id="a0132-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="a0132-144">Procedura di gestione delle licenze e accesso a SSPK</span><span class="sxs-lookup"><span data-stu-id="a0132-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="a0132-145">Per domande relative alla gestione delle licenze, inviare un messaggio di posta elettronica a [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) .</span><span class="sxs-lookup"><span data-stu-id="a0132-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="a0132-146">Il [portale di distribuzione di SSPK](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) è accessibile a licenziatari della versione Interim registrati.</span><span class="sxs-lookup"><span data-stu-id="a0132-146">The [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible to registered Interim licensees.</span></span>

<span data-ttu-id="a0132-147">I licenziatari di SSPK Interim e Final possono inviare domande tecniche a [smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a0132-147">Interim and Final SSPK licensees can submit technical questions to [smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="a0132-148">Licenziatari di contratti Microsoft Smooth Streaming Client Interim Product</span><span class="sxs-lookup"><span data-stu-id="a0132-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="a0132-149">Adroit Business Solutions, Inc</span><span class="sxs-lookup"><span data-stu-id="a0132-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="a0132-150">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="a0132-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="a0132-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="a0132-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="a0132-152">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="a0132-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="a0132-153">Alticast Corporation</span></span>
* <span data-ttu-id="a0132-154">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="a0132-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="a0132-155">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="a0132-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="a0132-156">AVC Multimedia Software Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="a0132-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="a0132-157">Cavium, Inc.</span></span>
* <span data-ttu-id="a0132-158">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="a0132-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="a0132-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="a0132-159">Enseo, Inc.</span></span>
* <span data-ttu-id="a0132-160">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="a0132-160">Fluendo S.A.</span></span>
* <span data-ttu-id="a0132-161">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="a0132-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="a0132-162">Infomir GMBH</span></span>
* <span data-ttu-id="a0132-163">Irdeto USA Inc.</span><span class="sxs-lookup"><span data-stu-id="a0132-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="a0132-164">iWEDIA S.A.</span><span class="sxs-lookup"><span data-stu-id="a0132-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="a0132-165">Liberty Global Services BV</span><span class="sxs-lookup"><span data-stu-id="a0132-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="a0132-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="a0132-166">MediaTek Inc.</span></span>
* <span data-ttu-id="a0132-167">MStar Co, Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="a0132-168">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="a0132-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="a0132-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="a0132-170">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="a0132-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="a0132-171">Sichuan Changhong Electric Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="a0132-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="a0132-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="a0132-172">SoftAtHome</span></span>
* <span data-ttu-id="a0132-173">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="a0132-173">Sony Corporation</span></span>
* <span data-ttu-id="a0132-174">Tatung Technology Inc.</span><span class="sxs-lookup"><span data-stu-id="a0132-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="a0132-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="a0132-176">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="a0132-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="a0132-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="a0132-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="a0132-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="a0132-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="a0132-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="a0132-180">Licenziatari di contratti Microsoft Smooth Streaming Client Final Product</span><span class="sxs-lookup"><span data-stu-id="a0132-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="a0132-181">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="a0132-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="a0132-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="a0132-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="a0132-183">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="a0132-184">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="a0132-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="a0132-185">AmTRAN Technology Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="a0132-186">Arcadyan Technology Corporation</span><span class="sxs-lookup"><span data-stu-id="a0132-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="a0132-187">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="a0132-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="a0132-188">ATMACA ELEKTRONİK SAN.</span><span class="sxs-lookup"><span data-stu-id="a0132-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="a0132-189">VE TİC.</span><span class="sxs-lookup"><span data-stu-id="a0132-189">VE TİC.</span></span> <span data-ttu-id="a0132-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="a0132-190">A.Ş</span></span>
* <span data-ttu-id="a0132-191">British Sky Broadcasting Limited</span><span class="sxs-lookup"><span data-stu-id="a0132-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="a0132-192">CastPal Technology Inc., Shenzhen</span><span class="sxs-lookup"><span data-stu-id="a0132-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="a0132-193">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="a0132-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="a0132-194">Dongguan Digital AV Technology Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="a0132-195">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="a0132-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="a0132-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="a0132-196">Enseo, Inc.</span></span>
* <span data-ttu-id="a0132-197">Filmflex Movies Limited</span><span class="sxs-lookup"><span data-stu-id="a0132-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="a0132-198">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="a0132-198">Fluendo S.A.</span></span>
* <span data-ttu-id="a0132-199">Gibson Innovations Limited</span><span class="sxs-lookup"><span data-stu-id="a0132-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="a0132-200">Haier Information Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="a0132-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="a0132-201">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="a0132-202">Hisense International Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="a0132-203">Homecast Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="a0132-203">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="a0132-204">Hon Hai Precision Industry Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="a0132-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="a0132-205">Infomir GMBH</span></span>
* <span data-ttu-id="a0132-206">Kaonmedia Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="a0132-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="a0132-207">KDDI Corporation</span></span>
* <span data-ttu-id="a0132-208">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="a0132-209">Orange SA</span><span class="sxs-lookup"><span data-stu-id="a0132-209">Orange SA</span></span>
* <span data-ttu-id="a0132-210">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="a0132-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="a0132-211">Sagemcom Broadband SAS</span><span class="sxs-lookup"><span data-stu-id="a0132-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="a0132-212">Shenzhen Coship Electronics CO., LTD</span><span class="sxs-lookup"><span data-stu-id="a0132-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="a0132-213">Shenzhen Jiuzhou Electric Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="a0132-213">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="a0132-214">Shenzhen Skyworth Digital Technology Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="a0132-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="a0132-215">Sichuan Changhong Electric Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="a0132-216">Skardin Industrial Corp.</span><span class="sxs-lookup"><span data-stu-id="a0132-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="a0132-217">Sky Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="a0132-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="a0132-218">SmarDTV S.A.</span><span class="sxs-lookup"><span data-stu-id="a0132-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="a0132-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="a0132-219">SoftAtHome</span></span>
* <span data-ttu-id="a0132-220">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="a0132-220">Sony Corporation</span></span>
* <span data-ttu-id="a0132-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span><span class="sxs-lookup"><span data-stu-id="a0132-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="a0132-222">Technicolor Delivery Technologies, SAS</span><span class="sxs-lookup"><span data-stu-id="a0132-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="a0132-223">Tongfang Global Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="a0132-224">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="a0132-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="a0132-225">Toshiba Lifestyle Products & Services Corporation</span><span class="sxs-lookup"><span data-stu-id="a0132-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="a0132-226">Universal Media Corporation /Slovakia/ s.r.o.</span><span class="sxs-lookup"><span data-stu-id="a0132-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="a0132-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="a0132-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="a0132-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="a0132-228">Wistron Corporation</span></span>
* <span data-ttu-id="a0132-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="a0132-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="a0132-230">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="a0132-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a0132-231">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="a0132-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

