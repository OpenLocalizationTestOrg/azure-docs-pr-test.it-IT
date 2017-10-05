---
title: Copiare dati da/verso Oracle con Data Factory | Microsoft Docs
description: Informazioni su come copiare dati da e verso database Oracle locali tramite Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: bb6af719fe6f1a30c5933ce4342a4c0c072f3ff4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="4fd94-103">Copiare dati da/verso un database Oracle locale con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="4fd94-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="4fd94-104">In questo articolo viene illustrato come usare l'attività di copia in Azure Data Factory per spostare i dati da e verso un database Oracle locale.</span><span class="sxs-lookup"><span data-stu-id="4fd94-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="4fd94-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="4fd94-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="4fd94-106">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="4fd94-106">Supported scenarios</span></span>
<span data-ttu-id="4fd94-107">È possibile copiare i dati **da un database di Oracle** negli archivi di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4fd94-107">You can copy data **from an Oracle database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="4fd94-108">È possibile copiare i dati dagli archivi dati seguenti **in un database di Oracle**:</span><span class="sxs-lookup"><span data-stu-id="4fd94-108">You can copy data from the following data stores **to an Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="4fd94-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4fd94-109">Prerequisites</span></span>
<span data-ttu-id="4fd94-110">Data Factory supporta la connessione a origini Oracle locali mediante il gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="4fd94-110">Data Factory supports connecting to on-premises Oracle sources using the Data Management Gateway.</span></span> <span data-ttu-id="4fd94-111">Vedere l'articolo [Gateway di gestione dati](data-factory-data-management-gateway.md) per informazioni sul Gateway di gestione dati e l'articolo [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) per istruzioni dettagliate su come configurare un gateway e una pipeline di dati per spostare i dati.</span><span class="sxs-lookup"><span data-stu-id="4fd94-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article to learn about Data Management Gateway and [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="4fd94-112">Il gateway è necessario anche se il database Oracle è ospitato in una macchina virtuale IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="4fd94-112">Gateway is required even if the Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="4fd94-113">È possibile installare il gateway nella stessa VM IaaS dell'archivio dati o in una macchina virtuale diversa, purché il gateway possa connettersi al database.</span><span class="sxs-lookup"><span data-stu-id="4fd94-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="4fd94-114">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="4fd94-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="4fd94-115">Versioni supportate e installazione</span><span class="sxs-lookup"><span data-stu-id="4fd94-115">Supported versions and installation</span></span>
<span data-ttu-id="4fd94-116">Il connettore Oracle supporta due versioni di driver:</span><span class="sxs-lookup"><span data-stu-id="4fd94-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="4fd94-117">**Driver Microsoft per Oracle (scelta consigliata)**: a partire dal Gateway di gestione dati versione 2.7, un driver Microsoft per Oracle viene installato automaticamente con il gateway, quindi non è necessario di gestire ulteriormente i driver per stabilire la connettività a Oracle ed è possibile inoltre ottenere migliori prestazioni di copia usando questo driver.</span><span class="sxs-lookup"><span data-stu-id="4fd94-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with the gateway, so you don't need to additionally handle the driver in order to establish connectivity to Oracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="4fd94-118">Di seguito sono indicate le versioni dei database di Oracle supportate:</span><span class="sxs-lookup"><span data-stu-id="4fd94-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="4fd94-119">Oracle 12c R1 (12.1)</span><span class="sxs-lookup"><span data-stu-id="4fd94-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="4fd94-120">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="4fd94-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="4fd94-121">Oracle 10g R1, R2 (10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="4fd94-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="4fd94-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="4fd94-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="4fd94-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="4fd94-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4fd94-124">Il driver Microsoft per Oracle supporta attualmente solo la copia dei dati da Oracle ma non la scrittura in Oracle.</span><span class="sxs-lookup"><span data-stu-id="4fd94-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing to Oracle.</span></span> <span data-ttu-id="4fd94-125">Si noti che la funzionalità di connessione di test nella scheda Diagnostica del Gateway di gestione dati supporta questo driver.</span><span class="sxs-lookup"><span data-stu-id="4fd94-125">And note the test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="4fd94-126">In alternativa, è possibile usare la procedura guidata di copia per convalidare la connettività.</span><span class="sxs-lookup"><span data-stu-id="4fd94-126">Alternatively, you can use the copy wizard to validate the connectivity.</span></span>
>

