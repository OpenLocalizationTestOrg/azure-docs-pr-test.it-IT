---
title: aaaMove dati da un tooSQL di SQL Server on-premise Azure con Data Factory di Azure | Documenti Microsoft
description: "Consente di impostare una pipeline ADF che riunisce due attività di migrazione di dati che spostano i dati su base giornaliera insieme tra i database locali e nel cloud hello."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a><span data-ttu-id="bec0f-103">Spostare i dati da un tooSQL di server SQL Azure con Data Factory di Azure in locale</span><span class="sxs-lookup"><span data-stu-id="bec0f-103">Move data from an on-premises SQL server tooSQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="bec0f-104">Questo argomento viene illustrato come toomove dati da un tooa di Database di SQL Server on-premise Database di SQL Azure tramite archiviazione Blob di Azure utilizzando hello Azure Data Factory (ADF).</span><span class="sxs-lookup"><span data-stu-id="bec0f-104">This topic shows how toomove data from an on-premises SQL Server Database tooa SQL Azure Database via Azure Blob Storage using hello Azure Data Factory (ADF).</span></span>

<span data-ttu-id="bec0f-105">Per una tabella che riepiloga le varie opzioni per lo spostamento dati tooan Database SQL di Azure, vedere [spostare dati tooan Database SQL di Azure per Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="bec0f-105">For a table that summarizes various options for moving data tooan Azure SQL Database, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <span data-ttu-id="bec0f-106"><a name="intro"></a>Introduzione: Che cos'è Azure Data factory e quando deve essere utilizzato toomigrate dati?</span><span class="sxs-lookup"><span data-stu-id="bec0f-106"><a name="intro"></a>Introduction: What is ADF and when should it be used toomigrate data?</span></span>
<span data-ttu-id="bec0f-107">Data Factory di Azure è un servizio di integrazione di dati basato su cloud completamente gestito che Orchestra e automatizza lo spostamento di hello e trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="bec0f-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="bec0f-108">concetto chiave Hello modello ADF hello è pipeline.</span><span class="sxs-lookup"><span data-stu-id="bec0f-108">hello key concept in hello ADF model is pipeline.</span></span> <span data-ttu-id="bec0f-109">Una pipeline è un raggruppamento logico delle attività, ognuna delle quali definisce hello azioni tooperform sui dati hello contenuti nel set di dati.</span><span class="sxs-lookup"><span data-stu-id="bec0f-109">A pipeline is a logical grouping of Activities, each of which defines hello actions tooperform on hello data contained in Datasets.</span></span> <span data-ttu-id="bec0f-110">Servizi collegati sono le informazioni di hello toodefine utilizzati necessarie per le risorse di dati di Data Factory tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="bec0f-110">Linked services are used toodefine hello information needed for Data Factory tooconnect toohello data resources.</span></span>

<span data-ttu-id="bec0f-111">Con Azure Data factory, i servizi di elaborazione dei dati esistenti possono essere composte in pipeline di dati che sono gestiti e a disponibilità elevata nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="bec0f-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in hello cloud.</span></span> <span data-ttu-id="bec0f-112">Queste pipeline di dati possono essere pianificati tooingest, preparare, trasformare, analizzare e pubblicare i dati e file ADF gestisce e gestisce dati complessi hello e dipendenze di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="bec0f-112">These data pipelines can be scheduled tooingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates hello complex data and processing dependencies.</span></span> <span data-ttu-id="bec0f-113">Le soluzioni possono essere cloud hello rapidamente compilato e distribuito in, la connessione a un numero crescente di on-premise e origini dati cloud.</span><span class="sxs-lookup"><span data-stu-id="bec0f-113">Solutions can be quickly built and deployed in hello cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="bec0f-114">Considerare l'uso di ADF:</span><span class="sxs-lookup"><span data-stu-id="bec0f-114">Consider using ADF:</span></span>

* <span data-ttu-id="bec0f-115">Quando dati esigenze toobe continuamente la migrazione in uno scenario ibrido che consente di accedere sia in locale e risorse cloud</span><span class="sxs-lookup"><span data-stu-id="bec0f-115">when data needs toobe continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="bec0f-116">Quando viene sottoposto a transazione dati hello o esigenze toobe modificato o dispone di logica di business aggiunto tooit quando viene eseguita la migrazione.</span><span class="sxs-lookup"><span data-stu-id="bec0f-116">when hello data is transacted or needs toobe modified or have business logic added tooit when being migrated.</span></span>

<span data-ttu-id="bec0f-117">ADF consente hello pianificazione e monitoraggio dei processi utilizzando semplici script JSON che gestiscono lo spostamento di hello dei dati su base periodica.</span><span class="sxs-lookup"><span data-stu-id="bec0f-117">ADF allows for hello scheduling and monitoring of jobs using simple JSON scripts that manage hello movement of data on a periodic basis.</span></span> <span data-ttu-id="bec0f-118">ADF dispone anche di altre funzionalità quali il supporto di operazioni complesse.</span><span class="sxs-lookup"><span data-stu-id="bec0f-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="bec0f-119">Per ulteriori informazioni sulla data factory di AZURE, vedere la documentazione di hello in [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="bec0f-119">For more information on ADF, see hello documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <span data-ttu-id="bec0f-120"><a name="scenario"></a>Hello Scenario</span><span class="sxs-lookup"><span data-stu-id="bec0f-120"><a name="scenario"></a>hello Scenario</span></span>
<span data-ttu-id="bec0f-121">Si configura una pipeline ADF che compone due attività di migrazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="bec0f-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="bec0f-122">Insieme passano dati su base giornaliera tra un database SQL locale e un Database di SQL Azure nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="bec0f-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in hello cloud.</span></span> <span data-ttu-id="bec0f-123">Hello due attività sono:</span><span class="sxs-lookup"><span data-stu-id="bec0f-123">hello two activities are:</span></span>

* <span data-ttu-id="bec0f-124">copiare i dati da un tooan di database di SQL Server on-premise account di archiviazione Blob di Azure</span><span class="sxs-lookup"><span data-stu-id="bec0f-124">copy data from an on-premises SQL Server database tooan Azure Blob Storage account</span></span>
* <span data-ttu-id="bec0f-125">copiare i dati da tooan account di archiviazione Blob di Azure hello Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="bec0f-125">copy data from hello Azure Blob Storage account tooan Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="bec0f-126">eseguire i passaggi illustrati di seguito sono state adattate da hello dettagliate esercitazione fornito dal team ADF hello Hello: [spostare dati tra origini locali e cloud con Gateway di gestione dati](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) fa riferimento a toohello sezioni rilevanti dell'argomento vengono forniti quando appropriato.</span><span class="sxs-lookup"><span data-stu-id="bec0f-126">hello steps shown here have been adapted from hello more detailed tutorial provided by hello ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References toohello relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <span data-ttu-id="bec0f-127"><a name="prereqs"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bec0f-127"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="bec0f-128">Il tutorial presuppone:</span><span class="sxs-lookup"><span data-stu-id="bec0f-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="bec0f-129">Una **sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="bec0f-129">An **Azure subscription**.</span></span> <span data-ttu-id="bec0f-130">Se non si ha una sottoscrizione, è possibile iscriversi per provare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bec0f-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="bec0f-131">Un **account di archiviazione Azure**.</span><span class="sxs-lookup"><span data-stu-id="bec0f-131">An **Azure storage account**.</span></span> <span data-ttu-id="bec0f-132">Utilizzare un account di archiviazione di Azure per archiviare i dati di hello in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="bec0f-132">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="bec0f-133">Se non si dispone di un account di archiviazione di Azure, vedere hello [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) articolo.</span><span class="sxs-lookup"><span data-stu-id="bec0f-133">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="bec0f-134">Dopo aver creato l'account di archiviazione hello, è necessario account hello tooobtain chiave utilizzata l'archiviazione di hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="bec0f-134">After you have created hello storage account, you need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="bec0f-135">Vedere la sezione [Gestire le chiavi di accesso alle risorse di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="bec0f-135">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="bec0f-136">Accesso tooan **Database SQL di Azure**.</span><span class="sxs-lookup"><span data-stu-id="bec0f-136">Access tooan **Azure SQL Database**.</span></span> <span data-ttu-id="bec0f-137">Se è necessario impostare un Database SQL di Azure, hello tpoic [Guida introduttiva a Database SQL di Microsoft Azure ](../sql-database/sql-database-get-started.md) fornisce informazioni su come tooprovision una nuova istanza di un Database di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bec0f-137">If you must set up an Azure SQL Database, hello tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how tooprovision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="bec0f-138">Installazione e configurazione di **Azure PowerShell** in locale.</span><span class="sxs-lookup"><span data-stu-id="bec0f-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="bec0f-139">Per istruzioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bec0f-139">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="bec0f-140">Questa procedura utilizza hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bec0f-140">This procedure uses hello [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <span data-ttu-id="bec0f-141"><a name="upload-data"></a>Caricamento hello dati tooyour SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="bec0f-141"><a name="upload-data"></a> Upload hello data tooyour on-premises SQL Server</span></span>
<span data-ttu-id="bec0f-142">Utilizziamo hello [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate processo di migrazione hello.</span><span class="sxs-lookup"><span data-stu-id="bec0f-142">We use hello [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate hello migration process.</span></span> <span data-ttu-id="bec0f-143">Hello NYC Taxi set di dati è disponibile, come indicato in questo post, nell'archiviazione blob di Azure [NYC Taxi dati](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="bec0f-143">hello NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="bec0f-144">dati Hello dispone di due file, file di trip_data.csv hello, che contiene i dettagli di andata e ritorno, e file di trip_far.csv hello, che contiene i dettagli della tariffa di hello pagata per ogni itinerario.</span><span class="sxs-lookup"><span data-stu-id="bec0f-144">hello data has two files, hello trip_data.csv file, which contains trip details, and hello  trip_far.csv file, which contains details of hello fare paid for each trip.</span></span> <span data-ttu-id="bec0f-145">Un esempio e una descrizione di questi file sono inclusi in [Descrizione del set di dati relativo alle corse dei taxi di NYC](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span><span class="sxs-lookup"><span data-stu-id="bec0f-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="bec0f-146">È possibile adattare hello procedura qui tooa set di dati personalizzati o seguire i passaggi di hello, come descritto utilizzando hello NYC Taxi set di dati.</span><span class="sxs-lookup"><span data-stu-id="bec0f-146">You can either adapt hello procedure provided here tooa set of your own data or follow hello steps as described by using hello NYC Taxi dataset.</span></span> <span data-ttu-id="bec0f-147">hello tooupload NYC Taxi set di dati nel database di SQL Server locale, attenersi alla procedura hello [importazione Bulk dei dati nel Database di SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span><span class="sxs-lookup"><span data-stu-id="bec0f-147">tooupload hello NYC Taxi dataset into your on-premises SQL Server database, follow hello procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="bec0f-148">Queste istruzioni sono valide per un Server SQL in una macchina virtuale di Azure, ma procedure hello per il caricamento toohello on-premise SQL Server è hello stesso.</span><span class="sxs-lookup"><span data-stu-id="bec0f-148">These instructions are for a SQL Server on an Azure Virtual Machine, but hello procedure for uploading toohello on-premises SQL Server is hello same.</span></span>

## <span data-ttu-id="bec0f-149"><a name="create-adf"></a> Creare un data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="bec0f-149"><a name="create-adf"></a> Create an Azure Data Factory</span></span>
<span data-ttu-id="bec0f-150">istruzioni per la creazione di una nuova Data Factory di Azure e un gruppo di risorse in hello Hello [portale di Azure](https://portal.azure.com/) forniti [creare una Data Factory di Azure](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span><span class="sxs-lookup"><span data-stu-id="bec0f-150">hello instructions for creating a new Azure Data Factory and a resource group in hello [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="bec0f-151">Nome hello nuova ADF istanza *adfdsp* e nome gruppo di risorse di hello creato *adfdsprg*.</span><span class="sxs-lookup"><span data-stu-id="bec0f-151">Name hello new ADF instance *adfdsp* and name hello resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-hello-data-management-gateway"></a><span data-ttu-id="bec0f-152">Installare e configurare il backup hello Gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="bec0f-152">Install and configure up hello Data Management Gateway</span></span>
<span data-ttu-id="bec0f-153">tooenable le pipeline in toowork un factory di dati di Azure con un Server SQL locale, è necessario tooadd come una data factory toohello servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="bec0f-153">tooenable your pipelines in an Azure data factory toowork with an on-premises SQL Server, you need tooadd it as a Linked Service toohello data factory.</span></span> <span data-ttu-id="bec0f-154">toocreate un servizio collegato per un Server SQL locale, è necessario:</span><span class="sxs-lookup"><span data-stu-id="bec0f-154">toocreate a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="bec0f-155">scaricare e installare il Gateway di gestione dati Microsoft nel computer locale hello.</span><span class="sxs-lookup"><span data-stu-id="bec0f-155">download and install Microsoft Data Management Gateway onto hello on-premises computer.</span></span>
* <span data-ttu-id="bec0f-156">configurare il servizio collegato hello per gateway di hello locale dati origine toouse hello.</span><span class="sxs-lookup"><span data-stu-id="bec0f-156">configure hello linked service for hello on-premises data source toouse hello gateway.</span></span>

<span data-ttu-id="bec0f-157">Hello Gateway di gestione dati serializza e deserializza i dati di origine e sink hello computer hello in cui è ospitato.</span><span class="sxs-lookup"><span data-stu-id="bec0f-157">hello Data Management Gateway serializes and deserializes hello source and sink data on hello computer where it is hosted.</span></span>

<span data-ttu-id="bec0f-158">Per le istruzioni di configurazione e i dettagli sul Gateway di gestione dati, vedere [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="bec0f-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <span data-ttu-id="bec0f-159"><a name="adflinkedservices"></a>Creare servizi collegati tooconnect toohello risorse di dati</span><span class="sxs-lookup"><span data-stu-id="bec0f-159"><a name="adflinkedservices"></a>Create linked services tooconnect toohello data resources</span></span>
<span data-ttu-id="bec0f-160">Un servizio collegato definisce informazioni di hello necessarie per la risorsa di Azure Data Factory tooconnect tooa dati.</span><span class="sxs-lookup"><span data-stu-id="bec0f-160">A linked service defines hello information needed for Azure Data Factory tooconnect tooa data resource.</span></span> <span data-ttu-id="bec0f-161">viene fornita la procedura dettagliata per la creazione di servizi collegati Hello in [creare i servizi collegati](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span><span class="sxs-lookup"><span data-stu-id="bec0f-161">hello step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="bec0f-162">Sono disponibili tre risorse in questo scenario per il quale sono necessari servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="bec0f-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="bec0f-163">Servizio collegato per SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="bec0f-163">Linked service for on-premises SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="bec0f-164">Servizio collegato per archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="bec0f-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="bec0f-165">Servizio collegato per il database SQL Azure</span><span class="sxs-lookup"><span data-stu-id="bec0f-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <span data-ttu-id="bec0f-166"><a name="adf-linked-service-onprem-sql"></a>Servizio collegato per il database SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="bec0f-166"><a name="adf-linked-service-onprem-sql"></a>Linked service for on-premises SQL Server database</span></span>
<span data-ttu-id="bec0f-167">servizio collegato hello toocreate per hello locale SQL Server:</span><span class="sxs-lookup"><span data-stu-id="bec0f-167">toocreate hello linked service for hello on-premises SQL Server:</span></span>

* <span data-ttu-id="bec0f-168">Fare clic su hello **archivio dati** nella pagina di destinazione ADF hello nel portale classico di Azure</span><span class="sxs-lookup"><span data-stu-id="bec0f-168">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="bec0f-169">Selezionare **SQL** e immettere hello *username* e *password* le credenziali per hello on-premise SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bec0f-169">select **SQL** and enter hello *username* and *password* credentials for hello on-premises SQL Server.</span></span> <span data-ttu-id="bec0f-170">È necessario tooenter hello servername come un **servername completo barra rovesciata nome dell'istanza (nomeserver\nomeistanza)**.</span><span class="sxs-lookup"><span data-stu-id="bec0f-170">You need tooenter hello servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="bec0f-171">Servizio collegato hello nome *adfonpremsql*.</span><span class="sxs-lookup"><span data-stu-id="bec0f-171">Name hello linked service *adfonpremsql*.</span></span>

### <span data-ttu-id="bec0f-172"><a name="adf-linked-service-blob-store"></a>Servizi collegati per BLOB</span><span class="sxs-lookup"><span data-stu-id="bec0f-172"><a name="adf-linked-service-blob-store"></a>Linked service for Blob</span></span>
<span data-ttu-id="bec0f-173">toocreate hello servizio collegato per l'account di archiviazione Blob di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="bec0f-173">toocreate hello linked service for hello Azure Blob Storage account:</span></span>

* <span data-ttu-id="bec0f-174">Fare clic su hello **archivio dati** nella pagina di destinazione ADF hello nel portale classico di Azure</span><span class="sxs-lookup"><span data-stu-id="bec0f-174">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="bec0f-175">selezionare **Account di archiviazione di Azure**</span><span class="sxs-lookup"><span data-stu-id="bec0f-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="bec0f-176">Immettere hello archiviazione Blob di Azure contenitore chiave e il nome dell'account.</span><span class="sxs-lookup"><span data-stu-id="bec0f-176">enter hello Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="bec0f-177">Hello Nome servizio collegato *adfds*.</span><span class="sxs-lookup"><span data-stu-id="bec0f-177">Name hello Linked Service *adfds*.</span></span>

### <span data-ttu-id="bec0f-178"><a name="adf-linked-service-azure-sql"></a>Servizio collegato per il database SQL Azure</span><span class="sxs-lookup"><span data-stu-id="bec0f-178"><a name="adf-linked-service-azure-sql"></a>Linked service for Azure SQL database</span></span>
<span data-ttu-id="bec0f-179">toocreate hello servizio collegato per hello Database SQL di Azure:</span><span class="sxs-lookup"><span data-stu-id="bec0f-179">toocreate hello linked service for hello Azure SQL Database:</span></span>

* <span data-ttu-id="bec0f-180">Fare clic su hello **archivio dati** nella pagina di destinazione ADF hello nel portale classico di Azure</span><span class="sxs-lookup"><span data-stu-id="bec0f-180">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="bec0f-181">Selezionare **SQL Azure** e immettere hello *username* e *password* le credenziali per hello Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="bec0f-181">select **Azure SQL** and enter hello *username* and *password* credentials for hello Azure SQL Database.</span></span> <span data-ttu-id="bec0f-182">Hello *username* deve essere specificato come  *user@servername* .</span><span class="sxs-lookup"><span data-stu-id="bec0f-182">hello *username* must be specified as *user@servername*.</span></span>   

## <span data-ttu-id="bec0f-183"><a name="adf-tables"></a>Definire e creare tabelle toospecify come tooaccess hello set di dati</span><span class="sxs-lookup"><span data-stu-id="bec0f-183"><a name="adf-tables"></a>Define and create tables toospecify how tooaccess hello datasets</span></span>
<span data-ttu-id="bec0f-184">Creare tabelle che specificano struttura hello, posizione e la disponibilità dei set di dati hello con hello procedure basato su script.</span><span class="sxs-lookup"><span data-stu-id="bec0f-184">Create tables that specify hello structure, location, and availability of hello datasets with hello following script-based procedures.</span></span> <span data-ttu-id="bec0f-185">File JSON vengono usati toodefine hello tabelle.</span><span class="sxs-lookup"><span data-stu-id="bec0f-185">JSON files are used toodefine hello tables.</span></span> <span data-ttu-id="bec0f-186">Per ulteriori informazioni sulla struttura hello di questi file, vedere [set di dati](../data-factory/data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="bec0f-186">For more information on hello structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bec0f-187">È consigliabile eseguire hello `Add-AzureAccount` cmdlet prima di eseguire hello [New AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) tooconfirm cmdlet che hello sottoscrizione di Azure a destra è selezionata per l'esecuzione del comando hello.</span><span class="sxs-lookup"><span data-stu-id="bec0f-187">You should execute hello `Add-AzureAccount` cmdlet before executing hello [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet tooconfirm that hello right Azure subscription is selected for hello command execution.</span></span> <span data-ttu-id="bec0f-188">Per la documentazione di questo cmdlet, vedere [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="bec0f-188">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="bec0f-189">le definizioni di basato su JSON di Hello nelle tabelle di hello utilizzare hello seguenti nomi:</span><span class="sxs-lookup"><span data-stu-id="bec0f-189">hello JSON-based definitions in hello tables use hello following names:</span></span>

* <span data-ttu-id="bec0f-190">Hello **nome tabella** hello on-premise SQL server è *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="bec0f-190">hello **table name** in hello on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="bec0f-191">Hello **nome contenitore** in hello archiviazione Blob di Azure è l'account *containername*</span><span class="sxs-lookup"><span data-stu-id="bec0f-191">hello **container name** in hello Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="bec0f-192">Per questa pipeline ADF sono necessarie tre definizioni di tabella:</span><span class="sxs-lookup"><span data-stu-id="bec0f-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="bec0f-193">Tabella SQL locale</span><span class="sxs-lookup"><span data-stu-id="bec0f-193">SQL on-premises Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="bec0f-194">Tabella BLOB </span><span class="sxs-lookup"><span data-stu-id="bec0f-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="bec0f-195">Tabella SQL Azure</span><span class="sxs-lookup"><span data-stu-id="bec0f-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="bec0f-196">Queste procedure utilizzano toodefine Azure PowerShell e creare hello attività ADF.</span><span class="sxs-lookup"><span data-stu-id="bec0f-196">These procedures use Azure PowerShell toodefine and create hello ADF activities.</span></span> <span data-ttu-id="bec0f-197">Tuttavia, queste attività possono inoltre essere eseguite utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bec0f-197">But these tasks can also be accomplished using hello Azure portal.</span></span> <span data-ttu-id="bec0f-198">Per informazioni dettagliate, vedere [Creare set di dati](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span><span class="sxs-lookup"><span data-stu-id="bec0f-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <span data-ttu-id="bec0f-199"><a name="adf-table-onprem-sql"></a>Tabella SQL locale</span><span class="sxs-lookup"><span data-stu-id="bec0f-199"><a name="adf-table-onprem-sql"></a>SQL on-premises Table</span></span>
<span data-ttu-id="bec0f-200">definizione della tabella Hello per hello on-premise SQL Server specificato nel seguente file JSON hello:</span><span class="sxs-lookup"><span data-stu-id="bec0f-200">hello table definition for hello on-premises SQL Server is specified in hello following JSON file:</span></span>

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

<span data-ttu-id="bec0f-201">non sono inclusi i nomi di colonna Hello.</span><span class="sxs-lookup"><span data-stu-id="bec0f-201">hello column names were not included here.</span></span> <span data-ttu-id="bec0f-202">È possibile selezionare i nomi di colonna hello Sub includendoli qui (per dettagli, vedere hello [documentazione ADF](../data-factory/data-factory-data-movement-activities.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="bec0f-202">You can sub-select on hello column names by including them here (for details check hello [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="bec0f-203">Copiare definizione JSON hello della tabella hello in un file denominato *onpremtabledef.json* file e salvarlo tooa percorso noto (di seguito si presuppone che toobe *C:\temp\onpremtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="bec0f-203">Copy hello JSON definition of hello table into a file called *onpremtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="bec0f-204">Creare tabella hello in ADF con hello cmdlet di Azure PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="bec0f-204">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <span data-ttu-id="bec0f-205"><a name="adf-table-blob-store"></a>Tabella BLOB</span><span class="sxs-lookup"><span data-stu-id="bec0f-205"><a name="adf-table-blob-store"></a>Blob Table</span></span>
<span data-ttu-id="bec0f-206">Definizione per la tabella hello per hello output blob si trova nella seguente hello (esegue il mapping dei dati di caricamento hello dal blob tooAzure locale):</span><span class="sxs-lookup"><span data-stu-id="bec0f-206">Definition for hello table for hello output blob location is in hello following (this maps hello ingested data from on-premises tooAzure blob):</span></span>

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

<span data-ttu-id="bec0f-207">Copiare definizione JSON hello della tabella hello in un file denominato *bloboutputtabledef.json* file e salvarlo tooa percorso noto (di seguito si presuppone che toobe *C:\temp\bloboutputtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="bec0f-207">Copy hello JSON definition of hello table into a file called *bloboutputtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="bec0f-208">Creare tabella hello in ADF con hello cmdlet di Azure PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="bec0f-208">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <span data-ttu-id="bec0f-209"><a name="adf-table-azure-sq"></a>Tabella SQL Azure</span><span class="sxs-lookup"><span data-stu-id="bec0f-209"><a name="adf-table-azure-sq"></a>SQL Azure Table</span></span>
<span data-ttu-id="bec0f-210">Definizione di tabella hello per SQL Azure di output di hello è seguito hello (questo schema Associa dati hello provenienti dal blob hello):</span><span class="sxs-lookup"><span data-stu-id="bec0f-210">Definition for hello table for hello SQL Azure output is in hello following (this schema maps hello data coming from hello blob):</span></span>

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

<span data-ttu-id="bec0f-211">Copiare definizione JSON hello della tabella hello in un file denominato *AzureSqlTable.json* file e salvarlo tooa percorso noto (di seguito si presuppone che toobe *C:\temp\AzureSqlTable.json*).</span><span class="sxs-lookup"><span data-stu-id="bec0f-211">Copy hello JSON definition of hello table into a file called *AzureSqlTable.json* file and save it tooa known location (here assumed toobe *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="bec0f-212">Creare tabella hello in ADF con hello cmdlet di Azure PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="bec0f-212">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <span data-ttu-id="bec0f-213"><a name="adf-pipeline"></a>Definire e creare pipeline hello</span><span class="sxs-lookup"><span data-stu-id="bec0f-213"><a name="adf-pipeline"></a>Define and create hello pipeline</span></span>
<span data-ttu-id="bec0f-214">Specificare le attività di hello appartenenti toohello della pipeline e creare pipeline hello con hello procedure basato su script.</span><span class="sxs-lookup"><span data-stu-id="bec0f-214">Specify hello activities that belong toohello pipeline and create hello pipeline with hello following script-based procedures.</span></span> <span data-ttu-id="bec0f-215">Un file JSON è toodefine usate le proprietà della pipeline di hello.</span><span class="sxs-lookup"><span data-stu-id="bec0f-215">A JSON file is used toodefine hello pipeline properties.</span></span>

* <span data-ttu-id="bec0f-216">Hello script si presuppone che hello **nome pipeline** è *AMLDSProcessPipeline*.</span><span class="sxs-lookup"><span data-stu-id="bec0f-216">hello script assumes that hello **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="bec0f-217">Si noti inoltre che è impostata la periodicità hello di hello pipeline toobe eseguito su ogni giorno base e utilizzare hello tempo di esecuzione predefinito per il processo di hello (12 am UTC).</span><span class="sxs-lookup"><span data-stu-id="bec0f-217">Also note that we set hello periodicity of hello pipeline toobe executed on daily basis and use hello default execution time for hello job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="bec0f-218">Hello procedure riportate di seguito utilizzano toodefine Azure PowerShell e creare pipeline ADF hello.</span><span class="sxs-lookup"><span data-stu-id="bec0f-218">hello following procedures use Azure PowerShell toodefine and create hello ADF pipeline.</span></span> <span data-ttu-id="bec0f-219">Tuttavia, questa attività può inoltre essere eseguita tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bec0f-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="bec0f-220">Per informazioni dettagliate, vedere [Creare una pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span><span class="sxs-lookup"><span data-stu-id="bec0f-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="bec0f-221">Utilizzo di definizioni di tabella hello fornito in precedenza, definizione di pipeline hello per hello che ADF viene specificata come segue:</span><span class="sxs-lookup"><span data-stu-id="bec0f-221">Using hello table definitions provided previously, hello pipeline definition for hello ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

<span data-ttu-id="bec0f-222">Copiare questa definizione JSON della pipeline hello in un file denominato *pipelinedef.json* file e salvarlo tooa percorso noto (di seguito si presuppone che toobe *C:\temp\pipelinedef.json*).</span><span class="sxs-lookup"><span data-stu-id="bec0f-222">Copy this JSON definition of hello pipeline into a file called *pipelinedef.json* file and save it tooa known location (here assumed toobe *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="bec0f-223">Creare pipeline hello in ADF con hello cmdlet di Azure PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="bec0f-223">Create hello pipeline in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="bec0f-224">Confermare che è possibile visualizzare pipeline hello in hello ADF nel portale di Azure classico hello visualizzati come riportato di seguito (quando si fa clic su diagramma hello)</span><span class="sxs-lookup"><span data-stu-id="bec0f-224">Confirm that you can see hello pipeline on hello ADF in hello Azure Classic Portal show up as following (when you click hello diagram)</span></span>

![Pipeline ADF](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <span data-ttu-id="bec0f-226"><a name="adf-pipeline-start"></a>Avviare hello Pipeline</span><span class="sxs-lookup"><span data-stu-id="bec0f-226"><a name="adf-pipeline-start"></a>Start hello Pipeline</span></span>
<span data-ttu-id="bec0f-227">è possibile eseguire pipeline Hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bec0f-227">hello pipeline can now be run using hello following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="bec0f-228">Hello *startdate* e *enddate* i valori di parametro devono toobe sostituito con date effettive di hello tra i quali si desidera toorun pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="bec0f-228">hello *startdate* and *enddate* parameter values need toobe replaced with hello actual dates between which you want hello pipeline toorun.</span></span>

<span data-ttu-id="bec0f-229">Una volta che viene eseguita la pipeline hello, si dovrebbe essere in grado di toosee hello dati visualizzati nel contenitore hello selezionati per il blob hello, un file per ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="bec0f-229">Once hello pipeline executes, you should be able toosee hello data show up in hello container selected for hello blob, one file per day.</span></span>

<span data-ttu-id="bec0f-230">Si noti che non è stato sfruttato funzionalità hello fornita dai dati toopipe ADF in modo incrementale.</span><span class="sxs-lookup"><span data-stu-id="bec0f-230">Note that we have not leveraged hello functionality provided by ADF toopipe data incrementally.</span></span> <span data-ttu-id="bec0f-231">Per ulteriori informazioni su come toodo questa e altre funzionalità fornite da Azure Data factory, vedere hello [documentazione ADF](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="bec0f-231">For more information on how toodo this and other capabilities provided by ADF, see hello [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
