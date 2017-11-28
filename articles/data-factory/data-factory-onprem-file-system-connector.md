---
title: aaaCopy dati da e verso un file system utilizzando Data Factory di Azure | Documenti Microsoft
description: Informazioni su come toocopy tooand di dati da un sistema di file locale con Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="10940-103">Copiare tooand dati da un file system locale usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="10940-103">Copy data tooand from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="10940-104">Questo articolo spiega come toouse hello attività di copia dei dati di Azure Data Factory toocopy a/da un file system locale.</span><span class="sxs-lookup"><span data-stu-id="10940-104">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data to/from an on-premises file system.</span></span> <span data-ttu-id="10940-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="10940-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="10940-106">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="10940-106">Supported scenarios</span></span>
<span data-ttu-id="10940-107">È possibile copiare dati **da un file system locale** toohello archivi dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="10940-107">You can copy data **from an on-premises file system** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="10940-108">È possibile copiare dati da archivi dati seguenti hello **tooan locale sistema file**:</span><span class="sxs-lookup"><span data-stu-id="10940-108">You can copy data from hello following data stores **tooan on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="10940-109">Attività di copia non elimina i file di origine hello dopo che è la destinazione toohello copiati correttamente.</span><span class="sxs-lookup"><span data-stu-id="10940-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="10940-110">Se è necessario toodelete file di origine hello dopo una copia ha esito positivo, creare un file di hello toodelete di attività personalizzata e utilizzare attività hello nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="10940-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="10940-111">Abilitazione della connettività</span><span class="sxs-lookup"><span data-stu-id="10940-111">Enabling connectivity</span></span>
<span data-ttu-id="10940-112">Data Factory supporta tooand connessione da un file di sistema locale tramite **Gateway di gestione dati**.</span><span class="sxs-lookup"><span data-stu-id="10940-112">Data Factory supports connecting tooand from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="10940-113">Nell'ambiente locale per hello Data Factory servizio tooconnect tooany supportate in locale archivio dati incluso il file system, è necessario installare hello Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="10940-113">You must install hello Data Management Gateway in your on-premises environment for hello Data Factory service tooconnect tooany supported on-premises data store including file system.</span></span> <span data-ttu-id="10940-114">toolearn sul Gateway di gestione dati e per istruzioni dettagliate sulla configurazione di gateway di hello, vedere [spostare dati tra origini locali e cloud hello con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="10940-114">toolearn about Data Management Gateway and for step-by-step instructions on setting up hello gateway, see [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="10940-115">Oltre ai Gateway di gestione dati, nessun altro file binario necessario tooand toocommunicate toobe installato da un file system locale.</span><span class="sxs-lookup"><span data-stu-id="10940-115">Apart from Data Management Gateway, no other binary files need toobe installed toocommunicate tooand from an on-premises file system.</span></span> <span data-ttu-id="10940-116">È necessario installare e utilizzare hello Gateway di gestione dati, anche se hello file system sia in Azure IaaS con macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10940-116">You must install and use hello Data Management Gateway even if hello file system is in Azure IaaS VM.</span></span> <span data-ttu-id="10940-117">Per informazioni dettagliate sul gateway hello, vedere [Gateway di gestione dati](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="10940-117">For detailed information about hello gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="10940-118">installare una condivisione di file di Linux, toouse [Samba](https://www.samba.org/) sul server Linux e installare il Gateway di gestione di dati in un server Windows.</span><span class="sxs-lookup"><span data-stu-id="10940-118">toouse a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="10940-119">L'installazione di un Gateway di gestione dati su un server Linux non è supportata.</span><span class="sxs-lookup"><span data-stu-id="10940-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="10940-120">Introduzione</span><span class="sxs-lookup"><span data-stu-id="10940-120">Getting started</span></span>
<span data-ttu-id="10940-121">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un file system usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="10940-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="10940-122">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="10940-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="10940-123">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="10940-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="10940-124">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="10940-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="10940-125">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="10940-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="10940-126">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="10940-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="10940-127">Creare una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="10940-127">Create a **data factory**.</span></span> <span data-ttu-id="10940-128">Una data factory può contenere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="10940-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="10940-129">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="10940-129">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="10940-130">Ad esempio, se si copiano dati da un file system locale di blob di Azure storage tooan, creerai due servizi collegati toolink il locale file system e data factory tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="10940-130">For example, if you are copying data from an Azure blob storage tooan on-premises file system, you create two linked services toolink your on-premises file system and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="10940-131">Per le proprietà di servizio collegato che sono tooan specifico nel file sistema locale, vedere [servizio proprietà collegate](#linked-service-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="10940-131">For linked service properties that are specific tooan on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="10940-132">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="10940-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="10940-133">Nell'esempio hello indicato nell'ultimo passaggio hello è creare un contenitore di blob hello toospecify set di dati e una cartella che contiene i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="10940-133">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="10940-134">E si crea un altro set di dati toospecify hello cartella e il nome (facoltativo) nel file system.</span><span class="sxs-lookup"><span data-stu-id="10940-134">And, you create another dataset toospecify hello folder and file name (optional) in your file system.</span></span> <span data-ttu-id="10940-135">Per le proprietà di set di dati specifici tooon locale del file system, vedere [proprietà set di dati](#dataset-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="10940-135">For dataset properties that are specific tooon-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="10940-136">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="10940-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="10940-137">Nell'esempio hello indicato in precedenza, si usa BlobSource come un'origine e FileSystemSink come sink per attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="10940-137">In hello example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for hello copy activity.</span></span> <span data-ttu-id="10940-138">Analogamente, se si sta copiando tooAzure di sistema di file locale nell'archiviazione Blob, utilizzare FileSystemSource e BlobSink nell'attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="10940-138">Similarly, if you are copying from on-premises file system tooAzure Blob Storage, you use FileSystemSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="10940-139">Per le proprietà di attività di copia locale tooon specifico del file system, vedere [copiare le proprietà dell'attività](#copy-activity-properties) sezione.</span><span class="sxs-lookup"><span data-stu-id="10940-139">For copy activity properties that are specific tooon-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="10940-140">Per informazioni dettagliate su come toouse un archivio dati come origine o un sink, fare clic sul collegamento di hello nella sezione precedente di hello per l'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="10940-140">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="10940-141">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="10940-141">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="10940-142">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="10940-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="10940-143">Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati i dati in o da un file system, vedere [esempi JSON](#json-examples-for-copying-data-to-and-from-file-system) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="10940-143">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="10940-144">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON dal sistema utilizzati toodefine Data Factory entità toofile specifico:</span><span class="sxs-lookup"><span data-stu-id="10940-144">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific toofile system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="10940-145">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="10940-145">Linked service properties</span></span>
<span data-ttu-id="10940-146">È possibile collegare una locale file system tooan data factory di Azure con hello **Server File locale** servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="10940-146">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="10940-147">Hello nella tabella seguente vengono fornite descrizioni per gli elementi JSON toohello specifico servizio locale di File Server collegato.</span><span class="sxs-lookup"><span data-stu-id="10940-147">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="10940-148">Proprietà</span><span class="sxs-lookup"><span data-stu-id="10940-148">Property</span></span> | <span data-ttu-id="10940-149">Descrizione</span><span class="sxs-lookup"><span data-stu-id="10940-149">Description</span></span> | <span data-ttu-id="10940-150">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="10940-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10940-151">type</span><span class="sxs-lookup"><span data-stu-id="10940-151">type</span></span> |<span data-ttu-id="10940-152">Verificare che la proprietà di tipo hello sia impostata troppo**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="10940-152">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="10940-153">Sì</span><span class="sxs-lookup"><span data-stu-id="10940-153">Yes</span></span> |
| <span data-ttu-id="10940-154">host</span><span class="sxs-lookup"><span data-stu-id="10940-154">host</span></span> |<span data-ttu-id="10940-155">Specifica il percorso radice hello della cartella hello che si desidera toocopy.</span><span class="sxs-lookup"><span data-stu-id="10940-155">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="10940-156">Utilizzare il carattere di escape hello ' \ ' per i caratteri speciali nella stringa hello.</span><span class="sxs-lookup"><span data-stu-id="10940-156">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="10940-157">Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="10940-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="10940-158">Sì</span><span class="sxs-lookup"><span data-stu-id="10940-158">Yes</span></span> |
| <span data-ttu-id="10940-159">userid</span><span class="sxs-lookup"><span data-stu-id="10940-159">userid</span></span> |<span data-ttu-id="10940-160">Specificare ID utente hello con server di accesso toohello hello.</span><span class="sxs-lookup"><span data-stu-id="10940-160">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="10940-161">No (se si sceglie encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="10940-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="10940-162">password</span><span class="sxs-lookup"><span data-stu-id="10940-162">password</span></span> |<span data-ttu-id="10940-163">Specificare la password hello per utente hello (userid).</span><span class="sxs-lookup"><span data-stu-id="10940-163">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="10940-164">No (se si sceglie encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="10940-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="10940-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="10940-165">encryptedCredential</span></span> |<span data-ttu-id="10940-166">Specificare le credenziali crittografato hello che è possibile ottenere eseguendo il cmdlet New-AzureRmDataFactoryEncryptValue hello.</span><span class="sxs-lookup"><span data-stu-id="10940-166">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="10940-167">No (se si sceglie toospecify userid e password in testo normale)</span><span class="sxs-lookup"><span data-stu-id="10940-167">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="10940-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="10940-168">gatewayName</span></span> |<span data-ttu-id="10940-169">Specifica il nome di hello del gateway hello che Data Factory deve usare tooconnect toohello ai file server locali.</span><span class="sxs-lookup"><span data-stu-id="10940-169">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="10940-170">Sì</span><span class="sxs-lookup"><span data-stu-id="10940-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="10940-171">Servizio collegato di esempio e definizioni del set di dati</span><span class="sxs-lookup"><span data-stu-id="10940-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="10940-172">Scenario</span><span class="sxs-lookup"><span data-stu-id="10940-172">Scenario</span></span> | <span data-ttu-id="10940-173">Host nella definizione del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="10940-173">Host in linked service definition</span></span> | <span data-ttu-id="10940-174">folderPath nella definizione del set di dati</span><span class="sxs-lookup"><span data-stu-id="10940-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10940-175">Cartella locale nel computer del gateway di gestione dati: </span><span class="sxs-lookup"><span data-stu-id="10940-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="10940-176">Esempi: D:\\\* o D:\cartella\sottocartella\\*</span><span class="sxs-lookup"><span data-stu-id="10940-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="10940-177">D:\\\\ (per Gateway di gestione dati versione 2.0 e successive)</span><span class="sxs-lookup"><span data-stu-id="10940-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="10940-178">localhost (per le versioni precedenti alla versione 2.0 di Gateway di gestione dati)</span><span class="sxs-lookup"><span data-stu-id="10940-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="10940-179">.\\\\ o cartella\\\\sottocartella (per Gateway di gestione dati 2.0 e versioni successive)</span><span class="sxs-lookup"><span data-stu-id="10940-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="10940-180">D:\\\\ o D:\\\\cartella\\\\sottocartella (per la versione del gateway precedente a 2.0)</span><span class="sxs-lookup"><span data-stu-id="10940-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="10940-181">Cartella condivisa remota: </span><span class="sxs-lookup"><span data-stu-id="10940-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="10940-182">Esempi: \\\\myserver\\share\\\* o \\\\myserver\\share\\cartella\\sottocartella\\*</span><span class="sxs-lookup"><span data-stu-id="10940-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="10940-183">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="10940-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="10940-184">.\\\\ o cartella\\\\sottocartella</span><span class="sxs-lookup"><span data-stu-id="10940-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="10940-185">Esempio: Uso di nome utente e password in testo normale</span><span class="sxs-lookup"><span data-stu-id="10940-185">Example: Using username and password in plain text</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="10940-186">Esempio: Uso di encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="10940-186">Example: Using encryptedcredential</span></span>

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="10940-187">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="10940-187">Dataset properties</span></span>
<span data-ttu-id="10940-188">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo [Creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="10940-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="10940-189">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati.</span><span class="sxs-lookup"><span data-stu-id="10940-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="10940-190">sezione typeProperties Hello è diverso per ogni tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="10940-190">hello typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="10940-191">Fornisce informazioni quali il percorso di hello e il formato dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="10940-191">It provides information such as hello location and format of hello data in hello data store.</span></span> <span data-ttu-id="10940-192">Hello typeProperties sezione hello set di dati di tipo **FileShare** ha hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="10940-192">hello typeProperties section for hello dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="10940-193">Proprietà</span><span class="sxs-lookup"><span data-stu-id="10940-193">Property</span></span> | <span data-ttu-id="10940-194">Descrizione</span><span class="sxs-lookup"><span data-stu-id="10940-194">Description</span></span> | <span data-ttu-id="10940-195">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="10940-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10940-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="10940-196">folderPath</span></span> |<span data-ttu-id="10940-197">Specifica hello sottopercorso toohello cartella.</span><span class="sxs-lookup"><span data-stu-id="10940-197">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="10940-198">Utilizzare il carattere di escape hello ' \' per i caratteri speciali nella stringa hello.</span><span class="sxs-lookup"><span data-stu-id="10940-198">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="10940-199">Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="10940-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="10940-200">È possibile combinare questa proprietà con **partitionBy** toohave i percorsi delle cartelle in base a intervallo iniziale o finale data e ora.</span><span class="sxs-lookup"><span data-stu-id="10940-200">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="10940-201">Sì</span><span class="sxs-lookup"><span data-stu-id="10940-201">Yes</span></span> |
| <span data-ttu-id="10940-202">fileName</span><span class="sxs-lookup"><span data-stu-id="10940-202">fileName</span></span> |<span data-ttu-id="10940-203">Specificare il nome di hello del file hello in hello **folderPath** se si desidera hello tabella toorefer tooa specifici file nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="10940-203">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="10940-204">Se non si specifica alcun valore per questa proprietà, la tabella hello punta tooall file nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="10940-204">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="10940-205">Quando **fileName** non viene specificato per un set di dati di output e **preserveHierarchy** viene omesso in sink di attività, hello nome del file hello generato è hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="10940-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="10940-206">`Data.<Guid>.txt` Esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="10940-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="10940-207">No</span><span class="sxs-lookup"><span data-stu-id="10940-207">No</span></span> |
| <span data-ttu-id="10940-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="10940-208">fileFilter</span></span> |<span data-ttu-id="10940-209">Specificare un filtro toobe tooselect un subset di file in hello folderPath, anziché tutti i file.</span><span class="sxs-lookup"><span data-stu-id="10940-209">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="10940-210">I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).</span><span class="sxs-lookup"><span data-stu-id="10940-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="10940-211">Esempio 1: "fileFilter": "*. log"</span><span class="sxs-lookup"><span data-stu-id="10940-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="10940-212">Esempio 2: "fileFilter": 2014 - 1-?. txt"</span><span class="sxs-lookup"><span data-stu-id="10940-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="10940-213">Si noti che fileFilter è applicabile per un set di dati di input FileShare.</span><span class="sxs-lookup"><span data-stu-id="10940-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="10940-214">No</span><span class="sxs-lookup"><span data-stu-id="10940-214">No</span></span> |
| <span data-ttu-id="10940-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="10940-215">partitionedBy</span></span> |<span data-ttu-id="10940-216">È possibile utilizzare partitionedBy toospecify dinamica folderPath/nome di file per i dati delle serie temporali.</span><span class="sxs-lookup"><span data-stu-id="10940-216">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="10940-217">Un esempio è folderPath con parametri per ogni ora di dati.</span><span class="sxs-lookup"><span data-stu-id="10940-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="10940-218">No</span><span class="sxs-lookup"><span data-stu-id="10940-218">No</span></span> |
| <span data-ttu-id="10940-219">format</span><span class="sxs-lookup"><span data-stu-id="10940-219">format</span></span> | <span data-ttu-id="10940-220">è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="10940-220">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="10940-221">Set hello **tipo** proprietà in formato tooone di questi valori.</span><span class="sxs-lookup"><span data-stu-id="10940-221">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="10940-222">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="10940-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="10940-223">Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="10940-223">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="10940-224">No</span><span class="sxs-lookup"><span data-stu-id="10940-224">No</span></span> |
| <span data-ttu-id="10940-225">compressione</span><span class="sxs-lookup"><span data-stu-id="10940-225">compression</span></span> | <span data-ttu-id="10940-226">Specificare il tipo di hello e livello di compressione per dati hello.</span><span class="sxs-lookup"><span data-stu-id="10940-226">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="10940-227">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="10940-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="10940-228">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="10940-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="10940-229">vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="10940-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="10940-230">No</span><span class="sxs-lookup"><span data-stu-id="10940-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="10940-231">Non è possibile usare fileName e fileFilter contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="10940-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="10940-232">Uso della proprietà partitionedBy</span><span class="sxs-lookup"><span data-stu-id="10940-232">Using partitionedBy property</span></span>
<span data-ttu-id="10940-233">Come indicato nella sezione precedente di hello, è possibile specificare un folderPath dinamico e il nome di dati della serie temporale con hello **partitionedBy** proprietà [funzioni di Data Factory e le variabili di sistema hello](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="10940-233">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="10940-234">toounderstand ulteriori informazioni sul set di dati di serie temporali, la pianificazione e le sezioni, vedere [creazione dei DataSet](data-factory-create-datasets.md), [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md), e [creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="10940-234">toounderstand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="10940-235">Esempio 1.</span><span class="sxs-lookup"><span data-stu-id="10940-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="10940-236">In questo esempio, {Slice} viene sostituito con il valore di hello della variabile sistema hello Data Factory SliceStart nel formato hello (YYYYMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="10940-236">In this example, {Slice} is replaced with hello value of hello Data Factory system variable SliceStart in hello format (YYYYMMDDHH).</span></span> <span data-ttu-id="10940-237">SliceStart fa riferimento all'ora toostart sezione hello.</span><span class="sxs-lookup"><span data-stu-id="10940-237">SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="10940-238">Hello folderPath è diversa per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="10940-238">hello folderPath is different for each slice.</span></span> <span data-ttu-id="10940-239">Ad esempio: wikisampledataout/wikidatagateway/2014100103 o wikisampledataout/wikidatagateway/2014100104.</span><span class="sxs-lookup"><span data-stu-id="10940-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="10940-240">Esempio 2:</span><span class="sxs-lookup"><span data-stu-id="10940-240">Sample 2:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

<span data-ttu-id="10940-241">In questo esempio, anno, mese, giorno e ora della proprietà SliceStart vengono estratti in variabili distinte che utilizzano proprietà folderPath e fileName hello.</span><span class="sxs-lookup"><span data-stu-id="10940-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that hello folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="10940-242">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="10940-242">Copy activity properties</span></span>
<span data-ttu-id="10940-243">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="10940-243">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="10940-244">Proprietà quali nome, descrizione, criteri e set di dati di input e di output sono disponibili per tutti i tipi di attività.</span><span class="sxs-lookup"><span data-stu-id="10940-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="10940-245">Mentre le proprietà disponibili nella hello **typeProperties** sezione dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="10940-245">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span>

<span data-ttu-id="10940-246">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="10940-246">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="10940-247">Se si stanno spostando i dati da un file system locale, impostare il tipo di origine hello nell'attività di copia hello troppo**FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="10940-247">If you are moving data from an on-premises file system, you set hello source type in hello copy activity too**FileSystemSource**.</span></span> <span data-ttu-id="10940-248">Analogamente, se si spostano dati tooan locale del file system, impostare il tipo di sink hello in attività di copia hello troppo**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="10940-248">Similarly, if you are moving data tooan on-premises file system, you set hello sink type in hello copy activity too**FileSystemSink**.</span></span> <span data-ttu-id="10940-249">Questa sezione presenta un elenco delle proprietà supportate da FileSystemSource e FileSystemSink.</span><span class="sxs-lookup"><span data-stu-id="10940-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="10940-250">**FileSystemSource** supporta hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="10940-250">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="10940-251">Proprietà</span><span class="sxs-lookup"><span data-stu-id="10940-251">Property</span></span> | <span data-ttu-id="10940-252">Descrizione</span><span class="sxs-lookup"><span data-stu-id="10940-252">Description</span></span> | <span data-ttu-id="10940-253">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="10940-253">Allowed values</span></span> | <span data-ttu-id="10940-254">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="10940-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="10940-255">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="10940-255">recursive</span></span> |<span data-ttu-id="10940-256">Indica se hello i dati letti in modo ricorsivo dalle sottocartelle di hello o solo dalla cartella specificata hello.</span><span class="sxs-lookup"><span data-stu-id="10940-256">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="10940-257">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="10940-257">True, False (default)</span></span> |<span data-ttu-id="10940-258">No</span><span class="sxs-lookup"><span data-stu-id="10940-258">No</span></span> |

<span data-ttu-id="10940-259">**FileSystemSink** supporta hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="10940-259">**FileSystemSink** supports hello following properties:</span></span>

| <span data-ttu-id="10940-260">Proprietà</span><span class="sxs-lookup"><span data-stu-id="10940-260">Property</span></span> | <span data-ttu-id="10940-261">Descrizione</span><span class="sxs-lookup"><span data-stu-id="10940-261">Description</span></span> | <span data-ttu-id="10940-262">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="10940-262">Allowed values</span></span> | <span data-ttu-id="10940-263">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="10940-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="10940-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="10940-264">copyBehavior</span></span> |<span data-ttu-id="10940-265">Definisce il comportamento di copia hello quando origine hello è BlobSource o file System.</span><span class="sxs-lookup"><span data-stu-id="10940-265">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="10940-266">**PreserveHierarchy:** mantiene la gerarchia di file hello nella cartella di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="10940-266">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="10940-267">Percorso relativo di hello hello origine toohello origine della cartella dei file, ovvero è hello come percorso relativo di hello hello file toohello destinazione della cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="10940-267">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="10940-268">**FlattenHierarchy:** tutti i file dalla cartella di origine hello vengono creati nel primo livello di hello della cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="10940-268">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="10940-269">file di destinazione Hello vengono creati con un nome generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="10940-269">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="10940-270">**Oggetto:** unisce tutti i file dal file tooone cartella di origine hello.</span><span class="sxs-lookup"><span data-stu-id="10940-270">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="10940-271">Se viene specificato nome di nome/blob file hello, nome di file uniti hello è nome specificato hello.</span><span class="sxs-lookup"><span data-stu-id="10940-271">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="10940-272">In caso contrario, verrà usato un nome file generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="10940-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="10940-273">No</span><span class="sxs-lookup"><span data-stu-id="10940-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="10940-274">esempi ricorsivi e copyBehavior</span><span class="sxs-lookup"><span data-stu-id="10940-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="10940-275">In questa sezione viene descritto il comportamento risultante hello dell'operazione di copia hello per diverse combinazioni di valori per le proprietà ricorsiva e copyBehavior hello.</span><span class="sxs-lookup"><span data-stu-id="10940-275">This section describes hello resulting behavior of hello Copy operation for different combinations of values for hello recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="10940-276">valore ricorsivo</span><span class="sxs-lookup"><span data-stu-id="10940-276">recursive value</span></span> | <span data-ttu-id="10940-277">valore di copyBehavior</span><span class="sxs-lookup"><span data-stu-id="10940-277">copyBehavior value</span></span> | <span data-ttu-id="10940-278">Comportamento risultante</span><span class="sxs-lookup"><span data-stu-id="10940-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10940-279">true</span><span class="sxs-lookup"><span data-stu-id="10940-279">true</span></span> |<span data-ttu-id="10940-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="10940-280">preserveHierarchy</span></span> |<span data-ttu-id="10940-281">Per una cartella di origine Cartella1 con hello seguente struttura,</span><span class="sxs-lookup"><span data-stu-id="10940-281">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="10940-282">Cartella1</span><span class="sxs-lookup"><span data-stu-id="10940-282">Folder1</span></span><br/><span data-ttu-id="10940-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="10940-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="10940-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="10940-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="10940-285">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="10940-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="10940-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="10940-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="10940-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="10940-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="10940-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="10940-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="10940-289">cartella di destinazione Hello Cartella1 viene creata con hello stessa struttura come origine di hello:</span><span class="sxs-lookup"><span data-stu-id="10940-289">hello target folder Folder1 is created with hello same structure as hello source:</span></span><br/><br/><span data-ttu-id="10940-290">Cartella1</span><span class="sxs-lookup"><span data-stu-id="10940-290">Folder1</span></span><br/><span data-ttu-id="10940-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="10940-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="10940-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="10940-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="10940-293">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="10940-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="10940-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="10940-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="10940-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="10940-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="10940-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="10940-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="10940-297">true</span><span class="sxs-lookup"><span data-stu-id="10940-297">true</span></span> |<span data-ttu-id="10940-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="10940-298">flattenHierarchy</span></span> |<span data-ttu-id="10940-299">Per una cartella di origine Cartella1 con hello seguente struttura,</span><span class="sxs-lookup"><span data-stu-id="10940-299">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="10940-300">Cartella1</span><span class="sxs-lookup"><span data-stu-id="10940-300">Folder1</span></span><br/><span data-ttu-id="10940-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="10940-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="10940-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="10940-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="10940-303">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="10940-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="10940-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="10940-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="10940-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="10940-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="10940-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="10940-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="10940-307">destinazione Hello Cartella1 viene creata con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="10940-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="10940-308">Cartella1</span><span class="sxs-lookup"><span data-stu-id="10940-308">Folder1</span></span><br/><span data-ttu-id="10940-309">&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1</span><span class="sxs-lookup"><span data-stu-id="10940-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="10940-310">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File2</span><span class="sxs-lookup"><span data-stu-id="10940-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="10940-311">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File3</span><span class="sxs-lookup"><span data-stu-id="10940-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="10940-312">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File4</span><span class="sxs-lookup"><span data-stu-id="10940-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="10940-313">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File5</span><span class="sxs-lookup"><span data-stu-id="10940-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="10940-314">true</span><span class="sxs-lookup"><span data-stu-id="10940-314">true</span></span> |<span data-ttu-id="10940-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="10940-315">mergeFiles</span></span> |<span data-ttu-id="10940-316">Per una cartella di origine Cartella1 con hello seguente struttura,</span><span class="sxs-lookup"><span data-stu-id="10940-316">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="10940-317">Cartella1</span><span class="sxs-lookup"><span data-stu-id="10940-317">Folder1</span></span><br/><span data-ttu-id="10940-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="10940-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="10940-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="10940-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="10940-320">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="10940-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="10940-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="10940-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="10940-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="10940-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="10940-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="10940-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="10940-324">destinazione Hello Cartella1 viene creata con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="10940-324">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="10940-325">Cartella1</span><span class="sxs-lookup"><span data-stu-id="10940-325">Folder1</span></span><br/><span data-ttu-id="10940-326">&nbsp;&nbsp;&nbsp;&nbsp;Il contenuto di File1 + File2 + File3 + File4 + File 5 viene unito in un file con nome generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="10940-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="10940-327">false</span><span class="sxs-lookup"><span data-stu-id="10940-327">false</span></span> |<span data-ttu-id="10940-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="10940-328">preserveHierarchy</span></span> |<span data-ttu-id="10940-329">Per una cartella di origine Cartella1 con hello seguente struttura,</span><span class="sxs-lookup"><span data-stu-id="10940-329">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="10940-330">Cartella1</span><span class="sxs-lookup"><span data-stu-id="10940-330">Folder1</span></span><br/><span data-ttu-id="10940-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="10940-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="10940-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="10940-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="10940-333">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="10940-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="10940-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="10940-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="10940-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="10940-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="10940-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="10940-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="10940-337">cartella di destinazione Hello Cartella1 viene creata con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="10940-337">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="10940-338">Cartella1</span><span class="sxs-lookup"><span data-stu-id="10940-338">Folder1</span></span><br/><span data-ttu-id="10940-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="10940-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="10940-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="10940-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="10940-341">La sottocartella1 con File3, File4 e File5 non viene considerata.</span><span class="sxs-lookup"><span data-stu-id="10940-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="10940-342">false</span><span class="sxs-lookup"><span data-stu-id="10940-342">false</span></span> |<span data-ttu-id="10940-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="10940-343">flattenHierarchy</span></span> |<span data-ttu-id="10940-344">Per una cartella di origine Cartella1 con hello seguente struttura,</span><span class="sxs-lookup"><span data-stu-id="10940-344">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="10940-345">Cartella1</span><span class="sxs-lookup"><span data-stu-id="10940-345">Folder1</span></span><br/><span data-ttu-id="10940-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="10940-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="10940-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="10940-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="10940-348">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="10940-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="10940-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="10940-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="10940-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="10940-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="10940-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="10940-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="10940-352">cartella di destinazione Hello Cartella1 viene creata con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="10940-352">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="10940-353">Cartella1</span><span class="sxs-lookup"><span data-stu-id="10940-353">Folder1</span></span><br/><span data-ttu-id="10940-354">&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1</span><span class="sxs-lookup"><span data-stu-id="10940-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="10940-355">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File2</span><span class="sxs-lookup"><span data-stu-id="10940-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="10940-356">La sottocartella1 con File3, File4 e File5 non viene considerata.</span><span class="sxs-lookup"><span data-stu-id="10940-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="10940-357">false</span><span class="sxs-lookup"><span data-stu-id="10940-357">false</span></span> |<span data-ttu-id="10940-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="10940-358">mergeFiles</span></span> |<span data-ttu-id="10940-359">Per una cartella di origine Cartella1 con hello seguente struttura,</span><span class="sxs-lookup"><span data-stu-id="10940-359">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="10940-360">Cartella1</span><span class="sxs-lookup"><span data-stu-id="10940-360">Folder1</span></span><br/><span data-ttu-id="10940-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="10940-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="10940-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="10940-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="10940-363">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="10940-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="10940-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="10940-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="10940-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="10940-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="10940-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="10940-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="10940-367">cartella di destinazione Hello Cartella1 viene creata con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="10940-367">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="10940-368">Cartella1</span><span class="sxs-lookup"><span data-stu-id="10940-368">Folder1</span></span><br/><span data-ttu-id="10940-369">&nbsp;&nbsp;&nbsp;&nbsp;Il contenuto di File1 + File2 viene unito in un file con un nome file generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="10940-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="10940-370">&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1</span><span class="sxs-lookup"><span data-stu-id="10940-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="10940-371">La sottocartella1 con File3, File4 e File5 non viene considerata.</span><span class="sxs-lookup"><span data-stu-id="10940-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="10940-372">Formati di file e di compressione supportati</span><span class="sxs-lookup"><span data-stu-id="10940-372">Supported file and compression formats</span></span>
<span data-ttu-id="10940-373">Per i dettagli, vedere l'articolo relativo ai [file e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="10940-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a><span data-ttu-id="10940-374">Esempi JSON per la copia dei dati tooand dal file system</span><span class="sxs-lookup"><span data-stu-id="10940-374">JSON examples for copying data tooand from file system</span></span>
<span data-ttu-id="10940-375">Negli esempi seguenti Hello forniscono definizioni JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando hello [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="10940-375">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="10940-376">Vengono visualizzate come toocopy tooand di dati da un file system in locale e l'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="10940-376">They show how toocopy data tooand from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="10940-377">Tuttavia, è possibile copiare dati *direttamente* da qualsiasi hello origini tooany di sink hello elencati in [origini e sink supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tramite attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="10940-377">However, you can copy data *directly* from any of hello sources tooany of hello sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a><span data-ttu-id="10940-378">Esempio: Copiare i dati da un tooAzure di sistema di file locale nell'archiviazione Blob</span><span class="sxs-lookup"><span data-stu-id="10940-378">Example: Copy data from an on-premises file system tooAzure Blob storage</span></span>
<span data-ttu-id="10940-379">Questo esempio viene illustrato come dati toocopy tooAzure di sistema un file locale nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="10940-379">This sample shows how toocopy data from an on-premises file system tooAzure Blob storage.</span></span> <span data-ttu-id="10940-380">esempio Hello è hello entità Data Factory di seguito:</span><span class="sxs-lookup"><span data-stu-id="10940-380">hello sample has hello following Data Factory entities:</span></span>

* <span data-ttu-id="10940-381">Un servizio collegato di tipo [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="10940-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="10940-382">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="10940-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="10940-383">Un [set di dati](data-factory-create-datasets.md) di input di tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="10940-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="10940-384">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="10940-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="10940-385">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="10940-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="10940-386">Dopo l'esempio Hello copia dati delle serie temporali da tooAzure di sistema un file locale nell'archiviazione Blob ogni ora.</span><span class="sxs-lookup"><span data-stu-id="10940-386">hello following sample copies time-series data from an on-premises file system tooAzure Blob storage every hour.</span></span> <span data-ttu-id="10940-387">le proprietà JSON Hello utilizzati in questi esempi vengono descritte nelle sezioni hello dopo gli esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="10940-387">hello JSON properties that are used in these samples are described in hello sections after hello samples.</span></span>

<span data-ttu-id="10940-388">Come primo passaggio, configurare il Gateway di gestione dati in base alle istruzioni hello [spostare dati tra origini locali e cloud hello con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="10940-388">As a first step, set up Data Management Gateway as per hello instructions in [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="10940-389">**Servizio collegato del file server locale:**</span><span class="sxs-lookup"><span data-stu-id="10940-389">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="10940-390">È consigliabile utilizzare hello **encryptedCredential** proprietà hello invece **userid** e **password** proprietà.</span><span class="sxs-lookup"><span data-stu-id="10940-390">We recommend using hello **encryptedCredential** property instead hello **userid** and **password** properties.</span></span> <span data-ttu-id="10940-391">Per informazioni dettagliate su questo servizio collegato, vedere l'articolo relativo al [servizio collegato del file server](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="10940-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="10940-392">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="10940-392">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="10940-393">**Set di dati di input del file system locale:**</span><span class="sxs-lookup"><span data-stu-id="10940-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="10940-394">I dati vengono prelevati da un nuovo file ogni ora.</span><span class="sxs-lookup"><span data-stu-id="10940-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="10940-395">Hello folderPath e fileName proprietà sono determinate in base a ora di inizio hello della sezione hello.</span><span class="sxs-lookup"><span data-stu-id="10940-395">hello folderPath and fileName properties are determined based on hello start time of hello slice.</span></span>  

<span data-ttu-id="10940-396">Impostazione `"external": "true"` informa Data Factory di set di dati hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="10940-396">Setting `"external": "true"` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
      ]
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

<span data-ttu-id="10940-397">**Set di dati di ouput di Archiviazione BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="10940-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="10940-398">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="10940-398">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="10940-399">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="10940-399">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="10940-400">percorso della cartella Hello Usa le parti di anno, mese, giorno e ora hello hello ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="10940-400">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="10940-401">**Un'attività di copia in una pipeline con un'origine su file system e un sink BLOB:**</span><span class="sxs-lookup"><span data-stu-id="10940-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="10940-402">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output, senza che sia pianificato toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="10940-402">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="10940-403">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**FileSystemSource**, e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="10940-403">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
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

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a><span data-ttu-id="10940-404">Esempio: Copia i dati dal Database SQL di Azure tooan locale file system</span><span class="sxs-lookup"><span data-stu-id="10940-404">Example: Copy data from Azure SQL Database tooan on-premises file system</span></span>
<span data-ttu-id="10940-405">Hello nel seguente esempio viene illustrato:</span><span class="sxs-lookup"><span data-stu-id="10940-405">hello following sample shows:</span></span>

* <span data-ttu-id="10940-406">Un servizio collegato di tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="10940-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="10940-407">Un servizio collegato di tipo [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="10940-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="10940-408">Un set di dati di input di tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="10940-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="10940-409">Un set di dati di output di tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="10940-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="10940-410">Una pipeline con attività di copia che usa [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) e [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="10940-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="10940-411">esempio Hello copia dati delle serie temporali da un file system locale di SQL Azure tabella tooan ogni ora.</span><span class="sxs-lookup"><span data-stu-id="10940-411">hello sample copies time-series data from an Azure SQL table tooan on-premises file system every hour.</span></span> <span data-ttu-id="10940-412">le proprietà JSON Hello utilizzati in questi esempi sono descritti nelle sezioni dopo gli esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="10940-412">hello JSON properties that are used in these samples are described in sections after hello samples.</span></span>

<span data-ttu-id="10940-413">**Servizio collegato per il database SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="10940-413">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

<span data-ttu-id="10940-414">**Servizio collegato del file server locale:**</span><span class="sxs-lookup"><span data-stu-id="10940-414">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="10940-415">È consigliabile utilizzare hello **encryptedCredential** proprietà anziché hello **userid** e **password** proprietà.</span><span class="sxs-lookup"><span data-stu-id="10940-415">We recommend using hello **encryptedCredential** property instead of using hello **userid** and **password** properties.</span></span> <span data-ttu-id="10940-416">Per informazioni dettagliate su questo servizio collegato, vedere l'articolo relativo al [servizio collegato del file system](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="10940-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="10940-417">**Set di dati di input SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="10940-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="10940-418">esempio Hello presuppone che si crea una tabella "MyTable" in SQL Azure e che contiene una colonna denominata "timestampcolumn" per i dati delle serie temporali.</span><span class="sxs-lookup"><span data-stu-id="10940-418">hello sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="10940-419">Impostazione ``“external”: ”true”`` informa Data Factory di set di dati hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="10940-419">Setting ``“external”: ”true”`` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

<span data-ttu-id="10940-420">**Set di dati di output del file system locale:**</span><span class="sxs-lookup"><span data-stu-id="10940-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="10940-421">Dati viene copiato tooa nuovo file ogni ora.</span><span class="sxs-lookup"><span data-stu-id="10940-421">Data is copied tooa new file every hour.</span></span> <span data-ttu-id="10940-422">folderPath Hello e il nome di blob hello vengono determinate in base all'ora di inizio hello del sezione hello.</span><span class="sxs-lookup"><span data-stu-id="10940-422">hello folderPath and fileName for hello blob are determined based on hello start time of hello slice.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
      ]
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

<span data-ttu-id="10940-423">**Un'attività di copia in una pipeline con un'origine SQL e un sink di file system:**</span><span class="sxs-lookup"><span data-stu-id="10940-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="10940-424">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output, senza che sia pianificato toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="10940-424">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="10940-425">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**SqlSource**, hello e **sink** tipo è stato impostato troppo**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="10940-425">In hello pipeline JSON definition, hello **source** type is set too**SqlSource**, and hello **sink** type is set too**FileSystemSink**.</span></span> <span data-ttu-id="10940-426">query SQL Hello specificato per hello **SqlReaderQuery** proprietà consente di selezionare dati hello hello oltre toocopy ora.</span><span class="sxs-lookup"><span data-stu-id="10940-426">hello SQL query that is specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


<span data-ttu-id="10940-427">È anche possibile mappare le colonne di origine toocolumns di set di dati dal set di dati di sink nella definizione di attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="10940-427">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="10940-428">Per altre informazioni, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="10940-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="10940-429">Prestazioni e ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="10940-429">Performance and tuning</span></span>
 <span data-ttu-id="10940-430">toolearn sulla chiave di fattori che influiscono sulle prestazioni di hello spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize, vedere hello [ottimizzazione Guida e alle prestazioni di attività di copia](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="10940-430">toolearn about key factors that impact hello performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
