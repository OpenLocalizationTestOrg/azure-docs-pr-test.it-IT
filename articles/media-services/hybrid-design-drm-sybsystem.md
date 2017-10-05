---
title: Uso di Servizi multimediali di Azure per la progettazione ibrida di sottosistemi DRM | Microsoft Docs
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
ms.openlocfilehash: 841b1164db6fd1a2c029b98392509c15f23158e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a><span data-ttu-id="8157f-103">Progettazione ibrida di sottosistemi DRM</span><span class="sxs-lookup"><span data-stu-id="8157f-103">Hybrid design of DRM subsystem(s)</span></span>

<span data-ttu-id="8157f-104">Questo articolo spiega come usare Servizi multimediali di Azure per la progettazione ibrida di sottosistemi DRM.</span><span class="sxs-lookup"><span data-stu-id="8157f-104">This topic discusses hybrid design of DRM subsystem(s) using Azure Media Services.</span></span>

## <a name="overview"></a><span data-ttu-id="8157f-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8157f-105">Overview</span></span>

<span data-ttu-id="8157f-106">Servizi multimediali di Azure offre supporto per i seguenti tre sistemi DRM:</span><span class="sxs-lookup"><span data-stu-id="8157f-106">Azure Media Services provides support for the following three DRM system:</span></span>

* <span data-ttu-id="8157f-107">PlayReady</span><span class="sxs-lookup"><span data-stu-id="8157f-107">PlayReady</span></span>
* <span data-ttu-id="8157f-108">Widevine (modulare)</span><span class="sxs-lookup"><span data-stu-id="8157f-108">Widevine (Modular)</span></span>
* <span data-ttu-id="8157f-109">FairPlay</span><span class="sxs-lookup"><span data-stu-id="8157f-109">FairPlay</span></span>

<span data-ttu-id="8157f-110">Il supporto per DRM include la crittografia DRM (crittografia dinamica) e la distribuzione della licenza, quando Azure Media Player supporta tutti e 3 i DRM come un SDK per lettore di browser.</span><span class="sxs-lookup"><span data-stu-id="8157f-110">The DRM support includes DRM encryption (dynamic encryption) and license delivery, with Azure Media Player supporting all 3 DRMs as a browser player SDK.</span></span>

