---
title: dati aaaCopy a/da Oracle utilizzando Data Factory | Documenti Microsoft
description: Informazioni su come dati toocopy a/da database Oracle in locale con Azure Data Factory.
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
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="4a0b5-103">Copiare dati da/verso un database Oracle locale con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="4a0b5-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="4a0b5-104">Questo articolo spiega come toouse hello attività di copia dei dati di Azure Data Factory toomove a/da un database Oracle locale.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="4a0b5-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="4a0b5-106">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="4a0b5-106">Supported scenarios</span></span>
<span data-ttu-id="4a0b5-107">È possibile copiare dati **da un database Oracle** toohello archivi dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a0b5-107">You can copy data **from an Oracle database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="4a0b5-108">È possibile copiare dati da archivi dati seguenti hello **database Oracle tooan**:</span><span class="sxs-lookup"><span data-stu-id="4a0b5-108">You can copy data from hello following data stores **tooan Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="4a0b5-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4a0b5-109">Prerequisites</span></span>
<span data-ttu-id="4a0b5-110">Data Factory supporta origini di Oracle locale tooon connessione hello Gateway di gestione dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-110">Data Factory supports connecting tooon-premises Oracle sources using hello Data Management Gateway.</span></span> <span data-ttu-id="4a0b5-111">Vedere [Gateway di gestione dati](data-factory-data-management-gateway.md) toolearn articolo sul Gateway di gestione dati e [spostare i dati da on-premise toocloud](data-factory-move-data-between-onprem-and-cloud.md) per istruzioni dettagliate su come configurare il gateway hello una pipeline di dati dati toomove.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article toolearn about Data Management Gateway and [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="4a0b5-112">Anche se hello Oracle è ospitato in una macchina virtuale IaaS di Azure, è necessario gateway.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-112">Gateway is required even if hello Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="4a0b5-113">È possibile installare il gateway di hello in hello stessa VM IaaS come dati hello archiviare o su una macchina virtuale diversa, purché il gateway hello può connettersi toohello database.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="4a0b5-114">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="4a0b5-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="4a0b5-115">Versioni supportate e installazione</span><span class="sxs-lookup"><span data-stu-id="4a0b5-115">Supported versions and installation</span></span>
<span data-ttu-id="4a0b5-116">Il connettore Oracle supporta due versioni di driver:</span><span class="sxs-lookup"><span data-stu-id="4a0b5-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="4a0b5-117">**Driver Microsoft per Oracle (scelta consigliata)**: a partire dal Gateway di gestione dati versione 2.7, un driver Microsoft per Oracle viene installato automaticamente insieme ai gateway hello, pertanto non è necessario driver hello di handle tooadditionally in ordine tooestablish connettività tooOracle ed è possibile inoltre prestazioni migliori copia utilizzando questo driver.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with hello gateway, so you don't need tooadditionally handle hello driver in order tooestablish connectivity tooOracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="4a0b5-118">Di seguito sono indicate le versioni dei database di Oracle supportate:</span><span class="sxs-lookup"><span data-stu-id="4a0b5-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="4a0b5-119">Oracle 12c R1 (12.1)</span><span class="sxs-lookup"><span data-stu-id="4a0b5-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="4a0b5-120">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="4a0b5-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="4a0b5-121">Oracle 10g R1, R2 (10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="4a0b5-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="4a0b5-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="4a0b5-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="4a0b5-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="4a0b5-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a0b5-124">Driver Microsoft per Oracle supporta attualmente solo copia dati da Oracle ma non di scrivere tooOracle.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing tooOracle.</span></span> <span data-ttu-id="4a0b5-125">E funzionalità di connessione di test nota hello nella scheda diagnostica Gateway di gestione dati non supporta questo driver.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-125">And note hello test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="4a0b5-126">In alternativa, è possibile utilizzare la connettività hello hello Copia guidata toovalidate.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-126">Alternatively, you can use hello copy wizard toovalidate hello connectivity.</span></span>
>

- <span data-ttu-id="4a0b5-127">**Provider di dati Oracle per .NET:** è anche possibile scegliere i dati di toocopy toouse Provider di dati Oracle da / tooOracle.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-127">**Oracle Data Provider for .NET:** you can also choose toouse Oracle Data Provider toocopy data from/tooOracle.</span></span> <span data-ttu-id="4a0b5-128">Questo componente è incluso in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="4a0b5-129">Installare la versione appropriata hello (32/64 bit) nel computer di hello in cui è installato il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-129">Install hello appropriate version (32/64 bit) on hello machine where hello gateway is installed.</span></span> <span data-ttu-id="4a0b5-130">[Il Provider di dati Oracle .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) possono accedere tooOracle Database 10g Release 2 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access tooOracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="4a0b5-131">Se si sceglie "Installazione di XCopy", seguire i passaggi in hello Readme. htm.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-131">If you choose “XCopy Installation”, follow steps in hello readme.htm.</span></span> <span data-ttu-id="4a0b5-132">Si consiglia di che scegliere installazione hello con interfaccia utente (non-XCopy uno).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-132">We recommend you choose hello installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="4a0b5-133">Dopo avere installato il provider di hello, **riavviare** hello servizio host di Gateway di gestione dati nel computer utilizzando servizi applet (o) Gestione configurazione di Gateway di gestione di dati.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-133">After installing hello provider, **restart** hello Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="4a0b5-134">Se si utilizza Copia guidata tooauthor hello copia pipeline, il tipo di driver hello sarà determinato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-134">If you use copy wizard tooauthor hello copy pipeline, hello driver type will be auto-determined.</span></span> <span data-ttu-id="4a0b5-135">Verrà usato il driver Microsoft per impostazione predefinita, a meno che la versione del gateway sia inferiore a 2.7 o se si sceglie Oracle come sink.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="4a0b5-136">Introduzione</span><span class="sxs-lookup"><span data-stu-id="4a0b5-136">Getting started</span></span>
<span data-ttu-id="4a0b5-137">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un database di Oracle locale usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="4a0b5-138">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-138">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="4a0b5-139">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="4a0b5-140">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-140">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4a0b5-141">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="4a0b5-142">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a0b5-142">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="4a0b5-143">Creare una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-143">Create a **data factory**.</span></span> <span data-ttu-id="4a0b5-144">Una data factory può contenere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="4a0b5-145">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-145">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="4a0b5-146">Ad esempio, se si copiano dati da un tooan database Oralce archiviazione blob di Azure, è creare due servizi collegati toolink il database Oracle e la data factory tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-146">For example, if you are copying data from an Oralce database tooan Azure blob storage, you create two linked services toolink your Oracle database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="4a0b5-147">Per le proprietà di servizio collegato che sono tooOracle specifici, vedere [servizio proprietà collegate](#linked-service-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-147">For linked service properties that are specific tooOracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="4a0b5-148">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-148">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="4a0b5-149">Nell'esempio hello indicato nell'ultimo passaggio hello creare una tabella di hello toospecify di set di dati nel database Oracle che contiene i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-149">In hello example mentioned in hello last step, you create a dataset toospecify hello table in your Oracle database that contains hello input data.</span></span> <span data-ttu-id="4a0b5-150">E, per creare un altro set di dati toospecify hello blob contenitore e cartella hello contenente hello dati copiati dal hello database Oracle.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-150">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello Oracle database.</span></span> <span data-ttu-id="4a0b5-151">Per le proprietà di set di dati che sono tooOracle specifici, vedere [proprietà set di dati](#dataset-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-151">For dataset properties that are specific tooOracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="4a0b5-152">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="4a0b5-153">Nell'esempio hello indicato in precedenza, si usa OracleSource come un'origine e BlobSink come sink per attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-153">In hello example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="4a0b5-154">Analogamente, se si sta copiando l'archiviazione Blob di Azure tooOracle Database, utilizzare BlobSource e OracleSink nell'attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-154">Similarly, if you are copying from Azure Blob Storage tooOracle Database, you use BlobSource and OracleSink in hello copy activity.</span></span> <span data-ttu-id="4a0b5-155">Per le proprietà di attività di copia che sono tooOracle specifici database, vedere [copiare le proprietà dell'attività](#copy-activity-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-155">For copy activity properties that are specific tooOracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="4a0b5-156">Per informazioni dettagliate su come toouse un archivio dati come origine o un sink, fare clic sul collegamento di hello nella sezione precedente di hello per l'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-156">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="4a0b5-157">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-157">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="4a0b5-158">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="4a0b5-159">Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati i dati in o da un database Oracle locale, vedere [esempi JSON](#json-examples-for-copying-data-to-and-from-oracle-database) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-159">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="4a0b5-160">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che sono utilizzati toodefine Data Factory entità:</span><span class="sxs-lookup"><span data-stu-id="4a0b5-160">hello following sections provide details about JSON properties that are used toodefine Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4a0b5-161">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="4a0b5-161">Linked service properties</span></span>
<span data-ttu-id="4a0b5-162">Hello nella tabella seguente fornisce una descrizione del servizio specifico tooOracle collegati gli elementi JSON.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-162">hello following table provides description for JSON elements specific tooOracle linked service.</span></span>

| <span data-ttu-id="4a0b5-163">Proprietà</span><span class="sxs-lookup"><span data-stu-id="4a0b5-163">Property</span></span> | <span data-ttu-id="4a0b5-164">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a0b5-164">Description</span></span> | <span data-ttu-id="4a0b5-165">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a0b5-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a0b5-166">type</span><span class="sxs-lookup"><span data-stu-id="4a0b5-166">type</span></span> |<span data-ttu-id="4a0b5-167">proprietà di tipo Hello deve essere impostata su: **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="4a0b5-167">hello type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="4a0b5-168">Sì</span><span class="sxs-lookup"><span data-stu-id="4a0b5-168">Yes</span></span> |
| <span data-ttu-id="4a0b5-169">driverType</span><span class="sxs-lookup"><span data-stu-id="4a0b5-169">driverType</span></span> | <span data-ttu-id="4a0b5-170">Specificare i dati del driver toouse toocopy da / tooOracle Database.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-170">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="4a0b5-171">I valori consentiti sono **Microsoft** o **ODP** (impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="4a0b5-172">Per informazioni dettagliate sui driver, vedere la sezione [Versione e installazione supportate](#supported-versions-and-installation).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="4a0b5-173">No</span><span class="sxs-lookup"><span data-stu-id="4a0b5-173">No</span></span> |
| <span data-ttu-id="4a0b5-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="4a0b5-174">connectionString</span></span> | <span data-ttu-id="4a0b5-175">Specificare l'istanza di Oracle Database toohello tooconnect necessarie informazioni per la proprietà connectionString hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-175">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="4a0b5-176">Sì</span><span class="sxs-lookup"><span data-stu-id="4a0b5-176">Yes</span></span> |
| <span data-ttu-id="4a0b5-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="4a0b5-177">gatewayName</span></span> | <span data-ttu-id="4a0b5-178">Nome del gateway hello che viene utilizzato tooconnect toohello server Oracle locale</span><span class="sxs-lookup"><span data-stu-id="4a0b5-178">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="4a0b5-179">Sì</span><span class="sxs-lookup"><span data-stu-id="4a0b5-179">Yes</span></span> |

<span data-ttu-id="4a0b5-180">**Esempio: mediante il driver Microsoft:**</span><span class="sxs-lookup"><span data-stu-id="4a0b5-180">**Example: using Microsoft driver:**</span></span>
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

<span data-ttu-id="4a0b5-181">**Esempio: mediante il driver ODP**</span><span class="sxs-lookup"><span data-stu-id="4a0b5-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="4a0b5-182">Fare riferimento troppo[questo sito](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) per hello formati consentito.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-182">Refer too[this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for hello allowed formats.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="4a0b5-183">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="4a0b5-183">Dataset properties</span></span>
<span data-ttu-id="4a0b5-184">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-184">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="4a0b5-185">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati (Oracle, BLOB di Azure, tabelle di Azure e così via).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="4a0b5-186">sezione typeProperties Hello è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-186">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="4a0b5-187">sezione di typeProperties Hello per hello set di dati di tipo OracleTable ha hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a0b5-187">hello typeProperties section for hello dataset of type OracleTable has hello following properties:</span></span>

| <span data-ttu-id="4a0b5-188">Proprietà</span><span class="sxs-lookup"><span data-stu-id="4a0b5-188">Property</span></span> | <span data-ttu-id="4a0b5-189">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a0b5-189">Description</span></span> | <span data-ttu-id="4a0b5-190">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a0b5-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a0b5-191">tableName</span><span class="sxs-lookup"><span data-stu-id="4a0b5-191">tableName</span></span> |<span data-ttu-id="4a0b5-192">Nome della tabella hello nel Database Oracle per il servizio collegato di hello hello fa riferimento a.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-192">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="4a0b5-193">No, se **oracleReaderQuery** di **OracleSource** è specificato</span><span class="sxs-lookup"><span data-stu-id="4a0b5-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="4a0b5-194">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="4a0b5-194">Copy activity properties</span></span>
<span data-ttu-id="4a0b5-195">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-195">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4a0b5-196">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="4a0b5-197">Hello attività di copia accetta un solo input e produce un solo output.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-197">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="4a0b5-198">Mentre le proprietà disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-198">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="4a0b5-199">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-199">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="4a0b5-200">OracleSource</span><span class="sxs-lookup"><span data-stu-id="4a0b5-200">OracleSource</span></span>
<span data-ttu-id="4a0b5-201">Nell'attività di copia, l'origine hello è di tipo **OracleSource** hello le proprietà seguenti sono disponibile in **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="4a0b5-201">In Copy activity, when hello source is of type **OracleSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="4a0b5-202">Proprietà</span><span class="sxs-lookup"><span data-stu-id="4a0b5-202">Property</span></span> | <span data-ttu-id="4a0b5-203">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a0b5-203">Description</span></span> | <span data-ttu-id="4a0b5-204">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="4a0b5-204">Allowed values</span></span> | <span data-ttu-id="4a0b5-205">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a0b5-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4a0b5-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="4a0b5-206">oracleReaderQuery</span></span> |<span data-ttu-id="4a0b5-207">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-207">Use hello custom query tooread data.</span></span> |<span data-ttu-id="4a0b5-208">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-208">SQL query string.</span></span> <span data-ttu-id="4a0b5-209">Ad esempio: selezionare * da MyTable</span><span class="sxs-lookup"><span data-stu-id="4a0b5-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="4a0b5-210">Se non specificato, hello istruzione SQL eseguita: selezionare * from MyTable</span><span class="sxs-lookup"><span data-stu-id="4a0b5-210">If not specified, hello SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="4a0b5-211">No (se **tableName** di **set di dati** è specificato)</span><span class="sxs-lookup"><span data-stu-id="4a0b5-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="4a0b5-212">OracleSink</span><span class="sxs-lookup"><span data-stu-id="4a0b5-212">OracleSink</span></span>
<span data-ttu-id="4a0b5-213">**OracleSink** supporta hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a0b5-213">**OracleSink** supports hello following properties:</span></span>

| <span data-ttu-id="4a0b5-214">Proprietà</span><span class="sxs-lookup"><span data-stu-id="4a0b5-214">Property</span></span> | <span data-ttu-id="4a0b5-215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a0b5-215">Description</span></span> | <span data-ttu-id="4a0b5-216">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="4a0b5-216">Allowed values</span></span> | <span data-ttu-id="4a0b5-217">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a0b5-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4a0b5-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="4a0b5-218">writeBatchTimeout</span></span> |<span data-ttu-id="4a0b5-219">Tempo di attesa per hello batch insert operazione toocomplete prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-219">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="4a0b5-220">Intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="4a0b5-220">timespan</span></span><br/><br/> <span data-ttu-id="4a0b5-221">Ad esempio: "00:30:00" (30 minuti).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="4a0b5-222">No</span><span class="sxs-lookup"><span data-stu-id="4a0b5-222">No</span></span> |
| <span data-ttu-id="4a0b5-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="4a0b5-223">writeBatchSize</span></span> |<span data-ttu-id="4a0b5-224">Inserisce dati in una tabella SQL hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-224">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="4a0b5-225">Numero intero (numero di righe)</span><span class="sxs-lookup"><span data-stu-id="4a0b5-225">Integer (number of rows)</span></span> |<span data-ttu-id="4a0b5-226">No (valore predefinito: 100)</span><span class="sxs-lookup"><span data-stu-id="4a0b5-226">No (default: 100)</span></span> |
| <span data-ttu-id="4a0b5-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="4a0b5-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="4a0b5-228">Specificare una query per attività di copia tooexecute modo che la pulitura dei dati di una sezione specifica.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-228">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="4a0b5-229">Istruzione di query.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-229">A query statement.</span></span> |<span data-ttu-id="4a0b5-230">No</span><span class="sxs-lookup"><span data-stu-id="4a0b5-230">No</span></span> |
| <span data-ttu-id="4a0b5-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="4a0b5-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="4a0b5-232">Specificare il nome di colonna per attività di copia toofill con identificatore di sezione generati automaticamente, che è usato tooclean dei dati di una sezione specifica quando eseguire di nuovo.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-232">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="4a0b5-233">Nome di colonna di una colonna con tipo di dati binario (32).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="4a0b5-234">No</span><span class="sxs-lookup"><span data-stu-id="4a0b5-234">No</span></span> |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a><span data-ttu-id="4a0b5-235">Esempi JSON per la copia dei dati tooand da database Oracle</span><span class="sxs-lookup"><span data-stu-id="4a0b5-235">JSON examples for copying data tooand from Oracle database</span></span>
<span data-ttu-id="4a0b5-236">esempio Hello fornisce definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-236">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="4a0b5-237">Vengono visualizzate come dati toocopy da tooan Oracle database da e verso l'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-237">They show how toocopy data from/tooan Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="4a0b5-238">Tuttavia, i dati possono essere copiati tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-238">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a><span data-ttu-id="4a0b5-239">Esempio: Copiare i dati da Oracle tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="4a0b5-239">Example: Copy data from Oracle tooAzure Blob</span></span>

<span data-ttu-id="4a0b5-240">esempio Hello è hello entità factory di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a0b5-240">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="4a0b5-241">Un servizio collegato di tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="4a0b5-242">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="4a0b5-243">Un [set di dati](data-factory-create-datasets.md) di input di tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="4a0b5-244">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="4a0b5-245">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) come origine e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) come sink.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="4a0b5-246">esempio Hello copia dati da una tabella in un blob di tooa database Oracle locale ogni ora.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-246">hello sample copies data from a table in an on-premises Oracle database tooa blob hourly.</span></span> <span data-ttu-id="4a0b5-247">Per ulteriori informazioni su varie proprietà utilizzate nell'esempio hello, vedere la documentazione nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-247">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="4a0b5-248">**Servizio collegato Oracle:**</span><span class="sxs-lookup"><span data-stu-id="4a0b5-248">**Oracle linked service:**</span></span>

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

<span data-ttu-id="4a0b5-249">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="4a0b5-249">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="4a0b5-250">**Set di dati di input Oracle:**</span><span class="sxs-lookup"><span data-stu-id="4a0b5-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="4a0b5-251">esempio Hello presuppone di aver creato una tabella "MyTable" in Oracle e contiene una colonna denominata "timestampcolumn" per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-251">hello sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="4a0b5-252">L'impostazione "external": "true" informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-252">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="4a0b5-253">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="4a0b5-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="4a0b5-254">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-254">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="4a0b5-255">Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-255">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="4a0b5-256">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-256">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="4a0b5-257">**Pipeline con attività di copia:**</span><span class="sxs-lookup"><span data-stu-id="4a0b5-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="4a0b5-258">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e si svolge ogni ora toorun pianificato.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-258">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="4a0b5-259">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**OracleSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-259">In hello pipeline JSON definition, hello **source** type is set too**OracleSource** and **sink** type is set too**BlobSink**.</span></span>  <span data-ttu-id="4a0b5-260">query SQL Hello specificata con **oracleReaderQuery** proprietà consente di selezionare dati hello hello oltre toocopy ora.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-260">hello SQL query specified with **oracleReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-toooracle"></a><span data-ttu-id="4a0b5-261">Esempio: Copiare i dati da Blob di Azure tooOracle</span><span class="sxs-lookup"><span data-stu-id="4a0b5-261">Example: Copy data from Azure Blob tooOracle</span></span>
<span data-ttu-id="4a0b5-262">Questo esempio viene illustrato come toocopy dati da un tooan di archiviazione Blob di Azure in locale il database Oracle.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-262">This sample shows how toocopy data from an Azure Blob Storage tooan on-premises Oracle database.</span></span> <span data-ttu-id="4a0b5-263">Tuttavia, i dati possono essere copiati **direttamente** da una delle origini di hello indicate [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-263">However, data can be copied **directly** from any of hello sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="4a0b5-264">esempio Hello è hello entità factory di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a0b5-264">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="4a0b5-265">Un servizio collegato di tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="4a0b5-266">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="4a0b5-267">Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="4a0b5-268">Un [set di dati](data-factory-create-datasets.md) di output di tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="4a0b5-269">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) come origine e [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) come sink.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="4a0b5-270">esempio Hello copia dati da una tabella tooa blob in un database Oracle locale ogni ora.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-270">hello sample copies data from a blob tooa table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="4a0b5-271">Per ulteriori informazioni su varie proprietà utilizzate nell'esempio hello, vedere la documentazione nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-271">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="4a0b5-272">**Servizio collegato Oracle:**</span><span class="sxs-lookup"><span data-stu-id="4a0b5-272">**Oracle linked service:**</span></span>
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

<span data-ttu-id="4a0b5-273">**Servizio collegato di archiviazione BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="4a0b5-273">**Azure Blob storage linked service:**</span></span>
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

<span data-ttu-id="4a0b5-274">**Set di dati di input del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="4a0b5-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="4a0b5-275">I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="4a0b5-276">Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-276">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="4a0b5-277">percorso della cartella Hello utilizza year, month e parte del giorno dell'ora di inizio hello e nome del file utilizza parte ora hello hello ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-277">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="4a0b5-278">"external": "true" impostazione informa il servizio di Data Factory hello che questa tabella è data factory di toohello esterni e non viene generata da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-278">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="4a0b5-279">**Set di dati di output Oracle:**</span><span class="sxs-lookup"><span data-stu-id="4a0b5-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="4a0b5-280">esempio Hello presuppone che aver creato una tabella "MyTable" in Oracle.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-280">hello sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="4a0b5-281">Creare la tabella hello in Oracle con hello stesso numero di colonne nel modo previsto toocontain di file CSV Blob hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-281">Create hello table in Oracle with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="4a0b5-282">Aggiunta di nuove righe nella tabella toohello ogni ora.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-282">New rows are added toohello table every hour.</span></span>

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

<span data-ttu-id="4a0b5-283">**Pipeline con attività di copia:**</span><span class="sxs-lookup"><span data-stu-id="4a0b5-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="4a0b5-284">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-284">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="4a0b5-285">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**BlobSource** hello e **sink** tipo è stato impostato troppo**OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-285">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and hello **sink** type is set too**OracleSink**.</span></span>  

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


## <a name="troubleshooting-tips"></a><span data-ttu-id="4a0b5-286">Suggerimenti per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="4a0b5-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="4a0b5-287">Problema 1: provider di dati .NET Framework</span><span class="sxs-lookup"><span data-stu-id="4a0b5-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="4a0b5-288">Verrà visualizzata la seguente hello **messaggio di errore**:</span><span class="sxs-lookup"><span data-stu-id="4a0b5-288">You see hello following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="4a0b5-289">**Possibili cause:**</span><span class="sxs-lookup"><span data-stu-id="4a0b5-289">**Possible causes:**</span></span>

1. <span data-ttu-id="4a0b5-290">non è stato installato il Provider di dati .NET Framework per Oracle Hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-290">hello .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="4a0b5-291">Hello Provider di dati .NET Framework per Oracle è stato installato too.NET Framework 2.0 e non viene trovato in cartelle hello .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-291">hello .NET Framework Data Provider for Oracle was installed too.NET Framework 2.0 and is not found in hello .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="4a0b5-292">**Risoluzione/Soluzione alternativa:**</span><span class="sxs-lookup"><span data-stu-id="4a0b5-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="4a0b5-293">Se non è stato installato il Provider .NET per Oracle, hello [installarlo](http://www.oracle.com/technetwork/topics/dotnet/downloads/) e ripetere scenario hello.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-293">If you haven't installed hello .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry hello scenario.</span></span>
2. <span data-ttu-id="4a0b5-294">Se viene visualizzato il messaggio di errore hello anche dopo l'installazione del provider di hello, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a0b5-294">If you get hello error message even after installing hello provider, do hello following steps:</span></span>
   1. <span data-ttu-id="4a0b5-295">Aprire la configurazione macchina di .NET 2.0 dalla cartella hello: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-295">Open machine config of .NET 2.0 from hello folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="4a0b5-296">Cercare **Oracle Data Provider for .NET**, e dovrebbe essere in grado di toofind una voce, come illustrato nel seguente esempio in hello **System. Data** -> **DbProviderFactories**: "<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Provider di dati oracle per .NET</span><span class="sxs-lookup"><span data-stu-id="4a0b5-296">Search for **Oracle Data Provider for .NET**, and you should be able toofind an entry as shown in hello following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="4a0b5-297">"</span><span class="sxs-lookup"><span data-stu-id="4a0b5-297">”</span></span>
3. <span data-ttu-id="4a0b5-298">Copiare il file Machine. config di voce toohello nella seguente cartella v 4.0 hello: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config e modifica hello versione too4.xxx.x.x.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-298">Copy this entry toohello machine.config file in hello following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change hello version too4.xxx.x.x.</span></span>
4. <span data-ttu-id="4a0b5-299">Installare "< percorso di installazione ODP.NET > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll" nella hello global assembly cache (GAC) eseguendo `gacutil /i [provider path]`. # # suggerimenti di risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="4a0b5-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into hello global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="4a0b5-300">Problema 2: formattazione di DateTime</span><span class="sxs-lookup"><span data-stu-id="4a0b5-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="4a0b5-301">Verrà visualizzata la seguente hello **messaggio di errore**:</span><span class="sxs-lookup"><span data-stu-id="4a0b5-301">You see hello following **error message**:</span></span>

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="4a0b5-302">**Risoluzione/Soluzione alternativa:**</span><span class="sxs-lookup"><span data-stu-id="4a0b5-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="4a0b5-303">Stringa di query hello tooadjust potrebbe essere necessario l'attività di copia in base alle modalità di configurazione delle date nel database Oracle, come illustrato nell'esempio hello (tramite la funzione to_date hello) esempio:</span><span class="sxs-lookup"><span data-stu-id="4a0b5-303">You may need tooadjust hello query string in your copy activity based on how dates are configured in your Oracle database, as shown in hello following sample (using hello to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="4a0b5-304">Mapping dei tipi per Oracle</span><span class="sxs-lookup"><span data-stu-id="4a0b5-304">Type mapping for Oracle</span></span>
<span data-ttu-id="4a0b5-305">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio passaggio 2:</span><span class="sxs-lookup"><span data-stu-id="4a0b5-305">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="4a0b5-306">Conversione dal tipo di origine nativa tipi too.NET</span><span class="sxs-lookup"><span data-stu-id="4a0b5-306">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="4a0b5-307">Eseguire la conversione da tipo di sink toonative tipo .NET</span><span class="sxs-lookup"><span data-stu-id="4a0b5-307">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="4a0b5-308">Quando si spostano dati da Oracle, hello seguendo i mapping viene utilizzato dal tipo too.NET tipo di dati Oracle e viceversa.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-308">When moving data from Oracle, hello following mappings are used from Oracle data type too.NET type and vice versa.</span></span>

| <span data-ttu-id="4a0b5-309">Tipo di dati Oracle</span><span class="sxs-lookup"><span data-stu-id="4a0b5-309">Oracle data type</span></span> | <span data-ttu-id="4a0b5-310">Tipo di dati .NET Framework</span><span class="sxs-lookup"><span data-stu-id="4a0b5-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="4a0b5-311">BFILE</span><span class="sxs-lookup"><span data-stu-id="4a0b5-311">BFILE</span></span> |<span data-ttu-id="4a0b5-312">Byte[]</span><span class="sxs-lookup"><span data-stu-id="4a0b5-312">Byte[]</span></span> |
| <span data-ttu-id="4a0b5-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="4a0b5-313">BLOB</span></span> |<span data-ttu-id="4a0b5-314">Byte[]</span><span class="sxs-lookup"><span data-stu-id="4a0b5-314">Byte[]</span></span> |
| <span data-ttu-id="4a0b5-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="4a0b5-315">CHAR</span></span> |<span data-ttu-id="4a0b5-316">String</span><span class="sxs-lookup"><span data-stu-id="4a0b5-316">String</span></span> |
| <span data-ttu-id="4a0b5-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="4a0b5-317">CLOB</span></span> |<span data-ttu-id="4a0b5-318">String</span><span class="sxs-lookup"><span data-stu-id="4a0b5-318">String</span></span> |
| <span data-ttu-id="4a0b5-319">DATE</span><span class="sxs-lookup"><span data-stu-id="4a0b5-319">DATE</span></span> |<span data-ttu-id="4a0b5-320">DateTime</span><span class="sxs-lookup"><span data-stu-id="4a0b5-320">DateTime</span></span> |
| <span data-ttu-id="4a0b5-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="4a0b5-321">FLOAT</span></span> |<span data-ttu-id="4a0b5-322">Decimal, String (se la precisione > 28)</span><span class="sxs-lookup"><span data-stu-id="4a0b5-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="4a0b5-323">INTEGER</span><span class="sxs-lookup"><span data-stu-id="4a0b5-323">INTEGER</span></span> |<span data-ttu-id="4a0b5-324">Decimal, String (se la precisione > 28)</span><span class="sxs-lookup"><span data-stu-id="4a0b5-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="4a0b5-325">INTERVALLO anno tooMONTH</span><span class="sxs-lookup"><span data-stu-id="4a0b5-325">INTERVAL YEAR tooMONTH</span></span> |<span data-ttu-id="4a0b5-326">Int32</span><span class="sxs-lookup"><span data-stu-id="4a0b5-326">Int32</span></span> |
| <span data-ttu-id="4a0b5-327">INTERVALLO giorno tooSECOND</span><span class="sxs-lookup"><span data-stu-id="4a0b5-327">INTERVAL DAY tooSECOND</span></span> |<span data-ttu-id="4a0b5-328">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="4a0b5-328">TimeSpan</span></span> |
| <span data-ttu-id="4a0b5-329">LONG</span><span class="sxs-lookup"><span data-stu-id="4a0b5-329">LONG</span></span> |<span data-ttu-id="4a0b5-330">String</span><span class="sxs-lookup"><span data-stu-id="4a0b5-330">String</span></span> |
| <span data-ttu-id="4a0b5-331">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="4a0b5-331">LONG RAW</span></span> |<span data-ttu-id="4a0b5-332">Byte[]</span><span class="sxs-lookup"><span data-stu-id="4a0b5-332">Byte[]</span></span> |
| <span data-ttu-id="4a0b5-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="4a0b5-333">NCHAR</span></span> |<span data-ttu-id="4a0b5-334">String</span><span class="sxs-lookup"><span data-stu-id="4a0b5-334">String</span></span> |
| <span data-ttu-id="4a0b5-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="4a0b5-335">NCLOB</span></span> |<span data-ttu-id="4a0b5-336">String</span><span class="sxs-lookup"><span data-stu-id="4a0b5-336">String</span></span> |
| <span data-ttu-id="4a0b5-337">NUMBER</span><span class="sxs-lookup"><span data-stu-id="4a0b5-337">NUMBER</span></span> |<span data-ttu-id="4a0b5-338">Decimal, String (se la precisione > 28)</span><span class="sxs-lookup"><span data-stu-id="4a0b5-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="4a0b5-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="4a0b5-339">NVARCHAR2</span></span> |<span data-ttu-id="4a0b5-340">String</span><span class="sxs-lookup"><span data-stu-id="4a0b5-340">String</span></span> |
| <span data-ttu-id="4a0b5-341">RAW</span><span class="sxs-lookup"><span data-stu-id="4a0b5-341">RAW</span></span> |<span data-ttu-id="4a0b5-342">Byte[]</span><span class="sxs-lookup"><span data-stu-id="4a0b5-342">Byte[]</span></span> |
| <span data-ttu-id="4a0b5-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="4a0b5-343">ROWID</span></span> |<span data-ttu-id="4a0b5-344">String</span><span class="sxs-lookup"><span data-stu-id="4a0b5-344">String</span></span> |
| <span data-ttu-id="4a0b5-345">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="4a0b5-345">TIMESTAMP</span></span> |<span data-ttu-id="4a0b5-346">DateTime</span><span class="sxs-lookup"><span data-stu-id="4a0b5-346">DateTime</span></span> |
| <span data-ttu-id="4a0b5-347">TIMESTAMP WITH LOCAL TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="4a0b5-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="4a0b5-348">DateTime</span><span class="sxs-lookup"><span data-stu-id="4a0b5-348">DateTime</span></span> |
| <span data-ttu-id="4a0b5-349">TIMESTAMP WITH TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="4a0b5-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="4a0b5-350">DateTime</span><span class="sxs-lookup"><span data-stu-id="4a0b5-350">DateTime</span></span> |
| <span data-ttu-id="4a0b5-351">UNSIGNED INTEGER</span><span class="sxs-lookup"><span data-stu-id="4a0b5-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="4a0b5-352">NUMBER</span><span class="sxs-lookup"><span data-stu-id="4a0b5-352">Number</span></span> |
| <span data-ttu-id="4a0b5-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="4a0b5-353">VARCHAR2</span></span> |<span data-ttu-id="4a0b5-354">String</span><span class="sxs-lookup"><span data-stu-id="4a0b5-354">String</span></span> |
| <span data-ttu-id="4a0b5-355">XML</span><span class="sxs-lookup"><span data-stu-id="4a0b5-355">XML</span></span> |<span data-ttu-id="4a0b5-356">String</span><span class="sxs-lookup"><span data-stu-id="4a0b5-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="4a0b5-357">Tipo di dati **intervallo anno tooMONTH** e **tooSECOND INTERVAL DAY** non sono supportati quando si utilizza il driver Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-357">Data type **INTERVAL YEAR tooMONTH** and **INTERVAL DAY tooSECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="4a0b5-358">Eseguire il mapping di colonne di origine toosink</span><span class="sxs-lookup"><span data-stu-id="4a0b5-358">Map source toosink columns</span></span>
<span data-ttu-id="4a0b5-359">toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-359">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="4a0b5-360">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="4a0b5-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="4a0b5-361">Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-361">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="4a0b5-362">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="4a0b5-363">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="4a0b5-364">Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-364">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="4a0b5-365">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="4a0b5-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="4a0b5-366">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="4a0b5-366">Performance and Tuning</span></span>
<span data-ttu-id="4a0b5-367">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="4a0b5-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
