---
title: Configurazione dei criteri di protezione del contenuto tramite il portale di Azure | Microsoft Docs
description: Questo articolo illustra come usare il portale di Azure per configurare i criteri di protezione del contenuto. Descrive anche come abilitare la crittografia dinamica per gli asset.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 67b3fa9936daebeafb7e87fe3a7b0c7e0105b3b3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-content-protection-policies-using-the-azure-portal"></a><span data-ttu-id="31bd3-104">Configurazione dei criteri di protezione del contenuto tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="31bd3-104">Configuring content protection policies using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="31bd3-105">Per completare l'esercitazione, è necessario un account Azure.</span><span class="sxs-lookup"><span data-stu-id="31bd3-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="31bd3-106">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="31bd3-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="31bd3-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="31bd3-107">Overview</span></span>
<span data-ttu-id="31bd3-108">Servizi multimediali di Microsoft Azure (AMS) consente di proteggere i file multimediali dal momento in cui escono dal computer fino alle fasi di archiviazione, elaborazione e recapito.</span><span class="sxs-lookup"><span data-stu-id="31bd3-108">Microsoft Azure Media Services (AMS) enables you to secure your media from the time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="31bd3-109">Servizi multimediali consente di distribuire contenuti crittografati dinamicamente con AES (Advanced Encryption Standard) mediante chiavi di crittografia a 128 bit, con la crittografia comune (CENC) mediante PlayReady e/o la soluzione DRM Widevine e Apple FairPlay.</span><span class="sxs-lookup"><span data-stu-id="31bd3-109">Media Services allows you to deliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="31bd3-110">AMS offre un servizio per la distribuzione di licenze DRM e chiavi non crittografate AES ai client autorizzati.</span><span class="sxs-lookup"><span data-stu-id="31bd3-110">AMS provides a service for delivering DRM licenses and AES clear keys to authorized clients.</span></span> <span data-ttu-id="31bd3-111">Il portale di Azure consente di creare un **criterio di autorizzazione per chiavi e licenze** per tutti i tipi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="31bd3-111">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="31bd3-112">Questo articolo illustra come configurare i criteri di protezione del contenuto con il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="31bd3-112">This article demonstrates how to configure content protection policies with the Azure portal.</span></span> <span data-ttu-id="31bd3-113">Descrive anche come applicare la crittografia dinamica agli asset.</span><span class="sxs-lookup"><span data-stu-id="31bd3-113">The article also shows how to apply dynamic encryption to your assets.</span></span>


