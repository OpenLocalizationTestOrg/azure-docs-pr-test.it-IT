---
title: criteri di protezione del contenuto aaaConfiguring usando hello portale di Azure | Documenti Microsoft
description: In questo articolo viene illustrato come toouse hello tooconfigure portale Azure i criteri di protezione del contenuto. Hello articolo inoltre illustrato come tooenable crittografia dinamica per le risorse.
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
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a><span data-ttu-id="86998-104">Configurazione dei criteri di protezione del contenuto tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="86998-104">Configuring content protection policies using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="86998-105">toocomplete questa esercitazione, è necessario un account di Azure.</span><span class="sxs-lookup"><span data-stu-id="86998-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="86998-106">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86998-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="86998-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="86998-107">Overview</span></span>
<span data-ttu-id="86998-108">Microsoft Azure Media Services (AMS) consente di toosecure gli elementi multimediali dal tempo hello che lascia computer tramite l'archiviazione, elaborazione e il recapito.</span><span class="sxs-lookup"><span data-stu-id="86998-108">Microsoft Azure Media Services (AMS) enables you toosecure your media from hello time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="86998-109">Servizi multimediali consente toodeliver il contenuto è crittografato in modo dinamico con Advanced Encryption Standard (AES) (utilizzando le chiavi di crittografia a 128 bit), common encryption (CENC) con PlayReady e/o DRM Widevine e FairPlay di Apple.</span><span class="sxs-lookup"><span data-stu-id="86998-109">Media Services allows you toodeliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="86998-110">AMS fornisce un servizio per la distribuzione di licenze DRM e i client tooauthorized chiavi non crittografata AES.</span><span class="sxs-lookup"><span data-stu-id="86998-110">AMS provides a service for delivering DRM licenses and AES clear keys tooauthorized clients.</span></span> <span data-ttu-id="86998-111">Hello portale di Azure consente toocreate uno **criteri di autorizzazione chiave licenza** per tutti i tipi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="86998-111">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="86998-112">In questo articolo viene illustrato come tooconfigure contenuto criteri di protezione con hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="86998-112">This article demonstrates how tooconfigure content protection policies with hello Azure portal.</span></span> <span data-ttu-id="86998-113">Hello articolo inoltre illustrato come asset di tooyour tooapply crittografia dinamica.</span><span class="sxs-lookup"><span data-stu-id="86998-113">hello article also shows how tooapply dynamic encryption tooyour assets.</span></span>


