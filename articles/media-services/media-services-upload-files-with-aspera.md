---
title: Caricare file in un account Servizi multimediali di Azure usando Aspera | Documentazione Microsoft
description: "Questa esercitazione viene illustrata la procedura di caricamento di file in un account di archiviazione è associato a un account di servizi multimediali con il * * il servizio Aspera Server su richiesta * * in Azure."
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
ms.openlocfilehash: e3090da9b2c5b8f99545a1f7f9601bfd8d5221f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-the-aspera-server-on-demand-service-on-azure"></a><span data-ttu-id="e4f62-103">Caricare file in un account Servizi multimediali usando il servizio Aspera Server On Demand in Azure</span><span class="sxs-lookup"><span data-stu-id="e4f62-103">Upload files into a Media Services account using the Aspera Server On Demand service on Azure</span></span>

## <a name="overview"></a><span data-ttu-id="e4f62-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e4f62-104">Overview</span></span>

<span data-ttu-id="e4f62-105">**Aspera** è un software di trasferimento di file ad alta velocità.</span><span class="sxs-lookup"><span data-stu-id="e4f62-105">**Aspera** is a high-speed file transfer software.</span></span> <span data-ttu-id="e4f62-106">**Aspera Server On Demand** per Azure consente il caricamento ad alta velocità e il download di file di grandi dimensioni direttamente nell'archivio di oggetti BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f62-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span></span> <span data-ttu-id="e4f62-107">Per informazioni su **Aspera On Demand**, vedere il sito [Aspera Cloud](http://cloud.asperasoft.com/).</span><span class="sxs-lookup"><span data-stu-id="e4f62-107">For information about **Aspera On Demand**, see the [Aspera Cloud](http://cloud.asperasoft.com/) site.</span></span> 
  
