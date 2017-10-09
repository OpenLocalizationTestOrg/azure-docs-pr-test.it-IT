---
title: dati aaaMove Cassandra utilizzando Data Factory | Documenti Microsoft
description: Informazioni sui database toomove dati da un Cassandra locali usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="682d3-103">Spostare dati da un database Cassandra locale mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="682d3-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="682d3-104">Questo articolo spiega come toouse hello attività di copia dei dati toomove Data Factory di Azure da un database Cassandra locale.</span><span class="sxs-lookup"><span data-stu-id="682d3-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Cassandra database.</span></span> <span data-ttu-id="682d3-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="682d3-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="682d3-106">È possibile copiare dati da un archivio di dati di on-premise Cassandra dati archivio tooany supportati sink.</span><span class="sxs-lookup"><span data-stu-id="682d3-106">You can copy data from an on-premises Cassandra data store tooany supported sink data store.</span></span> <span data-ttu-id="682d3-107">Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella.</span><span class="sxs-lookup"><span data-stu-id="682d3-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="682d3-108">Data factory di attualmente supporta solo lo spostamento di dati da un Cassandra archiviano tooother archivi di dati, ma non per lo spostamento dei dati da altro archivio dati di Cassandra tooa di archivi di dati.</span><span class="sxs-lookup"><span data-stu-id="682d3-108">Data factory currently supports only moving data from a Cassandra data store tooother data stores, but not for moving data from other data stores tooa Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="682d3-109">Versioni supportate</span><span class="sxs-lookup"><span data-stu-id="682d3-109">Supported versions</span></span>
<span data-ttu-id="682d3-110">connettore Cassandra Hello supporta hello seguenti versioni di Cassandra: 2. x.</span><span class="sxs-lookup"><span data-stu-id="682d3-110">hello Cassandra connector supports hello following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="682d3-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="682d3-111">Prerequisites</span></span>
<span data-ttu-id="682d3-112">Per hello Azure Data Factory servizio toobe tooconnect in grado di tooyour Cassandra database locale, è necessario installare un Gateway di gestione di dati in hello stesso computer che ospita il database hello o tooavoid un computer separato competono per le risorse con hello database.</span><span class="sxs-lookup"><span data-stu-id="682d3-112">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises Cassandra database, you must install a Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="682d3-113">Gateway di gestione dati è un componente che si connette a servizi di toocloud origini dati locali in modo sicuro e gestito.</span><span class="sxs-lookup"><span data-stu-id="682d3-113">Data Management Gateway is a component that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="682d3-114">Leggere l'articolo [Gateway di gestione dati](data-factory-data-management-gateway.md) per i dettagli sul Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="682d3-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="682d3-115">Vedere [spostare i dati da on-premise toocloud](data-factory-move-data-between-onprem-and-cloud.md) per istruzioni dettagliate sulla configurazione di gateway hello una pipeline di dati toomove dati.</span><span class="sxs-lookup"><span data-stu-id="682d3-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="682d3-116">È necessario utilizzare i database di hello gateway tooconnect tooa Cassandra anche se i database di hello è ospitato nel cloud hello, ad esempio, in una macchina virtuale IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="682d3-116">You must use hello gateway tooconnect tooa Cassandra database even if hello database is hosted in hello cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="682d3-117">È possibile avere gateway hello su Y hello stessa macchina virtuale che ospita il database hello oppure in una macchina virtuale separata, purché il gateway hello possono connettersi toohello database.</span><span class="sxs-lookup"><span data-stu-id="682d3-117">Y You can have hello gateway on hello same VM that hosts hello database or on a separate VM as long as hello gateway can connect toohello database.</span></span>  

