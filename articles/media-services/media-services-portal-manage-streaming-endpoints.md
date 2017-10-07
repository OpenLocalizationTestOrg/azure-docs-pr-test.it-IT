---
title: gli endpoint con hello portale di Azure di streaming aaaManage | Documenti Microsoft
description: Questo argomento viene illustrato come endpoint di streaming toomanage con hello portale di Azure.
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="f2ba5-103">Gestire gli endpoint di streaming con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f2ba5-103">Manage streaming endpoints with hello Azure portal</span></span>

<span data-ttu-id="f2ba5-104">Questo argomento viene illustrato come toouse hello gli endpoint di streaming toomanage portale Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-104">This topic shows  how toouse hello Azure portal toomanage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="f2ba5-105">Verificare che hello tooreview [Panoramica](media-services-streaming-endpoints-overview.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="f2ba5-106">Per informazioni su come tooscale hello endpoint di streaming, vedere [questo](media-services-portal-scale-streaming-endpoints.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-106">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="f2ba5-107">Iniziare a gestire gli endpoint di streaming</span><span class="sxs-lookup"><span data-stu-id="f2ba5-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="f2ba5-108">Gestione endpoint di streaming per il tuo account, toostart hello seguente.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-108">toostart managing streaming endpoints for your account, do hello following.</span></span>

