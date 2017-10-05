---
title: Gestire gli endpoint di streaming con il portale di Azure | Microsoft Docs
description: Questo argomento illustra come gestire gli endpoint di streaming mediante il portale di Azure.
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
ms.openlocfilehash: 797dced6c3e2525730afa29987259cb9b435ba66
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="30538-103">Gestire gli endpoint di streaming con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="30538-103">Manage streaming endpoints with the Azure portal</span></span>

<span data-ttu-id="30538-104">L'argomento illustra come usare il Portale di Azure per gestire gli endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="30538-104">This topic shows  how to use the Azure portal to manage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="30538-105">Assicurarsi di rivedere l'argomento sulla [panoramica](media-services-streaming-endpoints-overview.md).</span><span class="sxs-lookup"><span data-stu-id="30538-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="30538-106">Per informazioni su come ridimensionare l'endpoint di streaming, vedere [questo](media-services-portal-scale-streaming-endpoints.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="30538-106">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="30538-107">Iniziare a gestire gli endpoint di streaming</span><span class="sxs-lookup"><span data-stu-id="30538-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="30538-108">Per iniziare a gestire gli endpoint di streaming per l'account, procedere come segue.</span><span class="sxs-lookup"><span data-stu-id="30538-108">To start managing streaming endpoints for your account, do the following.</span></span>