<span data-ttu-id="e4f62-108">**Aspera Server On Demand** per Azure è acquistabile in [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/).</span><span class="sxs-lookup"><span data-stu-id="e4f62-108">**Aspera Server On Demand** for Azure is available for purchase from the [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span></span> <span data-ttu-id="e4f62-109">Per completare un acquisto di **Aspera Server On Demand** per Azure, accedere ad Azure Marketplace con il Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="e4f62-109">In order to complete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span></span>

<span data-ttu-id="e4f62-110">Questa esercitazione illustra la procedura per caricare file in un account di archiviazione associato a un account Servizi multimediali usando il servizio **Aspera Server On Demand** in Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f62-110">This tutorial walks you through the steps of uploading files into a storage account that is associated with a Media Services account using the **Aspera Server On Demand** service on Azure.</span></span> 

<span data-ttu-id="e4f62-111">Per un esempio che illustra come usare le funzioni di Azure con Aspera e Servizi multimediali, vedere [qui](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span><span class="sxs-lookup"><span data-stu-id="e4f62-111">You can find an example that shows how to use Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span></span>

>[!NOTE]
><span data-ttu-id="e4f62-112">È previsto un limite per le dimensioni massime dei file supportate per l'elaborazione con i processori di contenuti multimediali di Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f62-112">There is a limit to the maximum file size supported for processing with Azure Media Services media processors (MPs).</span></span> <span data-ttu-id="e4f62-113">Vedere [questo](media-services-quotas-and-limitations.md) argomento per informazioni dettagliate sulla limitazione per le dimensioni dei file.</span><span class="sxs-lookup"><span data-stu-id="e4f62-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="e4f62-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e4f62-114">Prerequisites</span></span> 

<span data-ttu-id="e4f62-115">Per completare questa esercitazione, sono necessari:</span><span class="sxs-lookup"><span data-stu-id="e4f62-115">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="e4f62-116">Un Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="e4f62-116">A Windows Live ID</span></span>
* <span data-ttu-id="e4f62-117">Un [account Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e4f62-117">An [Azure account](https://azure.microsoft.com).</span></span> <span data-ttu-id="e4f62-118">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e4f62-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="e4f62-119">Un [account Servizi multimediali di Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="e4f62-119">An [Azure Media Services account](media-services-portal-create-account.md).</span></span>

## <a name="purchase-aspera-on-demand-for-azure"></a><span data-ttu-id="e4f62-120">Acquistare Aspera On Demand per Azure</span><span class="sxs-lookup"><span data-stu-id="e4f62-120">Purchase Aspera On Demand for Azure</span></span>

<span data-ttu-id="e4f62-121">Dopo l'accesso ad Azure Marketplace, seguire questi semplici passaggi per completare l'acquisto di Aspera On Demand per Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f62-121">Once you have logged into Azure Marketplace,  follow these basic steps to complete your purchase of Aspera On Demand for Azure.</span></span>

1. <span data-ttu-id="e4f62-122">Cercare Aspera e selezionare "Server On Demand".</span><span class="sxs-lookup"><span data-stu-id="e4f62-122">Search for Aspera and select 'Server On Demand'.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. <span data-ttu-id="e4f62-124">Esaminare i piani di sottoscrizione e fare clic su "Iscriviti".</span><span class="sxs-lookup"><span data-stu-id="e4f62-124">Review the subscription plans and click on 'Sign Up'</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. <span data-ttu-id="e4f62-126">Immettere le specifiche per la sottoscrizione di Server on Demand.</span><span class="sxs-lookup"><span data-stu-id="e4f62-126">Fill in the specifics for your Server on Demand subscription.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. <span data-ttu-id="e4f62-128">Fare clic su **Piano tariffario** e selezionare il volume mensile desiderato nel pannello secondario.</span><span class="sxs-lookup"><span data-stu-id="e4f62-128">Click on the **Pricing Tier** and select your desired monthly volume in the sub panel.</span></span> <span data-ttu-id="e4f62-129">Nel pannello **Plan details** (Dettagli piano) fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4f62-129">In the **Plan details** panel, select **OK**.</span></span> <span data-ttu-id="e4f62-130">Nel pannello **Scegliere il piano tariffario** fare quindi clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="e4f62-130">Then, in the **Choose your Pricing Tier** panel, click **Select**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. <span data-ttu-id="e4f62-132">Fare clic su **Note legali** per visualizzare e accettare le note legali nel pannello secondario.</span><span class="sxs-lookup"><span data-stu-id="e4f62-132">Click on **Legal terms** to view and accept the legal terms in the sub panel.</span></span> <span data-ttu-id="e4f62-133">Dopo avere esaminato le note legali, fare clic su **Acquisto**.</span><span class="sxs-lookup"><span data-stu-id="e4f62-133">Once you have reviewed the legal terms, click **Purchase**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. <span data-ttu-id="e4f62-135">Completare l'acquisto facendo clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e4f62-135">Complete the purchase by clicking **Create**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. <span data-ttu-id="e4f62-137">Il dashboard di Azure informerà che è in corso il provisioning del servizio.</span><span class="sxs-lookup"><span data-stu-id="e4f62-137">The Azure dashboard will announce that it is provisioning the service.</span></span>  <span data-ttu-id="e4f62-138">Al termine del provisioning, è possibile trovare la nuova sottoscrizione cercando nelle risorse il nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="e4f62-138">Once it is completed with provisioning, you can find the new subscription by searching in your resources for the name of the service.</span></span> <span data-ttu-id="e4f62-139">Dopo averlo trovato, fare doppio clic sul servizio per avviare il portale di gestione del servizio.</span><span class="sxs-lookup"><span data-stu-id="e4f62-139">Once you have found the service, double click on it to launch the service management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. <span data-ttu-id="e4f62-141">Avviare il portale di gestione di Aspera.</span><span class="sxs-lookup"><span data-stu-id="e4f62-141">Launch the Aspera management portal.</span></span> <span data-ttu-id="e4f62-142">Dopo avere trovato il nuovo servizio Aspera, è possibile accedere al portale di gestione facendo clic sul servizio.</span><span class="sxs-lookup"><span data-stu-id="e4f62-142">Once you have found your new Aspera service, you can gain access to the management portal, by clicking on the service.</span></span>  <span data-ttu-id="e4f62-143">Verrà aperto un nuovo pannello.</span><span class="sxs-lookup"><span data-stu-id="e4f62-143">A new panel will be launched.</span></span> <span data-ttu-id="e4f62-144">In questo nuovo pannello è necessario fare clic sul **nome della risorsa** del nuovo servizio.</span><span class="sxs-lookup"><span data-stu-id="e4f62-144">From within that new panel, you need to click on the **Resource Name** of your new service.</span></span>  <span data-ttu-id="e4f62-145">Nello screenshot seguente il nome della risorsa è "AsperaTransferDemo".</span><span class="sxs-lookup"><span data-stu-id="e4f62-145">In the following screenshot, the resource name is 'AsperaTransferDemo'.</span></span> <span data-ttu-id="e4f62-146">Dopo avere fatto clic sul nome della risorsa, viene aperto un altro pannello.</span><span class="sxs-lookup"><span data-stu-id="e4f62-146">Once you click on the resource name, another panel is launched.</span></span> <span data-ttu-id="e4f62-147">Nel nuovo pannello aperto sarà visualizzato un collegamento "Manage" (Gestisci).</span><span class="sxs-lookup"><span data-stu-id="e4f62-147">In that newly launched panel, you will see a 'Manage' link.</span></span> <span data-ttu-id="e4f62-148">Fare clic sul collegamento "Manage" (Gestisci) per avviare il portale di gestione di Aspera.</span><span class="sxs-lookup"><span data-stu-id="e4f62-148">Click on the 'Manage' link to launch the Aspera management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. <span data-ttu-id="e4f62-150">Facendo clic sul collegamento Manage (Gestisci), si aprirà la pagina di registrazione, necessaria per accedere al servizio.</span><span class="sxs-lookup"><span data-stu-id="e4f62-150">By clicking on the manage link, you will get to the registration page, which is required to access the service.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. <span data-ttu-id="e4f62-152">A questo punto, si avrà accesso al portale di gestione del servizio Aspera, dove è possibile creare chiavi di accesso, scaricare client e licenze di Aspera, visualizzare l'utilizzo e trovare informazioni sulle API.</span><span class="sxs-lookup"><span data-stu-id="e4f62-152">At this point, you should have access to the Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about the APIs.</span></span>

    <span data-ttu-id="e4f62-153">Lo screenshot seguente illustra la creazione dell'accesso.</span><span class="sxs-lookup"><span data-stu-id="e4f62-153">The following screenshot shows the access creation.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    <span data-ttu-id="e4f62-155">Lo screenshot seguente illustra le interfacce di creazione di report sull'utilizzo nel portale.</span><span class="sxs-lookup"><span data-stu-id="e4f62-155">The following screenshot shows the usage reporting interfaces in the portal.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a><span data-ttu-id="e4f62-157">Caricare file con Aspera</span><span class="sxs-lookup"><span data-stu-id="e4f62-157">Upload files with Aspera</span></span>

1. <span data-ttu-id="e4f62-158">Scaricare e installare il software client Aspera:</span><span class="sxs-lookup"><span data-stu-id="e4f62-158">Download and install the Aspera client software:</span></span>
    
    * [<span data-ttu-id="e4f62-159">Plug-in del browser</span><span class="sxs-lookup"><span data-stu-id="e4f62-159">Browser plugin</span></span>](http://downloads.asperasoft.com/connect2/)
    * [<span data-ttu-id="e4f62-160">Rich client</span><span class="sxs-lookup"><span data-stu-id="e4f62-160">Rich client</span></span>](http://downloads.asperasoft.com/en/downloads/2)

2. <span data-ttu-id="e4f62-161">Eseguire il primo trasferimento.</span><span class="sxs-lookup"><span data-stu-id="e4f62-161">Make your first transfer.</span></span> <span data-ttu-id="e4f62-162">Per usare il client Aspera per il trasferimento con il servizio di trasferimento Aspera, è necessario completare le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e4f62-162">In order to use the Aspera client to transfer with the Aspera transfer service, you need to complete the following:</span></span> 

    1. <span data-ttu-id="e4f62-163">Creare una chiave di accesso usando il portale di Aspera.</span><span class="sxs-lookup"><span data-stu-id="e4f62-163">Create an access key, using the Aspera portal.</span></span>  
    2. <span data-ttu-id="e4f62-164">Scaricare, installare e concedere in licenza il client Aspera. Il software è disponibile nel portale di Aspera.</span><span class="sxs-lookup"><span data-stu-id="e4f62-164">Download, install, and license the Aspera client (software can be found in the Aspera portal).</span></span>  

    >[!NOTE]
    ><span data-ttu-id="e4f62-165">Leggere la guida al client Aspera per informazioni sulla configurazione.</span><span class="sxs-lookup"><span data-stu-id="e4f62-165">Please read the Aspera client guide for configuration information.</span></span>
    
    3. <span data-ttu-id="e4f62-166">Recuperare alcune informazioni dell'account di archiviazione associato all'account multimediale di Azure usando il [portale di Azure](https://portal.azure.com/),</span><span class="sxs-lookup"><span data-stu-id="e4f62-166">Retrieve some information of your storage account that is associated with your Azure Media Account using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="e4f62-167">in particolare il nome e la chiave e il nome del contenitore BLOB di archiviazione in cui si vuole inserire il contenuto.</span><span class="sxs-lookup"><span data-stu-id="e4f62-167">Specifically, name and key, and the storage blob container name in to which you want to place your content.</span></span> 

        * <span data-ttu-id="e4f62-168">Per ottenere le informazioni di archiviazione dal portale: trovare l'account di archiviazione, fare clic sulle chiavi di accesso e copiare il nome e la chiave dell'account.</span><span class="sxs-lookup"><span data-stu-id="e4f62-168">To get the storage info from the portal: find your storage account, click on the Access keys and copy the name and the key of your account.</span></span>
        * <span data-ttu-id="e4f62-169">Per ottenere il nome del contenitore: trovare l'account di archiviazione, selezionare **Blobs** (BLOB) e selezionare il nome del contenitore in cui si vuole caricare il contenuto.</span><span class="sxs-lookup"><span data-stu-id="e4f62-169">To get the container name: find your storage account, select **Blobs**, select the name of the container you want to upload the content into.</span></span> 

    <span data-ttu-id="e4f62-170">Il seguente è lo screenshot del client Aspera **Connection Manager** (Gestione connessioni) in cui è necessario specificare il tipo di archiviazione "Azure" e le credenziali, oltre al contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="e4f62-170">Below is the screenshot of the Aspera client **Connection Manager** where you must specify the 'Azure' storage type and credentials as well as the blob container.</span></span>

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a><span data-ttu-id="e4f62-172">Risorse</span><span class="sxs-lookup"><span data-stu-id="e4f62-172">Resources</span></span>

<span data-ttu-id="e4f62-173">Le risorse seguenti sono state citate in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e4f62-173">The following resources were mentioned in this article.</span></span> 

* [<span data-ttu-id="e4f62-174">Collegare il plug-in del browser</span><span class="sxs-lookup"><span data-stu-id="e4f62-174">Connect Browser Plugin</span></span>](http://downloads.asperasoft.com/connect2/)
* [<span data-ttu-id="e4f62-175">Guida alla connessione</span><span class="sxs-lookup"><span data-stu-id="e4f62-175">Connect Guide</span></span>](http://downloads.asperasoft.com/en/documentation/8)
* [<span data-ttu-id="e4f62-176">Client Aspera</span><span class="sxs-lookup"><span data-stu-id="e4f62-176">Aspera Client</span></span>](http://downloads.asperasoft.com/en/downloads/2)
* [<span data-ttu-id="e4f62-177">Guida al client</span><span class="sxs-lookup"><span data-stu-id="e4f62-177">Client Guide</span></span>](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a><span data-ttu-id="e4f62-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e4f62-178">Next steps</span></span>

<span data-ttu-id="e4f62-179">È ora possibile [copiare BLOB da un account di archiviazione in un account AMS](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span><span class="sxs-lookup"><span data-stu-id="e4f62-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="e4f62-180">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="e4f62-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e4f62-181">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="e4f62-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