- <span data-ttu-id="4fd94-127">**Provider di dati Oracle per .NET:** è possibile scegliere di usare il Provider di dati Oracle per copiare i dati da/in Oracle.</span><span class="sxs-lookup"><span data-stu-id="4fd94-127">**Oracle Data Provider for .NET:** you can also choose to use Oracle Data Provider to copy data from/to Oracle.</span></span> <span data-ttu-id="4fd94-128">Questo componente è incluso in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4fd94-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="4fd94-129">Installare la versione appropriata (32/64 bit) nel computer in cui è installato il gateway.</span><span class="sxs-lookup"><span data-stu-id="4fd94-129">Install the appropriate version (32/64 bit) on the machine where the gateway is installed.</span></span> <span data-ttu-id="4fd94-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) può accedere a Oracle Database 10g Release 2 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="4fd94-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access to Oracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="4fd94-131">Se si sceglie di installare XCopy, eseguire la procedura indicata nel file readme.htm.</span><span class="sxs-lookup"><span data-stu-id="4fd94-131">If you choose “XCopy Installation”, follow steps in the readme.htm.</span></span> <span data-ttu-id="4fd94-132">È consigliabile scegliere il programma di installazione con l'interfaccia utente (non XCopy).</span><span class="sxs-lookup"><span data-stu-id="4fd94-132">We recommend you choose the installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="4fd94-133">Dopo avere installato il provider, **riavviare** il servizio host di Gateway di gestione dati nel computer mediante l'applet Services (o) Gestione configurazione di Gateway di gestione di dati.</span><span class="sxs-lookup"><span data-stu-id="4fd94-133">After installing the provider, **restart** the Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="4fd94-134">Se si usa la copia guidata per creare la pipeline di copia, il tipo di driver sarà determinato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4fd94-134">If you use copy wizard to author the copy pipeline, the driver type will be auto-determined.</span></span> <span data-ttu-id="4fd94-135">Verrà usato il driver Microsoft per impostazione predefinita, a meno che la versione del gateway sia inferiore a 2.7 o se si sceglie Oracle come sink.</span><span class="sxs-lookup"><span data-stu-id="4fd94-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="4fd94-136">Introduzione</span><span class="sxs-lookup"><span data-stu-id="4fd94-136">Getting started</span></span>
<span data-ttu-id="4fd94-137">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un database di Oracle locale usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="4fd94-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="4fd94-138">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="4fd94-138">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="4fd94-139">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="4fd94-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="4fd94-140">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="4fd94-140">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4fd94-141">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="4fd94-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="4fd94-142">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="4fd94-142">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="4fd94-143">Creare una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="4fd94-143">Create a **data factory**.</span></span> <span data-ttu-id="4fd94-144">Una data factory può contenere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="4fd94-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="4fd94-145">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="4fd94-145">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="4fd94-146">Ad esempio, se si copiano i dati da un database di Oralce in un archivio BLOB di Azure, creare due servizi collegati per collegare il database di Oracle e l'account di archiviazione di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="4fd94-146">For example, if you are copying data from an Oralce database to an Azure blob storage, you create two linked services to link your Oracle database and Azure storage account to your data factory.</span></span> <span data-ttu-id="4fd94-147">Per le proprietà del servizio collegato specifiche per Oracle, vedere la sezione sulle [proprietà del servizio collegato](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4fd94-147">For linked service properties that are specific to Oracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="4fd94-148">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="4fd94-148">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="4fd94-149">Nell'esempio citato nel passaggio precedente si crea un set di dati per specificare la tabella nel database di Oracle che contiene i dati di input.</span><span class="sxs-lookup"><span data-stu-id="4fd94-149">In the example mentioned in the last step, you create a dataset to specify the table in your Oracle database that contains the input data.</span></span> <span data-ttu-id="4fd94-150">Si crea anche un altro set di dati per specificare il contenitore BLOB e la cartella che contiene i dati copiati dal database di Oracle.</span><span class="sxs-lookup"><span data-stu-id="4fd94-150">And, you create another dataset to specify the blob container and the folder that holds the data copied from the Oracle database.</span></span> <span data-ttu-id="4fd94-151">Per le proprietà del set di dati specifiche per Oracle, vedere la sezione sulle [proprietà del set di dati](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4fd94-151">For dataset properties that are specific to Oracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="4fd94-152">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="4fd94-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="4fd94-153">Nell'esempio indicato in precedenza si usa OracleSource come origine e BlobSink come sink per l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="4fd94-153">In the example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="4fd94-154">Analogamente, se si effettua la copia dall'archivio BLOB di Azure al database di Oracle, usare BlobSource e OracleSink nell'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="4fd94-154">Similarly, if you are copying from Azure Blob Storage to Oracle Database, you use BlobSource and OracleSink in the copy activity.</span></span> <span data-ttu-id="4fd94-155">Per le proprietà dell'attività di copia specifiche per il database di Oracle, vedere la sezione sulle [proprietà dell'attività di copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="4fd94-155">For copy activity properties that are specific to Oracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="4fd94-156">Per informazioni dettagliate su come usare un archivio dati come origine o come sink, fare clic sul collegamento nella sezione precedente per l'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="4fd94-156">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="4fd94-157">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4fd94-157">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="4fd94-158">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di data factory.</span><span class="sxs-lookup"><span data-stu-id="4fd94-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="4fd94-159">Per esempi con definizioni JSON per le entità di Data Factory che vengono usate per copiare i dati verso e dal database di Oracle locale, vedere la sezione degli [esempi JSON](#json-examples-for-copying-data-to-and-from-oracle-database) in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="4fd94-159">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="4fd94-160">Nelle sezioni seguenti sono disponibili le informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità della Data Factory:</span><span class="sxs-lookup"><span data-stu-id="4fd94-160">The following sections provide details about JSON properties that are used to define Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4fd94-161">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="4fd94-161">Linked service properties</span></span>
<span data-ttu-id="4fd94-162">La tabella seguente contiene le descrizioni degli elementi JSON specifici del servizio collegato Oracle.</span><span class="sxs-lookup"><span data-stu-id="4fd94-162">The following table provides description for JSON elements specific to Oracle linked service.</span></span>

