---
title: aaaHybrid progettazione di servizi multimediali di Azure usando i sottosistemi DRM | Documenti Microsoft
description: Questo articolo spiega come usare Servizi multimediali di Azure per la progettazione ibrida di sottosistemi DRM.
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 4206248420ccd4dbfc9a87a86f4763534c6254a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a><span data-ttu-id="cfd91-103">Progettazione ibrida di sottosistemi DRM</span><span class="sxs-lookup"><span data-stu-id="cfd91-103">Hybrid design of DRM subsystem(s)</span></span>

<span data-ttu-id="cfd91-104">Questo articolo spiega come usare Servizi multimediali di Azure per la progettazione ibrida di sottosistemi DRM.</span><span class="sxs-lookup"><span data-stu-id="cfd91-104">This topic discusses hybrid design of DRM subsystem(s) using Azure Media Services.</span></span>

## <a name="overview"></a><span data-ttu-id="cfd91-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="cfd91-105">Overview</span></span>

<span data-ttu-id="cfd91-106">Servizi multimediali di Azure fornisce il supporto per i seguenti tre sistema DRM hello:</span><span class="sxs-lookup"><span data-stu-id="cfd91-106">Azure Media Services provides support for hello following three DRM system:</span></span>

* <span data-ttu-id="cfd91-107">PlayReady</span><span class="sxs-lookup"><span data-stu-id="cfd91-107">PlayReady</span></span>
* <span data-ttu-id="cfd91-108">Widevine (modulare)</span><span class="sxs-lookup"><span data-stu-id="cfd91-108">Widevine (Modular)</span></span>
* <span data-ttu-id="cfd91-109">FairPlay</span><span class="sxs-lookup"><span data-stu-id="cfd91-109">FairPlay</span></span>

<span data-ttu-id="cfd91-110">supporto DRM Hello include crittografia DRM (crittografia dinamica) e il recapito di licenza, con Azure Media Player, che supporta tutti i 3 DRMs come un lettore di browser SDK.</span><span class="sxs-lookup"><span data-stu-id="cfd91-110">hello DRM support includes DRM encryption (dynamic encryption) and license delivery, with Azure Media Player supporting all 3 DRMs as a browser player SDK.</span></span>