<span data-ttu-id="682d3-118">Quando si installa il gateway di hello, viene automaticamente installato un database di Microsoft Cassandra ODBC driver utilizzato tooconnect tooCassandra.</span><span class="sxs-lookup"><span data-stu-id="682d3-118">When you install hello gateway, it automatically installs a Microsoft Cassandra ODBC driver used tooconnect tooCassandra database.</span></span> <span data-ttu-id="682d3-119">Pertanto, non è necessario toomanually installare i driver nel computer gateway hello quando si copiano dati da database Cassandra hello.</span><span class="sxs-lookup"><span data-stu-id="682d3-119">Therefore, you don't need toomanually install any driver on hello gateway machine when copying data from hello Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="682d3-120">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="682d3-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="682d3-121">Introduzione</span><span class="sxs-lookup"><span data-stu-id="682d3-121">Getting started</span></span>
<span data-ttu-id="682d3-122">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="682d3-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="682d3-123">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="682d3-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="682d3-124">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="682d3-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="682d3-125">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="682d3-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="682d3-126">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="682d3-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="682d3-127">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="682d3-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="682d3-128">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="682d3-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="682d3-129">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="682d3-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="682d3-130">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="682d3-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="682d3-131">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="682d3-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="682d3-132">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="682d3-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="682d3-133">Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un archivio di dati Cassandra locale, vedere [esempio JSON: copiare i dati da tooAzure Cassandra Blob](#json-example-copy-data-from-cassandra-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="682d3-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra tooAzure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="682d3-134">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che costituiscono toodefine utilizzato Data Factory archivio dati di entità specifico tooa Cassandra:</span><span class="sxs-lookup"><span data-stu-id="682d3-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="682d3-135">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="682d3-135">Linked service properties</span></span>
<span data-ttu-id="682d3-136">Hello nella tabella seguente fornisce una descrizione del servizio specifico tooCassandra collegato gli elementi JSON.</span><span class="sxs-lookup"><span data-stu-id="682d3-136">hello following table provides description for JSON elements specific tooCassandra linked service.</span></span>

| <span data-ttu-id="682d3-137">Proprietà</span><span class="sxs-lookup"><span data-stu-id="682d3-137">Property</span></span> | <span data-ttu-id="682d3-138">Descrizione</span><span class="sxs-lookup"><span data-stu-id="682d3-138">Description</span></span> | <span data-ttu-id="682d3-139">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="682d3-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="682d3-140">type</span><span class="sxs-lookup"><span data-stu-id="682d3-140">type</span></span> |<span data-ttu-id="682d3-141">proprietà di tipo Hello deve essere impostata su: **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="682d3-141">hello type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="682d3-142">Sì</span><span class="sxs-lookup"><span data-stu-id="682d3-142">Yes</span></span> |
| <span data-ttu-id="682d3-143">host</span><span class="sxs-lookup"><span data-stu-id="682d3-143">host</span></span> |<span data-ttu-id="682d3-144">Uno o più indirizzi IP o nomi host di server Cassandra.</span><span class="sxs-lookup"><span data-stu-id="682d3-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="682d3-145">Specificare un elenco delimitato da virgole di indirizzi IP o host nomi tooconnect tooall server contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="682d3-145">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="682d3-146">Sì</span><span class="sxs-lookup"><span data-stu-id="682d3-146">Yes</span></span> |
| <span data-ttu-id="682d3-147">port</span><span class="sxs-lookup"><span data-stu-id="682d3-147">port</span></span> |<span data-ttu-id="682d3-148">la porta TCP che hello server Cassandra Hello utilizza toolisten per le connessioni client.</span><span class="sxs-lookup"><span data-stu-id="682d3-148">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="682d3-149">No, valore predefinito: 9042</span><span class="sxs-lookup"><span data-stu-id="682d3-149">No, default value: 9042</span></span> |
| <span data-ttu-id="682d3-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="682d3-150">authenticationType</span></span> |<span data-ttu-id="682d3-151">Di base o anonima</span><span class="sxs-lookup"><span data-stu-id="682d3-151">Basic, or Anonymous</span></span> |<span data-ttu-id="682d3-152">Sì</span><span class="sxs-lookup"><span data-stu-id="682d3-152">Yes</span></span> |
| <span data-ttu-id="682d3-153">username</span><span class="sxs-lookup"><span data-stu-id="682d3-153">username</span></span> |<span data-ttu-id="682d3-154">Specificare nome utente per l'account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="682d3-154">Specify user name for hello user account.</span></span> |<span data-ttu-id="682d3-155">Sì, se authenticationType impostata tooBasic.</span><span class="sxs-lookup"><span data-stu-id="682d3-155">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="682d3-156">password</span><span class="sxs-lookup"><span data-stu-id="682d3-156">password</span></span> |<span data-ttu-id="682d3-157">Specificare la password per l'account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="682d3-157">Specify password for hello user account.</span></span> |<span data-ttu-id="682d3-158">Sì, se authenticationType impostata tooBasic.</span><span class="sxs-lookup"><span data-stu-id="682d3-158">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="682d3-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="682d3-159">gatewayName</span></span> |<span data-ttu-id="682d3-160">nome Hello del gateway hello tooconnect utilizzati toohello Cassandra database locale.</span><span class="sxs-lookup"><span data-stu-id="682d3-160">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="682d3-161">Sì</span><span class="sxs-lookup"><span data-stu-id="682d3-161">Yes</span></span> |
| <span data-ttu-id="682d3-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="682d3-162">encryptedCredential</span></span> |<span data-ttu-id="682d3-163">Credenziali crittografate dal gateway hello.</span><span class="sxs-lookup"><span data-stu-id="682d3-163">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="682d3-164">No</span><span class="sxs-lookup"><span data-stu-id="682d3-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="682d3-165">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="682d3-165">Dataset properties</span></span>
<span data-ttu-id="682d3-166">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="682d3-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="682d3-167">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="682d3-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="682d3-168">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="682d3-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="682d3-169">sezione Hello typeProperties per set di dati di tipo **CassandraTable** è hello seguenti proprietà</span><span class="sxs-lookup"><span data-stu-id="682d3-169">hello typeProperties section for dataset of type **CassandraTable** has hello following properties</span></span>

