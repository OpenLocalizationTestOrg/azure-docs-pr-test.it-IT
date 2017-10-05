---
title: Risoluzione dei problemi di compressione di file nella rete CDN di Azure | Microsoft Docs
description: Risolvere i problemi relativi alla compressione di file nella rete CDN di Azure.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5ef8a8262eb40aa827161764f03a63d031e43273
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="e8453-103">Risoluzione dei problemi della compressione dei file CDN</span><span class="sxs-lookup"><span data-stu-id="e8453-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="e8453-104">Questo articolo consente di risolvere i problemi relativi alla [compressione dei file CDN](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="e8453-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="e8453-105">Se in qualsiasi punto dell'articolo sono necessarie altre informazioni, è possibile contattare gli esperti di Azure nei [forum MSDN e overflow dello stack relativi ad Azure](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="e8453-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="e8453-106">In alternativa, è anche possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="e8453-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="e8453-107">Accedere al [sito del Supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e fare clic su **Ottenere supporto**.</span><span class="sxs-lookup"><span data-stu-id="e8453-107">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="e8453-108">Sintomo</span><span class="sxs-lookup"><span data-stu-id="e8453-108">Symptom</span></span>
<span data-ttu-id="e8453-109">La compressione per l'endpoint è abilitata, ma i file vengono restituiti non compressi.</span><span class="sxs-lookup"><span data-stu-id="e8453-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="e8453-110">Per verificare se i file restituiti sono compressi, è necessario usare uno strumento come[Fiddler](http://www.telerik.com/fiddler) o gli [strumenti di sviluppo](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) del browser.</span><span class="sxs-lookup"><span data-stu-id="e8453-110">To check whether your files are being returned compressed, you need to use a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="e8453-111">Verificare le intestazioni della risposta HTTP restituite con il contenuto della rete CDN memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="e8453-111">Check the HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="e8453-112">Se è presente un'intestazione denominata `Content-Encoding` con un valore **gzip**, **bzip2** o **deflate**, il contenuto è compresso.</span><span class="sxs-lookup"><span data-stu-id="e8453-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Intestazione Content-Encoding](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="e8453-114">Causa</span><span class="sxs-lookup"><span data-stu-id="e8453-114">Cause</span></span>
<span data-ttu-id="e8453-115">Le cause possono essere diverse, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e8453-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="e8453-116">Il contenuto richiesto non è idoneo per la compressione.</span><span class="sxs-lookup"><span data-stu-id="e8453-116">The requested content is not eligible for compression.</span></span>
* <span data-ttu-id="e8453-117">La compressione non è abilitata per il tipo di file richiesto.</span><span class="sxs-lookup"><span data-stu-id="e8453-117">Compression is not enabled for the requested file type.</span></span>
* <span data-ttu-id="e8453-118">La richiesta HTTP non include un'intestazione che richiede un tipo di compressione valido.</span><span class="sxs-lookup"><span data-stu-id="e8453-118">The HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="e8453-119">Passaggi per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="e8453-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="e8453-120">Come avviene con la distribuzione di nuovi endpoint, le modifiche alla configurazione della rete CDN richiedono tempo per propagarsi attraverso la rete.</span><span class="sxs-lookup"><span data-stu-id="e8453-120">As with deploying new endpoints, CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="e8453-121">In genere, le modifiche vengono applicate entro 90 minuti.</span><span class="sxs-lookup"><span data-stu-id="e8453-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="e8453-122">Se questa è la prima volta che si configura la compressione per l'endpoint della rete CDN, è consigliabile attendere 1-2 ore per assicurarsi che le impostazioni di compressione impostazioni si siano propagate ai POP.</span><span class="sxs-lookup"><span data-stu-id="e8453-122">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs.</span></span> 
> 
> 

