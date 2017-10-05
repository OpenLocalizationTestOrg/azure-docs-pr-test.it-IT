---
title: Copiare dati da e in un file system con Azure Data Factory | Microsoft Docs
description: Informazioni su come copiare i dati da e in un file system locale usando Azure Data Factory.
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
ms.openlocfilehash: 52305e54f539de6aba2ba9cc856a09e04d608ded
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="copy-data-to-and-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="bb2f2-103">Copiare dati da e in un file system locale usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="bb2f2-103">Copy data to and from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="bb2f2-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per copiare dati da e in un file system locale.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-104">This article explains how to use the Copy Activity in Azure Data Factory to copy data to/from an on-premises file system.</span></span> <span data-ttu-id="bb2f2-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="bb2f2-106">Scenari supportati</span><span class="sxs-lookup"><span data-stu-id="bb2f2-106">Supported scenarios</span></span>
<span data-ttu-id="bb2f2-107">È possibile copiare dati **da un file system locale** negli archivi dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-107">You can copy data **from an on-premises file system** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="bb2f2-108">È possibile copiare i dati dagli archivi dati seguenti **in un file system locale**:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-108">You can copy data from the following data stores **to an on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="bb2f2-109">L'attività di copia non elimina il file di origine dopo che è stato correttamente copiato nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-109">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="bb2f2-110">Se è necessario eliminare il file di origine dopo una copia con esito positivo, creare un'attività personalizzata per eliminare il file e usare l'attività nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-110">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="bb2f2-111">Abilitazione della connettività</span><span class="sxs-lookup"><span data-stu-id="bb2f2-111">Enabling connectivity</span></span>
<span data-ttu-id="bb2f2-112">Data Factory supporta la connessione da e verso il file system locale tramite il **Gateway di gestione dati**.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-112">Data Factory supports connecting to and from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="bb2f2-113">È necessario installare il Gateway di gestione di dati nell'ambiente locale per consentire al servizio Data Factory per connettersi a qualsiasi archivio dati locale supportato, incluso il file system.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-113">You must install the Data Management Gateway in your on-premises environment for the Data Factory service to connect to any supported on-premises data store including file system.</span></span> <span data-ttu-id="bb2f2-114">Per informazioni sul Gateway di gestione dati e per istruzioni dettagliate sulla configurazione del gateway vedere l'articolo [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-114">To learn about Data Management Gateway and for step-by-step instructions on setting up the gateway, see [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="bb2f2-115">Non è necessario installare altri file binari per la comunicazione da e verso il file system locale, tranne il Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-115">Apart from Data Management Gateway, no other binary files need to be installed to communicate to and from an on-premises file system.</span></span> <span data-ttu-id="bb2f2-116">È necessario installare e usare il Gateway di gestione dati anche se il file system si trova in una macchina virtuale di Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-116">You must install and use the Data Management Gateway even if the file system is in Azure IaaS VM.</span></span> <span data-ttu-id="bb2f2-117">Per informazioni dettagliate sul gateway, vedere [Gateway di gestione dati](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-117">For detailed information about the gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="bb2f2-118">Per usare una condivisione di file Linux, installare [Samba](https://www.samba.org/) sul server Linux e installare il Gateway di gestione dati in un server Windows.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-118">To use a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="bb2f2-119">L'installazione di un Gateway di gestione dati su un server Linux non è supportata.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="bb2f2-120">Introduzione</span><span class="sxs-lookup"><span data-stu-id="bb2f2-120">Getting started</span></span>
<span data-ttu-id="bb2f2-121">È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un file system usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="bb2f2-122">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="bb2f2-123">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="bb2f2-124">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="bb2f2-125">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="bb2f2-126">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="bb2f2-127">Creare una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-127">Create a **data factory**.</span></span> <span data-ttu-id="bb2f2-128">Una data factory può contenere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="bb2f2-129">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-129">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="bb2f2-130">Ad esempio, se si copiano dati da un archivio BLOB di Azure a un file system locale, si creano due servizi collegati per collegare il file system locale e l'account di archiviazione di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-130">For example, if you are copying data from an Azure blob storage to an on-premises file system, you create two linked services to link your on-premises file system and Azure storage account to your data factory.</span></span> <span data-ttu-id="bb2f2-131">Per le proprietà del servizio collegato specifiche del file system locale, vedere la sezione sulle [proprietà del servizio collegato](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-131">For linked service properties that are specific to an on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="bb2f2-132">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-132">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="bb2f2-133">Nell'esempio citato nel passaggio precedente, si crea un set di dati per specificare un contenitore BLOB e la cartella che contiene i dati di input.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-133">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="bb2f2-134">Si crea anche un altro set di dati per specificare la cartella e il nome file (facoltativo) nel file system.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-134">And, you create another dataset to specify the folder and file name (optional) in your file system.</span></span> <span data-ttu-id="bb2f2-135">Per le proprietà del set di dati specifiche del file system locale, vedere la sezione sulle [proprietà del set di dati](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-135">For dataset properties that are specific to on-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="bb2f2-136">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="bb2f2-137">Nell'esempio indicato in precedenza si usa BlobSource come origine e FileSystemSink come sink per l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-137">In the example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for the copy activity.</span></span> <span data-ttu-id="bb2f2-138">Analogamente, se si effettua la copia dal file system locale all'archivio BLOB di Azure, si usa FileSystemSource e BlobSink nell'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-138">Similarly, if you are copying from on-premises file system to Azure Blob Storage, you use FileSystemSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="bb2f2-139">Per le proprietà dell'attività di copia specifiche del file system locale, vedere la sezione sulle [proprietà dell'attività di copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-139">For copy activity properties that are specific to on-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="bb2f2-140">Per informazioni dettagliate su come usare un archivio dati come origine o come sink, fare clic sul collegamento nella sezione precedente per l'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-140">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="bb2f2-141">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-141">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="bb2f2-142">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di data factory.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="bb2f2-143">Per esempi con definizioni JSON per entità di data factory utilizzate per copiare i dati da e verso un file system, vedere la sezione degli [esempi JSON](#json-examples-for-copying-data-to-and-from-file-system) in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-143">For samples with JSON definitions for Data Factory entities that are used to copy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="bb2f2-144">Le sezioni seguenti riportano informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di data factory specifiche di un file system:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-144">The following sections provide details about JSON properties that are used to define Data Factory entities specific to file system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="bb2f2-145">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="bb2f2-145">Linked service properties</span></span>
<span data-ttu-id="bb2f2-146">È possibile collegare un file system locale a una data factory di Azure con il servizio collegato del **file server locale**.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-146">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="bb2f2-147">La tabella seguente include le descrizioni degli elementi JSON specifici del servizio collegato del file server locale.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-147">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="bb2f2-148">Proprietà</span><span class="sxs-lookup"><span data-stu-id="bb2f2-148">Property</span></span> | <span data-ttu-id="bb2f2-149">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bb2f2-149">Description</span></span> | <span data-ttu-id="bb2f2-150">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="bb2f2-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb2f2-151">type</span><span class="sxs-lookup"><span data-stu-id="bb2f2-151">type</span></span> |<span data-ttu-id="bb2f2-152">Verificare che la proprietà type sia impostata su **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-152">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="bb2f2-153">Sì</span><span class="sxs-lookup"><span data-stu-id="bb2f2-153">Yes</span></span> |
| <span data-ttu-id="bb2f2-154">host</span><span class="sxs-lookup"><span data-stu-id="bb2f2-154">host</span></span> |<span data-ttu-id="bb2f2-155">Specifica il percorso radice della cartella da copiare.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-155">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="bb2f2-156">Usare il carattere di escape '\' per i caratteri speciali nella stringa.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-156">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="bb2f2-157">Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="bb2f2-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="bb2f2-158">Sì</span><span class="sxs-lookup"><span data-stu-id="bb2f2-158">Yes</span></span> |
| <span data-ttu-id="bb2f2-159">userid</span><span class="sxs-lookup"><span data-stu-id="bb2f2-159">userid</span></span> |<span data-ttu-id="bb2f2-160">Specificare l'ID dell'utente che ha accesso al server.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-160">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="bb2f2-161">No (se si sceglie encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="bb2f2-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="bb2f2-162">password</span><span class="sxs-lookup"><span data-stu-id="bb2f2-162">password</span></span> |<span data-ttu-id="bb2f2-163">Specificare la password per l'utente (userid).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-163">Specify the password for the user (userid).</span></span> |<span data-ttu-id="bb2f2-164">No (se si sceglie encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="bb2f2-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="bb2f2-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="bb2f2-165">encryptedCredential</span></span> |<span data-ttu-id="bb2f2-166">Specificare le credenziali crittografate che è possibile ottenere eseguendo il cmdlet New-AzureRmDataFactoryEncryptValue.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-166">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="bb2f2-167">No (se si sceglie di specificare ID utente e password in testo normale)</span><span class="sxs-lookup"><span data-stu-id="bb2f2-167">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="bb2f2-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="bb2f2-168">gatewayName</span></span> |<span data-ttu-id="bb2f2-169">Specifica il nome del gateway che Data Factory deve usare per connettersi al file server locale.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-169">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="bb2f2-170">Sì</span><span class="sxs-lookup"><span data-stu-id="bb2f2-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="bb2f2-171">Servizio collegato di esempio e definizioni del set di dati</span><span class="sxs-lookup"><span data-stu-id="bb2f2-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="bb2f2-172">Scenario</span><span class="sxs-lookup"><span data-stu-id="bb2f2-172">Scenario</span></span> | <span data-ttu-id="bb2f2-173">Host nella definizione del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="bb2f2-173">Host in linked service definition</span></span> | <span data-ttu-id="bb2f2-174">folderPath nella definizione del set di dati</span><span class="sxs-lookup"><span data-stu-id="bb2f2-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb2f2-175">Cartella locale nel computer del gateway di gestione dati: </span><span class="sxs-lookup"><span data-stu-id="bb2f2-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="bb2f2-176">Esempi: D:\\\* o D:\cartella\sottocartella\\*</span><span class="sxs-lookup"><span data-stu-id="bb2f2-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="bb2f2-177">D:\\\\ (per Gateway di gestione dati versione 2.0 e successive)</span><span class="sxs-lookup"><span data-stu-id="bb2f2-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="bb2f2-178">localhost (per le versioni precedenti alla versione 2.0 di Gateway di gestione dati)</span><span class="sxs-lookup"><span data-stu-id="bb2f2-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="bb2f2-179">.\\\\ o cartella\\\\sottocartella (per Gateway di gestione dati 2.0 e versioni successive)</span><span class="sxs-lookup"><span data-stu-id="bb2f2-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="bb2f2-180">D:\\\\ o D:\\\\cartella\\\\sottocartella (per la versione del gateway precedente a 2.0)</span><span class="sxs-lookup"><span data-stu-id="bb2f2-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="bb2f2-181">Cartella condivisa remota: </span><span class="sxs-lookup"><span data-stu-id="bb2f2-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="bb2f2-182">Esempi: \\\\myserver\\share\\\* o \\\\myserver\\share\\cartella\\sottocartella\\*</span><span class="sxs-lookup"><span data-stu-id="bb2f2-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="bb2f2-183">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="bb2f2-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="bb2f2-184">.\\\\ o cartella\\\\sottocartella</span><span class="sxs-lookup"><span data-stu-id="bb2f2-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="bb2f2-185">Esempio: Uso di nome utente e password in testo normale</span><span class="sxs-lookup"><span data-stu-id="bb2f2-185">Example: Using username and password in plain text</span></span>

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

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="bb2f2-186">Esempio: Uso di encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="bb2f2-186">Example: Using encryptedcredential</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="bb2f2-187">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="bb2f2-187">Dataset properties</span></span>
<span data-ttu-id="bb2f2-188">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo [Creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="bb2f2-189">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="bb2f2-190">La sezione typeProperties è diversa per ogni tipo di set di dati</span><span class="sxs-lookup"><span data-stu-id="bb2f2-190">The typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="bb2f2-191">e fornisce informazioni come la posizione e il formato dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-191">It provides information such as the location and format of the data in the data store.</span></span> <span data-ttu-id="bb2f2-192">La sezione typeProperties per il set di dati di tipo **FileShare** presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-192">The typeProperties section for the dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="bb2f2-193">Proprietà</span><span class="sxs-lookup"><span data-stu-id="bb2f2-193">Property</span></span> | <span data-ttu-id="bb2f2-194">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bb2f2-194">Description</span></span> | <span data-ttu-id="bb2f2-195">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="bb2f2-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb2f2-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="bb2f2-196">folderPath</span></span> |<span data-ttu-id="bb2f2-197">Specifica il percorso secondario della cartella.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-197">Specifies the subpath to the folder.</span></span> <span data-ttu-id="bb2f2-198">Usare il carattere di escape '\' per i caratteri speciali nella stringa.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-198">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="bb2f2-199">Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="bb2f2-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="bb2f2-200">È possibile combinare questa proprietà con **partitionBy** per ottenere percorsi di cartelle basati su data e ora di inizio/fine delle sezioni.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-200">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="bb2f2-201">Sì</span><span class="sxs-lookup"><span data-stu-id="bb2f2-201">Yes</span></span> |
| <span data-ttu-id="bb2f2-202">fileName</span><span class="sxs-lookup"><span data-stu-id="bb2f2-202">fileName</span></span> |<span data-ttu-id="bb2f2-203">Specificare il nome del file in **folderPath** se si vuole che la tabella faccia riferimento a un file specifico nella cartella.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-203">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="bb2f2-204">Se non si specifica alcun valore per questa proprietà, la tabella punta a tutti i file nella cartella.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-204">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="bb2f2-205">Quando **fileName** non è specificato per un set di dati di output e **preserveHierarchy** non è specificato nel sink dell'attività, il nome del file generato avrà il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="bb2f2-206">`Data.<Guid>.txt` Esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="bb2f2-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="bb2f2-207">No</span><span class="sxs-lookup"><span data-stu-id="bb2f2-207">No</span></span> |
| <span data-ttu-id="bb2f2-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="bb2f2-208">fileFilter</span></span> |<span data-ttu-id="bb2f2-209">Specificare un filtro da usare per selezionare un sottoinsieme di file in folderPath anziché tutti i file.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-209">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="bb2f2-210">I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="bb2f2-211">Esempio 1: "fileFilter": "*. log"</span><span class="sxs-lookup"><span data-stu-id="bb2f2-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="bb2f2-212">Esempio 2: "fileFilter": 2014 - 1-?. txt"</span><span class="sxs-lookup"><span data-stu-id="bb2f2-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="bb2f2-213">Si noti che fileFilter è applicabile per un set di dati di input FileShare.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="bb2f2-214">No</span><span class="sxs-lookup"><span data-stu-id="bb2f2-214">No</span></span> |
| <span data-ttu-id="bb2f2-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="bb2f2-215">partitionedBy</span></span> |<span data-ttu-id="bb2f2-216">È possibile usare partitionedBy per specificare un valore folderPath/fileName dinamico per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-216">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="bb2f2-217">Un esempio è folderPath con parametri per ogni ora di dati.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="bb2f2-218">No</span><span class="sxs-lookup"><span data-stu-id="bb2f2-218">No</span></span> |
| <span data-ttu-id="bb2f2-219">format</span><span class="sxs-lookup"><span data-stu-id="bb2f2-219">format</span></span> | <span data-ttu-id="bb2f2-220">Sono supportati i tipi di formato seguenti: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-220">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="bb2f2-221">Impostare la proprietà **type** nell'area format su uno di questi valori.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-221">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="bb2f2-222">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="bb2f2-223">Per **copiare i file così come sono** tra archivi basati su file (copia binaria), è possibile ignorare la sezione del formato nelle definizioni dei set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-223">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="bb2f2-224">No</span><span class="sxs-lookup"><span data-stu-id="bb2f2-224">No</span></span> |
| <span data-ttu-id="bb2f2-225">compressione</span><span class="sxs-lookup"><span data-stu-id="bb2f2-225">compression</span></span> | <span data-ttu-id="bb2f2-226">Specificare il tipo e il livello di compressione dei dati.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-226">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="bb2f2-227">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="bb2f2-228">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="bb2f2-229">vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="bb2f2-230">No</span><span class="sxs-lookup"><span data-stu-id="bb2f2-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="bb2f2-231">Non è possibile usare fileName e fileFilter contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="bb2f2-232">Uso della proprietà partitionedBy</span><span class="sxs-lookup"><span data-stu-id="bb2f2-232">Using partitionedBy property</span></span>
<span data-ttu-id="bb2f2-233">Come indicato nella sezione precedente, è possibile specificare valori fileName e folderPath dinamici per i dati di una serie temporale con la proprietà **partitionedBy**, le [funzioni di data factory e le variabili di sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-233">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="bb2f2-234">Per altri dettagli sui set di dati delle serie temporali, sulla pianificazione e sulle sezioni, vedere gli articoli [Creazione di set di dati](data-factory-create-datasets.md), [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) e [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-234">To understand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="bb2f2-235">Esempio 1.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="bb2f2-236">In questo esempio {Slice} viene sostituito con il valore della variabile di sistema SliceStart di Data Factory nel formato (AAAAMMGGHH).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-236">In this example, {Slice} is replaced with the value of the Data Factory system variable SliceStart in the format (YYYYMMDDHH).</span></span> <span data-ttu-id="bb2f2-237">SliceStart fa riferimento all'ora di inizio della sezione.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-237">SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="bb2f2-238">La proprietà folderPath è diversa per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-238">The folderPath is different for each slice.</span></span> <span data-ttu-id="bb2f2-239">Ad esempio: wikisampledataout/wikidatagateway/2014100103 o wikisampledataout/wikidatagateway/2014100104.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="bb2f2-240">Esempio 2:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-240">Sample 2:</span></span>

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

<span data-ttu-id="bb2f2-241">In questo esempio l'anno, il mese, il giorno e l'ora di SliceStart vengono estratti in variabili separate usate dalle proprietà folderPath e fileName.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that the folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="bb2f2-242">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="bb2f2-242">Copy activity properties</span></span>
<span data-ttu-id="bb2f2-243">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-243">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="bb2f2-244">Proprietà quali nome, descrizione, criteri e set di dati di input e di output sono disponibili per tutti i tipi di attività.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="bb2f2-245">Le proprietà disponibili nella sezione **typeProperties** dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-245">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span>

<span data-ttu-id="bb2f2-246">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-246">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="bb2f2-247">Se si effettua il trasferimento dei dati da un file system locale, impostare il tipo di origine nell'attività di copia su **FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-247">If you are moving data from an on-premises file system, you set the source type in the copy activity to **FileSystemSource**.</span></span> <span data-ttu-id="bb2f2-248">Se si effettua il trasferimento dei dati verso un file system locale, impostare il tipo di sink nell'attività di copia su **FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-248">Similarly, if you are moving data to an on-premises file system, you set the sink type in the copy activity to **FileSystemSink**.</span></span> <span data-ttu-id="bb2f2-249">Questa sezione presenta un elenco delle proprietà supportate da FileSystemSource e FileSystemSink.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="bb2f2-250">**FileSystemSource** supporta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-250">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="bb2f2-251">Proprietà</span><span class="sxs-lookup"><span data-stu-id="bb2f2-251">Property</span></span> | <span data-ttu-id="bb2f2-252">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bb2f2-252">Description</span></span> | <span data-ttu-id="bb2f2-253">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="bb2f2-253">Allowed values</span></span> | <span data-ttu-id="bb2f2-254">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="bb2f2-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bb2f2-255">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="bb2f2-255">recursive</span></span> |<span data-ttu-id="bb2f2-256">Indica se i dati vengono letti in modo ricorsivo dalle cartelle secondarie o solo dalla cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-256">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="bb2f2-257">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="bb2f2-257">True, False (default)</span></span> |<span data-ttu-id="bb2f2-258">No</span><span class="sxs-lookup"><span data-stu-id="bb2f2-258">No</span></span> |

<span data-ttu-id="bb2f2-259">**FileSystemSink** supporta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-259">**FileSystemSink** supports the following properties:</span></span>

| <span data-ttu-id="bb2f2-260">Proprietà</span><span class="sxs-lookup"><span data-stu-id="bb2f2-260">Property</span></span> | <span data-ttu-id="bb2f2-261">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bb2f2-261">Description</span></span> | <span data-ttu-id="bb2f2-262">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="bb2f2-262">Allowed values</span></span> | <span data-ttu-id="bb2f2-263">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="bb2f2-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bb2f2-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="bb2f2-264">copyBehavior</span></span> |<span data-ttu-id="bb2f2-265">Definisce il comportamento di copia quando l'origine è BlobSource o FileSystem.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-265">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="bb2f2-266">**PreserveHierarchy:** mantiene la gerarchia dei file nella cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-266">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="bb2f2-267">Il percorso relativo del file di origine nella cartella di origine è identico al percorso relativo del file di destinazione nella cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-267">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="bb2f2-268">**FlattenHierarchy**: tutti i file della cartella di origine vengono creati nel primo livello della cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-268">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="bb2f2-269">Il nome dei file di destinazione viene generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-269">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="bb2f2-270">**MergeFiles**: unisce tutti i file della cartella di origine in un solo file.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-270">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="bb2f2-271">Se il nome file/BLOB viene specificato, il nome del file unito sarà il nome specificato.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-271">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="bb2f2-272">In caso contrario, verrà usato un nome file generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="bb2f2-273">No</span><span class="sxs-lookup"><span data-stu-id="bb2f2-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="bb2f2-274">esempi ricorsivi e copyBehavior</span><span class="sxs-lookup"><span data-stu-id="bb2f2-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="bb2f2-275">Questa sezione descrive il comportamento derivante dell'operazione di copia per diverse combinazioni di valori ricorsivi e delle proprietà copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-275">This section describes the resulting behavior of the Copy operation for different combinations of values for the recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="bb2f2-276">valore ricorsivo</span><span class="sxs-lookup"><span data-stu-id="bb2f2-276">recursive value</span></span> | <span data-ttu-id="bb2f2-277">valore di copyBehavior</span><span class="sxs-lookup"><span data-stu-id="bb2f2-277">copyBehavior value</span></span> | <span data-ttu-id="bb2f2-278">Comportamento risultante</span><span class="sxs-lookup"><span data-stu-id="bb2f2-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb2f2-279">true</span><span class="sxs-lookup"><span data-stu-id="bb2f2-279">true</span></span> |<span data-ttu-id="bb2f2-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="bb2f2-280">preserveHierarchy</span></span> |<span data-ttu-id="bb2f2-281">Per una cartella di origine Cartella1 con la struttura seguente,</span><span class="sxs-lookup"><span data-stu-id="bb2f2-281">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="bb2f2-282">Cartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-282">Folder1</span></span><br/><span data-ttu-id="bb2f2-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="bb2f2-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="bb2f2-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="bb2f2-285">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="bb2f2-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="bb2f2-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="bb2f2-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="bb2f2-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="bb2f2-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="bb2f2-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="bb2f2-289">la cartella di destinazione Cartella1 viene creata con la stessa struttura dell'origine:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-289">the target folder Folder1 is created with the same structure as the source:</span></span><br/><br/><span data-ttu-id="bb2f2-290">Cartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-290">Folder1</span></span><br/><span data-ttu-id="bb2f2-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="bb2f2-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="bb2f2-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="bb2f2-293">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="bb2f2-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="bb2f2-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="bb2f2-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="bb2f2-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="bb2f2-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="bb2f2-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="bb2f2-297">true</span><span class="sxs-lookup"><span data-stu-id="bb2f2-297">true</span></span> |<span data-ttu-id="bb2f2-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="bb2f2-298">flattenHierarchy</span></span> |<span data-ttu-id="bb2f2-299">Per una cartella di origine Cartella1 con la struttura seguente,</span><span class="sxs-lookup"><span data-stu-id="bb2f2-299">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="bb2f2-300">Cartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-300">Folder1</span></span><br/><span data-ttu-id="bb2f2-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="bb2f2-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="bb2f2-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="bb2f2-303">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="bb2f2-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="bb2f2-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="bb2f2-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="bb2f2-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="bb2f2-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="bb2f2-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="bb2f2-307">la Cartella1 di destinazione viene creata con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-307">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="bb2f2-308">Cartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-308">Folder1</span></span><br/><span data-ttu-id="bb2f2-309">&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="bb2f2-310">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File2</span><span class="sxs-lookup"><span data-stu-id="bb2f2-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="bb2f2-311">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File3</span><span class="sxs-lookup"><span data-stu-id="bb2f2-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="bb2f2-312">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File4</span><span class="sxs-lookup"><span data-stu-id="bb2f2-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="bb2f2-313">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File5</span><span class="sxs-lookup"><span data-stu-id="bb2f2-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="bb2f2-314">true</span><span class="sxs-lookup"><span data-stu-id="bb2f2-314">true</span></span> |<span data-ttu-id="bb2f2-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="bb2f2-315">mergeFiles</span></span> |<span data-ttu-id="bb2f2-316">Per una cartella di origine Cartella1 con la struttura seguente,</span><span class="sxs-lookup"><span data-stu-id="bb2f2-316">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="bb2f2-317">Cartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-317">Folder1</span></span><br/><span data-ttu-id="bb2f2-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="bb2f2-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="bb2f2-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="bb2f2-320">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="bb2f2-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="bb2f2-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="bb2f2-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="bb2f2-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="bb2f2-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="bb2f2-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="bb2f2-324">la Cartella1 di destinazione viene creata con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-324">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="bb2f2-325">Cartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-325">Folder1</span></span><br/><span data-ttu-id="bb2f2-326">&nbsp;&nbsp;&nbsp;&nbsp;Il contenuto di File1 + File2 + File3 + File4 + File 5 viene unito in un file con nome generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="bb2f2-327">false</span><span class="sxs-lookup"><span data-stu-id="bb2f2-327">false</span></span> |<span data-ttu-id="bb2f2-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="bb2f2-328">preserveHierarchy</span></span> |<span data-ttu-id="bb2f2-329">Per una cartella di origine Cartella1 con la struttura seguente,</span><span class="sxs-lookup"><span data-stu-id="bb2f2-329">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="bb2f2-330">Cartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-330">Folder1</span></span><br/><span data-ttu-id="bb2f2-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="bb2f2-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="bb2f2-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="bb2f2-333">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="bb2f2-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="bb2f2-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="bb2f2-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="bb2f2-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="bb2f2-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="bb2f2-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="bb2f2-337">la Cartella1 di destinazione viene creata con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-337">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="bb2f2-338">Cartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-338">Folder1</span></span><br/><span data-ttu-id="bb2f2-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="bb2f2-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="bb2f2-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="bb2f2-341">La sottocartella1 con File3, File4 e File5 non viene considerata.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="bb2f2-342">false</span><span class="sxs-lookup"><span data-stu-id="bb2f2-342">false</span></span> |<span data-ttu-id="bb2f2-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="bb2f2-343">flattenHierarchy</span></span> |<span data-ttu-id="bb2f2-344">Per una cartella di origine Cartella1 con la struttura seguente,</span><span class="sxs-lookup"><span data-stu-id="bb2f2-344">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="bb2f2-345">Cartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-345">Folder1</span></span><br/><span data-ttu-id="bb2f2-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="bb2f2-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="bb2f2-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="bb2f2-348">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="bb2f2-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="bb2f2-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="bb2f2-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="bb2f2-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="bb2f2-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="bb2f2-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="bb2f2-352">la Cartella1 di destinazione viene creata con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-352">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="bb2f2-353">Cartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-353">Folder1</span></span><br/><span data-ttu-id="bb2f2-354">&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="bb2f2-355">&nbsp;&nbsp;&nbsp;&nbsp;nome generato automaticamente per File2</span><span class="sxs-lookup"><span data-stu-id="bb2f2-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="bb2f2-356">La sottocartella1 con File3, File4 e File5 non viene considerata.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="bb2f2-357">false</span><span class="sxs-lookup"><span data-stu-id="bb2f2-357">false</span></span> |<span data-ttu-id="bb2f2-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="bb2f2-358">mergeFiles</span></span> |<span data-ttu-id="bb2f2-359">Per una cartella di origine Cartella1 con la struttura seguente,</span><span class="sxs-lookup"><span data-stu-id="bb2f2-359">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="bb2f2-360">Cartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-360">Folder1</span></span><br/><span data-ttu-id="bb2f2-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="bb2f2-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="bb2f2-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="bb2f2-363">&nbsp;&nbsp;&nbsp;&nbsp;Sottocartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="bb2f2-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="bb2f2-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="bb2f2-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="bb2f2-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="bb2f2-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="bb2f2-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="bb2f2-367">la Cartella1 di destinazione viene creata con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-367">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="bb2f2-368">Cartella1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-368">Folder1</span></span><br/><span data-ttu-id="bb2f2-369">&nbsp;&nbsp;&nbsp;&nbsp;Il contenuto di File1 + File2 viene unito in un file con un nome file generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="bb2f2-370">&nbsp;&nbsp;&nbsp;&nbsp;Nome generato automaticamente per File1</span><span class="sxs-lookup"><span data-stu-id="bb2f2-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="bb2f2-371">La sottocartella1 con File3, File4 e File5 non viene considerata.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="bb2f2-372">Formati di file e di compressione supportati</span><span class="sxs-lookup"><span data-stu-id="bb2f2-372">Supported file and compression formats</span></span>
<span data-ttu-id="bb2f2-373">Per i dettagli, vedere l'articolo relativo ai [file e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-file-system"></a><span data-ttu-id="bb2f2-374">Esempi JSON per la copia dei dati da e verso un file system</span><span class="sxs-lookup"><span data-stu-id="bb2f2-374">JSON examples for copying data to and from file system</span></span>
<span data-ttu-id="bb2f2-375">Gli esempi seguenti forniscono le definizioni JSON di esempio da usare per creare una pipeline con il [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-375">The following examples provide sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="bb2f2-376">Questi esempi mostrano come copiare dati da e nel file system locale e in Archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-376">They show how to copy data to and from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="bb2f2-377">È tuttavia possibile copiare dati *direttamente* da una qualsiasi delle origini in uno qualsiasi dei sink elencati in [Sink e origini supportate](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tramite l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-377">However, you can copy data *directly* from any of the sources to any of the sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-to-azure-blob-storage"></a><span data-ttu-id="bb2f2-378">Esempio: Copiare i dati da un file system locale in Archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="bb2f2-378">Example: Copy data from an on-premises file system to Azure Blob storage</span></span>
<span data-ttu-id="bb2f2-379">Questo esempio illustra come copiare dati da un file system locale in Archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-379">This sample shows how to copy data from an on-premises file system to Azure Blob storage.</span></span> <span data-ttu-id="bb2f2-380">L'esempio include le entità della data factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-380">The sample has the following Data Factory entities:</span></span>

* <span data-ttu-id="bb2f2-381">Un servizio collegato di tipo [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="bb2f2-382">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="bb2f2-383">Un [set di dati](data-factory-create-datasets.md) di input di tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="bb2f2-384">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="bb2f2-385">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="bb2f2-386">L'esempio seguente copia i dati appartenenti a una serie temporale da un file system locale in Archiviazione BLOB di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-386">The following sample copies time-series data from an on-premises file system to Azure Blob storage every hour.</span></span> <span data-ttu-id="bb2f2-387">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-387">The JSON properties that are used in these samples are described in the sections after the samples.</span></span>

<span data-ttu-id="bb2f2-388">Come primo passaggio configurare il Gateway di gestione dati secondo le istruzioni in [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-388">As a first step, set up Data Management Gateway as per the instructions in [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="bb2f2-389">**Servizio collegato del file server locale:**</span><span class="sxs-lookup"><span data-stu-id="bb2f2-389">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="bb2f2-390">Si consiglia di usare la proprietà **encryptedCredential** anziché le proprietà **userid** e **password**.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-390">We recommend using the **encryptedCredential** property instead the **userid** and **password** properties.</span></span> <span data-ttu-id="bb2f2-391">Per informazioni dettagliate su questo servizio collegato, vedere l'articolo relativo al [servizio collegato del file server](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="bb2f2-392">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="bb2f2-392">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="bb2f2-393">**Set di dati di input del file system locale:**</span><span class="sxs-lookup"><span data-stu-id="bb2f2-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="bb2f2-394">I dati vengono prelevati da un nuovo file ogni ora.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="bb2f2-395">Le proprietà folderPath e fileName vengono determinate in base all'ora di inizio della sezione.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-395">The folderPath and fileName properties are determined based on the start time of the slice.</span></span>  

<span data-ttu-id="bb2f2-396">L'impostazione di `"external": "true"` comunica a Data Factory che il set di dati è esterno alla data factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-396">Setting `"external": "true"` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="bb2f2-397">**Set di dati di ouput di Archiviazione BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="bb2f2-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="bb2f2-398">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-398">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="bb2f2-399">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-399">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="bb2f2-400">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-400">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

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

<span data-ttu-id="bb2f2-401">**Un'attività di copia in una pipeline con un'origine su file system e un sink BLOB:**</span><span class="sxs-lookup"><span data-stu-id="bb2f2-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="bb2f2-402">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-402">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="bb2f2-403">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **FileSystemSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-403">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

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

### <a name="example-copy-data-from-azure-sql-database-to-an-on-premises-file-system"></a><span data-ttu-id="bb2f2-404">Esempio: Copiare i dati dal database SQL di Azure in un file system locale</span><span class="sxs-lookup"><span data-stu-id="bb2f2-404">Example: Copy data from Azure SQL Database to an on-premises file system</span></span>
<span data-ttu-id="bb2f2-405">L'esempio seguente mostra:</span><span class="sxs-lookup"><span data-stu-id="bb2f2-405">The following sample shows:</span></span>

* <span data-ttu-id="bb2f2-406">Un servizio collegato di tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="bb2f2-407">Un servizio collegato di tipo [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="bb2f2-408">Un set di dati di input di tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="bb2f2-409">Un set di dati di output di tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="bb2f2-410">Una pipeline con attività di copia che usa [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) e [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="bb2f2-411">L'esempio copia i dati di una serie temporale da una tabella di Azure SQL a un sistema di file locale ogni ora.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-411">The sample copies time-series data from an Azure SQL table to an on-premises file system every hour.</span></span> <span data-ttu-id="bb2f2-412">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-412">The JSON properties that are used in these samples are described in sections after the samples.</span></span>

<span data-ttu-id="bb2f2-413">**Servizio collegato per il database SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="bb2f2-413">**Azure SQL Database linked service:**</span></span>

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

<span data-ttu-id="bb2f2-414">**Servizio collegato del file server locale:**</span><span class="sxs-lookup"><span data-stu-id="bb2f2-414">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="bb2f2-415">Si consiglia di usare la proprietà **encryptedCredential** anziché le proprietà **userid** e **password**.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-415">We recommend using the **encryptedCredential** property instead of using the **userid** and **password** properties.</span></span> <span data-ttu-id="bb2f2-416">Per informazioni dettagliate su questo servizio collegato, vedere l'articolo relativo al [servizio collegato del file system](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="bb2f2-417">**Set di dati di input SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="bb2f2-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="bb2f2-418">L'esempio presuppone che sia stata creata una tabella "MyTable" in SQL Azure e che contenga una colonna denominata "timestampcolumn" per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-418">The sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="bb2f2-419">L'impostazione di ``“external”: ”true”`` comunica a Data Factory che il set di dati è esterno alla data factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-419">Setting ``“external”: ”true”`` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="bb2f2-420">**Set di dati di output del file system locale:**</span><span class="sxs-lookup"><span data-stu-id="bb2f2-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="bb2f2-421">I dati vengono copiati in un nuovo file ogni ora.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-421">Data is copied to a new file every hour.</span></span> <span data-ttu-id="bb2f2-422">folderPath e fileName per il BLOB vengono determinati in base all'ora di inizio della sezione.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-422">The folderPath and fileName for the blob are determined based on the start time of the slice.</span></span>

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

<span data-ttu-id="bb2f2-423">**Un'attività di copia in una pipeline con un'origine SQL e un sink di file system:**</span><span class="sxs-lookup"><span data-stu-id="bb2f2-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="bb2f2-424">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-424">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="bb2f2-425">Nella definizione JSON della pipeline, il tipo **source** è impostato su **SqlSource** e il tipo **sink** è impostato su **FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-425">In the pipeline JSON definition, the **source** type is set to **SqlSource**, and the **sink** type is set to **FileSystemSink**.</span></span> <span data-ttu-id="bb2f2-426">La query SQL specificata per la proprietà **SqlReaderQuery** consente di selezionare i dati da copiare nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-426">The SQL query that is specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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


<span data-ttu-id="bb2f2-427">È anche possibile eseguire il mapping delle colonne del set di dati di origine alle colonne del set di dati sink nella definizione dell'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="bb2f2-427">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="bb2f2-428">Per altre informazioni, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="bb2f2-429">Prestazioni e ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="bb2f2-429">Performance and tuning</span></span>
 <span data-ttu-id="bb2f2-430">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="bb2f2-430">To learn about key factors that impact the performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
