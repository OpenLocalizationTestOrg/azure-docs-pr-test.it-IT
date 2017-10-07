---
title: dinamica AES-128 aaaUsing crittografia e la chiave di servizio di recapito | Documenti Microsoft
description: Servizi multimediali di Microsoft Azure consente di toodeliver il contenuto crittografato con chiavi di crittografia AES a 128 bit. Servizi multimediali fornisce anche i servizi di distribuzione delle chiavi hello che offre agli utenti di tooauthorized le chiavi di crittografia. Questo argomento viene illustrato come toodynamically crittografare con AES-128 e utilizzare il servizio di distribuzione delle chiavi di hello.
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
ms.openlocfilehash: cb1b413ec2ba79f7437464099cf72236ab93f312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a><span data-ttu-id="7f33c-105">Uso della crittografia dinamica AES-128 e del servizio di distribuzione delle chiavi</span><span class="sxs-lookup"><span data-stu-id="7f33c-105">Using AES-128 dynamic encryption and key delivery service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f33c-106">.NET</span><span class="sxs-lookup"><span data-stu-id="7f33c-106">.NET</span></span>](media-services-protect-with-aes128.md)
> * [<span data-ttu-id="7f33c-107">Java</span><span class="sxs-lookup"><span data-stu-id="7f33c-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="7f33c-108">PHP</span><span class="sxs-lookup"><span data-stu-id="7f33c-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="7f33c-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7f33c-109">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="7f33c-110">Vedere [questo](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video per una panoramica delle modalità tooprotect il supporto del contenuto con crittografia AES.</span><span class="sxs-lookup"><span data-stu-id="7f33c-110">See [this](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video for an overview of how tooprotect your Media Content with AES encryption.</span></span>
> 
> 

<span data-ttu-id="7f33c-111">Servizi multimediali di Microsoft Azure consente toodeliver Http Live Streaming (HLS) e Smooth Streams crittografato con Advanced Encryption Standard (AES) (utilizzando le chiavi di crittografia a 128 bit).</span><span class="sxs-lookup"><span data-stu-id="7f33c-111">Microsoft Azure Media Services enables you toodeliver Http-Live-Streaming (HLS) and Smooth Streams encrypted with Advanced Encryption Standard (AES) (using 128-bit encryption keys).</span></span> <span data-ttu-id="7f33c-112">Servizi multimediali fornisce anche i servizi di distribuzione delle chiavi hello che offre agli utenti di tooauthorized le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="7f33c-112">Media Services also provides hello Key Delivery service that delivers encryption keys tooauthorized users.</span></span> <span data-ttu-id="7f33c-113">Se si desidera per servizi multimediali tooencrypt un asset, è necessario tooassociate una chiave di crittografia con asset hello e inoltre configurare criteri di autorizzazione per la chiave di hello.</span><span class="sxs-lookup"><span data-stu-id="7f33c-113">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key with hello asset and also configure authorization policies for hello key.</span></span> <span data-ttu-id="7f33c-114">Quando un flusso è richiesto da un lettore, servizi multimediali Usa hello specificato toodynamically chiave crittografare il contenuto usando la crittografia AES.</span><span class="sxs-lookup"><span data-stu-id="7f33c-114">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES encryption.</span></span> <span data-ttu-id="7f33c-115">flusso di hello toodecrypt, hello lettore richiederà chiave hello dal servizio di distribuzione delle chiavi hello.</span><span class="sxs-lookup"><span data-stu-id="7f33c-115">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="7f33c-116">Se è o meno utente hello toodecide autorizzato chiave hello tooget, servizio hello valuta i criteri di autorizzazione hello specificato per la chiave di hello.</span><span class="sxs-lookup"><span data-stu-id="7f33c-116">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="7f33c-117">Servizi multimediali supporta più modalità di autenticazione degli utenti che eseguono richieste di chiavi.</span><span class="sxs-lookup"><span data-stu-id="7f33c-117">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="7f33c-118">Hello criteri di autorizzazione chiave contenuto potrebbero avere una o più restrizioni di autorizzazione: apertura o la limitazione del token.</span><span class="sxs-lookup"><span data-stu-id="7f33c-118">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="7f33c-119">criteri con restrizione token Hello devono essere accompagnato da un token rilasciato da un servizio (token di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="7f33c-119">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="7f33c-120">Servizi multimediali supporta i token in hello [token Web semplici](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) formato (SWT) e [Token Web JSON](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) formato (JWT).</span><span class="sxs-lookup"><span data-stu-id="7f33c-120">Media Services supports tokens in hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="7f33c-121">Per ulteriori informazioni, vedere [configurare criteri di autorizzazione della chiave simmetrica hello](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="7f33c-121">For more information, see [Configure hello content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span>

<span data-ttu-id="7f33c-122">Il vantaggio di tootake di crittografia dinamica, è necessario toohave un asset che contiene un set di file MP4 a più velocità in bit o file di origine Smooth Streaming con più velocità in bit.</span><span class="sxs-lookup"><span data-stu-id="7f33c-122">tootake advantage of dynamic encryption, you need toohave an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="7f33c-123">È inoltre necessario criteri di distribuzione hello tooconfigure per asset hello (descritta più avanti in questo argomento).</span><span class="sxs-lookup"><span data-stu-id="7f33c-123">You also need tooconfigure hello delivery policy for hello asset (described later in this topic).</span></span> <span data-ttu-id="7f33c-124">Quindi, basato sul formato di hello specificato nell'URL di streaming hello, il server di Streaming On Demand hello garantisce che tale flusso hello venga distribuito nel protocollo hello scelto.</span><span class="sxs-lookup"><span data-stu-id="7f33c-124">Then, based on hello format specified in hello streaming URL, hello On-Demand Streaming server will ensure that hello stream is delivered in hello protocol you have chosen.</span></span> <span data-ttu-id="7f33c-125">Di conseguenza, è necessario solo toostore e pagare per i file hello in unico formato di archiviazione e servizi multimediali creerà e fornirà hello risposta appropriata in base alle richieste da un client.</span><span class="sxs-lookup"><span data-stu-id="7f33c-125">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="7f33c-126">In questo argomento sarebbe utile toodevelopers di applicazioni che distribuiscono contenuti multimediali protetti.</span><span class="sxs-lookup"><span data-stu-id="7f33c-126">This topic would be useful toodevelopers that work on applications that deliver protected media.</span></span> <span data-ttu-id="7f33c-127">Hello argomento viene illustrato come tooconfigure hello del servizio di distribuzione delle chiavi con criteri di autorizzazione in modo che solo i client autorizzati potrebbero ricevere le chiavi di crittografia hello.</span><span class="sxs-lookup"><span data-stu-id="7f33c-127">hello topic shows you how tooconfigure hello key delivery service with authorization policies so that only authorized clients could receive hello encryption keys.</span></span> <span data-ttu-id="7f33c-128">Viene inoltre illustrato come la crittografia dinamica toouse.</span><span class="sxs-lookup"><span data-stu-id="7f33c-128">It also shows how toouse dynamic encryption.</span></span>


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a><span data-ttu-id="7f33c-129">Flusso di lavoro della crittografia dinamica AES-128 e servizio di distribuzione delle chiavi</span><span class="sxs-lookup"><span data-stu-id="7f33c-129">AES-128 Dynamic Encryption and Key Delivery Service Workflow</span></span>

<span data-ttu-id="7f33c-130">di seguito Hello sono passaggi generali che è necessario tooperform per crittografare gli asset con AES, tramite servizio di distribuzione delle chiavi di servizi multimediali hello e anche utilizzando la crittografia dinamica.</span><span class="sxs-lookup"><span data-stu-id="7f33c-130">hello following are general steps that you would need tooperform when encrypting your assets with AES, using hello Media Services key delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="7f33c-131">[Creare un asset e caricare i file nell'asset hello](media-services-protect-with-aes128.md#create_asset).</span><span class="sxs-lookup"><span data-stu-id="7f33c-131">[Create an asset and upload files into hello asset](media-services-protect-with-aes128.md#create_asset).</span></span>
2. <span data-ttu-id="7f33c-132">[Codificare asset hello contenente hello file toohello adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span><span class="sxs-lookup"><span data-stu-id="7f33c-132">[Encode hello asset containing hello file toohello adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span></span>
3. <span data-ttu-id="7f33c-133">[Creare una chiave simmetrica e associarlo all'asset codificato hello](media-services-protect-with-aes128.md#create_contentkey).</span><span class="sxs-lookup"><span data-stu-id="7f33c-133">[Create a content key and associate it with hello encoded asset](media-services-protect-with-aes128.md#create_contentkey).</span></span> <span data-ttu-id="7f33c-134">In servizi multimediali, la chiave simmetrica hello contiene la chiave di crittografia dell'asset hello.</span><span class="sxs-lookup"><span data-stu-id="7f33c-134">In Media Services, hello content key contains hello asset’s encryption key.</span></span>
4. <span data-ttu-id="7f33c-135">[Configurare i criteri di autorizzazione della chiave simmetrica hello](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="7f33c-135">[Configure hello content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span> <span data-ttu-id="7f33c-136">criteri di autorizzazione chiave del contenuto Hello devono essere configurato dall'utente e soddisfatti dal client hello affinché hello contenuto toobe chiave toohello recapitato client.</span><span class="sxs-lookup"><span data-stu-id="7f33c-136">hello content key authorization policy must be configured by you and met by hello client in order for hello content key toobe delivered toohello client.</span></span>
5. <span data-ttu-id="7f33c-137">[Configurare i criteri di distribuzione hello per un asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span><span class="sxs-lookup"><span data-stu-id="7f33c-137">[Configure hello delivery policy for an asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span></span> <span data-ttu-id="7f33c-138">configurazione dei criteri recapito Hello include: chiave URL di acquisizione e il vettore di inizializzazione (IV) (AES 128 richiede hello stesso vettore di Inizializzazione toobe fornito durante la crittografia e decrittografia), il protocollo di recapito (ad esempio, MPEG DASH, HLS, Smooth Streaming o tutti), hello tipo di crittografia dinamica (ad esempio, envelope o Nessuna crittografia dinamica).</span><span class="sxs-lookup"><span data-stu-id="7f33c-138">hello delivery policy configuration includes: key acquisition URL and Initialization Vector (IV) (AES 128 requires hello same IV toobe supplied when encrypting and decrypting), delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), hello type of dynamic encryption (for example, envelope or no dynamic encryption).</span></span>

    <span data-ttu-id="7f33c-139">È possibile applicare protocollo tooeach criteri diversi in hello stesso asset.</span><span class="sxs-lookup"><span data-stu-id="7f33c-139">You could apply different policy tooeach protocol on hello same asset.</span></span> <span data-ttu-id="7f33c-140">Ad esempio, è possibile applicare PlayReady crittografia tooSmooth/DASH e tooHLS Envelope AES.</span><span class="sxs-lookup"><span data-stu-id="7f33c-140">For example, you could apply PlayReady encryption tooSmooth/DASH and AES Envelope tooHLS.</span></span> <span data-ttu-id="7f33c-141">Tutti i protocolli che non sono definiti in un criterio di recapito (ad esempio, aggiungere un singolo criterio che specifica solo HLS come protocollo di hello) verrà impedito lo streaming.</span><span class="sxs-lookup"><span data-stu-id="7f33c-141">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="7f33c-142">toothis eccezione Hello è se non sono presenti criteri di recapito di asset definito in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="7f33c-142">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="7f33c-143">Quindi, saranno possibile tutti i protocolli in crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="7f33c-143">Then, all protocols will be allowed in hello clear.</span></span>

6. <span data-ttu-id="7f33c-144">[Creare un localizzatore OnDemand](media-services-protect-with-aes128.md#create_locator) in ordine tooget un URL di streaming.</span><span class="sxs-lookup"><span data-stu-id="7f33c-144">[Create an OnDemand locator](media-services-protect-with-aes128.md#create_locator) in order tooget a streaming URL.</span></span>

<span data-ttu-id="7f33c-145">argomento Hello viene inoltre illustrato [come un'applicazione client può richiedere una chiave dal servizio di distribuzione delle chiavi hello](media-services-protect-with-aes128.md#client_request).</span><span class="sxs-lookup"><span data-stu-id="7f33c-145">hello topic also shows [how a client application can request a key from hello key delivery service](media-services-protect-with-aes128.md#client_request).</span></span>

<span data-ttu-id="7f33c-146">Si noterà .NET completo [esempio](media-services-protect-with-aes128.md#example) alla fine di hello di hello argomento.</span><span class="sxs-lookup"><span data-stu-id="7f33c-146">You will find a complete .NET [example](media-services-protect-with-aes128.md#example) at hello end of hello topic.</span></span>

<span data-ttu-id="7f33c-147">Hello seguente immagine illustra del flusso di lavoro hello descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7f33c-147">hello following image demonstrates hello workflow described above.</span></span> <span data-ttu-id="7f33c-148">Token hello qui viene utilizzato per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="7f33c-148">Here hello token is used for authentication.</span></span>

![Proteggere con AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

<span data-ttu-id="7f33c-150">rest Hello di questo argomento fornisce spiegazioni dettagliate, esempi di codice e collegamenti tootopics che mostrano come tooachieve hello attività descritte in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7f33c-150">hello rest of this topic provides detailed explanations, code examples, and links tootopics that show you how tooachieve hello tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="7f33c-151">Limitazioni correnti</span><span class="sxs-lookup"><span data-stu-id="7f33c-151">Current limitations</span></span>
<span data-ttu-id="7f33c-152">Se si aggiungono o si aggiornano i criteri di distribuzione dell'asset, è necessario eliminare l'eventuale localizzatore esistente e creare un nuovo localizzatore.</span><span class="sxs-lookup"><span data-stu-id="7f33c-152">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>

## <span data-ttu-id="7f33c-153"><a id="create_asset"></a>Creare un asset e caricare i file nell'asset hello</span><span class="sxs-lookup"><span data-stu-id="7f33c-153"><a id="create_asset"></a>Create an asset and upload files into hello asset</span></span>
<span data-ttu-id="7f33c-154">In ordine toomanage, codificare e trasmettere in flusso i video, è innanzitutto necessario caricare il contenuto in servizi multimediali di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7f33c-154">In order toomanage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="7f33c-155">Una volta caricato, il contenuto è archiviato in modo sicuro nel cloud hello per un'ulteriore elaborazione e il flusso.</span><span class="sxs-lookup"><span data-stu-id="7f33c-155">Once uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

<span data-ttu-id="7f33c-156">Per informazioni dettagliate, vedere [Carica file in un account di servizi multimediali](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="7f33c-156">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <span data-ttu-id="7f33c-157"><a id="encode_asset"></a>Codificare hello asset contenente hello file toohello velocità in bit adattiva che set MP4</span><span class="sxs-lookup"><span data-stu-id="7f33c-157"><a id="encode_asset"></a>Encode hello asset containing hello file toohello adaptive bitrate MP4 set</span></span>
<span data-ttu-id="7f33c-158">Con la crittografia dinamica è sufficiente toocreate un asset che contiene un set di file MP4 a più velocità in bit o file di origine Smooth Streaming con più velocità in bit.</span><span class="sxs-lookup"><span data-stu-id="7f33c-158">With dynamic encryption all you need is toocreate an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="7f33c-159">Quindi, base hello formato specificato nel manifesto hello o frammentare la richiesta, hello server ti garantisce che il flusso di hello nel protocollo hello che si è scelto di Streaming On Demand.</span><span class="sxs-lookup"><span data-stu-id="7f33c-159">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="7f33c-160">Di conseguenza, è necessario solo toostore e pagare per i file hello in unico formato di archiviazione e servizi multimediali creerà e fornirà hello risposta appropriata in base alle richieste da un client.</span><span class="sxs-lookup"><span data-stu-id="7f33c-160">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span> <span data-ttu-id="7f33c-161">Per ulteriori informazioni, vedere hello [Panoramica della creazione di pacchetti dinamica](media-services-dynamic-packaging-overview.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="7f33c-161">For more information, see hello [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

>[!NOTE]
><span data-ttu-id="7f33c-162">Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato.</span><span class="sxs-lookup"><span data-stu-id="7f33c-162">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="7f33c-163">lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato.</span><span class="sxs-lookup"><span data-stu-id="7f33c-163">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="7f33c-164">Inoltre, toobe toouse in grado di creazione dinamica dei pacchetti e la crittografia dinamica dell'asset deve contenere un set di velocità in bit adattiva MP4s o file Smooth Streaming a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="7f33c-164">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="7f33c-165">Per istruzioni su come tooencode, vedere [come tooencode un asset con Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="7f33c-165">For instructions on how tooencode, see [How tooencode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="7f33c-166"><a id="create_contentkey"></a>Creare una chiave simmetrica e associarlo all'asset codificato hello</span><span class="sxs-lookup"><span data-stu-id="7f33c-166"><a id="create_contentkey"></a>Create a content key and associate it with hello encoded asset</span></span>
<span data-ttu-id="7f33c-167">In servizi multimediali, la chiave simmetrica hello contiene chiave hello che si desidera tooencrypt un asset con.</span><span class="sxs-lookup"><span data-stu-id="7f33c-167">In Media Services, hello content key contains hello key that you want tooencrypt an asset with.</span></span>

<span data-ttu-id="7f33c-168">Per informazioni dettagliate, vedere [Creare una chiave simmetrica](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="7f33c-168">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="7f33c-169"><a id="configure_key_auth_policy"></a>Configurare i criteri di autorizzazione della chiave simmetrica hello</span><span class="sxs-lookup"><span data-stu-id="7f33c-169"><a id="configure_key_auth_policy"></a>Configure hello content key’s authorization policy</span></span>
<span data-ttu-id="7f33c-170">Servizi multimediali supporta più modalità di autenticazione degli utenti che eseguono richieste di chiavi.</span><span class="sxs-lookup"><span data-stu-id="7f33c-170">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="7f33c-171">criteri di autorizzazione chiave del contenuto Hello devono essere configurato dall'utente e soddisfatti dal client hello (lettore) affinché toobe chiave di hello recapitati toohello client.</span><span class="sxs-lookup"><span data-stu-id="7f33c-171">hello content key authorization policy must be configured by you and met by hello client (player) in order for hello key toobe delivered toohello client.</span></span> <span data-ttu-id="7f33c-172">Hello criteri di autorizzazione chiave contenuto potrebbero avere una o più restrizioni di autorizzazione: aprire, token o restrizioni IP.</span><span class="sxs-lookup"><span data-stu-id="7f33c-172">hello content key authorization policy could have one or more authorization restrictions: open, token restriction, or IP restriction.</span></span>

<span data-ttu-id="7f33c-173">Per informazioni dettagliate, vedere l'argomento [Configurare i criteri di autorizzazione della chiave simmetrica](media-services-dotnet-configure-content-key-auth-policy.md).</span><span class="sxs-lookup"><span data-stu-id="7f33c-173">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md).</span></span>

## <span data-ttu-id="7f33c-174"><a id="configure_asset_delivery_policy"></a>Configurare i criteri di distribuzione dell'asset</span><span class="sxs-lookup"><span data-stu-id="7f33c-174"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="7f33c-175">Configurare i criteri di distribuzione hello dell'asset.</span><span class="sxs-lookup"><span data-stu-id="7f33c-175">Configure hello delivery policy for your asset.</span></span> <span data-ttu-id="7f33c-176">Le operazioni che hello configurazione dei criteri di recapito di asset include:</span><span class="sxs-lookup"><span data-stu-id="7f33c-176">Some things that hello asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="7f33c-177">URL di acquisizione chiave Hello.</span><span class="sxs-lookup"><span data-stu-id="7f33c-177">hello Key acquisition URL.</span></span> 
* <span data-ttu-id="7f33c-178">Hello toouse il vettore di inizializzazione (IV) per la crittografia envelope hello.</span><span class="sxs-lookup"><span data-stu-id="7f33c-178">hello Initialization Vector (IV) toouse for hello envelope encryption.</span></span> <span data-ttu-id="7f33c-179">AES 128 richiede hello stesso vettore di Inizializzazione toobe fornito per la crittografia e decrittografia.</span><span class="sxs-lookup"><span data-stu-id="7f33c-179">AES 128 requires hello same IV toobe supplied when encrypting and decrypting.</span></span> 
* <span data-ttu-id="7f33c-180">Hello asset protocollo di recapito (ad esempio, MPEG DASH, HLS, Smooth Streaming o tutti).</span><span class="sxs-lookup"><span data-stu-id="7f33c-180">hello asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="7f33c-181">tipo di Hello di crittografia dinamica (ad esempio, envelope AES) o Nessuna crittografia dinamica.</span><span class="sxs-lookup"><span data-stu-id="7f33c-181">hello type of dynamic encryption (for example, AES envelope) or no dynamic encryption.</span></span> 

<span data-ttu-id="7f33c-182">Per informazioni dettagliate, vedere [Configurare i criteri di distribuzione degli asset ](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="7f33c-182">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="7f33c-183"><a id="create_locator"></a>Creare un OnDemand streaming locator in ordine tooget un URL di streaming</span><span class="sxs-lookup"><span data-stu-id="7f33c-183"><a id="create_locator"></a>Create an OnDemand streaming locator in order tooget a streaming URL</span></span>
<span data-ttu-id="7f33c-184">Sarà necessario tooprovide l'utente con hello streaming URL per Smooth, DASH o HLS.</span><span class="sxs-lookup"><span data-stu-id="7f33c-184">You will need tooprovide your user with hello streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="7f33c-185">Se si aggiungono o si aggiornano i criteri di distribuzione dell'asset, è necessario eliminare l'eventuale localizzatore esistente e creare un nuovo localizzatore.</span><span class="sxs-lookup"><span data-stu-id="7f33c-185">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
> 
> 

<span data-ttu-id="7f33c-186">Per istruzioni su come toopublish un asset e compilare un URL di streaming, vedere [compilare un URL di streaming](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="7f33c-186">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="7f33c-187">Ottenere un token di test</span><span class="sxs-lookup"><span data-stu-id="7f33c-187">Get a test token</span></span>
<span data-ttu-id="7f33c-188">Ottenere un token di test in base a una restrizione token hello che è stata utilizzata per i criteri di autorizzazione chiave hello.</span><span class="sxs-lookup"><span data-stu-id="7f33c-188">Get a test token based on hello token restriction that was used for hello key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);

<span data-ttu-id="7f33c-189">È possibile utilizzare hello [Player AMS](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest il flusso.</span><span class="sxs-lookup"><span data-stu-id="7f33c-189">You can use hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest your stream.</span></span>

## <span data-ttu-id="7f33c-190"><a id="client_request"></a>Come il client può richiedere una chiave dal servizio di distribuzione delle chiavi hello?</span><span class="sxs-lookup"><span data-stu-id="7f33c-190"><a id="client_request"></a>How can your client request a key from hello key delivery service?</span></span>
<span data-ttu-id="7f33c-191">Nel passaggio precedente hello, è costruito hello URL che punta a file manifesto tooa.</span><span class="sxs-lookup"><span data-stu-id="7f33c-191">In hello previous step, you constructed hello URL that points tooa manifest file.</span></span> <span data-ttu-id="7f33c-192">Il client deve tooextract hello le informazioni necessarie dal flusso dei file manifesti in ordine toomake un servizio di distribuzione delle chiavi toohello richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="7f33c-192">Your client needs tooextract hello necessary information from hello streaming manifest files in order toomake a request toohello key delivery service.</span></span>

### <a name="manifest-files"></a><span data-ttu-id="7f33c-193">File manifesto</span><span class="sxs-lookup"><span data-stu-id="7f33c-193">Manifest files</span></span>
<span data-ttu-id="7f33c-194">client di Hello deve tooextract hello URL (che contiene anche la chiave simmetrica (kid) Id) del valore dal file manifesto hello.</span><span class="sxs-lookup"><span data-stu-id="7f33c-194">hello client needs tooextract hello URL (that also contains content key Id (kid)) value from hello manifest file.</span></span> <span data-ttu-id="7f33c-195">client Hello tenterà quindi chiave di crittografia tooget hello dal servizio di distribuzione delle chiavi hello.</span><span class="sxs-lookup"><span data-stu-id="7f33c-195">hello client will then try tooget hello encryption key from hello key delivery service.</span></span> <span data-ttu-id="7f33c-196">Hello client deve inoltre tooextract valore di hello IV e usarlo per decrittografare stream.hello hello seguente frammento di codice mostra hello <Protection> elemento del manifesto Smooth Streaming hello.</span><span class="sxs-lookup"><span data-stu-id="7f33c-196">hello client also needs tooextract hello IV value and use it do decrypt hello stream.hello following snippet shows hello <Protection> element of hello Smooth Streaming manifest.</span></span>

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

<span data-ttu-id="7f33c-197">Nel caso di hello di HLS, manifesto radice hello viene suddiviso in file di segmenti.</span><span class="sxs-lookup"><span data-stu-id="7f33c-197">In hello case of HLS, hello root manifest is broken into segment files.</span></span> 

<span data-ttu-id="7f33c-198">Ad esempio, manifesto radice hello è: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) e contiene un elenco di nomi di file di segmento.</span><span class="sxs-lookup"><span data-stu-id="7f33c-198">For example, hello root manifest is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) and it contains a list of segment file names.</span></span>

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

<span data-ttu-id="7f33c-199">Se si apre uno dei file di segmento hello nell'editor di testo (ad esempio, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contenere #EXT-X-KEY, che indica che file hello è crittografato.</span><span class="sxs-lookup"><span data-stu-id="7f33c-199">If you open one of hello segment files in text editor (for example, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contain #EXT-X-KEY which indicates that hello file is encrypted.</span></span>

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
><span data-ttu-id="7f33c-200">Se si intende tooplay un AES crittografata HLS in Safari, vedere [questo blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="7f33c-200">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

### <a name="request-hello-key-from-hello-key-delivery-service"></a><span data-ttu-id="7f33c-201">Richiedi chiave di hello dal servizio di distribuzione delle chiavi hello</span><span class="sxs-lookup"><span data-stu-id="7f33c-201">Request hello key from hello key delivery service</span></span>

<span data-ttu-id="7f33c-202">Hello codice seguente viene illustrato come toosend toohello una richiesta di servizi multimediali della chiave del servizio di recapito utilizzando un Uri (che è stato estratto dal manifesto hello) di recapito e un token (in questo argomento non è descritto come tooget token Web semplice da un servizio Token di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="7f33c-202">hello following code shows how toosend a request toohello Media Services key delivery service using a key delivery Uri (that was extracted from hello manifest) and a token (this topic does not talk about how tooget Simple Web Tokens from a Secure Token Service).</span></span>

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

## <a name="protect-your-content-with-aes-128-using-net"></a><span data-ttu-id="7f33c-203">Proteggere i contenuti con AES-128 tramite .NET</span><span class="sxs-lookup"><span data-stu-id="7f33c-203">Protect your content with AES-128 using .NET</span></span>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="7f33c-204">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7f33c-204">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="7f33c-205">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="7f33c-205">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="7f33c-206">Aggiungere i seguenti elementi troppo hello**appSettings** definiti nel file app. config:</span><span class="sxs-lookup"><span data-stu-id="7f33c-206">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <span data-ttu-id="7f33c-207"><a id="example"></a>Esempio</span><span class="sxs-lookup"><span data-stu-id="7f33c-207"><a id="example"></a>Example</span></span>

<span data-ttu-id="7f33c-208">Sovrascrivere il codice hello nel file Program.cs con il codice di hello illustrato in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="7f33c-208">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>
 
>[!NOTE]
><span data-ttu-id="7f33c-209">È previsto un limite di 1.000.000 di criteri per i diversi criteri AMS (ad esempio per i criteri Locator o ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="7f33c-209">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="7f33c-210">È consigliabile utilizzare hello stesso ID di criteri, se si utilizza sempre hello stesso giorni accesso le autorizzazioni, ad esempio, i criteri per i localizzatori che sono previsti tooremain sul posto per un lungo periodo (non-caricamento criteri).</span><span class="sxs-lookup"><span data-stu-id="7f33c-210">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="7f33c-211">Per altre informazioni, vedere [questo](media-services-dotnet-manage-entities.md#limit-access-policies) argomento.</span><span class="sxs-lookup"><span data-stu-id="7f33c-211">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="7f33c-212">Rendere le variabili tooupdate che toopoint toofolders in cui si trovano i file di input.</span><span class="sxs-lookup"><span data-stu-id="7f33c-212">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

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
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing hello issuer of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // hello Audience or Scope of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
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
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
            //so you have tooadd it in front of hello token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello bit.ly/aesplayer Flash player tootest hello URL 
            // (with open authorization policy). 
            // Paste hello URL and click hello Update button tooplay hello video. 
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
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
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

            // Associate hello key with hello asset.
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

            // Add ContentKeyAutorizationPolicy tooContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
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

            // Add ContentKeyAutorizationPolicy tooContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

            return tokenTemplateString;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose tooassociate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in hello key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  hello URL does not contains a key ID

            // hello following policy configuration specifies: 
            // key url that will have KID=<Guid> appended toohello envelope and
            // hello Initialization Vector (IV) toouse for hello envelope encryption.

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

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
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


## <a name="media-services-learning-paths"></a><span data-ttu-id="7f33c-213">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="7f33c-213">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7f33c-214">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="7f33c-214">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

