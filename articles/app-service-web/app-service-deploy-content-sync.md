---
title: aaaSync contenuto da un tooAzure cartella cloud servizio App
description: Informazioni su come toodeploy tooAzure l'app del servizio App tramite il contenuto di sincronizzazione da una cartella di cloud.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: e1c6d53a427c36126d9cdb33cc21b4126b9d9c2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a><span data-ttu-id="daf29-103">Sincronizza il contenuto da un tooAzure cartella cloud servizio App</span><span class="sxs-lookup"><span data-stu-id="daf29-103">Sync content from a cloud folder tooAzure App Service</span></span>
<span data-ttu-id="daf29-104">In questa esercitazione illustra come toodeploy troppo[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) per la sincronizzazione del contenuto da servizi di archiviazione cloud più diffusi come Dropbox e OneDrive.</span><span class="sxs-lookup"><span data-stu-id="daf29-104">This tutorial shows you how toodeploy too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="daf29-105"><a name="overview"></a>Panoramica della distribuzione per la sincronizzazione dei contenuti</span><span class="sxs-lookup"><span data-stu-id="daf29-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="daf29-106">distribuzione di sincronizzazione del contenuto su richiesta Hello è alimentata dalle hello [motore di distribuzione Kudu](https://github.com/projectkudu/kudu/wiki) integrato con il servizio App.</span><span class="sxs-lookup"><span data-stu-id="daf29-106">hello on-demand content sync deployment is powered by hello [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="daf29-107">In hello [portale Azure](https://portal.azure.com), è possibile specificare una cartella nella memoria cloud, con il codice dell'app e il contenuto della cartella di lavoro e fare clic su sincronizzazione tooApp servizio con hello di un pulsante.</span><span class="sxs-lookup"><span data-stu-id="daf29-107">In hello [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync tooApp Service with hello click of a button.</span></span> <span data-ttu-id="daf29-108">Sincronizzazione del contenuto utilizza processo Kudu hello per la compilazione e distribuzione.</span><span class="sxs-lookup"><span data-stu-id="daf29-108">Content sync utilizes hello Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="daf29-109"><a name="contentsync"></a>Modalità di sincronizzazione di distribuzione contenuto tooenable</span><span class="sxs-lookup"><span data-stu-id="daf29-109"><a name="contentsync"></a>How tooenable content sync deployment</span></span>
<span data-ttu-id="daf29-110">sincronizzazione del contenuto di tooenable da hello [portale Azure](https://portal.azure.com), seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="daf29-110">tooenable content sync from hello [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="daf29-111">Nel pannello dell'app nel portale di Azure hello, fare clic su **impostazioni** > **origine distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="daf29-111">In your app's blade in hello Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="daf29-112">Fare clic su **Scegli origine**, quindi selezionare **OneDrive** o **Dropbox** come origine di hello per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="daf29-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as hello source for deployment.</span></span> 
   
    ![Sincronizzazione dei contenuti](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="daf29-114">A causa delle differenze sottostanti in hello API, **OneDrive for Business** non è supportato in questo momento.</span><span class="sxs-lookup"><span data-stu-id="daf29-114">Because of underlying differences in hello APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="daf29-115">Hello completo autorizzazione del flusso di lavoro tooenable tooaccess di servizio App uno specifico predefiniti percorso designato per OneDrive o Dropbox tutto il contenuto di servizio App in cui verranno archiviati.</span><span class="sxs-lookup"><span data-stu-id="daf29-115">Complete hello authorization workflow tooenable App Service tooaccess a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="daf29-116">Dopo hello autorizzazione piattaforma del servizio App fornirà hello opzione toocreate una cartella del contenuto in hello definita percorso del contenuto o una cartella di contenuto esistente in questo percorso contenuto designato toochoose.</span><span class="sxs-lookup"><span data-stu-id="daf29-116">After authorization hello App Service platform will give you hello option toocreate a content folder under hello designated content path, or toochoose an existing content folder under this designated content path.</span></span> <span data-ttu-id="daf29-117">i percorsi del contenuto Hello designato in account di archiviazione cloud utilizzato per la sincronizzazione di servizio App sono seguente hello:</span><span class="sxs-lookup"><span data-stu-id="daf29-117">hello designated content paths under your cloud storage accounts used for App Service sync are hello following:</span></span>  
   
   * <span data-ttu-id="daf29-118">**OneDrive**: `Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="daf29-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="daf29-119">**Dropbox**: `Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="daf29-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="daf29-120">Dopo aver hello sincronizzazione contenuto hello di sincronizzazione iniziale di contenuto può essere avviata su richiesta dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="daf29-120">After hello initial content sync hello content sync can be initiated on demand from hello Azure portal.</span></span> <span data-ttu-id="daf29-121">Cronologia della distribuzione è disponibile con hello **distribuzioni** blade.</span><span class="sxs-lookup"><span data-stu-id="daf29-121">Deployment history is available with hello **Deployments** blade.</span></span>
   
    ![Cronologia di distribuzione](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="daf29-123">Altre informazioni sulla distribuzione con Dropbox sono disponibili in [Distribuzione tramite Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="daf29-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

