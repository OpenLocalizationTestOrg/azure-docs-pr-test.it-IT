---
title: Spostare dati da SQL Server locale a SQL Azure con Azure Data Factory | Microsoft Docs
description: "Impostare una pipeline di ADF che comprenda due attività di migrazione di dati che insieme spostino i dati giornalmente tra database locali e nel cloud."
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
ms.openlocfilehash: 39fe26d3388be8b558f05063a8965889c013a41e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-from-an-on-premises-sql-server-to-sql-azure-with-azure-data-factory"></a><span data-ttu-id="cdb30-103">Spostare i dati da SQL Server locale a SQL Azure con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="cdb30-103">Move data from an on-premises SQL server to SQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="cdb30-104">Questo argomento descrive come spostare i dati da un database di SQL Server locale a un database di SQL Azure tramite l'archiviazione BLOB di Azure usando Azure Data Factory (ADF).</span><span class="sxs-lookup"><span data-stu-id="cdb30-104">This topic shows how to move data from an on-premises SQL Server Database to a SQL Azure Database via Azure Blob Storage using the Azure Data Factory (ADF).</span></span>

<span data-ttu-id="cdb30-105">Per un tabella che riepiloga le varie opzioni per lo spostamento dei dati in un database SQL Azure, vedere [Spostare i dati a un database SQL Azure per Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="cdb30-105">For a table that summarizes various options for moving data to an Azure SQL Database, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <span data-ttu-id="cdb30-106"><a name="intro"></a>Introduzione: che cos'è l’ADF e quando deve essere utilizzato per la migrazione dei dati?</span><span class="sxs-lookup"><span data-stu-id="cdb30-106"><a name="intro"></a>Introduction: What is ADF and when should it be used to migrate data?</span></span>
<span data-ttu-id="cdb30-107">Il Data factory è un servizio di integrazione delle informazioni basato sul cloud che permette di automatizzare lo spostamento e la trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="cdb30-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="cdb30-108">Il concetto chiave nel modello ADF è pipeline.</span><span class="sxs-lookup"><span data-stu-id="cdb30-108">The key concept in the ADF model is pipeline.</span></span> <span data-ttu-id="cdb30-109">Una pipeline è un raggruppamento logico di attività, ognuna delle quali definisce le azioni da eseguire sui dati contenuti nel set di dati.</span><span class="sxs-lookup"><span data-stu-id="cdb30-109">A pipeline is a logical grouping of Activities, each of which defines the actions to perform on the data contained in Datasets.</span></span> <span data-ttu-id="cdb30-110">I servizi collegati vengono utilizzati per definire le informazioni necessarie affinché il servizio Data factory si connetta a risorse dati esterne.</span><span class="sxs-lookup"><span data-stu-id="cdb30-110">Linked services are used to define the information needed for Data Factory to connect to the data resources.</span></span>

<span data-ttu-id="cdb30-111">Con ADF, i servizi di elaborazione dei dati esistenti possono essere composti in pipeline di dati, altamente disponibili e gestiti nel cloud.</span><span class="sxs-lookup"><span data-stu-id="cdb30-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in the cloud.</span></span> <span data-ttu-id="cdb30-112">Queste pipeline di dati possono essere pianificate per inserire, preparare, trasformare, analizzare e pubblicare i dati e l’ADF gestisce e organizza i dati complessi e le dipendenze di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="cdb30-112">These data pipelines can be scheduled to ingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates the complex data and processing dependencies.</span></span> <span data-ttu-id="cdb30-113">Le soluzioni possono essere compilate e distribuite nel cloud, collegando un numero crescente di origini dati locali e cloud.</span><span class="sxs-lookup"><span data-stu-id="cdb30-113">Solutions can be quickly built and deployed in the cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="cdb30-114">Considerare l'uso di ADF:</span><span class="sxs-lookup"><span data-stu-id="cdb30-114">Consider using ADF:</span></span>

* <span data-ttu-id="cdb30-115">quando i dati sono soggetti a migrazione continua in uno scenario ibrido che accede alle risorse locali e cloud</span><span class="sxs-lookup"><span data-stu-id="cdb30-115">when data needs to be continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="cdb30-116">quando i dati sono soggetti a transazioni, devono essere modificati o si vedono aggiungere una logica di business quando vengono migrati.</span><span class="sxs-lookup"><span data-stu-id="cdb30-116">when the data is transacted or needs to be modified or have business logic added to it when being migrated.</span></span>

<span data-ttu-id="cdb30-117">L’ADF consente la pianificazione e il monitoraggio dei processi utilizzando semplici script JSON che gestiscono lo spostamento dei dati su base periodica.</span><span class="sxs-lookup"><span data-stu-id="cdb30-117">ADF allows for the scheduling and monitoring of jobs using simple JSON scripts that manage the movement of data on a periodic basis.</span></span> <span data-ttu-id="cdb30-118">ADF dispone anche di altre funzionalità quali il supporto di operazioni complesse.</span><span class="sxs-lookup"><span data-stu-id="cdb30-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="cdb30-119">Per ulteriori informazioni sul file ADF, vedere la documentazione di [Data factory di Azure (ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="cdb30-119">For more information on ADF, see the documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <span data-ttu-id="cdb30-120"><a name="scenario"></a>Scenario</span><span class="sxs-lookup"><span data-stu-id="cdb30-120"><a name="scenario"></a>The Scenario</span></span>
<span data-ttu-id="cdb30-121">Si configura una pipeline ADF che compone due attività di migrazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="cdb30-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="cdb30-122">Insieme, queste attività spostano i dati giornalmente tra un database SQL locale e un database di SQL Azure nel cloud.</span><span class="sxs-lookup"><span data-stu-id="cdb30-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in the cloud.</span></span> <span data-ttu-id="cdb30-123">Le due attività sono:</span><span class="sxs-lookup"><span data-stu-id="cdb30-123">The two activities are:</span></span>

* <span data-ttu-id="cdb30-124">Copiare dati da un database di SQL Server locale in un account dell'archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="cdb30-124">copy data from an on-premises SQL Server database to an Azure Blob Storage account</span></span>
* <span data-ttu-id="cdb30-125">Copiare i dati dall'account di archiviazione BLOB di Azure a un Database di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb30-125">copy data from the Azure Blob Storage account to an Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="cdb30-126">I passaggi illustrati di seguito sono stati adattati dall'esercitazione più specifica fornita dal team ADF: [Spostare dati tra origini locali e il cloud con gateway di gestione dati](../data-factory/data-factory-move-data-between-onprem-and-cloud.md). I riferimenti alle sezioni pertinenti dell'argomento vengono resi disponibili laddove opportuno.</span><span class="sxs-lookup"><span data-stu-id="cdb30-126">The steps shown here have been adapted from the more detailed tutorial provided by the ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References to the relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <span data-ttu-id="cdb30-127"><a name="prereqs"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cdb30-127"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="cdb30-128">Il tutorial presuppone:</span><span class="sxs-lookup"><span data-stu-id="cdb30-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="cdb30-129">Una **sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="cdb30-129">An **Azure subscription**.</span></span> <span data-ttu-id="cdb30-130">Se non si ha una sottoscrizione, è possibile iscriversi per provare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cdb30-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="cdb30-131">Un **account di archiviazione Azure**.</span><span class="sxs-lookup"><span data-stu-id="cdb30-131">An **Azure storage account**.</span></span> <span data-ttu-id="cdb30-132">In questa esercitazione si userà un account di archiviazione di Azure per archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="cdb30-132">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="cdb30-133">Se non si dispone di un account di archiviazione di Azure, vedere l'articolo [Creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) .</span><span class="sxs-lookup"><span data-stu-id="cdb30-133">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="cdb30-134">Dopo avere creato l'account di archiviazione, è necessario ottenere la chiave dell'account usata per accedere alla risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="cdb30-134">After you have created the storage account, you need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="cdb30-135">Vedere la sezione [Gestire le chiavi di accesso alle risorse di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="cdb30-135">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="cdb30-136">Accesso a un **database SQL di Azure**.</span><span class="sxs-lookup"><span data-stu-id="cdb30-136">Access to an **Azure SQL Database**.</span></span> <span data-ttu-id="cdb30-137">Se è necessario impostare un database di SQL Azure, l'argomento [Guida introduttiva al database SQL di Microsoft Azure ](../sql-database/sql-database-get-started.md) fornisce informazioni su come eseguire il provisioning di una nuova istanza di un database di SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb30-137">If you must set up an Azure SQL Database, the tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how to provision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="cdb30-138">Installazione e configurazione di **Azure PowerShell** in locale.</span><span class="sxs-lookup"><span data-stu-id="cdb30-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="cdb30-139">Per istruzioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cdb30-139">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="cdb30-140">In questa procedura viene utilizzato il [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cdb30-140">This procedure uses the [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <span data-ttu-id="cdb30-141"><a name="upload-data"></a> Caricare i dati in SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="cdb30-141"><a name="upload-data"></a> Upload the data to your on-premises SQL Server</span></span>
<span data-ttu-id="cdb30-142">Utilizziamo il [set di dati NYC Taxi](http://chriswhong.com/open-data/foil_nyc_taxi/) per illustrare il processo di migrazione.</span><span class="sxs-lookup"><span data-stu-id="cdb30-142">We use the [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) to demonstrate the migration process.</span></span> <span data-ttu-id="cdb30-143">Il set di dati NYC Taxi è disponibile, come indicato nel post, sull'archiviazione BLOB di Azure [Dati NYC Taxi](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="cdb30-143">The NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="cdb30-144">I dati dispongono di due file, il file trip_data.csv che contiene i dettagli relativi alle corse e il file trip_far.csv che contiene i dettagli della tariffa pagata per ogni corsa.</span><span class="sxs-lookup"><span data-stu-id="cdb30-144">The data has two files, the trip_data.csv file, which contains trip details, and the  trip_far.csv file, which contains details of the fare paid for each trip.</span></span> <span data-ttu-id="cdb30-145">Un esempio e una descrizione di questi file sono inclusi in [Descrizione del set di dati relativo alle corse dei taxi di NYC](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span><span class="sxs-lookup"><span data-stu-id="cdb30-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="cdb30-146">È possibile adattare le procedure riportate di seguito a un set di dati personalizzati o seguire i passaggi come descritto utilizzando il set di dati NYC Taxi.</span><span class="sxs-lookup"><span data-stu-id="cdb30-146">You can either adapt the procedure provided here to a set of your own data or follow the steps as described by using the NYC Taxi dataset.</span></span> <span data-ttu-id="cdb30-147">Per caricare il set di dati NYC Taxi nel database di SQL Server locale, seguire la procedura descritta in [Importazione in blocco dei dati nel database SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span><span class="sxs-lookup"><span data-stu-id="cdb30-147">To upload the NYC Taxi dataset into your on-premises SQL Server database, follow the procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="cdb30-148">Queste istruzioni sono per SQL Server in una macchina virtuale di Azure, ma la procedura per il caricamento in SQL Server locale è la stessa.</span><span class="sxs-lookup"><span data-stu-id="cdb30-148">These instructions are for a SQL Server on an Azure Virtual Machine, but the procedure for uploading to the on-premises SQL Server is the same.</span></span>

## <span data-ttu-id="cdb30-149"><a name="create-adf"></a> Creare un data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="cdb30-149"><a name="create-adf"></a> Create an Azure Data Factory</span></span>
<span data-ttu-id="cdb30-150">Le istruzioni per la creazione di una nuova data factory di Azure e un gruppo di risorse nel [portale di Azure](https://portal.azure.com/) sono disponibili in [Creazione di un'istanza di Data factory di Azure](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span><span class="sxs-lookup"><span data-stu-id="cdb30-150">The instructions for creating a new Azure Data Factory and a resource group in the [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="cdb30-151">Denominare la nuova istanza ADF *adfdsp*e assegnare il nome *adfdsprg* al gruppo di risorse creato.</span><span class="sxs-lookup"><span data-stu-id="cdb30-151">Name the new ADF instance *adfdsp* and name the resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-the-data-management-gateway"></a><span data-ttu-id="cdb30-152">Installare e configurare i Gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="cdb30-152">Install and configure up the Data Management Gateway</span></span>
<span data-ttu-id="cdb30-153">Per abilitare le pipeline in Azure Data Factory per il funzionamento con SQL Server locale, è necessario aggiungerle come servizio collegato ad Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cdb30-153">To enable your pipelines in an Azure data factory to work with an on-premises SQL Server, you need to add it as a Linked Service to the data factory.</span></span> <span data-ttu-id="cdb30-154">Per creare un servizio collegato per SQL Server locale, è necessario:</span><span class="sxs-lookup"><span data-stu-id="cdb30-154">To create a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="cdb30-155">scaricare e installare il gateway di gestione dati di Microsoft nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="cdb30-155">download and install Microsoft Data Management Gateway onto the on-premises computer.</span></span>
* <span data-ttu-id="cdb30-156">configurare il servizio collegato per l'origine dati locale per l'utilizzo del gateway.</span><span class="sxs-lookup"><span data-stu-id="cdb30-156">configure the linked service for the on-premises data source to use the gateway.</span></span>

<span data-ttu-id="cdb30-157">Gateway di gestione dati serializza e deserializza i dati di origine e sink sul computer in cui è ospitato.</span><span class="sxs-lookup"><span data-stu-id="cdb30-157">The Data Management Gateway serializes and deserializes the source and sink data on the computer where it is hosted.</span></span>

<span data-ttu-id="cdb30-158">Per le istruzioni di configurazione e i dettagli sul Gateway di gestione dati, vedere [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="cdb30-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <span data-ttu-id="cdb30-159"><a name="adflinkedservices"></a>Creare servizi collegati per connettersi alle risorse di dati</span><span class="sxs-lookup"><span data-stu-id="cdb30-159"><a name="adflinkedservices"></a>Create linked services to connect to the data resources</span></span>
<span data-ttu-id="cdb30-160">I servizi collegati definiscono le informazioni necessarie affinché il servizio data factory si connetta a risorse dati.</span><span class="sxs-lookup"><span data-stu-id="cdb30-160">A linked service defines the information needed for Azure Data Factory to connect to a data resource.</span></span> <span data-ttu-id="cdb30-161">In [Creazione di servizi collegati](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services)viene fornita la procedura dettagliata per la creazione di servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="cdb30-161">The step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="cdb30-162">Sono disponibili tre risorse in questo scenario per il quale sono necessari servizi collegati.</span><span class="sxs-lookup"><span data-stu-id="cdb30-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="cdb30-163">Servizio collegato per SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="cdb30-163">Linked service for on-premises SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="cdb30-164">Servizio collegato per archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="cdb30-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="cdb30-165">Servizio collegato per il database SQL Azure</span><span class="sxs-lookup"><span data-stu-id="cdb30-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <span data-ttu-id="cdb30-166"><a name="adf-linked-service-onprem-sql"></a>Servizio collegato per il database SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="cdb30-166"><a name="adf-linked-service-onprem-sql"></a>Linked service for on-premises SQL Server database</span></span>
<span data-ttu-id="cdb30-167">Per creare un servizio collegato per SQL Server locale:</span><span class="sxs-lookup"><span data-stu-id="cdb30-167">To create the linked service for the on-premises SQL Server:</span></span>

* <span data-ttu-id="cdb30-168">fare clic su **Archivio dati** nella pagina di destinazione di ADF nel portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="cdb30-168">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="cdb30-169">selezionare **SQL** e immettere il *nome utente* e la *password* per SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="cdb30-169">select **SQL** and enter the *username* and *password* credentials for the on-premises SQL Server.</span></span> <span data-ttu-id="cdb30-170">È necessario immettere il nome del server nella forma **nome dell'istanza nomeserver completa barra rovesciata (nomeserver\nomeistanza)**.</span><span class="sxs-lookup"><span data-stu-id="cdb30-170">You need to enter the servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="cdb30-171">Nome servizio collegato *adfonpremsql*.</span><span class="sxs-lookup"><span data-stu-id="cdb30-171">Name the linked service *adfonpremsql*.</span></span>

### <span data-ttu-id="cdb30-172"><a name="adf-linked-service-blob-store"></a>Servizi collegati per BLOB</span><span class="sxs-lookup"><span data-stu-id="cdb30-172"><a name="adf-linked-service-blob-store"></a>Linked service for Blob</span></span>
<span data-ttu-id="cdb30-173">Per creare un servizio collegato per l'account di archiviazione BLOB di Azure, è necessario:</span><span class="sxs-lookup"><span data-stu-id="cdb30-173">To create the linked service for the Azure Blob Storage account:</span></span>

* <span data-ttu-id="cdb30-174">fare clic su **Archivio dati** nella pagina di destinazione di ADF nel portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="cdb30-174">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="cdb30-175">selezionare **Account di archiviazione di Azure**</span><span class="sxs-lookup"><span data-stu-id="cdb30-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="cdb30-176">immettere il nome del contenitore e la chiave dell'account di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb30-176">enter the Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="cdb30-177">Rinominare il servizio collegato *adfds*.</span><span class="sxs-lookup"><span data-stu-id="cdb30-177">Name the Linked Service *adfds*.</span></span>

### <span data-ttu-id="cdb30-178"><a name="adf-linked-service-azure-sql"></a>Servizio collegato per il database SQL Azure</span><span class="sxs-lookup"><span data-stu-id="cdb30-178"><a name="adf-linked-service-azure-sql"></a>Linked service for Azure SQL database</span></span>
<span data-ttu-id="cdb30-179">Per creare un servizio collegato per il database SQL di Azure, è necessario:</span><span class="sxs-lookup"><span data-stu-id="cdb30-179">To create the linked service for the Azure SQL Database:</span></span>

* <span data-ttu-id="cdb30-180">fare clic su **Archivio dati** nella pagina di destinazione di ADF nel portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="cdb30-180">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="cdb30-181">selezionare **SQL di Azure** e immettere il *nome utente* e la *password* per il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb30-181">select **Azure SQL** and enter the *username* and *password* credentials for the Azure SQL Database.</span></span> <span data-ttu-id="cdb30-182">Il *nome utente* deve essere specificato come *user@servername*.</span><span class="sxs-lookup"><span data-stu-id="cdb30-182">The *username* must be specified as *user@servername*.</span></span>   

## <span data-ttu-id="cdb30-183"><a name="adf-tables"></a>Definire e creare tabelle per specificare la modalità di accesso al set di dati</span><span class="sxs-lookup"><span data-stu-id="cdb30-183"><a name="adf-tables"></a>Define and create tables to specify how to access the datasets</span></span>
<span data-ttu-id="cdb30-184">Creare tabelle che specificano la struttura, la posizione e la disponibilità dei set di dati con le seguenti procedure basate su script.</span><span class="sxs-lookup"><span data-stu-id="cdb30-184">Create tables that specify the structure, location, and availability of the datasets with the following script-based procedures.</span></span> <span data-ttu-id="cdb30-185">I file JSON vengono utilizzati per definire le tabelle.</span><span class="sxs-lookup"><span data-stu-id="cdb30-185">JSON files are used to define the tables.</span></span> <span data-ttu-id="cdb30-186">Per ulteriori informazioni sulla struttura di questi file, vedere [Set di dati](../data-factory/data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="cdb30-186">For more information on the structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cdb30-187">È necessario eseguire il cmdlet `Add-AzureAccount` prima di eseguire il cmdlet [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) per verificare che sia selezionata la sottoscrizione di Azure giusta per l'esecuzione del comando.</span><span class="sxs-lookup"><span data-stu-id="cdb30-187">You should execute the `Add-AzureAccount` cmdlet before executing the [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet to confirm that the right Azure subscription is selected for the command execution.</span></span> <span data-ttu-id="cdb30-188">Per la documentazione di questo cmdlet, vedere [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="cdb30-188">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="cdb30-189">Le definizioni basate su JSON nelle tabelle utilizzano i nomi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cdb30-189">The JSON-based definitions in the tables use the following names:</span></span>

* <span data-ttu-id="cdb30-190">il **nome della tabella** nel server SQL locale è *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="cdb30-190">the **table name** in the on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="cdb30-191">il **nome del contenitore** nell'account di archiviazione Blob di Azure è *nomecontenitore*</span><span class="sxs-lookup"><span data-stu-id="cdb30-191">the **container name** in the Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="cdb30-192">Per questa pipeline ADF sono necessarie tre definizioni di tabella:</span><span class="sxs-lookup"><span data-stu-id="cdb30-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="cdb30-193">Tabella SQL locale</span><span class="sxs-lookup"><span data-stu-id="cdb30-193">SQL on-premises Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="cdb30-194">Tabella BLOB </span><span class="sxs-lookup"><span data-stu-id="cdb30-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="cdb30-195">Tabella SQL Azure</span><span class="sxs-lookup"><span data-stu-id="cdb30-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="cdb30-196">Queste procedure utilizzano Azure PowerShell per definire e creare le attività del file ADF.</span><span class="sxs-lookup"><span data-stu-id="cdb30-196">These procedures use Azure PowerShell to define and create the ADF activities.</span></span> <span data-ttu-id="cdb30-197">Tuttavia, queste attività possono inoltre essere eseguite tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb30-197">But these tasks can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="cdb30-198">Per informazioni dettagliate, vedere [Creare set di dati](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span><span class="sxs-lookup"><span data-stu-id="cdb30-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <span data-ttu-id="cdb30-199"><a name="adf-table-onprem-sql"></a>Tabella SQL locale</span><span class="sxs-lookup"><span data-stu-id="cdb30-199"><a name="adf-table-onprem-sql"></a>SQL on-premises Table</span></span>
<span data-ttu-id="cdb30-200">La definizione della tabella per SQL Server locale viene specificata nel file JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="cdb30-200">The table definition for the on-premises SQL Server is specified in the following JSON file:</span></span>

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

<span data-ttu-id="cdb30-201">Qui non sono inclusi i nomi di colonna.</span><span class="sxs-lookup"><span data-stu-id="cdb30-201">The column names were not included here.</span></span> <span data-ttu-id="cdb30-202">È possibile sottoselezionare i nomi delle colonne includendoli qui (per ulteriori informazioni consultare l'argomento [Documentazione ADF](../data-factory/data-factory-data-movement-activities.md) ).</span><span class="sxs-lookup"><span data-stu-id="cdb30-202">You can sub-select on the column names by including them here (for details check the [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="cdb30-203">Copiare la definizione JSON della tabella in un file denominata *onpremtabledef.json* e salvarlo in una posizione nota (generalmente *C:\temp\onpremtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="cdb30-203">Copy the JSON definition of the table into a file called *onpremtabledef.json* file and save it to a known location (here assumed to be *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="cdb30-204">Creare la tabella nel file ADF con il seguente cmdlet Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="cdb30-204">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <span data-ttu-id="cdb30-205"><a name="adf-table-blob-store"></a>Tabella BLOB</span><span class="sxs-lookup"><span data-stu-id="cdb30-205"><a name="adf-table-blob-store"></a>Blob Table</span></span>
<span data-ttu-id="cdb30-206">La definizione della tabella per il percorso del BLOB di output è la seguente. I dati inseriti vengono così mappati dal server locale al BLOB di Azure:</span><span class="sxs-lookup"><span data-stu-id="cdb30-206">Definition for the table for the output blob location is in the following (this maps the ingested data from on-premises to Azure blob):</span></span>

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

<span data-ttu-id="cdb30-207">Copiare la definizione JSON della tabella in un file denominata *bloboutputtabledef.json* e salvarlo in una posizione nota (generalmente *C:\temp\bloboutputtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="cdb30-207">Copy the JSON definition of the table into a file called *bloboutputtabledef.json* file and save it to a known location (here assumed to be *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="cdb30-208">Creare la tabella nel file ADF con il seguente cmdlet Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="cdb30-208">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <span data-ttu-id="cdb30-209"><a name="adf-table-azure-sq"></a>Tabella SQL Azure</span><span class="sxs-lookup"><span data-stu-id="cdb30-209"><a name="adf-table-azure-sq"></a>SQL Azure Table</span></span>
<span data-ttu-id="cdb30-210">La definizione della tabella per l’output SQL Azure è la seguente (questo schema associa i dati provenienti dal blob):</span><span class="sxs-lookup"><span data-stu-id="cdb30-210">Definition for the table for the SQL Azure output is in the following (this schema maps the data coming from the blob):</span></span>

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

<span data-ttu-id="cdb30-211">Copiare la definizione JSON della tabella in un file denominata *AzureSqlTable.json* e salvarlo in una posizione nota (generalmente *C:\temp\AzureSqlTable.json*).</span><span class="sxs-lookup"><span data-stu-id="cdb30-211">Copy the JSON definition of the table into a file called *AzureSqlTable.json* file and save it to a known location (here assumed to be *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="cdb30-212">Creare la tabella nel file ADF con il seguente cmdlet Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="cdb30-212">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <span data-ttu-id="cdb30-213"><a name="adf-pipeline"></a>Definire e creare la pipeline</span><span class="sxs-lookup"><span data-stu-id="cdb30-213"><a name="adf-pipeline"></a>Define and create the pipeline</span></span>
<span data-ttu-id="cdb30-214">Specificare le attività che appartengono alla pipeline e creare la pipeline con le seguenti procedure basate su script.</span><span class="sxs-lookup"><span data-stu-id="cdb30-214">Specify the activities that belong to the pipeline and create the pipeline with the following script-based procedures.</span></span> <span data-ttu-id="cdb30-215">Un file JSON viene utilizzato per definire le proprietà della pipeline.</span><span class="sxs-lookup"><span data-stu-id="cdb30-215">A JSON file is used to define the pipeline properties.</span></span>

* <span data-ttu-id="cdb30-216">Lo script presuppone che il **nome della pipeline** sia *AMLDSProcessPipeline*.</span><span class="sxs-lookup"><span data-stu-id="cdb30-216">The script assumes that the **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="cdb30-217">Si noti inoltre che abbiamo impostato la periodicità della pipeline per l’esecuzione su base giornaliera e utilizza il tempo di esecuzione predefinito per il processo (12 am UTC).</span><span class="sxs-lookup"><span data-stu-id="cdb30-217">Also note that we set the periodicity of the pipeline to be executed on daily basis and use the default execution time for the job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="cdb30-218">Le procedure seguenti utilizzano Azure PowerShell per definire e creare la pipeline del file ADF.</span><span class="sxs-lookup"><span data-stu-id="cdb30-218">The following procedures use Azure PowerShell to define and create the ADF pipeline.</span></span> <span data-ttu-id="cdb30-219">Tuttavia, questa attività può inoltre essere eseguita tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cdb30-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="cdb30-220">Per informazioni dettagliate, vedere [Creare una pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span><span class="sxs-lookup"><span data-stu-id="cdb30-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="cdb30-221">Se si utilizzano le definizioni di tabella fornite in precedenza, la definizione della pipeline per il file ADF viene specificata come segue:</span><span class="sxs-lookup"><span data-stu-id="cdb30-221">Using the table definitions provided previously, the pipeline definition for the ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL to Azure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server to blob",     
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
                        "description": "Push data to Sql Azure",        
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

<span data-ttu-id="cdb30-222">Copiare la definizione JSON della pipeline in un file denominato *pipelinedef.json* e salvarlo in una posizione nota (generalmente *C:\temp\pipelinedef.json*).</span><span class="sxs-lookup"><span data-stu-id="cdb30-222">Copy this JSON definition of the pipeline into a file called *pipelinedef.json* file and save it to a known location (here assumed to be *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="cdb30-223">Creare la pipeline ADF con il seguente cmdlet Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="cdb30-223">Create the pipeline in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="cdb30-224">Accertarsi che sia possibile visualizzare la pipeline nel file ADF sul portale di Azure classico come indicato di seguito (quando si fa clic sul diagramma)</span><span class="sxs-lookup"><span data-stu-id="cdb30-224">Confirm that you can see the pipeline on the ADF in the Azure Classic Portal show up as following (when you click the diagram)</span></span>

![Pipeline ADF](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <span data-ttu-id="cdb30-226"><a name="adf-pipeline-start"></a>Avviare la pipeline</span><span class="sxs-lookup"><span data-stu-id="cdb30-226"><a name="adf-pipeline-start"></a>Start the Pipeline</span></span>
<span data-ttu-id="cdb30-227">La pipeline è avviabile con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cdb30-227">The pipeline can now be run using the following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="cdb30-228">I valori del parametro *startdate* ed *enddate* devono essere sostituiti con le date effettive tra le quali si desidera eseguire la pipeline.</span><span class="sxs-lookup"><span data-stu-id="cdb30-228">The *startdate* and *enddate* parameter values need to be replaced with the actual dates between which you want the pipeline to run.</span></span>

<span data-ttu-id="cdb30-229">Una volta eseguita la pipeline, si dovrebbe poter visualizzare i dati visualizzati nel contenitore selezionato per il blob, un file al giorno.</span><span class="sxs-lookup"><span data-stu-id="cdb30-229">Once the pipeline executes, you should be able to see the data show up in the container selected for the blob, one file per day.</span></span>

<span data-ttu-id="cdb30-230">Si noti che non abbiamo utilizzato la funzionalità fornita da ADF per dirigere i dati in modo incrementale.</span><span class="sxs-lookup"><span data-stu-id="cdb30-230">Note that we have not leveraged the functionality provided by ADF to pipe data incrementally.</span></span> <span data-ttu-id="cdb30-231">Per ulteriori informazioni su come eseguire questa e altre funzionalità fornite da ADF, vedere la [documentazione ADF](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="cdb30-231">For more information on how to do this and other capabilities provided by ADF, see the [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