<span data-ttu-id="8157f-111">Per una spiegazione dettagliata della progettazione e implementazione dei sottosistemi DRM/CENC, vedere il documento intitolato [CENC with Multi-DRM and Access Control](media-services-cenc-with-multidrm-access-control.md) (CENC con più DRM e controllo dell'accesso).</span><span class="sxs-lookup"><span data-stu-id="8157f-111">For a detailed treatment of DRM/CENC subsystem design and implementation, please see the document titled [CENC with Multi-DRM and Access Control](media-services-cenc-with-multidrm-access-control.md).</span></span>

<span data-ttu-id="8157f-112">Sebbene Microsoft offra un supporto completo per tutti e 3 i sistemi DRM, i clienti hanno talvolta l'esigenza di usare varie parti della propria infrastruttura/dei propri sottosistemi, oltre a Servizi multimediali di Azure, per creare un sottosistema DRM ibrido.</span><span class="sxs-lookup"><span data-stu-id="8157f-112">Although we offer complete support for three DRM systems, sometimes customers need to use various parts of their own infrastructure/subsystems in addition to Azure Media Services to build a hybrid DRM subsystem.</span></span>

<span data-ttu-id="8157f-113">Di seguito sono riportate alcune delle domande comuni poste dai clienti:</span><span class="sxs-lookup"><span data-stu-id="8157f-113">Below are some common questions asked by customers:</span></span>

* <span data-ttu-id="8157f-114">"Posso usare i miei server licenze DRM?"</span><span class="sxs-lookup"><span data-stu-id="8157f-114">"Can I use my own DRM license servers?"</span></span> <span data-ttu-id="8157f-115">(in questo caso, i clienti hanno investito in un farm di licenze server DRM con logica di business incorporata)</span><span class="sxs-lookup"><span data-stu-id="8157f-115">(In this case, customers have invested in DRM license server farm with embedded business logic).</span></span>
* <span data-ttu-id="8157f-116">"Posso usare solo la funzionalità di distribuzione della licenza DRM di Servizi multimediali di Azure senza ospitare contenuti in AMS?"</span><span class="sxs-lookup"><span data-stu-id="8157f-116">"Can I use only your DRM license delivery in Azure Media Services without hosting content in AMS?"</span></span>

## <a name="modularity-of-the-ams-drm-platform"></a><span data-ttu-id="8157f-117">Modularità della piattaforma DRM di AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-117">Modularity of the AMS DRM platform</span></span>

<span data-ttu-id="8157f-118">In quanto parte di una piattaforma video cloud completa, DRM di Servizi multimediali di Azure è stato progettato all'insegna della flessibilità e modularità.</span><span class="sxs-lookup"><span data-stu-id="8157f-118">As part of a comprehensive cloud video platform, Azure Media Services DRM has a design with flexibility and modularity in mind.</span></span> <span data-ttu-id="8157f-119">È possibile usare Servizi multimediali di Azure con una delle seguenti combinazioni diverse elencate nella seguente tabella (di seguito è riportata anche una spiegazione della notazione usata nella tabella).</span><span class="sxs-lookup"><span data-stu-id="8157f-119">You can use Azure Media Services with any of the following different combinations described in the table below (an explanation of the notation used in the table follows).</span></span> 

|<span data-ttu-id="8157f-120">**Hosting e origine del contenuto**</span><span class="sxs-lookup"><span data-stu-id="8157f-120">**Content hosting & origin**</span></span>|<span data-ttu-id="8157f-121">**Crittografia del contenuto**</span><span class="sxs-lookup"><span data-stu-id="8157f-121">**Content encryption**</span></span>|<span data-ttu-id="8157f-122">**Distribuzione di licenze DRM**</span><span class="sxs-lookup"><span data-stu-id="8157f-122">**DRM license delivery**</span></span>|
|---|---|---|
|<span data-ttu-id="8157f-123">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-123">AMS</span></span>|<span data-ttu-id="8157f-124">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-124">AMS</span></span>|<span data-ttu-id="8157f-125">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-125">AMS</span></span>|
|<span data-ttu-id="8157f-126">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-126">AMS</span></span>|<span data-ttu-id="8157f-127">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-127">AMS</span></span>|<span data-ttu-id="8157f-128">Terze parti</span><span class="sxs-lookup"><span data-stu-id="8157f-128">Third-party</span></span>|
|<span data-ttu-id="8157f-129">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-129">AMS</span></span>|<span data-ttu-id="8157f-130">Terze parti</span><span class="sxs-lookup"><span data-stu-id="8157f-130">Third-party</span></span>|<span data-ttu-id="8157f-131">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-131">AMS</span></span>|
|<span data-ttu-id="8157f-132">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-132">AMS</span></span>|<span data-ttu-id="8157f-133">Terze parti</span><span class="sxs-lookup"><span data-stu-id="8157f-133">Third-party</span></span>|<span data-ttu-id="8157f-134">Terze parti</span><span class="sxs-lookup"><span data-stu-id="8157f-134">Third-party</span></span>|
|<span data-ttu-id="8157f-135">Terze parti</span><span class="sxs-lookup"><span data-stu-id="8157f-135">Third-party</span></span>|<span data-ttu-id="8157f-136">Terze parti</span><span class="sxs-lookup"><span data-stu-id="8157f-136">Third-party</span></span>|<span data-ttu-id="8157f-137">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-137">AMS</span></span>|

### <a name="content-hosting--origin"></a><span data-ttu-id="8157f-138">Hosting e origine del contenuto</span><span class="sxs-lookup"><span data-stu-id="8157f-138">Content hosting & origin</span></span>

* <span data-ttu-id="8157f-139">AMS: l'asset video è ospitato in AMS mentre lo streaming viene eseguito tramite gli endpoint di streaming (ma non necessariamente tramite la creazione dinamica dei pacchetti).</span><span class="sxs-lookup"><span data-stu-id="8157f-139">AMS: video asset is hosted in AMS and streaming is through AMS streaming endpoints (but not necessarily dynamic packaging).</span></span>
* <span data-ttu-id="8157f-140">Terze parti: il video è ospitato e distribuito su una piattaforma di streaming di terze parti, esterna ad AMS.</span><span class="sxs-lookup"><span data-stu-id="8157f-140">Third-party: video is hosted and delivered on a third-party streaming platform outside of AMS.</span></span>

### <a name="content-encryption"></a><span data-ttu-id="8157f-141">Crittografia del contenuto</span><span class="sxs-lookup"><span data-stu-id="8157f-141">Content encryption</span></span>

* <span data-ttu-id="8157f-142">AMS: la crittografia del contenuto viene eseguita dinamicamente/on demand dalla crittografia dinamica di AMS.</span><span class="sxs-lookup"><span data-stu-id="8157f-142">AMS: content encryption is performed dynamically/on-demand by AMS dynamic encryption.</span></span>
* <span data-ttu-id="8157f-143">Terze parti: la crittografia del contenuto viene eseguita all'esterno di AMS usando un flusso di lavoro di pre-elaborazione.</span><span class="sxs-lookup"><span data-stu-id="8157f-143">Third-party: content encryption is performed outside of AMS using a pre-processing workflow.</span></span>

### <a name="drm-license-delivery"></a><span data-ttu-id="8157f-144">Distribuzione di licenze DRM</span><span class="sxs-lookup"><span data-stu-id="8157f-144">DRM license delivery</span></span>

* <span data-ttu-id="8157f-145">AMS: la licenza di DRM viene distribuita dal servizio di distribuzione della licenza di AMS.</span><span class="sxs-lookup"><span data-stu-id="8157f-145">AMS: DRM license is delivered by AMS license delivery service.</span></span>
* <span data-ttu-id="8157f-146">Terze parti: la licenza di DRM viene distribuita da un server licenze DRM di terze parti esterno ad AMS.</span><span class="sxs-lookup"><span data-stu-id="8157f-146">Third-party: DRM license is delivered by a third-party DRM license server outside of AMS.</span></span>

## <a name="configure-based-on-your-hybrid-scenario"></a><span data-ttu-id="8157f-147">Configurare in base allo scenario ibrido</span><span class="sxs-lookup"><span data-stu-id="8157f-147">Configure based on your hybrid scenario</span></span>

### <a name="content-key"></a><span data-ttu-id="8157f-148">Chiave simmetrica</span><span class="sxs-lookup"><span data-stu-id="8157f-148">Content key</span></span>

<span data-ttu-id="8157f-149">La configurazione di una chiave simmetrica permette di controllare i seguenti attributi della crittografia dinamica e del servizio di distribuzione della licenza di AMS:</span><span class="sxs-lookup"><span data-stu-id="8157f-149">Through configuration of a content key, you can control the following attributes of both AMS dynamic encryption and AMS license delivery service:</span></span>

* <span data-ttu-id="8157f-150">Chiave simmetrica usata per la crittografia dinamica di DRM.</span><span class="sxs-lookup"><span data-stu-id="8157f-150">The content key used for dynamic DRM encryption.</span></span>
* <span data-ttu-id="8157f-151">Contenuto della licenza DRM da distribuire tramite i servizi di distribuzione della licenza: diritti, chiave simmetrica e limitazioni.</span><span class="sxs-lookup"><span data-stu-id="8157f-151">DRM license content to be delivered by license delivery services: rights, content key and restrictions.</span></span>
* <span data-ttu-id="8157f-152">Tipo di **limitazione dei criteri di autorizzazione della chiave simmetrica**: aperta, IP o limitazione del token.</span><span class="sxs-lookup"><span data-stu-id="8157f-152">Type of **content key authorization policy restriction**: open, IP, or token restriction.</span></span>
* <span data-ttu-id="8157f-153">Se si usa il **token** per la **limitazione dei criteri di autorizzazione della chiave simmetrica**, è necessario che venga soddisfatta **questa limitazione** prima che la licenza possa essere rilasciata.</span><span class="sxs-lookup"><span data-stu-id="8157f-153">If **token** type of **content key authorization policy restriction is used**, the **content key authorization policy restriction** must be met before a license is issued.</span></span>

### <a name="asset-delivery-policy"></a><span data-ttu-id="8157f-154">Criteri di distribuzione degli asset</span><span class="sxs-lookup"><span data-stu-id="8157f-154">Asset delivery policy</span></span>

<span data-ttu-id="8157f-155">La configurazione di criteri di distribuzione di un asset permette di controllare i seguenti attributi usati dalla creazione di pacchetti dinamica e dalla crittografia dinamica di AMS di un endpoint di streaming AMS:</span><span class="sxs-lookup"><span data-stu-id="8157f-155">Through configuration of an asset delivery policy, you can control the following attributes used by AMS dynamic packager and dynamic encryption of an AMS streaming endpoint:</span></span>

* <span data-ttu-id="8157f-156">Combinazione di protocollo di streaming e crittografia DRM, come DASH in CENC (PlayReady e Widevine), Smooth Streaming in PlayReady, HLS in Widevine o PlayReady.</span><span class="sxs-lookup"><span data-stu-id="8157f-156">Streaming protocol and DRM encryption combination, such as DASH under CENC (PlayReady and Widevine), smooth streaming under PlayReady, HLS under Widevine or PlayReady.</span></span>
* <span data-ttu-id="8157f-157">Gli URL di distribuzione della licenza predefiniti/incorporati per ciascuno dei DRM interessati.</span><span class="sxs-lookup"><span data-stu-id="8157f-157">The default/embedded license delivery URLs for each of the involved DRMs.</span></span>
* <span data-ttu-id="8157f-158">Presenza o meno di una stringa query per l'ID chiave (KID) di Widevine e Fairplay negli URL di acquisizione della licenza (LA_URL) nell'elenco di riproduzione DASH MPD o HLS.</span><span class="sxs-lookup"><span data-stu-id="8157f-158">Whether license acquisition URLs (LA_URLs) in DASH MPD or HLS playlist contain query string of key ID (KID) for Widevine and FairPlay, respectively.</span></span>

## <a name="scenarios-and-samples"></a><span data-ttu-id="8157f-159">Scenari ed esempi</span><span class="sxs-lookup"><span data-stu-id="8157f-159">Scenarios and samples</span></span>

<span data-ttu-id="8157f-160">In base alle spiegazioni fornite nella sezione precedente, sono cinque gli scenari ibridi in cui vengono rispettivamente usate le combinazioni di configurazioni con **Chiave simmetrica**-**Criteri di distribuzione dell'asset** (gli esempi citati nell'ultima colonna seguono la tabella):</span><span class="sxs-lookup"><span data-stu-id="8157f-160">Based on the explanations in the previous section, the following five hybrid scenarios use respective **Content key**-**Asset delivery policy** configuration combinations (the samples mentioned in the last column follow the table):</span></span>

