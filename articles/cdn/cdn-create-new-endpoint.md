---
title: aaaGetting avviato con una rete CDN di Azure | Documenti Microsoft
description: Questo argomento viene illustrato come tooenable hello Azure rete CDN (Content Delivery). esercitazione Hello tramite la creazione di hello di un nuovo profilo di rete CDN e l'endpoint.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a><span data-ttu-id="7b537-104">Introduzione alla rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="7b537-104">Getting started with Azure CDN</span></span>
<span data-ttu-id="7b537-105">Questo argomento descrive in dettaglio l'abilitazione della rete CDN di Azure creando un nuovo profilo di rete CDN e un endpoint.</span><span class="sxs-lookup"><span data-stu-id="7b537-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b537-106">Per un funzionamento della rete CDN di introduzione toohow, nonché un elenco delle funzionalità, vedere hello [Panoramica della rete CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b537-106">For an introduction toohow CDN works, as well as a list of features, see hello [CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="7b537-107">Creare un nuovo profilo di rete CDN</span><span class="sxs-lookup"><span data-stu-id="7b537-107">Create a new CDN profile</span></span>
<span data-ttu-id="7b537-108">Un profilo di rete CDN è una raccolta di endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="7b537-108">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="7b537-109">Ogni profilo contiene uno o più endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="7b537-109">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="7b537-110">È preferibile toouse più profili tooorganize gli endpoint CDN dal dominio internet, l'applicazione web o ad altri criteri.</span><span class="sxs-lookup"><span data-stu-id="7b537-110">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="7b537-111">Per impostazione predefinita, una singola sottoscrizione di Azure è limitato tooeight i profili di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="7b537-111">By default, a single Azure subscription is limited tooeight CDN profiles.</span></span> <span data-ttu-id="7b537-112">Ogni profilo CDN è l'endpoint rete CDN tooten limitato.</span><span class="sxs-lookup"><span data-stu-id="7b537-112">Each CDN profile is limited tooten CDN endpoints.</span></span>
> 
> <span data-ttu-id="7b537-113">Rete CDN prezzi viene applicato a livello di profilo rete CDN di hello.</span><span class="sxs-lookup"><span data-stu-id="7b537-113">CDN pricing is applied at hello CDN profile level.</span></span> <span data-ttu-id="7b537-114">Se si desidera toouse una combinazione di rete CDN di Azure i livelli di prezzo, è necessario più profili di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="7b537-114">If you wish toouse a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="7b537-115">Creare un nuovo endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="7b537-115">Create a new CDN endpoint</span></span>
<span data-ttu-id="7b537-116">**toocreate un nuovo endpoint CDN**</span><span class="sxs-lookup"><span data-stu-id="7b537-116">**toocreate a new CDN endpoint**</span></span>

