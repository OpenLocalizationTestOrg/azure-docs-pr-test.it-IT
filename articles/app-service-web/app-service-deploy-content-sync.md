---
title: Sincronizzare i contenuti da una cartella nel cloud per il servizio app di Azure
description: Informazioni su come distribuire l'app nel servizio app di Azure tramite la sincronizzazione dei contenuti da una cartella nel cloud.
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
ms.openlocfilehash: 010e7dc492abefaa3afe814c0322af9f6fe5acd2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sync-content-from-a-cloud-folder-to-azure-app-service"></a><span data-ttu-id="1b2c4-103">Sincronizzare i contenuti da una cartella nel cloud per il servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="1b2c4-103">Sync content from a cloud folder to Azure App Service</span></span>
<span data-ttu-id="1b2c4-104">Questa esercitazione spiega come effettuare una distribuzione nel [Servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) sincronizzando i contenuti dai servizi di archiviazione cloud più diffusi, come Dropbox e OneDrive.</span><span class="sxs-lookup"><span data-stu-id="1b2c4-104">This tutorial shows you how to deploy to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="1b2c4-105"><a name="overview"></a>Panoramica della distribuzione per la sincronizzazione dei contenuti</span><span class="sxs-lookup"><span data-stu-id="1b2c4-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="1b2c4-106">La distribuzione per la sincronizzazione dei contenuti on demand si basa sul [motore di distribuzione Kudu](https://github.com/projectkudu/kudu/wiki) integrato con il servizio app.</span><span class="sxs-lookup"><span data-stu-id="1b2c4-106">The on-demand content sync deployment is powered by the [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="1b2c4-107">Nel [portale di Azure](https://portal.azure.com)è possibile designare una cartella speciale nel servizio di archiviazione cloud, utilizzare il codice e il contenuto dell'applicazione disponibile in tale cartella e procedere alla sincronizzazione con il servizio app con un semplice clic del mouse.</span><span class="sxs-lookup"><span data-stu-id="1b2c4-107">In the [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync to App Service with the click of a button.</span></span> <span data-ttu-id="1b2c4-108">La sincronizzazione usa il processo Kudu per la compilazione e la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="1b2c4-108">Content sync utilizes the Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="1b2c4-109"><a name="contentsync"></a>Come abilitare la distribuzione per la sincronizzazione dei contenuti</span><span class="sxs-lookup"><span data-stu-id="1b2c4-109"><a name="contentsync"></a>How to enable content sync deployment</span></span>
<span data-ttu-id="1b2c4-110">Per abilitare la sincronizzazione del contenuto dal [portale di Azure](https://portal.azure.com), seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1b2c4-110">To enable content sync from the [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="1b2c4-111">Nel pannello dell'app del portale di Azure fare clic su **Impostazioni** > **Origine distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="1b2c4-111">In your app's blade in the Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="1b2c4-112">Fare clic su **Scegliere l'origine** e quindi selezionare **OneDrive** o **Dropbox** come origine per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="1b2c4-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as the source for deployment.</span></span> 
   
    ![Sincronizzazione dei contenuti](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="1b2c4-114">A causa delle differenze sottostanti nelle API, **OneDrive for Business** non è attualmente supportato.</span><span class="sxs-lookup"><span data-stu-id="1b2c4-114">Because of underlying differences in the APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="1b2c4-115">Completare il flusso di lavoro di autorizzazione per consentire al servizio app di accedere a un determinato percorso designato predefinito per OneDrive o Dropbox in cui verranno archiviati tutti i contenuti del servizio app.</span><span class="sxs-lookup"><span data-stu-id="1b2c4-115">Complete the authorization workflow to enable App Service to access a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="1b2c4-116">Dopo l'autorizzazione la piattaforma del servizio app consentirà di creare una cartella dei contenuti nel percorso dei contenuti designato oppure di selezionare una cartella esistente in questo stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="1b2c4-116">After authorization the App Service platform will give you the option to create a content folder under the designated content path, or to choose an existing content folder under this designated content path.</span></span> <span data-ttu-id="1b2c4-117">I percorsi dei contenuti designati negli account di archiviazione cloud usati per la sincronizzazione del servizio app sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="1b2c4-117">The designated content paths under your cloud storage accounts used for App Service sync are the following:</span></span>  
   
   * <span data-ttu-id="1b2c4-118">**OneDrive**: `Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="1b2c4-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="1b2c4-119">**Dropbox**: `Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="1b2c4-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="1b2c4-120">Dopo la sincronizzazione dei contenuti iniziale, la sincronizzazione può essere avviata su richiesta dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b2c4-120">After the initial content sync the content sync can be initiated on demand from the Azure portal.</span></span> <span data-ttu-id="1b2c4-121">La cronologia di distribuzione è disponibile nel pannello **Distribuzioni** .</span><span class="sxs-lookup"><span data-stu-id="1b2c4-121">Deployment history is available with the **Deployments** blade.</span></span>
   
    ![Cronologia di distribuzione](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="1b2c4-123">Altre informazioni sulla distribuzione con Dropbox sono disponibili in [Distribuzione tramite Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b2c4-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

