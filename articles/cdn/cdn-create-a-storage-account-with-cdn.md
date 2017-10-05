---
title: Integrare un account di archiviazione di Azure con la rete CDN di Azure | Documentazione Microsoft
description: Informazioni su come usare la rete per la distribuzione di contenuti (rete CDN) di Azure per distribuire contenuto con esigenze di larghezza di banda elevata, tramite la memorizzazione nella cache di BLOB da Archiviazione di Azure.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 511076935d06ed0908341044e37069e74530be49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="7302d-103">Integrare un account di archiviazione di Azure con la rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="7302d-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="7302d-104">È possibile abilitare la rete CDN per memorizzare nella cache i contenuti delle risorse di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7302d-104">CDN can be enabled to cache content from your Azure storage.</span></span> <span data-ttu-id="7302d-105">Questa rete offre agli sviluppatori una soluzione globale per il recapito di contenuto con esigenze di larghezza di banda elevata, tramite la memorizzazione nella cache di oggetti BLOB e contenuto statico di istanze di calcolo in nodi fisici negli Stati Uniti, in Europa, Asia, Australia e Sud America.</span><span class="sxs-lookup"><span data-stu-id="7302d-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in the United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="7302d-106">Passaggio 1: Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="7302d-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="7302d-107">Usare la procedura seguente per creare un nuovo account di archiviazione per una sottoscrizione ad Azure.</span><span class="sxs-lookup"><span data-stu-id="7302d-107">Use the following procedure to create a new storage account for a Azure subscription.</span></span> <span data-ttu-id="7302d-108">Un account di archiviazione consente di accedere ai servizi di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7302d-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="7302d-109">L'account di archiviazione rappresenta il livello più elevato dello spazio dei nomi per l'accesso a ogni componente dei servizi di archiviazione di Azure, ovvero servizi BLOB, servizi di accodamento e servizi tabelle.</span><span class="sxs-lookup"><span data-stu-id="7302d-109">The storage account represents the highest level of the namespace for accessing each of the Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="7302d-110">Per altre informazioni, fare riferimento a [Introduzione ad Archiviazione di Microsoft Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7302d-110">For more information, refer to the [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="7302d-111">Per creare un account di archiviazione, è necessario essere amministratori del servizio o coamministratori della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7302d-111">To create a storage account, you must be either the service administrator or a co-administrator for the associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="7302d-112">Esistono diversi metodi che è possibile usare per creare un account di archiviazione, compresi il portale di Azure e Powershell.</span><span class="sxs-lookup"><span data-stu-id="7302d-112">There are several methods you can use to create a storage account, including the Azure Portal and Powershell.</span></span>  <span data-ttu-id="7302d-113">Per questa esercitazione, verrà utilizzato il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7302d-113">For this tutorial, we'll be using the Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="7302d-114">**Per creare un account di archiviazione per una sottoscrizione di Azure**</span><span class="sxs-lookup"><span data-stu-id="7302d-114">**To create a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="7302d-115">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7302d-115">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7302d-116">Nell'angolo in alto a sinistra della schermata fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="7302d-116">In the upper left corner, select **New**.</span></span> <span data-ttu-id="7302d-117">Nella finestra di dialogo **Nuovo** selezionare **Dati e archiviazione**, quindi fare clic su **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="7302d-117">In the **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="7302d-118">Viene visualizzato il pannello **Crea account di archiviazione** .</span><span class="sxs-lookup"><span data-stu-id="7302d-118">The **Create storage account** blade appears.</span></span>   

    ![Crea account di archiviazione][create-new-storage-account]  

3. <span data-ttu-id="7302d-120">Nel campo **Nome** digitare il nome di un sottodominio.</span><span class="sxs-lookup"><span data-stu-id="7302d-120">In the **Name** field, type a subdomain name.</span></span> <span data-ttu-id="7302d-121">Il nome può contenere tra 3 e 24 lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="7302d-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="7302d-122">Questo valore diventa il nome host all'interno dell'URI usato per fare riferimento a risorse BLOB, di accodamento o tabelle per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7302d-122">This value becomes the host name within the URI that is used to address Blob, Queue, or Table resources for the subscription.</span></span> <span data-ttu-id="7302d-123">Per fare riferimento a una risorsa contenitore nel servizio BLOB, usare un URI con il formato seguente, dove *&lt;EtichettaAccountArchiviazione&gt;* corrisponde al valore immesso in **Immettere un URL**:</span><span class="sxs-lookup"><span data-stu-id="7302d-123">To address a container resource in the Blob service, you would use a URI in the following format, where *&lt;StorageAccountLabel&gt;* refers to the value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="7302d-124">http://*&lt;EtichettaAccountArchiviazione&gt;*.blob.core.windows.net/*&lt;contenitorepersonale&gt;*</span><span class="sxs-lookup"><span data-stu-id="7302d-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="7302d-125">**Importante:** l'etichetta dell'URL costituisce il sottodominio dell'URI dell'account di archiviazione e deve essere univoca in tutti i servizi ospitati in Azure.</span><span class="sxs-lookup"><span data-stu-id="7302d-125">**Important:** The URL label forms the subdomain of the storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="7302d-126">Questo valore viene usato anche come nome dell'account di archiviazione nel portale o quando si accede a questo account a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="7302d-126">This value is also used as the name of this storage account in the portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="7302d-127">Lasciare le impostazioni predefinite per **Modello di distribuzione**, **Tipologia account**, **Prestazioni** e **Replica**.</span><span class="sxs-lookup"><span data-stu-id="7302d-127">Leave the defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="7302d-128">Selezionare la **Sottoscrizione** con cui verrà usato l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7302d-128">Select the **Subscription** that the storage account will be used with.</span></span>
6. <span data-ttu-id="7302d-129">Selezionare o creare un **gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="7302d-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="7302d-130">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="7302d-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="7302d-131">Selezionare la località per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7302d-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="7302d-132">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7302d-132">Click **Create**.</span></span> <span data-ttu-id="7302d-133">Il completamento del processo di creazione dell'account di archiviazione potrebbe richiedere diversi minuti.</span><span class="sxs-lookup"><span data-stu-id="7302d-133">The process of creating the storage account might take several minutes to complete.</span></span>

## <a name="step-2-enable-cdn-for-the-storage-account"></a><span data-ttu-id="7302d-134">Passaggio 2: Abilitare la rete CDN per l'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="7302d-134">Step 2: Enable CDN for the storage account</span></span>

<span data-ttu-id="7302d-135">Grazie all'integrazione più recente, è ora possibile abilitare la rete CDN per l'account di archiviazione senza lasciare l'estensione del portale di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7302d-135">With the newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="7302d-136">Selezionare l'account di archiviazione, cercare "CDN" o scorrere verso il basso dal menu di navigazione a sinistra, quindi fare clic su "Rete CDN di Azure".</span><span class="sxs-lookup"><span data-stu-id="7302d-136">Select the storage account, search "CDN" or scroll down from the left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="7302d-137">Viene visualizzato il pannello **Rete CDN di Azure**.</span><span class="sxs-lookup"><span data-stu-id="7302d-137">The **Azure CDN** blade appears.</span></span>

    ![spostamento per l'abilitazione della rete CDN][cdn-enable-navigation]
    
2. <span data-ttu-id="7302d-139">Creare un nuovo endpoint immettendo le informazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="7302d-139">Create a new endpoint by entering the required information</span></span>
    - <span data-ttu-id="7302d-140">**Profilo CDN**: è possibile creare un nuovo profilo o usarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="7302d-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="7302d-141">**Piano tariffario**: è possibile selezionare un piano tariffario solo se si crea un nuovo profilo CDN.</span><span class="sxs-lookup"><span data-stu-id="7302d-141">**Pricing tier**: You only need to select a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="7302d-142">**Nome endpoint rete CDN** : immettere un nome dell'endpoint a scelta.</span><span class="sxs-lookup"><span data-stu-id="7302d-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="7302d-143">L'endpoint della rete CDN creato utilizza il nome host dell'account di archiviazione come origine per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="7302d-143">The created CDN endpoint uses the hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="7302d-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span><span class="sxs-lookup"><span data-stu-id="7302d-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="7302d-145">Dopo la creazione, il nuovo endpoint verrà visualizzato nell'elenco degli endpoint sopra riportato.</span><span class="sxs-lookup"><span data-stu-id="7302d-145">After creation, the new endpoint will show up in the endpoint list above.</span></span>

    ![nuovo endpoint di archiviazione rete CDN][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="7302d-147">È anche possibile andare all'estensione Rete CDN di Azure per abilitare CDN.[Esercitazione](#Tutorial-cdn-create-profile).</span><span class="sxs-lookup"><span data-stu-id="7302d-147">You can also go to Azure CDN extension to enable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="7302d-148">Passaggio 3: Abilitare funzionalità aggiuntive della rete CDN</span><span class="sxs-lookup"><span data-stu-id="7302d-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="7302d-149">Dal pannello "Rete CDN di Azure" dell'account di archiviazione fare clic sull'endpoint della rete CDN dall'elenco per aprire il pannello di configurazione della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="7302d-149">From storage account "Azure CDN" blade, click the CDN endpoint from the list to open CDN configuration blade.</span></span> <span data-ttu-id="7302d-150">È possibile abilitare funzionalità aggiuntive della rete CDN per il recapito, ad esempio la compressione, la stringa di query, il filtro geografico.</span><span class="sxs-lookup"><span data-stu-id="7302d-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="7302d-151">È inoltre possibile aggiungere mapping dominio personalizzato all'endpoint della rete CDN e abilitare HTTPS per il dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="7302d-151">You can also add custom domain mapping to your CDN endpoint and enable custom domain HTTPS.</span></span>
    
![configurazione CDN di archiviazione della rete CDN][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="7302d-153">Passaggio 4: Accedere al contenuto della rete CDN</span><span class="sxs-lookup"><span data-stu-id="7302d-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="7302d-154">Per accedere al contenuto memorizzato nella cache nella rete CDN, usare l'URL della rete CDN specificato nel portale.</span><span class="sxs-lookup"><span data-stu-id="7302d-154">To access cached content on the CDN, use the CDN URL provided in the portal.</span></span> <span data-ttu-id="7302d-155">L'indirizzo per un oggetto BLOB memorizzato nella cache sarà analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="7302d-155">The address for a cached blob will be similar to the following:</span></span>

<span data-ttu-id="7302d-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span><span class="sxs-lookup"><span data-stu-id="7302d-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="7302d-157">Dopo l'abilitazione dell'accesso della rete CDN a un account di archiviazione, tutti gli oggetti disponibili pubblicamente saranno idonei per la memorizzazione nella cache perimetrale della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="7302d-157">Once you enable CDN access to a storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="7302d-158">Se si modifica un oggetto attualmente memorizzato nella cache nella rete CDN, il nuovo contenuto sarà disponibile tramite la rete CDN solo dopo l'aggiornamento dei contenuti della rete CDN alla scadenza della durata specificata per i contenuti memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="7302d-158">If you modify an object that is currently cached in the CDN, the new content will not be available via the CDN until the CDN refreshes its content when the cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-the-cdn"></a><span data-ttu-id="7302d-159">Passaggio 5: rimuovere contenuto dalla rete CDN</span><span class="sxs-lookup"><span data-stu-id="7302d-159">Step 5: Remove content from the CDN</span></span>
<span data-ttu-id="7302d-160">Se non si desidera più memorizzare un oggetto nella cache della rete per la distribuzione di contenuti (rete CDN) di Azure, è possibile eseguire una delle operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7302d-160">If you no longer wish to cache an object in the Azure Content Delivery Network (CDN), you can take one of the following steps:</span></span>

* <span data-ttu-id="7302d-161">È possibile rendere privato il contenitore, invece di pubblico.</span><span class="sxs-lookup"><span data-stu-id="7302d-161">You can make the container private instead of public.</span></span> <span data-ttu-id="7302d-162">Per altre informazioni, vedere [Gestire l'accesso in lettura anonimo a contenitori e BLOB](../storage/blobs/storage-manage-access-to-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="7302d-162">See [Manage anonymous read access to containers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="7302d-163">È possibile disabilitare o eliminare l'endpoint della rete CDN usando il portale di gestione.</span><span class="sxs-lookup"><span data-stu-id="7302d-163">You can disable or delete the CDN endpoint using the Management Portal.</span></span>
* <span data-ttu-id="7302d-164">È possibile modificare il servizio ospitato, in modo che non risponda più a richieste per l'oggetto.</span><span class="sxs-lookup"><span data-stu-id="7302d-164">You can modify your hosted service to no longer respond to requests for the object.</span></span>

<span data-ttu-id="7302d-165">Un oggetto già memorizzato nella cache della rete CDN rimarrà nella cache fino alla scadenza della durata prevista per l'oggetto o fino a quando l’endpoint non verrà eliminato.</span><span class="sxs-lookup"><span data-stu-id="7302d-165">An object already cached in the CDN will remain cached until the time-to-live period for the object expires or until the endpoint is purged.</span></span> <span data-ttu-id="7302d-166">Al termine della durata prevista, la rete CDN verificherà se l'endpoint della rete CDN è ancora valido e se l'oggetto è ancora accessibile in modo anonimo.</span><span class="sxs-lookup"><span data-stu-id="7302d-166">When the time-to-live period expires, the CDN will check to see whether the CDN endpoint is still valid and the object still anonymously accessible.</span></span> <span data-ttu-id="7302d-167">In caso contrario, l'oggetto non sarà più memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="7302d-167">If it is not, then the object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7302d-168">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7302d-168">Additional resources</span></span>
* [<span data-ttu-id="7302d-169">Come eseguire il mapping del contenuto della rete CDN a un dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="7302d-169">How to Map CDN Content to a Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="7302d-170">Abilitare HTTPS per il dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="7302d-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