### <a name="verify-the-request"></a><span data-ttu-id="e8453-123">Verificare la richiesta</span><span class="sxs-lookup"><span data-stu-id="e8453-123">Verify the request</span></span>
<span data-ttu-id="e8453-124">Per prima cosa, eseguire una rapida verifica dell'integrità della richiesta.</span><span class="sxs-lookup"><span data-stu-id="e8453-124">First, we should do a quick sanity check on the request.</span></span>  <span data-ttu-id="e8453-125">Per visualizzare le richieste in corso, è possibile usare gli [strumenti per sviluppatori](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) del browser.</span><span class="sxs-lookup"><span data-stu-id="e8453-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) to view the requests being made.</span></span>

* <span data-ttu-id="e8453-126">Verificare che la richiesta venga inviata all'URL dell'endpoint, `<endpointname>.azureedge.net`, non all'origine.</span><span class="sxs-lookup"><span data-stu-id="e8453-126">Verify the request is being sent to your endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="e8453-127">Verificare che la richiesta contenga un'intestazione **Accept-Encoding** e che il valore di tale intestazione contenga **gzip**, **deflate** o **bzip2**.</span><span class="sxs-lookup"><span data-stu-id="e8453-127">Verify the request contains an **Accept-Encoding** header, and the value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="e8453-128">I profili della **rete CDN di Azure fornita da Akamai** supportano solo la codifica **gzip**.</span><span class="sxs-lookup"><span data-stu-id="e8453-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![Intestazioni di richiesta CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="e8453-130">Verificare le impostazioni di compressione (profilo di rete CDN Standard)</span><span class="sxs-lookup"><span data-stu-id="e8453-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="e8453-131">Questo passaggio va eseguito solo se il profilo CDN è un profilo di **rete CDN Standard di Azure fornita da Verizon** o di **rete CDN Standard di Azure fornita da Akamai**.</span><span class="sxs-lookup"><span data-stu-id="e8453-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="e8453-132">Passare all'endpoint nel [portale di Azure](https://portal.azure.com) e fare clic sul pulsante **Configura** .</span><span class="sxs-lookup"><span data-stu-id="e8453-132">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Configure** button.</span></span>

* <span data-ttu-id="e8453-133">Verificare se la compressione è abilitata.</span><span class="sxs-lookup"><span data-stu-id="e8453-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="e8453-134">Verificare che il tipo MIME per il contenuto da comprimere sia incluso nell'elenco dei formati compressi.</span><span class="sxs-lookup"><span data-stu-id="e8453-134">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![Impostazioni di compressione CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="e8453-136">Verificare le impostazioni di compressione (profilo di rete CDN Premium)</span><span class="sxs-lookup"><span data-stu-id="e8453-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="e8453-137">Questo passaggio va eseguito solo se il profilo CDN è un profilo di **rete CDN Premium di Azure fornita da Verizon** .</span><span class="sxs-lookup"><span data-stu-id="e8453-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="e8453-138">Passare all'endpoint nel [portale di Azure](https://portal.azure.com) e fare clic sul pulsante **Gestisci** .</span><span class="sxs-lookup"><span data-stu-id="e8453-138">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Manage** button.</span></span>  <span data-ttu-id="e8453-139">Verrà aperto il portale supplementare.</span><span class="sxs-lookup"><span data-stu-id="e8453-139">The supplemental portal will open.</span></span>  <span data-ttu-id="e8453-140">Passare il puntatore sulla scheda **HTTP Grande**, quindi passare il puntatore sul riquadro a comparsa **Impostazioni della memorizzazione nella cache**.</span><span class="sxs-lookup"><span data-stu-id="e8453-140">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="e8453-141">Fare clic su **Compressione**.</span><span class="sxs-lookup"><span data-stu-id="e8453-141">Click **Compression**.</span></span> 