|<span data-ttu-id="8157f-161">**Hosting e origine del contenuto**</span><span class="sxs-lookup"><span data-stu-id="8157f-161">**Content hosting & origin**</span></span>|<span data-ttu-id="8157f-162">**Crittografia DRM**</span><span class="sxs-lookup"><span data-stu-id="8157f-162">**DRM encryption**</span></span>|<span data-ttu-id="8157f-163">**Distribuzione di licenze DRM**</span><span class="sxs-lookup"><span data-stu-id="8157f-163">**DRM license delivery**</span></span>|<span data-ttu-id="8157f-164">**Configurare la chiave simmetrica**</span><span class="sxs-lookup"><span data-stu-id="8157f-164">**Configure content key**</span></span>|<span data-ttu-id="8157f-165">**Configurare i criteri di distribuzione dell'asset**</span><span class="sxs-lookup"><span data-stu-id="8157f-165">**Configure asset delivery policy**</span></span>|<span data-ttu-id="8157f-166">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="8157f-166">**Sample**</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="8157f-167">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-167">AMS</span></span>|<span data-ttu-id="8157f-168">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-168">AMS</span></span>|<span data-ttu-id="8157f-169">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-169">AMS</span></span>|<span data-ttu-id="8157f-170">Sì</span><span class="sxs-lookup"><span data-stu-id="8157f-170">Yes</span></span>|<span data-ttu-id="8157f-171">Sì</span><span class="sxs-lookup"><span data-stu-id="8157f-171">Yes</span></span>|<span data-ttu-id="8157f-172">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="8157f-172">Sample 1</span></span>|
|<span data-ttu-id="8157f-173">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-173">AMS</span></span>|<span data-ttu-id="8157f-174">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-174">AMS</span></span>|<span data-ttu-id="8157f-175">Terze parti</span><span class="sxs-lookup"><span data-stu-id="8157f-175">Third-party</span></span>|<span data-ttu-id="8157f-176">Sì</span><span class="sxs-lookup"><span data-stu-id="8157f-176">Yes</span></span>|<span data-ttu-id="8157f-177">Sì</span><span class="sxs-lookup"><span data-stu-id="8157f-177">Yes</span></span>|<span data-ttu-id="8157f-178">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="8157f-178">Sample 2</span></span>|
|<span data-ttu-id="8157f-179">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-179">AMS</span></span>|<span data-ttu-id="8157f-180">Terze parti</span><span class="sxs-lookup"><span data-stu-id="8157f-180">Third-party</span></span>|<span data-ttu-id="8157f-181">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-181">AMS</span></span>|<span data-ttu-id="8157f-182">Sì</span><span class="sxs-lookup"><span data-stu-id="8157f-182">Yes</span></span>|<span data-ttu-id="8157f-183">No</span><span class="sxs-lookup"><span data-stu-id="8157f-183">No</span></span>|<span data-ttu-id="8157f-184">Esempio 3</span><span class="sxs-lookup"><span data-stu-id="8157f-184">Sample 3</span></span>|
|<span data-ttu-id="8157f-185">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-185">AMS</span></span>|<span data-ttu-id="8157f-186">Terze parti</span><span class="sxs-lookup"><span data-stu-id="8157f-186">Third-party</span></span>|<span data-ttu-id="8157f-187">Esterno</span><span class="sxs-lookup"><span data-stu-id="8157f-187">Outside</span></span>|<span data-ttu-id="8157f-188">No</span><span class="sxs-lookup"><span data-stu-id="8157f-188">No</span></span>|<span data-ttu-id="8157f-189">No</span><span class="sxs-lookup"><span data-stu-id="8157f-189">No</span></span>|<span data-ttu-id="8157f-190">Esempio 4</span><span class="sxs-lookup"><span data-stu-id="8157f-190">Sample 4</span></span>|
|<span data-ttu-id="8157f-191">Terze parti</span><span class="sxs-lookup"><span data-stu-id="8157f-191">Third-party</span></span>|<span data-ttu-id="8157f-192">Terze parti</span><span class="sxs-lookup"><span data-stu-id="8157f-192">Third-party</span></span>|<span data-ttu-id="8157f-193">AMS</span><span class="sxs-lookup"><span data-stu-id="8157f-193">AMS</span></span>|<span data-ttu-id="8157f-194">Sì</span><span class="sxs-lookup"><span data-stu-id="8157f-194">Yes</span></span>|<span data-ttu-id="8157f-195">No</span><span class="sxs-lookup"><span data-stu-id="8157f-195">No</span></span>|    

