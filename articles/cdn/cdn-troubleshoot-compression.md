---
title: la compressione dei file aaaTroubleshooting nella rete CDN di Azure | Documenti Microsoft
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
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="27e4c-103">Risoluzione dei problemi della compressione dei file CDN</span><span class="sxs-lookup"><span data-stu-id="27e4c-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="27e4c-104">Questo articolo consente di risolvere i problemi relativi alla [compressione dei file CDN](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="27e4c-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="27e4c-105">Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello MSDN di Azure e forum di Overflow dello Stack di hello](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="27e4c-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="27e4c-106">In alternativa, è anche possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="27e4c-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="27e4c-107">Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e fare clic su **supporto**.</span><span class="sxs-lookup"><span data-stu-id="27e4c-107">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="27e4c-108">Sintomo</span><span class="sxs-lookup"><span data-stu-id="27e4c-108">Symptom</span></span>
<span data-ttu-id="27e4c-109">La compressione per l'endpoint è abilitata, ma i file vengono restituiti non compressi.</span><span class="sxs-lookup"><span data-stu-id="27e4c-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="27e4c-110">toocheck se vengono restituiti i file compressi, è necessario uno strumento come toouse [Fiddler](http://www.telerik.com/fiddler) del browser o [gli strumenti di sviluppo](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span><span class="sxs-lookup"><span data-stu-id="27e4c-110">toocheck whether your files are being returned compressed, you need toouse a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="27e4c-111">Intestazioni della risposta HTTP hello controllo restituito con memorizzati nella cache della rete CDN in contenuto.</span><span class="sxs-lookup"><span data-stu-id="27e4c-111">Check hello HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="27e4c-112">Se è presente un'intestazione denominata `Content-Encoding` con un valore **gzip**, **bzip2** o **deflate**, il contenuto è compresso.</span><span class="sxs-lookup"><span data-stu-id="27e4c-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Intestazione Content-Encoding](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="27e4c-114">Causa</span><span class="sxs-lookup"><span data-stu-id="27e4c-114">Cause</span></span>
<span data-ttu-id="27e4c-115">Le cause possono essere diverse, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="27e4c-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="27e4c-116">Hello richiesto contenuto non è idoneo per la compressione.</span><span class="sxs-lookup"><span data-stu-id="27e4c-116">hello requested content is not eligible for compression.</span></span>
* <span data-ttu-id="27e4c-117">La compressione non è abilitata per hello il tipo di file richiesto.</span><span class="sxs-lookup"><span data-stu-id="27e4c-117">Compression is not enabled for hello requested file type.</span></span>
* <span data-ttu-id="27e4c-118">Hello HTTP richiesta non include un'intestazione di richiesta di un tipo di compressione valido.</span><span class="sxs-lookup"><span data-stu-id="27e4c-118">hello HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="27e4c-119">Passaggi per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="27e4c-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="27e4c-120">Come distribuire i nuovi endpoint, le modifiche alla configurazione della rete CDN richiedere alcune toopropagate ora tramite rete hello.</span><span class="sxs-lookup"><span data-stu-id="27e4c-120">As with deploying new endpoints, CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="27e4c-121">In genere, le modifiche vengono applicate entro 90 minuti.</span><span class="sxs-lookup"><span data-stu-id="27e4c-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="27e4c-122">Se si tratta di hello prima di che aver configurato la compressione per l'endpoint CDN, è consigliabile in attesa che le impostazioni di compressione hello siano propagate POP toohello toobe di 1-2 ore.</span><span class="sxs-lookup"><span data-stu-id="27e4c-122">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs.</span></span> 
> 
> 

### <a name="verify-hello-request"></a><span data-ttu-id="27e4c-123">Verificare una richiesta di hello</span><span class="sxs-lookup"><span data-stu-id="27e4c-123">Verify hello request</span></span>
<span data-ttu-id="27e4c-124">In primo luogo, eseguire una verifica dell'integrità di rapido su richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="27e4c-124">First, we should do a quick sanity check on hello request.</span></span>  <span data-ttu-id="27e4c-125">È possibile utilizzare il browser [gli strumenti di sviluppo](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) hello tooview le richieste effettuate.</span><span class="sxs-lookup"><span data-stu-id="27e4c-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello requests being made.</span></span>

* <span data-ttu-id="27e4c-126">Verificare che la richiesta hello viene inviata tooyour URL dell'endpoint, `<endpointname>.azureedge.net`e non all'origine.</span><span class="sxs-lookup"><span data-stu-id="27e4c-126">Verify hello request is being sent tooyour endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="27e4c-127">Verificare che la richiesta di hello contiene un **Accept-Encoding** intestazione, hello e il valore per l'intestazione contiene **gzip**, **deflate**, o **bzip2** .</span><span class="sxs-lookup"><span data-stu-id="27e4c-127">Verify hello request contains an **Accept-Encoding** header, and hello value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="27e4c-128">I profili della **rete CDN di Azure fornita da Akamai** supportano solo la codifica **gzip**.</span><span class="sxs-lookup"><span data-stu-id="27e4c-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![Intestazioni di richiesta CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="27e4c-130">Verificare le impostazioni di compressione (profilo di rete CDN Standard)</span><span class="sxs-lookup"><span data-stu-id="27e4c-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="27e4c-131">Questo passaggio va eseguito solo se il profilo CDN è un profilo di **rete CDN Standard di Azure fornita da Verizon** o di **rete CDN Standard di Azure fornita da Akamai**.</span><span class="sxs-lookup"><span data-stu-id="27e4c-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="27e4c-132">Passare l'endpoint tooyour hello [portale di Azure](https://portal.azure.com) e fare clic su hello **configura** pulsante.</span><span class="sxs-lookup"><span data-stu-id="27e4c-132">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Configure** button.</span></span>

* <span data-ttu-id="27e4c-133">Verificare se la compressione è abilitata.</span><span class="sxs-lookup"><span data-stu-id="27e4c-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="27e4c-134">Verificare il tipo MIME hello per hello contenuto toobe compresso è incluso nell'elenco di hello dei formati compressi.</span><span class="sxs-lookup"><span data-stu-id="27e4c-134">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![Impostazioni di compressione CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="27e4c-136">Verificare le impostazioni di compressione (profilo di rete CDN Premium)</span><span class="sxs-lookup"><span data-stu-id="27e4c-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="27e4c-137">Questo passaggio va eseguito solo se il profilo CDN è un profilo di **rete CDN Premium di Azure fornita da Verizon** .</span><span class="sxs-lookup"><span data-stu-id="27e4c-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="27e4c-138">Passare l'endpoint tooyour hello [portale di Azure](https://portal.azure.com) e fare clic su hello **Gestisci** pulsante.</span><span class="sxs-lookup"><span data-stu-id="27e4c-138">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Manage** button.</span></span>  <span data-ttu-id="27e4c-139">verrà aperto il portale supplementare di Hello.</span><span class="sxs-lookup"><span data-stu-id="27e4c-139">hello supplemental portal will open.</span></span>  <span data-ttu-id="27e4c-140">Passare il mouse su hello **HTTP grandi** scheda, quindi passare il mouse su hello **le impostazioni della Cache** riquadro a comparsa.</span><span class="sxs-lookup"><span data-stu-id="27e4c-140">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="27e4c-141">Fare clic su **Compressione**.</span><span class="sxs-lookup"><span data-stu-id="27e4c-141">Click **Compression**.</span></span> 

* <span data-ttu-id="27e4c-142">Verificare se la compressione è abilitata.</span><span class="sxs-lookup"><span data-stu-id="27e4c-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="27e4c-143">Verificare hello **tipi di File** elenco contiene un elenco delimitato da virgole (senza spazi) di tipi MIME.</span><span class="sxs-lookup"><span data-stu-id="27e4c-143">Verify hello **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="27e4c-144">Verificare il tipo MIME hello per hello contenuto toobe compresso è incluso nell'elenco di hello dei formati compressi.</span><span class="sxs-lookup"><span data-stu-id="27e4c-144">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![Impostazioni di compressione CDN premium](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a><span data-ttu-id="27e4c-146">Verificare il contenuto di hello è memorizzato nella cache</span><span class="sxs-lookup"><span data-stu-id="27e4c-146">Verify hello content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="27e4c-147">Questo passaggio va eseguito solo se il profilo CDN è un profilo di **rete CDN di Azure fornita da Verizon** (Standard o Premium).</span><span class="sxs-lookup"><span data-stu-id="27e4c-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="27e4c-148">Utilizzando gli strumenti di sviluppo del browser, verificare hello risposta intestazioni tooensure hello memorizzato nell'area di hello in cui viene richiesto.</span><span class="sxs-lookup"><span data-stu-id="27e4c-148">Using your browser's developer tools, check hello response headers tooensure hello file is cached in hello region where it is being requested.</span></span>

* <span data-ttu-id="27e4c-149">Controllare hello **Server** intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="27e4c-149">Check hello **Server** response header.</span></span>  <span data-ttu-id="27e4c-150">intestazione Hello deve avere il formato di hello **piattaforma (POP/Server ID)**, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="27e4c-150">hello header should have hello format **Platform (POP/Server ID)**, as seen in hello following example.</span></span>
* <span data-ttu-id="27e4c-151">Controllare hello **X Cache** intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="27e4c-151">Check hello **X-Cache** response header.</span></span>  <span data-ttu-id="27e4c-152">intestazione Hello dovrebbe essere **HIT**.</span><span class="sxs-lookup"><span data-stu-id="27e4c-152">hello header should read **HIT**.</span></span>  

![Intestazioni di risposta CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a><span data-ttu-id="27e4c-154">Verificare il file hello soddisfi i requisiti di dimensione hello</span><span class="sxs-lookup"><span data-stu-id="27e4c-154">Verify hello file meets hello size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="27e4c-155">Questo passaggio va eseguito solo se il profilo CDN è un profilo di **rete CDN di Azure fornita da Verizon** (Standard o Premium).</span><span class="sxs-lookup"><span data-stu-id="27e4c-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="27e4c-156">toobe idonee per la compressione, un file deve soddisfare hello seguenti requisiti di dimensione:</span><span class="sxs-lookup"><span data-stu-id="27e4c-156">toobe eligible for compression, a file must meet hello following size requirements:</span></span>

* <span data-ttu-id="27e4c-157">Maggiore di 128 byte.</span><span class="sxs-lookup"><span data-stu-id="27e4c-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="27e4c-158">Minore di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="27e4c-158">Smaller than 1 MB.</span></span>

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a><span data-ttu-id="27e4c-159">Controllo hello richiesta al server di origine hello un **tramite** intestazione</span><span class="sxs-lookup"><span data-stu-id="27e4c-159">Check hello request at hello origin server for a **Via** header</span></span>
<span data-ttu-id="27e4c-160">Hello **tramite** intestazione HTTP indica i server web toohello che hello richiesta viene passato da un server proxy.</span><span class="sxs-lookup"><span data-stu-id="27e4c-160">hello **Via** HTTP header indicates toohello web server that hello request is being passed by a proxy server.</span></span>  <span data-ttu-id="27e4c-161">Server web IIS Microsoft per impostazione predefinita non comprimere le risposte quando hello richiesta contiene un **tramite** intestazione.</span><span class="sxs-lookup"><span data-stu-id="27e4c-161">Microsoft IIS web servers by default do not compress responses when hello request contains a **Via** header.</span></span>  <span data-ttu-id="27e4c-162">toooverride questo comportamento, eseguire l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="27e4c-162">toooverride this behavior, perform hello following:</span></span>

* <span data-ttu-id="27e4c-163">**IIS 6**: [impostare HcNoCompressionForProxies = "FALSE" nelle proprietà della Metabase di IIS hello](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="27e4c-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in hello IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="27e4c-164">**IIS 7 e successive**: [impostare sia **noCompressionForHttp10** e **noCompressionForProxies** tooFalse in configurazione server hello](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="27e4c-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** tooFalse in hello server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