* <span data-ttu-id="e8453-142">Verificare se la compressione è abilitata.</span><span class="sxs-lookup"><span data-stu-id="e8453-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="e8453-143">Verificare che l'elenco dei **Tipi di file** contenga un elenco di tipi MIME delimitati da virgole (senza spazi).</span><span class="sxs-lookup"><span data-stu-id="e8453-143">Verify the **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="e8453-144">Verificare che il tipo MIME per il contenuto da comprimere sia incluso nell'elenco dei formati compressi.</span><span class="sxs-lookup"><span data-stu-id="e8453-144">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![Impostazioni di compressione CDN premium](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-the-content-is-cached"></a><span data-ttu-id="e8453-146">Verificare che il contenuto venga memorizzato nella cache</span><span class="sxs-lookup"><span data-stu-id="e8453-146">Verify the content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="e8453-147">Questo passaggio va eseguito solo se il profilo CDN è un profilo di **rete CDN di Azure fornita da Verizon** (Standard o Premium).</span><span class="sxs-lookup"><span data-stu-id="e8453-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="e8453-148">Usando gli strumenti per sviluppatori del browser, controllare le intestazioni di risposta per verificare se il file è memorizzato nella cache nell'area in cui viene richiesto.</span><span class="sxs-lookup"><span data-stu-id="e8453-148">Using your browser's developer tools, check the response headers to ensure the file is cached in the region where it is being requested.</span></span>

* <span data-ttu-id="e8453-149">Controllare l'intestazione della risposta **Server** .</span><span class="sxs-lookup"><span data-stu-id="e8453-149">Check the **Server** response header.</span></span>  <span data-ttu-id="e8453-150">L'intestazione deve avere il formato **Piattaforma (POP/ID server)**, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="e8453-150">The header should have the format **Platform (POP/Server ID)**, as seen in the following example.</span></span>
* <span data-ttu-id="e8453-151">Controllare che l'intestazione della risposta **X-Cache** .</span><span class="sxs-lookup"><span data-stu-id="e8453-151">Check the **X-Cache** response header.</span></span>  <span data-ttu-id="e8453-152">corrisponda a **HIT**.</span><span class="sxs-lookup"><span data-stu-id="e8453-152">The header should read **HIT**.</span></span>  

![Intestazioni di risposta CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-the-file-meets-the-size-requirements"></a><span data-ttu-id="e8453-154">Verificare che il file soddisfi i requisiti di dimensione</span><span class="sxs-lookup"><span data-stu-id="e8453-154">Verify the file meets the size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="e8453-155">Questo passaggio va eseguito solo se il profilo CDN è un profilo di **rete CDN di Azure fornita da Verizon** (Standard o Premium).</span><span class="sxs-lookup"><span data-stu-id="e8453-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="e8453-156">Per essere idoneo per la compressione, un file deve avere le dimensioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e8453-156">To be eligible for compression, a file must meet the following size requirements:</span></span>

* <span data-ttu-id="e8453-157">Maggiore di 128 byte.</span><span class="sxs-lookup"><span data-stu-id="e8453-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="e8453-158">Minore di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="e8453-158">Smaller than 1 MB.</span></span>

### <a name="check-the-request-at-the-origin-server-for-a-via-header"></a><span data-ttu-id="e8453-159">Cercare nelle richieste nel server di origine un'intestazione **Via**</span><span class="sxs-lookup"><span data-stu-id="e8453-159">Check the request at the origin server for a **Via** header</span></span>
<span data-ttu-id="e8453-160">L'intestazione HTPP **Via** indica al server Web che la richiesta viene passata da un server proxy.</span><span class="sxs-lookup"><span data-stu-id="e8453-160">The **Via** HTTP header indicates to the web server that the request is being passed by a proxy server.</span></span>  <span data-ttu-id="e8453-161">Per impostazione predefinita, i server Web Microsoft IIS non comprimono le risposte quando la richiesta contiene un'intestazione **Via** .</span><span class="sxs-lookup"><span data-stu-id="e8453-161">Microsoft IIS web servers by default do not compress responses when the request contains a **Via** header.</span></span>  <span data-ttu-id="e8453-162">Per eseguire l'override di questo comportamento, eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="e8453-162">To override this behavior, perform the following:</span></span>

* <span data-ttu-id="e8453-163">**IIS 6**: [Impostare HcNoCompressionForProxies="FALSE" nelle proprietà della metabase di IIS](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="e8453-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in the IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="e8453-164">**IIS 7 e versioni successive**: [Impostare sia **noCompressionForHttp10** che **noCompressionForProxies** su False nella configurazione del server](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="e8453-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** to False in the server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

