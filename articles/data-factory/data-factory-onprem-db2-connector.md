---
title: aaaMove dati da DB2 utilizzando Data Factory di Azure | Documenti Microsoft
description: "Informazioni su come toomove dati da un DB2 locale del database tramite l'attività di copia di Azure Data Factory"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="c232c-103">Spostare dati da DB2 mediante l'attività di copia di Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c232c-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="c232c-104">In questo articolo viene descritto come usare attività di copia dei dati toocopy Data Factory di Azure da un archivio di dati locale tooa database DB2.</span><span class="sxs-lookup"><span data-stu-id="c232c-104">This article describes how you can use Copy Activity in Azure Data Factory toocopy data from an on-premises DB2 database tooa data store.</span></span> <span data-ttu-id="c232c-105">È possibile copiare l'archivio dati tooany elencato come un sink supportato in hello [attività lo spostamento dei dati di Data Factory](data-factory-data-movement-activities.md#supported-data-stores-and-formats) articolo.</span><span class="sxs-lookup"><span data-stu-id="c232c-105">You can copy data tooany store that is listed as a supported sink in hello [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="c232c-106">Questo argomento si basa sull'articolo Data Factory di hello, che viene presentata una panoramica di spostamento dei dati tramite l'attività di copia e l'elenco delle combinazioni di archivio dati hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="c232c-106">This topic builds on hello Data Factory article, which presents an overview of data movement by using Copy Activity and lists hello supported data store combinations.</span></span> 

<span data-ttu-id="c232c-107">Data Factory supporta attualmente solo lo spostamento dei dati da un tooa database DB2 [archivio dati sink supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c232c-107">Data Factory currently supports only moving data from a DB2 database tooa [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="c232c-108">Lo spostamento dei dati da altri dati archivia tooa DB2 database non è supportato.</span><span class="sxs-lookup"><span data-stu-id="c232c-108">Moving data from other data stores tooa DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c232c-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c232c-109">Prerequisites</span></span>
<span data-ttu-id="c232c-110">Data Factory supporta connessione database DB2 locale di tooan utilizzando hello [gateway di gestione dati](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="c232c-110">Data Factory supports connecting tooan on-premises DB2 database by using hello [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="c232c-111">Per istruzioni dettagliate tooset dei dati gateway hello pipeline toomove i dati, vedere hello [spostare i dati da on-premise toocloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="c232c-111">For step-by-step instructions tooset up hello gateway data pipeline toomove your data, see hello [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="c232c-112">Anche se hello DB2 è ospitato in Azure IaaS con macchina virtuale, è necessario un gateway.</span><span class="sxs-lookup"><span data-stu-id="c232c-112">A gateway is required even if hello DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="c232c-113">È possibile installare il gateway hello in hello stessa VM IaaS come archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="c232c-113">You can install hello gateway on hello same IaaS VM as hello data store.</span></span> <span data-ttu-id="c232c-114">Se il gateway di hello possa connettersi toohello database, è possibile installare il gateway di hello in una macchina virtuale diversa.</span><span class="sxs-lookup"><span data-stu-id="c232c-114">If hello gateway can connect toohello database, you can install hello gateway on a different VM.</span></span>

<span data-ttu-id="c232c-115">gateway di gestione dati Hello fornisce un driver DB2 predefinito, pertanto non è necessario toomanually installare un driver toocopy dati da DB2.</span><span class="sxs-lookup"><span data-stu-id="c232c-115">hello data management gateway provides a built-in DB2 driver, so you don't need toomanually install a driver toocopy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="c232c-116">Per suggerimenti sulla risoluzione dei problemi del gateway e connessione, vedere hello [risolvere i problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) articolo.</span><span class="sxs-lookup"><span data-stu-id="c232c-116">For tips on troubleshooting connection and gateway issues, see hello [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="c232c-117">Versioni supportate</span><span class="sxs-lookup"><span data-stu-id="c232c-117">Supported versions</span></span>
<span data-ttu-id="c232c-118">connettore Hello Data Factory DB2 supporta hello seguenti piattaforme IBM DB2 e le versioni con le versioni di gestione di accesso SQL Distributed Relational Database Architecture (DRDA) 9, 10 e 11:</span><span class="sxs-lookup"><span data-stu-id="c232c-118">hello Data Factory DB2 connector supports hello following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="c232c-119">IBM DB2 per z/OS versione 11.1</span><span class="sxs-lookup"><span data-stu-id="c232c-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="c232c-120">IBM DB2 per z/OS versione 10.1</span><span class="sxs-lookup"><span data-stu-id="c232c-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="c232c-121">IBM DB2 per i (AS400) versione 7.2</span><span class="sxs-lookup"><span data-stu-id="c232c-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="c232c-122">IBM DB2 per i (AS400) versione 7.1</span><span class="sxs-lookup"><span data-stu-id="c232c-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="c232c-123">IBM DB2 per Linux, UNIX e Windows (LUW) versione 11</span><span class="sxs-lookup"><span data-stu-id="c232c-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="c232c-124">IBM DB2 per LUW versione 10.5</span><span class="sxs-lookup"><span data-stu-id="c232c-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="c232c-125">IBM DB2 per LUW versione 10.1</span><span class="sxs-lookup"><span data-stu-id="c232c-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="c232c-126">Se si riceve il messaggio di errore hello "hello pacchetto corrispondente tooan SQL istruzione richiesta di esecuzione non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="c232c-126">If you receive hello error message "hello package corresponding tooan SQL statement execution request was not found.</span></span> <span data-ttu-id="c232c-127">SQLSTATE = 51002 SQLCODE = a 805, "hello, infatti, non è viene creato un pacchetto necessario per utente normale hello hello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c232c-127">SQLSTATE=51002 SQLCODE=-805," hello reason is a necessary package is not created for hello normal user on hello OS.</span></span> <span data-ttu-id="c232c-128">tooresolve questo problema, seguire queste istruzioni per il tipo di server DB2:</span><span class="sxs-lookup"><span data-stu-id="c232c-128">tooresolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="c232c-129">DB2 per i (AS400): consentono a un utente di creare la raccolta di hello per utente normale hello prima di eseguire attività di copia.</span><span class="sxs-lookup"><span data-stu-id="c232c-129">DB2 for i (AS400): Let a power user create hello collection for hello normal user before running Copy Activity.</span></span> <span data-ttu-id="c232c-130">raccolta di hello toocreate, utilizzare hello comando:`create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="c232c-130">toocreate hello collection, use hello command: `create collection <username>`</span></span>
> - <span data-ttu-id="c232c-131">DB2 per z/OS o LUW: utilizzare un account con privilegi elevati, un power user o l'amministratore che dispone di autorità di pacchetto e binding, BINDADD, disporre delle autorizzazioni EXECUTE tooPUBLIC - copia di hello toorun una volta.</span><span class="sxs-lookup"><span data-stu-id="c232c-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE tooPUBLIC permissions--toorun hello copy once.</span></span> <span data-ttu-id="c232c-132">pacchetto necessario Hello viene creato automaticamente durante la copia di hello.</span><span class="sxs-lookup"><span data-stu-id="c232c-132">hello necessary package is automatically created during hello copy.</span></span> <span data-ttu-id="c232c-133">In seguito, è possibile passare utente normale toohello indietro per le esecuzioni successive di copia.</span><span class="sxs-lookup"><span data-stu-id="c232c-133">Afterward, you can switch back toohello normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c232c-134">introduttiva</span><span class="sxs-lookup"><span data-stu-id="c232c-134">Getting started</span></span>
<span data-ttu-id="c232c-135">È possibile creare una pipeline con dati toomove di un attività di copia da un archivio di dati DB2 locale tramite diversi strumenti e API:</span><span class="sxs-lookup"><span data-stu-id="c232c-135">You can create a pipeline with a copy activity toomove data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="c232c-136">toocreate modo più semplice di Hello una pipeline è toouse hello Azure Data Factory Copia guidata.</span><span class="sxs-lookup"><span data-stu-id="c232c-136">hello easiest way toocreate a pipeline is toouse hello Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="c232c-137">Per un'esercitazione rapida sulla creazione di una pipeline mediante Copia guidata hello, vedere hello [esercitazione: creare una pipeline mediante Copia guidata hello](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="c232c-137">For a quick walkthrough on creating a pipeline by using hello Copy Wizard, see hello [Tutorial: Create a pipeline by using hello Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="c232c-138">È inoltre possibile utilizzare strumenti toocreate una pipeline, tra cui hello portale di Azure, Visual Studio, Azure PowerShell, un modello Gestione risorse di Azure, hello API .NET e hello API REST.</span><span class="sxs-lookup"><span data-stu-id="c232c-138">You can also use tools toocreate a pipeline, including hello Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, hello .NET API, and hello REST API.</span></span> <span data-ttu-id="c232c-139">Per istruzioni dettagliate toocreate una pipeline con attività di copia, vedere hello [esercitazione attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c232c-139">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="c232c-140">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="c232c-140">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="c232c-141">Creare servizi collegati toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="c232c-141">Create linked services toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="c232c-142">Creare set di dati toorepresent input e output dei dati per l'operazione di copia hello.</span><span class="sxs-lookup"><span data-stu-id="c232c-142">Create datasets toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="c232c-143">Creare una pipeline con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="c232c-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c232c-144">Quando si utilizza Copia guidata, le definizioni di JSON per i servizi di Data Factory collegato hello, hello vengono creati automaticamente set di dati e le entità di pipeline per l'utente.</span><span class="sxs-lookup"><span data-stu-id="c232c-144">When you use hello Copy Wizard, JSON definitions for hello Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="c232c-145">Quando si utilizzano strumenti o le API (ad eccezione di hello API .NET), per definire entità Data Factory di hello, utilizzando il formato JSON hello.</span><span class="sxs-lookup"><span data-stu-id="c232c-145">When you use tools or APIs (except hello .NET API), you define hello Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="c232c-146">Hello [esempio JSON: copiare i dati da DB2 tooAzure nell'archiviazione Blob](#json-example-copy-data-from-db2-to-azure-blob) Mostra le definizioni di JSON hello per hello entità Data Factory che vengono utilizzati toocopy dati da un archivio di dati DB2 locale.</span><span class="sxs-lookup"><span data-stu-id="c232c-146">hello [JSON example: Copy data from DB2 tooAzure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows hello JSON definitions for hello Data Factory entities that are used toocopy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="c232c-147">Hello le sezioni seguenti fornisce dettagli sulle hello proprietà JSON che sono utilizzati toodefine hello Data Factory entità che sono l'archivio dati specifico tooa DB2.</span><span class="sxs-lookup"><span data-stu-id="c232c-147">hello following sections provide details about hello JSON properties that are used toodefine hello Data Factory entities that are specific tooa DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="c232c-148">Proprietà del servizio collegato DB2</span><span class="sxs-lookup"><span data-stu-id="c232c-148">DB2 linked service properties</span></span>
<span data-ttu-id="c232c-149">Hello nella tabella seguente elenca le proprietà JSON hello sono tooa specifico del servizio collegato DB2.</span><span class="sxs-lookup"><span data-stu-id="c232c-149">hello following table lists hello JSON properties that are specific tooa DB2 linked service.</span></span>

| <span data-ttu-id="c232c-150">Proprietà</span><span class="sxs-lookup"><span data-stu-id="c232c-150">Property</span></span> | <span data-ttu-id="c232c-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c232c-151">Description</span></span> | <span data-ttu-id="c232c-152">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c232c-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c232c-153">**type**</span><span class="sxs-lookup"><span data-stu-id="c232c-153">**type**</span></span> |<span data-ttu-id="c232c-154">Questa proprietà deve essere impostata troppo**OnPremisesDB2**.</span><span class="sxs-lookup"><span data-stu-id="c232c-154">This property must be set too**OnPremisesDB2**.</span></span> |<span data-ttu-id="c232c-155">Sì</span><span class="sxs-lookup"><span data-stu-id="c232c-155">Yes</span></span> |
| <span data-ttu-id="c232c-156">**server**</span><span class="sxs-lookup"><span data-stu-id="c232c-156">**server**</span></span> |<span data-ttu-id="c232c-157">nome di Hello del server DB2 hello.</span><span class="sxs-lookup"><span data-stu-id="c232c-157">hello name of hello DB2 server.</span></span> |<span data-ttu-id="c232c-158">Sì</span><span class="sxs-lookup"><span data-stu-id="c232c-158">Yes</span></span> |
| <span data-ttu-id="c232c-159">**database**</span><span class="sxs-lookup"><span data-stu-id="c232c-159">**database**</span></span> |<span data-ttu-id="c232c-160">nome di Hello del database DB2 hello.</span><span class="sxs-lookup"><span data-stu-id="c232c-160">hello name of hello DB2 database.</span></span> |<span data-ttu-id="c232c-161">Sì</span><span class="sxs-lookup"><span data-stu-id="c232c-161">Yes</span></span> |
| <span data-ttu-id="c232c-162">**schema**</span><span class="sxs-lookup"><span data-stu-id="c232c-162">**schema**</span></span> |<span data-ttu-id="c232c-163">nome Hello dello schema di hello in database DB2 hello.</span><span class="sxs-lookup"><span data-stu-id="c232c-163">hello name of hello schema in hello DB2 database.</span></span> <span data-ttu-id="c232c-164">Questa proprietà fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="c232c-164">This property is case-sensitive.</span></span> |<span data-ttu-id="c232c-165">No</span><span class="sxs-lookup"><span data-stu-id="c232c-165">No</span></span> |
| <span data-ttu-id="c232c-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="c232c-166">**authenticationType**</span></span> |<span data-ttu-id="c232c-167">tipo di Hello di autenticazione è il database di DB2 toohello tooconnect utilizzato.</span><span class="sxs-lookup"><span data-stu-id="c232c-167">hello type of authentication that is used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="c232c-168">Hello i valori possibili sono: anonima, base e Windows.</span><span class="sxs-lookup"><span data-stu-id="c232c-168">hello possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="c232c-169">Sì</span><span class="sxs-lookup"><span data-stu-id="c232c-169">Yes</span></span> |
| <span data-ttu-id="c232c-170">**username**</span><span class="sxs-lookup"><span data-stu-id="c232c-170">**username**</span></span> |<span data-ttu-id="c232c-171">nome Hello per account utente di hello se si utilizza l'autenticazione di base o di Windows.</span><span class="sxs-lookup"><span data-stu-id="c232c-171">hello name for hello user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="c232c-172">No</span><span class="sxs-lookup"><span data-stu-id="c232c-172">No</span></span> |
| <span data-ttu-id="c232c-173">**password**</span><span class="sxs-lookup"><span data-stu-id="c232c-173">**password**</span></span> |<span data-ttu-id="c232c-174">password di Hello per account utente di hello.</span><span class="sxs-lookup"><span data-stu-id="c232c-174">hello password for hello user account.</span></span> |<span data-ttu-id="c232c-175">No</span><span class="sxs-lookup"><span data-stu-id="c232c-175">No</span></span> |
| <span data-ttu-id="c232c-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="c232c-176">**gatewayName**</span></span> |<span data-ttu-id="c232c-177">nome Hello del gateway hello hello servizio Data Factory deve usare database di DB2 tooconnect toohello locale.</span><span class="sxs-lookup"><span data-stu-id="c232c-177">hello name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="c232c-178">Sì</span><span class="sxs-lookup"><span data-stu-id="c232c-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="c232c-179">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="c232c-179">Dataset properties</span></span>
<span data-ttu-id="c232c-180">Per un elenco di sezioni hello e proprietà che sono disponibili per la definizione di set di dati, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="c232c-180">For a list of hello sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c232c-181">Le sezioni, ad esempio **struttura**, **disponibilità**, hello e **criteri** per un set di dati JSON, sono simili per tutti i tipi di set di dati (SQL Azure, archiviazione Blob di Azure, tabelle di Azure archiviazione e così via).</span><span class="sxs-lookup"><span data-stu-id="c232c-181">Sections, such as **structure**, **availability**, and hello **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="c232c-182">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="c232c-182">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="c232c-183">Hello **typeProperties** sezione per un set di dati di tipo **RelationalTable**, che include set di dati DB2 hello, ha hello seguenti proprietà:</span><span class="sxs-lookup"><span data-stu-id="c232c-183">hello **typeProperties** section for a dataset of type **RelationalTable**, which includes hello DB2 dataset, has hello following property:</span></span>

| <span data-ttu-id="c232c-184">Proprietà</span><span class="sxs-lookup"><span data-stu-id="c232c-184">Property</span></span> | <span data-ttu-id="c232c-185">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c232c-185">Description</span></span> | <span data-ttu-id="c232c-186">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c232c-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c232c-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="c232c-187">**tableName**</span></span> |<span data-ttu-id="c232c-188">nome Hello della tabella di hello nell'istanza di database DB2 hello che hello servizio collegato fa riferimento a.</span><span class="sxs-lookup"><span data-stu-id="c232c-188">hello name of hello table in hello DB2 database instance that hello linked service refers to.</span></span> <span data-ttu-id="c232c-189">Questa proprietà fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="c232c-189">This property is case-sensitive.</span></span> |<span data-ttu-id="c232c-190">No (se hello **query** proprietà di un'attività di copia di tipo **RelationalSource** è specificato)</span><span class="sxs-lookup"><span data-stu-id="c232c-190">No (if hello **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="c232c-191">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="c232c-191">Copy Activity properties</span></span>
<span data-ttu-id="c232c-192">Per un elenco di sezioni di hello e le proprietà disponibili per la definizione delle attività di copia, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="c232c-192">For a list of hello sections and properties that are available for defining copy activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c232c-193">Per tutti i tipi di attività sono disponibili le proprietà dell'attività di copia, come **name**, **description**, tabella **inputs**, tabella **outputs** e **policy**.</span><span class="sxs-lookup"><span data-stu-id="c232c-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="c232c-194">le proprietà disponibili in hello Hello **typeProperties** sezione dell'attività hello per ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="c232c-194">hello properties that are available in hello **typeProperties** section of hello activity for each activity type.</span></span> <span data-ttu-id="c232c-195">Per attività di copia, la proprietà hello varia a seconda di hello tipi di origini dati e sink.</span><span class="sxs-lookup"><span data-stu-id="c232c-195">For Copy Activity, hello properties vary depending on hello types of data sources and sinks.</span></span>

<span data-ttu-id="c232c-196">Per attività di copia, l'origine hello è di tipo **RelationalSource** (che include DB2), hello le proprietà seguenti sono disponibile in hello **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="c232c-196">For Copy Activity, when hello source is of type **RelationalSource** (which includes DB2), hello following properties are available in hello **typeProperties** section:</span></span>

| <span data-ttu-id="c232c-197">Proprietà</span><span class="sxs-lookup"><span data-stu-id="c232c-197">Property</span></span> | <span data-ttu-id="c232c-198">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c232c-198">Description</span></span> | <span data-ttu-id="c232c-199">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="c232c-199">Allowed values</span></span> | <span data-ttu-id="c232c-200">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="c232c-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c232c-201">**query**</span><span class="sxs-lookup"><span data-stu-id="c232c-201">**query**</span></span> |<span data-ttu-id="c232c-202">Utilizzare i dati di hello tooread query personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="c232c-202">Use hello custom query tooread hello data.</span></span> |<span data-ttu-id="c232c-203">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="c232c-203">SQL query string.</span></span> <span data-ttu-id="c232c-204">Ad esempio: `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="c232c-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="c232c-205">No (se hello **tableName** proprietà di un set di dati è specificato)</span><span class="sxs-lookup"><span data-stu-id="c232c-205">No (if hello **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="c232c-206">I nomi di schemi e tabelle fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="c232c-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="c232c-207">Nell'istruzione di query hello, racchiudere i nomi delle proprietà utilizzando "" (virgolette doppie).</span><span class="sxs-lookup"><span data-stu-id="c232c-207">In hello query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="c232c-208">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c232c-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a><span data-ttu-id="c232c-209">Esempio JSON: copiare i dati da DB2 tooAzure nell'archiviazione Blob</span><span class="sxs-lookup"><span data-stu-id="c232c-209">JSON example: Copy data from DB2 tooAzure Blob storage</span></span>
<span data-ttu-id="c232c-210">In questo esempio vengono fornite le definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando hello [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c232c-210">This example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c232c-211">esempio Hello Mostra come toocopy dati da un DB2 tooBlob archiviazione del database.</span><span class="sxs-lookup"><span data-stu-id="c232c-211">hello example shows you how toocopy data from a DB2 database tooBlob storage.</span></span> <span data-ttu-id="c232c-212">Tuttavia, i dati possono essere copiati troppo[tutti i dati supportati archiviano il tipo di sink](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tramite attività di copia di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c232c-212">However, data can be copied too[any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="c232c-213">esempio Hello è hello entità Data Factory di seguito:</span><span class="sxs-lookup"><span data-stu-id="c232c-213">hello sample has hello following Data Factory entities:</span></span>

- <span data-ttu-id="c232c-214">Un servizio collegato DB2 di tipo [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="c232c-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="c232c-215">Un servizio collegato di archiviazione BLOB di Azure di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="c232c-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="c232c-216">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="c232c-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="c232c-217">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="c232c-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="c232c-218">Oggetto [pipeline](data-factory-create-pipelines.md) con un'attività di copia che utilizza hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) proprietà</span><span class="sxs-lookup"><span data-stu-id="c232c-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="c232c-219">esempio Hello copia dati da un risultato di query in un tooan database DB2 blob di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="c232c-219">hello sample copies data from a query result in a DB2 database tooan Azure blob hourly.</span></span> <span data-ttu-id="c232c-220">le proprietà JSON Hello utilizzati nell'esempio hello descritti nelle sezioni hello che seguono le definizioni di entità hello.</span><span class="sxs-lookup"><span data-stu-id="c232c-220">hello JSON properties that are used in hello sample are described in hello sections that follow hello entity definitions.</span></span>

<span data-ttu-id="c232c-221">Innanzitutto installare e configurare un gateway dati.</span><span class="sxs-lookup"><span data-stu-id="c232c-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="c232c-222">Le istruzioni sono in hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="c232c-222">Instructions are in hello [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="c232c-223">**Servizio collegato DB2**</span><span class="sxs-lookup"><span data-stu-id="c232c-223">**DB2 linked service**</span></span>

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="c232c-224">**Servizio collegato di archiviazione BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="c232c-224">**Azure Blob storage linked service**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="c232c-225">**Set di dati di input DB2**</span><span class="sxs-lookup"><span data-stu-id="c232c-225">**DB2 input dataset**</span></span>

<span data-ttu-id="c232c-226">esempio Hello presuppone che sia stato creato una tabella in DB2 denominata "MyTable" che dispone di una colonna con etichetta "timestamp" per i dati della serie temporale hello.</span><span class="sxs-lookup"><span data-stu-id="c232c-226">hello sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for hello time series data.</span></span>

<span data-ttu-id="c232c-227">Hello **esterno** proprietà è impostata su troppo "true".</span><span class="sxs-lookup"><span data-stu-id="c232c-227">hello **external** property is set too"true."</span></span> <span data-ttu-id="c232c-228">Questa impostazione indica a servizio Data Factory hello di questo set di dati è esterna toohello data factory non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="c232c-228">This setting informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="c232c-229">Si noti che hello **tipo** impostata troppo**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="c232c-229">Notice that hello **type** property is set too**RelationalTable**.</span></span>


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
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

<span data-ttu-id="c232c-230">**Set di dati di output del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="c232c-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="c232c-231">I dati vengono scritti tooa nuovo blob ogni ora per l'impostazione hello **frequenza** proprietà troppo "Ora" e hello **intervallo** too1 di proprietà.</span><span class="sxs-lookup"><span data-stu-id="c232c-231">Data is written tooa new blob every hour by setting hello **frequency** property too"Hour" and hello **interval** property too1.</span></span> <span data-ttu-id="c232c-232">Hello **folderPath** proprietà per il blob hello viene valutato dinamicamente in base ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="c232c-232">hello **folderPath** property for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="c232c-233">percorso della cartella Hello Usa le parti di anno, mese, giorno e ora hello hello ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="c232c-233">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="c232c-234">**Pipeline per attività di copia hello**</span><span class="sxs-lookup"><span data-stu-id="c232c-234">**Pipeline for hello copy activity**</span></span>

<span data-ttu-id="c232c-235">pipeline di Hello contiene un'attività di copia che è configurata toouse specificato set di dati di input e output e che è pianificato toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="c232c-235">hello pipeline contains a copy activity that is configured toouse specified input and output datasets and which is scheduled toorun every hour.</span></span> <span data-ttu-id="c232c-236">Nella definizione JSON per la pipeline di hello hello, hello **origine** tipo è stato impostato troppo**RelationalSource** hello e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c232c-236">In hello JSON definition for hello pipeline, hello **source** type is set too**RelationalSource** and hello **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="c232c-237">query SQL Hello specificata per hello **query** proprietà consente di selezionare dati hello dalla tabella "Orders" hello.</span><span class="sxs-lookup"><span data-stu-id="c232c-237">hello SQL query specified for hello **query** property selects hello data from hello "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a><span data-ttu-id="c232c-238">Mapping dei tipi per DB2</span><span class="sxs-lookup"><span data-stu-id="c232c-238">Type mapping for DB2</span></span>
<span data-ttu-id="c232c-239">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, l'attività di copia esegue le conversioni dal tipo di origine tipo toosink automatica tramite hello approccio in due passaggi:</span><span class="sxs-lookup"><span data-stu-id="c232c-239">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type toosink type by using hello following two-step approach:</span></span>

1. <span data-ttu-id="c232c-240">Convertire un tipo di origine nativa tipo tooa .NET</span><span class="sxs-lookup"><span data-stu-id="c232c-240">Convert from a native source type tooa .NET type</span></span>
2. <span data-ttu-id="c232c-241">Convertire un tipo di sink native tooa tipo .NET</span><span class="sxs-lookup"><span data-stu-id="c232c-241">Convert from a .NET type tooa native sink type</span></span>

<span data-ttu-id="c232c-242">i seguenti mapping Hello vengono utilizzati quando l'attività di copia converte dati hello da un tipo di DB2 tipo tooa .NET:</span><span class="sxs-lookup"><span data-stu-id="c232c-242">hello following mappings are used when Copy Activity converts hello data from a DB2 type tooa .NET type:</span></span>

| <span data-ttu-id="c232c-243">Tipo di database DB2</span><span class="sxs-lookup"><span data-stu-id="c232c-243">DB2 database type</span></span> | <span data-ttu-id="c232c-244">Tipo di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="c232c-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="c232c-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="c232c-245">SmallInt</span></span> |<span data-ttu-id="c232c-246">Int16</span><span class="sxs-lookup"><span data-stu-id="c232c-246">Int16</span></span> |
| <span data-ttu-id="c232c-247">Integer</span><span class="sxs-lookup"><span data-stu-id="c232c-247">Integer</span></span> |<span data-ttu-id="c232c-248">Int32</span><span class="sxs-lookup"><span data-stu-id="c232c-248">Int32</span></span> |
| <span data-ttu-id="c232c-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="c232c-249">BigInt</span></span> |<span data-ttu-id="c232c-250">Int64</span><span class="sxs-lookup"><span data-stu-id="c232c-250">Int64</span></span> |
| <span data-ttu-id="c232c-251">Real</span><span class="sxs-lookup"><span data-stu-id="c232c-251">Real</span></span> |<span data-ttu-id="c232c-252">Single</span><span class="sxs-lookup"><span data-stu-id="c232c-252">Single</span></span> |
| <span data-ttu-id="c232c-253">Double</span><span class="sxs-lookup"><span data-stu-id="c232c-253">Double</span></span> |<span data-ttu-id="c232c-254">Double</span><span class="sxs-lookup"><span data-stu-id="c232c-254">Double</span></span> |
| <span data-ttu-id="c232c-255">Float</span><span class="sxs-lookup"><span data-stu-id="c232c-255">Float</span></span> |<span data-ttu-id="c232c-256">Double</span><span class="sxs-lookup"><span data-stu-id="c232c-256">Double</span></span> |
| <span data-ttu-id="c232c-257">Decimal</span><span class="sxs-lookup"><span data-stu-id="c232c-257">Decimal</span></span> |<span data-ttu-id="c232c-258">Decimal</span><span class="sxs-lookup"><span data-stu-id="c232c-258">Decimal</span></span> |
| <span data-ttu-id="c232c-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="c232c-259">DecimalFloat</span></span> |<span data-ttu-id="c232c-260">Decimal</span><span class="sxs-lookup"><span data-stu-id="c232c-260">Decimal</span></span> |
| <span data-ttu-id="c232c-261">Numeric</span><span class="sxs-lookup"><span data-stu-id="c232c-261">Numeric</span></span> |<span data-ttu-id="c232c-262">Decimal</span><span class="sxs-lookup"><span data-stu-id="c232c-262">Decimal</span></span> |
| <span data-ttu-id="c232c-263">Date</span><span class="sxs-lookup"><span data-stu-id="c232c-263">Date</span></span> |<span data-ttu-id="c232c-264">DateTime</span><span class="sxs-lookup"><span data-stu-id="c232c-264">DateTime</span></span> |
| <span data-ttu-id="c232c-265">Time</span><span class="sxs-lookup"><span data-stu-id="c232c-265">Time</span></span> |<span data-ttu-id="c232c-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c232c-266">TimeSpan</span></span> |
| <span data-ttu-id="c232c-267">Timestamp</span><span class="sxs-lookup"><span data-stu-id="c232c-267">Timestamp</span></span> |<span data-ttu-id="c232c-268">Datetime</span><span class="sxs-lookup"><span data-stu-id="c232c-268">DateTime</span></span> |
| <span data-ttu-id="c232c-269">xml</span><span class="sxs-lookup"><span data-stu-id="c232c-269">Xml</span></span> |<span data-ttu-id="c232c-270">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c232c-270">Byte[]</span></span> |
| <span data-ttu-id="c232c-271">Char</span><span class="sxs-lookup"><span data-stu-id="c232c-271">Char</span></span> |<span data-ttu-id="c232c-272">String</span><span class="sxs-lookup"><span data-stu-id="c232c-272">String</span></span> |
| <span data-ttu-id="c232c-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="c232c-273">VarChar</span></span> |<span data-ttu-id="c232c-274">String</span><span class="sxs-lookup"><span data-stu-id="c232c-274">String</span></span> |
| <span data-ttu-id="c232c-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="c232c-275">LongVarChar</span></span> |<span data-ttu-id="c232c-276">String</span><span class="sxs-lookup"><span data-stu-id="c232c-276">String</span></span> |
| <span data-ttu-id="c232c-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="c232c-277">DB2DynArray</span></span> |<span data-ttu-id="c232c-278">String</span><span class="sxs-lookup"><span data-stu-id="c232c-278">String</span></span> |
| <span data-ttu-id="c232c-279">Binary</span><span class="sxs-lookup"><span data-stu-id="c232c-279">Binary</span></span> |<span data-ttu-id="c232c-280">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c232c-280">Byte[]</span></span> |
| <span data-ttu-id="c232c-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="c232c-281">VarBinary</span></span> |<span data-ttu-id="c232c-282">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c232c-282">Byte[]</span></span> |
| <span data-ttu-id="c232c-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="c232c-283">LongVarBinary</span></span> |<span data-ttu-id="c232c-284">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c232c-284">Byte[]</span></span> |
| <span data-ttu-id="c232c-285">Graphic</span><span class="sxs-lookup"><span data-stu-id="c232c-285">Graphic</span></span> |<span data-ttu-id="c232c-286">String</span><span class="sxs-lookup"><span data-stu-id="c232c-286">String</span></span> |
| <span data-ttu-id="c232c-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="c232c-287">VarGraphic</span></span> |<span data-ttu-id="c232c-288">String</span><span class="sxs-lookup"><span data-stu-id="c232c-288">String</span></span> |
| <span data-ttu-id="c232c-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="c232c-289">LongVarGraphic</span></span> |<span data-ttu-id="c232c-290">String</span><span class="sxs-lookup"><span data-stu-id="c232c-290">String</span></span> |
| <span data-ttu-id="c232c-291">Clob</span><span class="sxs-lookup"><span data-stu-id="c232c-291">Clob</span></span> |<span data-ttu-id="c232c-292">String</span><span class="sxs-lookup"><span data-stu-id="c232c-292">String</span></span> |
| <span data-ttu-id="c232c-293">BLOB</span><span class="sxs-lookup"><span data-stu-id="c232c-293">Blob</span></span> |<span data-ttu-id="c232c-294">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c232c-294">Byte[]</span></span> |
| <span data-ttu-id="c232c-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="c232c-295">DbClob</span></span> |<span data-ttu-id="c232c-296">String</span><span class="sxs-lookup"><span data-stu-id="c232c-296">String</span></span> |
| <span data-ttu-id="c232c-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="c232c-297">SmallInt</span></span> |<span data-ttu-id="c232c-298">Int16</span><span class="sxs-lookup"><span data-stu-id="c232c-298">Int16</span></span> |
| <span data-ttu-id="c232c-299">Integer</span><span class="sxs-lookup"><span data-stu-id="c232c-299">Integer</span></span> |<span data-ttu-id="c232c-300">Int32</span><span class="sxs-lookup"><span data-stu-id="c232c-300">Int32</span></span> |
| <span data-ttu-id="c232c-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="c232c-301">BigInt</span></span> |<span data-ttu-id="c232c-302">Int64</span><span class="sxs-lookup"><span data-stu-id="c232c-302">Int64</span></span> |
| <span data-ttu-id="c232c-303">Real</span><span class="sxs-lookup"><span data-stu-id="c232c-303">Real</span></span> |<span data-ttu-id="c232c-304">Single</span><span class="sxs-lookup"><span data-stu-id="c232c-304">Single</span></span> |
| <span data-ttu-id="c232c-305">Double</span><span class="sxs-lookup"><span data-stu-id="c232c-305">Double</span></span> |<span data-ttu-id="c232c-306">Double</span><span class="sxs-lookup"><span data-stu-id="c232c-306">Double</span></span> |
| <span data-ttu-id="c232c-307">Float</span><span class="sxs-lookup"><span data-stu-id="c232c-307">Float</span></span> |<span data-ttu-id="c232c-308">Double</span><span class="sxs-lookup"><span data-stu-id="c232c-308">Double</span></span> |
| <span data-ttu-id="c232c-309">Decimal</span><span class="sxs-lookup"><span data-stu-id="c232c-309">Decimal</span></span> |<span data-ttu-id="c232c-310">Decimal</span><span class="sxs-lookup"><span data-stu-id="c232c-310">Decimal</span></span> |
| <span data-ttu-id="c232c-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="c232c-311">DecimalFloat</span></span> |<span data-ttu-id="c232c-312">Decimal</span><span class="sxs-lookup"><span data-stu-id="c232c-312">Decimal</span></span> |
| <span data-ttu-id="c232c-313">Numeric</span><span class="sxs-lookup"><span data-stu-id="c232c-313">Numeric</span></span> |<span data-ttu-id="c232c-314">Decimal</span><span class="sxs-lookup"><span data-stu-id="c232c-314">Decimal</span></span> |
| <span data-ttu-id="c232c-315">Date</span><span class="sxs-lookup"><span data-stu-id="c232c-315">Date</span></span> |<span data-ttu-id="c232c-316">DateTime</span><span class="sxs-lookup"><span data-stu-id="c232c-316">DateTime</span></span> |
| <span data-ttu-id="c232c-317">Time</span><span class="sxs-lookup"><span data-stu-id="c232c-317">Time</span></span> |<span data-ttu-id="c232c-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c232c-318">TimeSpan</span></span> |
| <span data-ttu-id="c232c-319">Timestamp</span><span class="sxs-lookup"><span data-stu-id="c232c-319">Timestamp</span></span> |<span data-ttu-id="c232c-320">Datetime</span><span class="sxs-lookup"><span data-stu-id="c232c-320">DateTime</span></span> |
| <span data-ttu-id="c232c-321">xml</span><span class="sxs-lookup"><span data-stu-id="c232c-321">Xml</span></span> |<span data-ttu-id="c232c-322">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c232c-322">Byte[]</span></span> |
| <span data-ttu-id="c232c-323">Char</span><span class="sxs-lookup"><span data-stu-id="c232c-323">Char</span></span> |<span data-ttu-id="c232c-324">String</span><span class="sxs-lookup"><span data-stu-id="c232c-324">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="c232c-325">Eseguire il mapping di colonne di origine toosink</span><span class="sxs-lookup"><span data-stu-id="c232c-325">Map source toosink columns</span></span>
<span data-ttu-id="c232c-326">colonne toomap toocolumns set di dati di origine hello hello sink set di dati, vedere toolearn [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c232c-326">toolearn how toomap columns in hello source dataset toocolumns in hello sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="c232c-327">Letture ripetibili da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="c232c-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="c232c-328">Quando si copiano dati da un archivio dati relazionale, tenere ripetibilità presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="c232c-328">When you copy data from a relational data store, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="c232c-329">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="c232c-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="c232c-330">È inoltre possibile configurare i tentativi di hello **criteri** proprietà per toorerun un set di dati una sezione quando si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="c232c-330">You can also configure hello retry **policy** property for a dataset toorerun a slice when a failure occurs.</span></span> <span data-ttu-id="c232c-331">Assicurarsi che hello stessi dati non vengono letti questione come sezione hello molte volte sia eseguire di nuovo, indipendentemente dalla modalità con cui si esegue nuovamente sezione hello.</span><span class="sxs-lookup"><span data-stu-id="c232c-331">Make sure that hello same data is read no matter how many times hello slice is rerun, and regardless of how you rerun hello slice.</span></span> <span data-ttu-id="c232c-332">Per altre informazioni, vedere [Letture ripetibili da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="c232c-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c232c-333">Prestazioni e ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="c232c-333">Performance and tuning</span></span>
<span data-ttu-id="c232c-334">Informazioni sui fattori che influiscono sulle prestazioni di hello delle attività di copia e le modalità prestazioni toooptimize in hello [ottimizzazione Guida e alle prestazioni di attività di copia](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="c232c-334">Learn about key factors that affect hello performance of Copy Activity and ways toooptimize performance in hello [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
