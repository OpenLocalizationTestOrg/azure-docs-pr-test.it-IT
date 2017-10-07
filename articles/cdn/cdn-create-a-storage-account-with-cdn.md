---
title: un account di archiviazione di Azure con la rete CDN Azure aaaIntegrate | Documenti Microsoft
description: Informazioni su come contenuto di toouse hello rete recapito contenuti (CDN) di Azure toodeliver larghezza di banda elevata memorizzando nella cache BLOB dall'archiviazione di Azure.
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
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="527b6-103">Integrare un account di archiviazione di Azure con la rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="527b6-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="527b6-104">Rete CDN può essere abilitato toocache contenuto lo spazio di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="527b6-104">CDN can be enabled toocache content from your Azure storage.</span></span> <span data-ttu-id="527b6-105">Offre agli sviluppatori una soluzione globale per recapitare contenuti di larghezza di banda elevata memorizzando nella cache BLOB e il contenuto statico delle istanze di calcolo in nodi fisici di hello Uniti, Europa, Asia, Australia e del Sud America.</span><span class="sxs-lookup"><span data-stu-id="527b6-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in hello United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="527b6-106">Passaggio 1: Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="527b6-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="527b6-107">Utilizzare hello seguendo procedure toocreate un nuovo account di archiviazione per una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="527b6-107">Use hello following procedure toocreate a new storage account for a Azure subscription.</span></span> <span data-ttu-id="527b6-108">Un account di archiviazione consente di accedere ai servizi di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="527b6-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="527b6-109">account di archiviazione Hello rappresenta livello più elevato di hello dello spazio dei nomi di hello per accedere a ognuno dei componenti del servizio di archiviazione di Azure hello: Blob services, servizi di coda e i servizi di tabella.</span><span class="sxs-lookup"><span data-stu-id="527b6-109">hello storage account represents hello highest level of hello namespace for accessing each of hello Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="527b6-110">Per ulteriori informazioni, vedere toohello [tooMicrosoft introduzione di archiviazione di Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="527b6-110">For more information, refer toohello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="527b6-111">toocreate un account di archiviazione, è necessario essere amministratore del servizio hello o un coamministratore per hello associata sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="527b6-111">toocreate a storage account, you must be either hello service administrator or a co-administrator for hello associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="527b6-112">Esistono diversi metodi che è possibile utilizzare un account di archiviazione, tra cui hello portale di Azure e Powershell toocreate.</span><span class="sxs-lookup"><span data-stu-id="527b6-112">There are several methods you can use toocreate a storage account, including hello Azure Portal and Powershell.</span></span>  <span data-ttu-id="527b6-113">Per questa esercitazione, verrà usato hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="527b6-113">For this tutorial, we'll be using hello Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="527b6-114">**toocreate un account di archiviazione per una sottoscrizione di Azure**</span><span class="sxs-lookup"><span data-stu-id="527b6-114">**toocreate a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="527b6-115">Accedi toohello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="527b6-115">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="527b6-116">In hello nell'angolo superiore sinistro, selezionare **New**.</span><span class="sxs-lookup"><span data-stu-id="527b6-116">In hello upper left corner, select **New**.</span></span> <span data-ttu-id="527b6-117">In hello **New** selezionare **dati e archiviazione**, quindi fare clic su **account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="527b6-117">In hello **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="527b6-118">Hello **creare account di archiviazione** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="527b6-118">hello **Create storage account** blade appears.</span></span>   

    ![Crea account di archiviazione][create-new-storage-account]  

3. <span data-ttu-id="527b6-120">In hello **nome** , digitare un nome di sottodominio.</span><span class="sxs-lookup"><span data-stu-id="527b6-120">In hello **Name** field, type a subdomain name.</span></span> <span data-ttu-id="527b6-121">Il nome può contenere tra 3 e 24 lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="527b6-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="527b6-122">Questo valore diventa il nome host hello all'interno di hello URI utilizzato per indirizzare le risorse Blob, coda o tabella per la sottoscrizione di hello.</span><span class="sxs-lookup"><span data-stu-id="527b6-122">This value becomes hello host name within hello URI that is used to address Blob, Queue, or Table resources for hello subscription.</span></span> <span data-ttu-id="527b6-123">Per risolvere una risorsa contenitore nel servizio Blob hello, si utilizzerebbe un URI nel seguente formato, hello in  *&lt;StorageAccountLabel&gt;*  toohello valore digitato in **immettere un URL**:</span><span class="sxs-lookup"><span data-stu-id="527b6-123">To address a container resource in hello Blob service, you would use a URI in hello following format, where *&lt;StorageAccountLabel&gt;* refers toohello value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="527b6-124">http://*&lt;EtichettaAccountArchiviazione&gt;*.blob.core.windows.net/*&lt;contenitorepersonale&gt;*</span><span class="sxs-lookup"><span data-stu-id="527b6-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="527b6-125">**Importante:** hello sottodominio di hello form etichetta URL dell'account di archiviazione hello URI e deve essere univoco tra tutti i servizi ospitati in Azure.</span><span class="sxs-lookup"><span data-stu-id="527b6-125">**Important:** hello URL label forms hello subdomain of hello storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="527b6-126">Questo valore è utilizzato anche come nome hello di questo account di archiviazione nel portale di hello o quando si accede a questo account a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="527b6-126">This value is also used as hello name of this storage account in hello portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="527b6-127">Lasciare i valori predefiniti di hello per **modello di distribuzione**, **Account kind**, **prestazioni**, e **replica**.</span><span class="sxs-lookup"><span data-stu-id="527b6-127">Leave hello defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="527b6-128">Seleziona hello **sottoscrizione** verrà utilizzato con account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="527b6-128">Select hello **Subscription** that hello storage account will be used with.</span></span>
6. <span data-ttu-id="527b6-129">Selezionare o creare un **gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="527b6-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="527b6-130">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="527b6-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="527b6-131">Selezionare la località per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="527b6-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="527b6-132">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="527b6-132">Click **Create**.</span></span> <span data-ttu-id="527b6-133">Hello creazione account di archiviazione hello potrebbe richiedere diversi minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="527b6-133">hello process of creating hello storage account might take several minutes toocomplete.</span></span>

## <a name="step-2-enable-cdn-for-hello-storage-account"></a><span data-ttu-id="527b6-134">Passaggio 2: Abilitare la rete CDN per account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="527b6-134">Step 2: Enable CDN for hello storage account</span></span>

<span data-ttu-id="527b6-135">Con l'integrazione più recente di hello è ora possibile abilitare rete CDN per l'account di archiviazione senza lasciare l'estensione del portale di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="527b6-135">With hello newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="527b6-136">Selezionare l'account di archiviazione hello, cercare "CDN" o scorrere verso il basso dal menu di navigazione a sinistra di hello, quindi fare clic su "Rete CDN di Azure".</span><span class="sxs-lookup"><span data-stu-id="527b6-136">Select hello storage account, search "CDN" or scroll down from hello left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="527b6-137">Hello **rete CDN di Azure** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="527b6-137">hello **Azure CDN** blade appears.</span></span>

    ![spostamento per l'abilitazione della rete CDN][cdn-enable-navigation]
    
2. <span data-ttu-id="527b6-139">Creare un nuovo endpoint immettendo le informazioni necessarie hello</span><span class="sxs-lookup"><span data-stu-id="527b6-139">Create a new endpoint by entering hello required information</span></span>
    - <span data-ttu-id="527b6-140">**Profilo CDN**: è possibile creare un nuovo profilo o usarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="527b6-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="527b6-141">**Livello di prezzo**: È necessario solo tooselect prezzi di un livello se si crea un nuovo profilo di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="527b6-141">**Pricing tier**: You only need tooselect a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="527b6-142">**Nome endpoint rete CDN** : immettere un nome dell'endpoint a scelta.</span><span class="sxs-lookup"><span data-stu-id="527b6-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="527b6-143">l'endpoint rete CDN Hello creato Usa hello nome host dell'account di archiviazione come origine per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="527b6-143">hello created CDN endpoint uses hello hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="527b6-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span><span class="sxs-lookup"><span data-stu-id="527b6-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="527b6-145">Dopo la creazione del nuovo endpoint hello verrà visualizzata nell'elenco di endpoint hello precedente.</span><span class="sxs-lookup"><span data-stu-id="527b6-145">After creation, hello new endpoint will show up in hello endpoint list above.</span></span>

    ![nuovo endpoint di archiviazione rete CDN][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="527b6-147">È anche possibile passare tooAzure CDN estensione tooenable rete CDN. [Esercitazione](#Tutorial-cdn-create-profile).</span><span class="sxs-lookup"><span data-stu-id="527b6-147">You can also go tooAzure CDN extension tooenable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="527b6-148">Passaggio 3: Abilitare funzionalità aggiuntive della rete CDN</span><span class="sxs-lookup"><span data-stu-id="527b6-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="527b6-149">Pannello "Rete CDN di Azure" account di archiviazione, fare clic su endpoint rete CDN hello dal Pannello di configurazione della rete CDN tooopen elenco hello.</span><span class="sxs-lookup"><span data-stu-id="527b6-149">From storage account "Azure CDN" blade, click hello CDN endpoint from hello list tooopen CDN configuration blade.</span></span> <span data-ttu-id="527b6-150">È possibile abilitare funzionalità aggiuntive della rete CDN per il recapito, ad esempio la compressione, la stringa di query, il filtro geografico.</span><span class="sxs-lookup"><span data-stu-id="527b6-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="527b6-151">È anche possibile aggiungere endpoint rete CDN tooyour mapping del dominio personalizzato e abilitare il dominio personalizzato HTTPS.</span><span class="sxs-lookup"><span data-stu-id="527b6-151">You can also add custom domain mapping tooyour CDN endpoint and enable custom domain HTTPS.</span></span>
    
![configurazione CDN di archiviazione della rete CDN][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="527b6-153">Passaggio 4: Accedere al contenuto della rete CDN</span><span class="sxs-lookup"><span data-stu-id="527b6-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="527b6-154">tooaccess memorizzato nella cache il contenuto nella rete CDN hello, utilizzare hello URL della rete CDN fornito nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="527b6-154">tooaccess cached content on hello CDN, use hello CDN URL provided in hello portal.</span></span> <span data-ttu-id="527b6-155">indirizzo di Hello per un blob memorizzato nella cache sarà simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="527b6-155">hello address for a cached blob will be similar toohello following:</span></span>

<span data-ttu-id="527b6-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span><span class="sxs-lookup"><span data-stu-id="527b6-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="527b6-157">Dopo aver abilitato l'account di archiviazione tooa accesso alla rete CDN, tutti gli oggetti disponibili pubblicamente sono idonei per la memorizzazione nella cache perimetrale della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="527b6-157">Once you enable CDN access tooa storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="527b6-158">Se si modifica un oggetto attualmente memorizzato nella cache di hello CDN, il nuovo contenuto hello non sarà disponibile tramite hello CDN fino a quando non hello CDN consente di aggiornare il contenuto quando scade il periodo time-to-live del contenuto memorizzato nella cache di hello.</span><span class="sxs-lookup"><span data-stu-id="527b6-158">If you modify an object that is currently cached in hello CDN, hello new content will not be available via hello CDN until hello CDN refreshes its content when hello cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a><span data-ttu-id="527b6-159">Passaggio 5: Rimuovere contenuto dalla rete CDN hello</span><span class="sxs-lookup"><span data-stu-id="527b6-159">Step 5: Remove content from hello CDN</span></span>
<span data-ttu-id="527b6-160">Se non si desidera più toocache un oggetto in hello Azure rete CDN (Content Delivery), è possibile eseguire una delle hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="527b6-160">If you no longer wish toocache an object in hello Azure Content Delivery Network (CDN), you can take one of hello following steps:</span></span>

* <span data-ttu-id="527b6-161">È possibile apportare hello contenitore privato anziché pubblico.</span><span class="sxs-lookup"><span data-stu-id="527b6-161">You can make hello container private instead of public.</span></span> <span data-ttu-id="527b6-162">Vedere [gestire BLOB e accesso in lettura anonimo toocontainers](../storage/blobs/storage-manage-access-to-resources.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="527b6-162">See [Manage anonymous read access toocontainers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="527b6-163">È possibile disabilitare o eliminare l'endpoint rete CDN hello utilizzando hello portale di gestione.</span><span class="sxs-lookup"><span data-stu-id="527b6-163">You can disable or delete hello CDN endpoint using hello Management Portal.</span></span>
* <span data-ttu-id="527b6-164">È possibile modificare il toorequests di rispondere più servizio ospitato toono per oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="527b6-164">You can modify your hosted service toono longer respond toorequests for hello object.</span></span>

<span data-ttu-id="527b6-165">Un oggetto già memorizzato nella cache di hello CDN rimarrà memorizzato fino alla scadenza del periodo di time-to-live hello per oggetto hello o fino a quando non vengono eliminati l'endpoint di hello.</span><span class="sxs-lookup"><span data-stu-id="527b6-165">An object already cached in hello CDN will remain cached until hello time-to-live period for hello object expires or until hello endpoint is purged.</span></span> <span data-ttu-id="527b6-166">Allo scadere hello time-to-live, hello CDN controllerà toosee se l'endpoint rete CDN hello è ancora valido e oggetto hello ancora accessibile in modo anonimo.</span><span class="sxs-lookup"><span data-stu-id="527b6-166">When hello time-to-live period expires, hello CDN will check toosee whether hello CDN endpoint is still valid and hello object still anonymously accessible.</span></span> <span data-ttu-id="527b6-167">In caso contrario, non verrà memorizzata non più oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="527b6-167">If it is not, then hello object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="527b6-168">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="527b6-168">Additional resources</span></span>
* [<span data-ttu-id="527b6-169">Come tooMap CDN contenuto tooa dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="527b6-169">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="527b6-170">Abilitare HTTPS per il dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="527b6-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
