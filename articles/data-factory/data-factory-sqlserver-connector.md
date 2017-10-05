---
title: Spostare i dati da e verso SQL Server | Microsoft Docs
description: Informazioni su come spostare i dati da/verso il database di SQL Server locale o in una VM di Azure utilizzando Data factory di Azure.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: 9cd2077d897631457925cda5ef5e6df3c0c33177
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="2dbbb-103">Spostare i dati da e verso SQL Server locale o in IaaS (VM di Azure) utilizzando Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="2dbbb-103">Move data to and from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="2dbbb-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da e verso un database SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="2dbbb-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="2dbbb-106">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="2dbbb-106">Supported scenarios</span></span>
<span data-ttu-id="2dbbb-107">È possibile copiare i dati **da un database SQL Server** negli archivi di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="2dbbb-107">You can copy data **from a SQL Server database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="2dbbb-108">È possibile copiare i dati dagli archivi dati seguenti **a un database SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="2dbbb-108">You can copy data from the following data stores **to a SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="2dbbb-109">Versioni di SQL Server supportate</span><span class="sxs-lookup"><span data-stu-id="2dbbb-109">Supported SQL Server versions</span></span>
<span data-ttu-id="2dbbb-110">Questo connettore di SQL Server supporta la copia dei dati da e verso le seguenti versioni dell'istanza ospitate in locale o in IaaS di Azure tramite l'autenticazione SQL e l'autenticazione Windows: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="2dbbb-110">This SQL Server connector support copying data from/to the following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="2dbbb-111">Abilitazione della connettività</span><span class="sxs-lookup"><span data-stu-id="2dbbb-111">Enabling connectivity</span></span>
<span data-ttu-id="2dbbb-112">I concetti e i passaggi necessari per la connessione con SQL Server ospitato in locale o in macchine virtuali di Azure IaaS (Infrastructure-as-a-Service) sono gli stessi.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-112">The concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are the same.</span></span> <span data-ttu-id="2dbbb-113">In entrambi i casi, è necessario usare il Gateway di gestione dati per la connettività.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-113">In both cases, you need to use Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="2dbbb-114">Vedere l'articolo sullo [spostamento di dati tra sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) per informazioni sul Gateway di gestione dati e per istruzioni dettagliate sulla configurazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="2dbbb-115">L'impostazione di un'istanza del gateway è un prerequisito per la connessione con SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="2dbbb-116">Sebbene sia possibile installare il gateway nello stesso computer locale o istanza cloud della macchina virtuale come SQL Server per migliorare le prestazioni, si consiglia di installarli in computer separati,</span><span class="sxs-lookup"><span data-stu-id="2dbbb-116">While you can install gateway on the same on-premises machine or cloud VM instance as the SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="2dbbb-117">per evitare che il gateway e il server SQL entrino in conflitto sulle risorse.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-117">Having the gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2dbbb-118">Introduzione</span><span class="sxs-lookup"><span data-stu-id="2dbbb-118">Getting started</span></span>
<span data-ttu-id="2dbbb-119">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un SQL Server locale usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="2dbbb-120">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="2dbbb-121">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="2dbbb-122">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2dbbb-123">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="2dbbb-124">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="2dbbb-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="2dbbb-125">Creare una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-125">Create a **data factory**.</span></span> <span data-ttu-id="2dbbb-126">Una data factory può contenere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="2dbbb-127">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="2dbbb-128">Ad esempio, se si copiano i dati da un database SQL Server in un'archiviazione BLOB di Azure, si creano due servizi collegati per collegare il database SQL Server e l'account di archiviazione di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-128">For example, if you are copying data from a SQL Server database to an Azure blob storage, you create two linked services to link your SQL Server database and Azure storage account to your data factory.</span></span> <span data-ttu-id="2dbbb-129">Per le proprietà del servizio collegato specifiche per il database SQL Server, vedere la sezione sulle [proprietà del servizio collegato](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-129">For linked service properties that are specific to SQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="2dbbb-130">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="2dbbb-131">Nell'esempio citato nel passaggio precedente, si crea un set di dati per specificare la tabella nel database SQL Server che contiene i dati di input.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-131">In the example mentioned in the last step, you create a dataset to specify the SQL table in your SQL Server database that contains the input data.</span></span> <span data-ttu-id="2dbbb-132">Si crea anche un altro set di dati per specificare il contenitore BLOB e la cartella che contiene i dati copiati dal database SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-132">And, you create another dataset to specify the blob container and the folder that holds the data copied from the SQL Server database.</span></span> <span data-ttu-id="2dbbb-133">Per le proprietà del set di dati specifiche per il database SQL Server, vedere la sezione sulle [proprietà del set di dati](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-133">For dataset properties that are specific to SQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="2dbbb-134">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="2dbbb-135">Nell'esempio indicato in precedenza si usa SqlSource come origine e BlobSink come sink per l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-135">In the example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="2dbbb-136">Analogamente, se si effettua la copia dall'archiviazione BLOB di Azure al database SQL Server, usare BlobSource e SqlSink nell'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-136">Similarly, if you are copying from Azure Blob Storage to SQL Server Database, you use BlobSource and SqlSink in the copy activity.</span></span> <span data-ttu-id="2dbbb-137">Per le proprietà dell'attività di copia specifiche per il database SQL Server, vedere la sezione sulle [proprietà dell'attività di copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-137">For copy activity properties that are specific to SQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="2dbbb-138">Per informazioni dettagliate su come usare un archivio dati come origine o come sink, fare clic sul collegamento nella sezione precedente per l'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="2dbbb-139">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="2dbbb-140">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="2dbbb-141">Per esempi con definizioni JSON per le entità di Data Factory che vengono usate per copiare dati da e verso un database SQL Server locale, vedere la sezione degli [esempi JSON](#json-examples-for-copying-data-from-and-to-sql-server) in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="2dbbb-142">Nelle sezioni seguenti sono disponibili le informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità della Data Factory specifiche di SQL Server:</span><span class="sxs-lookup"><span data-stu-id="2dbbb-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to SQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="2dbbb-143">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="2dbbb-143">Linked service properties</span></span>
<span data-ttu-id="2dbbb-144">Viene creato un servizio collegato di tipo **OnPremisesSqlServer** per collegare un database di SQL Server locale a una data factory.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-144">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="2dbbb-145">La tabella seguente contiene le descrizioni degli elementi JSON specifici per il servizio collegato di SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-145">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="2dbbb-146">La tabella seguente contiene le descrizioni degli elementi JSON specifici del servizio collegato SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-146">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="2dbbb-147">Proprietà</span><span class="sxs-lookup"><span data-stu-id="2dbbb-147">Property</span></span> | <span data-ttu-id="2dbbb-148">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2dbbb-148">Description</span></span> | <span data-ttu-id="2dbbb-149">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2dbbb-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2dbbb-150">type</span><span class="sxs-lookup"><span data-stu-id="2dbbb-150">type</span></span> |<span data-ttu-id="2dbbb-151">La proprietà type deve essere impostata su **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-151">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="2dbbb-152">Sì</span><span class="sxs-lookup"><span data-stu-id="2dbbb-152">Yes</span></span> |
| <span data-ttu-id="2dbbb-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="2dbbb-153">connectionString</span></span> |<span data-ttu-id="2dbbb-154">Specificare le informazioni di connectionString necessarie per connettersi al database di SQL Server locale usando l'autenticazione di SQL o Windows.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-154">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="2dbbb-155">Sì</span><span class="sxs-lookup"><span data-stu-id="2dbbb-155">Yes</span></span> |
| <span data-ttu-id="2dbbb-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="2dbbb-156">gatewayName</span></span> |<span data-ttu-id="2dbbb-157">Nome del gateway che il servizio Data factory deve usare per connettersi al database di SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-157">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="2dbbb-158">Sì</span><span class="sxs-lookup"><span data-stu-id="2dbbb-158">Yes</span></span> |
| <span data-ttu-id="2dbbb-159">username</span><span class="sxs-lookup"><span data-stu-id="2dbbb-159">username</span></span> |<span data-ttu-id="2dbbb-160">Specificare il nome utente se si usa l'autenticazione Windows.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="2dbbb-161">Esempio: **nomedominio\\nomeutente**.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="2dbbb-162">No</span><span class="sxs-lookup"><span data-stu-id="2dbbb-162">No</span></span> |
| <span data-ttu-id="2dbbb-163">password</span><span class="sxs-lookup"><span data-stu-id="2dbbb-163">password</span></span> |<span data-ttu-id="2dbbb-164">Specificare la password per l'account utente specificato per il nome utente.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-164">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="2dbbb-165">No</span><span class="sxs-lookup"><span data-stu-id="2dbbb-165">No</span></span> |

<span data-ttu-id="2dbbb-166">È possibile crittografare le credenziali usando il cmdlet **New-AzureRmDataFactoryEncryptValue** e usarle nella stringa di connessione, come illustrato nell'esempio seguente (proprietà **EncryptedCredential**):</span><span class="sxs-lookup"><span data-stu-id="2dbbb-166">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="2dbbb-167">Esempi</span><span class="sxs-lookup"><span data-stu-id="2dbbb-167">Samples</span></span>
<span data-ttu-id="2dbbb-168">**JSON per l'uso dell'Autenticazione di SQL**</span><span class="sxs-lookup"><span data-stu-id="2dbbb-168">**JSON for using SQL Authentication**</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
<span data-ttu-id="2dbbb-169">**JSON per l'uso dell'Autenticazione Windows**</span><span class="sxs-lookup"><span data-stu-id="2dbbb-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="2dbbb-170">Gateway di gestione dati rappresenta l'account utente specificato per la connessione al database SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-170">Data Management Gateway will impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="2dbbb-171">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="2dbbb-171">Dataset properties</span></span>
<span data-ttu-id="2dbbb-172">Negli esempi si è usato un set di dati di tipo **SqlServerTable** per rappresentare una tabella in un database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-172">In the samples, you have used a dataset of type **SqlServerTable** to represent a table in a SQL Server database.</span></span>  

<span data-ttu-id="2dbbb-173">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2dbbb-174">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati (SQL Server, BLOB di Azure, tabelle di Azure e così via).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2dbbb-175">La sezione typeProperties è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-175">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="2dbbb-176">La sezione **typeProperties** per il set di dati di tipo **SqlServerTable** presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="2dbbb-176">The **typeProperties** section for the dataset of type **SqlServerTable** has the following properties:</span></span>

| <span data-ttu-id="2dbbb-177">Proprietà</span><span class="sxs-lookup"><span data-stu-id="2dbbb-177">Property</span></span> | <span data-ttu-id="2dbbb-178">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2dbbb-178">Description</span></span> | <span data-ttu-id="2dbbb-179">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2dbbb-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2dbbb-180">tableName</span><span class="sxs-lookup"><span data-stu-id="2dbbb-180">tableName</span></span> |<span data-ttu-id="2dbbb-181">Nome della tabella o vista nell'istanza del database di SQL Server a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-181">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="2dbbb-182">Sì</span><span class="sxs-lookup"><span data-stu-id="2dbbb-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="2dbbb-183">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="2dbbb-183">Copy activity properties</span></span>
<span data-ttu-id="2dbbb-184">Se si effettua il trasferimento dei dati da un database di SQL Server, impostare il tipo di origine nell'attività di copia su **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-184">If you are moving data from a SQL Server database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="2dbbb-185">Analogamente, se si effettua il trasferimento dei dati in un database di SQL Server, impostare il tipo di sink nell'attività di copia su **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-185">Similarly, if you are moving data to a SQL Server database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="2dbbb-186">Questa sezione presenta un elenco delle proprietà supportate da SqlSource e SqlSink.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="2dbbb-187">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-187">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2dbbb-188">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="2dbbb-189">L'attività di copia accetta solo un input e produce solo un output.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-189">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="2dbbb-190">Le proprietà disponibili nella sezione typeProperties dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-190">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="2dbbb-191">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-191">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="2dbbb-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="2dbbb-192">SqlSource</span></span>
<span data-ttu-id="2dbbb-193">Se in un'attività di copia l'origine è di tipo **SqlSource**, nella sezione **typeProperties** sono disponibili le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="2dbbb-193">When source in a copy activity is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="2dbbb-194">Proprietà</span><span class="sxs-lookup"><span data-stu-id="2dbbb-194">Property</span></span> | <span data-ttu-id="2dbbb-195">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2dbbb-195">Description</span></span> | <span data-ttu-id="2dbbb-196">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="2dbbb-196">Allowed values</span></span> | <span data-ttu-id="2dbbb-197">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2dbbb-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2dbbb-198">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="2dbbb-198">sqlReaderQuery</span></span> |<span data-ttu-id="2dbbb-199">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-199">Use the custom query to read data.</span></span> |<span data-ttu-id="2dbbb-200">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-200">SQL query string.</span></span> <span data-ttu-id="2dbbb-201">Ad esempio: selezionare * da MyTable.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-201">For example: select * from MyTable.</span></span> <span data-ttu-id="2dbbb-202">Può fare riferimento a più tabelle del database a cui fa riferimento il set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-202">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="2dbbb-203">Se non specificato, l'istruzione SQL eseguita: selezionare da MyTable.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-203">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="2dbbb-204">No</span><span class="sxs-lookup"><span data-stu-id="2dbbb-204">No</span></span> |
| <span data-ttu-id="2dbbb-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="2dbbb-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="2dbbb-206">Nome della stored procedure che legge i dati dalla tabella di origine.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-206">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="2dbbb-207">Nome della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-207">Name of the stored procedure.</span></span> <span data-ttu-id="2dbbb-208">L'ultima istruzione SQL deve essere un'istruzione SELECT nella stored procedure.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-208">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="2dbbb-209">No</span><span class="sxs-lookup"><span data-stu-id="2dbbb-209">No</span></span> |
| <span data-ttu-id="2dbbb-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="2dbbb-210">storedProcedureParameters</span></span> |<span data-ttu-id="2dbbb-211">Parametri per la stored procedure.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-211">Parameters for the stored procedure.</span></span> |<span data-ttu-id="2dbbb-212">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-212">Name/value pairs.</span></span> <span data-ttu-id="2dbbb-213">I nomi e le maiuscole e minuscole dei parametri devono corrispondere ai nomi e alle maiuscole e minuscole dei parametri della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-213">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="2dbbb-214">No</span><span class="sxs-lookup"><span data-stu-id="2dbbb-214">No</span></span> |

<span data-ttu-id="2dbbb-215">Se la proprietà **sqlReaderQuery** è specificata per SqlSource, l'attività di copia esegue questa query nell'origine del database del server di SQL per ottenere i dati.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-215">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="2dbbb-216">In alternativa, è possibile specificare una stored procedure indicando i parametri **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se la stored procedure accetta parametri).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-216">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="2dbbb-217">Se non si specifica il parametro sqlReaderQuery o sqlReaderStoredProcedureName, le colonne definite nella sezione della struttura vengono usate per compilare una query da eseguire nel database del server di SQL.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="2dbbb-218">Se la definizione del set di dati non dispone della struttura, vengono selezionate tutte le colonne della tabella.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-218">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="2dbbb-219">Quando si usa **sqlReaderStoredProcedureName** è necessario specificare un valore per la proprietà **tableName** nel set di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-219">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="2dbbb-220">Non sono disponibili convalide eseguite su questa tabella.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="2dbbb-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="2dbbb-221">SqlSink</span></span>
<span data-ttu-id="2dbbb-222">**SqlSink** supporta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="2dbbb-222">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="2dbbb-223">Proprietà</span><span class="sxs-lookup"><span data-stu-id="2dbbb-223">Property</span></span> | <span data-ttu-id="2dbbb-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2dbbb-224">Description</span></span> | <span data-ttu-id="2dbbb-225">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="2dbbb-225">Allowed values</span></span> | <span data-ttu-id="2dbbb-226">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2dbbb-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2dbbb-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="2dbbb-227">writeBatchTimeout</span></span> |<span data-ttu-id="2dbbb-228">Tempo di attesa per l'operazione di inserimento batch da completare prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-228">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="2dbbb-229">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="2dbbb-229">timespan</span></span><br/><br/> <span data-ttu-id="2dbbb-230">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="2dbbb-231">No</span><span class="sxs-lookup"><span data-stu-id="2dbbb-231">No</span></span> |
| <span data-ttu-id="2dbbb-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="2dbbb-232">writeBatchSize</span></span> |<span data-ttu-id="2dbbb-233">Inserisce dati nella tabella SQL quando la dimensione del buffer raggiunge writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-233">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="2dbbb-234">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="2dbbb-234">Integer (number of rows)</span></span> |<span data-ttu-id="2dbbb-235">No (valore predefinito: 10000)</span><span class="sxs-lookup"><span data-stu-id="2dbbb-235">No (default: 10000)</span></span> |
| <span data-ttu-id="2dbbb-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="2dbbb-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="2dbbb-237">Specificare la query per l'attività di copia da eseguire in modo che i dati di una sezione specifica vengano eliminati.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-237">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="2dbbb-238">Per altre informazioni, vedere la sezione [Copia ripetibile](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="2dbbb-239">Istruzione di query.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-239">A query statement.</span></span> |<span data-ttu-id="2dbbb-240">No</span><span class="sxs-lookup"><span data-stu-id="2dbbb-240">No</span></span> |
| <span data-ttu-id="2dbbb-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="2dbbb-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="2dbbb-242">Specificare il nome della colonna per l'attività di copia da riempire con l'identificatore di sezione generato automaticamente, che viene usato per eliminare i dati di una sezione specifica quando viene nuovamente eseguita.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-242">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="2dbbb-243">Per altre informazioni, vedere la sezione [Copia ripetibile](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="2dbbb-244">Nome di colonna di una colonna con tipo di dati binario (32).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="2dbbb-245">No</span><span class="sxs-lookup"><span data-stu-id="2dbbb-245">No</span></span> |
| <span data-ttu-id="2dbbb-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="2dbbb-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="2dbbb-247">Nome della stored procedure che esegue l'upsert (aggiornamenti/inserimenti) nella tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-247">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="2dbbb-248">Nome della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-248">Name of the stored procedure.</span></span> |<span data-ttu-id="2dbbb-249">No</span><span class="sxs-lookup"><span data-stu-id="2dbbb-249">No</span></span> |
| <span data-ttu-id="2dbbb-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="2dbbb-250">storedProcedureParameters</span></span> |<span data-ttu-id="2dbbb-251">Parametri per la stored procedure.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-251">Parameters for the stored procedure.</span></span> |<span data-ttu-id="2dbbb-252">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-252">Name/value pairs.</span></span> <span data-ttu-id="2dbbb-253">I nomi e le maiuscole e minuscole dei parametri devono corrispondere ai nomi e alle maiuscole e minuscole dei parametri della stored procedure.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-253">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="2dbbb-254">No</span><span class="sxs-lookup"><span data-stu-id="2dbbb-254">No</span></span> |
| <span data-ttu-id="2dbbb-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="2dbbb-255">sqlWriterTableType</span></span> |<span data-ttu-id="2dbbb-256">Specificare il tipo di tabella da usare nella stored procedure.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-256">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="2dbbb-257">L'attività di copia rende i dati spostati disponibili in una tabella temporanea con questo tipo di tabella.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-257">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="2dbbb-258">Il codice della stored procedure può quindi unire i dati copiati con i dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-258">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="2dbbb-259">Nome del tipo di tabella.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-259">A table type name.</span></span> |<span data-ttu-id="2dbbb-260">No</span><span class="sxs-lookup"><span data-stu-id="2dbbb-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-to-sql-server"></a><span data-ttu-id="2dbbb-261">Esempi JSON per la copia dei dati da e a SQL Server</span><span class="sxs-lookup"><span data-stu-id="2dbbb-261">JSON examples for copying data from and to SQL Server</span></span>
<span data-ttu-id="2dbbb-262">Gli esempi seguenti forniscono le definizioni JSON di esempio da usare per creare una pipeline con il [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-262">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2dbbb-263">Gli esempi seguenti mostrano come copiare dati da e verso SQL Server e l'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-263">The following samples show how to copy data to and from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="2dbbb-264">Tuttavia, i dati possono essere copiati **direttamente** da una delle origini in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-264">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-to-azure-blob"></a><span data-ttu-id="2dbbb-265">Esempio: Copiare i dati da SQL Server al BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="2dbbb-265">Example: Copy data from SQL Server to Azure Blob</span></span>
<span data-ttu-id="2dbbb-266">L'esempio seguente mostra:</span><span class="sxs-lookup"><span data-stu-id="2dbbb-266">The following sample shows:</span></span>

1. <span data-ttu-id="2dbbb-267">Un servizio collegato di tipo [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="2dbbb-268">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="2dbbb-269">Un [set di dati](data-factory-create-datasets.md) di tipo [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="2dbbb-270">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="2dbbb-271">La [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [SqlSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-271">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2dbbb-272">L'esempio copia i dati di una serie temporale dalla tabella del server SQL in un archivio BLOB di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-272">The sample copies time-series data from a SQL Server table to an Azure blob every hour.</span></span> <span data-ttu-id="2dbbb-273">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-273">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="2dbbb-274">Come primo passaggio, impostare il Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-274">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="2dbbb-275">Le istruzioni sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="2dbbb-275">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="2dbbb-276">**Servizio collegato di SQL Server**</span><span class="sxs-lookup"><span data-stu-id="2dbbb-276">**SQL Server linked service**</span></span>
```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="2dbbb-277">**Servizio collegato di archiviazione BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="2dbbb-277">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="2dbbb-278">**Set di dati input di SQL Server**</span><span class="sxs-lookup"><span data-stu-id="2dbbb-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="2dbbb-279">L'esempio presuppone che sia stata creata una tabella "MyTable" in SQL Server e che contenga una colonna denominata "timestampcolumn" per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-279">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="2dbbb-280">È possibile eseguire query su più tabelle all'interno dello stesso database usando un singolo set di dati, ma come typeProperty tableName del set di dati deve essere usata una sola tabella.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-280">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="2dbbb-281">Impostando "external" su "true" si comunica al servizio Data Factory che il set di dati è esterno a Data Factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-281">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "SqlServerInput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
<span data-ttu-id="2dbbb-282">**Set di dati di output del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="2dbbb-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="2dbbb-283">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-283">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="2dbbb-284">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-284">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="2dbbb-285">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-285">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="2dbbb-286">**Pipeline con attività di copia**</span><span class="sxs-lookup"><span data-stu-id="2dbbb-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="2dbbb-287">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-287">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="2dbbb-288">Nella definizione JSON della pipeline, il tipo **source** è impostato su **SqlSource** e il tipo **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-288">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="2dbbb-289">La query SQL specificata per la proprietà **SqlReaderQuery** consente di selezionare i dati da copiare nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-289">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```
<span data-ttu-id="2dbbb-290">In questo esempio la proprietà **sqlReaderQuery** è specificata per SqlSource.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-290">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="2dbbb-291">L'attività di copia esegue questa query nell'origine del database del server SQL per ottenere i dati.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-291">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="2dbbb-292">In alternativa, è possibile specificare una stored procedure indicando i parametri **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se la stored procedure accetta parametri).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-292">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="2dbbb-293">La proprietà sqlReaderQuery può fare riferimento a più tabelle nel database a cui fa riferimento il set di dati di input.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-293">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="2dbbb-294">Non è limitato solo alla tabella impostata come typeProperty tableName del set di dati.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-294">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="2dbbb-295">Se non si specifica il parametro sqlReaderQuery o sqlReaderStoredProcedureName, le colonne definite nella sezione della struttura vengono usate per compilare una query di selezione da eseguire nel database del server di SQL.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="2dbbb-296">Se la definizione del set di dati non dispone della struttura, vengono selezionate tutte le colonne della tabella.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-296">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="2dbbb-297">Vedere la sezione [SqlSource](#sqlsource) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) per l'elenco delle proprietà supportate da SqlSource e BlobSink.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-297">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-to-sql-server"></a><span data-ttu-id="2dbbb-298">Esempio: Copiare i dati dal BLOB di Azure in SQL Server</span><span class="sxs-lookup"><span data-stu-id="2dbbb-298">Example: Copy data from Azure Blob to SQL Server</span></span>
<span data-ttu-id="2dbbb-299">L'esempio seguente mostra:</span><span class="sxs-lookup"><span data-stu-id="2dbbb-299">The following sample shows:</span></span>

1. <span data-ttu-id="2dbbb-300">Il servizio collegato di tipo [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-300">The linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="2dbbb-301">Il servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-301">The linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="2dbbb-302">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="2dbbb-303">Un [set di dati](data-factory-create-datasets.md) di output di tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="2dbbb-304">La [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-304">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="2dbbb-305">L'esempio copia i dati di una serie temporale da un archivio BLOB di Azure a una tabella del server SQL ogni ora.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-305">The sample copies time-series data from an Azure blob to a SQL Server table every hour.</span></span> <span data-ttu-id="2dbbb-306">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-306">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="2dbbb-307">**Servizio collegato di SQL Server**</span><span class="sxs-lookup"><span data-stu-id="2dbbb-307">**SQL Server linked service**</span></span>

```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="2dbbb-308">**Servizio collegato di archiviazione BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="2dbbb-308">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="2dbbb-309">**Set di dati di input del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="2dbbb-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="2dbbb-310">I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="2dbbb-311">Il percorso della cartella e il nome del file per il BLOB vengono valutati dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-311">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="2dbbb-312">Il percorso della cartella usa le parti anno, mese, e giorno dell'ora di inizio e il nome del file usa la parte dell'ora di inizio relativa all'ora.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-312">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="2dbbb-313">L'impostazione di "external" su "true" comunica al servizio Data Factory che il set di dati è esterno a Data Factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-313">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
<span data-ttu-id="2dbbb-314">**Set di dati output di SQL Server**</span><span class="sxs-lookup"><span data-stu-id="2dbbb-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="2dbbb-315">L'esempio copia i dati in una tabella denominata "MyTable" in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-315">The sample copies data to a table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="2dbbb-316">Creare la tabella in SQL Server con lo stesso numero di colonne di quelle contenute nel file con estensione csv del BLOB.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-316">Create the table in SQL Server with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="2dbbb-317">Alla tabella vengono aggiunte nuove righe ogni ora.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-317">New rows are added to the table every hour.</span></span>

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="2dbbb-318">**Pipeline con attività di copia**</span><span class="sxs-lookup"><span data-stu-id="2dbbb-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="2dbbb-319">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-319">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="2dbbb-320">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **BlobSource** e il tipo **sink** è impostato su **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-320">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="2dbbb-321">Risoluzione dei problemi di connessione</span><span class="sxs-lookup"><span data-stu-id="2dbbb-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="2dbbb-322">Configurare SQL Server per accettare le connessioni remote.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-322">Configure your SQL Server to accept remote connections.</span></span> <span data-ttu-id="2dbbb-323">Avviare **SQL Server Management Studio**, fare clic con il pulsante destro del mouse su **server** e selezionare **Properties**.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="2dbbb-324">Scegliere **Connessioni** dall'elenco e selezionare **Consenti connessioni remote al server**.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-324">Select **Connections** from the list and check **Allow remote connections to the server**.</span></span>

    ![Abilitare le connessioni remote](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="2dbbb-326">Per una procedura dettagliata, vedere [Configurare l'opzione di configurazione del server remote access](https://msdn.microsoft.com/library/ms191464.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2dbbb-326">See [Configure the remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="2dbbb-327">Avviare **Gestione configurazione SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="2dbbb-328">Espandere **Configurazione di rete SQL Server** per l'istanza prevista e selezionare **Protocolli per MSSQLSERVER**.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-328">Expand **SQL Server Network Configuration** for the instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="2dbbb-329">I protocolli sono visualizzati nel riquadro di destra.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-329">You should see protocols in the right-pane.</span></span> <span data-ttu-id="2dbbb-330">Abilitare il protocollo TCP/IP facendo clic con il pulsante destro del mouse su **TCP/IP** e selezionando **Abilita**.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![Abilitare TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="2dbbb-332">Per informazioni dettagliate e modalità alternative di abilitazione del protocollo TCP/IP, vedere [Abilitare o disabilitare un protocollo di rete del server](https://msdn.microsoft.com/library/ms191294.aspx).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="2dbbb-333">Nella stessa finestra fare doppio clic su **TCP/IP** per aprire la finestra **Proprietà TCP/IP**.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-333">In the same window, double-click **TCP/IP** to launch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="2dbbb-334">Passare alla scheda **Indirizzi IP** .</span><span class="sxs-lookup"><span data-stu-id="2dbbb-334">Switch to the **IP Addresses** tab.</span></span> <span data-ttu-id="2dbbb-335">Scorrere verso il basso per vedere la sezione **IPAll** .</span><span class="sxs-lookup"><span data-stu-id="2dbbb-335">Scroll down to see **IPAll** section.</span></span> <span data-ttu-id="2dbbb-336">Annotare la **Porta TCP**: il valore predefinito è **1433**.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-336">Note down the **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="2dbbb-337">Creare una **regola per Windows Firewall** nel computer per consentire il traffico in ingresso attraverso questa porta.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-337">Create a **rule for the Windows Firewall** on the machine to allow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="2dbbb-338">**Verificare la connessione**: per connettersi al server SQL con un nome completo, usare SQL Server Management Studio da un computer diverso.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-338">**Verify connection**: To connect to the SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="2dbbb-339">Ad esempio: "<machine><domain>.corp<company>.com,1433."</span><span class="sxs-lookup"><span data-stu-id="2dbbb-339">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="2dbbb-340">Per informazioni dettagliate, vedere [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-340">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="2dbbb-341">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="2dbbb-341">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="2dbbb-342">Colonne Identity nel database di destinazione</span><span class="sxs-lookup"><span data-stu-id="2dbbb-342">Identity columns in the target database</span></span>
<span data-ttu-id="2dbbb-343">Questa sezione fornisce un esempio per la copia di dati da una tabella di origine senza una colonna identity in una tabella di destinazione con una colonna identity.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-343">This section provides an example that copies data from a source table with no identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="2dbbb-344">**Tabella di origine:**</span><span class="sxs-lookup"><span data-stu-id="2dbbb-344">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="2dbbb-345">**Tabella di destinazione:**</span><span class="sxs-lookup"><span data-stu-id="2dbbb-345">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="2dbbb-346">Si noti che la tabella di destinazione contiene una colonna identity.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-346">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="2dbbb-347">**Definizione JSON del set di dati di origine**</span><span class="sxs-lookup"><span data-stu-id="2dbbb-347">**Source dataset JSON definition**</span></span>

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="2dbbb-348">**Definizione JSON del set di dati di destinazione**</span><span class="sxs-lookup"><span data-stu-id="2dbbb-348">**Destination dataset JSON definition**</span></span>

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

<span data-ttu-id="2dbbb-349">Si noti che la tabella di origine e la tabella di destinazione hanno schemi diversi (la destinazione include una colonna aggiuntiva identity).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-349">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="2dbbb-350">In questo scenario è necessario specificare la proprietà **structure** nella definizione del set di dati di destinazione che non include la colonna identity.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-350">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="2dbbb-351">Chiamare una stored procedure da un sink SQL</span><span class="sxs-lookup"><span data-stu-id="2dbbb-351">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="2dbbb-352">Per un esempio di come chiamare una stored procedure da un sink SQL in un'attività di copia di una pipeline, vedere l'articolo su come [richiamare una stored procedure per il sink SQL nell'attività di copia](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-352">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="2dbbb-353">Mapping dei tipi per SQL Server</span><span class="sxs-lookup"><span data-stu-id="2dbbb-353">Type mapping for SQL server</span></span>
<span data-ttu-id="2dbbb-354">Come accennato nell'articolo [Attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni di tipi automatiche da tipi di origine a tipi di sink con l'approccio seguente in 2 passaggi:</span><span class="sxs-lookup"><span data-stu-id="2dbbb-354">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="2dbbb-355">Conversione dai tipi di origine nativi al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="2dbbb-355">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="2dbbb-356">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="2dbbb-356">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="2dbbb-357">Quando si spostano dati da e verso SQL Server, vengono usati i mapping seguenti dal tipo SQL al tipo .NET e viceversa.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-357">When moving data to & from SQL server, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="2dbbb-358">Il mapping è uguale al mapping del tipo di dati di SQL Server per ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-358">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="2dbbb-359">Tipo di motore di database di SQL Server</span><span class="sxs-lookup"><span data-stu-id="2dbbb-359">SQL Server Database Engine type</span></span> | <span data-ttu-id="2dbbb-360">Tipo di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="2dbbb-360">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="2dbbb-361">bigint</span><span class="sxs-lookup"><span data-stu-id="2dbbb-361">bigint</span></span> |<span data-ttu-id="2dbbb-362">Int64</span><span class="sxs-lookup"><span data-stu-id="2dbbb-362">Int64</span></span> |
| <span data-ttu-id="2dbbb-363">binary</span><span class="sxs-lookup"><span data-stu-id="2dbbb-363">binary</span></span> |<span data-ttu-id="2dbbb-364">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2dbbb-364">Byte[]</span></span> |
| <span data-ttu-id="2dbbb-365">bit</span><span class="sxs-lookup"><span data-stu-id="2dbbb-365">bit</span></span> |<span data-ttu-id="2dbbb-366">Boolean</span><span class="sxs-lookup"><span data-stu-id="2dbbb-366">Boolean</span></span> |
| <span data-ttu-id="2dbbb-367">char</span><span class="sxs-lookup"><span data-stu-id="2dbbb-367">char</span></span> |<span data-ttu-id="2dbbb-368">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="2dbbb-368">String, Char[]</span></span> |
| <span data-ttu-id="2dbbb-369">date</span><span class="sxs-lookup"><span data-stu-id="2dbbb-369">date</span></span> |<span data-ttu-id="2dbbb-370">DateTime</span><span class="sxs-lookup"><span data-stu-id="2dbbb-370">DateTime</span></span> |
| <span data-ttu-id="2dbbb-371">DateTime</span><span class="sxs-lookup"><span data-stu-id="2dbbb-371">Datetime</span></span> |<span data-ttu-id="2dbbb-372">DateTime</span><span class="sxs-lookup"><span data-stu-id="2dbbb-372">DateTime</span></span> |
| <span data-ttu-id="2dbbb-373">datetime2</span><span class="sxs-lookup"><span data-stu-id="2dbbb-373">datetime2</span></span> |<span data-ttu-id="2dbbb-374">DateTime</span><span class="sxs-lookup"><span data-stu-id="2dbbb-374">DateTime</span></span> |
| <span data-ttu-id="2dbbb-375">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="2dbbb-375">Datetimeoffset</span></span> |<span data-ttu-id="2dbbb-376">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="2dbbb-376">DateTimeOffset</span></span> |
| <span data-ttu-id="2dbbb-377">Decimale</span><span class="sxs-lookup"><span data-stu-id="2dbbb-377">Decimal</span></span> |<span data-ttu-id="2dbbb-378">Decimale</span><span class="sxs-lookup"><span data-stu-id="2dbbb-378">Decimal</span></span> |
| <span data-ttu-id="2dbbb-379">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="2dbbb-379">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="2dbbb-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2dbbb-380">Byte[]</span></span> |
| <span data-ttu-id="2dbbb-381">Float</span><span class="sxs-lookup"><span data-stu-id="2dbbb-381">Float</span></span> |<span data-ttu-id="2dbbb-382">Double</span><span class="sxs-lookup"><span data-stu-id="2dbbb-382">Double</span></span> |
| <span data-ttu-id="2dbbb-383">immagine</span><span class="sxs-lookup"><span data-stu-id="2dbbb-383">image</span></span> |<span data-ttu-id="2dbbb-384">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2dbbb-384">Byte[]</span></span> |
| <span data-ttu-id="2dbbb-385">int</span><span class="sxs-lookup"><span data-stu-id="2dbbb-385">int</span></span> |<span data-ttu-id="2dbbb-386">Int32</span><span class="sxs-lookup"><span data-stu-id="2dbbb-386">Int32</span></span> |
| <span data-ttu-id="2dbbb-387">money</span><span class="sxs-lookup"><span data-stu-id="2dbbb-387">money</span></span> |<span data-ttu-id="2dbbb-388">Decimale</span><span class="sxs-lookup"><span data-stu-id="2dbbb-388">Decimal</span></span> |
| <span data-ttu-id="2dbbb-389">nchar</span><span class="sxs-lookup"><span data-stu-id="2dbbb-389">nchar</span></span> |<span data-ttu-id="2dbbb-390">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="2dbbb-390">String, Char[]</span></span> |
| <span data-ttu-id="2dbbb-391">ntext</span><span class="sxs-lookup"><span data-stu-id="2dbbb-391">ntext</span></span> |<span data-ttu-id="2dbbb-392">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="2dbbb-392">String, Char[]</span></span> |
| <span data-ttu-id="2dbbb-393">numeric</span><span class="sxs-lookup"><span data-stu-id="2dbbb-393">numeric</span></span> |<span data-ttu-id="2dbbb-394">Decimale</span><span class="sxs-lookup"><span data-stu-id="2dbbb-394">Decimal</span></span> |
| <span data-ttu-id="2dbbb-395">nvarchar</span><span class="sxs-lookup"><span data-stu-id="2dbbb-395">nvarchar</span></span> |<span data-ttu-id="2dbbb-396">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="2dbbb-396">String, Char[]</span></span> |
| <span data-ttu-id="2dbbb-397">real</span><span class="sxs-lookup"><span data-stu-id="2dbbb-397">real</span></span> |<span data-ttu-id="2dbbb-398">Single</span><span class="sxs-lookup"><span data-stu-id="2dbbb-398">Single</span></span> |
| <span data-ttu-id="2dbbb-399">rowversion</span><span class="sxs-lookup"><span data-stu-id="2dbbb-399">rowversion</span></span> |<span data-ttu-id="2dbbb-400">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2dbbb-400">Byte[]</span></span> |
| <span data-ttu-id="2dbbb-401">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="2dbbb-401">smalldatetime</span></span> |<span data-ttu-id="2dbbb-402">DateTime</span><span class="sxs-lookup"><span data-stu-id="2dbbb-402">DateTime</span></span> |
| <span data-ttu-id="2dbbb-403">smallint</span><span class="sxs-lookup"><span data-stu-id="2dbbb-403">smallint</span></span> |<span data-ttu-id="2dbbb-404">Int16</span><span class="sxs-lookup"><span data-stu-id="2dbbb-404">Int16</span></span> |
| <span data-ttu-id="2dbbb-405">smallmoney</span><span class="sxs-lookup"><span data-stu-id="2dbbb-405">smallmoney</span></span> |<span data-ttu-id="2dbbb-406">Decimale</span><span class="sxs-lookup"><span data-stu-id="2dbbb-406">Decimal</span></span> |
| <span data-ttu-id="2dbbb-407">sql_variant</span><span class="sxs-lookup"><span data-stu-id="2dbbb-407">sql_variant</span></span> |<span data-ttu-id="2dbbb-408">Object *</span><span class="sxs-lookup"><span data-stu-id="2dbbb-408">Object *</span></span> |
| <span data-ttu-id="2dbbb-409">text</span><span class="sxs-lookup"><span data-stu-id="2dbbb-409">text</span></span> |<span data-ttu-id="2dbbb-410">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="2dbbb-410">String, Char[]</span></span> |
| <span data-ttu-id="2dbbb-411">time</span><span class="sxs-lookup"><span data-stu-id="2dbbb-411">time</span></span> |<span data-ttu-id="2dbbb-412">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="2dbbb-412">TimeSpan</span></span> |
| <span data-ttu-id="2dbbb-413">timestamp</span><span class="sxs-lookup"><span data-stu-id="2dbbb-413">timestamp</span></span> |<span data-ttu-id="2dbbb-414">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2dbbb-414">Byte[]</span></span> |
| <span data-ttu-id="2dbbb-415">tinyint</span><span class="sxs-lookup"><span data-stu-id="2dbbb-415">tinyint</span></span> |<span data-ttu-id="2dbbb-416">Byte</span><span class="sxs-lookup"><span data-stu-id="2dbbb-416">Byte</span></span> |
| <span data-ttu-id="2dbbb-417">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="2dbbb-417">uniqueidentifier</span></span> |<span data-ttu-id="2dbbb-418">Guid</span><span class="sxs-lookup"><span data-stu-id="2dbbb-418">Guid</span></span> |
| <span data-ttu-id="2dbbb-419">varbinary</span><span class="sxs-lookup"><span data-stu-id="2dbbb-419">varbinary</span></span> |<span data-ttu-id="2dbbb-420">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2dbbb-420">Byte[]</span></span> |
| <span data-ttu-id="2dbbb-421">varchar</span><span class="sxs-lookup"><span data-stu-id="2dbbb-421">varchar</span></span> |<span data-ttu-id="2dbbb-422">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="2dbbb-422">String, Char[]</span></span> |
| <span data-ttu-id="2dbbb-423">xml</span><span class="sxs-lookup"><span data-stu-id="2dbbb-423">xml</span></span> |<span data-ttu-id="2dbbb-424">xml</span><span class="sxs-lookup"><span data-stu-id="2dbbb-424">Xml</span></span> |

## <a name="mapping-source-to-sink-columns"></a><span data-ttu-id="2dbbb-425">Eseguire il mapping delle colonne dell'origine alle colonne del sink</span><span class="sxs-lookup"><span data-stu-id="2dbbb-425">Mapping source to sink columns</span></span>
<span data-ttu-id="2dbbb-426">Per eseguire il mapping dal set di dati di origine alle colonne del set di dati sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-426">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="2dbbb-427">Copia ripetibile</span><span class="sxs-lookup"><span data-stu-id="2dbbb-427">Repeatable copy</span></span>
<span data-ttu-id="2dbbb-428">Quando si copiano dati in un database SQL Server, per impostazione predefinita l'attività di copia accoda i dati alla tabella di sink.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-428">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="2dbbb-429">Per eseguire invece un UPSERT, vedere l'articolo [Scrittura ripetibile in SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-429">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="2dbbb-430">Quando si copiano dati da archivi dati relazionali, è necessario tenere presente la ripetibilità per evitare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-430">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="2dbbb-431">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-431">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="2dbbb-432">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-432">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="2dbbb-433">Quando una sezione viene rieseguita in uno dei due modi, è necessario assicurarsi che non vengano letti gli stessi dati, indipendentemente da quante volte viene eseguita la sezione.</span><span class="sxs-lookup"><span data-stu-id="2dbbb-433">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="2dbbb-434">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-434">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2dbbb-435">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="2dbbb-435">Performance and Tuning</span></span>
<span data-ttu-id="2dbbb-436">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="2dbbb-436">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
