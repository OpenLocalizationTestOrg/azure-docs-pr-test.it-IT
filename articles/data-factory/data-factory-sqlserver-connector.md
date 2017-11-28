---
title: aaaMove tooand di dati da SQL Server | Documenti Microsoft
description: "Informazioni su come dati toomove a/da SQL Server database che è locale o in una macchina virtuale di Azure usando Azure Data Factory."
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
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="6f76a-103">Spostare dati tooand da SQL Server locale o in IaaS (VM di Azure) usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6f76a-103">Move data tooand from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="6f76a-104">Questo articolo spiega come toouse hello attività di copia nei dati di Azure Data Factory toomove a/da un database di SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="6f76a-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="6f76a-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="6f76a-106">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="6f76a-106">Supported scenarios</span></span>
<span data-ttu-id="6f76a-107">È possibile copiare dati **da un database di SQL Server** toohello archivi dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f76a-107">You can copy data **from a SQL Server database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="6f76a-108">È possibile copiare dati da archivi dati seguenti hello **database di SQL Server tooa**:</span><span class="sxs-lookup"><span data-stu-id="6f76a-108">You can copy data from hello following data stores **tooa SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="6f76a-109">Versioni di SQL Server supportate</span><span class="sxs-lookup"><span data-stu-id="6f76a-109">Supported SQL Server versions</span></span>
<span data-ttu-id="6f76a-110">Copia di dati da questo supporto di connettore SQL Server / toohello seguenti versioni di istanza ospitata in locale o in Azure IaaS tramite l'autenticazione di Windows e autenticazione di SQL Server: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="6f76a-110">This SQL Server connector support copying data from/toohello following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="6f76a-111">Abilitazione della connettività</span><span class="sxs-lookup"><span data-stu-id="6f76a-111">Enabling connectivity</span></span>
<span data-ttu-id="6f76a-112">concetti di Hello e i passaggi necessari per la connessione con SQL Server ospitato in locale o in Azure IaaS (Infrastructure-as-a-Service) VM sono hello stesso.</span><span class="sxs-lookup"><span data-stu-id="6f76a-112">hello concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are hello same.</span></span> <span data-ttu-id="6f76a-113">In entrambi i casi, è necessario toouse Gateway di gestione dati per la connettività.</span><span class="sxs-lookup"><span data-stu-id="6f76a-113">In both cases, you need toouse Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="6f76a-114">Vedere [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn articolo sul Gateway di gestione dati e istruzioni dettagliate su come configurare il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="6f76a-115">L'impostazione di un'istanza del gateway è un prerequisito per la connessione con SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6f76a-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="6f76a-116">Sebbene sia possibile installare gateway su hello stesso locali istanza macchina o di cloud della macchina virtuale come hello di SQL Server per ottenere prestazioni migliori, è consigliabile installarli in computer separati.</span><span class="sxs-lookup"><span data-stu-id="6f76a-116">While you can install gateway on hello same on-premises machine or cloud VM instance as hello SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="6f76a-117">Con gateway hello e SQL Server in computer separati riduce la contesa di risorse.</span><span class="sxs-lookup"><span data-stu-id="6f76a-117">Having hello gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6f76a-118">introduttiva</span><span class="sxs-lookup"><span data-stu-id="6f76a-118">Getting started</span></span>
<span data-ttu-id="6f76a-119">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un SQL Server locale usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="6f76a-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="6f76a-120">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="6f76a-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="6f76a-121">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="6f76a-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="6f76a-122">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="6f76a-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6f76a-123">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="6f76a-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="6f76a-124">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f76a-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="6f76a-125">Creare una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="6f76a-125">Create a **data factory**.</span></span> <span data-ttu-id="6f76a-126">Una data factory può contenere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="6f76a-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="6f76a-127">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="6f76a-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="6f76a-128">Ad esempio, se si copiano dati da un tooan di database di SQL Server archiviazione blob di Azure, è creare due servizi collegati toolink il database di SQL Server e l'archiviazione di Azure account tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="6f76a-128">For example, if you are copying data from a SQL Server database tooan Azure blob storage, you create two linked services toolink your SQL Server database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="6f76a-129">Per le proprietà di servizio collegato che sono specifici tooSQL database del Server, vedere [servizio proprietà collegate](#linked-service-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="6f76a-129">For linked service properties that are specific tooSQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="6f76a-130">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="6f76a-131">Nell'esempio hello indicato nell'ultimo passaggio hello, crei una tabella SQL hello toospecify set di dati nel database di SQL Server che contiene i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-131">In hello example mentioned in hello last step, you create a dataset toospecify hello SQL table in your SQL Server database that contains hello input data.</span></span> <span data-ttu-id="6f76a-132">E, per creare un altro set di dati toospecify hello blob contenitore e cartella hello contenente hello dati copiati dal hello database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6f76a-132">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello SQL Server database.</span></span> <span data-ttu-id="6f76a-133">Per le proprietà di set di dati che sono specifici tooSQL database del Server, vedere [proprietà set di dati](#dataset-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="6f76a-133">For dataset properties that are specific tooSQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="6f76a-134">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="6f76a-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="6f76a-135">Nell'esempio hello indicato in precedenza, si usa SqlSource come un'origine e BlobSink come sink per attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-135">In hello example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="6f76a-136">Analogamente, se si sta copiando l'archiviazione Blob di Azure tooSQL Database del Server, utilizzare BlobSource e SqlSink nell'attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-136">Similarly, if you are copying from Azure Blob Storage tooSQL Server Database, you use BlobSource and SqlSink in hello copy activity.</span></span> <span data-ttu-id="6f76a-137">Per le proprietà di attività di copia che sono specifici tooSQL Database del Server, vedere [copiare le proprietà dell'attività](#copy-activity-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="6f76a-137">For copy activity properties that are specific tooSQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="6f76a-138">Per informazioni dettagliate su come toouse un archivio dati come origine o un sink, fare clic sul collegamento di hello nella sezione precedente di hello per l'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="6f76a-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="6f76a-139">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="6f76a-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="6f76a-140">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6f76a-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="6f76a-141">Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati i dati in o da un database di SQL Server locale, vedere [esempi JSON](#json-examples-for-copying-data-from-and-to-sql-server) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="6f76a-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="6f76a-142">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooSQL Server:</span><span class="sxs-lookup"><span data-stu-id="6f76a-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="6f76a-143">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="6f76a-143">Linked service properties</span></span>
<span data-ttu-id="6f76a-144">Creare un servizio collegato di tipo **OnPremisesSqlServer** toolink una data factory tooa di on-premise SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="6f76a-144">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="6f76a-145">Hello nella tabella seguente fornisce una descrizione del servizio collegato SQL Server locale tooon specifici elementi JSON.</span><span class="sxs-lookup"><span data-stu-id="6f76a-145">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="6f76a-146">Hello nella tabella seguente fornisce una descrizione JSON elementi specifici tooSQL servizio del Server collegato.</span><span class="sxs-lookup"><span data-stu-id="6f76a-146">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="6f76a-147">Proprietà</span><span class="sxs-lookup"><span data-stu-id="6f76a-147">Property</span></span> | <span data-ttu-id="6f76a-148">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6f76a-148">Description</span></span> | <span data-ttu-id="6f76a-149">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="6f76a-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6f76a-150">type</span><span class="sxs-lookup"><span data-stu-id="6f76a-150">type</span></span> |<span data-ttu-id="6f76a-151">proprietà di tipo Hello deve essere impostata su: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="6f76a-151">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="6f76a-152">Sì</span><span class="sxs-lookup"><span data-stu-id="6f76a-152">Yes</span></span> |
| <span data-ttu-id="6f76a-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="6f76a-153">connectionString</span></span> |<span data-ttu-id="6f76a-154">Specificare le informazioni connectionString necessarie tooconnect database di SQL Server on-premise toohello utilizzando l'autenticazione di SQL Server o l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="6f76a-154">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="6f76a-155">Sì</span><span class="sxs-lookup"><span data-stu-id="6f76a-155">Yes</span></span> |
| <span data-ttu-id="6f76a-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6f76a-156">gatewayName</span></span> |<span data-ttu-id="6f76a-157">Nome del gateway hello hello servizio Data Factory deve utilizzare i database di SQL Server on-premise toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="6f76a-157">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="6f76a-158">Sì</span><span class="sxs-lookup"><span data-stu-id="6f76a-158">Yes</span></span> |
| <span data-ttu-id="6f76a-159">username</span><span class="sxs-lookup"><span data-stu-id="6f76a-159">username</span></span> |<span data-ttu-id="6f76a-160">Specificare il nome utente se si usa l'autenticazione Windows.</span><span class="sxs-lookup"><span data-stu-id="6f76a-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="6f76a-161">Esempio: **nomedominio\\nomeutente**.</span><span class="sxs-lookup"><span data-stu-id="6f76a-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="6f76a-162">No</span><span class="sxs-lookup"><span data-stu-id="6f76a-162">No</span></span> |
| <span data-ttu-id="6f76a-163">password</span><span class="sxs-lookup"><span data-stu-id="6f76a-163">password</span></span> |<span data-ttu-id="6f76a-164">Specificare la password per account utente di hello specificato per il nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="6f76a-165">No</span><span class="sxs-lookup"><span data-stu-id="6f76a-165">No</span></span> |

<span data-ttu-id="6f76a-166">È possibile crittografare le credenziali utilizzando hello **New AzureRmDataFactoryEncryptValue** cmdlet e utilizzarli nella stringa di connessione hello, come illustrato nell'esempio seguente hello (**EncryptedCredential** proprietà):</span><span class="sxs-lookup"><span data-stu-id="6f76a-166">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="6f76a-167">Esempi</span><span class="sxs-lookup"><span data-stu-id="6f76a-167">Samples</span></span>
<span data-ttu-id="6f76a-168">**JSON per l'uso dell'Autenticazione di SQL**</span><span class="sxs-lookup"><span data-stu-id="6f76a-168">**JSON for using SQL Authentication**</span></span>

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
<span data-ttu-id="6f76a-169">**JSON per l'uso dell'Autenticazione Windows**</span><span class="sxs-lookup"><span data-stu-id="6f76a-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="6f76a-170">Gateway di gestione dati rappresenterà hello specificato database di SQL Server on-premise toohello tooconnect account utente.</span><span class="sxs-lookup"><span data-stu-id="6f76a-170">Data Management Gateway will impersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> 

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

## <a name="dataset-properties"></a><span data-ttu-id="6f76a-171">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="6f76a-171">Dataset properties</span></span>
<span data-ttu-id="6f76a-172">Negli esempi di hello è stato utilizzato un set di dati di tipo **SqlServerTable** toorepresent una tabella in un database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6f76a-172">In hello samples, you have used a dataset of type **SqlServerTable** toorepresent a table in a SQL Server database.</span></span>  

<span data-ttu-id="6f76a-173">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="6f76a-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6f76a-174">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati (SQL Server, BLOB di Azure, tabelle di Azure e così via).</span><span class="sxs-lookup"><span data-stu-id="6f76a-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6f76a-175">sezione typeProperties Hello è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-175">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="6f76a-176">Hello **typeProperties** sezione per hello set di dati di tipo **SqlServerTable** è hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f76a-176">hello **typeProperties** section for hello dataset of type **SqlServerTable** has hello following properties:</span></span>

| <span data-ttu-id="6f76a-177">Proprietà</span><span class="sxs-lookup"><span data-stu-id="6f76a-177">Property</span></span> | <span data-ttu-id="6f76a-178">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6f76a-178">Description</span></span> | <span data-ttu-id="6f76a-179">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="6f76a-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6f76a-180">tableName</span><span class="sxs-lookup"><span data-stu-id="6f76a-180">tableName</span></span> |<span data-ttu-id="6f76a-181">Nome della tabella hello o della vista nell'istanza di Database di SQL Server hello che il servizio collegato fa riferimento a.</span><span class="sxs-lookup"><span data-stu-id="6f76a-181">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="6f76a-182">Sì</span><span class="sxs-lookup"><span data-stu-id="6f76a-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="6f76a-183">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="6f76a-183">Copy activity properties</span></span>
<span data-ttu-id="6f76a-184">Se si stanno spostando i dati da un database di SQL Server, impostare il tipo di origine hello nell'attività di copia hello troppo**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="6f76a-184">If you are moving data from a SQL Server database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="6f76a-185">Analogamente, se si stanno spostando i database di SQL Server tooa di dati, impostare il tipo di sink hello nell'attività di copia hello troppo**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="6f76a-185">Similarly, if you are moving data tooa SQL Server database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="6f76a-186">Questa sezione presenta un elenco delle proprietà supportate da SqlSource e SqlSink.</span><span class="sxs-lookup"><span data-stu-id="6f76a-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="6f76a-187">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="6f76a-187">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6f76a-188">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="6f76a-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="6f76a-189">Hello attività di copia accetta un solo input e produce un solo output.</span><span class="sxs-lookup"><span data-stu-id="6f76a-189">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="6f76a-190">Mentre le proprietà disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="6f76a-190">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="6f76a-191">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="6f76a-191">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="6f76a-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="6f76a-192">SqlSource</span></span>
<span data-ttu-id="6f76a-193">Quando l'origine in un'attività di copia è di tipo **SqlSource**, hello le proprietà seguenti sono disponibile in **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="6f76a-193">When source in a copy activity is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="6f76a-194">Proprietà</span><span class="sxs-lookup"><span data-stu-id="6f76a-194">Property</span></span> | <span data-ttu-id="6f76a-195">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6f76a-195">Description</span></span> | <span data-ttu-id="6f76a-196">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="6f76a-196">Allowed values</span></span> | <span data-ttu-id="6f76a-197">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="6f76a-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6f76a-198">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="6f76a-198">sqlReaderQuery</span></span> |<span data-ttu-id="6f76a-199">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="6f76a-199">Use hello custom query tooread data.</span></span> |<span data-ttu-id="6f76a-200">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="6f76a-200">SQL query string.</span></span> <span data-ttu-id="6f76a-201">Ad esempio: selezionare * da MyTable.</span><span class="sxs-lookup"><span data-stu-id="6f76a-201">For example: select * from MyTable.</span></span> <span data-ttu-id="6f76a-202">Può fare riferimento a più tabelle dal database hello hello di un set di dati dell'input a cui fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="6f76a-202">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="6f76a-203">Se non specificato, hello istruzione SQL eseguita: select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="6f76a-203">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="6f76a-204">No</span><span class="sxs-lookup"><span data-stu-id="6f76a-204">No</span></span> |
| <span data-ttu-id="6f76a-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="6f76a-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="6f76a-206">Nome di hello stored procedure che legge i dati dalla tabella di origine hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-206">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="6f76a-207">Nome di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="6f76a-207">Name of hello stored procedure.</span></span> <span data-ttu-id="6f76a-208">ultima istruzione SQL di Hello deve essere un'istruzione SELECT nella procedura hello archiviato.</span><span class="sxs-lookup"><span data-stu-id="6f76a-208">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="6f76a-209">No</span><span class="sxs-lookup"><span data-stu-id="6f76a-209">No</span></span> |
| <span data-ttu-id="6f76a-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="6f76a-210">storedProcedureParameters</span></span> |<span data-ttu-id="6f76a-211">I parametri per hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="6f76a-211">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="6f76a-212">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="6f76a-212">Name/value pairs.</span></span> <span data-ttu-id="6f76a-213">Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="6f76a-213">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="6f76a-214">No</span><span class="sxs-lookup"><span data-stu-id="6f76a-214">No</span></span> |

<span data-ttu-id="6f76a-215">Se hello **sqlReaderQuery** specificato per hello SqlSource, hello attività di copia viene eseguita questa query hello Database di SQL Server tooget hello dati.</span><span class="sxs-lookup"><span data-stu-id="6f76a-215">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="6f76a-216">In alternativa, è possibile specificare una stored procedure specificando hello **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello stored procedure accetta parametri).</span><span class="sxs-lookup"><span data-stu-id="6f76a-216">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="6f76a-217">Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne di hello definite nella sezione di struttura hello sono utilizzati toobuild toorun una query select su hello Database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6f76a-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="6f76a-218">Se non dispone di definizione del set di dati hello struttura hello, vengono selezionate tutte le colonne dalla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-218">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="6f76a-219">Quando si utilizza **sqlReaderStoredProcedureName**, è comunque necessario toospecify un valore per hello **tableName** proprietà hello set di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="6f76a-219">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="6f76a-220">Non sono disponibili convalide eseguite su questa tabella.</span><span class="sxs-lookup"><span data-stu-id="6f76a-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="6f76a-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="6f76a-221">SqlSink</span></span>
<span data-ttu-id="6f76a-222">**SqlSink** supporta hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="6f76a-222">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="6f76a-223">Proprietà</span><span class="sxs-lookup"><span data-stu-id="6f76a-223">Property</span></span> | <span data-ttu-id="6f76a-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6f76a-224">Description</span></span> | <span data-ttu-id="6f76a-225">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="6f76a-225">Allowed values</span></span> | <span data-ttu-id="6f76a-226">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="6f76a-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6f76a-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="6f76a-227">writeBatchTimeout</span></span> |<span data-ttu-id="6f76a-228">Tempo di attesa per hello batch insert operazione toocomplete prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="6f76a-228">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="6f76a-229">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="6f76a-229">timespan</span></span><br/><br/> <span data-ttu-id="6f76a-230">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="6f76a-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="6f76a-231">No</span><span class="sxs-lookup"><span data-stu-id="6f76a-231">No</span></span> |
| <span data-ttu-id="6f76a-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="6f76a-232">writeBatchSize</span></span> |<span data-ttu-id="6f76a-233">Inserisce dati in una tabella SQL hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-233">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="6f76a-234">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="6f76a-234">Integer (number of rows)</span></span> |<span data-ttu-id="6f76a-235">No (valore predefinito: 10000)</span><span class="sxs-lookup"><span data-stu-id="6f76a-235">No (default: 10000)</span></span> |
| <span data-ttu-id="6f76a-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="6f76a-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="6f76a-237">Specificare query per l'attività di copia tooexecute modo che la pulitura dei dati di una sezione specifica.</span><span class="sxs-lookup"><span data-stu-id="6f76a-237">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="6f76a-238">Per altre informazioni, vedere la sezione [Copia ripetibile](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="6f76a-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="6f76a-239">Istruzione di query.</span><span class="sxs-lookup"><span data-stu-id="6f76a-239">A query statement.</span></span> |<span data-ttu-id="6f76a-240">No</span><span class="sxs-lookup"><span data-stu-id="6f76a-240">No</span></span> |
| <span data-ttu-id="6f76a-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="6f76a-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="6f76a-242">Specificare il nome di colonna per attività di copia toofill con identificatore di sezione generati automaticamente, che è usato tooclean dei dati di una sezione specifica quando eseguire di nuovo.</span><span class="sxs-lookup"><span data-stu-id="6f76a-242">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="6f76a-243">Per altre informazioni, vedere la sezione [Copia ripetibile](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="6f76a-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="6f76a-244">Nome di colonna di una colonna con tipo di dati binario (32).</span><span class="sxs-lookup"><span data-stu-id="6f76a-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="6f76a-245">No</span><span class="sxs-lookup"><span data-stu-id="6f76a-245">No</span></span> |
| <span data-ttu-id="6f76a-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="6f76a-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="6f76a-247">Nome della hello stored procedure che upserts (aggiornamenti/inserimenti) i dati nella tabella di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-247">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="6f76a-248">Nome di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="6f76a-248">Name of hello stored procedure.</span></span> |<span data-ttu-id="6f76a-249">No</span><span class="sxs-lookup"><span data-stu-id="6f76a-249">No</span></span> |
| <span data-ttu-id="6f76a-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="6f76a-250">storedProcedureParameters</span></span> |<span data-ttu-id="6f76a-251">I parametri per hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="6f76a-251">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="6f76a-252">Coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="6f76a-252">Name/value pairs.</span></span> <span data-ttu-id="6f76a-253">Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="6f76a-253">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="6f76a-254">No</span><span class="sxs-lookup"><span data-stu-id="6f76a-254">No</span></span> |
| <span data-ttu-id="6f76a-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="6f76a-255">sqlWriterTableType</span></span> |<span data-ttu-id="6f76a-256">Specificare toobe nome tipo di tabella utilizzati in hello stored procedure.</span><span class="sxs-lookup"><span data-stu-id="6f76a-256">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="6f76a-257">Attività di copia rende disponibili in una tabella temporanea con questo tipo di tabella dati di hello viene spostati.</span><span class="sxs-lookup"><span data-stu-id="6f76a-257">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="6f76a-258">Codice della stored procedure può unire dati hello copiati con i dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="6f76a-258">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="6f76a-259">Nome del tipo di tabella.</span><span class="sxs-lookup"><span data-stu-id="6f76a-259">A table type name.</span></span> |<span data-ttu-id="6f76a-260">No</span><span class="sxs-lookup"><span data-stu-id="6f76a-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a><span data-ttu-id="6f76a-261">Esempi JSON per la copia dei dati da e tooSQL Server</span><span class="sxs-lookup"><span data-stu-id="6f76a-261">JSON examples for copying data from and tooSQL Server</span></span>
<span data-ttu-id="6f76a-262">Negli esempi seguenti Hello forniscono definizioni JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6f76a-262">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6f76a-263">Hello seguente mostra esempi come toocopy tooand di dati da SQL Server e archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="6f76a-263">hello following samples show how toocopy data tooand from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="6f76a-264">Tuttavia, i dati possono essere copiati **direttamente** da una qualsiasi delle origini tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6f76a-264">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a><span data-ttu-id="6f76a-265">Esempio: Copiare i dati da SQL Server tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="6f76a-265">Example: Copy data from SQL Server tooAzure Blob</span></span>
<span data-ttu-id="6f76a-266">Hello nel seguente esempio viene illustrato:</span><span class="sxs-lookup"><span data-stu-id="6f76a-266">hello following sample shows:</span></span>

1. <span data-ttu-id="6f76a-267">Un servizio collegato di tipo [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6f76a-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="6f76a-268">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6f76a-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6f76a-269">Un [set di dati](data-factory-create-datasets.md) di tipo [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6f76a-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="6f76a-270">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6f76a-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6f76a-271">Hello [pipeline](data-factory-create-pipelines.md) con attività di copia che utilizza [SqlSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6f76a-271">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="6f76a-272">esempio Hello copia dati delle serie temporali da un tooan tabella di SQL Server blob di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="6f76a-272">hello sample copies time-series data from a SQL Server table tooan Azure blob every hour.</span></span> <span data-ttu-id="6f76a-273">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-273">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="6f76a-274">Come primo passaggio, configurare il gateway di gestione dati hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-274">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="6f76a-275">istruzioni di Hello presenti hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="6f76a-275">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="6f76a-276">**Servizio collegato di SQL Server**</span><span class="sxs-lookup"><span data-stu-id="6f76a-276">**SQL Server linked service**</span></span>
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
<span data-ttu-id="6f76a-277">**Servizio collegato di archiviazione BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="6f76a-277">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="6f76a-278">**Set di dati input di SQL Server**</span><span class="sxs-lookup"><span data-stu-id="6f76a-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="6f76a-279">esempio Hello presuppone di aver creato una tabella "MyTable" in SQL Server e contiene una colonna denominata "timestampcolumn" per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="6f76a-279">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="6f76a-280">È possibile eseguire query su più tabelle all'interno di hello stesso database con un singolo set di dati, ma una singola tabella deve essere utilizzato per typeProperty tableName hello del dataset.</span><span class="sxs-lookup"><span data-stu-id="6f76a-280">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="6f76a-281">L'impostazione "external": "true" informa il servizio Data Factory hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-281">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="6f76a-282">**Set di dati di output del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="6f76a-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="6f76a-283">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="6f76a-283">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6f76a-284">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="6f76a-284">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6f76a-285">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-285">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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
<span data-ttu-id="6f76a-286">**Pipeline con attività di copia**</span><span class="sxs-lookup"><span data-stu-id="6f76a-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="6f76a-287">pipeline di Hello contiene un'attività di copia che è configurato toouse questi set di dati di input e output e toorun pianificato ogni ora.</span><span class="sxs-lookup"><span data-stu-id="6f76a-287">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="6f76a-288">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**SqlSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6f76a-288">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="6f76a-289">query SQL Hello specificata per hello **SqlReaderQuery** proprietà consente di selezionare dati hello hello oltre toocopy ora.</span><span class="sxs-lookup"><span data-stu-id="6f76a-289">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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
<span data-ttu-id="6f76a-290">In questo esempio, **sqlReaderQuery** specificato per hello SqlSource.</span><span class="sxs-lookup"><span data-stu-id="6f76a-290">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="6f76a-291">Attività di copia Hello consente di eseguire questa query hello dati hello tooget origine di Database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6f76a-291">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="6f76a-292">In alternativa, è possibile specificare una stored procedure specificando hello **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello stored procedure accetta parametri).</span><span class="sxs-lookup"><span data-stu-id="6f76a-292">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="6f76a-293">Hello sqlReaderQuery può fare riferimento a più tabelle all'interno del database hello hello di un set di dati dell'input a cui fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="6f76a-293">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="6f76a-294">Non è limitato tooonly hello tabella impostata come hello typeProperty tableName del set di dati.</span><span class="sxs-lookup"><span data-stu-id="6f76a-294">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="6f76a-295">Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne di hello definite nella sezione di struttura hello sono utilizzati toobuild toorun una query select su hello Database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6f76a-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="6f76a-296">Se non dispone di definizione del set di dati hello struttura hello, vengono selezionate tutte le colonne dalla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-296">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="6f76a-297">Vedere hello [origine Sql](#sqlsource) sezione e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) per elenco hello delle proprietà supportate da SqlSource e BlobSink.</span><span class="sxs-lookup"><span data-stu-id="6f76a-297">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-toosql-server"></a><span data-ttu-id="6f76a-298">Esempio: Copiare i dati da Blob di Azure tooSQL Server</span><span class="sxs-lookup"><span data-stu-id="6f76a-298">Example: Copy data from Azure Blob tooSQL Server</span></span>
<span data-ttu-id="6f76a-299">Hello nel seguente esempio viene illustrato:</span><span class="sxs-lookup"><span data-stu-id="6f76a-299">hello following sample shows:</span></span>

1. <span data-ttu-id="6f76a-300">servizio del tipo di Hello collegato [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6f76a-300">hello linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="6f76a-301">servizio del tipo di Hello collegato [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6f76a-301">hello linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6f76a-302">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6f76a-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="6f76a-303">Un [set di dati](data-factory-create-datasets.md) di output di tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6f76a-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6f76a-304">Hello [pipeline](data-factory-create-pipelines.md) con attività di copia che utilizza [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="6f76a-304">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="6f76a-305">esempio Hello copia dati delle serie temporali da una tabella di SQL Server tooa blob di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="6f76a-305">hello sample copies time-series data from an Azure blob tooa SQL Server table every hour.</span></span> <span data-ttu-id="6f76a-306">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-306">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="6f76a-307">**Servizio collegato di SQL Server**</span><span class="sxs-lookup"><span data-stu-id="6f76a-307">**SQL Server linked service**</span></span>

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
<span data-ttu-id="6f76a-308">**Servizio collegato di archiviazione BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="6f76a-308">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="6f76a-309">**Set di dati di input del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="6f76a-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="6f76a-310">I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="6f76a-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6f76a-311">Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="6f76a-311">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6f76a-312">percorso della cartella Hello utilizza year, month e parte del giorno dell'ora di inizio hello e nome del file utilizza parte ora hello hello ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="6f76a-312">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="6f76a-313">"external": "true" impostazione informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-313">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="6f76a-314">**Set di dati output di SQL Server**</span><span class="sxs-lookup"><span data-stu-id="6f76a-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="6f76a-315">esempio Hello copia tabella tooa dati denominata "MyTable" in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6f76a-315">hello sample copies data tooa table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="6f76a-316">Creare la tabella hello in SQL Server con hello stesso numero di colonne nel modo previsto toocontain di file CSV Blob hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-316">Create hello table in SQL Server with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="6f76a-317">Aggiunta di nuove righe nella tabella toohello ogni ora.</span><span class="sxs-lookup"><span data-stu-id="6f76a-317">New rows are added toohello table every hour.</span></span>

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
<span data-ttu-id="6f76a-318">**Pipeline con attività di copia**</span><span class="sxs-lookup"><span data-stu-id="6f76a-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="6f76a-319">pipeline di Hello contiene un'attività di copia che è configurato toouse questi set di dati di input e output e toorun pianificato ogni ora.</span><span class="sxs-lookup"><span data-stu-id="6f76a-319">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="6f76a-320">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**BlobSource** e **sink** tipo è stato impostato troppo**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="6f76a-320">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="6f76a-321">Risoluzione dei problemi di connessione</span><span class="sxs-lookup"><span data-stu-id="6f76a-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="6f76a-322">Configurare le connessioni remote tooaccept di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6f76a-322">Configure your SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="6f76a-323">Avviare **SQL Server Management Studio**, fare clic con il pulsante destro del mouse su **server** e selezionare **Properties**.</span><span class="sxs-lookup"><span data-stu-id="6f76a-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="6f76a-324">Selezionare **connessioni** dall'elenco di hello e controllo **server toohello di Consenti connessioni remote**.</span><span class="sxs-lookup"><span data-stu-id="6f76a-324">Select **Connections** from hello list and check **Allow remote connections toohello server**.</span></span>

    ![Abilitare le connessioni remote](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="6f76a-326">Vedere [configurare accesso remoto hello opzione di configurazione del Server](https://msdn.microsoft.com/library/ms191464.aspx) per i passaggi dettagliati.</span><span class="sxs-lookup"><span data-stu-id="6f76a-326">See [Configure hello remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="6f76a-327">Avviare **Gestione configurazione SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="6f76a-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="6f76a-328">Espandere **configurazione di rete SQL Server** per hello istanza che si desidera, quindi selezionare **protocolli per MSSQLSERVER**.</span><span class="sxs-lookup"><span data-stu-id="6f76a-328">Expand **SQL Server Network Configuration** for hello instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="6f76a-329">Verrà visualizzato protocolli nel riquadro di destra hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-329">You should see protocols in hello right-pane.</span></span> <span data-ttu-id="6f76a-330">Abilitare il protocollo TCP/IP facendo clic con il pulsante destro del mouse su **TCP/IP** e selezionando **Abilita**.</span><span class="sxs-lookup"><span data-stu-id="6f76a-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![Abilitare TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="6f76a-332">Per informazioni dettagliate e modalità alternative di abilitazione del protocollo TCP/IP, vedere [Abilitare o disabilitare un protocollo di rete del server](https://msdn.microsoft.com/library/ms191294.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f76a-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="6f76a-333">Nella stessa finestra hello fare doppio clic su **TCP/IP** toolaunch **proprietà TCP/IP** finestra.</span><span class="sxs-lookup"><span data-stu-id="6f76a-333">In hello same window, double-click **TCP/IP** toolaunch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="6f76a-334">Passare toohello **gli indirizzi IP** scheda. Scorrere verso il basso toosee **IPAll** sezione.</span><span class="sxs-lookup"><span data-stu-id="6f76a-334">Switch toohello **IP Addresses** tab. Scroll down toosee **IPAll** section.</span></span> <span data-ttu-id="6f76a-335">Annotare hello * * la porta TCP * * (valore predefinito è **1433**).</span><span class="sxs-lookup"><span data-stu-id="6f76a-335">Note down hello **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="6f76a-336">Creare un **regola per il Firewall di Windows hello** hello macchina tooallow il traffico in ingresso tramite questa porta.</span><span class="sxs-lookup"><span data-stu-id="6f76a-336">Create a **rule for hello Windows Firewall** on hello machine tooallow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="6f76a-337">**Verifica connessione**: tooconnect toohello SQL Server utilizzando il nome completo, utilizzare SQL Server Management Studio da un computer diverso.</span><span class="sxs-lookup"><span data-stu-id="6f76a-337">**Verify connection**: tooconnect toohello SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="6f76a-338">Ad esempio: "<machine><domain>.corp<company>.com,1433."</span><span class="sxs-lookup"><span data-stu-id="6f76a-338">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="6f76a-339">Vedere [spostare dati tra origini locali e cloud hello con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="6f76a-339">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="6f76a-340">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="6f76a-340">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="6f76a-341">Colonne Identity nel database di destinazione hello</span><span class="sxs-lookup"><span data-stu-id="6f76a-341">Identity columns in hello target database</span></span>
<span data-ttu-id="6f76a-342">In questa sezione viene fornito un esempio che copia i dati da una tabella di origine con alcuna tabella di destinazione tooa colonna identity con una colonna identity.</span><span class="sxs-lookup"><span data-stu-id="6f76a-342">This section provides an example that copies data from a source table with no identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="6f76a-343">**Tabella di origine:**</span><span class="sxs-lookup"><span data-stu-id="6f76a-343">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="6f76a-344">**Tabella di destinazione:**</span><span class="sxs-lookup"><span data-stu-id="6f76a-344">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="6f76a-345">Si noti che la tabella di destinazione hello include una colonna identity.</span><span class="sxs-lookup"><span data-stu-id="6f76a-345">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="6f76a-346">**Definizione JSON del set di dati di origine**</span><span class="sxs-lookup"><span data-stu-id="6f76a-346">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="6f76a-347">**Definizione JSON del set di dati di destinazione**</span><span class="sxs-lookup"><span data-stu-id="6f76a-347">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="6f76a-348">Si noti che la tabella di origine e la tabella di destinazione hanno schemi diversi (la destinazione include una colonna aggiuntiva identity).</span><span class="sxs-lookup"><span data-stu-id="6f76a-348">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="6f76a-349">In questo scenario, è necessario toospecify **struttura** proprietà nella definizione di set di dati destinazione hello, che non include una colonna identity hello.</span><span class="sxs-lookup"><span data-stu-id="6f76a-349">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="6f76a-350">Chiamare una stored procedure da un sink SQL</span><span class="sxs-lookup"><span data-stu-id="6f76a-350">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="6f76a-351">Per un esempio di come chiamare una stored procedure da un sink SQL in un'attività di copia di una pipeline, vedere l'articolo su come [richiamare una stored procedure per il sink SQL nell'attività di copia](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="6f76a-351">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="6f76a-352">Mapping dei tipi per SQL Server</span><span class="sxs-lookup"><span data-stu-id="6f76a-352">Type mapping for SQL server</span></span>
<span data-ttu-id="6f76a-353">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo hello attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio passaggio 2:</span><span class="sxs-lookup"><span data-stu-id="6f76a-353">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="6f76a-354">Conversione dal tipo di origine nativa tipi too.NET</span><span class="sxs-lookup"><span data-stu-id="6f76a-354">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="6f76a-355">Eseguire la conversione da tipo di sink toonative tipo .NET</span><span class="sxs-lookup"><span data-stu-id="6f76a-355">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="6f76a-356">Quando lo spostamento dei dati troppo & da SQL server, hello mapping seguenti vengono utilizzate dal tipo too.NET di tipo SQL e viceversa.</span><span class="sxs-lookup"><span data-stu-id="6f76a-356">When moving data too& from SQL server, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="6f76a-357">mapping di Hello è identico a hello mapping dei tipi di dati di SQL Server per ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="6f76a-357">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="6f76a-358">Tipo di motore di database di SQL Server</span><span class="sxs-lookup"><span data-stu-id="6f76a-358">SQL Server Database Engine type</span></span> | <span data-ttu-id="6f76a-359">Tipo di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6f76a-359">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="6f76a-360">bigint</span><span class="sxs-lookup"><span data-stu-id="6f76a-360">bigint</span></span> |<span data-ttu-id="6f76a-361">Int64</span><span class="sxs-lookup"><span data-stu-id="6f76a-361">Int64</span></span> |
| <span data-ttu-id="6f76a-362">binary</span><span class="sxs-lookup"><span data-stu-id="6f76a-362">binary</span></span> |<span data-ttu-id="6f76a-363">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6f76a-363">Byte[]</span></span> |
| <span data-ttu-id="6f76a-364">bit</span><span class="sxs-lookup"><span data-stu-id="6f76a-364">bit</span></span> |<span data-ttu-id="6f76a-365">Boolean</span><span class="sxs-lookup"><span data-stu-id="6f76a-365">Boolean</span></span> |
| <span data-ttu-id="6f76a-366">char</span><span class="sxs-lookup"><span data-stu-id="6f76a-366">char</span></span> |<span data-ttu-id="6f76a-367">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6f76a-367">String, Char[]</span></span> |
| <span data-ttu-id="6f76a-368">date</span><span class="sxs-lookup"><span data-stu-id="6f76a-368">date</span></span> |<span data-ttu-id="6f76a-369">DateTime</span><span class="sxs-lookup"><span data-stu-id="6f76a-369">DateTime</span></span> |
| <span data-ttu-id="6f76a-370">DateTime</span><span class="sxs-lookup"><span data-stu-id="6f76a-370">Datetime</span></span> |<span data-ttu-id="6f76a-371">DateTime</span><span class="sxs-lookup"><span data-stu-id="6f76a-371">DateTime</span></span> |
| <span data-ttu-id="6f76a-372">datetime2</span><span class="sxs-lookup"><span data-stu-id="6f76a-372">datetime2</span></span> |<span data-ttu-id="6f76a-373">DateTime</span><span class="sxs-lookup"><span data-stu-id="6f76a-373">DateTime</span></span> |
| <span data-ttu-id="6f76a-374">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="6f76a-374">Datetimeoffset</span></span> |<span data-ttu-id="6f76a-375">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="6f76a-375">DateTimeOffset</span></span> |
| <span data-ttu-id="6f76a-376">Decimale</span><span class="sxs-lookup"><span data-stu-id="6f76a-376">Decimal</span></span> |<span data-ttu-id="6f76a-377">Decimale</span><span class="sxs-lookup"><span data-stu-id="6f76a-377">Decimal</span></span> |
| <span data-ttu-id="6f76a-378">FILESTREAM attribute (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="6f76a-378">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="6f76a-379">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6f76a-379">Byte[]</span></span> |
| <span data-ttu-id="6f76a-380">Float</span><span class="sxs-lookup"><span data-stu-id="6f76a-380">Float</span></span> |<span data-ttu-id="6f76a-381">Double</span><span class="sxs-lookup"><span data-stu-id="6f76a-381">Double</span></span> |
| <span data-ttu-id="6f76a-382">immagine</span><span class="sxs-lookup"><span data-stu-id="6f76a-382">image</span></span> |<span data-ttu-id="6f76a-383">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6f76a-383">Byte[]</span></span> |
| <span data-ttu-id="6f76a-384">int</span><span class="sxs-lookup"><span data-stu-id="6f76a-384">int</span></span> |<span data-ttu-id="6f76a-385">Int32</span><span class="sxs-lookup"><span data-stu-id="6f76a-385">Int32</span></span> |
| <span data-ttu-id="6f76a-386">money</span><span class="sxs-lookup"><span data-stu-id="6f76a-386">money</span></span> |<span data-ttu-id="6f76a-387">Decimale</span><span class="sxs-lookup"><span data-stu-id="6f76a-387">Decimal</span></span> |
| <span data-ttu-id="6f76a-388">nchar</span><span class="sxs-lookup"><span data-stu-id="6f76a-388">nchar</span></span> |<span data-ttu-id="6f76a-389">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6f76a-389">String, Char[]</span></span> |
| <span data-ttu-id="6f76a-390">ntext</span><span class="sxs-lookup"><span data-stu-id="6f76a-390">ntext</span></span> |<span data-ttu-id="6f76a-391">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6f76a-391">String, Char[]</span></span> |
| <span data-ttu-id="6f76a-392">numeric</span><span class="sxs-lookup"><span data-stu-id="6f76a-392">numeric</span></span> |<span data-ttu-id="6f76a-393">Decimale</span><span class="sxs-lookup"><span data-stu-id="6f76a-393">Decimal</span></span> |
| <span data-ttu-id="6f76a-394">nvarchar</span><span class="sxs-lookup"><span data-stu-id="6f76a-394">nvarchar</span></span> |<span data-ttu-id="6f76a-395">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6f76a-395">String, Char[]</span></span> |
| <span data-ttu-id="6f76a-396">real</span><span class="sxs-lookup"><span data-stu-id="6f76a-396">real</span></span> |<span data-ttu-id="6f76a-397">Single</span><span class="sxs-lookup"><span data-stu-id="6f76a-397">Single</span></span> |
| <span data-ttu-id="6f76a-398">rowversion</span><span class="sxs-lookup"><span data-stu-id="6f76a-398">rowversion</span></span> |<span data-ttu-id="6f76a-399">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6f76a-399">Byte[]</span></span> |
| <span data-ttu-id="6f76a-400">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="6f76a-400">smalldatetime</span></span> |<span data-ttu-id="6f76a-401">DateTime</span><span class="sxs-lookup"><span data-stu-id="6f76a-401">DateTime</span></span> |
| <span data-ttu-id="6f76a-402">smallint</span><span class="sxs-lookup"><span data-stu-id="6f76a-402">smallint</span></span> |<span data-ttu-id="6f76a-403">Int16</span><span class="sxs-lookup"><span data-stu-id="6f76a-403">Int16</span></span> |
| <span data-ttu-id="6f76a-404">smallmoney</span><span class="sxs-lookup"><span data-stu-id="6f76a-404">smallmoney</span></span> |<span data-ttu-id="6f76a-405">Decimale</span><span class="sxs-lookup"><span data-stu-id="6f76a-405">Decimal</span></span> |
| <span data-ttu-id="6f76a-406">sql_variant</span><span class="sxs-lookup"><span data-stu-id="6f76a-406">sql_variant</span></span> |<span data-ttu-id="6f76a-407">Object *</span><span class="sxs-lookup"><span data-stu-id="6f76a-407">Object *</span></span> |
| <span data-ttu-id="6f76a-408">text</span><span class="sxs-lookup"><span data-stu-id="6f76a-408">text</span></span> |<span data-ttu-id="6f76a-409">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6f76a-409">String, Char[]</span></span> |
| <span data-ttu-id="6f76a-410">time</span><span class="sxs-lookup"><span data-stu-id="6f76a-410">time</span></span> |<span data-ttu-id="6f76a-411">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="6f76a-411">TimeSpan</span></span> |
| <span data-ttu-id="6f76a-412">timestamp</span><span class="sxs-lookup"><span data-stu-id="6f76a-412">timestamp</span></span> |<span data-ttu-id="6f76a-413">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6f76a-413">Byte[]</span></span> |
| <span data-ttu-id="6f76a-414">tinyint</span><span class="sxs-lookup"><span data-stu-id="6f76a-414">tinyint</span></span> |<span data-ttu-id="6f76a-415">Byte</span><span class="sxs-lookup"><span data-stu-id="6f76a-415">Byte</span></span> |
| <span data-ttu-id="6f76a-416">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="6f76a-416">uniqueidentifier</span></span> |<span data-ttu-id="6f76a-417">Guid</span><span class="sxs-lookup"><span data-stu-id="6f76a-417">Guid</span></span> |
| <span data-ttu-id="6f76a-418">varbinary</span><span class="sxs-lookup"><span data-stu-id="6f76a-418">varbinary</span></span> |<span data-ttu-id="6f76a-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6f76a-419">Byte[]</span></span> |
| <span data-ttu-id="6f76a-420">varchar</span><span class="sxs-lookup"><span data-stu-id="6f76a-420">varchar</span></span> |<span data-ttu-id="6f76a-421">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="6f76a-421">String, Char[]</span></span> |
| <span data-ttu-id="6f76a-422">xml</span><span class="sxs-lookup"><span data-stu-id="6f76a-422">xml</span></span> |<span data-ttu-id="6f76a-423">xml</span><span class="sxs-lookup"><span data-stu-id="6f76a-423">Xml</span></span> |

## <a name="mapping-source-toosink-columns"></a><span data-ttu-id="6f76a-424">Mapping di colonne di origine toosink</span><span class="sxs-lookup"><span data-stu-id="6f76a-424">Mapping source toosink columns</span></span>
<span data-ttu-id="6f76a-425">colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6f76a-425">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="6f76a-426">Copia ripetibile</span><span class="sxs-lookup"><span data-stu-id="6f76a-426">Repeatable copy</span></span>
<span data-ttu-id="6f76a-427">Quando si copiano dati tooSQL Database del Server, attività di copia hello Accoda tabella di dati toohello sink per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6f76a-427">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="6f76a-428">Vedere invece tooperform UPSERT [tooSqlSink scrittura Repeatable](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) articolo.</span><span class="sxs-lookup"><span data-stu-id="6f76a-428">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="6f76a-429">Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="6f76a-429">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="6f76a-430">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="6f76a-430">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="6f76a-431">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="6f76a-431">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="6f76a-432">Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione.</span><span class="sxs-lookup"><span data-stu-id="6f76a-432">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="6f76a-433">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="6f76a-433">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6f76a-434">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="6f76a-434">Performance and Tuning</span></span>
<span data-ttu-id="6f76a-435">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="6f76a-435">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
