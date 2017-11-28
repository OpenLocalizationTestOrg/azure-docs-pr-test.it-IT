---
title: prestazioni aaaImprove compressione dei file nella rete CDN di Azure | Documenti Microsoft
description: "Informazioni su come file tooimprove trasferire velocità e aumentare le prestazioni di caricamento pagina per la compressione dei file nella rete CDN di Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="1226a-103">Migliorare le prestazioni con la compressione dei file nella rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="1226a-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="1226a-104">La compressione è la velocità di trasferimento file un metodo semplice ed efficace tooimprove e aumento delle prestazioni di caricamento pagina grazie alla riduzione delle dimensioni del file prima di esso viene inviato dal server hello.</span><span class="sxs-lookup"><span data-stu-id="1226a-104">Compression is a simple and effective method tooimprove file transfer speed and increase page load performance by reducing file size before it is sent from hello server.</span></span> <span data-ttu-id="1226a-105">Riduce i costi della larghezza di banda e offre un'esperienza più reattiva per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="1226a-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="1226a-106">Esistono due modi tooenable compressione:</span><span class="sxs-lookup"><span data-stu-id="1226a-106">There are two ways tooenable compression:</span></span>

* <span data-ttu-id="1226a-107">È possibile abilitare la compressione sul server di origine, nel qual caso hello CDN passaggi hello file compressi e recapitare tooclients file compressi che ne fanno richiesta.</span><span class="sxs-lookup"><span data-stu-id="1226a-107">You can enable compression on your origin server, in which case hello CDN passes through hello compressed files and deliver compressed files tooclients that request them.</span></span>
* <span data-ttu-id="1226a-108">È possibile abilitare la compressione direttamente su un server di edge CDN, in cui hello case CDN comprime, hello file ed esse forniscono agli utenti di tooend, anche se essi non vengono compressi dal server di origine hello.</span><span class="sxs-lookup"><span data-stu-id="1226a-108">You can enable compression directly on CDN edge servers, in which case hello CDN compresses hello files and serve them tooend users, even if they are not compressed by hello origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1226a-109">Modifiche alla configurazione di rete CDN vengono alcuni toopropagate ora tramite rete hello.</span><span class="sxs-lookup"><span data-stu-id="1226a-109">CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="1226a-110">La propagazione dei profili della <b>Rete CDN di Azure fornita da Akamai</b> in genere dura meno di un minuto.</span><span class="sxs-lookup"><span data-stu-id="1226a-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="1226a-111">La propagazione dei profili della <b>Rete CDN di Azure fornita da Verizon</b> , in genere le modifiche vengono applicate entro 90 minuti.</span><span class="sxs-lookup"><span data-stu-id="1226a-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="1226a-112">Se si tratta di hello prima di che aver configurato la compressione per l'endpoint CDN, è necessario considerare in attesa che le impostazioni di compressione hello siano propagate POP toohello prima della risoluzione dei problemi di toobe 1-2 ore</span><span class="sxs-lookup"><span data-stu-id="1226a-112">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="1226a-113">Abilitare la compressione</span><span class="sxs-lookup"><span data-stu-id="1226a-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="1226a-114">forniscono Hello livelli Standard e Premium CDN hello stessa funzionalità di compressione, ma hello interfaccia utente diversa.</span><span class="sxs-lookup"><span data-stu-id="1226a-114">hello Standard and Premium CDN tiers provide hello same compression functionality, but hello user interface differs.</span></span>  <span data-ttu-id="1226a-115">Per ulteriori informazioni sulle differenze di hello tra i livelli Standard e Premium CDN, vedere [Panoramica della rete CDN di Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1226a-115">For more information about hello differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="1226a-116">Livello Standard</span><span class="sxs-lookup"><span data-stu-id="1226a-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="1226a-117">Questa sezione si applica troppo**Azure CDN Standard da Verizon** e **Azure CDN Standard da Akamai** profili.</span><span class="sxs-lookup"><span data-stu-id="1226a-117">This section applies too**Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="1226a-118">Dalla pagina del profilo CDN hello, fare clic su endpoint rete CDN hello desiderato toomanage.</span><span class="sxs-lookup"><span data-stu-id="1226a-118">From hello CDN profile page, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![Endpoint della pagina del profilo di rete CDN](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="1226a-120">verrà visualizzata la pagina endpoint rete CDN di Hello.</span><span class="sxs-lookup"><span data-stu-id="1226a-120">hello CDN endpoint page opens.</span></span>
2. <span data-ttu-id="1226a-121">Fare clic su hello **configura** pulsante.</span><span class="sxs-lookup"><span data-stu-id="1226a-121">Click hello **Configure** button.</span></span>
   
    ![Pulsante di gestione della pagina del profilo di rete CDN](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="1226a-123">verrà visualizzata la pagina di configurazione della rete CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="1226a-123">hello CDN Configuration page opens.</span></span>
3. <span data-ttu-id="1226a-124">Attivare **compressione**.</span><span class="sxs-lookup"><span data-stu-id="1226a-124">Turn on **Compression**.</span></span>
   
    ![Opzioni di compressione della rete CDN](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="1226a-126">Utilizzare i tipi predefiniti hello o modificare l'elenco di hello mediante la rimozione o aggiunta di tipi di file.</span><span class="sxs-lookup"><span data-stu-id="1226a-126">Use hello default types, or modify hello list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="1226a-127">Mentre è possibile, si consiglia di formati di toocompressed compressione tooapply, ad esempio ZIP, MP3, MP4, JPG e così via.</span><span class="sxs-lookup"><span data-stu-id="1226a-127">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="1226a-128">Dopo aver apportato le modifiche, fare clic su hello **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="1226a-128">After making your changes, click hello **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="1226a-129">Livello Premium</span><span class="sxs-lookup"><span data-stu-id="1226a-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="1226a-130">Questa sezione si applica troppo**Premium rete CDN di Azure da Verizon** profili.</span><span class="sxs-lookup"><span data-stu-id="1226a-130">This section applies too**Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="1226a-131">Dalla pagina del profilo CDN hello, fare clic su hello **Gestisci** pulsante.</span><span class="sxs-lookup"><span data-stu-id="1226a-131">From hello CDN profile page, click hello **Manage** button.</span></span>
   
    ![Pulsante di gestione della pagina del profilo di rete CDN](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="1226a-133">viene visualizzato il portale di gestione della rete CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="1226a-133">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="1226a-134">Passare il mouse su hello **HTTP grandi** scheda, quindi passare il mouse su hello **le impostazioni della Cache** riquadro a comparsa.</span><span class="sxs-lookup"><span data-stu-id="1226a-134">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="1226a-135">Fare clic su **Compressione**.</span><span class="sxs-lookup"><span data-stu-id="1226a-135">Click on **Compression**.</span></span>

    ![Selezione della compressione file](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="1226a-137">Vengono visualizzate le opzioni di compressione.</span><span class="sxs-lookup"><span data-stu-id="1226a-137">Compression options are displayed.</span></span>
   
    ![Compressione dei file](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="1226a-139">Abilitare la compressione facendo hello **è abilitata la compressione** pulsante di opzione.</span><span class="sxs-lookup"><span data-stu-id="1226a-139">Enable compression by clicking hello **Compression Enabled** radio button.</span></span>  <span data-ttu-id="1226a-140">Immettere i tipi MIME hello desiderato toocompress come un elenco delimitato da virgole (senza spazi) in hello **tipi di File** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="1226a-140">Enter hello MIME types you wish toocompress as a comma-delimited list (no spaces) in hello **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="1226a-141">Mentre è possibile, si consiglia di formati di toocompressed compressione tooapply, ad esempio ZIP, MP3, MP4, JPG e così via.</span><span class="sxs-lookup"><span data-stu-id="1226a-141">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="1226a-142">Dopo aver apportato le modifiche, fare clic su hello **aggiornamento** pulsante.</span><span class="sxs-lookup"><span data-stu-id="1226a-142">After making your changes, click hello **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="1226a-143">Regole di compressione</span><span class="sxs-lookup"><span data-stu-id="1226a-143">Compression rules</span></span>
<span data-ttu-id="1226a-144">Le tabelle seguenti descrivono il comportamento della compressione della rete CDN di Azure per ogni scenario.</span><span class="sxs-lookup"><span data-stu-id="1226a-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1226a-145">Per la **Rete CDN di Azure fornita da Verizon** (Standard e Premium) vengono compressi soltanto i file idonei.</span><span class="sxs-lookup"><span data-stu-id="1226a-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="1226a-146">toobe idonee per la compressione, un file necessario:</span><span class="sxs-lookup"><span data-stu-id="1226a-146">toobe eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="1226a-147">Maggiore di 128 byte.</span><span class="sxs-lookup"><span data-stu-id="1226a-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="1226a-148">Minore di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="1226a-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="1226a-149">Per la **Rete CDN di Azure fornita da Akamai**, tutti i file sono idonei per la compressione.</span><span class="sxs-lookup"><span data-stu-id="1226a-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="1226a-150">Per tutti i prodotti della rete CDN di Azure, il file deve essere un file di tipo MIME [configurato per la compressione](#enabling-compression).</span><span class="sxs-lookup"><span data-stu-id="1226a-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="1226a-151">I profili della **rete CDN di Azure fornita da Verizon** (Standard e Premium) supportano la codifica **gzip** (zip GNU), **deflate**, **bzip2** o **br** (Brotli).</span><span class="sxs-lookup"><span data-stu-id="1226a-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="1226a-152">Per la codifica Brotli, la compressione di hello viene eseguita solo nel bordo hello.</span><span class="sxs-lookup"><span data-stu-id="1226a-152">For Brotli encoding, hello compression is done only at hello edge.</span></span> <span data-ttu-id="1226a-153">Hello client/browser deve inviare una richiesta hello per la codifica Brotli e asset compresso hello deve sono stati compressi sul lato di origine hello prima.</span><span class="sxs-lookup"><span data-stu-id="1226a-153">hello client/browser must send hello request for Brotli encoding and hello compressed asset must have been compressed on hello origin side first.</span></span> 
>
><span data-ttu-id="1226a-154">I profili della **rete CDN di Azure fornita da Akamai** supportano solo la codifica **gzip**.</span><span class="sxs-lookup"><span data-stu-id="1226a-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="1226a-155">**Rete CDN di Azure da Akamai** endpoint sempre richiesta **gzip** con codifica di file di origine di hello, indipendentemente dalla richiesta di hello del client.</span><span class="sxs-lookup"><span data-stu-id="1226a-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from hello origin, regardless of hello client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="1226a-156">Compressione disabilitata o file non idoneo per la compressione</span><span class="sxs-lookup"><span data-stu-id="1226a-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="1226a-157">Formato richiesto del client tramite l'intestazione Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="1226a-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="1226a-158">Formato del file memorizzato nella cache</span><span class="sxs-lookup"><span data-stu-id="1226a-158">Cached file format</span></span> | <span data-ttu-id="1226a-159">Client toohello di risposta della rete CDN</span><span class="sxs-lookup"><span data-stu-id="1226a-159">CDN response toohello client</span></span> | <span data-ttu-id="1226a-160">Note</span><span class="sxs-lookup"><span data-stu-id="1226a-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1226a-161">Compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-161">Compressed</span></span> |<span data-ttu-id="1226a-162">Compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-162">Compressed</span></span> |<span data-ttu-id="1226a-163">Compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-163">Compressed</span></span> | |
| <span data-ttu-id="1226a-164">Compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-164">Compressed</span></span> |<span data-ttu-id="1226a-165">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-165">Uncompressed</span></span> |<span data-ttu-id="1226a-166">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-166">Uncompressed</span></span> | |
| <span data-ttu-id="1226a-167">Compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-167">Compressed</span></span> |<span data-ttu-id="1226a-168">Non memorizzato nella cache</span><span class="sxs-lookup"><span data-stu-id="1226a-168">Not cached</span></span> |<span data-ttu-id="1226a-169">Compressa o non compressa</span><span class="sxs-lookup"><span data-stu-id="1226a-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="1226a-170">A seconda della risposta dell'origine</span><span class="sxs-lookup"><span data-stu-id="1226a-170">Depends on origin response</span></span> |
| <span data-ttu-id="1226a-171">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-171">Uncompressed</span></span> |<span data-ttu-id="1226a-172">Compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-172">Compressed</span></span> |<span data-ttu-id="1226a-173">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-173">Uncompressed</span></span> | |
| <span data-ttu-id="1226a-174">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-174">Uncompressed</span></span> |<span data-ttu-id="1226a-175">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-175">Uncompressed</span></span> |<span data-ttu-id="1226a-176">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-176">Uncompressed</span></span> | |
| <span data-ttu-id="1226a-177">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-177">Uncompressed</span></span> |<span data-ttu-id="1226a-178">Non memorizzato nella cache</span><span class="sxs-lookup"><span data-stu-id="1226a-178">Not cached</span></span> |<span data-ttu-id="1226a-179">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="1226a-180">Compressione abilitata e file idoneo per la compressione</span><span class="sxs-lookup"><span data-stu-id="1226a-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="1226a-181">Formato richiesto del client tramite l'intestazione Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="1226a-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="1226a-182">Formato del file memorizzato nella cache</span><span class="sxs-lookup"><span data-stu-id="1226a-182">Cached file format</span></span> | <span data-ttu-id="1226a-183">Client toohello di risposta della rete CDN</span><span class="sxs-lookup"><span data-stu-id="1226a-183">CDN response toohello client</span></span> | <span data-ttu-id="1226a-184">Note</span><span class="sxs-lookup"><span data-stu-id="1226a-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1226a-185">Compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-185">Compressed</span></span> |<span data-ttu-id="1226a-186">Compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-186">Compressed</span></span> |<span data-ttu-id="1226a-187">Compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-187">Compressed</span></span> |<span data-ttu-id="1226a-188">Transcodifica della rete CDN tra formati supportati</span><span class="sxs-lookup"><span data-stu-id="1226a-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="1226a-189">Compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-189">Compressed</span></span> |<span data-ttu-id="1226a-190">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-190">Uncompressed</span></span> |<span data-ttu-id="1226a-191">Compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-191">Compressed</span></span> |<span data-ttu-id="1226a-192">Compressione da parte della rete CDN</span><span class="sxs-lookup"><span data-stu-id="1226a-192">CDN performs compression</span></span> |
| <span data-ttu-id="1226a-193">Compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-193">Compressed</span></span> |<span data-ttu-id="1226a-194">Non memorizzato nella cache</span><span class="sxs-lookup"><span data-stu-id="1226a-194">Not cached</span></span> |<span data-ttu-id="1226a-195">Compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-195">Compressed</span></span> |<span data-ttu-id="1226a-196">La rete CDN esegue la compressione se l'origine restituisce Non compresso.</span><span class="sxs-lookup"><span data-stu-id="1226a-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="1226a-197">**Rete CDN di Azure da Verizon** passa hello file non compresso della prima richiesta hello e quindi comprime e memorizza nella cache di hello file per le richieste successive.</span><span class="sxs-lookup"><span data-stu-id="1226a-197">**Azure CDN from Verizon** passes hello uncompressed file on hello first request and then compresses and caches hello file for subsequent requests.</span></span>  <span data-ttu-id="1226a-198">I file con l'intestazione `Cache-Control: no-cache` non verranno mai compressi.</span><span class="sxs-lookup"><span data-stu-id="1226a-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="1226a-199">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-199">Uncompressed</span></span> |<span data-ttu-id="1226a-200">Compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-200">Compressed</span></span> |<span data-ttu-id="1226a-201">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-201">Uncompressed</span></span> |<span data-ttu-id="1226a-202">Decompressione da parte della rete CDN</span><span class="sxs-lookup"><span data-stu-id="1226a-202">CDN performs decompression</span></span> |
| <span data-ttu-id="1226a-203">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-203">Uncompressed</span></span> |<span data-ttu-id="1226a-204">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-204">Uncompressed</span></span> |<span data-ttu-id="1226a-205">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-205">Uncompressed</span></span> | |
| <span data-ttu-id="1226a-206">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-206">Uncompressed</span></span> |<span data-ttu-id="1226a-207">Non memorizzato nella cache</span><span class="sxs-lookup"><span data-stu-id="1226a-207">Not cached</span></span> |<span data-ttu-id="1226a-208">Non compresso</span><span class="sxs-lookup"><span data-stu-id="1226a-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="1226a-209">Compressione della rete CDN dei servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1226a-209">Media Services CDN Compression</span></span>
<span data-ttu-id="1226a-210">Per gli endpoint di streaming abilitata la rete CDN di servizi multimediali, la compressione è abilitata per impostazione predefinita per i seguenti tipi di contenuto hello: application/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, applicazione/f4m + xml.</span><span class="sxs-lookup"><span data-stu-id="1226a-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for hello following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="1226a-211">È possibile abilitare/disabilitare la compressione per hello indicato tipi utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1226a-211">You cannot enable/disable compression for hello mentioned types using hello Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="1226a-212">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1226a-212">See also</span></span>
* [<span data-ttu-id="1226a-213">Risoluzione dei problemi della compressione dei file CDN</span><span class="sxs-lookup"><span data-stu-id="1226a-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

