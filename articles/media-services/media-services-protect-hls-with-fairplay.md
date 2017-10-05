---
title: Proteggere il contenuto HLS con Microsoft PlayReady o con Apple FairPlay | Documentazione Microsoft
description: Questo argomento offre una panoramica su come usare Servizi multimediali di Azure per crittografare dinamicamente il contenuto HTTP Live Streaming (HLS) con Apple FairPlay. Viene anche illustrato come usare il servizio di distribuzione delle licenze di Servizi multimediali per distribuire le licenze FairPlay ai client.
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
ms.openlocfilehash: 895d6307b1cef74e195cc2ffd8dbef4196e97b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="b5c11-104">Proteggere il contenuto HLS con Apple FairPlay o Microsoft PlayReady</span><span class="sxs-lookup"><span data-stu-id="b5c11-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="b5c11-105">Servizi multimediali di Azure consente di crittografare dinamicamente il contenuto di HTTP Live Streaming (HLS) usando i formati seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5c11-105">Azure Media Services enables you to dynamically encrypt your HTTP Live Streaming (HLS) content by using the following formats:</span></span>  

* <span data-ttu-id="b5c11-106">**Chiave envelope non crittografata AES-128**</span><span class="sxs-lookup"><span data-stu-id="b5c11-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="b5c11-107">L'intero blocco viene crittografato usando la modalità **AES-128 CBC**.</span><span class="sxs-lookup"><span data-stu-id="b5c11-107">The entire chunk is encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="b5c11-108">La decrittografia del flusso è supportata dai lettori iOS e OSX in modo nativo.</span><span class="sxs-lookup"><span data-stu-id="b5c11-108">The decryption of the stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="b5c11-109">Per altre informazioni, vedere [Uso della crittografia dinamica AES-128 e del servizio di distribuzione delle chiavi](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="b5c11-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="b5c11-110">**Apple FairPlay**</span><span class="sxs-lookup"><span data-stu-id="b5c11-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="b5c11-111">I singoli campioni audio e video vengono crittografati con la modalità **AES-128 CBC**.</span><span class="sxs-lookup"><span data-stu-id="b5c11-111">The individual video and audio samples are encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="b5c11-112">**FairPlay Streaming** (FPS) è integrato nei sistemi operativi dei dispositivi, con supporto nativo per iOS e Apple TV.</span><span class="sxs-lookup"><span data-stu-id="b5c11-112">**FairPlay Streaming** (FPS) is integrated into the device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="b5c11-113">Safari su OS X abilita FPS con il supporto dell'interfaccia EME (Encrypted Media Extensions).</span><span class="sxs-lookup"><span data-stu-id="b5c11-113">Safari on OS X enables FPS by using the Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="b5c11-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="b5c11-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="b5c11-115">L'immagine seguente illustra il flusso di lavoro della **crittografia dinamica HLS + FairPlay o PlayReady**.</span><span class="sxs-lookup"><span data-stu-id="b5c11-115">The following image shows the **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![Diagramma del flusso di lavoro della crittografia dinamica](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="b5c11-117">Questo argomento illustra come usare Servizi multimediali per crittografare dinamicamente il contenuto HLS con Apple FairPlay.</span><span class="sxs-lookup"><span data-stu-id="b5c11-117">This topic demonstrates how to use Media Services to dynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="b5c11-118">Viene anche illustrato come usare il servizio di distribuzione delle licenze di Servizi multimediali per distribuire le licenze FairPlay ai client.</span><span class="sxs-lookup"><span data-stu-id="b5c11-118">It also shows how to use the Media Services license delivery service to deliver FairPlay licenses to clients.</span></span>

> [!NOTE]
> <span data-ttu-id="b5c11-119">Se si vuole crittografare anche il contenuto HLS con PlayReady, è necessario creare una chiave di contenuto comune e associarla all'asset.</span><span class="sxs-lookup"><span data-stu-id="b5c11-119">If you also want to encrypt your HLS content with PlayReady, you need to create a common content key and associate it with your asset.</span></span> <span data-ttu-id="b5c11-120">È anche necessario configurare i criteri di autorizzazione della chiave simmetrica, come descritto in [Uso della crittografia comune dinamica PlayReady](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="b5c11-120">You also need to configure the content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="b5c11-121">Problemi e considerazioni</span><span class="sxs-lookup"><span data-stu-id="b5c11-121">Requirements and considerations</span></span>