1. <span data-ttu-id="30538-109">Nel [portale di Azure ](https://portal.azure.com/) selezionare l'account Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="30538-109">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="30538-110">Nel pannello **Impostazioni** selezionare **Endpoint di streaming**.</span><span class="sxs-lookup"><span data-stu-id="30538-110">In the **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![endpoint di streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="30538-112">Il costo verrà addebitato solo quando StreamingEndpoint è in stato di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="30538-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="30538-113">Aggiungere o eliminare un endpoint di streaming</span><span class="sxs-lookup"><span data-stu-id="30538-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="30538-114">Gli endpoint di streaming predefiniti non possono essere eliminati.</span><span class="sxs-lookup"><span data-stu-id="30538-114">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="30538-115">Per aggiungere o eliminare gli endpoint di streaming tramite il portale di Azure, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="30538-115">To add/delete streaming endpoint using the Azure portal, do the following:</span></span>

1. <span data-ttu-id="30538-116">Per aggiungere un endpoint di streaming, fare clic su **+ Endpoint** nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="30538-116">To add a streaming endpoint, click the **+ Endpoint** at the top of the page.</span></span> 

    <span data-ttu-id="30538-117">Se si prevedono più reti CDN o una rete CDN e l'accesso diretto, potrebbero essere necessari più endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="30538-117">You might want multiple Streaming Endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="30538-118">Per eliminare un endpoint di streaming, fare clic sul pulsante **Elimina** .</span><span class="sxs-lookup"><span data-stu-id="30538-118">To delete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="30538-119">Fare clic sul pulsante **Avvia** per avviare l'endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="30538-119">Click the **Start** button to start the streaming endpoint.</span></span>
   
    ![endpoint di streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="30538-121"><a id="configure_streaming_endpoints"></a>Configurare l'endpoint di streaming</span><span class="sxs-lookup"><span data-stu-id="30538-121"><a id="configure_streaming_endpoints"></a>Configuring the Streaming Endpoint</span></span>
<span data-ttu-id="30538-122">L'endpoint di streaming consente di configurare le seguenti proprietà:</span><span class="sxs-lookup"><span data-stu-id="30538-122">Streaming Endpoint enables you to configure the following properties:</span></span>

* <span data-ttu-id="30538-123">Controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="30538-123">Access control</span></span>
* <span data-ttu-id="30538-124">Controllo cache</span><span class="sxs-lookup"><span data-stu-id="30538-124">Cache control</span></span>
* <span data-ttu-id="30538-125">Criteri di accesso tra siti</span><span class="sxs-lookup"><span data-stu-id="30538-125">Cross site access policies</span></span>

<span data-ttu-id="30538-126">Per informazioni dettagliate su queste proprietà, vedere [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="30538-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="30538-127">È possibile configurare un endpoint di streaming eseguendo le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="30538-127">You can configure streaming endpoint by doing the following:</span></span>

1. <span data-ttu-id="30538-128">Selezionare l'endpoint di streaming che si desidera configurare.</span><span class="sxs-lookup"><span data-stu-id="30538-128">Select the streaming endpoint you want to configure.</span></span>
2. <span data-ttu-id="30538-129">Fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="30538-129">Click **Settings**.</span></span>

<span data-ttu-id="30538-130">Seguirà una breve descrizione dei campi.</span><span class="sxs-lookup"><span data-stu-id="30538-130">A brief description of the fields follows.</span></span>

![endpoint di streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="30538-132">Criteri della cache massima: consente di configurare la durata della cache per gli asset serviti tramite questo endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="30538-132">Maximum cache policy: used to configure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="30538-133">Se non si imposta alcun valore, viene usato il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="30538-133">If no value is set, the default is used.</span></span> <span data-ttu-id="30538-134">I valori predefiniti possono anche essere definiti direttamente in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="30538-134">The default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="30538-135">Se la rete CDN di Azure è abilitata per l'endpoint di streaming, non impostare il valore dei criteri della cache a meno di 600 secondi.</span><span class="sxs-lookup"><span data-stu-id="30538-135">If Azure CDN is enabled for the streaming endpoint, you should not set the cache policy value to less than 600 seconds.</span></span>  
2. <span data-ttu-id="30538-136">Indirizzi IP consentiti: consente di specificare gli indirizzi IP che possono connettersi all'endpoint di streaming pubblicato.</span><span class="sxs-lookup"><span data-stu-id="30538-136">Allowed IP addresses: used to specify IP addresses that would be allowed to connect to the published streaming endpoint.</span></span> <span data-ttu-id="30538-137">Se non viene specificato alcun indirizzo IP, la connessione è consentita a qualsiasi indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="30538-137">If no IP addresses specified, any IP address would be able to connect.</span></span> <span data-ttu-id="30538-138">È possibile specificare gli indirizzi IP come un singolo indirizzo IP (ad esempio "10.0.0.1"), un intervallo IP con un indirizzo IP e una subnet mask CIDR (ad esempio "10.0.0.1/22") o un intervallo IP con un indirizzo IP e una subnet mask decimale puntata (ad esempio "10.0.0.1(255.255.255.0)").</span><span class="sxs-lookup"><span data-stu-id="30538-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="30538-139">Configurazione per l'autenticazione dell'intestazione firma Akamai: consente di specificare la configurazione della richiesta di autenticazione intestazione firma proveniente dai server Akamai.</span><span class="sxs-lookup"><span data-stu-id="30538-139">Configuration for Akamai signature header authentication: used to specify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="30538-140">La scadenza è in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="30538-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="30538-141">Scalabilità dell'endpoint di streaming Premium</span><span class="sxs-lookup"><span data-stu-id="30538-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="30538-142">Per altre informazioni, vedere [questo](media-services-portal-scale-streaming-endpoints.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="30538-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="30538-143"><a id="enable_cdn"></a>Abilitare l'integrazione della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="30538-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="30538-144">Quando si crea un nuovo account, l'integrazione della rete CDN di Azure dell'endpoint di streaming predefinita viene abilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="30538-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="30538-145">Se in seguito si desidera disabilitare o abilitare la rete CDN, l'endpoint di streaming deve essere nello stato **interrotto**.</span><span class="sxs-lookup"><span data-stu-id="30538-145">If you later want to disable/enable the CDN, your streaming endpoint must be in the **stopped** state.</span></span> <span data-ttu-id="30538-146">L'abilitazione dell'integrazione della rete CDN di Azure e l'attivazione delle modifiche in tutti i POP della rete CDN potrebbero richiedere fino a due ore.</span><span class="sxs-lookup"><span data-stu-id="30538-146">It could take up to 2 hours for the Azure CDN integration to get enabled and for the changes to be active across all the CDN POPs.</span></span> <span data-ttu-id="30538-147">Tuttavia, è possibile avviare l'endpoint di streaming e il flusso senza interruzioni dall'endpoint di streaming e dopo aver completato l'integrazione, il flusso verrà distribuito dalla rete CDN.</span><span class="sxs-lookup"><span data-stu-id="30538-147">However, your can start your streaming endpoint and stream without interruptions from the streaming endpoint and once the integration is complete, the stream will be delivered from the CDN.</span></span> <span data-ttu-id="30538-148">Durante il periodo di provisioning l'endpoint di streaming è nello stato **avvio** ed è possibile osservarne le prestazioni ridotte.</span><span class="sxs-lookup"><span data-stu-id="30538-148">During the provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="30538-149">L'integrazione della rete CDN è abilitata in tutti i centri dati di Azure ad eccezione della Cina e delle aree con governi federali.</span><span class="sxs-lookup"><span data-stu-id="30538-149">CDN integration is enabled in all the Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="30538-150">Dopo essere stata attivata, la configurazione di **Controllo di accesso**, **Nome host personalizzato** e **Autenticazione firma Akamai** viene disabilitata.</span><span class="sxs-lookup"><span data-stu-id="30538-150">Once it is enabled, the **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="30538-151">L'integrazione di Servizi multimediali di Azure con la rete CDN di Azure è implementata nella **rete CDN di Azure da Verizon** per gli endpoint di streaming standard.</span><span class="sxs-lookup"><span data-stu-id="30538-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="30538-152">Gli endpoint di streaming Premium possono essere configurati usando tutti **i provider e i livelli di prezzo della rete CDN di Azure**.</span><span class="sxs-lookup"><span data-stu-id="30538-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="30538-153">Per altre informazioni sulle funzionalità della rete CDN di Azure, vedere la [Panoramica della rete per la distribuzione di contenuti (rete CDN) di Azure](../cdn/cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="30538-153">For more information about Azure CDN features, see the [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="30538-154">Considerazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="30538-154">Additional considerations</span></span>

* <span data-ttu-id="30538-155">Quando la rete CDN è abilitata per un endpoint di streaming, i client non possono richiedere il contenuto direttamente dall'origine.</span><span class="sxs-lookup"><span data-stu-id="30538-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from the origin.</span></span> <span data-ttu-id="30538-156">Se è necessario testare il contenuto con o senza la rete CDN, è possibile creare un altro endpoint di streaming per la rete CDN.</span><span class="sxs-lookup"><span data-stu-id="30538-156">If you need the ability to test your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="30538-157">Il nome host dell'endpoint di streaming rimane invariato dopo l'abilitazione della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="30538-157">Your streaming endpoint hostname remains the same after enabling CDN.</span></span> <span data-ttu-id="30538-158">Non è necessario apportare modifiche al flusso di lavoro di Servizi multimediali dopo l'abilitazione della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="30538-158">You don’t need to make any changes to your media services workflow after CDN is enabled.</span></span> <span data-ttu-id="30538-159">Ad esempio, se il nome host dell'endpoint di streaming è strasbourg.streaming.mediaservices.windows.net, dopo avere abilitato la rete CDN, viene usato lo stesso identico nome host.</span><span class="sxs-lookup"><span data-stu-id="30538-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, the exact same hostname is used.</span></span>
* <span data-ttu-id="30538-160">Per i nuovi endpoint di streaming, è possibile abilitare la rete CDN semplicemente creando un nuovo endpoint. Per gli endpoint di streaming esistenti, è necessario arrestare prima l'endpoint e quindi abilitare/disabilitare la rete CDN.</span><span class="sxs-lookup"><span data-stu-id="30538-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need to first stop the endpoint and then enable/disable the CDN.</span></span>
* <span data-ttu-id="30538-161">L'endpoint di streaming standard può essere configurato solo tramite **il provider della rete CDN Standard di Verizon** nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="30538-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="30538-162">Tuttavia, è possibile abilitare altri provider della rete CDN di Azure usando le API REST.</span><span class="sxs-lookup"><span data-stu-id="30538-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="30538-163">Configurazione del profilo della rete CDN</span><span class="sxs-lookup"><span data-stu-id="30538-163">Configure CDN profile</span></span>

<span data-ttu-id="30538-164">È possibile configurare il profilo della rete CDN selezionando il pulsante **Gestisci rete CDN** nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="30538-164">You can configure the CDN profile by selecting the **Manage CDN** button from the top.</span></span>

![endpoint di streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="30538-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="30538-166">Next steps</span></span>
<span data-ttu-id="30538-167">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="30538-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="30538-168">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="30538-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

