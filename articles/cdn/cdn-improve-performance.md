---
title: Migliorare le prestazioni con la compressione dei file nella rete CDN di Azure | Documentazione Microsoft
description: "Informazioni su come migliorare la velocità di trasferimento di file e aumentare le prestazioni di caricamento delle pagine comprimendo i file nella rete CDN di Azure."
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
ms.openlocfilehash: 7546650e6096a880f4fb4d0c94dd4ecc00b70160
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="ba0d8-103">Migliorare le prestazioni con la compressione dei file nella rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="ba0d8-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="ba0d8-104">La compressione è un metodo semplice ed efficace per aumentare la velocità di trasferimento dei file e migliorare le prestazioni di caricamento delle pagine mediante la riduzione delle dimensioni del file prima che venga inviato dal server.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-104">Compression is a simple and effective method to improve file transfer speed and increase page load performance by reducing file size before it is sent from the server.</span></span> <span data-ttu-id="ba0d8-105">Riduce i costi della larghezza di banda e offre un'esperienza più reattiva per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="ba0d8-106">Esistono due modi per abilitare la compressione:</span><span class="sxs-lookup"><span data-stu-id="ba0d8-106">There are two ways to enable compression:</span></span>

* <span data-ttu-id="ba0d8-107">È possibile abilitare la compressione nel server di origine, nel qual caso la rete CDN esegue il pass-through dei file compressi e distribuisce i file compressi ai client che li hanno richiesti.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-107">You can enable compression on your origin server, in which case the CDN passes through the compressed files and deliver compressed files to clients that request them.</span></span>
* <span data-ttu-id="ba0d8-108">È possibile abilitare la compressione direttamente sui server perimetrali della rete CDN. In questo caso, la rete CDN comprime i file e li trasmette agli utenti finali anche se non sono stati compressi dal server di origine.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-108">You can enable compression directly on CDN edge servers, in which case the CDN compresses the files and serve them to end users, even if they are not compressed by the origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba0d8-109">Le modifiche alla configurazione della rete CDN richiedono tempo per propagarsi attraverso la rete.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-109">CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="ba0d8-110">La propagazione dei profili della <b>Rete CDN di Azure fornita da Akamai</b> in genere dura meno di un minuto.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="ba0d8-111">La propagazione dei profili della <b>Rete CDN di Azure fornita da Verizon</b> , in genere le modifiche vengono applicate entro 90 minuti.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="ba0d8-112">Se questa è la prima volta che si configura la compressione per l'endpoint della rete CDN, è consigliabile attendere 1-2 ore per assicurarsi che le impostazioni di compressione si siano propagate ai POP prima di intraprendere la risoluzione di eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-112">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="ba0d8-113">Abilitare la compressione</span><span class="sxs-lookup"><span data-stu-id="ba0d8-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="ba0d8-114">I livelli della rete CDN Standard e Premium forniscono la stessa funzionalità di compressione, ma l'interfaccia utente è diversa.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-114">The Standard and Premium CDN tiers provide the same compression functionality, but the user interface differs.</span></span>  <span data-ttu-id="ba0d8-115">Per altre informazioni sulle differenze tra i livelli della rete CDN Standard e Premium, vedere [Panoramica della rete CDN di Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ba0d8-115">For more information about the differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="ba0d8-116">Livello Standard</span><span class="sxs-lookup"><span data-stu-id="ba0d8-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="ba0d8-117">Questa sezione si applica ai profili della **rete CDN Standard di Azure fornita da Verizon** e della **rete CDN Standard di Azure fornita da Akamai**.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-117">This section applies to **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="ba0d8-118">Nella pagina del profilo di rete CDN fare clic sull'endpoint della rete CDN che si desidera gestire.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-118">From the CDN profile page, click the CDN endpoint you wish to manage.</span></span>
   
    ![Endpoint della pagina del profilo di rete CDN](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="ba0d8-120">Viene aperta la pagina dell'endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-120">The CDN endpoint page opens.</span></span>
2. <span data-ttu-id="ba0d8-121">Fare clic sul pulsante **Configura** .</span><span class="sxs-lookup"><span data-stu-id="ba0d8-121">Click the **Configure** button.</span></span>
   
    ![Pulsante di gestione della pagina del profilo di rete CDN](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="ba0d8-123">Viene aperta la pagina di configurazione della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-123">The CDN Configuration page opens.</span></span>
3. <span data-ttu-id="ba0d8-124">Attivare **compressione**.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-124">Turn on **Compression**.</span></span>
   
    ![Opzioni di compressione della rete CDN](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="ba0d8-126">Usare i tipi predefiniti, o modificare l'elenco eliminando o aggiungendo tipi di file.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-126">Use the default types, or modify the list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="ba0d8-127">Se possibile, non è consigliabile applicare la compressione a formati compressi, ad esempio ZIP, MP3, MP4, JPG e così via.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-127">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="ba0d8-128">Dopo aver apportato le modifiche, fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ba0d8-128">After making your changes, click the **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="ba0d8-129">Livello Premium</span><span class="sxs-lookup"><span data-stu-id="ba0d8-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="ba0d8-130">Questa sezione si applica ai profili di **Rete CDN Premium di Azure da Verizon** .</span><span class="sxs-lookup"><span data-stu-id="ba0d8-130">This section applies to **Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="ba0d8-131">Nella pagina del profilo della rete CDN fare clic sul pulsante **Gestisci**.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-131">From the CDN profile page, click the **Manage** button.</span></span>
   
    ![Pulsante di gestione della pagina del profilo di rete CDN](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="ba0d8-133">Si aprirà il portale di gestione della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-133">The CDN management portal opens.</span></span>
2. <span data-ttu-id="ba0d8-134">Passare il puntatore sulla scheda **HTTP Large** (HTTP esteso) e quindi sul riquadro a comparsa **Impostazioni cache**.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-134">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="ba0d8-135">Fare clic su **Compressione**.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-135">Click on **Compression**.</span></span>

    ![Selezione della compressione file](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="ba0d8-137">Vengono visualizzate le opzioni di compressione.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-137">Compression options are displayed.</span></span>
   
    ![Compressione dei file](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="ba0d8-139">Abilitare la compressione facendo clic sul pulsante di opzione **Compressione abilitata** .</span><span class="sxs-lookup"><span data-stu-id="ba0d8-139">Enable compression by clicking the **Compression Enabled** radio button.</span></span>  <span data-ttu-id="ba0d8-140">Immettere i tipi MIM da comprimere sotto forma di elenco delimitato da virgole, senza spazi, nella casella di testo **Tipi di file** .</span><span class="sxs-lookup"><span data-stu-id="ba0d8-140">Enter the MIME types you wish to compress as a comma-delimited list (no spaces) in the **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="ba0d8-141">Se possibile, non è consigliabile applicare la compressione a formati compressi, ad esempio ZIP, MP3, MP4, JPG e così via.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-141">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="ba0d8-142">Dopo aver apportato le modifiche, fare clic sul pulsante **Aggiorna** .</span><span class="sxs-lookup"><span data-stu-id="ba0d8-142">After making your changes, click the **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="ba0d8-143">Regole di compressione</span><span class="sxs-lookup"><span data-stu-id="ba0d8-143">Compression rules</span></span>
<span data-ttu-id="ba0d8-144">Le tabelle seguenti descrivono il comportamento della compressione della rete CDN di Azure per ogni scenario.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba0d8-145">Per la **Rete CDN di Azure fornita da Verizon** (Standard e Premium) vengono compressi soltanto i file idonei.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="ba0d8-146">Per essere idoneo per la compressione, un file deve essere:</span><span class="sxs-lookup"><span data-stu-id="ba0d8-146">To be eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="ba0d8-147">Maggiore di 128 byte.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="ba0d8-148">Minore di 1 MB.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="ba0d8-149">Per la **Rete CDN di Azure fornita da Akamai**, tutti i file sono idonei per la compressione.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="ba0d8-150">Per tutti i prodotti della rete CDN di Azure, il file deve essere un file di tipo MIME [configurato per la compressione](#enabling-compression).</span><span class="sxs-lookup"><span data-stu-id="ba0d8-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="ba0d8-151">I profili della **rete CDN di Azure fornita da Verizon** (Standard e Premium) supportano la codifica **gzip** (zip GNU), **deflate**, **bzip2** o **br** (Brotli).</span><span class="sxs-lookup"><span data-stu-id="ba0d8-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="ba0d8-152">Per la codifica Brotli, la compressione viene eseguita solo sul server perimetrale.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-152">For Brotli encoding, the compression is done only at the edge.</span></span> <span data-ttu-id="ba0d8-153">Il client/browser deve inviare la richiesta per la codifica Brotli ed è necessario che l'asset sia stato in primo luogo compresso sul lato di origine.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-153">The client/browser must send the request for Brotli encoding and the compressed asset must have been compressed on the origin side first.</span></span> 
>
><span data-ttu-id="ba0d8-154">I profili della **rete CDN di Azure fornita da Akamai** supportano solo la codifica **gzip**.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="ba0d8-155">Gli endpoint della **rete CDN di Azure fornita da Akamai** richiedono sempre file con codifica **gzip** dall'origine, indipendentemente dalla richiesta del client.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from the origin, regardless of the client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="ba0d8-156">Compressione disabilitata o file non idoneo per la compressione</span><span class="sxs-lookup"><span data-stu-id="ba0d8-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="ba0d8-157">Formato richiesto del client tramite l'intestazione Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="ba0d8-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="ba0d8-158">Formato del file memorizzato nella cache</span><span class="sxs-lookup"><span data-stu-id="ba0d8-158">Cached file format</span></span> | <span data-ttu-id="ba0d8-159">Risposta della rete CDN al client</span><span class="sxs-lookup"><span data-stu-id="ba0d8-159">CDN response to the client</span></span> | <span data-ttu-id="ba0d8-160">Note</span><span class="sxs-lookup"><span data-stu-id="ba0d8-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ba0d8-161">Compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-161">Compressed</span></span> |<span data-ttu-id="ba0d8-162">Compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-162">Compressed</span></span> |<span data-ttu-id="ba0d8-163">Compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-163">Compressed</span></span> | |
| <span data-ttu-id="ba0d8-164">Compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-164">Compressed</span></span> |<span data-ttu-id="ba0d8-165">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-165">Uncompressed</span></span> |<span data-ttu-id="ba0d8-166">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-166">Uncompressed</span></span> | |
| <span data-ttu-id="ba0d8-167">Compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-167">Compressed</span></span> |<span data-ttu-id="ba0d8-168">Non memorizzato nella cache</span><span class="sxs-lookup"><span data-stu-id="ba0d8-168">Not cached</span></span> |<span data-ttu-id="ba0d8-169">Compressa o non compressa</span><span class="sxs-lookup"><span data-stu-id="ba0d8-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="ba0d8-170">A seconda della risposta dell'origine</span><span class="sxs-lookup"><span data-stu-id="ba0d8-170">Depends on origin response</span></span> |
| <span data-ttu-id="ba0d8-171">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-171">Uncompressed</span></span> |<span data-ttu-id="ba0d8-172">Compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-172">Compressed</span></span> |<span data-ttu-id="ba0d8-173">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-173">Uncompressed</span></span> | |
| <span data-ttu-id="ba0d8-174">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-174">Uncompressed</span></span> |<span data-ttu-id="ba0d8-175">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-175">Uncompressed</span></span> |<span data-ttu-id="ba0d8-176">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-176">Uncompressed</span></span> | |
| <span data-ttu-id="ba0d8-177">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-177">Uncompressed</span></span> |<span data-ttu-id="ba0d8-178">Non memorizzato nella cache</span><span class="sxs-lookup"><span data-stu-id="ba0d8-178">Not cached</span></span> |<span data-ttu-id="ba0d8-179">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="ba0d8-180">Compressione abilitata e file idoneo per la compressione</span><span class="sxs-lookup"><span data-stu-id="ba0d8-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="ba0d8-181">Formato richiesto del client tramite l'intestazione Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="ba0d8-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="ba0d8-182">Formato del file memorizzato nella cache</span><span class="sxs-lookup"><span data-stu-id="ba0d8-182">Cached file format</span></span> | <span data-ttu-id="ba0d8-183">Risposta della rete CDN al client</span><span class="sxs-lookup"><span data-stu-id="ba0d8-183">CDN response to the client</span></span> | <span data-ttu-id="ba0d8-184">Note</span><span class="sxs-lookup"><span data-stu-id="ba0d8-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ba0d8-185">Compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-185">Compressed</span></span> |<span data-ttu-id="ba0d8-186">Compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-186">Compressed</span></span> |<span data-ttu-id="ba0d8-187">Compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-187">Compressed</span></span> |<span data-ttu-id="ba0d8-188">Transcodifica della rete CDN tra formati supportati</span><span class="sxs-lookup"><span data-stu-id="ba0d8-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="ba0d8-189">Compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-189">Compressed</span></span> |<span data-ttu-id="ba0d8-190">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-190">Uncompressed</span></span> |<span data-ttu-id="ba0d8-191">Compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-191">Compressed</span></span> |<span data-ttu-id="ba0d8-192">Compressione da parte della rete CDN</span><span class="sxs-lookup"><span data-stu-id="ba0d8-192">CDN performs compression</span></span> |
| <span data-ttu-id="ba0d8-193">Compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-193">Compressed</span></span> |<span data-ttu-id="ba0d8-194">Non memorizzato nella cache</span><span class="sxs-lookup"><span data-stu-id="ba0d8-194">Not cached</span></span> |<span data-ttu-id="ba0d8-195">Compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-195">Compressed</span></span> |<span data-ttu-id="ba0d8-196">La rete CDN esegue la compressione se l'origine restituisce Non compresso.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="ba0d8-197">**La rete CDN di Azure fornita da Verizon** effettua il passaggio del file non compresso per la prima richiesta, per poi eseguire la compressione e la memorizzazione nella cache del file per le richieste successive.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-197">**Azure CDN from Verizon** passes the uncompressed file on the first request and then compresses and caches the file for subsequent requests.</span></span>  <span data-ttu-id="ba0d8-198">I file con l'intestazione `Cache-Control: no-cache` non verranno mai compressi.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="ba0d8-199">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-199">Uncompressed</span></span> |<span data-ttu-id="ba0d8-200">Compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-200">Compressed</span></span> |<span data-ttu-id="ba0d8-201">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-201">Uncompressed</span></span> |<span data-ttu-id="ba0d8-202">Decompressione da parte della rete CDN</span><span class="sxs-lookup"><span data-stu-id="ba0d8-202">CDN performs decompression</span></span> |
| <span data-ttu-id="ba0d8-203">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-203">Uncompressed</span></span> |<span data-ttu-id="ba0d8-204">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-204">Uncompressed</span></span> |<span data-ttu-id="ba0d8-205">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-205">Uncompressed</span></span> | |
| <span data-ttu-id="ba0d8-206">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-206">Uncompressed</span></span> |<span data-ttu-id="ba0d8-207">Non memorizzato nella cache</span><span class="sxs-lookup"><span data-stu-id="ba0d8-207">Not cached</span></span> |<span data-ttu-id="ba0d8-208">Non compresso</span><span class="sxs-lookup"><span data-stu-id="ba0d8-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="ba0d8-209">Compressione della rete CDN dei servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="ba0d8-209">Media Services CDN Compression</span></span>
<span data-ttu-id="ba0d8-210">Per endpoint di streaming abilitati alla rete CDN dei servizi multimediali, la compressione è abilitata per impostazione predefinita per i seguenti tipi di contenuto: application/vnd.ms-sstr+xml,application/dash+xml,application/vnd.apple.mpegurl,application/f4m+xml.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for the following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="ba0d8-211">Non è possibile attivare o disattivare la compressione per i tipi indicati tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba0d8-211">You cannot enable/disable compression for the mentioned types using the Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="ba0d8-212">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ba0d8-212">See also</span></span>
* [<span data-ttu-id="ba0d8-213">Risoluzione dei problemi della compressione dei file CDN</span><span class="sxs-lookup"><span data-stu-id="ba0d8-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