1. <span data-ttu-id="f2ba5-109">In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-109">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="f2ba5-110">In hello **impostazioni** pannello seleziona **gli endpoint di Streaming**.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-110">In hello **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![endpoint di streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="f2ba5-112">Il costo verrà addebitato solo quando StreamingEndpoint è in stato di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="f2ba5-113">Aggiungere o eliminare un endpoint di streaming</span><span class="sxs-lookup"><span data-stu-id="f2ba5-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="f2ba5-114">Impossibile eliminare l'endpoint di streaming predefinito di Hello.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-114">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="f2ba5-115">tooadd/eliminazione tramite endpoint di streaming hello portale di Azure, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="f2ba5-115">tooadd/delete streaming endpoint using hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="f2ba5-116">tooadd un endpoint di streaming, fare clic su hello **+ Endpoint** nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-116">tooadd a streaming endpoint, click hello **+ Endpoint** at hello top of hello page.</span></span> 

    <span data-ttu-id="f2ba5-117">Più endpoint di Streaming è necessario se si prevede di toohave CDN diversa o una rete CDN e l'accesso diretto.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-117">You might want multiple Streaming Endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="f2ba5-118">Premere un endpoint di streaming, toodelete **eliminare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-118">toodelete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="f2ba5-119">Fare clic su hello **avviare** hello toostart pulsante endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-119">Click hello **Start** button toostart hello streaming endpoint.</span></span>
   
    ![endpoint di streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="f2ba5-121"><a id="configure_streaming_endpoints"></a>Configurazione di Endpoint di Streaming hello</span><span class="sxs-lookup"><span data-stu-id="f2ba5-121"><a id="configure_streaming_endpoints"></a>Configuring hello Streaming Endpoint</span></span>
<span data-ttu-id="f2ba5-122">Endpoint di streaming consente hello tooconfigure le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="f2ba5-122">Streaming Endpoint enables you tooconfigure hello following properties:</span></span>

* <span data-ttu-id="f2ba5-123">Controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="f2ba5-123">Access control</span></span>
* <span data-ttu-id="f2ba5-124">Controllo cache</span><span class="sxs-lookup"><span data-stu-id="f2ba5-124">Cache control</span></span>
* <span data-ttu-id="f2ba5-125">Criteri di accesso tra siti</span><span class="sxs-lookup"><span data-stu-id="f2ba5-125">Cross site access policies</span></span>

<span data-ttu-id="f2ba5-126">Per informazioni dettagliate su queste proprietà, vedere [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="f2ba5-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="f2ba5-127">È possibile configurare l'endpoint di streaming eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="f2ba5-127">You can configure streaming endpoint by doing hello following:</span></span>

1. <span data-ttu-id="f2ba5-128">Selezionare hello desiderato tooconfigure endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-128">Select hello streaming endpoint you want tooconfigure.</span></span>
2. <span data-ttu-id="f2ba5-129">Fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-129">Click **Settings**.</span></span>

<span data-ttu-id="f2ba5-130">Di seguito una breve descrizione dei campi hello.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-130">A brief description of hello fields follows.</span></span>

![endpoint di streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="f2ba5-132">Criteri massima della cache: durata cache tooconfigure utilizzati per gli asset serviti tramite questo endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-132">Maximum cache policy: used tooconfigure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="f2ba5-133">Se è impostato alcun valore, viene usato predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-133">If no value is set, hello default is used.</span></span> <span data-ttu-id="f2ba5-134">i valori predefiniti di Hello possono anche essere definiti direttamente nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-134">hello default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="f2ba5-135">Se la rete CDN Azure è abilitata per hello endpoint di streaming, non è necessario impostare tooless di valore dei criteri della cache hello di 600 secondi.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-135">If Azure CDN is enabled for hello streaming endpoint, you should not set hello cache policy value tooless than 600 seconds.</span></span>  
2. <span data-ttu-id="f2ba5-136">Indirizzi IP consentiti: gli indirizzi IP toospecify che sia possibile usare tooconnect toohello pubblicati endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-136">Allowed IP addresses: used toospecify IP addresses that would be allowed tooconnect toohello published streaming endpoint.</span></span> <span data-ttu-id="f2ba5-137">Se nessun indirizzo IP specificato, qualsiasi indirizzo IP sarebbe in grado di tooconnect.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-137">If no IP addresses specified, any IP address would be able tooconnect.</span></span> <span data-ttu-id="f2ba5-138">È possibile specificare gli indirizzi IP come un singolo indirizzo IP (ad esempio "10.0.0.1"), un intervallo IP con un indirizzo IP e una subnet mask CIDR (ad esempio "10.0.0.1/22") o un intervallo IP con un indirizzo IP e una subnet mask decimale puntata (ad esempio "10.0.0.1(255.255.255.0)").</span><span class="sxs-lookup"><span data-stu-id="f2ba5-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="f2ba5-139">Configurazione per l'autenticazione dell'intestazione firma Akamai: utilizzato toospecify configurazione richiesta di autenticazione intestazione firma dai server Akamai.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-139">Configuration for Akamai signature header authentication: used toospecify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="f2ba5-140">La scadenza è in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="f2ba5-141">Scalabilità dell'endpoint di streaming Premium</span><span class="sxs-lookup"><span data-stu-id="f2ba5-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="f2ba5-142">Per altre informazioni, vedere [questo](media-services-portal-scale-streaming-endpoints.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="f2ba5-143"><a id="enable_cdn"></a>Abilitare l'integrazione della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="f2ba5-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="f2ba5-144">Quando si crea un nuovo account, l'integrazione della rete CDN di Azure dell'endpoint di streaming predefinita viene abilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="f2ba5-145">Se in seguito si abilita toodisable/hello CDN, l'endpoint di streaming deve essere in hello **arrestato** stato.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-145">If you later want toodisable/enable hello CDN, your streaming endpoint must be in hello **stopped** state.</span></span> <span data-ttu-id="f2ba5-146">Potrebbero richiedere alcune ore too2 per hello rete CDN di Azure integration tooget abilitata e per hello modifiche toobe active tra tutti hello POP della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-146">It could take up too2 hours for hello Azure CDN integration tooget enabled and for hello changes toobe active across all hello CDN POPs.</span></span> <span data-ttu-id="f2ba5-147">Tuttavia, è possibile avviare l'endpoint di streaming e flusso senza interruzioni da endpoint di streaming hello e una volta completato l'integrazione di hello, flusso hello verrà fornito da hello CDN.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-147">However, your can start your streaming endpoint and stream without interruptions from hello streaming endpoint and once hello integration is complete, hello stream will be delivered from hello CDN.</span></span> <span data-ttu-id="f2ba5-148">Durante il periodo di provisioning hello sarà l'endpoint di streaming in **avvio** e non è possibile osservare degredad prestazioni.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-148">During hello provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="f2ba5-149">Integrazione della rete CDN è abilitata in tutte le aree Goverment Federal ed execpt di centri dati di Azure hello Cina.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-149">CDN integration is enabled in all hello Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="f2ba5-150">Una volta attivato, hello **controllo di accesso**, **nome host personalizzato** e **autenticazione della firma Akamai** configurazione Ottiene disabilitata.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-150">Once it is enabled, hello **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="f2ba5-151">L'integrazione di Servizi multimediali di Azure con la rete CDN di Azure è implementata nella **rete CDN di Azure da Verizon** per gli endpoint di streaming standard.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="f2ba5-152">Gli endpoint di streaming Premium possono essere configurati usando tutti **i provider e i livelli di prezzo della rete CDN di Azure**.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="f2ba5-153">Per ulteriori informazioni sulle funzionalità di rete CDN di Azure, vedere hello [Panoramica della rete CDN](../cdn/cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f2ba5-153">For more information about Azure CDN features, see hello [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="f2ba5-154">Considerazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f2ba5-154">Additional considerations</span></span>

* <span data-ttu-id="f2ba5-155">Quando rete CDN è abilitata per un endpoint di streaming, i client non è possibile richiedere contenuto direttamente dall'origine di hello.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from hello origin.</span></span> <span data-ttu-id="f2ba5-156">Se è necessario hello possibilità tootest i contenuti con o senza rete CDN, è possibile creare un altro endpoint di streaming che non è abilitata CDN.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-156">If you need hello ability tootest your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="f2ba5-157">I flusso rimane hostname endpoint hello uguale dopo l'abilitazione della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-157">Your streaming endpoint hostname remains hello same after enabling CDN.</span></span> <span data-ttu-id="f2ba5-158">Non è necessario toomake qualsiasi flusso di lavoro servizi di supporto tooyour di modifiche dopo aver abilitata la rete CDN.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-158">You don’t need toomake any changes tooyour media services workflow after CDN is enabled.</span></span> <span data-ttu-id="f2ba5-159">Ad esempio, se il nome host dell'endpoint di streaming è strasbourg.streaming.mediaservices.windows.net, dopo l'abilitazione della rete CDN, hello esatta stesso nome host viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, hello exact same hostname is used.</span></span>
* <span data-ttu-id="f2ba5-160">Per i nuovi endpoint di streaming, è possibile abilitare CDN semplicemente creando un nuovo endpoint; per gli endpoint di streaming esistenti, è necessario endpoint hello di arresto toofirst e quindi abilitare o disabilitare hello CDN.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need toofirst stop hello endpoint and then enable/disable hello CDN.</span></span>
* <span data-ttu-id="f2ba5-161">L'endpoint di streaming standard può essere configurato solo tramite **il provider della rete CDN Standard di Verizon** nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="f2ba5-162">Tuttavia, è possibile abilitare altri provider della rete CDN di Azure usando le API REST.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="f2ba5-163">Configurazione del profilo della rete CDN</span><span class="sxs-lookup"><span data-stu-id="f2ba5-163">Configure CDN profile</span></span>

<span data-ttu-id="f2ba5-164">È possibile configurare il profilo CDN hello selezionando hello **gestire CDN** pulsante dall'alto hello.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-164">You can configure hello CDN profile by selecting hello **Manage CDN** button from hello top.</span></span>

![endpoint di streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="f2ba5-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f2ba5-166">Next steps</span></span>
<span data-ttu-id="f2ba5-167">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="f2ba5-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f2ba5-168">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="f2ba5-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

