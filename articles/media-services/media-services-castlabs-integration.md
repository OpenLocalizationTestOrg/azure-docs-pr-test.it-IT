---
title: le licenze di servizi multimediali tooAzure aaaUsing castLabs toodeliver Widevine | Documenti Microsoft
description: In questo articolo viene descritto come usare Azure Media Services (AMS) toodeliver un flusso che viene crittografato in modo dinamico dal sistema AMS con PlayReady e Widevine DRMs. la licenza PlayReady Hello proviene dal server licenze PlayReady di servizi multimediali e viene recapitata licenze Widevine dal server licenze castLabs.
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
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="2e928-104">Utilizzando castLabs toodeliver Widevine licenze tooAzure servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="2e928-104">Using castLabs toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e928-105">Axinom</span><span class="sxs-lookup"><span data-stu-id="2e928-105">Axinom</span></span>](media-services-axinom-integration.md)
> * [<span data-ttu-id="2e928-106">castLabs</span><span class="sxs-lookup"><span data-stu-id="2e928-106">castLabs</span></span>](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="2e928-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2e928-107">Overview</span></span>
<span data-ttu-id="2e928-108">In questo articolo viene descritto come usare Azure Media Services (AMS) toodeliver un flusso che viene crittografato in modo dinamico dal sistema AMS con PlayReady e Widevine DRMs.</span><span class="sxs-lookup"><span data-stu-id="2e928-108">This article describes how you can use Azure Media Services (AMS) toodeliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="2e928-109">la licenza PlayReady Hello proviene dal server licenze PlayReady di servizi multimediali e licenze Widevine viene recapitata da **castLabs** server licenze.</span><span class="sxs-lookup"><span data-stu-id="2e928-109">hello PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="2e928-110">streaming di contenuto protetto tooplayback CENC (PlayReady e/o Widevine), è possibile usare [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="2e928-110">tooplayback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="2e928-111">Per informazioni dettagliate vedere la [documentazione dell’AMP](http://amp.azure.net/libs/amp/latest/docs/)</span><span class="sxs-lookup"><span data-stu-id="2e928-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="2e928-112">Hello seguente diagramma viene illustrata un'architettura di integrazione di servizi multimediali di Azure e castLabs ad alto livello.</span><span class="sxs-lookup"><span data-stu-id="2e928-112">hello following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![integrazione](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="2e928-114">Configurazione di sistema tipica</span><span class="sxs-lookup"><span data-stu-id="2e928-114">Typical system set up</span></span>
* <span data-ttu-id="2e928-115">I contenuti multimediali vengono archiviati in Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e928-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="2e928-116">Gli ID delle chiavi simmetriche vengono archiviati sia in castLabs sia in Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e928-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="2e928-117">castLabs e Servizi multimediali di Azure dispongono entrambi di un sistema di autenticazione dei token integrato.</span><span class="sxs-lookup"><span data-stu-id="2e928-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="2e928-118">Hello le sezioni seguenti illustrano i token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="2e928-118">hello following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="2e928-119">Quando un client richiede video hello toostream, il contenuto di hello è crittografato in modo dinamico con **crittografia comune** (CENC) e compresso in modo dinamico dal sistema AMS tooSmooth Streaming e trattino.</span><span class="sxs-lookup"><span data-stu-id="2e928-119">When a client requests toostream hello video, hello content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS tooSmooth Streaming and DASH.</span></span> <span data-ttu-id="2e928-120">Viene inoltre fornita la crittografia dei flussi elementari M2TS PlayReady per il protocollo di streaming HLS.</span><span class="sxs-lookup"><span data-stu-id="2e928-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="2e928-121">La licenza per PlayReady viene recuperata dal server licenze di Servizi multimediali di Azure, mentre la licenza per Widevine viene recuperata dal server licenze castLabs.</span><span class="sxs-lookup"><span data-stu-id="2e928-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="2e928-122">Media Player automaticamente decide quali toofetch di licenza in base alle funzionalità di piattaforma client hello.</span><span class="sxs-lookup"><span data-stu-id="2e928-122">Media Player automatically decides which license toofetch based on hello client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="2e928-123">Generazione di token di autenticazione per ottenere una licenza</span><span class="sxs-lookup"><span data-stu-id="2e928-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="2e928-124">CastLabs e AMS supportano entrambi JWT (JSON Web Token) formato di token utilizzato tooauthorize una licenza.</span><span class="sxs-lookup"><span data-stu-id="2e928-124">Both castLabs and AMS support JWT (JSON Web Token) token format used tooauthorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="2e928-125">Token JWT in Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="2e928-125">JWT token in AMS</span></span>
<span data-ttu-id="2e928-126">Hello nella tabella seguente descrive i token JWT in AMS.</span><span class="sxs-lookup"><span data-stu-id="2e928-126">hello following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="2e928-127">Issuer</span><span class="sxs-lookup"><span data-stu-id="2e928-127">Issuer</span></span> | <span data-ttu-id="2e928-128">Stringa dell'autorità di certificazione da hello scelto servizio Token (sicurezza)</span><span class="sxs-lookup"><span data-stu-id="2e928-128">Issuer string from hello chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="2e928-129">Audience</span><span class="sxs-lookup"><span data-stu-id="2e928-129">Audience</span></span> |<span data-ttu-id="2e928-130">Stringa di destinatari da hello utilizzata servizio token di sicurezza</span><span class="sxs-lookup"><span data-stu-id="2e928-130">Audience string from hello used STS</span></span> |
| <span data-ttu-id="2e928-131">Claims</span><span class="sxs-lookup"><span data-stu-id="2e928-131">Claims</span></span> |<span data-ttu-id="2e928-132">Set di attestazioni</span><span class="sxs-lookup"><span data-stu-id="2e928-132">A set of claims</span></span> |
| <span data-ttu-id="2e928-133">NotBefore</span><span class="sxs-lookup"><span data-stu-id="2e928-133">NotBefore</span></span> |<span data-ttu-id="2e928-134">Inizio validità del token hello</span><span class="sxs-lookup"><span data-stu-id="2e928-134">Start validity of hello token</span></span> |
| <span data-ttu-id="2e928-135">Expires</span><span class="sxs-lookup"><span data-stu-id="2e928-135">Expires</span></span> |<span data-ttu-id="2e928-136">Fine validità del token hello</span><span class="sxs-lookup"><span data-stu-id="2e928-136">End validity of hello token</span></span> |
| <span data-ttu-id="2e928-137">SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="2e928-137">SigningCredentials</span></span> |<span data-ttu-id="2e928-138">chiave Hello condiviso tra i Server licenze PlayReady, castLabs Server licenze e servizio token di sicurezza, potrebbe trattarsi di una chiave simmetrica o asimmetrica.</span><span class="sxs-lookup"><span data-stu-id="2e928-138">hello key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="2e928-139">Token JWT in castLabs</span><span class="sxs-lookup"><span data-stu-id="2e928-139">JWT token in castLabs</span></span>
<span data-ttu-id="2e928-140">Hello nella tabella seguente descrive i token JWT in castLabs.</span><span class="sxs-lookup"><span data-stu-id="2e928-140">hello following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="2e928-141">Nome</span><span class="sxs-lookup"><span data-stu-id="2e928-141">Name</span></span> | <span data-ttu-id="2e928-142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2e928-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2e928-143">optData</span><span class="sxs-lookup"><span data-stu-id="2e928-143">optData</span></span> |<span data-ttu-id="2e928-144">Stringa JSON contenente informazioni relative all'utente.</span><span class="sxs-lookup"><span data-stu-id="2e928-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="2e928-145">crt</span><span class="sxs-lookup"><span data-stu-id="2e928-145">crt</span></span> |<span data-ttu-id="2e928-146">Oggetto JSON stringa contenente informazioni sull'asset hello, i relativi diritti di licenza info e la riproduzione.</span><span class="sxs-lookup"><span data-stu-id="2e928-146">A JSON string containing information about hello asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="2e928-147">iat</span><span class="sxs-lookup"><span data-stu-id="2e928-147">iat</span></span> |<span data-ttu-id="2e928-148">Hello data/ora corrente nel periodo.</span><span class="sxs-lookup"><span data-stu-id="2e928-148">hello current datetime in epoch.</span></span> |
| <span data-ttu-id="2e928-149">jti</span><span class="sxs-lookup"><span data-stu-id="2e928-149">jti</span></span> |<span data-ttu-id="2e928-150">Identificatore univoco su questo token (ogni token sono utilizzabili solo una volta nel sistema castLabs hello).</span><span class="sxs-lookup"><span data-stu-id="2e928-150">A unique identifier about this token (every token can only be used once in hello castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="2e928-151">Configurazione della soluzione di esempio</span><span class="sxs-lookup"><span data-stu-id="2e928-151">Sample solution set up</span></span>
<span data-ttu-id="2e928-152">Hello [soluzione di esempio](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) è costituito da due progetti:</span><span class="sxs-lookup"><span data-stu-id="2e928-152">hello [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="2e928-153">Un'applicazione console che può essere presenti restrizioni DRM tooset utilizzata su una risorsa già acquisita, per PlayReady e Widevine.</span><span class="sxs-lookup"><span data-stu-id="2e928-153">A console app that can be used tooset DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="2e928-154">Un'applicazione Web incaricata della distribuzione dei token, che possono essere considerati come una versione molto semplificata di un servizio token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="2e928-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="2e928-155">applicazione console hello toouse:</span><span class="sxs-lookup"><span data-stu-id="2e928-155">toouse hello console application:</span></span>

1. <span data-ttu-id="2e928-156">Modificare le credenziali toosetup AMS di hello app. config, castLabs credenziali, configurazione di servizio token di sicurezza e una chiave condivisa.</span><span class="sxs-lookup"><span data-stu-id="2e928-156">Change hello app.config toosetup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="2e928-157">Caricare un asset in Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e928-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="2e928-158">Get hello UUID da hello caricato Asset e modificare 32 riga nel file Program.cs hello:</span><span class="sxs-lookup"><span data-stu-id="2e928-158">Get hello UUID from hello uploaded Asset, and change Line 32 in hello Program.cs file:</span></span>
   
      <span data-ttu-id="2e928-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="2e928-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="2e928-160">Usare un AssetId per la denominazione asset hello nel sistema castLabs hello (44 riga nel file Program.cs hello).</span><span class="sxs-lookup"><span data-stu-id="2e928-160">Use an AssetId for naming hello asset in hello castLabs system (Line 44 in hello Program.cs file).</span></span>
   
   <span data-ttu-id="2e928-161">È necessario impostare AssetId per **castLabs**; è necessario toobe una stringa alfanumerica univoca.</span><span class="sxs-lookup"><span data-stu-id="2e928-161">You must set AssetId for **castLabs**; it needs toobe a unique alphanumeric string.</span></span>
5. <span data-ttu-id="2e928-162">Eseguire il programma hello.</span><span class="sxs-lookup"><span data-stu-id="2e928-162">Run hello program.</span></span>

<span data-ttu-id="2e928-163">hello toouse applicazione Web (STS):</span><span class="sxs-lookup"><span data-stu-id="2e928-163">toouse hello Web Application (STS):</span></span>

1. <span data-ttu-id="2e928-164">Merchant castlabs di modifica hello Web. config toosetup ID, la configurazione di STS hello e chiave condivisa hello.</span><span class="sxs-lookup"><span data-stu-id="2e928-164">Change hello web.config toosetup castlabs merchant ID, hello STS configuration and hello shared key.</span></span>
2. <span data-ttu-id="2e928-165">Distribuire tooAzure siti Web.</span><span class="sxs-lookup"><span data-stu-id="2e928-165">Deploy tooAzure Websites.</span></span>
3. <span data-ttu-id="2e928-166">Passare sito Web toohello.</span><span class="sxs-lookup"><span data-stu-id="2e928-166">Navigate toohello website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="2e928-167">Riproduzione di un video</span><span class="sxs-lookup"><span data-stu-id="2e928-167">Playing back a video</span></span>
<span data-ttu-id="2e928-168">tooplayback un video crittografata con la crittografia comune (PlayReady e/o Widevine), è possibile usare hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="2e928-168">tooplayback a video encrypted with common encryption (PlayReady and/or Widevine), you can use hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="2e928-169">Quando si esegue l'applicazione console hello, vengono restituite hello ID chiave contenuto e hello manifesto URL.</span><span class="sxs-lookup"><span data-stu-id="2e928-169">When running hello console app, hello Content Key ID and hello Manifest URL are echoed.</span></span>

1. <span data-ttu-id="2e928-170">Aprire una nuova scheda e avviare il servizio token di sicurezza: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span><span class="sxs-lookup"><span data-stu-id="2e928-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="2e928-171">Andare troppo[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="2e928-171">Go too[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="2e928-172">Incollare in hello URL di streaming.</span><span class="sxs-lookup"><span data-stu-id="2e928-172">Paste in hello streaming URL.</span></span>
4. <span data-ttu-id="2e928-173">Fare clic su hello **opzioni avanzate** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="2e928-173">Click hello **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="2e928-174">In hello **protezione** elenco a discesa selezionare PlayReady e/o Widevine.</span><span class="sxs-lookup"><span data-stu-id="2e928-174">In hello **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="2e928-175">Incollare il token hello recuperato dal servizio token di sicurezza nella casella di testo hello Token.</span><span class="sxs-lookup"><span data-stu-id="2e928-175">Paste hello token that you got from your STS in hello Token textbox.</span></span> 
   
   <span data-ttu-id="2e928-176">server licenze di Hello castLab non è necessario hello "portatore =" prefisso token hello.</span><span class="sxs-lookup"><span data-stu-id="2e928-176">hello castLab license server does not need hello “Bearer=” prefix in front of hello token.</span></span> <span data-ttu-id="2e928-177">Pertanto, rimuovere prima di inviare il token hello.</span><span class="sxs-lookup"><span data-stu-id="2e928-177">So please remove that before submitting hello token.</span></span>
7. <span data-ttu-id="2e928-178">Aggiornare Windows Media player hello.</span><span class="sxs-lookup"><span data-stu-id="2e928-178">Update hello player.</span></span>
8. <span data-ttu-id="2e928-179">Hello video deve essere in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2e928-179">hello video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="2e928-180">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="2e928-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2e928-181">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="2e928-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