<span data-ttu-id="b5c11-122">Se si usa Servizi multimediali per distribuire contenuto HLS crittografato con FairPlay e per distribuire licenze FairPlay, è necessario:</span><span class="sxs-lookup"><span data-stu-id="b5c11-122">The following are required when using Media Services to deliver HLS encrypted with FairPlay, and to deliver FairPlay licenses:</span></span>

  * <span data-ttu-id="b5c11-123">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="b5c11-123">An Azure account.</span></span> <span data-ttu-id="b5c11-124">Per informazioni dettagliate, vedere la pagina relativa alla [versione di prova gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="b5c11-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="b5c11-125">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="b5c11-125">A Media Services account.</span></span> <span data-ttu-id="b5c11-126">Per crearne uno, vedere [Creare un account Servizi multimediali di Azure con il portale di Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="b5c11-126">To create one, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="b5c11-127">Eseguire l'iscrizione all' [Apple Development Program](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="b5c11-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="b5c11-128">Apple richiede che il proprietario del contenuto ottenga il [pacchetto di distribuzione](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="b5c11-128">Apple requires the content owner to obtain the [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="b5c11-129">Indicare che è già stato implementato il modulo KSM (Key Security Module) con Servizi multimediali e che si sta richiedendo il pacchetto FPS finale.</span><span class="sxs-lookup"><span data-stu-id="b5c11-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting the final FPS package.</span></span> <span data-ttu-id="b5c11-130">Il pacchetto FPS finale contiene istruzioni per generare la certificazione e ottenere la chiave privata dell'applicazione,</span><span class="sxs-lookup"><span data-stu-id="b5c11-130">There are instructions in the final FPS package to generate certification and obtain the Application Secret Key (ASK).</span></span> <span data-ttu-id="b5c11-131">che verrà usata per configurare FairPlay.</span><span class="sxs-lookup"><span data-stu-id="b5c11-131">You use ASK to configure FairPlay.</span></span>
  * <span data-ttu-id="b5c11-132">Azure Media Services .NET SDK versione **3.6.0** o successiva.</span><span class="sxs-lookup"><span data-stu-id="b5c11-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="b5c11-133">È necessario impostare quanto segue in aggiunta alla distribuzione delle chiavi di Servizi multimediali:</span><span class="sxs-lookup"><span data-stu-id="b5c11-133">The following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="b5c11-134">**App Cert (AC)**: file con estensione pfx contenente la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="b5c11-134">**App Cert (AC)**: This is a .pfx file that contains the private key.</span></span> <span data-ttu-id="b5c11-135">Creare il file e crittografarlo con una password.</span><span class="sxs-lookup"><span data-stu-id="b5c11-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="b5c11-136">Quando si configurano i criteri di distribuzione delle chiavi, è necessario specificare la password e il file pfx in formato Base64.</span><span class="sxs-lookup"><span data-stu-id="b5c11-136">When you configure a key delivery policy, you must provide that password and the .pfx file in Base64 format.</span></span>

      <span data-ttu-id="b5c11-137">La procedura seguente descrive come generare un file di certificato pfx per FairPlay:</span><span class="sxs-lookup"><span data-stu-id="b5c11-137">The following steps describe how to generate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="b5c11-138">Installare OpenSSL da https://slproweb.com/products/Win32OpenSSL.html.</span><span class="sxs-lookup"><span data-stu-id="b5c11-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="b5c11-139">Passare alla cartella contenente il certificato FairPlay e altri file forniti da Apple.</span><span class="sxs-lookup"><span data-stu-id="b5c11-139">Go to the folder where the FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="b5c11-140">Eseguire il comando seguente dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="b5c11-140">Run the following command from the command line.</span></span> <span data-ttu-id="b5c11-141">Il comando converte il file con estensione cer in un file con estensione pem.</span><span class="sxs-lookup"><span data-stu-id="b5c11-141">This converts the .cer file to a .pem file.</span></span>

        <span data-ttu-id="b5c11-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span><span class="sxs-lookup"><span data-stu-id="b5c11-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="b5c11-143">Eseguire il comando seguente dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="b5c11-143">Run the following command from the command line.</span></span> <span data-ttu-id="b5c11-144">Questo comando converte il file con estensione pem in un file con estensione pfx con la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="b5c11-144">This converts the .pem file to a .pfx file with the private key.</span></span> <span data-ttu-id="b5c11-145">La password per il file con estensione pfx viene quindi richiesta da OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="b5c11-145">The password for the .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="b5c11-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="b5c11-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="b5c11-147">**App Cert password**: password del cliente per creare il file con estensione pfx.</span><span class="sxs-lookup"><span data-stu-id="b5c11-147">**App Cert password**: The password for creating the .pfx file.</span></span>
  * <span data-ttu-id="b5c11-148">**App Cert password ID**: è necessario caricare la password con una procedura simile a quella usata per caricare le altre chiavi di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="b5c11-148">**App Cert password ID**: You must upload the password, similar to how they upload other Media Services keys.</span></span> <span data-ttu-id="b5c11-149">Usare il valore di enumerazione **ContentKeyType.FairPlayPfxPassword** per ottenere l'ID di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="b5c11-149">Use the **ContentKeyType.FairPlayPfxPassword** enum value to get the Media Services ID.</span></span> <span data-ttu-id="b5c11-150">Questo valore è necessario nell'opzione dei criteri di distribuzione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="b5c11-150">This is what they need to use inside the key delivery policy option.</span></span>
  * <span data-ttu-id="b5c11-151">**iv**: valore casuale di 16 byte</span><span class="sxs-lookup"><span data-stu-id="b5c11-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="b5c11-152">che deve corrispondere al valore iv nei criteri di distribuzione dell'asset.</span><span class="sxs-lookup"><span data-stu-id="b5c11-152">It must match the iv in the asset delivery policy.</span></span> <span data-ttu-id="b5c11-153">Si genera l'iv e lo inserisce sia nei criteri di distribuzione dell'asset che nell'opzione dei criteri di distribuzione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="b5c11-153">You generate the iv, and put it in both places: the asset delivery policy and the key delivery policy option.</span></span>
  * <span data-ttu-id="b5c11-154">**ASK**: chiave ricevuta quando si genera la certificazione usando il portale Apple Developer.</span><span class="sxs-lookup"><span data-stu-id="b5c11-154">**ASK**: This key is received when you generate the certification by using the Apple Developer portal.</span></span> <span data-ttu-id="b5c11-155">Ogni team di sviluppo riceve una chiave ASK univoca.</span><span class="sxs-lookup"><span data-stu-id="b5c11-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="b5c11-156">Salvare una copia della chiave ASK e archiviarla in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="b5c11-156">Save a copy of the ASK, and store it in a safe place.</span></span> <span data-ttu-id="b5c11-157">Successivamente sarà necessario configurare la chiave ASK come FairPlayAsk in Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="b5c11-157">You will need to configure ASK as FairPlayAsk to Media Services later.</span></span>
  * <span data-ttu-id="b5c11-158">**ID ASK**: ID ottenuto quando si carica la chiave privata dell'applicazione in Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="b5c11-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="b5c11-159">È necessario caricare la chiave privata dell'applicazione usando il valore di enumerazione **ContentKeyType.FairPlayASk**.</span><span class="sxs-lookup"><span data-stu-id="b5c11-159">You must upload ASK by using the **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="b5c11-160">Verrà restituito l'ID di Servizi multimediali che dovrà essere usato per impostare l'opzione dei criteri di distribuzione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="b5c11-160">As the result, the Media Services ID is returned, and this is what should be used when setting the key delivery policy option.</span></span>

<span data-ttu-id="b5c11-161">Sul lato client FPS è necessario impostare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b5c11-161">The following things must be set by the FPS client side:</span></span>

  * <span data-ttu-id="b5c11-162">**App Cert (AC)**: file con estensione cer/der contenente la chiave pubblica usata dal sistema operativo per crittografare alcuni payload.</span><span class="sxs-lookup"><span data-stu-id="b5c11-162">**App Cert (AC)**: This is a .cer/.der file that contains the public key, which the operating system uses to encrypt some payload.</span></span> <span data-ttu-id="b5c11-163">È necessario che Servizi multimediali lo riconosca perché è richiesto dal lettore.</span><span class="sxs-lookup"><span data-stu-id="b5c11-163">Media Services needs to know about it because it is required by the player.</span></span> <span data-ttu-id="b5c11-164">Il servizio di distribuzione delle chiavi lo decrittografa usando la chiave privata corrispondente.</span><span class="sxs-lookup"><span data-stu-id="b5c11-164">The key delivery service decrypts it using the corresponding private key.</span></span>

<span data-ttu-id="b5c11-165">Per riprodurre un flusso crittografato FairPlay, ottenere prima una chiave privata dell'applicazione reale, quindi generare un certificato reale.</span><span class="sxs-lookup"><span data-stu-id="b5c11-165">To play back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="b5c11-166">Questo processo crea tutte le 3 parti:</span><span class="sxs-lookup"><span data-stu-id="b5c11-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="b5c11-167">file con estensione der</span><span class="sxs-lookup"><span data-stu-id="b5c11-167">.der file</span></span>
  * <span data-ttu-id="b5c11-168">file con estensione pfx</span><span class="sxs-lookup"><span data-stu-id="b5c11-168">.pfx file</span></span>
  * <span data-ttu-id="b5c11-169">password per il file pfx</span><span class="sxs-lookup"><span data-stu-id="b5c11-169">password for the .pfx</span></span>

<span data-ttu-id="b5c11-170">I client seguenti supportano il formato HLS con la crittografia **AES-128 CBC**: Safari in OS X, Apple TV e iOS.</span><span class="sxs-lookup"><span data-stu-id="b5c11-170">The following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="b5c11-171">Configurare la crittografia dinamica FairPlay e i servizi di distribuzione delle licenze</span><span class="sxs-lookup"><span data-stu-id="b5c11-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="b5c11-172">Di seguito sono indicati i passaggi generali per la protezione degli asset con FairPlay usando il servizio di distribuzione delle licenze di Servizi multimediali e la crittografia dinamica.</span><span class="sxs-lookup"><span data-stu-id="b5c11-172">The following are general steps for protecting your assets with FairPlay by using the Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="b5c11-173">Creare un asset e caricare file al suo interno.</span><span class="sxs-lookup"><span data-stu-id="b5c11-173">Create an asset, and upload files into the asset.</span></span>
2. <span data-ttu-id="b5c11-174">Codificare l'asset contenente il file nel set MP4 con velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="b5c11-174">Encode the asset that contains the file to the adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="b5c11-175">Creare una chiave simmetrica e associarla all'asset codificato.</span><span class="sxs-lookup"><span data-stu-id="b5c11-175">Create a content key, and associate it with the encoded asset.</span></span>  
4. <span data-ttu-id="b5c11-176">Configurare i criteri di autorizzazione della chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="b5c11-176">Configure the content key’s authorization policy.</span></span> <span data-ttu-id="b5c11-177">Specificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b5c11-177">Specify the following:</span></span>

   * <span data-ttu-id="b5c11-178">metodo di distribuzione, in questo caso FairPlay,</span><span class="sxs-lookup"><span data-stu-id="b5c11-178">The delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="b5c11-179">configurazione delle opzioni dei criteri FairPlay.</span><span class="sxs-lookup"><span data-stu-id="b5c11-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="b5c11-180">Per informazioni dettagliate sulla configurazione di FairPlay, vedere il metodo **ConfigureFairPlayPolicyOptions()** nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="b5c11-180">For details on how to configure FairPlay, see the **ConfigureFairPlayPolicyOptions()** method in the sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b5c11-181">In genere è opportuno configurare le opzioni dei criteri FairPlay una sola volta, dato che sarà presente un solo set di certificazione e chiave privata dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b5c11-181">Usually, you would want to configure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="b5c11-182">Restrizioni aperte o token.</span><span class="sxs-lookup"><span data-stu-id="b5c11-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="b5c11-183">Informazioni specifiche per il tipo di distribuzione delle chiavi che definiscono la modalità di distribuzione della chiave al client.</span><span class="sxs-lookup"><span data-stu-id="b5c11-183">Information specific to the key delivery type that defines how the key is delivered to the client.</span></span>
5. <span data-ttu-id="b5c11-184">Configurare i criteri di distribuzione dell'asset.</span><span class="sxs-lookup"><span data-stu-id="b5c11-184">Configure the asset delivery policy.</span></span> <span data-ttu-id="b5c11-185">La configurazione dei criteri di distribuzione include:</span><span class="sxs-lookup"><span data-stu-id="b5c11-185">The delivery policy configuration includes:</span></span>

   * <span data-ttu-id="b5c11-186">Il protocollo di recapito (HLS).</span><span class="sxs-lookup"><span data-stu-id="b5c11-186">The delivery protocol (HLS).</span></span>
   * <span data-ttu-id="b5c11-187">Il tipo di crittografia dinamica (crittografia CBC comune).</span><span class="sxs-lookup"><span data-stu-id="b5c11-187">The type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="b5c11-188">L'URL di acquisizione delle licenze.</span><span class="sxs-lookup"><span data-stu-id="b5c11-188">The license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b5c11-189">Per distribuire un flusso crittografato con FairPlay e un altro sistema Digital Rights Management (DRM), è necessario configurare criteri di distribuzione separati:</span><span class="sxs-lookup"><span data-stu-id="b5c11-189">If you want to deliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have to configure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="b5c11-190">Una norma IAssetDeliveryPolicy per configurare Dynamic Adaptive Streaming over HTTP (DASH) con Common Encryption (CENC) (PlayReady e Widevine) e Smooth con PlayReady</span><span class="sxs-lookup"><span data-stu-id="b5c11-190">One IAssetDeliveryPolicy to configure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="b5c11-191">Un altro criterio IAssetDeliveryPolicy per configurare FairPlay per HLS</span><span class="sxs-lookup"><span data-stu-id="b5c11-191">Another IAssetDeliveryPolicy to configure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="b5c11-192">Creare un localizzatore OnDemand per ottenere un URL di streaming.</span><span class="sxs-lookup"><span data-stu-id="b5c11-192">Create an OnDemand locator to get a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="b5c11-193">Usare la distribuzione delle chiavi FairPlay con applicazioni lettore</span><span class="sxs-lookup"><span data-stu-id="b5c11-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="b5c11-194">È possibile sviluppare applicazioni lettore usando l'SDK per iOS.</span><span class="sxs-lookup"><span data-stu-id="b5c11-194">You can develop player apps by using the iOS SDK.</span></span> <span data-ttu-id="b5c11-195">Per riprodurre contenuto FairPlay, è necessario implementare il protocollo di scambio delle licenze.</span><span class="sxs-lookup"><span data-stu-id="b5c11-195">To be able to play FairPlay content, you have to implement the license exchange protocol.</span></span> <span data-ttu-id="b5c11-196">Questo protocollo non è specificato da Apple.</span><span class="sxs-lookup"><span data-stu-id="b5c11-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="b5c11-197">Spetta a ogni app scegliere come inviare le richieste di distribuzione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="b5c11-197">It is up to each app how to send key delivery requests.</span></span> <span data-ttu-id="b5c11-198">Il servizio di distribuzione delle chiavi FairPlay di Servizi multimediali prevede che SPC venga indicato in un messaggio codificato come www-form-url nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="b5c11-198">The Media Services FairPlay key delivery service expects the SPC to come as a www-form-url encoded post message, in the following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="b5c11-199">Per impostazione predefinita, Azure Media Player non supporta la riproduzione FairPlay.</span><span class="sxs-lookup"><span data-stu-id="b5c11-199">Azure Media Player doesn’t support FairPlay playback out of the box.</span></span> <span data-ttu-id="b5c11-200">Per poter eseguire la riproduzione FairPlay in MAC OS X, ottenere il lettore di esempio dall'account per sviluppatori di Apple.</span><span class="sxs-lookup"><span data-stu-id="b5c11-200">To get FairPlay playback on MAC OS X, obtain the sample player from the Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="b5c11-201">URL di streaming</span><span class="sxs-lookup"><span data-stu-id="b5c11-201">Streaming URLs</span></span>
<span data-ttu-id="b5c11-202">Se l'asset è stato crittografato con più soluzioni DRM, è necessario usare un tag di crittografia nell'URL di streaming (format='m3u8-aapl', encryption='xxx').</span><span class="sxs-lookup"><span data-stu-id="b5c11-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in the streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="b5c11-203">Si applicano le considerazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5c11-203">The following considerations apply:</span></span>

* <span data-ttu-id="b5c11-204">Può essere specificato solo un tipo di crittografia oppure nessuno.</span><span class="sxs-lookup"><span data-stu-id="b5c11-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="b5c11-205">Il tipo di crittografia non deve essere specificato nell'URL se all'asset è stata applicata una sola crittografia.</span><span class="sxs-lookup"><span data-stu-id="b5c11-205">The encryption type doesn't have to be specified in the URL if only one encryption was applied to the asset.</span></span>
* <span data-ttu-id="b5c11-206">Il tipo di crittografia non fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="b5c11-206">The encryption type is case insensitive.</span></span>
* <span data-ttu-id="b5c11-207">Possono essere specificati i seguenti tipi di crittografia:</span><span class="sxs-lookup"><span data-stu-id="b5c11-207">The following encryption types can be specified:</span></span>  
  * <span data-ttu-id="b5c11-208">**cenc**: crittografia comune (PlayReady o Widevine)</span><span class="sxs-lookup"><span data-stu-id="b5c11-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="b5c11-209">**cbcs-aapl**: FairPlay</span><span class="sxs-lookup"><span data-stu-id="b5c11-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="b5c11-210">**cbc**: crittografia busta AES</span><span class="sxs-lookup"><span data-stu-id="b5c11-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="b5c11-211">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b5c11-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="b5c11-212">Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b5c11-212">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="b5c11-213">Aggiungere gli elementi seguenti alla sezione **appSettings** definita nel file app.config:</span><span class="sxs-lookup"><span data-stu-id="b5c11-213">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="b5c11-214">Esempio</span><span class="sxs-lookup"><span data-stu-id="b5c11-214">Example</span></span>

<span data-ttu-id="b5c11-215">L'esempio seguente illustra la funzionalità che consente di usare Servizi multimediali per distribuire contenuto crittografato con FairPlay.</span><span class="sxs-lookup"><span data-stu-id="b5c11-215">The following sample demonstrates the ability to use Media Services to deliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="b5c11-216">Questa funzionalità è stata introdotta in Azure Media Services SDK for .NET, versione 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="b5c11-216">This functionality was introduced in the Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="b5c11-217">Sovrascrivere il codice nel file Program.cs con il codice riportato in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="b5c11-217">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="b5c11-218">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="b5c11-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="b5c11-219">Usare lo stesso ID criterio se si usano sempre gli stessi giorni/autorizzazioni di accesso, come nel cado di criteri per i localizzatori che devono rimanere attivi per molto tempo (criteri di non caricamento).</span><span class="sxs-lookup"><span data-stu-id="b5c11-219">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="b5c11-220">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="b5c11-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="b5c11-221">Assicurarsi di aggiornare le variabili in modo da puntare alle cartelle in cui si trovano i file di input.</span><span class="sxs-lookup"><span data-stu-id="b5c11-221">Make sure to update variables to point to folders where your input files are located.</span></span>

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
        // Read values from the App.config file.
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
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on the the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
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

            // Associate the key with the asset.
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

            // Associate the content key authorization policy with the content key.
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

            // Associate the content key authorization policy with the content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with the cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound to a real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key to generate the response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating the .pfx file.
            string pfxPassword = "<customer password for creating the .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key to generate the response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match the iv in the asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify the .pfx file created by the customer.
            var appCert = new X509Certificate2("path to the .pfx file created by the customer", pfxPassword, X509KeyStorageFlags.Exportable);

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

            // Get the FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // The reason the below code replaces "https://" with "skd://" is because
            // in the IOS player sample code which you obtained in Apple developer account,
            // the player only recognizes a Key URL that starts with skd://.
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

            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets the streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator to the streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL to the manifest file.
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


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="b5c11-222">Passaggi successivi: Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="b5c11-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b5c11-223">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="b5c11-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