> [!NOTE]
> <span data-ttu-id="86998-114">Se si usa criteri di protezione di Azure toocreate portale classico di hello, criteri hello potrebbero emergere hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="86998-114">If you used hello Azure classic portal toocreate protection policies, hello policies may not appear in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="86998-115">Tuttavia, tutti hello precedente criteri ancora esiste.</span><span class="sxs-lookup"><span data-stu-id="86998-115">However, all hello old polices still exist.</span></span> <span data-ttu-id="86998-116">È possibile esaminarli utilizzando hello Azure Media Services .NET SDK o hello [Esplora servizi di supporto di Azure](https://github.com/Azure/Azure-Media-Services-Explorer/releases) strumento (criteri hello toosee, pulsante destro del mouse su asset hello -> visualizzazione di informazioni (F4) -> fare clic su chiavi simmetriche -> scheda Fare clic sulla chiave hello).</span><span class="sxs-lookup"><span data-stu-id="86998-116">You can examine them using hello Azure Media Services .NET SDK or hello [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (toosee hello policies, right-click on hello asset -> Display information (F4)->click on Content keys tab-> click on hello key).</span></span> 
> 
> <span data-ttu-id="86998-117">Se si desidera tooencrypt all'asset usando i nuovi criteri, configurarli con hello portale di Azure, fare clic su Salva e riapplicare la crittografia dinamica.</span><span class="sxs-lookup"><span data-stu-id="86998-117">If you want tooencrypt your asset using new policies, configure them with hello Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="86998-118">Avviare la configurazione della protezione del contenuto</span><span class="sxs-lookup"><span data-stu-id="86998-118">Start configuring content protection</span></span>
<span data-ttu-id="86998-119">portale toostart hello toouse la configurazione di protezione del contenuto, account globali tooyour AMS, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="86998-119">toouse hello portal toostart configuring content protection, global tooyour AMS account, do hello following:</span></span>

1. <span data-ttu-id="86998-120">In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="86998-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="86998-121">Selezionare **Impostazioni** > **Protezione del contenuto**.</span><span class="sxs-lookup"><span data-stu-id="86998-121">Select **Settings** > **Content protection**.</span></span>

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="86998-123">criterio di autorizzazione per chiavi e licenze</span><span class="sxs-lookup"><span data-stu-id="86998-123">Key/license authorization policy</span></span>
<span data-ttu-id="86998-124">AMS supporta più modalità di autenticazione degli utenti che eseguono richieste di chiavi o licenze.</span><span class="sxs-lookup"><span data-stu-id="86998-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="86998-125">criteri di autorizzazione chiave del contenuto Hello devono essere configurato dall'utente e soddisfatti dal client affinché hello chiave licenza toobe toohello delived client.</span><span class="sxs-lookup"><span data-stu-id="86998-125">hello content key authorization policy must be configured by you and met by your client in order for hello key/license toobe delived toohello client.</span></span> <span data-ttu-id="86998-126">Hello criteri di autorizzazione chiave contenuto potrebbero avere una o più restrizioni di autorizzazione: **aprire** o **token** restrizione.</span><span class="sxs-lookup"><span data-stu-id="86998-126">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="86998-127">Hello portale di Azure consente toocreate uno **criteri di autorizzazione chiave licenza** per tutti i tipi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="86998-127">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="86998-128">Apri</span><span class="sxs-lookup"><span data-stu-id="86998-128">Open</span></span>
<span data-ttu-id="86998-129">Restrizione Open significa che il sistema di hello distribuirà tooanyone di chiave hello che effettua una richiesta di chiave.</span><span class="sxs-lookup"><span data-stu-id="86998-129">Open restriction means that hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="86998-130">Questo tipo di limitazione può risultare utile ai fini dei test.</span><span class="sxs-lookup"><span data-stu-id="86998-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="86998-131">token</span><span class="sxs-lookup"><span data-stu-id="86998-131">Token</span></span>
<span data-ttu-id="86998-132">criteri con restrizione token Hello devono essere accompagnato da un token rilasciato da un servizio (token di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="86998-132">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="86998-133">Servizi multimediali supporta i token in formato JSON Web Token (JWT) e i token SWT (Simple Web token) hello.</span><span class="sxs-lookup"><span data-stu-id="86998-133">Media Services supports tokens in hello Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="86998-134">Servizi multimediali non fornisce servizi token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="86998-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="86998-135">È possibile creare un servizio token di sicurezza personalizzato o utilizzare i token tooissue ACS di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="86998-135">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="86998-136">Hello servizio token di sicurezza deve essere configurato toocreate un token firmato con hello specificato chiave e rilasciare le attestazioni specificate nella configurazione della restrizione token hello.</span><span class="sxs-lookup"><span data-stu-id="86998-136">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration.</span></span> <span data-ttu-id="86998-137">attestazioni di servizi multimediali Hello servizio di distribuzione chiavi restituirà hello richiesto hello e chiave (o licenza) client toohello se hello token è valido in hello token corrispondono a quelle configurate per la chiave di hello (o licenza).</span><span class="sxs-lookup"><span data-stu-id="86998-137">hello Media Services key delivery service will return hello requested key (or license) toohello client if hello token is valid and hello claims in hello token match those configured for hello key (or license).</span></span>

<span data-ttu-id="86998-138">Quando si configurano i criteri con restrizione token hello, è necessario specificare la chiave di verifica primaria hello, autorità emittente e parametri pubblico.</span><span class="sxs-lookup"><span data-stu-id="86998-138">When configuring hello token restricted policy, you must specify hello primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="86998-139">chiave di verifica primaria Hello contiene hello chiave che hello token è stato firmato con, autorità emittente è hello servizio token di sicurezza che rilascia token hello.</span><span class="sxs-lookup"><span data-stu-id="86998-139">hello primary verification key contains hello key that hello token was signed with, issuer is hello secure token service that issues hello token.</span></span> <span data-ttu-id="86998-140">destinatari Hello (talvolta denominato ambito) descrive finalità hello del token hello o hello risorse hello token autorizza l'accesso.</span><span class="sxs-lookup"><span data-stu-id="86998-140">hello audience (sometimes called scope) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="86998-141">Hello servizio di distribuzione delle chiavi di servizi multimediali verifica che i valori nel token hello corrispondano valori hello hello modello.</span><span class="sxs-lookup"><span data-stu-id="86998-141">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span>

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="86998-143">Modello dei diritti PlayReady</span><span class="sxs-lookup"><span data-stu-id="86998-143">PlayReady rights template</span></span>
<span data-ttu-id="86998-144">Per informazioni dettagliate sul modello di diritti di hello PlayReady, vedere [Panoramica del modello di licenza PlayReady servizi multimediali](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="86998-144">For detailed information about hello PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="86998-145">Non persistente</span><span class="sxs-lookup"><span data-stu-id="86998-145">Non persistent</span></span>
<span data-ttu-id="86998-146">Se si configura una licenza come non persistenti, è solo conservato in memoria mentre player hello utilizza licenza hello.</span><span class="sxs-lookup"><span data-stu-id="86998-146">If you configure license as non-persistent, it is only held in memory while hello player is using hello license.</span></span>  

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="86998-148">Persistente</span><span class="sxs-lookup"><span data-stu-id="86998-148">Persistent</span></span>
<span data-ttu-id="86998-149">Se si configura la licenza hello come permanente, esso viene salvato nell'archivio permanente in client hello.</span><span class="sxs-lookup"><span data-stu-id="86998-149">If you configure hello license  as persistent, it is saved in persistent storage on hello client.</span></span>

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="86998-151">Modello dei diritti Widevine</span><span class="sxs-lookup"><span data-stu-id="86998-151">Widevine rights template</span></span>
<span data-ttu-id="86998-152">Per informazioni dettagliate sul modello di hello Widevine diritti, vedere [Cenni preliminari sui modelli di licenza Widevine](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="86998-152">For detailed information about hello Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="86998-153">Basic</span><span class="sxs-lookup"><span data-stu-id="86998-153">Basic</span></span>
<span data-ttu-id="86998-154">Quando si seleziona **base**, hello modello verrà creato con tutti i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="86998-154">When you select **Basic**, hello template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="86998-155">Avanzate</span><span class="sxs-lookup"><span data-stu-id="86998-155">Advanced</span></span>
<span data-ttu-id="86998-156">Per informazioni dettagliate sull'opzione avanzata delle configurazioni Widevine, vedere [questo](media-services-widevine-license-template-overview.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="86998-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="86998-158">Configurazione di FairPlay</span><span class="sxs-lookup"><span data-stu-id="86998-158">FairPlay configuration</span></span>
<span data-ttu-id="86998-159">crittografia FairPlay tooenable, è necessario tooprovide hello App certificato e chiave privata dell'applicazione (chiedere) tramite l'opzione di configurazione FairPlay hello.</span><span class="sxs-lookup"><span data-stu-id="86998-159">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option.</span></span> <span data-ttu-id="86998-160">Per informazioni dettagliate sulla configurazione e i requisiti di FairPlay, vedere [questo](media-services-protect-hls-with-fairplay.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="86998-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a><span data-ttu-id="86998-162">Applicare asset tooyour crittografia dinamica</span><span class="sxs-lookup"><span data-stu-id="86998-162">Apply dynamic encryption tooyour asset</span></span>
<span data-ttu-id="86998-163">Il vantaggio di tootake di crittografia dinamica, è necessario tooencode il file di origine in un set di file MP4 a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="86998-163">tootake advantage of dynamic encryption, you need tooencode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-tooencrypt"></a><span data-ttu-id="86998-164">Selezionare una risorsa che si desidera tooencrypt</span><span class="sxs-lookup"><span data-stu-id="86998-164">Select an asset that you want tooencrypt</span></span>
<span data-ttu-id="86998-165">Selezionare tutte le attività, toosee **impostazioni** > **asset**.</span><span class="sxs-lookup"><span data-stu-id="86998-165">toosee all your assets, select **Settings** > **Assets**.</span></span>

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="86998-167">Crittografare con AES o DRM</span><span class="sxs-lookup"><span data-stu-id="86998-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="86998-168">Quando si seleziona **Crittografa** per un asset, sono disponibili due opzioni: **AES** o **DRM**.</span><span class="sxs-lookup"><span data-stu-id="86998-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="86998-169">AES</span><span class="sxs-lookup"><span data-stu-id="86998-169">AES</span></span>
<span data-ttu-id="86998-170">La crittografia con chiave non crittografata AES sarà abilitata su tutti i protocolli di streaming: Smooth Streaming, HLS e MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="86998-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="86998-172">DRM</span><span class="sxs-lookup"><span data-stu-id="86998-172">DRM</span></span>
<span data-ttu-id="86998-173">Quando si seleziona una scheda DRM hello, viene visualizzata con diverse opzioni di criteri di protezione del contenuto (che è necessario aver configurato a questo punto) + un set di protocolli di flusso.</span><span class="sxs-lookup"><span data-stu-id="86998-173">When you select hello DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="86998-174">**PlayReady e Widevine con MPEG-DASH** : il flusso MPEG-DASH verrà crittografato dinamicamente con le soluzioni DRM PlayReady e Widevine.</span><span class="sxs-lookup"><span data-stu-id="86998-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="86998-175">**PlayReady e Widevine con MPEG-DASH + FairPlay con HLS** : il flusso MPEG-DASH verrà crittografato dinamicamente con le soluzioni DRM PlayReady e Widevine.</span><span class="sxs-lookup"><span data-stu-id="86998-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="86998-176">Verranno anche crittografati i flussi HLS con FairPlay.</span><span class="sxs-lookup"><span data-stu-id="86998-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="86998-177">**PlayReady solo con Smooth Streaming, HLS e MPEG-DASH** : i flussi Smooth Streaming, HLS e MPEG-DASH verranno crittografati dinamicamente con la soluzione DRM PlayReady.</span><span class="sxs-lookup"><span data-stu-id="86998-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="86998-178">**Solo Widevine con MPEG-DASH** : il flusso MPEG-DASH verrà crittografato dinamicamente con la soluzione DRM Widevine.</span><span class="sxs-lookup"><span data-stu-id="86998-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="86998-179">**Solo FairPlay con HLS** : il flusso HLS verrà crittografato dinamicamente con FairPlay.</span><span class="sxs-lookup"><span data-stu-id="86998-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="86998-180">crittografia FairPlay tooenable, è necessario tooprovide hello App certificato e chiave privata dell'applicazione (chiedere) tramite l'opzione di configurazione FairPlay del pannello delle impostazioni di protezione del contenuto hello hello.</span><span class="sxs-lookup"><span data-stu-id="86998-180">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option of hello Content Protection settings blade.</span></span>

![Proteggere il contenuto](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="86998-182">Una volta apportate selezione della crittografia hello, premere **applica**.</span><span class="sxs-lookup"><span data-stu-id="86998-182">Once you make hello encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="86998-183">Se si intende tooplay un AES crittografata HLS in Safari, vedere [questo blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="86998-183">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86998-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="86998-184">Next steps</span></span>
<span data-ttu-id="86998-185">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="86998-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="86998-186">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="86998-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

