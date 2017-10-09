---
title: file aaaUpload in un account di servizi multimediali di Azure tramite Aspera | Documenti Microsoft
description: "In questa esercitazione illustra i passaggi hello di caricamento di file in un account di archiviazione che è associato a un account di servizi multimediali tramite hello * * il servizio Aspera Server su richiesta * * in Azure."
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a><span data-ttu-id="1312a-103">Caricare file in un account di servizi multimediali con il servizio di Aspera Server On Demand hello in Azure</span><span class="sxs-lookup"><span data-stu-id="1312a-103">Upload files into a Media Services account using hello Aspera Server On Demand service on Azure</span></span>

## <a name="overview"></a><span data-ttu-id="1312a-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1312a-104">Overview</span></span>

<span data-ttu-id="1312a-105">**Aspera** è un software di trasferimento di file ad alta velocità.</span><span class="sxs-lookup"><span data-stu-id="1312a-105">**Aspera** is a high-speed file transfer software.</span></span> <span data-ttu-id="1312a-106">**Aspera Server On Demand** per Azure consente il caricamento ad alta velocità e il download di file di grandi dimensioni direttamente nell'archivio di oggetti BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="1312a-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span></span> <span data-ttu-id="1312a-107">Per informazioni su **Aspera On Demand**, vedere hello [Aspera Cloud](http://cloud.asperasoft.com/) sito.</span><span class="sxs-lookup"><span data-stu-id="1312a-107">For information about **Aspera On Demand**, see hello [Aspera Cloud](http://cloud.asperasoft.com/) site.</span></span> 
  
<span data-ttu-id="1312a-108">**Aspera Server On Demand** per Azure è disponibile per l'acquisto di hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span><span class="sxs-lookup"><span data-stu-id="1312a-108">**Aspera Server On Demand** for Azure is available for purchase from hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span></span> <span data-ttu-id="1312a-109">Ordinare toocomplete un acquisto **Aspera Server On Demand** per Azure, accedere in Azure Marketplace con Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="1312a-109">In order toocomplete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span></span>

<span data-ttu-id="1312a-110">In questa esercitazione illustra i passaggi hello di caricamento di file in un account di archiviazione che è associato a un account di servizi multimediali tramite hello **Aspera Server On Demand** servizio in Azure.</span><span class="sxs-lookup"><span data-stu-id="1312a-110">This tutorial walks you through hello steps of uploading files into a storage account that is associated with a Media Services account using hello **Aspera Server On Demand** service on Azure.</span></span> 