> [!NOTE]
> <span data-ttu-id="31bd3-114">Se è stato usato portale di Azure classico per creare criteri di protezione, i criteri potrebbero non essere visualizzati nel [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="31bd3-114">If you used the Azure classic portal to create protection policies, the policies may not appear in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="31bd3-115">Questi criteri sono tuttavia ancora disponibili.</span><span class="sxs-lookup"><span data-stu-id="31bd3-115">However, all the old polices still exist.</span></span> <span data-ttu-id="31bd3-116">È possibile esaminarli mediante Azure Media Services .NET SDK o lo [strumento di esplorazione di Servizi multimediali di Azure](https://github.com/Azure/Azure-Media-Services-Explorer/releases). Per visualizzare i criteri, fare clic con il pulsante destro del mouse sull'asset, scegliere Display information (Visualizza informazioni) (F4), fare clic sulla scheda Content keys (Chiavi simmetriche), quindi sulla chiave.</span><span class="sxs-lookup"><span data-stu-id="31bd3-116">You can examine them using the Azure Media Services .NET SDK or the [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (to see the policies, right-click on the asset -> Display information (F4)->click on Content keys tab-> click on the key).</span></span> 
> 
> <span data-ttu-id="31bd3-117">Se si vuole crittografare l'asset con i nuovi criteri, configurarli con il portale di Azure, fare clic su Salva e riapplicare la crittografia dinamica.</span><span class="sxs-lookup"><span data-stu-id="31bd3-117">If you want to encrypt your asset using new policies, configure them with the Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="31bd3-118">Avviare la configurazione della protezione del contenuto</span><span class="sxs-lookup"><span data-stu-id="31bd3-118">Start configuring content protection</span></span>
<span data-ttu-id="31bd3-119">Per usare il portale per avviare la configurazione della protezione del contenuto per l'intero account AMS, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="31bd3-119">To use the portal to start configuring content protection, global to your AMS account, do the following:</span></span>

1. <span data-ttu-id="31bd3-120">Nel [portale di Azure ](https://portal.azure.com/) selezionare l'account Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="31bd3-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="31bd3-121">Selezionare **Impostazioni** > **Protezione del contenuto**.</span><span class="sxs-lookup"><span data-stu-id="31bd3-121">Select **Settings** > **Content protection**.</span></span>

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="31bd3-123">criterio di autorizzazione per chiavi e licenze</span><span class="sxs-lookup"><span data-stu-id="31bd3-123">Key/license authorization policy</span></span>
<span data-ttu-id="31bd3-124">AMS supporta più modalità di autenticazione degli utenti che eseguono richieste di chiavi o licenze.</span><span class="sxs-lookup"><span data-stu-id="31bd3-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="31bd3-125">I criteri di autorizzazione delle chiavi simmetriche devono essere configurati dall'utente e soddisfatti dal client perché la chiave o la licenza possa essere distribuita al client.</span><span class="sxs-lookup"><span data-stu-id="31bd3-125">The content key authorization policy must be configured by you and met by your client in order for the key/license to be delived to the client.</span></span> <span data-ttu-id="31bd3-126">I criteri di autorizzazione delle chiavi simmetriche possono avere una o più restrizioni di tipo **Open** o **Token**.</span><span class="sxs-lookup"><span data-stu-id="31bd3-126">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="31bd3-127">Il portale di Azure consente di creare un **criterio di autorizzazione per chiavi e licenze** per tutti i tipi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="31bd3-127">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="31bd3-128">Apri</span><span class="sxs-lookup"><span data-stu-id="31bd3-128">Open</span></span>
<span data-ttu-id="31bd3-129">Limitazione aperta indica che il sistema distribuirà la chiave a chiunque ne faccia richiesta.</span><span class="sxs-lookup"><span data-stu-id="31bd3-129">Open restriction means that the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="31bd3-130">Questo tipo di limitazione può risultare utile ai fini dei test.</span><span class="sxs-lookup"><span data-stu-id="31bd3-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="31bd3-131">token</span><span class="sxs-lookup"><span data-stu-id="31bd3-131">Token</span></span>
<span data-ttu-id="31bd3-132">I criteri con restrizione Token devono essere accompagnati da un token rilasciato da un servizio STS (Secure Token Service, servizio token di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="31bd3-132">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="31bd3-133">Servizi multimediali supporta i token nei formati Simple Web Tokens (SWT) e JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="31bd3-133">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="31bd3-134">Servizi multimediali non fornisce servizi token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="31bd3-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="31bd3-135">Per il rilascio di token è possibile creare un servizio token di sicurezza personalizzato oppure usare il Servizio di controllo di accesso di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="31bd3-135">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="31bd3-136">Il servizio token di sicurezza deve essere configurato in modo da creare un token firmato con la chiave specificata e rilasciare le attestazioni specificate nella configurazione della restrizione token.</span><span class="sxs-lookup"><span data-stu-id="31bd3-136">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration.</span></span> <span data-ttu-id="31bd3-137">Il servizio di distribuzione di chiavi di Servizi multimediali restituirà al client la chiave o la licenza richiesta se il token è valido e le attestazioni del token corrispondono a quelle configurate per la chiave o la licenza.</span><span class="sxs-lookup"><span data-stu-id="31bd3-137">The Media Services key delivery service will return the requested key (or license) to the client if the token is valid and the claims in the token match those configured for the key (or license).</span></span>

<span data-ttu-id="31bd3-138">Quando si configurano i criteri di restrizione token, è necessario specificare i parametri primary verification key, issuer e audience.</span><span class="sxs-lookup"><span data-stu-id="31bd3-138">When configuring the token restricted policy, you must specify the primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="31bd3-139">Il parametro primary verification key include la chiave usata per firmare il token. Il parametro issuer è il servizio token di sicurezza che emette il token.</span><span class="sxs-lookup"><span data-stu-id="31bd3-139">The primary verification key contains the key that the token was signed with, issuer is the secure token service that issues the token.</span></span> <span data-ttu-id="31bd3-140">Il parametro audience (talvolta denominato scope) descrive l'ambito del token o la risorsa a cui il token autorizza l'accesso.</span><span class="sxs-lookup"><span data-stu-id="31bd3-140">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="31bd3-141">Il servizio di distribuzione delle chiavi di Servizi multimediali verifica che i valori nel token corrispondano ai valori nel modello.</span><span class="sxs-lookup"><span data-stu-id="31bd3-141">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span>

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="31bd3-143">Modello dei diritti PlayReady</span><span class="sxs-lookup"><span data-stu-id="31bd3-143">PlayReady rights template</span></span>
<span data-ttu-id="31bd3-144">Per informazioni dettagliate sul modello dei diritti PlayReady, vedere [Panoramica del modello di licenza PlayReady di Servizi multimediali](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="31bd3-144">For detailed information about the PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="31bd3-145">Non persistente</span><span class="sxs-lookup"><span data-stu-id="31bd3-145">Non persistent</span></span>
<span data-ttu-id="31bd3-146">Se viene configurata come non persistente, la licenza verrà conservata in memoria solo mentre il lettore la usa.</span><span class="sxs-lookup"><span data-stu-id="31bd3-146">If you configure license as non-persistent, it is only held in memory while the player is using the license.</span></span>  

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="31bd3-148">Persistente</span><span class="sxs-lookup"><span data-stu-id="31bd3-148">Persistent</span></span>
<span data-ttu-id="31bd3-149">Se si configura la licenza come persistente, questa verrà salvata nell'archivio persistente del client.</span><span class="sxs-lookup"><span data-stu-id="31bd3-149">If you configure the license  as persistent, it is saved in persistent storage on the client.</span></span>

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="31bd3-151">Modello dei diritti Widevine</span><span class="sxs-lookup"><span data-stu-id="31bd3-151">Widevine rights template</span></span>
<span data-ttu-id="31bd3-152">Per informazioni dettagliate sul modello dei diritti Widevine, vedere [Panoramica del modello di licenza Widevine](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="31bd3-152">For detailed information about the Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="31bd3-153">Basic</span><span class="sxs-lookup"><span data-stu-id="31bd3-153">Basic</span></span>
<span data-ttu-id="31bd3-154">Se si seleziona **Basic**, il modello verrà creato con tutti i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="31bd3-154">When you select **Basic**, the template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="31bd3-155">Avanzate</span><span class="sxs-lookup"><span data-stu-id="31bd3-155">Advanced</span></span>
<span data-ttu-id="31bd3-156">Per informazioni dettagliate sull'opzione avanzata delle configurazioni Widevine, vedere [questo](media-services-widevine-license-template-overview.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="31bd3-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="31bd3-158">Configurazione di FairPlay</span><span class="sxs-lookup"><span data-stu-id="31bd3-158">FairPlay configuration</span></span>
<span data-ttu-id="31bd3-159">Per abilitare la crittografia FairPlay, è necessario indicare il certificato dell'app e la chiave privata dell'applicazione (ASK) tramite l'opzione di configurazione FairPlay.</span><span class="sxs-lookup"><span data-stu-id="31bd3-159">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option.</span></span> <span data-ttu-id="31bd3-160">Per informazioni dettagliate sulla configurazione e i requisiti di FairPlay, vedere [questo](media-services-protect-hls-with-fairplay.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="31bd3-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-to-your-asset"></a><span data-ttu-id="31bd3-162">Applicare la crittografia dinamica agli asset</span><span class="sxs-lookup"><span data-stu-id="31bd3-162">Apply dynamic encryption to your asset</span></span>
<span data-ttu-id="31bd3-163">Per sfruttare i vantaggi della crittografia dinamica, è necessario codificare il file di origine in un set di file MP4 a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="31bd3-163">To take advantage of dynamic encryption, you need to encode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-to-encrypt"></a><span data-ttu-id="31bd3-164">Selezionare un asset da crittografare</span><span class="sxs-lookup"><span data-stu-id="31bd3-164">Select an asset that you want to encrypt</span></span>
<span data-ttu-id="31bd3-165">Per visualizzare tutti gli asset, selezionare **Impostazioni** > **Asset**.</span><span class="sxs-lookup"><span data-stu-id="31bd3-165">To see all your assets, select **Settings** > **Assets**.</span></span>

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="31bd3-167">Crittografare con AES o DRM</span><span class="sxs-lookup"><span data-stu-id="31bd3-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="31bd3-168">Quando si seleziona **Crittografa** per un asset, sono disponibili due opzioni: **AES** o **DRM**.</span><span class="sxs-lookup"><span data-stu-id="31bd3-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="31bd3-169">AES</span><span class="sxs-lookup"><span data-stu-id="31bd3-169">AES</span></span>
<span data-ttu-id="31bd3-170">La crittografia con chiave non crittografata AES sarà abilitata su tutti i protocolli di streaming: Smooth Streaming, HLS e MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="31bd3-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="31bd3-172">DRM</span><span class="sxs-lookup"><span data-stu-id="31bd3-172">DRM</span></span>
<span data-ttu-id="31bd3-173">Nella scheda DRM sono disponibili diverse opzioni per i criteri di protezione del contenuto (che è necessario aver configurato a questo punto) e un set di protocolli di streaming.</span><span class="sxs-lookup"><span data-stu-id="31bd3-173">When you select the DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="31bd3-174">**PlayReady e Widevine con MPEG-DASH** : il flusso MPEG-DASH verrà crittografato dinamicamente con le soluzioni DRM PlayReady e Widevine.</span><span class="sxs-lookup"><span data-stu-id="31bd3-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="31bd3-175">**PlayReady e Widevine con MPEG-DASH + FairPlay con HLS** : il flusso MPEG-DASH verrà crittografato dinamicamente con le soluzioni DRM PlayReady e Widevine.</span><span class="sxs-lookup"><span data-stu-id="31bd3-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="31bd3-176">Verranno anche crittografati i flussi HLS con FairPlay.</span><span class="sxs-lookup"><span data-stu-id="31bd3-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="31bd3-177">**PlayReady solo con Smooth Streaming, HLS e MPEG-DASH** : i flussi Smooth Streaming, HLS e MPEG-DASH verranno crittografati dinamicamente con la soluzione DRM PlayReady.</span><span class="sxs-lookup"><span data-stu-id="31bd3-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="31bd3-178">**Solo Widevine con MPEG-DASH** : il flusso MPEG-DASH verrà crittografato dinamicamente con la soluzione DRM Widevine.</span><span class="sxs-lookup"><span data-stu-id="31bd3-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="31bd3-179">**Solo FairPlay con HLS** : il flusso HLS verrà crittografato dinamicamente con FairPlay.</span><span class="sxs-lookup"><span data-stu-id="31bd3-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="31bd3-180">Per abilitare la crittografia FairPlay, è necessario indicare il certificato dell'app e la chiave privata dell'applicazione (ASK) tramite l'opzione di configurazione FairPlay del pannello delle impostazioni di Protezione del contenuto.</span><span class="sxs-lookup"><span data-stu-id="31bd3-180">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option of the Content Protection settings blade.</span></span>

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="31bd3-182">Dopo aver selezionato la crittografia, fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="31bd3-182">Once you make the encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="31bd3-183">Se si prevede di eseguire un flusso HLS crittografato con AES in Safari, vedere [questo blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="31bd3-183">If you are planning to play an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31bd3-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31bd3-184">Next steps</span></span>
<span data-ttu-id="31bd3-185">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="31bd3-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="31bd3-186">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="31bd3-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

