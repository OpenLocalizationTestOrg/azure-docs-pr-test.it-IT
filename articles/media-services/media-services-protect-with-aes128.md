---
title: Uso della crittografia dinamica AES-128 e del servizio di distribuzione delle chiavi | Microsoft Docs
description: Servizi multimediali di Microsoft Azure consente di distribuire contenuti crittografati con AES mediante chiavi di crittografia a 128 bit. Servizi multimediali fornisce anche il servizio di distribuzione chiavi che distribuisce chiavi di crittografia agli utenti autorizzati. In questo argomento viene illustrato come crittografare con AES-128 e utilizzare il servizio di distribuzione delle chiavi in modo dinamico.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: ae1b36c26e688e74eb8fcc1a4cdbd3be0c014c08
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a><span data-ttu-id="d51e4-105">Uso della crittografia dinamica AES-128 e del servizio di distribuzione delle chiavi</span><span class="sxs-lookup"><span data-stu-id="d51e4-105">Using AES-128 dynamic encryption and key delivery service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d51e4-106">.NET</span><span class="sxs-lookup"><span data-stu-id="d51e4-106">.NET</span></span>](media-services-protect-with-aes128.md)
> * [<span data-ttu-id="d51e4-107">Java</span><span class="sxs-lookup"><span data-stu-id="d51e4-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="d51e4-108">PHP</span><span class="sxs-lookup"><span data-stu-id="d51e4-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="d51e4-109">Overview</span><span class="sxs-lookup"><span data-stu-id="d51e4-109">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="d51e4-110">Vedere [questo](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video per una panoramica di come proteggere il contenuto multimediale con la crittografia AES.</span><span class="sxs-lookup"><span data-stu-id="d51e4-110">See [this](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video for an overview of how to protect your Media Content with AES encryption.</span></span>
> 
> 

<span data-ttu-id="d51e4-111">Servizi multimediali di Microsoft Azure consente di distribuire Http-Live-Streaming (HLS) e Smooth Streams crittografati con AES (Advanced Encryption Standard) mediante chiavi di crittografia a 128 bit.</span><span class="sxs-lookup"><span data-stu-id="d51e4-111">Microsoft Azure Media Services enables you to deliver Http-Live-Streaming (HLS) and Smooth Streams encrypted with Advanced Encryption Standard (AES) (using 128-bit encryption keys).</span></span> <span data-ttu-id="d51e4-112">Servizi multimediali fornisce anche il servizio di distribuzione chiavi che distribuisce chiavi di crittografia agli utenti autorizzati.</span><span class="sxs-lookup"><span data-stu-id="d51e4-112">Media Services also provides the Key Delivery service that delivers encryption keys to authorized users.</span></span> <span data-ttu-id="d51e4-113">Per consentire a Servizi multimediali di crittografare un asset, è necessario associare una chiave di crittografia all'asset e configurare anche i criteri di autorizzazione per la chiave.</span><span class="sxs-lookup"><span data-stu-id="d51e4-113">If you want for Media Services to encrypt an asset, you need to associate an encryption key with the asset and also configure authorization policies for the key.</span></span> <span data-ttu-id="d51e4-114">Quando un flusso viene richiesto da un lettore, Servizi multimediali usa la chiave specificata per crittografare dinamicamente i contenuti mediante AES.</span><span class="sxs-lookup"><span data-stu-id="d51e4-114">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES encryption.</span></span> <span data-ttu-id="d51e4-115">Per decrittografare il flusso, il lettore richiederà la chiave dal servizio di distribuzione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="d51e4-115">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="d51e4-116">Per decidere se l'utente è autorizzato a ottenere la chiave, il servizio valuta i criteri di autorizzazione specificati.</span><span class="sxs-lookup"><span data-stu-id="d51e4-116">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="d51e4-117">Servizi multimediali supporta più modalità di autenticazione degli utenti che eseguono richieste di chiavi.</span><span class="sxs-lookup"><span data-stu-id="d51e4-117">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="d51e4-118">I criteri di autorizzazione delle chiavi simmetriche possono avere una o più restrizioni di tipo Open o Token.</span><span class="sxs-lookup"><span data-stu-id="d51e4-118">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="d51e4-119">I criteri con restrizione Token devono essere accompagnati da un token rilasciato da un servizio STS (Secure Token Service, servizio token di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="d51e4-119">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="d51e4-120">Servizi multimediali supporta i token nei formati [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) e [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT).</span><span class="sxs-lookup"><span data-stu-id="d51e4-120">Media Services supports tokens in the [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="d51e4-121">Per altre informazioni, vedere l'argomento [Configurare i criteri di autorizzazione della chiave simmetrica](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="d51e4-121">For more information, see [Configure the content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span>

<span data-ttu-id="d51e4-122">Per sfruttare la crittografia dinamica, è necessario disporre di un asset che contenga un set di file MP4 con velocità in bit multipla o di file di origine Smooth Streaming con velocità in bit multipla.</span><span class="sxs-lookup"><span data-stu-id="d51e4-122">To take advantage of dynamic encryption, you need to have an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="d51e4-123">È inoltre necessario configurare i criteri di distribuzione dell'asset (descritti più avanti in questo argomento).</span><span class="sxs-lookup"><span data-stu-id="d51e4-123">You also need to configure the delivery policy for the asset (described later in this topic).</span></span> <span data-ttu-id="d51e4-124">Quindi, in base al formato specificato nell'URL del flusso, il server di streaming on demand garantirà che il flusso sia distribuito nel protocollo scelto.</span><span class="sxs-lookup"><span data-stu-id="d51e4-124">Then, based on the format specified in the streaming URL, the On-Demand Streaming server will ensure that the stream is delivered in the protocol you have chosen.</span></span> <span data-ttu-id="d51e4-125">Di conseguenza, si archiviano e si pagano solo i file in un singolo formato di archiviazione e il servizio Servizi multimediali crea e fornisce la risposta appropriata in base alle richieste di un client.</span><span class="sxs-lookup"><span data-stu-id="d51e4-125">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="d51e4-126">Questo argomento potrebbe essere utile per gli sviluppatori che utilizzano applicazioni che forniscono contenuti protetti.</span><span class="sxs-lookup"><span data-stu-id="d51e4-126">This topic would be useful to developers that work on applications that deliver protected media.</span></span> <span data-ttu-id="d51e4-127">L'argomento illustra come configurare il servizio di distribuzione delle chiavi con criteri di autorizzazione, in modo che solo i client autorizzati possano ricevere le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="d51e4-127">The topic shows you how to configure the key delivery service with authorization policies so that only authorized clients could receive the encryption keys.</span></span> <span data-ttu-id="d51e4-128">Viene inoltre illustrato come utilizzare la crittografia dinamica.</span><span class="sxs-lookup"><span data-stu-id="d51e4-128">It also shows how to use dynamic encryption.</span></span>


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a><span data-ttu-id="d51e4-129">Flusso di lavoro della crittografia dinamica AES-128 e servizio di distribuzione delle chiavi</span><span class="sxs-lookup"><span data-stu-id="d51e4-129">AES-128 Dynamic Encryption and Key Delivery Service Workflow</span></span>

<span data-ttu-id="d51e4-130">Di seguito sono indicati i passaggi generali da eseguire quando si esegue la crittografia degli asset con AES, tramite il servizio di distribuzione delle chiavi di Servizi multimediali e tramite la crittografia dinamica.</span><span class="sxs-lookup"><span data-stu-id="d51e4-130">The following are general steps that you would need to perform when encrypting your assets with AES, using the Media Services key delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="d51e4-131">[Creare un asset e caricare file nell'asset](media-services-protect-with-aes128.md#create_asset).</span><span class="sxs-lookup"><span data-stu-id="d51e4-131">[Create an asset and upload files into the asset](media-services-protect-with-aes128.md#create_asset).</span></span>
2. <span data-ttu-id="d51e4-132">[Codificare l'asset contenente il file per il set di file MP4 con velocità in bit adattiva](media-services-protect-with-aes128.md#encode_asset).</span><span class="sxs-lookup"><span data-stu-id="d51e4-132">[Encode the asset containing the file to the adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span></span>
3. <span data-ttu-id="d51e4-133">[Creare una chiave simmetrica e associarla all'asset codificato](media-services-protect-with-aes128.md#create_contentkey).</span><span class="sxs-lookup"><span data-stu-id="d51e4-133">[Create a content key and associate it with the encoded asset](media-services-protect-with-aes128.md#create_contentkey).</span></span> <span data-ttu-id="d51e4-134">In Servizi multimediali, la chiave simmetrica contiene la chiave di crittografia dell'asset.</span><span class="sxs-lookup"><span data-stu-id="d51e4-134">In Media Services, the content key contains the asset’s encryption key.</span></span>
4. <span data-ttu-id="d51e4-135">[Configurare i criteri di autorizzazione della chiave simmetrica](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="d51e4-135">[Configure the content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span> <span data-ttu-id="d51e4-136">I criteri di autorizzazione della chiave simmetrica devono essere configurati dall'utente e soddisfatti dal client affinché la chiave simmetrica possa essere distribuita al client.</span><span class="sxs-lookup"><span data-stu-id="d51e4-136">The content key authorization policy must be configured by you and met by the client in order for the content key to be delivered to the client.</span></span>
5. <span data-ttu-id="d51e4-137">[Configurare i criteri di distribuzione di un asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span><span class="sxs-lookup"><span data-stu-id="d51e4-137">[Configure the delivery policy for an asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span></span> <span data-ttu-id="d51e4-138">La configurazione dei criteri di distribuzione include: l'URL di acquisizione della chiave e il vettore di inizializzazione, AES 128 richiede che venga fornito lo stesso vettore di inizializzazione per la crittografia e la decrittografia; il protocollo di recapito, ad esempio MPEG-DASH, HLS, Smooth Streaming o tutti; il tipo di crittografia dinamica, ad esempio envelope o nessuna crittografia dinamica.</span><span class="sxs-lookup"><span data-stu-id="d51e4-138">The delivery policy configuration includes: key acquisition URL and Initialization Vector (IV) (AES 128 requires the same IV to be supplied when encrypting and decrypting), delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), the type of dynamic encryption (for example, envelope or no dynamic encryption).</span></span>

    <span data-ttu-id="d51e4-139">È possibile applicare criteri diversi per ogni protocollo allo stesso asset.</span><span class="sxs-lookup"><span data-stu-id="d51e4-139">You could apply different policy to each protocol on the same asset.</span></span> <span data-ttu-id="d51e4-140">Ad esempio, è possibile applicare la crittografia PlayReady a Smooth/DASH e AES Envelope ad HLS.</span><span class="sxs-lookup"><span data-stu-id="d51e4-140">For example, you could apply PlayReady encryption to Smooth/DASH and AES Envelope to HLS.</span></span> <span data-ttu-id="d51e4-141">Gli eventuali protocolli non definiti nei criteri di distribuzione (ad esempio quando si aggiunge un singolo criterio che specifica soltanto HLS come protocollo) verranno esclusi dallo streaming.</span><span class="sxs-lookup"><span data-stu-id="d51e4-141">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="d51e4-142">Questo comportamento non si verifica quando non è presente alcun criterio di distribuzione degli asset.</span><span class="sxs-lookup"><span data-stu-id="d51e4-142">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="d51e4-143">In tal caso, sono consentiti tutti i protocolli in chiaro.</span><span class="sxs-lookup"><span data-stu-id="d51e4-143">Then, all protocols will be allowed in the clear.</span></span>

6. <span data-ttu-id="d51e4-144">[Creare un localizzatore OnDemand](media-services-protect-with-aes128.md#create_locator) per ottenere un URL di streaming.</span><span class="sxs-lookup"><span data-stu-id="d51e4-144">[Create an OnDemand locator](media-services-protect-with-aes128.md#create_locator) in order to get a streaming URL.</span></span>

<span data-ttu-id="d51e4-145">L’argomento inoltre indica [come un'applicazione client può richiedere una chiave dal servizio di distribuzione delle chiavi](media-services-protect-with-aes128.md#client_request).</span><span class="sxs-lookup"><span data-stu-id="d51e4-145">The topic also shows [how a client application can request a key from the key delivery service](media-services-protect-with-aes128.md#client_request).</span></span>

<span data-ttu-id="d51e4-146">Si noterà un [esempio](media-services-protect-with-aes128.md#example) .NET completo alla fine dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="d51e4-146">You will find a complete .NET [example](media-services-protect-with-aes128.md#example) at the end of the topic.</span></span>

<span data-ttu-id="d51e4-147">Nell'immagine seguente viene illustrato il flusso di lavoro descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d51e4-147">The following image demonstrates the workflow described above.</span></span> <span data-ttu-id="d51e4-148">Di seguito viene utilizzato il token per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="d51e4-148">Here the token is used for authentication.</span></span>

![Proteggere con AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

<span data-ttu-id="d51e4-150">Nella parte rimanente di questo argomento vengono fornite spiegazioni dettagliate, esempi di codice e collegamenti ad argomenti che illustrano come eseguire le attività descritte in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d51e4-150">The rest of this topic provides detailed explanations, code examples, and links to topics that show you how to achieve the tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="d51e4-151">Limitazioni correnti</span><span class="sxs-lookup"><span data-stu-id="d51e4-151">Current limitations</span></span>
<span data-ttu-id="d51e4-152">Se si aggiungono o si aggiornano i criteri di distribuzione dell'asset, è necessario eliminare l'eventuale localizzatore esistente e creare un nuovo localizzatore.</span><span class="sxs-lookup"><span data-stu-id="d51e4-152">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>

## <span data-ttu-id="d51e4-153"><a id="create_asset"></a>Creare un asset e caricare file nell'asset</span><span class="sxs-lookup"><span data-stu-id="d51e4-153"><a id="create_asset"></a>Create an asset and upload files into the asset</span></span>
<span data-ttu-id="d51e4-154">Per gestire, codificare e trasmettere i video, è innanzitutto necessario caricare il contenuto in Servizi multimediali di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d51e4-154">In order to manage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="d51e4-155">Dopo aver caricato i file, i contenuti vengono archiviati in modo sicuro nel cloud per altre operazioni di elaborazione e streaming.</span><span class="sxs-lookup"><span data-stu-id="d51e4-155">Once uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> 

<span data-ttu-id="d51e4-156">Per informazioni dettagliate, vedere [Carica file in un account di servizi multimediali](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="d51e4-156">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <span data-ttu-id="d51e4-157"><a id="encode_asset"></a>Codificare l'asset contenente il file per il set di file MP4 con velocità in bit adattiva</span><span class="sxs-lookup"><span data-stu-id="d51e4-157"><a id="encode_asset"></a>Encode the asset containing the file to the adaptive bitrate MP4 set</span></span>
<span data-ttu-id="d51e4-158">Con la crittografia dinamica, è necessario solamente creare un asset che contenga un set di file MP4 con velocità in bit multipla o di file di origine Smooth Streaming con velocità in bit multipla.</span><span class="sxs-lookup"><span data-stu-id="d51e4-158">With dynamic encryption all you need is to create an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="d51e4-159">In base al formato specificato nella richiesta del manifesto o del frammento, il server di streaming on demand garantirà che il flusso sia ricevuto nel protocollo scelto.</span><span class="sxs-lookup"><span data-stu-id="d51e4-159">Then, based on the specified format in the manifest or fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="d51e4-160">Di conseguenza, si archiviano e si pagano solo i file in un singolo formato di archiviazione e il servizio Servizi multimediali crea e fornisce la risposta appropriata in base alle richieste di un client.</span><span class="sxs-lookup"><span data-stu-id="d51e4-160">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span> <span data-ttu-id="d51e4-161">Per altre informazioni, vedere l'argomento [Creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="d51e4-161">For more information, see the [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

>[!NOTE]
><span data-ttu-id="d51e4-162">Quando l'account AMS viene creato, un endpoint di streaming **predefinito** viene aggiunto all'account con stato **Arrestato**.</span><span class="sxs-lookup"><span data-stu-id="d51e4-162">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="d51e4-163">Per avviare lo streaming del contenuto e sfruttare i vantaggi della creazione dinamica dei pacchetti e della crittografia dinamica, l'endpoint di streaming da cui si vuole trasmettere il contenuto deve essere nello stato **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="d51e4-163">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="d51e4-164">Per usare la creazione dinamica dei pacchetti e la crittografia dinamica, l'asset deve contenere un set di file MP4 o Smooth Streaming a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="d51e4-164">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="d51e4-165">Per istruzioni su come eseguire la codifica, vedere [Come codificare un asset mediante Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="d51e4-165">For instructions on how to encode, see [How to encode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="d51e4-166"><a id="create_contentkey"></a>Creare una chiave simmetrica e associarla all'asset codificato</span><span class="sxs-lookup"><span data-stu-id="d51e4-166"><a id="create_contentkey"></a>Create a content key and associate it with the encoded asset</span></span>
<span data-ttu-id="d51e4-167">In Servizi multimediali, la chiave simmetrica contiene la chiave con cui si desidera crittografare un asset.</span><span class="sxs-lookup"><span data-stu-id="d51e4-167">In Media Services, the content key contains the key that you want to encrypt an asset with.</span></span>

<span data-ttu-id="d51e4-168">Per informazioni dettagliate, vedere [Creare una chiave simmetrica](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="d51e4-168">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="d51e4-169"><a id="configure_key_auth_policy"></a>Configurare i criteri di autorizzazione della chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="d51e4-169"><a id="configure_key_auth_policy"></a>Configure the content key’s authorization policy</span></span>
<span data-ttu-id="d51e4-170">Servizi multimediali supporta più modalità di autenticazione degli utenti che eseguono richieste di chiavi.</span><span class="sxs-lookup"><span data-stu-id="d51e4-170">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="d51e4-171">I criteri di autorizzazione della chiave simmetrica devono essere configurati dall'utente e soddisfatti dal client (lettore) affinché la chiave possa essere distribuita al client.</span><span class="sxs-lookup"><span data-stu-id="d51e4-171">The content key authorization policy must be configured by you and met by the client (player) in order for the key to be delivered to the client.</span></span> <span data-ttu-id="d51e4-172">I criteri di autorizzazione delle chiavi simmetriche possono avere una o più restrizioni di tipo Open, Token o IP.</span><span class="sxs-lookup"><span data-stu-id="d51e4-172">The content key authorization policy could have one or more authorization restrictions: open, token restriction, or IP restriction.</span></span>

<span data-ttu-id="d51e4-173">Per informazioni dettagliate, vedere l'argomento [Configurare i criteri di autorizzazione della chiave simmetrica](media-services-dotnet-configure-content-key-auth-policy.md).</span><span class="sxs-lookup"><span data-stu-id="d51e4-173">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md).</span></span>

## <span data-ttu-id="d51e4-174"><a id="configure_asset_delivery_policy"></a>Configurare i criteri di distribuzione dell'asset</span><span class="sxs-lookup"><span data-stu-id="d51e4-174"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="d51e4-175">Configurare i criteri di distribuzione dell'asset.</span><span class="sxs-lookup"><span data-stu-id="d51e4-175">Configure the delivery policy for your asset.</span></span> <span data-ttu-id="d51e4-176">Alcuni aspetti inclusi nella configurazione dei criteri di distribuzione dell’asset:</span><span class="sxs-lookup"><span data-stu-id="d51e4-176">Some things that the asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="d51e4-177">URL di acquisizione della chiave.</span><span class="sxs-lookup"><span data-stu-id="d51e4-177">The Key acquisition URL.</span></span> 
* <span data-ttu-id="d51e4-178">Vettore di inizializzazione (IV) da utilizzare per la crittografia envelope.</span><span class="sxs-lookup"><span data-stu-id="d51e4-178">The Initialization Vector (IV) to use for the envelope encryption.</span></span> <span data-ttu-id="d51e4-179">AES 128 richiede che venga fornito lo stesso IV per la crittografia e la decrittografia.</span><span class="sxs-lookup"><span data-stu-id="d51e4-179">AES 128 requires the same IV to be supplied when encrypting and decrypting.</span></span> 
* <span data-ttu-id="d51e4-180">Il protocollo di recapito dell'asset (ad esempio, MPEG DASH, HLS, Smooth Streaming o tutti).</span><span class="sxs-lookup"><span data-stu-id="d51e4-180">The asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="d51e4-181">Il tipo di crittografia dinamica (ad esempio, envelope AES) o nessuna crittografia dinamica.</span><span class="sxs-lookup"><span data-stu-id="d51e4-181">The type of dynamic encryption (for example, AES envelope) or no dynamic encryption.</span></span> 

<span data-ttu-id="d51e4-182">Per informazioni dettagliate, vedere [Configurare i criteri di distribuzione degli asset ](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="d51e4-182">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="d51e4-183"><a id="create_locator"></a>Creare un localizzatore di streaming on demand per ottenere un URL di streaming</span><span class="sxs-lookup"><span data-stu-id="d51e4-183"><a id="create_locator"></a>Create an OnDemand streaming locator in order to get a streaming URL</span></span>
<span data-ttu-id="d51e4-184">È necessario fornire all'utente l'URL del flusso per Smooth, DASH o HLS.</span><span class="sxs-lookup"><span data-stu-id="d51e4-184">You will need to provide your user with the streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="d51e4-185">Se si aggiungono o si aggiornano i criteri di distribuzione dell'asset, è necessario eliminare l'eventuale localizzatore esistente e creare un nuovo localizzatore.</span><span class="sxs-lookup"><span data-stu-id="d51e4-185">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
> 
> 

<span data-ttu-id="d51e4-186">Per istruzioni su come pubblicare un asset e creare un URL di streaming, vedere la sezione [Creare URL di streaming](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="d51e4-186">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="d51e4-187">Ottenere un token di test</span><span class="sxs-lookup"><span data-stu-id="d51e4-187">Get a test token</span></span>
<span data-ttu-id="d51e4-188">Ottenere un token di test basato sulla restrizione Token usata per i criteri di autorizzazione della chiave.</span><span class="sxs-lookup"><span data-stu-id="d51e4-188">Get a test token based on the token restriction that was used for the key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the data in the given TokenRestrictionTemplate.
    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);

<span data-ttu-id="d51e4-189">È possibile utilizzare il [lettore AMS](http://amsplayer.azurewebsites.net/azuremediaplayer.html) per testare il flusso.</span><span class="sxs-lookup"><span data-stu-id="d51e4-189">You can use the [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to test your stream.</span></span>

## <span data-ttu-id="d51e4-190"><a id="client_request"></a>In che modo il client può richiedere una chiave dal servizio di distribuzione delle chiavi?</span><span class="sxs-lookup"><span data-stu-id="d51e4-190"><a id="client_request"></a>How can your client request a key from the key delivery service?</span></span>
<span data-ttu-id="d51e4-191">Nel passaggio precedente, è stato realizzato l'URL che punta a un file manifesto.</span><span class="sxs-lookup"><span data-stu-id="d51e4-191">In the previous step, you constructed the URL that points to a manifest file.</span></span> <span data-ttu-id="d51e4-192">Il client deve estrarre le informazioni necessarie dai file manifesto del flusso per effettuare una richiesta al servizio di distribuzione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="d51e4-192">Your client needs to extract the necessary information from the streaming manifest files in order to make a request to the key delivery service.</span></span>

### <a name="manifest-files"></a><span data-ttu-id="d51e4-193">File manifesto</span><span class="sxs-lookup"><span data-stu-id="d51e4-193">Manifest files</span></span>
<span data-ttu-id="d51e4-194">Il client deve estrarre il valore URL (che contiene anche l’ID della chiave simmetrica (kid)) dal file manifesto.</span><span class="sxs-lookup"><span data-stu-id="d51e4-194">The client needs to extract the URL (that also contains content key Id (kid)) value from the manifest file.</span></span> <span data-ttu-id="d51e4-195">Il client tenterà quindi di ottenere la chiave di crittografia dal servizio di distribuzione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="d51e4-195">The client will then try to get the encryption key from the key delivery service.</span></span> <span data-ttu-id="d51e4-196">Inoltre, il client deve estrarre il valore IV e utilizzarlo per decrittografare il flusso. Il frammento di codice seguente illustra l’elemento <Protection> del manifesto Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="d51e4-196">The client also needs to extract the IV value and use it do decrypt the stream.The following snippet shows the <Protection> element of the Smooth Streaming manifest.</span></span>

    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>

<span data-ttu-id="d51e4-197">Nel caso di HLS, il manifesto radice viene suddiviso in file di segmento.</span><span class="sxs-lookup"><span data-stu-id="d51e4-197">In the case of HLS, the root manifest is broken into segment files.</span></span> 

<span data-ttu-id="d51e4-198">Ad esempio, il manifesto radice è: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) e contiene un elenco di nomi di file di segmento.</span><span class="sxs-lookup"><span data-stu-id="d51e4-198">For example, the root manifest is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) and it contains a list of segment file names.</span></span>

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

<span data-ttu-id="d51e4-199">Se si apre uno dei file del segmento nell'editor di testo (ad esempio, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), deve essere presente #EXT-X-KEY che indica che il file è crittografato.</span><span class="sxs-lookup"><span data-stu-id="d51e4-199">If you open one of the segment files in text editor (for example, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contain #EXT-X-KEY which indicates that the file is encrypted.</span></span>

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
><span data-ttu-id="d51e4-200">Se si prevede di eseguire un flusso HLS crittografato con AES in Safari, vedere [questo blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="d51e4-200">If you are planning to play an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

### <a name="request-the-key-from-the-key-delivery-service"></a><span data-ttu-id="d51e4-201">Richiedere la chiave dal servizio di distribuzione delle chiavi</span><span class="sxs-lookup"><span data-stu-id="d51e4-201">Request the key from the key delivery service</span></span>

<span data-ttu-id="d51e4-202">Il codice seguente indica come inviare una richiesta al servizio di distribuzione delle chiavi di Servizi multimediali utilizzando un Uri di distribuzione della chiave (che è stato estratto dal manifesto) e un token (in questo argomento non viene discusso come ottenere token Web semplici da un servizio Secure Token).</span><span class="sxs-lookup"><span data-stu-id="d51e4-202">The following code shows how to send a request to the Media Services key delivery service using a key delivery Uri (that was extracted from the manifest) and a token (this topic does not talk about how to get Simple Web Tokens from a Secure Token Service).</span></span>

    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }

## <a name="protect-your-content-with-aes-128-using-net"></a><span data-ttu-id="d51e4-203">Proteggere i contenuti con AES-128 tramite .NET</span><span class="sxs-lookup"><span data-stu-id="d51e4-203">Protect your content with AES-128 using .NET</span></span>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d51e4-204">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d51e4-204">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="d51e4-205">Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d51e4-205">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="d51e4-206">Aggiungere i seguenti elementi alla sezione **appSettings** definita nel file app.config:</span><span class="sxs-lookup"><span data-stu-id="d51e4-206">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <span data-ttu-id="d51e4-207"><a id="example"></a>Esempio</span><span class="sxs-lookup"><span data-stu-id="d51e4-207"><a id="example"></a>Example</span></span>

<span data-ttu-id="d51e4-208">Sovrascrivere il codice nel file Program.cs con il codice riportato in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="d51e4-208">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>
 
>[!NOTE]
><span data-ttu-id="d51e4-209">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="d51e4-209">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="d51e4-210">Usare lo stesso ID criterio se si usano sempre gli stessi giorni/autorizzazioni di accesso, come nel cado di criteri per i localizzatori che devono rimanere attivi per molto tempo (criteri di non caricamento).</span><span class="sxs-lookup"><span data-stu-id="d51e4-210">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="d51e4-211">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="d51e4-211">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="d51e4-212">Assicurarsi di aggiornare le variabili in modo da puntare alle cartelle in cui si trovano i file di input.</span><span class="sxs-lookup"><span data-stu-id="d51e4-212">Make sure to update variables to point to folders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace AESDynamicEncryptionAndKeyDeliverySvc
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing the issuer of the token.  
        // Must match the value in the token for the token to be considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // The Audience or Scope of the token.  
        // Must match the value in the token for the token to be considered valid.
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

            IContentKey key = CreateEnvelopeTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //The GenerateTestToken method returns the token without the word “Bearer” in front
            //so you have to add it in front of the token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use the bit.ly/aesplayer Flash player to test the URL 
            // (with open authorization policy). 
            // Paste the URL and click the Update button to play the video. 
            //
            string URL = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Smooth Streaming Url: {0}/manifest", URL);
            Console.WriteLine();
            Console.WriteLine("HLS Url: {0}/manifest(format=m3u8-aapl)", URL);
            Console.WriteLine();

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
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.StorageEncrypted);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);


            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
        {
            // Create envelope encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                keyId,
                contentKey,
                "ContentKey",
                ContentKeyType.EnvelopeEncryption);

            // Associate the key with the asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions 
            // and create authorization policy             
            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Open Authorization Policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
            Name = "HLS Open Authorization Policy",
            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
            Requirements = null // no requirements needed for HLS
        };

            restrictions.Add(restriction);

            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            "");

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy to ContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("HLS token restricted authorization policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "Token Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString
            };

            restrictions.Add(restriction);

            //You could have multiple options 
            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "Token option for HLS",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            null  // no key delivery data is needed for HLS
            );

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy to ContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);

            return tokenTemplateString;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose to associate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in the key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  the URL does not contains a key ID

            // The following policy configuration specifies: 
            // key url that will have KID=<Guid> appended to the envelope and
            // the Initialization Vector (IV) to use for the envelope encryption.

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeKeyAcquisitionUrl, keyAcquisitionUri.ToString()}
            };

            IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
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

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int size)
        {
            byte[] randomBytes = new byte[size];
            using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(randomBytes);
            }

            return randomBytes;
        }
        }
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="d51e4-213">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="d51e4-213">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d51e4-214">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="d51e4-214">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