| <span data-ttu-id="682d3-170">Proprietà</span><span class="sxs-lookup"><span data-stu-id="682d3-170">Property</span></span> | <span data-ttu-id="682d3-171">Descrizione</span><span class="sxs-lookup"><span data-stu-id="682d3-171">Description</span></span> | <span data-ttu-id="682d3-172">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="682d3-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="682d3-173">keyspace</span><span class="sxs-lookup"><span data-stu-id="682d3-173">keyspace</span></span> |<span data-ttu-id="682d3-174">Nome di schema nel database Cassandra o di spazio delle chiavi hello.</span><span class="sxs-lookup"><span data-stu-id="682d3-174">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="682d3-175">Sì, se **query** per **CassandraSource** non è definito.</span><span class="sxs-lookup"><span data-stu-id="682d3-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="682d3-176">tableName</span><span class="sxs-lookup"><span data-stu-id="682d3-176">tableName</span></span> |<span data-ttu-id="682d3-177">Nome della tabella hello Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="682d3-177">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="682d3-178">Sì, se **query** per **CassandraSource** non è definito.</span><span class="sxs-lookup"><span data-stu-id="682d3-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="682d3-179">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="682d3-179">Copy activity properties</span></span>
<span data-ttu-id="682d3-180">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="682d3-180">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="682d3-181">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="682d3-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="682d3-182">Mentre le proprietà disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="682d3-182">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="682d3-183">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="682d3-183">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="682d3-184">Quando l'origine è di tipo **CassandraSource**, hello le proprietà seguenti sono disponibile nella sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="682d3-184">When source is of type **CassandraSource**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="682d3-185">Proprietà</span><span class="sxs-lookup"><span data-stu-id="682d3-185">Property</span></span> | <span data-ttu-id="682d3-186">Descrizione</span><span class="sxs-lookup"><span data-stu-id="682d3-186">Description</span></span> | <span data-ttu-id="682d3-187">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="682d3-187">Allowed values</span></span> | <span data-ttu-id="682d3-188">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="682d3-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="682d3-189">query</span><span class="sxs-lookup"><span data-stu-id="682d3-189">query</span></span> |<span data-ttu-id="682d3-190">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="682d3-190">Use hello custom query tooread data.</span></span> |<span data-ttu-id="682d3-191">Query SQL-92 o query CQL.</span><span class="sxs-lookup"><span data-stu-id="682d3-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="682d3-192">Vedere il [riferimento a CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="682d3-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="682d3-193">Quando si utilizza una query SQL, specificare **spazio delle chiavi name.table nome** toorepresent hello tabella tooquery.</span><span class="sxs-lookup"><span data-stu-id="682d3-193">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="682d3-194">No (se tableName e keyspace sul set di dati sono definiti).</span><span class="sxs-lookup"><span data-stu-id="682d3-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="682d3-195">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="682d3-195">consistencyLevel</span></span> |<span data-ttu-id="682d3-196">livello di coerenza Hello specifica il numero di repliche deve rispondere tooa richiesta di lettura prima della restituzione dell'applicazione client toohello di dati.</span><span class="sxs-lookup"><span data-stu-id="682d3-196">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="682d3-197">Controlli Cassandra hello specificato numero di repliche per hello toosatisfy dati richiesta di lettura.</span><span class="sxs-lookup"><span data-stu-id="682d3-197">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="682d3-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="682d3-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="682d3-199">Per informazioni dettagliate, vedere [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Configurazione della coerenza dei dati).</span><span class="sxs-lookup"><span data-stu-id="682d3-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="682d3-200">No.</span><span class="sxs-lookup"><span data-stu-id="682d3-200">No.</span></span> <span data-ttu-id="682d3-201">Il valore predefinito è ONE.</span><span class="sxs-lookup"><span data-stu-id="682d3-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a><span data-ttu-id="682d3-202">Esempio JSON: copiare i dati da tooAzure Cassandra Blob</span><span class="sxs-lookup"><span data-stu-id="682d3-202">JSON example: Copy data from Cassandra tooAzure Blob</span></span>
<span data-ttu-id="682d3-203">In questo esempio vengono fornite le definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="682d3-203">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="682d3-204">Viene illustrato come toocopy dati da un Cassandra locale database tooan archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="682d3-204">It shows how toocopy data from an on-premises Cassandra database tooan Azure Blob Storage.</span></span> <span data-ttu-id="682d3-205">Tuttavia, i dati possono essere copiati tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="682d3-205">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="682d3-206">Questo esempio fornisce frammenti di codice JSON.</span><span class="sxs-lookup"><span data-stu-id="682d3-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="682d3-207">Non include istruzioni dettagliate per la creazione di data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="682d3-207">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="682d3-208">Le istruzioni dettagliate sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="682d3-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="682d3-209">esempio Hello è hello entità factory di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="682d3-209">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="682d3-210">Un servizio collegato di tipo [OnPremisesCassandra](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="682d3-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="682d3-211">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="682d3-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="682d3-212">Un [set di dati](data-factory-create-datasets.md) di input di tipo [CassandraTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="682d3-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="682d3-213">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="682d3-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="682d3-214">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [CassandraSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="682d3-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="682d3-215">**Servizio collegato Cassandra:**</span><span class="sxs-lookup"><span data-stu-id="682d3-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="682d3-216">Questo esempio viene utilizzato hello **Cassandra** servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="682d3-216">This example uses hello **Cassandra** linked service.</span></span> <span data-ttu-id="682d3-217">Vedere [servizio collegato Cassandra](#linked-service-properties) sezione per le proprietà di hello è supportato da questo servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="682d3-217">See [Cassandra linked service](#linked-service-properties) section for hello properties supported by this linked service.</span></span>  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="682d3-218">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="682d3-218">**Azure Storage linked service:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

<span data-ttu-id="682d3-219">**Set di dati di input Cassandra:**</span><span class="sxs-lookup"><span data-stu-id="682d3-219">**Cassandra input dataset:**</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="682d3-220">Impostazione **esterno** troppo**true** informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="682d3-220">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="682d3-221">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="682d3-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="682d3-222">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="682d3-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="682d3-223">**Attività di copia in una pipeline con un'origine Cassandra e un sink BLOB:**</span><span class="sxs-lookup"><span data-stu-id="682d3-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="682d3-224">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="682d3-224">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="682d3-225">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**CassandraSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="682d3-225">In hello pipeline JSON definition, hello **source** type is set too**CassandraSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="682d3-226">Vedere [le proprietà del tipo RelationalSource](#copy-activity-properties) per elenco hello delle proprietà supportate da hello RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="682d3-226">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties supported by hello RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="682d3-227">Mapping dei tipi per Cassandra</span><span class="sxs-lookup"><span data-stu-id="682d3-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="682d3-228">Tipo Cassandra</span><span class="sxs-lookup"><span data-stu-id="682d3-228">Cassandra Type</span></span> | <span data-ttu-id="682d3-229">Tipo basato su .Net</span><span class="sxs-lookup"><span data-stu-id="682d3-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="682d3-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="682d3-230">ASCII</span></span> |<span data-ttu-id="682d3-231">String</span><span class="sxs-lookup"><span data-stu-id="682d3-231">String</span></span> |
| <span data-ttu-id="682d3-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="682d3-232">BIGINT</span></span> |<span data-ttu-id="682d3-233">Int64</span><span class="sxs-lookup"><span data-stu-id="682d3-233">Int64</span></span> |
| <span data-ttu-id="682d3-234">BLOB</span><span class="sxs-lookup"><span data-stu-id="682d3-234">BLOB</span></span> |<span data-ttu-id="682d3-235">Byte[]</span><span class="sxs-lookup"><span data-stu-id="682d3-235">Byte[]</span></span> |
| <span data-ttu-id="682d3-236">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="682d3-236">BOOLEAN</span></span> |<span data-ttu-id="682d3-237">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="682d3-237">Boolean</span></span> |
| <span data-ttu-id="682d3-238">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="682d3-238">DECIMAL</span></span> |<span data-ttu-id="682d3-239">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="682d3-239">Decimal</span></span> |
| <span data-ttu-id="682d3-240">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="682d3-240">DOUBLE</span></span> |<span data-ttu-id="682d3-241">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="682d3-241">Double</span></span> |
| <span data-ttu-id="682d3-242">FLOAT</span><span class="sxs-lookup"><span data-stu-id="682d3-242">FLOAT</span></span> |<span data-ttu-id="682d3-243">Single</span><span class="sxs-lookup"><span data-stu-id="682d3-243">Single</span></span> |
| <span data-ttu-id="682d3-244">INET</span><span class="sxs-lookup"><span data-stu-id="682d3-244">INET</span></span> |<span data-ttu-id="682d3-245">String</span><span class="sxs-lookup"><span data-stu-id="682d3-245">String</span></span> |
| <span data-ttu-id="682d3-246">INT</span><span class="sxs-lookup"><span data-stu-id="682d3-246">INT</span></span> |<span data-ttu-id="682d3-247">Int32</span><span class="sxs-lookup"><span data-stu-id="682d3-247">Int32</span></span> |
| <span data-ttu-id="682d3-248">TEXT</span><span class="sxs-lookup"><span data-stu-id="682d3-248">TEXT</span></span> |<span data-ttu-id="682d3-249">String</span><span class="sxs-lookup"><span data-stu-id="682d3-249">String</span></span> |
| <span data-ttu-id="682d3-250">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="682d3-250">TIMESTAMP</span></span> |<span data-ttu-id="682d3-251">DateTime</span><span class="sxs-lookup"><span data-stu-id="682d3-251">DateTime</span></span> |
| <span data-ttu-id="682d3-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="682d3-252">TIMEUUID</span></span> |<span data-ttu-id="682d3-253">Guid</span><span class="sxs-lookup"><span data-stu-id="682d3-253">Guid</span></span> |
| <span data-ttu-id="682d3-254">UUID</span><span class="sxs-lookup"><span data-stu-id="682d3-254">UUID</span></span> |<span data-ttu-id="682d3-255">Guid</span><span class="sxs-lookup"><span data-stu-id="682d3-255">Guid</span></span> |
| <span data-ttu-id="682d3-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="682d3-256">VARCHAR</span></span> |<span data-ttu-id="682d3-257">String</span><span class="sxs-lookup"><span data-stu-id="682d3-257">String</span></span> |
| <span data-ttu-id="682d3-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="682d3-258">VARINT</span></span> |<span data-ttu-id="682d3-259">Decimal</span><span class="sxs-lookup"><span data-stu-id="682d3-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="682d3-260">Per la raccolta di tipi (mappa, set, elenco, e così via), fare riferimento troppo[lavorare con i tipi di raccolta Cassandra utilizzando una tabella virtuale](#work-with-collections-using-virtual-table) sezione.</span><span class="sxs-lookup"><span data-stu-id="682d3-260">For collection types (map, set, list, etc.), refer too[Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="682d3-261">I tipi definiti dall'utente non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="682d3-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="682d3-262">lunghezza Hello delle lunghezze di colonna di dati binari e di colonna stringa non può essere maggiore di 4000.</span><span class="sxs-lookup"><span data-stu-id="682d3-262">hello length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="682d3-263">Uso delle raccolte con una tabella virtuale</span><span class="sxs-lookup"><span data-stu-id="682d3-263">Work with collections using virtual table</span></span>
<span data-ttu-id="682d3-264">Data Factory di Azure Usa un ODBC driver tooconnect tooand copia dati predefinito dal database Cassandra.</span><span class="sxs-lookup"><span data-stu-id="682d3-264">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your Cassandra database.</span></span> <span data-ttu-id="682d3-265">Per i tipi di raccolta inclusi mappa, set e un elenco, il driver hello rinormalizza dati hello in tabelle virtuali corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="682d3-265">For collection types including map, set and list, hello driver renormalizes hello data into corresponding virtual tables.</span></span> <span data-ttu-id="682d3-266">In particolare, se una tabella contiene tutte le colonne della raccolta, il driver hello genera l'errore hello le tabelle virtuali seguenti:</span><span class="sxs-lookup"><span data-stu-id="682d3-266">Specifically, if a table contains any collection columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="682d3-267">Oggetto **tabella di base**, che contiene hello stessi dati di tabella ad eccezione delle colonne insieme hello hello.</span><span class="sxs-lookup"><span data-stu-id="682d3-267">A **base table**, which contains hello same data as hello real table except for hello collection columns.</span></span> <span data-ttu-id="682d3-268">tabella di base Hello utilizza hello stesso nome come tabella reale hello che rappresenta.</span><span class="sxs-lookup"><span data-stu-id="682d3-268">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="682d3-269">Oggetto **tabella virtuale** per ogni colonna della raccolta, che espande dati hello annidato.</span><span class="sxs-lookup"><span data-stu-id="682d3-269">A **virtual table** for each collection column, which expands hello nested data.</span></span> <span data-ttu-id="682d3-270">tabelle virtuali Hello che rappresentano le raccolte vengono denominate usando hello Nome tabella hello reale, un separatore "*vt*" e il nome della colonna hello hello.</span><span class="sxs-lookup"><span data-stu-id="682d3-270">hello virtual tables that represent collections are named using hello name of hello real table, a separator “*vt*” and hello name of hello column.</span></span>

<span data-ttu-id="682d3-271">Tabelle virtuali fare riferimento ai dati toohello nella tabella reale hello, abilitazione hello driver tooaccess hello dati denormalizzati.</span><span class="sxs-lookup"><span data-stu-id="682d3-271">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="682d3-272">Per i dettagli vedere la sezione Esempio.</span><span class="sxs-lookup"><span data-stu-id="682d3-272">See Example section for details.</span></span> <span data-ttu-id="682d3-273">È possibile accedere a contenuto hello di raccolte Cassandra eseguendo una query e join di tabelle virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="682d3-273">You can access hello content of Cassandra collections by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="682d3-274">È possibile utilizzare hello [Copia guidata](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively visualizzazione elenco di tabelle nel database di Cassandra inclusi tabelle virtuali hello hello e visualizzare l'anteprima dati hello all'interno.</span><span class="sxs-lookup"><span data-stu-id="682d3-274">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in Cassandra database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="682d3-275">Inoltre, è possibile costruire una query nella copia guidata hello e convalidare i risultati di hello toosee.</span><span class="sxs-lookup"><span data-stu-id="682d3-275">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="682d3-276">Esempio</span><span class="sxs-lookup"><span data-stu-id="682d3-276">Example</span></span>
<span data-ttu-id="682d3-277">Ad esempio, hello seguente "ExampleTable" è una tabella di database Cassandra che contiene una colonna chiave primaria integer denominate "pk_int", una colonna di testo denominato value, una colonna di elenco, una colonna della mappa e un set di colonne (denominato "StringSet").</span><span class="sxs-lookup"><span data-stu-id="682d3-277">For example, hello following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="682d3-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="682d3-278">pk_int</span></span> | <span data-ttu-id="682d3-279">Valore</span><span class="sxs-lookup"><span data-stu-id="682d3-279">Value</span></span> | <span data-ttu-id="682d3-280">Elenco</span><span class="sxs-lookup"><span data-stu-id="682d3-280">List</span></span> | <span data-ttu-id="682d3-281">Mappa</span><span class="sxs-lookup"><span data-stu-id="682d3-281">Map</span></span> | <span data-ttu-id="682d3-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="682d3-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="682d3-283">1</span><span class="sxs-lookup"><span data-stu-id="682d3-283">1</span></span> |<span data-ttu-id="682d3-284">"valore di esempio 1"</span><span class="sxs-lookup"><span data-stu-id="682d3-284">"sample value 1"</span></span> |<span data-ttu-id="682d3-285">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="682d3-285">["1", "2", "3"]</span></span> |<span data-ttu-id="682d3-286">{"S1": "a", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="682d3-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="682d3-287">{"A", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="682d3-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="682d3-288">3</span><span class="sxs-lookup"><span data-stu-id="682d3-288">3</span></span> |<span data-ttu-id="682d3-289">"valore di esempio 3"</span><span class="sxs-lookup"><span data-stu-id="682d3-289">"sample value 3"</span></span> |<span data-ttu-id="682d3-290">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="682d3-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="682d3-291">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="682d3-291">{"S1": "t"}</span></span> |<span data-ttu-id="682d3-292">{"A", "E"}</span><span class="sxs-lookup"><span data-stu-id="682d3-292">{"A", "E"}</span></span> |

<span data-ttu-id="682d3-293">driver Hello genera più tabelle virtuali toorepresent di questa tabella.</span><span class="sxs-lookup"><span data-stu-id="682d3-293">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="682d3-294">Hello le colonne chiave esterna nelle tabelle virtuali hello fare riferimento alle colonne chiave primaria hello nella tabella reale hello e indicare quali reale tabella hello tabella virtuale in una riga corrisponde a.</span><span class="sxs-lookup"><span data-stu-id="682d3-294">hello foreign key columns in hello virtual tables reference hello primary key columns in hello real table, and indicate which real table row hello virtual table row corresponds to.</span></span>

<span data-ttu-id="682d3-295">la tabella virtuale prima di Hello è denominata "ExampleTable" della tabella di base hello viene visualizzata in hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="682d3-295">hello first virtual table is hello base table named “ExampleTable” is shown in hello following table.</span></span> <span data-ttu-id="682d3-296">tabella di base Hello contiene hello stessi dati della tabella del database originale hello ad eccezione di raccolte di hello, che vengono omessi dalla tabella ed espanso in altre tabelle virtuali.</span><span class="sxs-lookup"><span data-stu-id="682d3-296">hello base table contains hello same data as hello original database table except for hello collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="682d3-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="682d3-297">pk_int</span></span> | <span data-ttu-id="682d3-298">Valore</span><span class="sxs-lookup"><span data-stu-id="682d3-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="682d3-299">1</span><span class="sxs-lookup"><span data-stu-id="682d3-299">1</span></span> |<span data-ttu-id="682d3-300">"valore di esempio 1"</span><span class="sxs-lookup"><span data-stu-id="682d3-300">"sample value 1"</span></span> |
| <span data-ttu-id="682d3-301">3</span><span class="sxs-lookup"><span data-stu-id="682d3-301">3</span></span> |<span data-ttu-id="682d3-302">"valore di esempio 3"</span><span class="sxs-lookup"><span data-stu-id="682d3-302">"sample value 3"</span></span> |

<span data-ttu-id="682d3-303">Hello tabelle seguenti illustrano tabelle virtuali hello che renormalize dati hello dalle colonne di elenco, mappa e StringSet hello.</span><span class="sxs-lookup"><span data-stu-id="682d3-303">hello following tables show hello virtual tables that renormalize hello data from hello List, Map, and StringSet columns.</span></span> <span data-ttu-id="682d3-304">colonne di Hello con nomi che terminano con index"o Key" indicano la posizione di hello dei dati di hello all'interno di elenco originale hello o mappa.</span><span class="sxs-lookup"><span data-stu-id="682d3-304">hello columns with names that end with “_index” or “_key” indicate hello position of hello data within hello original list or map.</span></span> <span data-ttu-id="682d3-305">colonne di Hello con nomi che terminano con value"contengono dati hello espanso raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="682d3-305">hello columns with names that end with “_value” contain hello expanded data from hello collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="682d3-306">Tabella “ExampleTable_vt_List”:</span><span class="sxs-lookup"><span data-stu-id="682d3-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="682d3-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="682d3-307">pk_int</span></span> | <span data-ttu-id="682d3-308">List_index</span><span class="sxs-lookup"><span data-stu-id="682d3-308">List_index</span></span> | <span data-ttu-id="682d3-309">List_value</span><span class="sxs-lookup"><span data-stu-id="682d3-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="682d3-310">1</span><span class="sxs-lookup"><span data-stu-id="682d3-310">1</span></span> |<span data-ttu-id="682d3-311">0</span><span class="sxs-lookup"><span data-stu-id="682d3-311">0</span></span> |<span data-ttu-id="682d3-312">1</span><span class="sxs-lookup"><span data-stu-id="682d3-312">1</span></span> |
| <span data-ttu-id="682d3-313">1</span><span class="sxs-lookup"><span data-stu-id="682d3-313">1</span></span> |<span data-ttu-id="682d3-314">1</span><span class="sxs-lookup"><span data-stu-id="682d3-314">1</span></span> |<span data-ttu-id="682d3-315">2</span><span class="sxs-lookup"><span data-stu-id="682d3-315">2</span></span> |
| <span data-ttu-id="682d3-316">1</span><span class="sxs-lookup"><span data-stu-id="682d3-316">1</span></span> |<span data-ttu-id="682d3-317">2</span><span class="sxs-lookup"><span data-stu-id="682d3-317">2</span></span> |<span data-ttu-id="682d3-318">3</span><span class="sxs-lookup"><span data-stu-id="682d3-318">3</span></span> |
| <span data-ttu-id="682d3-319">3</span><span class="sxs-lookup"><span data-stu-id="682d3-319">3</span></span> |<span data-ttu-id="682d3-320">0</span><span class="sxs-lookup"><span data-stu-id="682d3-320">0</span></span> |<span data-ttu-id="682d3-321">100</span><span class="sxs-lookup"><span data-stu-id="682d3-321">100</span></span> |
| <span data-ttu-id="682d3-322">3</span><span class="sxs-lookup"><span data-stu-id="682d3-322">3</span></span> |<span data-ttu-id="682d3-323">1</span><span class="sxs-lookup"><span data-stu-id="682d3-323">1</span></span> |<span data-ttu-id="682d3-324">101</span><span class="sxs-lookup"><span data-stu-id="682d3-324">101</span></span> |
| <span data-ttu-id="682d3-325">3</span><span class="sxs-lookup"><span data-stu-id="682d3-325">3</span></span> |<span data-ttu-id="682d3-326">2</span><span class="sxs-lookup"><span data-stu-id="682d3-326">2</span></span> |<span data-ttu-id="682d3-327">102</span><span class="sxs-lookup"><span data-stu-id="682d3-327">102</span></span> |
| <span data-ttu-id="682d3-328">3</span><span class="sxs-lookup"><span data-stu-id="682d3-328">3</span></span> |<span data-ttu-id="682d3-329">3</span><span class="sxs-lookup"><span data-stu-id="682d3-329">3</span></span> |<span data-ttu-id="682d3-330">103</span><span class="sxs-lookup"><span data-stu-id="682d3-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="682d3-331">Tabella “ExampleTable_vt_Map”:</span><span class="sxs-lookup"><span data-stu-id="682d3-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="682d3-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="682d3-332">pk_int</span></span> | <span data-ttu-id="682d3-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="682d3-333">Map_key</span></span> | <span data-ttu-id="682d3-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="682d3-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="682d3-335">1</span><span class="sxs-lookup"><span data-stu-id="682d3-335">1</span></span> |<span data-ttu-id="682d3-336">S1</span><span class="sxs-lookup"><span data-stu-id="682d3-336">S1</span></span> |<span data-ttu-id="682d3-337">Una </span><span class="sxs-lookup"><span data-stu-id="682d3-337">A</span></span> |
| <span data-ttu-id="682d3-338">1</span><span class="sxs-lookup"><span data-stu-id="682d3-338">1</span></span> |<span data-ttu-id="682d3-339">S2</span><span class="sxs-lookup"><span data-stu-id="682d3-339">S2</span></span> |<span data-ttu-id="682d3-340">b</span><span class="sxs-lookup"><span data-stu-id="682d3-340">b</span></span> |
| <span data-ttu-id="682d3-341">3</span><span class="sxs-lookup"><span data-stu-id="682d3-341">3</span></span> |<span data-ttu-id="682d3-342">S1</span><span class="sxs-lookup"><span data-stu-id="682d3-342">S1</span></span> |<span data-ttu-id="682d3-343">t</span><span class="sxs-lookup"><span data-stu-id="682d3-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="682d3-344">Tabella “ExampleTable_vt_StringSet”:</span><span class="sxs-lookup"><span data-stu-id="682d3-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="682d3-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="682d3-345">pk_int</span></span> | <span data-ttu-id="682d3-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="682d3-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="682d3-347">1</span><span class="sxs-lookup"><span data-stu-id="682d3-347">1</span></span> |<span data-ttu-id="682d3-348">Una </span><span class="sxs-lookup"><span data-stu-id="682d3-348">A</span></span> |
| <span data-ttu-id="682d3-349">1</span><span class="sxs-lookup"><span data-stu-id="682d3-349">1</span></span> |<span data-ttu-id="682d3-350">b</span><span class="sxs-lookup"><span data-stu-id="682d3-350">B</span></span> |
| <span data-ttu-id="682d3-351">1</span><span class="sxs-lookup"><span data-stu-id="682d3-351">1</span></span> |<span data-ttu-id="682d3-352">C</span><span class="sxs-lookup"><span data-stu-id="682d3-352">C</span></span> |
| <span data-ttu-id="682d3-353">3</span><span class="sxs-lookup"><span data-stu-id="682d3-353">3</span></span> |<span data-ttu-id="682d3-354">Una </span><span class="sxs-lookup"><span data-stu-id="682d3-354">A</span></span> |
| <span data-ttu-id="682d3-355">3</span><span class="sxs-lookup"><span data-stu-id="682d3-355">3</span></span> |<span data-ttu-id="682d3-356">E</span><span class="sxs-lookup"><span data-stu-id="682d3-356">E</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="682d3-357">Eseguire il mapping di colonne di origine toosink</span><span class="sxs-lookup"><span data-stu-id="682d3-357">Map source toosink columns</span></span>
<span data-ttu-id="682d3-358">toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="682d3-358">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="682d3-359">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="682d3-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="682d3-360">Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="682d3-360">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="682d3-361">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="682d3-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="682d3-362">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="682d3-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="682d3-363">Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione.</span><span class="sxs-lookup"><span data-stu-id="682d3-363">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="682d3-364">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="682d3-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="682d3-365">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="682d3-365">Performance and Tuning</span></span>
<span data-ttu-id="682d3-366">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="682d3-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