<span data-ttu-id="8157f-196">Negli esempi, la protezione PlayReady funziona sia per DASH che per Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="8157f-196">In the samples, PlayReady protection works for both DASH and smooth streaming.</span></span> <span data-ttu-id="8157f-197">Gli URL del video mostrati di seguito sono URL Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="8157f-197">The video URLs below are smooth streaming URLs.</span></span> <span data-ttu-id="8157f-198">Per ottenere gli URL DASH corrispondenti, aggiungere semplicemente "(format=mpd-time-csf)".</span><span class="sxs-lookup"><span data-stu-id="8157f-198">To get the corresponding DASH URLs, just append "(format=mpd-time-csf)".</span></span> <span data-ttu-id="8157f-199">È possibile usare il [lettore multimediale di test di Azure](http://aka.ms/amtest) per effettuare il test nel browser.</span><span class="sxs-lookup"><span data-stu-id="8157f-199">You could use the [azure media test player](http://aka.ms/amtest) to test in a browser.</span></span> <span data-ttu-id="8157f-200">Consente di configurare il protocollo di streaming e specificare in quale tecnologia usarlo.</span><span class="sxs-lookup"><span data-stu-id="8157f-200">It allows you to configure which streaming protocol to use, under which tech.</span></span> <span data-ttu-id="8157f-201">IE11 e MS Edge in Windows 10 supportano PlayReady tramite EME.</span><span class="sxs-lookup"><span data-stu-id="8157f-201">IE11 and MS Edge on Windows 10 support PlayReady through EME.</span></span> <span data-ttu-id="8157f-202">Per altre informazioni, vedere i [dettagli sullo strumento di test](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span><span class="sxs-lookup"><span data-stu-id="8157f-202">For more information, see [details about the test tool](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span></span>

### <a name="sample-1"></a><span data-ttu-id="8157f-203">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="8157f-203">Sample 1</span></span>

* <span data-ttu-id="8157f-204">URL di origine (di base): https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="8157f-204">Source (base) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span></span> 
* <span data-ttu-id="8157f-205">LA_URL di PlayReady (DASH e smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="8157f-205">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 
* <span data-ttu-id="8157f-206">LA_URL di Widevine (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span><span class="sxs-lookup"><span data-stu-id="8157f-206">Widevine LA_URL (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span></span> 
* <span data-ttu-id="8157f-207">LA_URL di FairPlay (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span><span class="sxs-lookup"><span data-stu-id="8157f-207">FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span></span> 

### <a name="sample-2"></a><span data-ttu-id="8157f-208">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="8157f-208">Sample 2</span></span>

* <span data-ttu-id="8157f-209">URL di origine (di base): http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="8157f-209">Source (base) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span></span> 
* <span data-ttu-id="8157f-210">LA_URL di PlayReady (DASH e smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span><span class="sxs-lookup"><span data-stu-id="8157f-210">PlayReady LA_URL (DASH & smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span></span> 

### <a name="sample-3"></a><span data-ttu-id="8157f-211">Esempio 3</span><span class="sxs-lookup"><span data-stu-id="8157f-211">Sample 3</span></span>

* <span data-ttu-id="8157f-212">URL di origine: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="8157f-212">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="8157f-213">LA_URL di PlayReady (DASH e smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="8157f-213">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 

### <a name="sample-4"></a><span data-ttu-id="8157f-214">Esempio 4</span><span class="sxs-lookup"><span data-stu-id="8157f-214">Sample 4</span></span>

* <span data-ttu-id="8157f-215">URL di origine: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="8157f-215">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="8157f-216">LA_URL di PlayReady (DASH e smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span><span class="sxs-lookup"><span data-stu-id="8157f-216">PlayReady LA_URL (DASH & smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span></span> 

## <a name="summary"></a><span data-ttu-id="8157f-217">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="8157f-217">Summary</span></span>

<span data-ttu-id="8157f-218">In sintesi, i componenti DRM di Servizi multimediali di Azure sono flessibili ed è possibile usarli in uno scenario ibrido configurando correttamente la chiave simmetrica e i criteri di distribuzione della licenza, come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="8157f-218">In summary, Azure Media Services DRM components are flexible, you can use them in a hybrid scenario by properly configuring content key and asset delivery policy, as described in this topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8157f-219">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8157f-219">Next steps</span></span>
<span data-ttu-id="8157f-220">Visualizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="8157f-220">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8157f-221">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="8157f-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