| <span data-ttu-id="4fd94-163">Proprietà</span><span class="sxs-lookup"><span data-stu-id="4fd94-163">Property</span></span> | <span data-ttu-id="4fd94-164">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4fd94-164">Description</span></span> | <span data-ttu-id="4fd94-165">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4fd94-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4fd94-166">type</span><span class="sxs-lookup"><span data-stu-id="4fd94-166">type</span></span> |<span data-ttu-id="4fd94-167">La proprietà type deve essere impostata su: **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="4fd94-167">The type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="4fd94-168">Sì</span><span class="sxs-lookup"><span data-stu-id="4fd94-168">Yes</span></span> |
| <span data-ttu-id="4fd94-169">driverType</span><span class="sxs-lookup"><span data-stu-id="4fd94-169">driverType</span></span> | <span data-ttu-id="4fd94-170">Specificare il driver da usare per copiare i dati da/verso il database Oracle.</span><span class="sxs-lookup"><span data-stu-id="4fd94-170">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="4fd94-171">I valori consentiti sono **Microsoft** o **ODP** (impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="4fd94-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="4fd94-172">Per informazioni dettagliate sui driver, vedere la sezione [Versione e installazione supportate](#supported-versions-and-installation).</span><span class="sxs-lookup"><span data-stu-id="4fd94-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="4fd94-173">No</span><span class="sxs-lookup"><span data-stu-id="4fd94-173">No</span></span> |
| <span data-ttu-id="4fd94-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="4fd94-174">connectionString</span></span> | <span data-ttu-id="4fd94-175">Specificare le informazioni necessarie per connettersi all'istanza del database Oracle per la proprietà connectionString.</span><span class="sxs-lookup"><span data-stu-id="4fd94-175">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="4fd94-176">Sì</span><span class="sxs-lookup"><span data-stu-id="4fd94-176">Yes</span></span> |
| <span data-ttu-id="4fd94-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="4fd94-177">gatewayName</span></span> | <span data-ttu-id="4fd94-178">Nome del gateway usato per connettersi al server Oracle locale</span><span class="sxs-lookup"><span data-stu-id="4fd94-178">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="4fd94-179">Sì</span><span class="sxs-lookup"><span data-stu-id="4fd94-179">Yes</span></span> |

<span data-ttu-id="4fd94-180">**Esempio: mediante il driver Microsoft:**</span><span class="sxs-lookup"><span data-stu-id="4fd94-180">**Example: using Microsoft driver:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="4fd94-181">**Esempio: mediante il driver ODP**</span><span class="sxs-lookup"><span data-stu-id="4fd94-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="4fd94-182">Per informazioni sui formati consentiti, vedere [questo sito](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/).</span><span class="sxs-lookup"><span data-stu-id="4fd94-182">Refer to [this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for the allowed formats.</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="4fd94-183">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="4fd94-183">Dataset properties</span></span>
<span data-ttu-id="4fd94-184">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="4fd94-184">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="4fd94-185">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati (Oracle, BLOB di Azure, tabelle di Azure e così via).</span><span class="sxs-lookup"><span data-stu-id="4fd94-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="4fd94-186">La sezione typeProperties è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="4fd94-186">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="4fd94-187">La sezione typeProperties per il set di dati di tipo OracleTable presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="4fd94-187">The typeProperties section for the dataset of type OracleTable has the following properties:</span></span>

| <span data-ttu-id="4fd94-188">Proprietà</span><span class="sxs-lookup"><span data-stu-id="4fd94-188">Property</span></span> | <span data-ttu-id="4fd94-189">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4fd94-189">Description</span></span> | <span data-ttu-id="4fd94-190">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4fd94-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4fd94-191">tableName</span><span class="sxs-lookup"><span data-stu-id="4fd94-191">tableName</span></span> |<span data-ttu-id="4fd94-192">Nome della tabella nell'istanza del database Oracle a cui fa riferimento il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="4fd94-192">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="4fd94-193">No, se **oracleReaderQuery** di **OracleSource** è specificato</span><span class="sxs-lookup"><span data-stu-id="4fd94-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="4fd94-194">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="4fd94-194">Copy activity properties</span></span>
<span data-ttu-id="4fd94-195">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="4fd94-195">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4fd94-196">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="4fd94-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="4fd94-197">L'attività di copia accetta solo un input e produce solo un output.</span><span class="sxs-lookup"><span data-stu-id="4fd94-197">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="4fd94-198">Le proprietà disponibili nella sezione typeProperties dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="4fd94-198">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="4fd94-199">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="4fd94-199">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="4fd94-200">OracleSource</span><span class="sxs-lookup"><span data-stu-id="4fd94-200">OracleSource</span></span>
<span data-ttu-id="4fd94-201">Nell'attività di copia con origine di tipo **OracleSource** sono disponibili le proprietà seguenti nella sezione **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="4fd94-201">In Copy activity, when the source is of type **OracleSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="4fd94-202">Proprietà</span><span class="sxs-lookup"><span data-stu-id="4fd94-202">Property</span></span> | <span data-ttu-id="4fd94-203">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4fd94-203">Description</span></span> | <span data-ttu-id="4fd94-204">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="4fd94-204">Allowed values</span></span> | <span data-ttu-id="4fd94-205">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4fd94-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4fd94-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="4fd94-206">oracleReaderQuery</span></span> |<span data-ttu-id="4fd94-207">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="4fd94-207">Use the custom query to read data.</span></span> |<span data-ttu-id="4fd94-208">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="4fd94-208">SQL query string.</span></span> <span data-ttu-id="4fd94-209">Ad esempio: selezionare * da MyTable</span><span class="sxs-lookup"><span data-stu-id="4fd94-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="4fd94-210">Se non specificato, l'istruzione SQL eseguita è: selezionare * da MyTable</span><span class="sxs-lookup"><span data-stu-id="4fd94-210">If not specified, the SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="4fd94-211">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="4fd94-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="4fd94-212">OracleSink</span><span class="sxs-lookup"><span data-stu-id="4fd94-212">OracleSink</span></span>
<span data-ttu-id="4fd94-213">**OracleSink** supporta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="4fd94-213">**OracleSink** supports the following properties:</span></span>

| <span data-ttu-id="4fd94-214">Proprietà</span><span class="sxs-lookup"><span data-stu-id="4fd94-214">Property</span></span> | <span data-ttu-id="4fd94-215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4fd94-215">Description</span></span> | <span data-ttu-id="4fd94-216">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="4fd94-216">Allowed values</span></span> | <span data-ttu-id="4fd94-217">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4fd94-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4fd94-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="4fd94-218">writeBatchTimeout</span></span> |<span data-ttu-id="4fd94-219">Tempo di attesa per l'operazione di inserimento batch da completare prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="4fd94-219">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="4fd94-220">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="4fd94-220">timespan</span></span><br/><br/> <span data-ttu-id="4fd94-221">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="4fd94-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="4fd94-222">No</span><span class="sxs-lookup"><span data-stu-id="4fd94-222">No</span></span> |
| <span data-ttu-id="4fd94-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="4fd94-223">writeBatchSize</span></span> |<span data-ttu-id="4fd94-224">Inserisce dati nella tabella SQL quando la dimensione del buffer raggiunge writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="4fd94-224">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="4fd94-225">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="4fd94-225">Integer (number of rows)</span></span> |<span data-ttu-id="4fd94-226">No (valore predefinito: 100)</span><span class="sxs-lookup"><span data-stu-id="4fd94-226">No (default: 100)</span></span> |
| <span data-ttu-id="4fd94-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="4fd94-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="4fd94-228">Specificare una query da eseguire nell'attività di copia per pulire i dati di una sezione specifica.</span><span class="sxs-lookup"><span data-stu-id="4fd94-228">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="4fd94-229">Istruzione di query.</span><span class="sxs-lookup"><span data-stu-id="4fd94-229">A query statement.</span></span> |<span data-ttu-id="4fd94-230">No</span><span class="sxs-lookup"><span data-stu-id="4fd94-230">No</span></span> |
| <span data-ttu-id="4fd94-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="4fd94-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="4fd94-232">Specificare il nome della colonna per l'attività di copia da riempire con l'identificatore di sezione generato automaticamente, che viene usato per eliminare i dati di una sezione specifica quando viene nuovamente eseguita.</span><span class="sxs-lookup"><span data-stu-id="4fd94-232">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="4fd94-233">Nome di colonna di una colonna con tipo di dati binario (32).</span><span class="sxs-lookup"><span data-stu-id="4fd94-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="4fd94-234">No</span><span class="sxs-lookup"><span data-stu-id="4fd94-234">No</span></span> |

## <a name="json-examples-for-copying-data-to-and-from-oracle-database"></a><span data-ttu-id="4fd94-235">Esempi JSON per la copia dei dati da e verso un database di Oracle</span><span class="sxs-lookup"><span data-stu-id="4fd94-235">JSON examples for copying data to and from Oracle database</span></span>
<span data-ttu-id="4fd94-236">L'esempio seguente fornisce le definizioni JSON campione da usare per creare una pipeline con il [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4fd94-236">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="4fd94-237">Illustrano come copiare dati da un database Oracle in un archivio BLOB di Azure e viceversa.</span><span class="sxs-lookup"><span data-stu-id="4fd94-237">They show how to copy data from/to an Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="4fd94-238">Tuttavia, i dati possono essere copiati in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4fd94-238">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-to-azure-blob"></a><span data-ttu-id="4fd94-239">Esempio: Copiare i dati da Oracle a BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="4fd94-239">Example: Copy data from Oracle to Azure Blob</span></span>

<span data-ttu-id="4fd94-240">L'esempio include le entità di Data factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="4fd94-240">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="4fd94-241">Un servizio collegato di tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4fd94-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="4fd94-242">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4fd94-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="4fd94-243">Un [set di dati](data-factory-create-datasets.md) di input di tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4fd94-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="4fd94-244">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4fd94-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="4fd94-245">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) come origine e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) come sink.</span><span class="sxs-lookup"><span data-stu-id="4fd94-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="4fd94-246">L'esempio copia i dati da una tabella di un database Oracle locale a un BLOB ogni ora.</span><span class="sxs-lookup"><span data-stu-id="4fd94-246">The sample copies data from a table in an on-premises Oracle database to a blob hourly.</span></span> <span data-ttu-id="4fd94-247">Per altre informazioni sulle varie proprietà usate nell'esempio, vedere la documentazione nelle sezioni che seguono gli esempi.</span><span class="sxs-lookup"><span data-stu-id="4fd94-247">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="4fd94-248">**Servizio collegato Oracle:**</span><span class="sxs-lookup"><span data-stu-id="4fd94-248">**Oracle linked service:**</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="4fd94-249">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="4fd94-249">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="4fd94-250">**Set di dati di input Oracle:**</span><span class="sxs-lookup"><span data-stu-id="4fd94-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="4fd94-251">L'esempio presuppone che sia stata creata una tabella "MyTable" in Oracle e che contenga una colonna denominata "timestampcolumn" per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="4fd94-251">The sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="4fd94-252">Impostando "external" su "true" si comunica al servizio Data Factory che il set di dati è esterno alla data factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="4fd94-252">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
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

<span data-ttu-id="4fd94-253">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="4fd94-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="4fd94-254">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="4fd94-254">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="4fd94-255">Il percorso della cartella e il nome del file per il BLOB vengono valutati dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="4fd94-255">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="4fd94-256">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="4fd94-256">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="4fd94-257">**Pipeline con attività di copia:**</span><span class="sxs-lookup"><span data-stu-id="4fd94-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="4fd94-258">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="4fd94-258">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="4fd94-259">Nella definizione JSON della pipeline il tipo di **origine** è impostato su **OracleSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="4fd94-259">In the pipeline JSON definition, the **source** type is set to **OracleSource** and **sink** type is set to **BlobSink**.</span></span>  <span data-ttu-id="4fd94-260">La query SQL specificata con la proprietà **oracleReaderQuery** consente di selezionare i dati da copiare nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="4fd94-260">The SQL query specified with **oracleReaderQuery** property selects the data in the past hour to copy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-to-oracle"></a><span data-ttu-id="4fd94-261">Esempio: Copiare i dati dal BLOB di Azure in Oracle</span><span class="sxs-lookup"><span data-stu-id="4fd94-261">Example: Copy data from Azure Blob to Oracle</span></span>
<span data-ttu-id="4fd94-262">Questo esempio illustra come copiare dati da un archivio BLOB di Azure a un database Oracle locale.</span><span class="sxs-lookup"><span data-stu-id="4fd94-262">This sample shows how to copy data from an Azure Blob Storage to an on-premises Oracle database.</span></span> <span data-ttu-id="4fd94-263">I dati possono tuttavia essere copiati **direttamente** da qualsiasi origine dichiarata [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4fd94-263">However, data can be copied **directly** from any of the sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="4fd94-264">L'esempio include le entità di Data factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="4fd94-264">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="4fd94-265">Un servizio collegato di tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4fd94-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="4fd94-266">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4fd94-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="4fd94-267">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4fd94-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="4fd94-268">Un [set di dati](data-factory-create-datasets.md) di output di tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4fd94-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="4fd94-269">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) come origine e [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) come sink.</span><span class="sxs-lookup"><span data-stu-id="4fd94-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="4fd94-270">L'esempio copia i dati da un BLOB a una tabella nel database Oracle locale ogni ora.</span><span class="sxs-lookup"><span data-stu-id="4fd94-270">The sample copies data from a blob to a table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="4fd94-271">Per altre informazioni sulle varie proprietà usate nell'esempio, vedere la documentazione nelle sezioni che seguono gli esempi.</span><span class="sxs-lookup"><span data-stu-id="4fd94-271">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="4fd94-272">**Servizio collegato Oracle:**</span><span class="sxs-lookup"><span data-stu-id="4fd94-272">**Oracle linked service:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="4fd94-273">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="4fd94-273">**Azure Blob storage linked service:**</span></span>
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="4fd94-274">**Set di dati di input del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="4fd94-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="4fd94-275">I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="4fd94-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="4fd94-276">Il percorso della cartella e il nome del file per il BLOB vengono valutati dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="4fd94-276">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="4fd94-277">Il percorso della cartella usa le parti di anno, mese e giorno della data/ora di inizio e il nome file usa la parte relativa all'ora.</span><span class="sxs-lookup"><span data-stu-id="4fd94-277">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="4fd94-278">L'impostazione di "external" su "true" comunica al servizio Data Factory che la tabella è esterna alla data factory e non è prodotta da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="4fd94-278">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
            "frequency": "Day",
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

<span data-ttu-id="4fd94-279">**Set di dati di output Oracle:**</span><span class="sxs-lookup"><span data-stu-id="4fd94-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="4fd94-280">L'esempio presuppone che sia stata creata una tabella "MyTable" in Oracle.</span><span class="sxs-lookup"><span data-stu-id="4fd94-280">The sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="4fd94-281">È necessario creare la tabella in Oracle con lo stesso numero di colonne contenute nel file con estensione csv del BLOB.</span><span class="sxs-lookup"><span data-stu-id="4fd94-281">Create the table in Oracle with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="4fd94-282">Alla tabella vengono aggiunte nuove righe ogni ora.</span><span class="sxs-lookup"><span data-stu-id="4fd94-282">New rows are added to the table every hour.</span></span>

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

<span data-ttu-id="4fd94-283">**Pipeline con attività di copia:**</span><span class="sxs-lookup"><span data-stu-id="4fd94-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="4fd94-284">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="4fd94-284">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="4fd94-285">Nella definizione JSON della pipeline il tipo di **origine** è impostato su **BlobSource** e il tipo di **sink** è impostato su **OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="4fd94-285">In the pipeline JSON definition, the **source** type is set to **BlobSource** and the **sink** type is set to **OracleSink**.</span></span>  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a><span data-ttu-id="4fd94-286">Suggerimenti per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="4fd94-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="4fd94-287">Problema 1: provider di dati .NET Framework</span><span class="sxs-lookup"><span data-stu-id="4fd94-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="4fd94-288">Viene visualizzato il **messaggio di errore** seguente:</span><span class="sxs-lookup"><span data-stu-id="4fd94-288">You see the following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable to find the requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="4fd94-289">**Possibili cause:**</span><span class="sxs-lookup"><span data-stu-id="4fd94-289">**Possible causes:**</span></span>

1. <span data-ttu-id="4fd94-290">Non è stato installato il Provider di dati Framework .NET per Oracle.</span><span class="sxs-lookup"><span data-stu-id="4fd94-290">The .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="4fd94-291">Il Provider di dati Framework .NET per Oracle è stato installato nel Framework .NET 2.0 e non è disponibile nelle cartelle del Framework.NET 4.0.</span><span class="sxs-lookup"><span data-stu-id="4fd94-291">The .NET Framework Data Provider for Oracle was installed to .NET Framework 2.0 and is not found in the .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="4fd94-292">**Risoluzione/Soluzione alternativa:**</span><span class="sxs-lookup"><span data-stu-id="4fd94-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="4fd94-293">Se non è stato installato il provider .NET per Oracle, [installarlo](http://www.oracle.com/technetwork/topics/dotnet/downloads/) e ripetere lo scenario.</span><span class="sxs-lookup"><span data-stu-id="4fd94-293">If you haven't installed the .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry the scenario.</span></span>
2. <span data-ttu-id="4fd94-294">Se viene visualizzato il messaggio di errore anche dopo l'installazione del provider, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4fd94-294">If you get the error message even after installing the provider, do the following steps:</span></span>
   1. <span data-ttu-id="4fd94-295">Aprire la configurazione del computer di .NET 2.0 dalla cartella: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="4fd94-295">Open machine config of .NET 2.0 from the folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="4fd94-296">Cercare **Provider di dati Oracle per .NET** per trovare una voce, come illustrato nell'esempio seguente in **system.data** -> **DbProviderFactories**: "<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Provider di dati Oracle per .NET</span><span class="sxs-lookup"><span data-stu-id="4fd94-296">Search for **Oracle Data Provider for .NET**, and you should be able to find an entry as shown in the following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="4fd94-297">"</span><span class="sxs-lookup"><span data-stu-id="4fd94-297">”</span></span>
3. <span data-ttu-id="4fd94-298">Copiare questa voce nel file .config del computer nella seguente cartella v4.0: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config e modificare la versione a 4.xxx.x.x.</span><span class="sxs-lookup"><span data-stu-id="4fd94-298">Copy this entry to the machine.config file in the following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change the version to 4.xxx.x.x.</span></span>
4. <span data-ttu-id="4fd94-299">Installare "<percorso di installazione di ODP.NET>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll" nella Global Assembly Cache eseguendo `gacutil /i [provider path]`.## Suggerimenti per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="4fd94-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into the global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="4fd94-300">Problema 2: formattazione di DateTime</span><span class="sxs-lookup"><span data-stu-id="4fd94-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="4fd94-301">Viene visualizzato il **messaggio di errore** seguente:</span><span class="sxs-lookup"><span data-stu-id="4fd94-301">You see the following **error message**:</span></span>

    Message=Operation failed in Oracle Database with the following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="4fd94-302">**Risoluzione/Soluzione alternativa:**</span><span class="sxs-lookup"><span data-stu-id="4fd94-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="4fd94-303">Potrebbe essere necessario modificare la stringa di query nell'attività di copia in base al modo in cui le date sono configurate nel database Oracle, come illustrato nell'esempio seguente (usando la funzione to_date):</span><span class="sxs-lookup"><span data-stu-id="4fd94-303">You may need to adjust the query string in your copy activity based on how dates are configured in your Oracle database, as shown in the following sample (using the to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="4fd94-304">Mapping dei tipi per Oracle</span><span class="sxs-lookup"><span data-stu-id="4fd94-304">Type mapping for Oracle</span></span>
<span data-ttu-id="4fd94-305">Come accennato nell'articolo sulle [attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni automatiche da tipi di origine a tipi di sink con l'approccio seguente in 2 passaggi:</span><span class="sxs-lookup"><span data-stu-id="4fd94-305">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="4fd94-306">Conversione dai tipi di origine nativi al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="4fd94-306">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="4fd94-307">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="4fd94-307">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="4fd94-308">Quando si spostano dati da Oracle, vengono usati i mapping seguenti dal tipo di dati Oracle al tipo .NET e viceversa.</span><span class="sxs-lookup"><span data-stu-id="4fd94-308">When moving data from Oracle, the following mappings are used from Oracle data type to .NET type and vice versa.</span></span>

| <span data-ttu-id="4fd94-309">Tipo di dati Oracle</span><span class="sxs-lookup"><span data-stu-id="4fd94-309">Oracle data type</span></span> | <span data-ttu-id="4fd94-310">Tipo di dati .NET Framework</span><span class="sxs-lookup"><span data-stu-id="4fd94-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="4fd94-311">BFILE</span><span class="sxs-lookup"><span data-stu-id="4fd94-311">BFILE</span></span> |<span data-ttu-id="4fd94-312">Byte[]</span><span class="sxs-lookup"><span data-stu-id="4fd94-312">Byte[]</span></span> |
| <span data-ttu-id="4fd94-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="4fd94-313">BLOB</span></span> |<span data-ttu-id="4fd94-314">Byte[]</span><span class="sxs-lookup"><span data-stu-id="4fd94-314">Byte[]</span></span> |
| <span data-ttu-id="4fd94-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="4fd94-315">CHAR</span></span> |<span data-ttu-id="4fd94-316">String</span><span class="sxs-lookup"><span data-stu-id="4fd94-316">String</span></span> |
| <span data-ttu-id="4fd94-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="4fd94-317">CLOB</span></span> |<span data-ttu-id="4fd94-318">String</span><span class="sxs-lookup"><span data-stu-id="4fd94-318">String</span></span> |
| <span data-ttu-id="4fd94-319">DATE</span><span class="sxs-lookup"><span data-stu-id="4fd94-319">DATE</span></span> |<span data-ttu-id="4fd94-320">DateTime</span><span class="sxs-lookup"><span data-stu-id="4fd94-320">DateTime</span></span> |
| <span data-ttu-id="4fd94-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="4fd94-321">FLOAT</span></span> |<span data-ttu-id="4fd94-322">Decimal, String (se la precisione > 28)</span><span class="sxs-lookup"><span data-stu-id="4fd94-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="4fd94-323">INTEGER</span><span class="sxs-lookup"><span data-stu-id="4fd94-323">INTEGER</span></span> |<span data-ttu-id="4fd94-324">Decimal, String (se la precisione > 28)</span><span class="sxs-lookup"><span data-stu-id="4fd94-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="4fd94-325">INTERVAL YEAR TO MONTH</span><span class="sxs-lookup"><span data-stu-id="4fd94-325">INTERVAL YEAR TO MONTH</span></span> |<span data-ttu-id="4fd94-326">Int32</span><span class="sxs-lookup"><span data-stu-id="4fd94-326">Int32</span></span> |
| <span data-ttu-id="4fd94-327">INTERVAL DAY TO SECOND</span><span class="sxs-lookup"><span data-stu-id="4fd94-327">INTERVAL DAY TO SECOND</span></span> |<span data-ttu-id="4fd94-328">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="4fd94-328">TimeSpan</span></span> |
| <span data-ttu-id="4fd94-329">LONG</span><span class="sxs-lookup"><span data-stu-id="4fd94-329">LONG</span></span> |<span data-ttu-id="4fd94-330">String</span><span class="sxs-lookup"><span data-stu-id="4fd94-330">String</span></span> |
| <span data-ttu-id="4fd94-331">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="4fd94-331">LONG RAW</span></span> |<span data-ttu-id="4fd94-332">Byte[]</span><span class="sxs-lookup"><span data-stu-id="4fd94-332">Byte[]</span></span> |
| <span data-ttu-id="4fd94-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="4fd94-333">NCHAR</span></span> |<span data-ttu-id="4fd94-334">String</span><span class="sxs-lookup"><span data-stu-id="4fd94-334">String</span></span> |
| <span data-ttu-id="4fd94-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="4fd94-335">NCLOB</span></span> |<span data-ttu-id="4fd94-336">String</span><span class="sxs-lookup"><span data-stu-id="4fd94-336">String</span></span> |
| <span data-ttu-id="4fd94-337">NUMBER</span><span class="sxs-lookup"><span data-stu-id="4fd94-337">NUMBER</span></span> |<span data-ttu-id="4fd94-338">Decimal, String (se la precisione > 28)</span><span class="sxs-lookup"><span data-stu-id="4fd94-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="4fd94-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="4fd94-339">NVARCHAR2</span></span> |<span data-ttu-id="4fd94-340">String</span><span class="sxs-lookup"><span data-stu-id="4fd94-340">String</span></span> |
| <span data-ttu-id="4fd94-341">RAW</span><span class="sxs-lookup"><span data-stu-id="4fd94-341">RAW</span></span> |<span data-ttu-id="4fd94-342">Byte[]</span><span class="sxs-lookup"><span data-stu-id="4fd94-342">Byte[]</span></span> |
| <span data-ttu-id="4fd94-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="4fd94-343">ROWID</span></span> |<span data-ttu-id="4fd94-344">String</span><span class="sxs-lookup"><span data-stu-id="4fd94-344">String</span></span> |
| <span data-ttu-id="4fd94-345">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="4fd94-345">TIMESTAMP</span></span> |<span data-ttu-id="4fd94-346">DateTime</span><span class="sxs-lookup"><span data-stu-id="4fd94-346">DateTime</span></span> |
| <span data-ttu-id="4fd94-347">TIMESTAMP WITH LOCAL TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="4fd94-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="4fd94-348">DateTime</span><span class="sxs-lookup"><span data-stu-id="4fd94-348">DateTime</span></span> |
| <span data-ttu-id="4fd94-349">TIMESTAMP WITH TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="4fd94-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="4fd94-350">DateTime</span><span class="sxs-lookup"><span data-stu-id="4fd94-350">DateTime</span></span> |
| <span data-ttu-id="4fd94-351">UNSIGNED INTEGER</span><span class="sxs-lookup"><span data-stu-id="4fd94-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="4fd94-352">NUMBER</span><span class="sxs-lookup"><span data-stu-id="4fd94-352">Number</span></span> |
| <span data-ttu-id="4fd94-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="4fd94-353">VARCHAR2</span></span> |<span data-ttu-id="4fd94-354">String</span><span class="sxs-lookup"><span data-stu-id="4fd94-354">String</span></span> |
| <span data-ttu-id="4fd94-355">XML</span><span class="sxs-lookup"><span data-stu-id="4fd94-355">XML</span></span> |<span data-ttu-id="4fd94-356">string</span><span class="sxs-lookup"><span data-stu-id="4fd94-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="4fd94-357">I tipi di dati **INTERVAL YEAR TO MONTH** e **INTERVAL DAY TO SECOND** non sono supportati quando si usa il driver Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4fd94-357">Data type **INTERVAL YEAR TO MONTH** and **INTERVAL DAY TO SECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="4fd94-358">Eseguire il mapping delle colonne dell'origine alle colonne del sink</span><span class="sxs-lookup"><span data-stu-id="4fd94-358">Map source to sink columns</span></span>
<span data-ttu-id="4fd94-359">Per informazioni sul mapping delle colonne del set di dati di origine alle colonne del set di dati del sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="4fd94-359">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="4fd94-360">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="4fd94-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="4fd94-361">Quando si copiano dati da archivi dati relazionali, è necessario tenere presente la ripetibilità per evitare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="4fd94-361">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="4fd94-362">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="4fd94-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="4fd94-363">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="4fd94-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="4fd94-364">Quando una sezione viene rieseguita in uno dei due modi, è necessario assicurarsi che non vengano letti gli stessi dati, indipendentemente da quante volte viene eseguita la sezione.</span><span class="sxs-lookup"><span data-stu-id="4fd94-364">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="4fd94-365">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="4fd94-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="4fd94-366">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="4fd94-366">Performance and Tuning</span></span>
<span data-ttu-id="4fd94-367">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="4fd94-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