<span data-ttu-id="1312a-111">È possibile trovare un esempio che illustra il funzionamento di Azure toouse con servizi multimediali e di Aspera [qui](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span><span class="sxs-lookup"><span data-stu-id="1312a-111">You can find an example that shows how toouse Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span></span>

>[!NOTE]
><span data-ttu-id="1312a-112">Vi è limite toohello dimensioni massime supportate per l'elaborazione con servizi multimediali di Azure processori di contenuti multimediali (MP).</span><span class="sxs-lookup"><span data-stu-id="1312a-112">There is a limit toohello maximum file size supported for processing with Azure Media Services media processors (MPs).</span></span> <span data-ttu-id="1312a-113">Vedere [questo](media-services-quotas-and-limitations.md) per informazioni sulla limitazione delle dimensioni del file hello.</span><span class="sxs-lookup"><span data-stu-id="1312a-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="1312a-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1312a-114">Prerequisites</span></span> 

<span data-ttu-id="1312a-115">toocomplete questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="1312a-115">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="1312a-116">Un Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="1312a-116">A Windows Live ID</span></span>
* <span data-ttu-id="1312a-117">Un [account Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="1312a-117">An [Azure account](https://azure.microsoft.com).</span></span> <span data-ttu-id="1312a-118">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1312a-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="1312a-119">Un [account Servizi multimediali di Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="1312a-119">An [Azure Media Services account](media-services-portal-create-account.md).</span></span>

## <a name="purchase-aspera-on-demand-for-azure"></a><span data-ttu-id="1312a-120">Acquistare Aspera On Demand per Azure</span><span class="sxs-lookup"><span data-stu-id="1312a-120">Purchase Aspera On Demand for Azure</span></span>

<span data-ttu-id="1312a-121">Dopo aver eseguito l'accesso in Azure Marketplace, seguire questi passaggi di base di toocomplete l'acquisto di Aspera On Demand per Azure.</span><span class="sxs-lookup"><span data-stu-id="1312a-121">Once you have logged into Azure Marketplace,  follow these basic steps toocomplete your purchase of Aspera On Demand for Azure.</span></span>

1. <span data-ttu-id="1312a-122">Cercare Aspera e selezionare "Server On Demand".</span><span class="sxs-lookup"><span data-stu-id="1312a-122">Search for Aspera and select 'Server On Demand'.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. <span data-ttu-id="1312a-124">Esaminare i piani di abbonamento hello e fare clic su 'Iscrizione'</span><span class="sxs-lookup"><span data-stu-id="1312a-124">Review hello subscription plans and click on 'Sign Up'</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. <span data-ttu-id="1312a-126">Compilare le specifiche di hello del Server per la sottoscrizione richiesta.</span><span class="sxs-lookup"><span data-stu-id="1312a-126">Fill in hello specifics for your Server on Demand subscription.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. <span data-ttu-id="1312a-128">Fare clic su hello **tariffario** e selezionare il volume mensile desiderato nel Pannello di hello sub.</span><span class="sxs-lookup"><span data-stu-id="1312a-128">Click on hello **Pricing Tier** and select your desired monthly volume in hello sub panel.</span></span> <span data-ttu-id="1312a-129">In hello **pianificare dettagli** Pannello di seleziona **OK**.</span><span class="sxs-lookup"><span data-stu-id="1312a-129">In hello **Plan details** panel, select **OK**.</span></span> <span data-ttu-id="1312a-130">Quindi, nel hello **scegliere il livello di prezzo** pannello, fare clic su **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="1312a-130">Then, in hello **Choose your Pricing Tier** panel, click **Select**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. <span data-ttu-id="1312a-132">Fare clic su **legali** tooview e accettare i termini legali specifici hello nel Pannello di hello sub.</span><span class="sxs-lookup"><span data-stu-id="1312a-132">Click on **Legal terms** tooview and accept hello legal terms in hello sub panel.</span></span> <span data-ttu-id="1312a-133">Dopo avere esaminato le note legali hello, fare clic su **acquisto**.</span><span class="sxs-lookup"><span data-stu-id="1312a-133">Once you have reviewed hello legal terms, click **Purchase**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. <span data-ttu-id="1312a-135">Completare l'acquisto di hello facendo **crea**.</span><span class="sxs-lookup"><span data-stu-id="1312a-135">Complete hello purchase by clicking **Create**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. <span data-ttu-id="1312a-137">dashboard di Azure Hello annuncerà che esegue il provisioning del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="1312a-137">hello Azure dashboard will announce that it is provisioning hello service.</span></span>  <span data-ttu-id="1312a-138">Una volta completata con il provisioning, è possibile trovare una nuova sottoscrizione hello eseguendo una ricerca delle risorse per il nome del servizio hello hello.</span><span class="sxs-lookup"><span data-stu-id="1312a-138">Once it is completed with provisioning, you can find hello new subscription by searching in your resources for hello name of hello service.</span></span> <span data-ttu-id="1312a-139">Dopo avere trovato servizio hello, fare doppio clic su di esso toolaunch hello portale.</span><span class="sxs-lookup"><span data-stu-id="1312a-139">Once you have found hello service, double click on it toolaunch hello service management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. <span data-ttu-id="1312a-141">Avviare il portale di gestione di hello Aspera.</span><span class="sxs-lookup"><span data-stu-id="1312a-141">Launch hello Aspera management portal.</span></span> <span data-ttu-id="1312a-142">Dopo aver individuato il nuovo servizio Aspera, è possibile delineare portale di gestione di accessi toohello, facendo clic sul servizio hello.</span><span class="sxs-lookup"><span data-stu-id="1312a-142">Once you have found your new Aspera service, you can gain access toohello management portal, by clicking on hello service.</span></span>  <span data-ttu-id="1312a-143">Verrà aperto un nuovo pannello.</span><span class="sxs-lookup"><span data-stu-id="1312a-143">A new panel will be launched.</span></span> <span data-ttu-id="1312a-144">Da all'interno di tale pannello nuova, è necessario tooclick su hello **nome risorsa** del nuovo servizio.</span><span class="sxs-lookup"><span data-stu-id="1312a-144">From within that new panel, you need tooclick on hello **Resource Name** of your new service.</span></span>  <span data-ttu-id="1312a-145">Nella seguente schermata di hello, il nome di risorsa hello è 'AsperaTransferDemo'.</span><span class="sxs-lookup"><span data-stu-id="1312a-145">In hello following screenshot, hello resource name is 'AsperaTransferDemo'.</span></span> <span data-ttu-id="1312a-146">Quando si fa clic sul nome di risorsa hello, viene avviato un altro pannello.</span><span class="sxs-lookup"><span data-stu-id="1312a-146">Once you click on hello resource name, another panel is launched.</span></span> <span data-ttu-id="1312a-147">Nel nuovo pannello aperto sarà visualizzato un collegamento "Manage" (Gestisci).</span><span class="sxs-lookup"><span data-stu-id="1312a-147">In that newly launched panel, you will see a 'Manage' link.</span></span> <span data-ttu-id="1312a-148">Fare clic su hello portale di gestione di Aspera hello toolaunch di collegamento 'Gestisci'.</span><span class="sxs-lookup"><span data-stu-id="1312a-148">Click on hello 'Manage' link toolaunch hello Aspera management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. <span data-ttu-id="1312a-150">Facendo clic su hello gestire collegamento, si otterrà una pagina di registrazione toohello, che è necessario tooaccess hello del servizio.</span><span class="sxs-lookup"><span data-stu-id="1312a-150">By clicking on hello manage link, you will get toohello registration page, which is required tooaccess hello service.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. <span data-ttu-id="1312a-152">A questo punto, è necessario disporre di accesso toohello Aspera servizio portale di gestione, in cui è possibile creare chiavi di accesso, scaricare le licenze e i client di Aspera, visualizzare l'utilizzo e informazioni sulle API hello.</span><span class="sxs-lookup"><span data-stu-id="1312a-152">At this point, you should have access toohello Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about hello APIs.</span></span>

    <span data-ttu-id="1312a-153">Hello figura seguente viene illustrata la creazione di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="1312a-153">hello following screenshot shows hello access creation.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    <span data-ttu-id="1312a-155">Hello seguente schermata Mostra utilizzo hello reporting interfacce nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="1312a-155">hello following screenshot shows hello usage reporting interfaces in hello portal.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a><span data-ttu-id="1312a-157">Caricare file con Aspera</span><span class="sxs-lookup"><span data-stu-id="1312a-157">Upload files with Aspera</span></span>

1. <span data-ttu-id="1312a-158">Scaricare e installare il software client di Aspera hello:</span><span class="sxs-lookup"><span data-stu-id="1312a-158">Download and install hello Aspera client software:</span></span>
    
    * [<span data-ttu-id="1312a-159">Plug-in del browser</span><span class="sxs-lookup"><span data-stu-id="1312a-159">Browser plugin</span></span>](http://downloads.asperasoft.com/connect2/)
    * [<span data-ttu-id="1312a-160">Rich client</span><span class="sxs-lookup"><span data-stu-id="1312a-160">Rich client</span></span>](http://downloads.asperasoft.com/en/downloads/2)

2. <span data-ttu-id="1312a-161">Eseguire il primo trasferimento.</span><span class="sxs-lookup"><span data-stu-id="1312a-161">Make your first transfer.</span></span> <span data-ttu-id="1312a-162">In ordine toouse hello Aspera client tootransfer con servizio trasferimento Aspera hello, è necessario seguente hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="1312a-162">In order toouse hello Aspera client tootransfer with hello Aspera transfer service, you need toocomplete hello following:</span></span> 

    1. <span data-ttu-id="1312a-163">Creare una chiave di accesso, tramite il portale di Aspera hello.</span><span class="sxs-lookup"><span data-stu-id="1312a-163">Create an access key, using hello Aspera portal.</span></span>  
    2. <span data-ttu-id="1312a-164">Download, l'installazione e client delle licenze hello Aspera (software sono disponibili nel portale di Aspera hello).</span><span class="sxs-lookup"><span data-stu-id="1312a-164">Download, install, and license hello Aspera client (software can be found in hello Aspera portal).</span></span>  

    >[!NOTE]
    ><span data-ttu-id="1312a-165">Leggere una Guida di client Aspera hello per le informazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1312a-165">Please read hello Aspera client guide for configuration information.</span></span>
    
    3. <span data-ttu-id="1312a-166">Recuperare alcune informazioni dell'account di archiviazione che è associato con l'Account di supporto di Azure tramite hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1312a-166">Retrieve some information of your storage account that is associated with your Azure Media Account using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="1312a-167">In particolare, nome e chiave e al nome contenitore blob di archiviazione hello in toowhich desiderato tooplace il contenuto.</span><span class="sxs-lookup"><span data-stu-id="1312a-167">Specifically, name and key, and hello storage blob container name in toowhich you want tooplace your content.</span></span> 

        * <span data-ttu-id="1312a-168">informazioni di archiviazione hello tooget dal portale hello: trovare account di archiviazione, fare clic sulle chiavi di accesso hello e copia hello nome e hello la chiave dell'account.</span><span class="sxs-lookup"><span data-stu-id="1312a-168">tooget hello storage info from hello portal: find your storage account, click on hello Access keys and copy hello name and hello key of your account.</span></span>
        * <span data-ttu-id="1312a-169">nome del contenitore hello tooget: trovare l'account di archiviazione, seleziona **BLOB**, selezionare il nome di hello del contenitore di hello si desidera tooupload hello contenuto in.</span><span class="sxs-lookup"><span data-stu-id="1312a-169">tooget hello container name: find your storage account, select **Blobs**, select hello name of hello container you want tooupload hello content into.</span></span> 

    <span data-ttu-id="1312a-170">Di seguito è la schermata di hello del client di Aspera hello **Connection Manager** in cui è necessario specificare il tipo di archiviazione 'Azure' hello e le credenziali, nonché il contenitore di blob hello.</span><span class="sxs-lookup"><span data-stu-id="1312a-170">Below is hello screenshot of hello Aspera client **Connection Manager** where you must specify hello 'Azure' storage type and credentials as well as hello blob container.</span></span>

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a><span data-ttu-id="1312a-172">Risorse</span><span class="sxs-lookup"><span data-stu-id="1312a-172">Resources</span></span>

<span data-ttu-id="1312a-173">Hello seguenti risorse è citata in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="1312a-173">hello following resources were mentioned in this article.</span></span> 

* [<span data-ttu-id="1312a-174">Collegare il plug-in del browser</span><span class="sxs-lookup"><span data-stu-id="1312a-174">Connect Browser Plugin</span></span>](http://downloads.asperasoft.com/connect2/)
* [<span data-ttu-id="1312a-175">Guida alla connessione</span><span class="sxs-lookup"><span data-stu-id="1312a-175">Connect Guide</span></span>](http://downloads.asperasoft.com/en/documentation/8)
* [<span data-ttu-id="1312a-176">Client Aspera</span><span class="sxs-lookup"><span data-stu-id="1312a-176">Aspera Client</span></span>](http://downloads.asperasoft.com/en/downloads/2)
* [<span data-ttu-id="1312a-177">Guida al client</span><span class="sxs-lookup"><span data-stu-id="1312a-177">Client Guide</span></span>](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a><span data-ttu-id="1312a-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1312a-178">Next steps</span></span>

<span data-ttu-id="1312a-179">È ora possibile [copiare BLOB da un account di archiviazione in un account AMS](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span><span class="sxs-lookup"><span data-stu-id="1312a-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="1312a-180">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1312a-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1312a-181">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="1312a-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

