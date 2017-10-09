---
title: aaaProtect del contenuto HLS con Microsoft PlayReady o Apple FairPlay - Azure | Documenti Microsoft
description: Questo argomento viene fornita una panoramica e illustra come crittografare i contenuti FairPlay Apple HTTP Live Streaming (HLS) toouse toodynamically di servizi multimediali di Azure. Viene inoltre illustrato come toouse hello servizi multimediali di licenza del servizio di recapito toodeliver tooclients licenze FairPlay.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="6db13-104">Proteggere il contenuto HLS con Apple FairPlay o Microsoft PlayReady</span><span class="sxs-lookup"><span data-stu-id="6db13-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="6db13-105">Azure consente di servizi multimediali è toodynamically crittografare il contenuto HTTP Live Streaming (HLS) tramite hello seguenti formati:</span><span class="sxs-lookup"><span data-stu-id="6db13-105">Azure Media Services enables you toodynamically encrypt your HTTP Live Streaming (HLS) content by using hello following formats:</span></span>  

* <span data-ttu-id="6db13-106">**Chiave envelope non crittografata AES-128**</span><span class="sxs-lookup"><span data-stu-id="6db13-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="6db13-107">Hello intero blocco verrà crittografato tramite hello **CBC AES-128** modalità.</span><span class="sxs-lookup"><span data-stu-id="6db13-107">hello entire chunk is encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="6db13-108">decrittografia di Hello del flusso di hello è supportata da iOS e Windows Media player OS X in modo nativo.</span><span class="sxs-lookup"><span data-stu-id="6db13-108">hello decryption of hello stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="6db13-109">Per altre informazioni, vedere [Uso della crittografia dinamica AES-128 e del servizio di distribuzione delle chiavi](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="6db13-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="6db13-110">**Apple FairPlay**</span><span class="sxs-lookup"><span data-stu-id="6db13-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="6db13-111">Hello singolo video e audio esempi vengono crittografati tramite hello **CBC AES-128** modalità.</span><span class="sxs-lookup"><span data-stu-id="6db13-111">hello individual video and audio samples are encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="6db13-112">**Streaming FairPlay** (FPS) è integrato nei sistemi operativi per dispositivi hello, con il supporto nativo in iOS e Apple TV.</span><span class="sxs-lookup"><span data-stu-id="6db13-112">**FairPlay Streaming** (FPS) is integrated into hello device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="6db13-113">Safari su OS X consente FPS usando il supporto di interfaccia di hello crittografati supporti le estensioni (EME).</span><span class="sxs-lookup"><span data-stu-id="6db13-113">Safari on OS X enables FPS by using hello Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="6db13-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="6db13-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="6db13-115">Hello immagine seguente viene illustrato hello **HLS + FairPlay o PlayReady crittografia dinamica** flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6db13-115">hello following image shows hello **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![Diagramma del flusso di lavoro della crittografia dinamica](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="6db13-117">In questo argomento viene illustrato come crittografare il contenuto HLS con Apple FairPlay i toouse toodynamically di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="6db13-117">This topic demonstrates how toouse Media Services toodynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="6db13-118">Viene inoltre illustrato come toouse hello servizi multimediali di licenza del servizio di recapito toodeliver tooclients licenze FairPlay.</span><span class="sxs-lookup"><span data-stu-id="6db13-118">It also shows how toouse hello Media Services license delivery service toodeliver FairPlay licenses tooclients.</span></span>

> [!NOTE]
> <span data-ttu-id="6db13-119">Se si desidera tooencrypt il contenuto HLS contenuto con PlayReady, è necessario toocreate una chiave simmetrica comune e associarlo all'asset.</span><span class="sxs-lookup"><span data-stu-id="6db13-119">If you also want tooencrypt your HLS content with PlayReady, you need toocreate a common content key and associate it with your asset.</span></span> <span data-ttu-id="6db13-120">È inoltre necessario criteri di autorizzazione tooconfigure hello della chiave simmetrica, come descritto in [PlayReady usando la crittografia dinamica comune](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="6db13-120">You also need tooconfigure hello content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="6db13-121">Problemi e considerazioni</span><span class="sxs-lookup"><span data-stu-id="6db13-121">Requirements and considerations</span></span>

<span data-ttu-id="6db13-122">di seguito Hello sono necessarie quando si usa servizi multimediali toodeliver che HLS crittografato con FairPlay e licenze FairPlay toodeliver:</span><span class="sxs-lookup"><span data-stu-id="6db13-122">hello following are required when using Media Services toodeliver HLS encrypted with FairPlay, and toodeliver FairPlay licenses:</span></span>

  * <span data-ttu-id="6db13-123">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="6db13-123">An Azure account.</span></span> <span data-ttu-id="6db13-124">Per informazioni dettagliate, vedere la pagina relativa alla [versione di prova gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="6db13-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="6db13-125">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="6db13-125">A Media Services account.</span></span> <span data-ttu-id="6db13-126">toocreate uno, vedere [creare un account di servizi multimediali di Azure tramite il portale di Azure hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="6db13-126">toocreate one, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="6db13-127">Eseguire l'iscrizione all' [Apple Development Program](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="6db13-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="6db13-128">Apple richiede hello tooobtain proprietario del contenuto di hello [pacchetto di distribuzione](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="6db13-128">Apple requires hello content owner tooobtain hello [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="6db13-129">Stato che già stata implementata chiave protezione modulo (KSM) con servizi multimediali e che si sta richiedendo pacchetto FPS finale hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting hello final FPS package.</span></span> <span data-ttu-id="6db13-130">Sono disponibili istruzioni hello FPS finale pacchetto certificazione toogenerate e ottenere hello chiave segreto applicazione (ricerca).</span><span class="sxs-lookup"><span data-stu-id="6db13-130">There are instructions in hello final FPS package toogenerate certification and obtain hello Application Secret Key (ASK).</span></span> <span data-ttu-id="6db13-131">Consente di chiedere tooconfigure FairPlay.</span><span class="sxs-lookup"><span data-stu-id="6db13-131">You use ASK tooconfigure FairPlay.</span></span>
  * <span data-ttu-id="6db13-132">Azure Media Services .NET SDK versione **3.6.0** o successiva.</span><span class="sxs-lookup"><span data-stu-id="6db13-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="6db13-133">sul lato di distribuzione delle chiavi di servizi multimediali, è necessario impostare Hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="6db13-133">hello following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="6db13-134">**App del certificato (CA)**: si tratta di un file con estensione pfx che contiene la chiave privata di hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-134">**App Cert (AC)**: This is a .pfx file that contains hello private key.</span></span> <span data-ttu-id="6db13-135">Creare il file e crittografarlo con una password.</span><span class="sxs-lookup"><span data-stu-id="6db13-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="6db13-136">Quando si configura un criterio di distribuzione delle chiavi, è necessario fornire il file con estensione pfx hello e password in formato base 64.</span><span class="sxs-lookup"><span data-stu-id="6db13-136">When you configure a key delivery policy, you must provide that password and hello .pfx file in Base64 format.</span></span>

      <span data-ttu-id="6db13-137">Hello alla procedura seguente viene descritto come file di toogenerate un certificato PFX per FairPlay:</span><span class="sxs-lookup"><span data-stu-id="6db13-137">hello following steps describe how toogenerate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="6db13-138">Installare OpenSSL da https://slproweb.com/products/Win32OpenSSL.html.</span><span class="sxs-lookup"><span data-stu-id="6db13-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="6db13-139">Passare toohello cartella in cui il certificato di FairPlay hello e altri file recapitati da Apple.</span><span class="sxs-lookup"><span data-stu-id="6db13-139">Go toohello folder where hello FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="6db13-140">Eseguire hello comando seguente dalla riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-140">Run hello following command from hello command line.</span></span> <span data-ttu-id="6db13-141">Consente di convertire il file con estensione PEM tooa di hello. cer file.</span><span class="sxs-lookup"><span data-stu-id="6db13-141">This converts hello .cer file tooa .pem file.</span></span>

        <span data-ttu-id="6db13-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span><span class="sxs-lookup"><span data-stu-id="6db13-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="6db13-143">Eseguire hello comando seguente dalla riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-143">Run hello following command from hello command line.</span></span> <span data-ttu-id="6db13-144">Consente di convertire file con estensione pfx tooa file con estensione PEM hello con la chiave privata di hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-144">This converts hello .pem file tooa .pfx file with hello private key.</span></span> <span data-ttu-id="6db13-145">password Hello per file con estensione pfx hello viene quindi richiesto da OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="6db13-145">hello password for hello .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="6db13-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="6db13-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="6db13-147">**La password del certificato app**: password hello per la creazione di file con estensione pfx hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-147">**App Cert password**: hello password for creating hello .pfx file.</span></span>
  * <span data-ttu-id="6db13-148">**ID della password di App Cert**: È necessario caricare password hello, toohow simile caricamento altre chiavi di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="6db13-148">**App Cert password ID**: You must upload hello password, similar toohow they upload other Media Services keys.</span></span> <span data-ttu-id="6db13-149">Hello utilizzare **ContentKeyType.FairPlayPfxPassword** hello tooget valore di enumerazione ID servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="6db13-149">Use hello **ContentKeyType.FairPlayPfxPassword** enum value tooget hello Media Services ID.</span></span> <span data-ttu-id="6db13-150">Questo è ciò che richiedono toouse all'interno di opzione del criterio hello distribuzione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="6db13-150">This is what they need toouse inside hello key delivery policy option.</span></span>
  * <span data-ttu-id="6db13-151">**iv**: valore casuale di 16 byte</span><span class="sxs-lookup"><span data-stu-id="6db13-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="6db13-152">Deve corrispondere hello iv in Criteri di distribuzione di asset hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-152">It must match hello iv in hello asset delivery policy.</span></span> <span data-ttu-id="6db13-153">Generare hello iv e inserirlo in entrambe le posizioni: criteri di distribuzione di asset hello e l'opzione criteri di distribuzione delle chiavi hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-153">You generate hello iv, and put it in both places: hello asset delivery policy and hello key delivery policy option.</span></span>
  * <span data-ttu-id="6db13-154">**CHIEDERE**: questa chiave viene ricevuta quando si genera certificazione hello tramite hello Apple Developer portal.</span><span class="sxs-lookup"><span data-stu-id="6db13-154">**ASK**: This key is received when you generate hello certification by using hello Apple Developer portal.</span></span> <span data-ttu-id="6db13-155">Ogni team di sviluppo riceve una chiave ASK univoca.</span><span class="sxs-lookup"><span data-stu-id="6db13-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="6db13-156">Salvare una copia di hello chiedere e archiviarlo in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="6db13-156">Save a copy of hello ASK, and store it in a safe place.</span></span> <span data-ttu-id="6db13-157">È necessario chiedere tooconfigure come FairPlayAsk tooMedia servizi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="6db13-157">You will need tooconfigure ASK as FairPlayAsk tooMedia Services later.</span></span>
  * <span data-ttu-id="6db13-158">**ID ASK**: ID ottenuto quando si carica la chiave privata dell'applicazione in Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="6db13-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="6db13-159">È necessario caricare chiedere utilizzando hello **ContentKeyType.FairPlayAsk** valore enum.</span><span class="sxs-lookup"><span data-stu-id="6db13-159">You must upload ASK by using hello **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="6db13-160">Di conseguenza hello, viene restituito l'ID di servizi multimediali hello e questo è ciò che deve essere utilizzato quando l'impostazione di opzione di criteri di distribuzione delle chiavi hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-160">As hello result, hello Media Services ID is returned, and this is what should be used when setting hello key delivery policy option.</span></span>

<span data-ttu-id="6db13-161">Hello operazioni indicate di seguito devono essere impostate dal lato client FPS hello:</span><span class="sxs-lookup"><span data-stu-id="6db13-161">hello following things must be set by hello FPS client side:</span></span>

  * <span data-ttu-id="6db13-162">**App del certificato (CA)**: si tratta di un file.cer/.der contenente hello chiave pubblica, il sistema operativo hello utilizza tooencrypt alcuni payload.</span><span class="sxs-lookup"><span data-stu-id="6db13-162">**App Cert (AC)**: This is a .cer/.der file that contains hello public key, which hello operating system uses tooencrypt some payload.</span></span> <span data-ttu-id="6db13-163">Servizi multimediali deve tooknow su di esso perché è richiesto da Windows Media player hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-163">Media Services needs tooknow about it because it is required by hello player.</span></span> <span data-ttu-id="6db13-164">il servizio di distribuzione delle chiavi Hello decrittografa usando la chiave privata corrispondente di hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-164">hello key delivery service decrypts it using hello corresponding private key.</span></span>

<span data-ttu-id="6db13-165">tooplay un flusso crittografato FairPlay, ottenere una reale chiedere prima e quindi generare un certificato reale.</span><span class="sxs-lookup"><span data-stu-id="6db13-165">tooplay back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="6db13-166">Questo processo crea tutte le 3 parti:</span><span class="sxs-lookup"><span data-stu-id="6db13-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="6db13-167">file con estensione der</span><span class="sxs-lookup"><span data-stu-id="6db13-167">.der file</span></span>
  * <span data-ttu-id="6db13-168">file con estensione pfx</span><span class="sxs-lookup"><span data-stu-id="6db13-168">.pfx file</span></span>
  * <span data-ttu-id="6db13-169">password per PFX hello</span><span class="sxs-lookup"><span data-stu-id="6db13-169">password for hello .pfx</span></span>

<span data-ttu-id="6db13-170">i seguenti client Hello supporta contenuto HLS con **CBC AES-128** crittografia: Safari su OS X, Apple TV, iOS.</span><span class="sxs-lookup"><span data-stu-id="6db13-170">hello following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="6db13-171">Configurare la crittografia dinamica FairPlay e i servizi di distribuzione delle licenze</span><span class="sxs-lookup"><span data-stu-id="6db13-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="6db13-172">di seguito Hello sono passaggi generali per proteggere gli asset con FairPlay utilizzando hello licenza recapito servizi multimediali e usando la crittografia dinamica.</span><span class="sxs-lookup"><span data-stu-id="6db13-172">hello following are general steps for protecting your assets with FairPlay by using hello Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="6db13-173">Creare un asset e caricare i file nell'asset hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-173">Create an asset, and upload files into hello asset.</span></span>
2. <span data-ttu-id="6db13-174">Codificare asset hello contenente hello file toohello velocità in bit adattiva che set MP4.</span><span class="sxs-lookup"><span data-stu-id="6db13-174">Encode hello asset that contains hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="6db13-175">Creare una chiave simmetrica e associarlo all'asset codificato hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-175">Create a content key, and associate it with hello encoded asset.</span></span>  
4. <span data-ttu-id="6db13-176">Configurare criteri di autorizzazione della chiave simmetrica hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-176">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="6db13-177">Specificare hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="6db13-177">Specify hello following:</span></span>

   * <span data-ttu-id="6db13-178">metodo di recapito Hello (in questo caso, FairPlay).</span><span class="sxs-lookup"><span data-stu-id="6db13-178">hello delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="6db13-179">configurazione delle opzioni dei criteri FairPlay.</span><span class="sxs-lookup"><span data-stu-id="6db13-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="6db13-180">Per informazioni dettagliate su come tooconfigure FairPlay, vedere hello **ConfigureFairPlayPolicyOptions()** metodo esempio hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6db13-180">For details on how tooconfigure FairPlay, see hello **ConfigureFairPlayPolicyOptions()** method in hello sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="6db13-181">In genere, è opportuno tooconfigure FairPlay criteri opzioni una sola volta, poiché è solo un set di un certificato e una ricerca.</span><span class="sxs-lookup"><span data-stu-id="6db13-181">Usually, you would want tooconfigure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="6db13-182">Restrizioni aperte o token.</span><span class="sxs-lookup"><span data-stu-id="6db13-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="6db13-183">Tipo distribuzione delle chiavi specifico toohello informazioni che definisce come chiave hello viene recapitato toohello client.</span><span class="sxs-lookup"><span data-stu-id="6db13-183">Information specific toohello key delivery type that defines how hello key is delivered toohello client.</span></span>
5. <span data-ttu-id="6db13-184">Configurare i criteri di distribuzione di asset hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-184">Configure hello asset delivery policy.</span></span> <span data-ttu-id="6db13-185">configurazione dei criteri di recapito Hello include:</span><span class="sxs-lookup"><span data-stu-id="6db13-185">hello delivery policy configuration includes:</span></span>

   * <span data-ttu-id="6db13-186">protocollo di recapito Hello (HLS).</span><span class="sxs-lookup"><span data-stu-id="6db13-186">hello delivery protocol (HLS).</span></span>
   * <span data-ttu-id="6db13-187">tipo di Hello di crittografia dinamica (crittografia CBC comune).</span><span class="sxs-lookup"><span data-stu-id="6db13-187">hello type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="6db13-188">URL di acquisizione della licenza Hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-188">hello license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="6db13-189">Se si desidera toodeliver un flusso che viene crittografato con FairPlay e un altro sistema di Digital Rights Management (DRM), si dispone di criteri di recapito di tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="6db13-189">If you want toodeliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have tooconfigure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="6db13-190">Un tooconfigure IAssetDeliveryPolicy lo Streaming adattivo dinamica su HTTP (trattino) con CENC (Common Encryption) (PlayReady + Widevine) e Smooth Streaming con PlayReady</span><span class="sxs-lookup"><span data-stu-id="6db13-190">One IAssetDeliveryPolicy tooconfigure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="6db13-191">Un altro IAssetDeliveryPolicy tooconfigure FairPlay per HLS</span><span class="sxs-lookup"><span data-stu-id="6db13-191">Another IAssetDeliveryPolicy tooconfigure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="6db13-192">Creare un tooget localizzatore OnDemand un URL di streaming.</span><span class="sxs-lookup"><span data-stu-id="6db13-192">Create an OnDemand locator tooget a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="6db13-193">Usare la distribuzione delle chiavi FairPlay con applicazioni lettore</span><span class="sxs-lookup"><span data-stu-id="6db13-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="6db13-194">È possibile sviluppare applicazioni di Windows Media player utilizzando hello iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="6db13-194">You can develop player apps by using hello iOS SDK.</span></span> <span data-ttu-id="6db13-195">toobe tooplay in grado di FairPlay contenuto, è necessario protocollo di scambio tooimplement hello licenza.</span><span class="sxs-lookup"><span data-stu-id="6db13-195">toobe able tooplay FairPlay content, you have tooimplement hello license exchange protocol.</span></span> <span data-ttu-id="6db13-196">Questo protocollo non è specificato da Apple.</span><span class="sxs-lookup"><span data-stu-id="6db13-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="6db13-197">È la distribuzione delle chiavi toosend richiede backup tooeach app.</span><span class="sxs-lookup"><span data-stu-id="6db13-197">It is up tooeach app how toosend key delivery requests.</span></span> <span data-ttu-id="6db13-198">Hello del servizio di distribuzione delle chiavi di Media Services FairPlay hello SPC toocome previsto è un messaggio post codificati www-form-url hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="6db13-198">hello Media Services FairPlay key delivery service expects hello SPC toocome as a www-form-url encoded post message, in hello following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="6db13-199">Azure Media Player non supporta la riproduzione di FairPlay predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="6db13-199">Azure Media Player doesn’t support FairPlay playback out of hello box.</span></span> <span data-ttu-id="6db13-200">riproduzione di FairPlay tooget su MAC OS X, ottenere il lettore di esempio hello da hello account per sviluppatori di Apple.</span><span class="sxs-lookup"><span data-stu-id="6db13-200">tooget FairPlay playback on MAC OS X, obtain hello sample player from hello Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="6db13-201">URL di streaming</span><span class="sxs-lookup"><span data-stu-id="6db13-201">Streaming URLs</span></span>
<span data-ttu-id="6db13-202">Se l'asset è stata crittografata con più DRM, è necessario utilizzare un tag di crittografia nell'URL di streaming hello: (formato = 'm3u8-aapl', crittografia = 'xxx').</span><span class="sxs-lookup"><span data-stu-id="6db13-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in hello streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="6db13-203">si applica Hello seguenti considerazioni:</span><span class="sxs-lookup"><span data-stu-id="6db13-203">hello following considerations apply:</span></span>

* <span data-ttu-id="6db13-204">Può essere specificato solo un tipo di crittografia oppure nessuno.</span><span class="sxs-lookup"><span data-stu-id="6db13-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="6db13-205">tipo di crittografia Hello privo di toobe specificata nell'URL di hello se solo uno di crittografia è stata applicata toohello asset.</span><span class="sxs-lookup"><span data-stu-id="6db13-205">hello encryption type doesn't have toobe specified in hello URL if only one encryption was applied toohello asset.</span></span>
* <span data-ttu-id="6db13-206">tipo di crittografia Hello viene fatta distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="6db13-206">hello encryption type is case insensitive.</span></span>
* <span data-ttu-id="6db13-207">è possibile specificare i seguenti tipi di crittografia Hello:</span><span class="sxs-lookup"><span data-stu-id="6db13-207">hello following encryption types can be specified:</span></span>  
  * <span data-ttu-id="6db13-208">**cenc**: crittografia comune (PlayReady o Widevine)</span><span class="sxs-lookup"><span data-stu-id="6db13-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="6db13-209">**cbcs-aapl**: FairPlay</span><span class="sxs-lookup"><span data-stu-id="6db13-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="6db13-210">**cbc**: crittografia busta AES</span><span class="sxs-lookup"><span data-stu-id="6db13-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="6db13-211">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6db13-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="6db13-212">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="6db13-212">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="6db13-213">Aggiungere i seguenti elementi troppo hello**appSettings** definiti nel file app. config:</span><span class="sxs-lookup"><span data-stu-id="6db13-213">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="6db13-214">Esempio</span><span class="sxs-lookup"><span data-stu-id="6db13-214">Example</span></span>

<span data-ttu-id="6db13-215">Hello seguente esempio viene illustrato hello possibilità toouse toodeliver di servizi multimediali del contenuto crittografato con FairPlay.</span><span class="sxs-lookup"><span data-stu-id="6db13-215">hello following sample demonstrates hello ability toouse Media Services toodeliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="6db13-216">Questa funzionalità è stata introdotta in hello Azure Media Services SDK per .NET versione 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="6db13-216">This functionality was introduced in hello Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="6db13-217">Sovrascrivere il codice hello nel file Program.cs con il codice di hello illustrato in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="6db13-217">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="6db13-218">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="6db13-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="6db13-219">È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni accesso le autorizzazioni, ad esempio, i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri).</span><span class="sxs-lookup"><span data-stu-id="6db13-219">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="6db13-220">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="6db13-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="6db13-221">Rendere le variabili tooupdate che toopoint toofolders in cui si trovano i file di input.</span><span class="sxs-lookup"><span data-stu-id="6db13-221">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }


        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Open",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                        Requirements = null
                    }
                    };


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Token Authorization Policy",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                        Requirements = tokenTemplateString,
                    }
                    };

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();
            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
            assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="6db13-222">Passaggi successivi: Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="6db13-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6db13-223">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="6db13-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