<span data-ttu-id="cfd91-111">Per una trattazione dettagliata di DRM/CENC sottosistema progettazione e implementazione, vedere il documento hello intitolato [CENC con Multi-DRM e controllo di accesso](media-services-cenc-with-multidrm-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="cfd91-111">For a detailed treatment of DRM/CENC subsystem design and implementation, please see hello document titled [CENC with Multi-DRM and Access Control](media-services-cenc-with-multidrm-access-control.md).</span></span>

<span data-ttu-id="cfd91-112">Anche se è offrono supporto completo per i tre sistemi DRM, in alcuni casi i clienti devono toouse varie parti dell'infrastruttura/i propri sottosistemi toobuild di servizi multimediali tooAzure inoltre un sottosistema DRM ibrido.</span><span class="sxs-lookup"><span data-stu-id="cfd91-112">Although we offer complete support for three DRM systems, sometimes customers need toouse various parts of their own infrastructure/subsystems in addition tooAzure Media Services toobuild a hybrid DRM subsystem.</span></span>

<span data-ttu-id="cfd91-113">Di seguito sono riportate alcune delle domande comuni poste dai clienti:</span><span class="sxs-lookup"><span data-stu-id="cfd91-113">Below are some common questions asked by customers:</span></span>

* <span data-ttu-id="cfd91-114">"Posso usare i miei server licenze DRM?"</span><span class="sxs-lookup"><span data-stu-id="cfd91-114">"Can I use my own DRM license servers?"</span></span> <span data-ttu-id="cfd91-115">(in questo caso, i clienti hanno investito in un farm di licenze server DRM con logica di business incorporata)</span><span class="sxs-lookup"><span data-stu-id="cfd91-115">(In this case, customers have invested in DRM license server farm with embedded business logic).</span></span>
* <span data-ttu-id="cfd91-116">"Posso usare solo la funzionalità di distribuzione della licenza DRM di Servizi multimediali di Azure senza ospitare contenuti in AMS?"</span><span class="sxs-lookup"><span data-stu-id="cfd91-116">"Can I use only your DRM license delivery in Azure Media Services without hosting content in AMS?"</span></span>

## <a name="modularity-of-hello-ams-drm-platform"></a><span data-ttu-id="cfd91-117">Modularità di hello piattaforma AMS DRM</span><span class="sxs-lookup"><span data-stu-id="cfd91-117">Modularity of hello AMS DRM platform</span></span>

<span data-ttu-id="cfd91-118">In quanto parte di una piattaforma video cloud completa, DRM di Servizi multimediali di Azure è stato progettato all'insegna della flessibilità e modularità.</span><span class="sxs-lookup"><span data-stu-id="cfd91-118">As part of a comprehensive cloud video platform, Azure Media Services DRM has a design with flexibility and modularity in mind.</span></span> <span data-ttu-id="cfd91-119">È possibile utilizzare servizi multimediali di Azure con una delle seguenti combinazioni diverse, descritte nella seguente tabella hello (segue una spiegazione della notazione hello utilizzata nella tabella hello) hello.</span><span class="sxs-lookup"><span data-stu-id="cfd91-119">You can use Azure Media Services with any of hello following different combinations described in hello table below (an explanation of hello notation used in hello table follows).</span></span> 

|<span data-ttu-id="cfd91-120">**Hosting e origine del contenuto**</span><span class="sxs-lookup"><span data-stu-id="cfd91-120">**Content hosting & origin**</span></span>|<span data-ttu-id="cfd91-121">**Crittografia del contenuto**</span><span class="sxs-lookup"><span data-stu-id="cfd91-121">**Content encryption**</span></span>|<span data-ttu-id="cfd91-122">**Distribuzione di licenze DRM**</span><span class="sxs-lookup"><span data-stu-id="cfd91-122">**DRM license delivery**</span></span>|
|---|---|---|
|<span data-ttu-id="cfd91-123">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-123">AMS</span></span>|<span data-ttu-id="cfd91-124">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-124">AMS</span></span>|<span data-ttu-id="cfd91-125">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-125">AMS</span></span>|
|<span data-ttu-id="cfd91-126">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-126">AMS</span></span>|<span data-ttu-id="cfd91-127">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-127">AMS</span></span>|<span data-ttu-id="cfd91-128">Terze parti</span><span class="sxs-lookup"><span data-stu-id="cfd91-128">Third-party</span></span>|
|<span data-ttu-id="cfd91-129">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-129">AMS</span></span>|<span data-ttu-id="cfd91-130">Terze parti</span><span class="sxs-lookup"><span data-stu-id="cfd91-130">Third-party</span></span>|<span data-ttu-id="cfd91-131">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-131">AMS</span></span>|
|<span data-ttu-id="cfd91-132">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-132">AMS</span></span>|<span data-ttu-id="cfd91-133">Terze parti</span><span class="sxs-lookup"><span data-stu-id="cfd91-133">Third-party</span></span>|<span data-ttu-id="cfd91-134">Terze parti</span><span class="sxs-lookup"><span data-stu-id="cfd91-134">Third-party</span></span>|
|<span data-ttu-id="cfd91-135">Terze parti</span><span class="sxs-lookup"><span data-stu-id="cfd91-135">Third-party</span></span>|<span data-ttu-id="cfd91-136">Terze parti</span><span class="sxs-lookup"><span data-stu-id="cfd91-136">Third-party</span></span>|<span data-ttu-id="cfd91-137">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-137">AMS</span></span>|

### <a name="content-hosting--origin"></a><span data-ttu-id="cfd91-138">Hosting e origine del contenuto</span><span class="sxs-lookup"><span data-stu-id="cfd91-138">Content hosting & origin</span></span>

* <span data-ttu-id="cfd91-139">AMS: l'asset video è ospitato in AMS mentre lo streaming viene eseguito tramite gli endpoint di streaming (ma non necessariamente tramite la creazione dinamica dei pacchetti).</span><span class="sxs-lookup"><span data-stu-id="cfd91-139">AMS: video asset is hosted in AMS and streaming is through AMS streaming endpoints (but not necessarily dynamic packaging).</span></span>
* <span data-ttu-id="cfd91-140">Terze parti: il video è ospitato e distribuito su una piattaforma di streaming di terze parti, esterna ad AMS.</span><span class="sxs-lookup"><span data-stu-id="cfd91-140">Third-party: video is hosted and delivered on a third-party streaming platform outside of AMS.</span></span>

### <a name="content-encryption"></a><span data-ttu-id="cfd91-141">Crittografia del contenuto</span><span class="sxs-lookup"><span data-stu-id="cfd91-141">Content encryption</span></span>

* <span data-ttu-id="cfd91-142">AMS: la crittografia del contenuto viene eseguita dinamicamente/on demand dalla crittografia dinamica di AMS.</span><span class="sxs-lookup"><span data-stu-id="cfd91-142">AMS: content encryption is performed dynamically/on-demand by AMS dynamic encryption.</span></span>
* <span data-ttu-id="cfd91-143">Terze parti: la crittografia del contenuto viene eseguita all'esterno di AMS usando un flusso di lavoro di pre-elaborazione.</span><span class="sxs-lookup"><span data-stu-id="cfd91-143">Third-party: content encryption is performed outside of AMS using a pre-processing workflow.</span></span>

### <a name="drm-license-delivery"></a><span data-ttu-id="cfd91-144">Distribuzione di licenze DRM</span><span class="sxs-lookup"><span data-stu-id="cfd91-144">DRM license delivery</span></span>

* <span data-ttu-id="cfd91-145">AMS: la licenza di DRM viene distribuita dal servizio di distribuzione della licenza di AMS.</span><span class="sxs-lookup"><span data-stu-id="cfd91-145">AMS: DRM license is delivered by AMS license delivery service.</span></span>
* <span data-ttu-id="cfd91-146">Terze parti: la licenza di DRM viene distribuita da un server licenze DRM di terze parti esterno ad AMS.</span><span class="sxs-lookup"><span data-stu-id="cfd91-146">Third-party: DRM license is delivered by a third-party DRM license server outside of AMS.</span></span>

## <a name="configure-based-on-your-hybrid-scenario"></a><span data-ttu-id="cfd91-147">Configurare in base allo scenario ibrido</span><span class="sxs-lookup"><span data-stu-id="cfd91-147">Configure based on your hybrid scenario</span></span>

### <a name="content-key"></a><span data-ttu-id="cfd91-148">Chiave simmetrica</span><span class="sxs-lookup"><span data-stu-id="cfd91-148">Content key</span></span>

<span data-ttu-id="cfd91-149">La configurazione di una chiave simmetrica, è possibile controllare hello gli attributi di crittografia dinamica AMS sia il servizio di recapito licenza AMS seguenti:</span><span class="sxs-lookup"><span data-stu-id="cfd91-149">Through configuration of a content key, you can control hello following attributes of both AMS dynamic encryption and AMS license delivery service:</span></span>

* <span data-ttu-id="cfd91-150">chiave simmetrica Hello utilizzato per la crittografia dinamica DRM.</span><span class="sxs-lookup"><span data-stu-id="cfd91-150">hello content key used for dynamic DRM encryption.</span></span>
* <span data-ttu-id="cfd91-151">DRM licenza contenuto toobe recapitati da servizi multimediali di licenza: diritti, chiave simmetrica e le restrizioni.</span><span class="sxs-lookup"><span data-stu-id="cfd91-151">DRM license content toobe delivered by license delivery services: rights, content key and restrictions.</span></span>
* <span data-ttu-id="cfd91-152">Tipo di **limitazione dei criteri di autorizzazione della chiave simmetrica**: aperta, IP o limitazione del token.</span><span class="sxs-lookup"><span data-stu-id="cfd91-152">Type of **content key authorization policy restriction**: open, IP, or token restriction.</span></span>
* <span data-ttu-id="cfd91-153">Se **token** tipo **restrizione dei criteri di autorizzazione chiave del contenuto viene utilizzato**, hello **contenuto restrizione dei criteri di autorizzazione della chiave** devono essere soddisfatti prima del rilascio di una licenza.</span><span class="sxs-lookup"><span data-stu-id="cfd91-153">If **token** type of **content key authorization policy restriction is used**, hello **content key authorization policy restriction** must be met before a license is issued.</span></span>

### <a name="asset-delivery-policy"></a><span data-ttu-id="cfd91-154">Criteri di distribuzione degli asset</span><span class="sxs-lookup"><span data-stu-id="cfd91-154">Asset delivery policy</span></span>

<span data-ttu-id="cfd91-155">Tramite la configurazione di un criterio di recapito di asset, è possibile controllare hello gli attributi utilizzati da creazione dinamica dei pacchetti AMS e la crittografia dinamica di un sistema AMS di endpoint di streaming seguenti:</span><span class="sxs-lookup"><span data-stu-id="cfd91-155">Through configuration of an asset delivery policy, you can control hello following attributes used by AMS dynamic packager and dynamic encryption of an AMS streaming endpoint:</span></span>

* <span data-ttu-id="cfd91-156">Combinazione di protocollo di streaming e crittografia DRM, come DASH in CENC (PlayReady e Widevine), Smooth Streaming in PlayReady, HLS in Widevine o PlayReady.</span><span class="sxs-lookup"><span data-stu-id="cfd91-156">Streaming protocol and DRM encryption combination, such as DASH under CENC (PlayReady and Widevine), smooth streaming under PlayReady, HLS under Widevine or PlayReady.</span></span>
* <span data-ttu-id="cfd91-157">Hello predefinito/incorporati licenza recapito URL per ogni hello coinvolti DRMs.</span><span class="sxs-lookup"><span data-stu-id="cfd91-157">hello default/embedded license delivery URLs for each of hello involved DRMs.</span></span>
* <span data-ttu-id="cfd91-158">Presenza o meno di una stringa query per l'ID chiave (KID) di Widevine e Fairplay negli URL di acquisizione della licenza (LA_URL) nell'elenco di riproduzione DASH MPD o HLS.</span><span class="sxs-lookup"><span data-stu-id="cfd91-158">Whether license acquisition URLs (LA_URLs) in DASH MPD or HLS playlist contain query string of key ID (KID) for Widevine and FairPlay, respectively.</span></span>

## <a name="scenarios-and-samples"></a><span data-ttu-id="cfd91-159">Scenari ed esempi</span><span class="sxs-lookup"><span data-stu-id="cfd91-159">Scenarios and samples</span></span>

<span data-ttu-id="cfd91-160">In base a una spiegazione hello nella sezione precedente di hello, hello seguenti cinque scenari ibridi utilizza rispettivi **chiave simmetrica**-**criteri di distribuzione Asset** (Buongiorno combinazioni di configurazioni gli esempi indicati nell'ultima colonna hello seguono tabella hello):</span><span class="sxs-lookup"><span data-stu-id="cfd91-160">Based on hello explanations in hello previous section, hello following five hybrid scenarios use respective **Content key**-**Asset delivery policy** configuration combinations (hello samples mentioned in hello last column follow hello table):</span></span>

|<span data-ttu-id="cfd91-161">**Hosting e origine del contenuto**</span><span class="sxs-lookup"><span data-stu-id="cfd91-161">**Content hosting & origin**</span></span>|<span data-ttu-id="cfd91-162">**Crittografia DRM**</span><span class="sxs-lookup"><span data-stu-id="cfd91-162">**DRM encryption**</span></span>|<span data-ttu-id="cfd91-163">**Distribuzione di licenze DRM**</span><span class="sxs-lookup"><span data-stu-id="cfd91-163">**DRM license delivery**</span></span>|<span data-ttu-id="cfd91-164">**Configurare la chiave simmetrica**</span><span class="sxs-lookup"><span data-stu-id="cfd91-164">**Configure content key**</span></span>|<span data-ttu-id="cfd91-165">**Configurare i criteri di distribuzione dell'asset**</span><span class="sxs-lookup"><span data-stu-id="cfd91-165">**Configure asset delivery policy**</span></span>|<span data-ttu-id="cfd91-166">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="cfd91-166">**Sample**</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="cfd91-167">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-167">AMS</span></span>|<span data-ttu-id="cfd91-168">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-168">AMS</span></span>|<span data-ttu-id="cfd91-169">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-169">AMS</span></span>|<span data-ttu-id="cfd91-170">Sì</span><span class="sxs-lookup"><span data-stu-id="cfd91-170">Yes</span></span>|<span data-ttu-id="cfd91-171">Sì</span><span class="sxs-lookup"><span data-stu-id="cfd91-171">Yes</span></span>|<span data-ttu-id="cfd91-172">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="cfd91-172">Sample 1</span></span>|
|<span data-ttu-id="cfd91-173">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-173">AMS</span></span>|<span data-ttu-id="cfd91-174">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-174">AMS</span></span>|<span data-ttu-id="cfd91-175">Terze parti</span><span class="sxs-lookup"><span data-stu-id="cfd91-175">Third-party</span></span>|<span data-ttu-id="cfd91-176">Sì</span><span class="sxs-lookup"><span data-stu-id="cfd91-176">Yes</span></span>|<span data-ttu-id="cfd91-177">Sì</span><span class="sxs-lookup"><span data-stu-id="cfd91-177">Yes</span></span>|<span data-ttu-id="cfd91-178">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="cfd91-178">Sample 2</span></span>|
|<span data-ttu-id="cfd91-179">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-179">AMS</span></span>|<span data-ttu-id="cfd91-180">Terze parti</span><span class="sxs-lookup"><span data-stu-id="cfd91-180">Third-party</span></span>|<span data-ttu-id="cfd91-181">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-181">AMS</span></span>|<span data-ttu-id="cfd91-182">Sì</span><span class="sxs-lookup"><span data-stu-id="cfd91-182">Yes</span></span>|<span data-ttu-id="cfd91-183">No</span><span class="sxs-lookup"><span data-stu-id="cfd91-183">No</span></span>|<span data-ttu-id="cfd91-184">Esempio 3</span><span class="sxs-lookup"><span data-stu-id="cfd91-184">Sample 3</span></span>|
|<span data-ttu-id="cfd91-185">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-185">AMS</span></span>|<span data-ttu-id="cfd91-186">Terze parti</span><span class="sxs-lookup"><span data-stu-id="cfd91-186">Third-party</span></span>|<span data-ttu-id="cfd91-187">Esterno</span><span class="sxs-lookup"><span data-stu-id="cfd91-187">Outside</span></span>|<span data-ttu-id="cfd91-188">No</span><span class="sxs-lookup"><span data-stu-id="cfd91-188">No</span></span>|<span data-ttu-id="cfd91-189">No</span><span class="sxs-lookup"><span data-stu-id="cfd91-189">No</span></span>|<span data-ttu-id="cfd91-190">Esempio 4</span><span class="sxs-lookup"><span data-stu-id="cfd91-190">Sample 4</span></span>|
|<span data-ttu-id="cfd91-191">Terze parti</span><span class="sxs-lookup"><span data-stu-id="cfd91-191">Third-party</span></span>|<span data-ttu-id="cfd91-192">Terze parti</span><span class="sxs-lookup"><span data-stu-id="cfd91-192">Third-party</span></span>|<span data-ttu-id="cfd91-193">AMS</span><span class="sxs-lookup"><span data-stu-id="cfd91-193">AMS</span></span>|<span data-ttu-id="cfd91-194">Sì</span><span class="sxs-lookup"><span data-stu-id="cfd91-194">Yes</span></span>|<span data-ttu-id="cfd91-195">No</span><span class="sxs-lookup"><span data-stu-id="cfd91-195">No</span></span>|    

<span data-ttu-id="cfd91-196">Negli esempi di hello, PlayReady protection funziona per DASH e smooth streaming.</span><span class="sxs-lookup"><span data-stu-id="cfd91-196">In hello samples, PlayReady protection works for both DASH and smooth streaming.</span></span> <span data-ttu-id="cfd91-197">URL video Hello seguenti sono smooth streaming URL.</span><span class="sxs-lookup"><span data-stu-id="cfd91-197">hello video URLs below are smooth streaming URLs.</span></span> <span data-ttu-id="cfd91-198">tooget hello URL DASH corrispondenti, aggiungere solo "(formato = mpd-tempo-csf)".</span><span class="sxs-lookup"><span data-stu-id="cfd91-198">tooget hello corresponding DASH URLs, just append "(format=mpd-time-csf)".</span></span> <span data-ttu-id="cfd91-199">È possibile utilizzare hello [test di azure media player](http://aka.ms/amtest) tootest in un browser.</span><span class="sxs-lookup"><span data-stu-id="cfd91-199">You could use hello [azure media test player](http://aka.ms/amtest) tootest in a browser.</span></span> <span data-ttu-id="cfd91-200">Consente di tooconfigure cui streaming toouse di protocollo, in cui tecnico.</span><span class="sxs-lookup"><span data-stu-id="cfd91-200">It allows you tooconfigure which streaming protocol toouse, under which tech.</span></span> <span data-ttu-id="cfd91-201">IE11 e MS Edge in Windows 10 supportano PlayReady tramite EME.</span><span class="sxs-lookup"><span data-stu-id="cfd91-201">IE11 and MS Edge on Windows 10 support PlayReady through EME.</span></span> <span data-ttu-id="cfd91-202">Per ulteriori informazioni, vedere [informazioni dettagliate su hello testare strumento](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span><span class="sxs-lookup"><span data-stu-id="cfd91-202">For more information, see [details about hello test tool](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span></span>

### <a name="sample-1"></a><span data-ttu-id="cfd91-203">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="cfd91-203">Sample 1</span></span>

* <span data-ttu-id="cfd91-204">URL di origine (di base): https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="cfd91-204">Source (base) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span></span> 
* <span data-ttu-id="cfd91-205">LA_URL di PlayReady (DASH e smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="cfd91-205">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 
* <span data-ttu-id="cfd91-206">LA_URL di Widevine (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span><span class="sxs-lookup"><span data-stu-id="cfd91-206">Widevine LA_URL (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span></span> 
* <span data-ttu-id="cfd91-207">LA_URL di FairPlay (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span><span class="sxs-lookup"><span data-stu-id="cfd91-207">FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span></span> 

### <a name="sample-2"></a><span data-ttu-id="cfd91-208">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="cfd91-208">Sample 2</span></span>

* <span data-ttu-id="cfd91-209">URL di origine (di base): http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="cfd91-209">Source (base) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span></span> 
* <span data-ttu-id="cfd91-210">LA_URL di PlayReady (DASH e smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span><span class="sxs-lookup"><span data-stu-id="cfd91-210">PlayReady LA_URL (DASH & smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span></span> 

### <a name="sample-3"></a><span data-ttu-id="cfd91-211">Esempio 3</span><span class="sxs-lookup"><span data-stu-id="cfd91-211">Sample 3</span></span>

* <span data-ttu-id="cfd91-212">URL di origine: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="cfd91-212">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="cfd91-213">LA_URL di PlayReady (DASH e smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="cfd91-213">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 

### <a name="sample-4"></a><span data-ttu-id="cfd91-214">Esempio 4</span><span class="sxs-lookup"><span data-stu-id="cfd91-214">Sample 4</span></span>

* <span data-ttu-id="cfd91-215">URL di origine: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="cfd91-215">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="cfd91-216">LA_URL di PlayReady (DASH e smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span><span class="sxs-lookup"><span data-stu-id="cfd91-216">PlayReady LA_URL (DASH & smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span></span> 

## <a name="summary"></a><span data-ttu-id="cfd91-217">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="cfd91-217">Summary</span></span>

<span data-ttu-id="cfd91-218">In sintesi, i componenti DRM di Servizi multimediali di Azure sono flessibili ed è possibile usarli in uno scenario ibrido configurando correttamente la chiave simmetrica e i criteri di distribuzione della licenza, come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="cfd91-218">In summary, Azure Media Services DRM components are flexible, you can use them in a hybrid scenario by properly configuring content key and asset delivery policy, as described in this topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfd91-219">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cfd91-219">Next steps</span></span>
<span data-ttu-id="cfd91-220">Visualizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="cfd91-220">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cfd91-221">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="cfd91-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

