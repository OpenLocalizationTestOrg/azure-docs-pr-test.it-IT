---
title: Introduzione alla rete CDN di Azure | Documentazione Microsoft
description: Questo argomento illustra come abilitare la rete per la distribuzione di contenuti (CDN) di Azure. Questa esercitazione illustra la creazione di un nuovo profilo ed endpoint della rete CDN.
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
ms.openlocfilehash: d263e911d0d0b3cdc1e48e300a3c8a0994b38c39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-cdn"></a><span data-ttu-id="b3070-104">Introduzione alla rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="b3070-104">Getting started with Azure CDN</span></span>
<span data-ttu-id="b3070-105">Questo argomento descrive in dettaglio l'abilitazione della rete CDN di Azure creando un nuovo profilo di rete CDN e un endpoint.</span><span class="sxs-lookup"><span data-stu-id="b3070-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3070-106">Per un'introduzione al funzionamento della rete CDN e per un elenco delle funzionalità, vedere [Panoramica della rete CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b3070-106">For an introduction to how CDN works, as well as a list of features, see the [CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="b3070-107">Creare un nuovo profilo di rete CDN</span><span class="sxs-lookup"><span data-stu-id="b3070-107">Create a new CDN profile</span></span>
<span data-ttu-id="b3070-108">Un profilo di rete CDN è una raccolta di endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="b3070-108">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="b3070-109">Ogni profilo contiene uno o più endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="b3070-109">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="b3070-110">Si consiglia di usare più profili per organizzare gli endpoint della rete CDN tramite il dominio internet, l’applicazione web o altri criteri.</span><span class="sxs-lookup"><span data-stu-id="b3070-110">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="b3070-111">Per impostazione predefinita, ogni sottoscrizione di Azure è limitata a otto profili della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="b3070-111">By default, a single Azure subscription is limited to eight CDN profiles.</span></span> <span data-ttu-id="b3070-112">Ogni profilo della rete CDN è limitato a dieci endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="b3070-112">Each CDN profile is limited to ten CDN endpoints.</span></span>
> 
> <span data-ttu-id="b3070-113">I prezzi della rete CDN vengono applicati a livello di profilo della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="b3070-113">CDN pricing is applied at the CDN profile level.</span></span> <span data-ttu-id="b3070-114">Se si vuole usare una combinazione di piani tariffari della rete CDN di Azure, è necessario avere più profili CDN.</span><span class="sxs-lookup"><span data-stu-id="b3070-114">If you wish to use a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="b3070-115">Creare un nuovo endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="b3070-115">Create a new CDN endpoint</span></span>
<span data-ttu-id="b3070-116">**Per creare nuovo endpoint della rete CDN**</span><span class="sxs-lookup"><span data-stu-id="b3070-116">**To create a new CDN endpoint**</span></span>

1. <span data-ttu-id="b3070-117">Nel [portale di Azure](https://portal.azure.com)passare al profilo della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="b3070-117">In the [Azure Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="b3070-118">Lo si potrebbe aver bloccato nel dashboard nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="b3070-118">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="b3070-119">Se così non fosse, è possibile trovarlo facendo clic su **Esplora**, quindi su **Profili rete CDN** e facendo clic sul profilo in cui si prevede di aggiungere l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="b3070-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="b3070-120">Viene visualizzato il pannello del profilo di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="b3070-120">The CDN profile blade appears.</span></span>
   
    ![Profilo di rete CDN][cdn-profile-settings]
2. <span data-ttu-id="b3070-122">Fare clic sul pulsante **Aggiungi Endpoint** .</span><span class="sxs-lookup"><span data-stu-id="b3070-122">Click the **Add Endpoint** button.</span></span>
   
    ![Pulsante Aggiungi endpoint][cdn-new-endpoint-button]
   
    <span data-ttu-id="b3070-124">Viene visualizzato il pannello **Aggiungi un endpoint** .</span><span class="sxs-lookup"><span data-stu-id="b3070-124">The **Add an endpoint** blade appears.</span></span>
   
    ![Pannello Aggiungi endpoint][cdn-add-endpoint]
3. <span data-ttu-id="b3070-126">Immettere un **Nome** per questo endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="b3070-126">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="b3070-127">Questo nome verrà usato per accedere alle risorse memorizzate nella cache nel dominio `<endpointname>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="b3070-127">This name will be used to access your cached resources at the domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="b3070-128">Nell'elenco a discesa **Tipo origine** selezionare il tipo di origine.</span><span class="sxs-lookup"><span data-stu-id="b3070-128">In the **Origin type** dropdown, select your origin type.</span></span>  <span data-ttu-id="b3070-129">Selezionare **Archiviazione** per un account di archiviazione di Azure, **Servizio Cloud** per un servizio cloud di Azure, **App Web** per un'app Web di Azure oppure **Origine personalizzata** per qualsiasi altra origine di server Web accessibile pubblicamente, ospitata in Azure o altrove.</span><span class="sxs-lookup"><span data-stu-id="b3070-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span></span>
   
    ![Tipo di origine della rete CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. <span data-ttu-id="b3070-131">Nell'elenco a discesa **Nome host origine** selezionare o digitare il dominio di origine.</span><span class="sxs-lookup"><span data-stu-id="b3070-131">In the **Origin hostname** dropdown, select or type your origin domain.</span></span>  <span data-ttu-id="b3070-132">Nell’elenco a discesa compariranno tutte le origini disponibili del tipo specificato nel passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="b3070-132">The dropdown will list all available origins of the type you specified in step 4.</span></span>  <span data-ttu-id="b3070-133">Se è stato selezionato l’elemento *Origine personalizzata* come **Tipo di origine**, si digiterà nel dominio di origine personalizzato.</span><span class="sxs-lookup"><span data-stu-id="b3070-133">If you selected *Custom origin* as your **Origin type**, you will type in the domain of your custom origin.</span></span>
6. <span data-ttu-id="b3070-134">Nella casella di testo **Percorso origine** inserire il percorso per le risorse che si desidera memorizzare nella cache oppure lasciare vuoto per consentire la memorizzazione nella cache di qualsiasi risorsa nel dominio specificato nel passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="b3070-134">In the **Origin path** text box, enter the path to the resources you want to cache, or leave blank to allow cache any resource at the domain you specified in step 5.</span></span>
7. <span data-ttu-id="b3070-135">Nell’ **Intestazione dell’host di origine**, inserire l'intestazione dell’host che si desidera che la rete CDN invii con ogni richiesta di immettere, o lasciare il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="b3070-135">In the **Origin host header**, enter the host header you want the CDN to send with each request, or leave the default.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="b3070-136">Per alcuni tipi di origini, ad esempio Archiviazione di Azure e App Web, è necessario che l'intestazione host corrisponda al dominio dell'origine.</span><span class="sxs-lookup"><span data-stu-id="b3070-136">Some types of origins, such as Azure Storage and Web Apps, require the host header to match the domain of the origin.</span></span> <span data-ttu-id="b3070-137">A meno che non si abbia un'origine che richiede un'intestazione host diversa dal dominio, è consigliabile lasciare il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="b3070-137">Unless you have an origin that requires a host header different from its domain, you should leave the default value.</span></span>
   > 
   > 
8. <span data-ttu-id="b3070-138">Per **Protocollo** e **Porta dell'origine** specificare i protocolli e le porte usate per accedere alle risorse in corrispondenza dell'origine.</span><span class="sxs-lookup"><span data-stu-id="b3070-138">For **Protocol** and **Origin port**, specify the protocols and ports used to access your resources at the origin.</span></span>  <span data-ttu-id="b3070-139">È necessario selezionare almeno un protocollo (HTTP o HTTPS).</span><span class="sxs-lookup"><span data-stu-id="b3070-139">At least one protocol (HTTP or HTTPS) must be selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b3070-140">**Porta dell'origine** interessa solo la porta usata dall'endpoint per recuperare informazioni dall'origine.</span><span class="sxs-lookup"><span data-stu-id="b3070-140">The **Origin port** only affects what port the endpoint uses to retrieve information from the origin.</span></span>  <span data-ttu-id="b3070-141">L'endpoint stesso sarà disponibile solo per i client finali sulle porte HTTP e HTTPS (80 e 443), indipendentemente dalla **Porta dell'origine**.</span><span class="sxs-lookup"><span data-stu-id="b3070-141">The endpoint itself will only be available to end clients on the default HTTP and HTTPS ports (80 and 443), regardless of the **Origin port**.</span></span>  
   > 
   > <span data-ttu-id="b3070-142">**Rete CDN di Azure da Akamai** non consentono l'intera gamma di porte TCP per le origini.</span><span class="sxs-lookup"><span data-stu-id="b3070-142">**Azure CDN from Akamai** endpoints do not allow the full TCP port range for origins.</span></span>  <span data-ttu-id="b3070-143">Per un elenco delle porte di origine non consentite, vedere l'articolo relativo ai [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx)(Porte di origine consentite in Rete CDN di Azure da Akamai).</span><span class="sxs-lookup"><span data-stu-id="b3070-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="b3070-144">L'accesso al contenuto della rete CDN tramite HTTPS presenta i vincoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="b3070-144">Accessing CDN content using HTTPS has the following constraints:</span></span>
   > 
   > * <span data-ttu-id="b3070-145">È necessario usare il certificato SSL fornito dalla rete CDN.</span><span class="sxs-lookup"><span data-stu-id="b3070-145">You must use the SSL certificate provided by the CDN.</span></span> <span data-ttu-id="b3070-146">I certificati di terze parti non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="b3070-146">Third party certificates are not supported.</span></span>
   > * <span data-ttu-id="b3070-147">È necessario usare il dominio fornito dalla rete CDN,`<endpointname>.azureedge.net`, per accedere al contenuto HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b3070-147">You must use the CDN-provided domain (`<endpointname>.azureedge.net`) to access HTTPS content.</span></span> <span data-ttu-id="b3070-148">Il supporto HTTPS non è disponibile per i nomi di dominio personalizzati (CNAME) perché la rete CDN attualmente non supporta i certificati personalizzati.</span><span class="sxs-lookup"><span data-stu-id="b3070-148">HTTPS support is not available for custom domain names (CNAMEs) since the CDN does not support custom certificates at this time.</span></span>
   > 
   > 
9. <span data-ttu-id="b3070-149">Per creare il nuovo endpoint, fare clic sul pulsante **Aggiungi** .</span><span class="sxs-lookup"><span data-stu-id="b3070-149">Click the **Add** button to create the new endpoint.</span></span>
10. <span data-ttu-id="b3070-150">Dopo la creazione, l'endpoint sarà visualizzato in un elenco di endpoint per il profilo.</span><span class="sxs-lookup"><span data-stu-id="b3070-150">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="b3070-151">Nella visualizzazione elenco sono mostrati gli URL da usare per accedere a contenuti memorizzati nella cache, oltre al dominio di origine.</span><span class="sxs-lookup"><span data-stu-id="b3070-151">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
    
    ![Endpoint della rete CDN][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > <span data-ttu-id="b3070-153">L'endpoint non sarà disponibile immediatamente per l'uso, perché la propagazione della registrazione nella rete CDN richiede tempo.</span><span class="sxs-lookup"><span data-stu-id="b3070-153">The endpoint will not immediately be available for use, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="b3070-154">Per <b>Rete CDN di Azure da Akamai</b> la propagazione in genere viene completata entro un minuto.</span><span class="sxs-lookup"><span data-stu-id="b3070-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="b3070-155">Per i profili della <b>rete CDN di Azure fornita da Verizon</b>, la propagazione in genere viene completata entro 90 minuti, ma in alcuni casi può richiedere più tempo.</span><span class="sxs-lookup"><span data-stu-id="b3070-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
    > 
    > <span data-ttu-id="b3070-156">Gli utenti che provano a usare il nome di dominio della rete CDN prima che la configurazione dell'endpoint sia stata propagata ai POP riceveranno codici di risposta HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="b3070-156">Users who try to use the CDN domain name before the endpoint configuration has propagated to the POPs will receive HTTP 404 response codes.</span></span>  <span data-ttu-id="b3070-157">Se sono trascorse diverse ore da quando è stato creato l'endpoint e si ricevono ancora risposte 404, vedere l'articolo relativo alla [risoluzione dei problemi degli endpoint della rete CDN che restituiscono stati 404](cdn-troubleshoot-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="b3070-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span></span>
    > 
    > 

## <a name="see-also"></a><span data-ttu-id="b3070-158">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b3070-158">See Also</span></span>
* [<span data-ttu-id="b3070-159">Controllo del comportamento di memorizzazione nella cache delle richieste della rete CDN con le stringhe di query</span><span class="sxs-lookup"><span data-stu-id="b3070-159">Controlling caching behavior of requests with query strings</span></span>](cdn-query-string.md)
* [<span data-ttu-id="b3070-160">Come eseguire il mapping del contenuto della rete CDN a un dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="b3070-160">How to Map CDN Content to a Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="b3070-161">Precaricamento di risorse in un endpoint della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="b3070-161">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="b3070-162">Ripulire un endpoint della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="b3070-162">Purge an Azure CDN Endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="b3070-163">Risoluzione dei problemi degli endpoint della rete CDN che restituiscono stati 404</span><span class="sxs-lookup"><span data-stu-id="b3070-163">Troubleshooting CDN endpoints returning 404 statuses</span></span>](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