1. <span data-ttu-id="7b537-117">In hello [portale Azure](https://portal.azure.com), passare il profilo CDN tooyour.</span><span class="sxs-lookup"><span data-stu-id="7b537-117">In hello [Azure Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="7b537-118">Si potrebbe avere aggiunto toohello dashboard nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="7b537-118">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="7b537-119">Se è, non sarà possibile trovarlo facendo **Sfoglia**, quindi **i profili di rete CDN**, e fare clic sul profilo hello prevede tooadd l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="7b537-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="7b537-120">verrà visualizzata la finestra di blade profilo rete CDN di Hello.</span><span class="sxs-lookup"><span data-stu-id="7b537-120">hello CDN profile blade appears.</span></span>
   
    ![Profilo di rete CDN][cdn-profile-settings]
2. <span data-ttu-id="7b537-122">Fare clic su hello **Aggiungi Endpoint** pulsante.</span><span class="sxs-lookup"><span data-stu-id="7b537-122">Click hello **Add Endpoint** button.</span></span>
   
    ![Pulsante Aggiungi endpoint][cdn-new-endpoint-button]
   
    <span data-ttu-id="7b537-124">Hello **aggiungere un endpoint** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="7b537-124">hello **Add an endpoint** blade appears.</span></span>
   
    ![Pannello Aggiungi endpoint][cdn-add-endpoint]
3. <span data-ttu-id="7b537-126">Immettere un **Nome** per questo endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="7b537-126">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="7b537-127">Questo nome verrà usato tooaccess le risorse memorizzate nella cache nel dominio hello `<endpointname>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="7b537-127">This name will be used tooaccess your cached resources at hello domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="7b537-128">In hello **tipo di origine** elenco a discesa selezionare il tipo di origine.</span><span class="sxs-lookup"><span data-stu-id="7b537-128">In hello **Origin type** dropdown, select your origin type.</span></span>  <span data-ttu-id="7b537-129">Selezionare **Archiviazione** per un account di archiviazione di Azure, **Servizio Cloud** per un servizio cloud di Azure, **App Web** per un'app Web di Azure oppure **Origine personalizzata** per qualsiasi altra origine di server Web accessibile pubblicamente, ospitata in Azure o altrove.</span><span class="sxs-lookup"><span data-stu-id="7b537-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span></span>
   
    ![Tipo di origine della rete CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. <span data-ttu-id="7b537-131">In hello **nome host dell'origine** elenco a discesa, selezionare o digitare il dominio di origine.</span><span class="sxs-lookup"><span data-stu-id="7b537-131">In hello **Origin hostname** dropdown, select or type your origin domain.</span></span>  <span data-ttu-id="7b537-132">elenco a discesa Hello elencherà tutte le origini disponibili del tipo di hello che è specificato nel passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="7b537-132">hello dropdown will list all available origins of hello type you specified in step 4.</span></span>  <span data-ttu-id="7b537-133">Se si seleziona *origine personalizzata* come il **tipo di origine**, digitato nel dominio hello dell'origine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="7b537-133">If you selected *Custom origin* as your **Origin type**, you will type in hello domain of your custom origin.</span></span>
6. <span data-ttu-id="7b537-134">In hello **il percorso di origine** testo immettere hello percorso toohello risorse desiderate toocache o lasciare vuoto tooallow cache qualsiasi risorsa dominio hello specificato nel passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="7b537-134">In hello **Origin path** text box, enter hello path toohello resources you want toocache, or leave blank tooallow cache any resource at hello domain you specified in step 5.</span></span>
7. <span data-ttu-id="7b537-135">In hello **intestazione host di origine**, intestazione host hello desiderato hello CDN toosend con ogni richiesta di immettere o lasciare hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="7b537-135">In hello **Origin host header**, enter hello host header you want hello CDN toosend with each request, or leave hello default.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="7b537-136">Alcuni tipi di origini, ad esempio l'archiviazione di Azure e le applicazioni Web, richiedono hello intestazione toomatch hello dominio di origine hello.</span><span class="sxs-lookup"><span data-stu-id="7b537-136">Some types of origins, such as Azure Storage and Web Apps, require hello host header toomatch hello domain of hello origin.</span></span> <span data-ttu-id="7b537-137">A meno che non si dispone di un'origine che richiede un'intestazione host diversa dal relativo dominio, è consigliabile lasciare il valore di predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="7b537-137">Unless you have an origin that requires a host header different from its domain, you should leave hello default value.</span></span>
   > 
   > 
8. <span data-ttu-id="7b537-138">Per **protocollo** e **porta di origine**, specificare hello protocolli e porte tooaccess usate le risorse di origine hello.</span><span class="sxs-lookup"><span data-stu-id="7b537-138">For **Protocol** and **Origin port**, specify hello protocols and ports used tooaccess your resources at hello origin.</span></span>  <span data-ttu-id="7b537-139">È necessario selezionare almeno un protocollo (HTTP o HTTPS).</span><span class="sxs-lookup"><span data-stu-id="7b537-139">At least one protocol (HTTP or HTTPS) must be selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7b537-140">Hello **porta di origine** influisce solo sulle quali endpoint hello porta utilizza le informazioni tooretrieve origine hello.</span><span class="sxs-lookup"><span data-stu-id="7b537-140">hello **Origin port** only affects what port hello endpoint uses tooretrieve information from hello origin.</span></span>  <span data-ttu-id="7b537-141">Hello endpoint stesso sarà solo client tooend disponibili su hello predefinito porte HTTP e HTTPS (80 e 443), indipendentemente dal hello **porta di origine**.</span><span class="sxs-lookup"><span data-stu-id="7b537-141">hello endpoint itself will only be available tooend clients on hello default HTTP and HTTPS ports (80 and 443), regardless of hello **Origin port**.</span></span>  
   > 
   > <span data-ttu-id="7b537-142">**Rete CDN di Azure da Akamai** endpoint non consentano hello completo TCP intervallo di porte per le origini.</span><span class="sxs-lookup"><span data-stu-id="7b537-142">**Azure CDN from Akamai** endpoints do not allow hello full TCP port range for origins.</span></span>  <span data-ttu-id="7b537-143">Per un elenco delle porte di origine non consentite, vedere l'articolo relativo ai [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx)(Porte di origine consentite in Rete CDN di Azure da Akamai).</span><span class="sxs-lookup"><span data-stu-id="7b537-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="7b537-144">Accesso rete CDN il contenuto usando HTTPS ha hello seguenti vincoli:</span><span class="sxs-lookup"><span data-stu-id="7b537-144">Accessing CDN content using HTTPS has hello following constraints:</span></span>
   > 
   > * <span data-ttu-id="7b537-145">È necessario utilizzare il certificato SSL hello fornito da hello CDN.</span><span class="sxs-lookup"><span data-stu-id="7b537-145">You must use hello SSL certificate provided by hello CDN.</span></span> <span data-ttu-id="7b537-146">I certificati di terze parti non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="7b537-146">Third party certificates are not supported.</span></span>
   > * <span data-ttu-id="7b537-147">È necessario utilizzare il dominio di condizione della rete CDN hello (`<endpointname>.azureedge.net`) contenuto HTTPS tooaccess.</span><span class="sxs-lookup"><span data-stu-id="7b537-147">You must use hello CDN-provided domain (`<endpointname>.azureedge.net`) tooaccess HTTPS content.</span></span> <span data-ttu-id="7b537-148">Il supporto HTTPS non è disponibile per i nomi di dominio personalizzato (CNAME) poiché hello CDN non supporta i certificati personalizzati in questo momento.</span><span class="sxs-lookup"><span data-stu-id="7b537-148">HTTPS support is not available for custom domain names (CNAMEs) since hello CDN does not support custom certificates at this time.</span></span>
   > 
   > 
9. <span data-ttu-id="7b537-149">Fare clic su hello **Aggiungi** toocreate pulsante hello nuovo endpoint.</span><span class="sxs-lookup"><span data-stu-id="7b537-149">Click hello **Add** button toocreate hello new endpoint.</span></span>
10. <span data-ttu-id="7b537-150">Dopo aver creato endpoint hello, viene visualizzato in un elenco di endpoint per il profilo hello.</span><span class="sxs-lookup"><span data-stu-id="7b537-150">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="7b537-151">visualizzazione elenco Hello Mostra hello URL toouse tooaccess memorizzati nella cache il contenuto, nonché il dominio di origine hello.</span><span class="sxs-lookup"><span data-stu-id="7b537-151">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
    
    ![Endpoint della rete CDN][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > <span data-ttu-id="7b537-153">endpoint di Hello non immediatamente saranno disponibili per l'utilizzo, come il tempo per hello registrazione toopropagate tramite hello CDN.</span><span class="sxs-lookup"><span data-stu-id="7b537-153">hello endpoint will not immediately be available for use, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="7b537-154">Per <b>Rete CDN di Azure da Akamai</b> la propagazione in genere viene completata entro un minuto.</span><span class="sxs-lookup"><span data-stu-id="7b537-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="7b537-155">Per i profili della <b>rete CDN di Azure fornita da Verizon</b>, la propagazione in genere viene completata entro 90 minuti, ma in alcuni casi può richiedere più tempo.</span><span class="sxs-lookup"><span data-stu-id="7b537-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
    > 
    > <span data-ttu-id="7b537-156">Gli utenti che tentano di nome di dominio della rete CDN hello toouse prima configurazione di endpoint hello è propagata POP toohello riceverà i codici di risposta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="7b537-156">Users who try toouse hello CDN domain name before hello endpoint configuration has propagated toohello POPs will receive HTTP 404 response codes.</span></span>  <span data-ttu-id="7b537-157">Se sono trascorse diverse ore da quando è stato creato l'endpoint e si ricevono ancora risposte 404, vedere l'articolo relativo alla [risoluzione dei problemi degli endpoint della rete CDN che restituiscono stati 404](cdn-troubleshoot-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="7b537-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span></span>
    > 
    > 

## <a name="see-also"></a><span data-ttu-id="7b537-158">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7b537-158">See Also</span></span>
* [<span data-ttu-id="7b537-159">Controllo del comportamento di memorizzazione nella cache delle richieste della rete CDN con le stringhe di query</span><span class="sxs-lookup"><span data-stu-id="7b537-159">Controlling caching behavior of requests with query strings</span></span>](cdn-query-string.md)
* [<span data-ttu-id="7b537-160">Come tooMap CDN contenuto tooa dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="7b537-160">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="7b537-161">Precaricamento di risorse in un endpoint della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="7b537-161">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="7b537-162">Ripulire un endpoint della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="7b537-162">Purge an Azure CDN Endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="7b537-163">Risoluzione dei problemi degli endpoint della rete CDN che restituiscono stati 404</span><span class="sxs-lookup"><span data-stu-id="7b537-163">Troubleshooting CDN endpoints returning 404 statuses</span></span>](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
