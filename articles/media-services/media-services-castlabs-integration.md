---
title: Uso di castLabs per distribuire licenze Widevine a Servizi multimediali di Azure | Microsoft Docs
description: Questo articolo illustra come usare Servizi multimediali di Azure per distribuire un flusso crittografato in modo dinamico da Servizi multimediali di Azure mediante DRM di PlayReady e Widevine. La licenza per PlayReady viene distribuita dal server licenze PlayReady di Servizi multimediali, mentre la licenza per Widevine viene distribuita dal server licenze castLabs.
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 5b69e804809f834e81221fb2787a997a52dbe286
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="using-castlabs-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="0b0b2-104">Uso di castLabs per distribuire licenze Widevine a Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="0b0b2-104">Using castLabs to deliver Widevine licenses to Azure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0b0b2-105">Axinom</span><span class="sxs-lookup"><span data-stu-id="0b0b2-105">Axinom</span></span>](media-services-axinom-integration.md)
> * [<span data-ttu-id="0b0b2-106">castLabs</span><span class="sxs-lookup"><span data-stu-id="0b0b2-106">castLabs</span></span>](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="0b0b2-107">Overview</span><span class="sxs-lookup"><span data-stu-id="0b0b2-107">Overview</span></span>
<span data-ttu-id="0b0b2-108">Questo articolo illustra come usare Servizi multimediali di Azure per distribuire un flusso crittografato in modo dinamico da Servizi multimediali di Azure mediante DRM di PlayReady e Widevine.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-108">This article describes how you can use Azure Media Services (AMS) to deliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="0b0b2-109">La licenza per PlayReady viene distribuita dal server licenze PlayReady di Servizi multimediali, mentre la licenza per Widevine viene distribuita dal server licenze **castLabs** .</span><span class="sxs-lookup"><span data-stu-id="0b0b2-109">The PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="0b0b2-110">Per la riproduzione di contenuti in streaming protetti da CENC (PlayReady e/o Widevine), è possibile usare [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="0b0b2-110">To playback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="0b0b2-111">Per informazioni dettagliate vedere la [documentazione dell’AMP](http://amp.azure.net/libs/amp/latest/docs/)</span><span class="sxs-lookup"><span data-stu-id="0b0b2-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="0b0b2-112">Il diagramma seguente illustra un'architettura di integrazione di alto livello tra castLabs e Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-112">The following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![integrazione](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="0b0b2-114">Configurazione di sistema tipica</span><span class="sxs-lookup"><span data-stu-id="0b0b2-114">Typical system set up</span></span>
* <span data-ttu-id="0b0b2-115">I contenuti multimediali vengono archiviati in Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="0b0b2-116">Gli ID delle chiavi simmetriche vengono archiviati sia in castLabs sia in Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="0b0b2-117">castLabs e Servizi multimediali di Azure dispongono entrambi di un sistema di autenticazione dei token integrato.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="0b0b2-118">I token di autenticazione vengono illustrati nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-118">The following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="0b0b2-119">Quando un client deve trasmettere un video in streaming, il contenuto viene crittografato dinamicamente con la **crittografia comune** e organizzato da Servizi multimediali di Azure in pacchetti dinamici creati con i protocolli Smooth Streaming e DASH.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-119">When a client requests to stream the video, the content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS to Smooth Streaming and DASH.</span></span> <span data-ttu-id="0b0b2-120">Viene inoltre fornita la crittografia dei flussi elementari M2TS PlayReady per il protocollo di streaming HLS.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="0b0b2-121">La licenza per PlayReady viene recuperata dal server licenze di Servizi multimediali di Azure, mentre la licenza per Widevine viene recuperata dal server licenze castLabs.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="0b0b2-122">Media Player decide automaticamente le licenze da recuperare in base alle caratteristiche della piattaforma client.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-122">Media Player automatically decides which license to fetch based on the client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="0b0b2-123">Generazione di token di autenticazione per ottenere una licenza</span><span class="sxs-lookup"><span data-stu-id="0b0b2-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="0b0b2-124">castLabs e Servizi multimediali di Azure supportano entrambi il formato di token JWT (JSON Web Token), necessario per autorizzare una licenza.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-124">Both castLabs and AMS support JWT (JSON Web Token) token format used to authorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="0b0b2-125">Token JWT in Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="0b0b2-125">JWT token in AMS</span></span>
<span data-ttu-id="0b0b2-126">La tabella seguente descrive il token JWT usato in Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-126">The following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="0b0b2-127">Issuer</span><span class="sxs-lookup"><span data-stu-id="0b0b2-127">Issuer</span></span> | <span data-ttu-id="0b0b2-128">Stringa dell'autorità di certificazione rilasciata dal servizio token di sicurezza scelto</span><span class="sxs-lookup"><span data-stu-id="0b0b2-128">Issuer string from the chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="0b0b2-129">Audience</span><span class="sxs-lookup"><span data-stu-id="0b0b2-129">Audience</span></span> |<span data-ttu-id="0b0b2-130">Stringa dei destinatari rilasciata dal servizio token di sicurezza usato</span><span class="sxs-lookup"><span data-stu-id="0b0b2-130">Audience string from the used STS</span></span> |
| <span data-ttu-id="0b0b2-131">Claims</span><span class="sxs-lookup"><span data-stu-id="0b0b2-131">Claims</span></span> |<span data-ttu-id="0b0b2-132">Set di attestazioni</span><span class="sxs-lookup"><span data-stu-id="0b0b2-132">A set of claims</span></span> |
| <span data-ttu-id="0b0b2-133">NotBefore</span><span class="sxs-lookup"><span data-stu-id="0b0b2-133">NotBefore</span></span> |<span data-ttu-id="0b0b2-134">Validità di inizio del token</span><span class="sxs-lookup"><span data-stu-id="0b0b2-134">Start validity of the token</span></span> |
| <span data-ttu-id="0b0b2-135">Expires</span><span class="sxs-lookup"><span data-stu-id="0b0b2-135">Expires</span></span> |<span data-ttu-id="0b0b2-136">Validità di fine del token</span><span class="sxs-lookup"><span data-stu-id="0b0b2-136">End validity of the token</span></span> |
| <span data-ttu-id="0b0b2-137">SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="0b0b2-137">SigningCredentials</span></span> |<span data-ttu-id="0b0b2-138">Chiave condivisa tra il server licenze PlayReady, il server licenze castLabs e il servizio token di sicurezza (STS); può essere una chiave simmetrica o asimmetrica.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-138">The key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="0b0b2-139">Token JWT in castLabs</span><span class="sxs-lookup"><span data-stu-id="0b0b2-139">JWT token in castLabs</span></span>
<span data-ttu-id="0b0b2-140">La tabella seguente descrive il token JWT usato in castLabs.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-140">The following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="0b0b2-141">Nome</span><span class="sxs-lookup"><span data-stu-id="0b0b2-141">Name</span></span> | <span data-ttu-id="0b0b2-142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0b0b2-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0b0b2-143">optData</span><span class="sxs-lookup"><span data-stu-id="0b0b2-143">optData</span></span> |<span data-ttu-id="0b0b2-144">Stringa JSON contenente informazioni relative all'utente.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="0b0b2-145">crt</span><span class="sxs-lookup"><span data-stu-id="0b0b2-145">crt</span></span> |<span data-ttu-id="0b0b2-146">Stringa JSON contenente informazioni sull'asset, sulla relativa licenza e sui diritti di riproduzione.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-146">A JSON string containing information about the asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="0b0b2-147">iat</span><span class="sxs-lookup"><span data-stu-id="0b0b2-147">iat</span></span> |<span data-ttu-id="0b0b2-148">Data e ora corrente nel periodo.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-148">The current datetime in epoch.</span></span> |
| <span data-ttu-id="0b0b2-149">jti</span><span class="sxs-lookup"><span data-stu-id="0b0b2-149">jti</span></span> |<span data-ttu-id="0b0b2-150">Identificatore univoco per il token (ogni token può essere usato una sola volta nel sistema castLabs).</span><span class="sxs-lookup"><span data-stu-id="0b0b2-150">A unique identifier about this token (every token can only be used once in the castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="0b0b2-151">Configurazione della soluzione di esempio</span><span class="sxs-lookup"><span data-stu-id="0b0b2-151">Sample solution set up</span></span>
<span data-ttu-id="0b0b2-152">La [soluzione di esempio](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) è costituita da due progetti:</span><span class="sxs-lookup"><span data-stu-id="0b0b2-152">The [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="0b0b2-153">Un'app console che consente di impostare le restrizioni DRM su un asset già acquisito, sia per PlayReady sia per Widevine.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-153">A console app that can be used to set DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="0b0b2-154">Un'applicazione Web incaricata della distribuzione dei token, che possono essere considerati come una versione molto semplificata di un servizio token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="0b0b2-155">Per usare l'applicazione console:</span><span class="sxs-lookup"><span data-stu-id="0b0b2-155">To use the console application:</span></span>

1. <span data-ttu-id="0b0b2-156">Modificare il file app.config per impostare le credenziali di Servizi multimediali di Azure, le credenziali di castLabs, la configurazione del servizio token di sicurezza e la chiave condivisa.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-156">Change the app.config to setup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="0b0b2-157">Caricare un asset in Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="0b0b2-158">Ottenere l'UUID dall'asset caricato e modificare la riga 32 nel file Program.cs:</span><span class="sxs-lookup"><span data-stu-id="0b0b2-158">Get the UUID from the uploaded Asset, and change Line 32 in the Program.cs file:</span></span>
   
      <span data-ttu-id="0b0b2-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="0b0b2-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="0b0b2-160">Usare un ID asset per assegnare un nome all'asset nel sistema castLabs (riga 44 nel file Program.cs).</span><span class="sxs-lookup"><span data-stu-id="0b0b2-160">Use an AssetId for naming the asset in the castLabs system (Line 44 in the Program.cs file).</span></span>
   
   <span data-ttu-id="0b0b2-161">È necessario impostare l'ID asset per **castLabs**: deve essere una stringa alfanumerica univoca.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-161">You must set AssetId for **castLabs**; it needs to be a unique alphanumeric string.</span></span>
5. <span data-ttu-id="0b0b2-162">Eseguire il programma.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-162">Run the program.</span></span>

<span data-ttu-id="0b0b2-163">Per usare l'applicazione Web (STS):</span><span class="sxs-lookup"><span data-stu-id="0b0b2-163">To use the Web Application (STS):</span></span>

1. <span data-ttu-id="0b0b2-164">Modificare il file web.config per impostare l'ID società di castlabs, la configurazione del servizio token di sicurezza e la chiave condivisa.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-164">Change the web.config to setup castlabs merchant ID, the STS configuration and the shared key.</span></span>
2. <span data-ttu-id="0b0b2-165">Eseguire la distribuzione nei siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-165">Deploy to Azure Websites.</span></span>
3. <span data-ttu-id="0b0b2-166">Passare al sito Web.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-166">Navigate to the website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="0b0b2-167">Riproduzione di un video</span><span class="sxs-lookup"><span data-stu-id="0b0b2-167">Playing back a video</span></span>
<span data-ttu-id="0b0b2-168">Per riprodurre un video crittografato con la crittografia comune (PlayReady e/o Widevine), è possibile usare [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="0b0b2-168">To playback a video encrypted with common encryption (PlayReady and/or Widevine), you can use the [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="0b0b2-169">Quando si esegue l'app console, vengono restituiti l'ID della chiave simmetrica e l'URL del manifesto.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-169">When running the console app, the Content Key ID and the Manifest URL are echoed.</span></span>

1. <span data-ttu-id="0b0b2-170">Aprire una nuova scheda e avviare il servizio token di sicurezza: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span><span class="sxs-lookup"><span data-stu-id="0b0b2-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="0b0b2-171">Accedere a [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="0b0b2-171">Go to [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="0b0b2-172">Incollare l'URL di streaming </span><span class="sxs-lookup"><span data-stu-id="0b0b2-172">Paste in the streaming URL.</span></span>
4. <span data-ttu-id="0b0b2-173">Scegliere la casella di controllo **Opzioni avanzate** .</span><span class="sxs-lookup"><span data-stu-id="0b0b2-173">Click the **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="0b0b2-174">Nell'elenco a discesa **Protezione** , selezionare PlayReady e/o Widevine.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-174">In the **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="0b0b2-175">Incollare il token ottenuto dal servizio token di sicurezza nella casella di testo Token.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-175">Paste the token that you got from your STS in the Token textbox.</span></span> 
   
   <span data-ttu-id="0b0b2-176">Quando si usa il server licenze castLabs, non è necessario aggiungere il prefisso "Bearer=" davanti al token.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-176">The castLab license server does not need the “Bearer=” prefix in front of the token.</span></span> <span data-ttu-id="0b0b2-177">Se presente, quindi, è necessario rimuoverlo prima di inviare il token.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-177">So please remove that before submitting the token.</span></span>
7. <span data-ttu-id="0b0b2-178">Aggiornare il lettore.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-178">Update the player.</span></span>
8. <span data-ttu-id="0b0b2-179">A questo punto, dovrebbe essere possibile riprodurre il video.</span><span class="sxs-lookup"><span data-stu-id="0b0b2-179">The video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="0b0b2-180">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="0b0b2-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0b0b2-181">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="0b0b2-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

