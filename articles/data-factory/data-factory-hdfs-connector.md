---
title: Spostare dati da HDFS locale | Documentazione Microsoft
description: Informazioni su come spostare dati da un HDFS locale con Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9a8f3156a62a1a7aa49377349e8a85454efeda50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="fa38b-103">Spostare dati da HDFS locale con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="fa38b-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
<span data-ttu-id="fa38b-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da un HDFS locale.</span><span class="sxs-lookup"><span data-stu-id="fa38b-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises HDFS.</span></span> <span data-ttu-id="fa38b-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="fa38b-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="fa38b-106">È possibile copiare dati da un HDFS a qualsiasi archivio dati di sink supportato.</span><span class="sxs-lookup"><span data-stu-id="fa38b-106">You can copy data from HDFS to any supported sink data store.</span></span> <span data-ttu-id="fa38b-107">Per un elenco degli archivi dati supportati come sink dall'attività di copia, vedere la tabella relativa agli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="fa38b-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="fa38b-108">Data Factory supporta attualmente solo lo spostamento di dati da un HDFS ad altri archivi dati, ma non da altri archivi dati a un HDFS locale.</span><span class="sxs-lookup"><span data-stu-id="fa38b-108">Data factory currently supports only moving data from an on-premises HDFS to other data stores, but not for moving data from other data stores to an on-premises HDFS.</span></span>

> [!NOTE]
> <span data-ttu-id="fa38b-109">L'attività di copia non elimina il file di origine dopo che è stato correttamente copiato nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="fa38b-109">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="fa38b-110">Se è necessario eliminare il file di origine dopo una copia con esito positivo, creare un'attività personalizzata per eliminare il file e usare l'attività nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="fa38b-110">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="fa38b-111">Abilitazione della connettività</span><span class="sxs-lookup"><span data-stu-id="fa38b-111">Enabling connectivity</span></span>
<span data-ttu-id="fa38b-112">Il servizio Data Factory supporta la connessione a un HDFS locale tramite il Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="fa38b-112">Data Factory service supports connecting to on-premises HDFS using the Data Management Gateway.</span></span> <span data-ttu-id="fa38b-113">Vedere l'articolo sullo [spostamento di dati tra sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) per informazioni sul Gateway di gestione dati e per istruzioni dettagliate sulla configurazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="fa38b-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="fa38b-114">Usare il gateway per connettersi a HDFS anche se è ospitato in una VM IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa38b-114">Use the gateway to connect to HDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="fa38b-115">Assicurarsi che il gateway di gestione dati possa accedere a **TUTTI** i [server del nodo dei nomi]: [porta del nodo dei nomi] e [server del nodo dati]: [porta del nodo dati] del cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="fa38b-115">Make sure the Data Management Gateway can access to **ALL** the [name node server]:[name node port] and [data node servers]:[data node port] of the Hadoop cluster.</span></span> <span data-ttu-id="fa38b-116">La [porta del nodo dei nomi] predefinita è 50070 e la [porta del nodo dati] predefinita è 50075.</span><span class="sxs-lookup"><span data-stu-id="fa38b-116">Default [name node port] is 50070, and default [data node port] is 50075.</span></span>

<span data-ttu-id="fa38b-117">Anche se è possibile installare il gateway nello stesso computer locale o nella stessa VM di Azure di HDFS, è consigliabile installarlo in un diverso computer o in una diversa VM IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa38b-117">While you can install gateway on the same on-premises machine or the Azure VM as the HDFS, we recommend that you install the gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="fa38b-118">La presenza del gateway su un computer separato riduce i conflitti di risorse e consente di ottenere prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="fa38b-118">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="fa38b-119">Quando si installa il gateway in un computer separato, questo deve poter accedere al computer con un HDFS.</span><span class="sxs-lookup"><span data-stu-id="fa38b-119">When you install the gateway on a separate machine, the machine should be able to access the machine with the HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fa38b-120">Introduzione</span><span class="sxs-lookup"><span data-stu-id="fa38b-120">Getting started</span></span>
<span data-ttu-id="fa38b-121">È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine HDFS usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="fa38b-121">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="fa38b-122">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="fa38b-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="fa38b-123">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="fa38b-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="fa38b-124">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="fa38b-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="fa38b-125">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="fa38b-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="fa38b-126">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="fa38b-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="fa38b-127">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="fa38b-127">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="fa38b-128">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="fa38b-128">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="fa38b-129">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="fa38b-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="fa38b-130">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fa38b-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="fa38b-131">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di data factory.</span><span class="sxs-lookup"><span data-stu-id="fa38b-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="fa38b-132">Per un esempio con definizioni JSON per entità di data factory utilizzate per copiare dati da un archivio dati HDFS, vedere la sezione [Esempio JSON: Copiare dati da un HDFS locale al BLOB di Azure](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="fa38b-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS to Azure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="fa38b-133">Le sezioni seguenti riportano informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di data factory specifiche di HDFS:</span><span class="sxs-lookup"><span data-stu-id="fa38b-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to HDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="fa38b-134">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="fa38b-134">Linked service properties</span></span>
<span data-ttu-id="fa38b-135">Un servizio collegato collega un archivio dati a una data factory.</span><span class="sxs-lookup"><span data-stu-id="fa38b-135">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="fa38b-136">Viene creato un servizio collegato di tipo **Hdfs** per collegare un HDFS locale alla data factory.</span><span class="sxs-lookup"><span data-stu-id="fa38b-136">You create a linked service of type **Hdfs** to link an on-premises HDFS to your data factory.</span></span> <span data-ttu-id="fa38b-137">La tabella seguente contiene le descrizioni degli elementi JSON specifici del servizio collegato HDFS.</span><span class="sxs-lookup"><span data-stu-id="fa38b-137">The following table provides description for JSON elements specific to HDFS linked service.</span></span>

| <span data-ttu-id="fa38b-138">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fa38b-138">Property</span></span> | <span data-ttu-id="fa38b-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fa38b-139">Description</span></span> | <span data-ttu-id="fa38b-140">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fa38b-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fa38b-141">type</span><span class="sxs-lookup"><span data-stu-id="fa38b-141">type</span></span> |<span data-ttu-id="fa38b-142">La proprietà type deve essere impostata su: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="fa38b-142">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="fa38b-143">Sì</span><span class="sxs-lookup"><span data-stu-id="fa38b-143">Yes</span></span> |
| <span data-ttu-id="fa38b-144">Url</span><span class="sxs-lookup"><span data-stu-id="fa38b-144">Url</span></span> |<span data-ttu-id="fa38b-145">URL di HDFS</span><span class="sxs-lookup"><span data-stu-id="fa38b-145">URL to the HDFS</span></span> |<span data-ttu-id="fa38b-146">Sì</span><span class="sxs-lookup"><span data-stu-id="fa38b-146">Yes</span></span> |
| <span data-ttu-id="fa38b-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="fa38b-147">authenticationType</span></span> |<span data-ttu-id="fa38b-148">Anonima o Windows.</span><span class="sxs-lookup"><span data-stu-id="fa38b-148">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="fa38b-149">Per usare l'**autenticazione Kerberos** per il connettore HDFS, fare riferimento a [questa sezione](#use-kerberos-authentication-for-hdfs-connector) per impostare correttamente l'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="fa38b-149">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="fa38b-150">Sì</span><span class="sxs-lookup"><span data-stu-id="fa38b-150">Yes</span></span> |
| <span data-ttu-id="fa38b-151">userName</span><span class="sxs-lookup"><span data-stu-id="fa38b-151">userName</span></span> |<span data-ttu-id="fa38b-152">Nome utente per l'autenticazione di Windows</span><span class="sxs-lookup"><span data-stu-id="fa38b-152">Username for Windows authentication.</span></span> |<span data-ttu-id="fa38b-153">Sì (per l'autenticazione di Windows)</span><span class="sxs-lookup"><span data-stu-id="fa38b-153">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="fa38b-154">password</span><span class="sxs-lookup"><span data-stu-id="fa38b-154">password</span></span> |<span data-ttu-id="fa38b-155">Password per l'autenticazione di Windows</span><span class="sxs-lookup"><span data-stu-id="fa38b-155">Password for Windows authentication.</span></span> |<span data-ttu-id="fa38b-156">Sì (per l'autenticazione di Windows)</span><span class="sxs-lookup"><span data-stu-id="fa38b-156">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="fa38b-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="fa38b-157">gatewayName</span></span> |<span data-ttu-id="fa38b-158">Nome del gateway che il servizio Data Factory deve usare per connettersi a HDFS.</span><span class="sxs-lookup"><span data-stu-id="fa38b-158">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="fa38b-159">Sì</span><span class="sxs-lookup"><span data-stu-id="fa38b-159">Yes</span></span> |
| <span data-ttu-id="fa38b-160">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="fa38b-160">encryptedCredential</span></span> |<span data-ttu-id="fa38b-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) delle credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="fa38b-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span></span> |<span data-ttu-id="fa38b-162">No</span><span class="sxs-lookup"><span data-stu-id="fa38b-162">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="fa38b-163">Uso dell'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="fa38b-163">Using Anonymous authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a><span data-ttu-id="fa38b-164">Uso dell'autenticazione di Windows</span><span class="sxs-lookup"><span data-stu-id="fa38b-164">Using Windows authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a><span data-ttu-id="fa38b-165">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="fa38b-165">Dataset properties</span></span>
<span data-ttu-id="fa38b-166">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="fa38b-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="fa38b-167">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="fa38b-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="fa38b-168">La sezione **typeProperties** è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="fa38b-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="fa38b-169">La sezione typeProperties per il set di dati di tipo **FileShare** , che include il set di dati HDFS, presenta le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="fa38b-169">The typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has the following properties</span></span>

| <span data-ttu-id="fa38b-170">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fa38b-170">Property</span></span> | <span data-ttu-id="fa38b-171">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fa38b-171">Description</span></span> | <span data-ttu-id="fa38b-172">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fa38b-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fa38b-173">folderPath</span><span class="sxs-lookup"><span data-stu-id="fa38b-173">folderPath</span></span> |<span data-ttu-id="fa38b-174">Percorso della cartella.</span><span class="sxs-lookup"><span data-stu-id="fa38b-174">Path to the folder.</span></span> <span data-ttu-id="fa38b-175">Esempio: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="fa38b-175">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="fa38b-176">Usare il carattere di escape "\" per i caratteri speciali nella stringa.</span><span class="sxs-lookup"><span data-stu-id="fa38b-176">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="fa38b-177">Ad esempio: per cartella\sottocartella specificare cartella\\\\sottocartella e per d:\cartellaesempio specificare l'unità d:\\\\cartellaesempio.</span><span class="sxs-lookup"><span data-stu-id="fa38b-177">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="fa38b-178">È possibile combinare questa proprietà con **partitionBy** per ottenere percorsi di cartelle basati su data e ora di inizio/fine delle sezioni.</span><span class="sxs-lookup"><span data-stu-id="fa38b-178">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="fa38b-179">Sì</span><span class="sxs-lookup"><span data-stu-id="fa38b-179">Yes</span></span> |
| <span data-ttu-id="fa38b-180">fileName</span><span class="sxs-lookup"><span data-stu-id="fa38b-180">fileName</span></span> |<span data-ttu-id="fa38b-181">Specificare il nome del file in **folderPath** se si vuole che la tabella faccia riferimento a un file specifico nella cartella.</span><span class="sxs-lookup"><span data-stu-id="fa38b-181">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="fa38b-182">Se non si specifica alcun valore per questa proprietà, la tabella punta a tutti i file nella cartella.</span><span class="sxs-lookup"><span data-stu-id="fa38b-182">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="fa38b-183">Quando fileName non viene specificato per un set di dati di output, il nome del file generato sarà nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="fa38b-183">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="fa38b-184">Data<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="fa38b-184">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="fa38b-185">No</span><span class="sxs-lookup"><span data-stu-id="fa38b-185">No</span></span> |
| <span data-ttu-id="fa38b-186">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="fa38b-186">partitionedBy</span></span> |<span data-ttu-id="fa38b-187">partitionedBy può essere usato per specificare un valore folderPath dinamico e un nome file per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="fa38b-187">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="fa38b-188">Ad esempio, folderPath con parametri per ogni ora di dati.</span><span class="sxs-lookup"><span data-stu-id="fa38b-188">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="fa38b-189">No</span><span class="sxs-lookup"><span data-stu-id="fa38b-189">No</span></span> |
| <span data-ttu-id="fa38b-190">format</span><span class="sxs-lookup"><span data-stu-id="fa38b-190">format</span></span> | <span data-ttu-id="fa38b-191">Sono supportati i tipi di formato seguenti: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="fa38b-191">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="fa38b-192">Impostare la proprietà **type** nell'area format su uno di questi valori.</span><span class="sxs-lookup"><span data-stu-id="fa38b-192">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="fa38b-193">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="fa38b-193">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="fa38b-194">Per **copiare i file così come sono** tra archivi basati su file (copia binaria), è possibile ignorare la sezione del formato nelle definizioni dei set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="fa38b-194">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="fa38b-195">No</span><span class="sxs-lookup"><span data-stu-id="fa38b-195">No</span></span> |
| <span data-ttu-id="fa38b-196">compressione</span><span class="sxs-lookup"><span data-stu-id="fa38b-196">compression</span></span> | <span data-ttu-id="fa38b-197">Specificare il tipo e il livello di compressione dei dati.</span><span class="sxs-lookup"><span data-stu-id="fa38b-197">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="fa38b-198">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="fa38b-198">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="fa38b-199">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="fa38b-199">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="fa38b-200">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="fa38b-200">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="fa38b-201">No</span><span class="sxs-lookup"><span data-stu-id="fa38b-201">No</span></span> |

> [!NOTE]
> <span data-ttu-id="fa38b-202">filename e fileFilter non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="fa38b-202">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="fa38b-203">Uso della proprietà partionedBy</span><span class="sxs-lookup"><span data-stu-id="fa38b-203">Using partionedBy property</span></span>
<span data-ttu-id="fa38b-204">Come indicato nella sezione precedente, è possibile specificare valori fileName e folderPath dinamici per i dati di una serie temporale con la proprietà **partitionedBy**, le [funzioni di data factory e le variabili di sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="fa38b-204">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="fa38b-205">Per ulteriori informazioni sui set di dati delle serie temporali, sulla pianificazione e sulle sezioni, vedere gli articoli [Creazione di set di dati](data-factory-create-datasets.md), [Pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) e [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="fa38b-205">To learn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="fa38b-206">Esempio 1.</span><span class="sxs-lookup"><span data-stu-id="fa38b-206">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="fa38b-207">In questo esempio {Slice} viene sostituito con il valore della variabile di sistema SliceStart di Data Factory nel formato (AAAAMMGGHH) specificato.</span><span class="sxs-lookup"><span data-stu-id="fa38b-207">In this example {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="fa38b-208">SliceStart fa riferimento all'ora di inizio della sezione.</span><span class="sxs-lookup"><span data-stu-id="fa38b-208">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="fa38b-209">La proprietà folderPath è diversa per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="fa38b-209">The folderPath is different for each slice.</span></span> <span data-ttu-id="fa38b-210">Ad esempio: wikisampledataout/wikidatagateway/2014100103 o wikisampledataout/wikidatagateway/2014100104.</span><span class="sxs-lookup"><span data-stu-id="fa38b-210">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="fa38b-211">Esempio 2:</span><span class="sxs-lookup"><span data-stu-id="fa38b-211">Sample 2:</span></span>

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
<span data-ttu-id="fa38b-212">In questo esempio l'anno, il mese, il giorno e l'ora di SliceStart vengono estratti in variabili separate che vengono usate dalle proprietà folderPath e fileName.</span><span class="sxs-lookup"><span data-stu-id="fa38b-212">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="fa38b-213">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="fa38b-213">Copy activity properties</span></span>
<span data-ttu-id="fa38b-214">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="fa38b-214">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fa38b-215">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="fa38b-215">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="fa38b-216">Le proprietà disponibili nella sezione typeProperties dell'attività variano invece in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="fa38b-216">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="fa38b-217">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="fa38b-217">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="fa38b-218">Per l'attività di copia con origine di tipo **FileSystemSource** , nella sezione typeProperties sono disponibili le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa38b-218">For Copy Activity, when source is of type **FileSystemSource** the following properties are available in typeProperties section:</span></span>

<span data-ttu-id="fa38b-219">**FileSystemSource** supporta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa38b-219">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="fa38b-220">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fa38b-220">Property</span></span> | <span data-ttu-id="fa38b-221">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fa38b-221">Description</span></span> | <span data-ttu-id="fa38b-222">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="fa38b-222">Allowed values</span></span> | <span data-ttu-id="fa38b-223">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="fa38b-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fa38b-224">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="fa38b-224">recursive</span></span> |<span data-ttu-id="fa38b-225">Indica se i dati vengono letti in modo ricorsivo dalle cartelle secondarie o solo dalla cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="fa38b-225">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="fa38b-226">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="fa38b-226">True, False (default)</span></span> |<span data-ttu-id="fa38b-227">No</span><span class="sxs-lookup"><span data-stu-id="fa38b-227">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="fa38b-228">Formati di file e di compressione supportati</span><span class="sxs-lookup"><span data-stu-id="fa38b-228">Supported file and compression formats</span></span>
<span data-ttu-id="fa38b-229">Per i dettagli, vedere l'articolo relativo ai [file e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="fa38b-229">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-to-azure-blob"></a><span data-ttu-id="fa38b-230">Esempio JSON: Copiare dati da un HDFS locale al BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="fa38b-230">JSON example: Copy data from on-premises HDFS to Azure Blob</span></span>
<span data-ttu-id="fa38b-231">Questo esempio illustra come copiare dati da HDFS locale all'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa38b-231">This sample shows how to copy data from an on-premises HDFS to Azure Blob Storage.</span></span> <span data-ttu-id="fa38b-232">Tuttavia, i dati possono essere copiati **direttamente** in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fa38b-232">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="fa38b-233">L'esempio fornisce le definizioni JSON per le entità di data factory seguenti.</span><span class="sxs-lookup"><span data-stu-id="fa38b-233">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="fa38b-234">È possibile usare queste definizioni per creare una pipeline per copiare dati da HDFS a un'archiviazione BLOB di Azure mediante il [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fa38b-234">You can use these definitions to create a pipeline to copy data from HDFS to Azure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="fa38b-235">Un servizio collegato di tipo [OnPremisesHdfs](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fa38b-235">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="fa38b-236">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fa38b-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fa38b-237">Un [set di dati](data-factory-create-datasets.md) di input di tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fa38b-237">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="fa38b-238">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fa38b-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="fa38b-239">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fa38b-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="fa38b-240">L'esempio copia i dati da un HDFS locale a un BLOB di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="fa38b-240">The sample copies data from an on-premises HDFS to an Azure blob every hour.</span></span> <span data-ttu-id="fa38b-241">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="fa38b-241">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="fa38b-242">Come primo passaggio, impostare il gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="fa38b-242">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="fa38b-243">Le istruzioni sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="fa38b-243">The instructions in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="fa38b-244">**Servizio collegato HDFS**: questo esempio usa l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="fa38b-244">**HDFS linked service:** This example uses the Windows authentication.</span></span> <span data-ttu-id="fa38b-245">Per i diversi tipi di autenticazione disponibili, vedere la sezione [Proprietà del servizio collegato HDFS](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="fa38b-245">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="fa38b-246">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="fa38b-246">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="fa38b-247">**Set di dati di input HDFS**: questo set di dati fa riferimento alla cartella HDFS DataTransfer/UnitTest/.</span><span class="sxs-lookup"><span data-stu-id="fa38b-247">**HDFS input dataset:** This dataset refers to the HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="fa38b-248">La pipeline copia tutti i file di questa cartella nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="fa38b-248">The pipeline copies all the files in this folder to the destination.</span></span>

<span data-ttu-id="fa38b-249">Impostando "external" su "true" si comunica al servizio Data Factory che il set di dati è esterno alla data factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="fa38b-249">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

<span data-ttu-id="fa38b-250">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="fa38b-250">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="fa38b-251">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="fa38b-251">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="fa38b-252">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="fa38b-252">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="fa38b-253">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="fa38b-253">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="fa38b-254">**Un'attività di copia in una pipeline con un'origine su file system e un sink BLOB:**</span><span class="sxs-lookup"><span data-stu-id="fa38b-254">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="fa38b-255">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="fa38b-255">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="fa38b-256">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **FileSystemSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="fa38b-256">In the pipeline JSON definition, the **source** type is set to **FileSystemSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="fa38b-257">La query SQL specificata per la proprietà **query** consente di selezionare i dati da copiare nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="fa38b-257">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="fa38b-258">Uso dell'autenticazione Kerberos per il connettore HDFS</span><span class="sxs-lookup"><span data-stu-id="fa38b-258">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="fa38b-259">Sono disponibili due opzioni per configurare l'ambiente locale in modo da poter usare l'autenticazione Kerberos nel connettore HDFS.</span><span class="sxs-lookup"><span data-stu-id="fa38b-259">There are two options to set up the on-premises environment so as to use Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="fa38b-260">L'utente può scegliere quella più adatta al caso specifico.</span><span class="sxs-lookup"><span data-stu-id="fa38b-260">You can choose the one better fits your case.</span></span>
* <span data-ttu-id="fa38b-261">Opzione 1: [aggiungere un computer gateway all'area di autenticazione di Kerberos](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="fa38b-261">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="fa38b-262">Opzione 2: [Abilitare il trust reciproco tra il dominio di Windows e l'area di autenticazione di Kerberos](#kerberos-mutual-trust)</span><span class="sxs-lookup"><span data-stu-id="fa38b-262">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <span data-ttu-id="fa38b-263"><a name="kerberos-join-realm"></a>Opzione 1: aggiungere un computer gateway all'area di autenticazione di Kerberos</span><span class="sxs-lookup"><span data-stu-id="fa38b-263"><a name="kerberos-join-realm"></a>Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="fa38b-264">Requisito:</span><span class="sxs-lookup"><span data-stu-id="fa38b-264">Requirement:</span></span>

* <span data-ttu-id="fa38b-265">Il computer gateway deve essere aggiunto all'area di autenticazione di Kerberos e non può essere aggiunto a un dominio di Windows.</span><span class="sxs-lookup"><span data-stu-id="fa38b-265">The gateway machine needs to join the Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-to-configure"></a><span data-ttu-id="fa38b-266">Come configurare:</span><span class="sxs-lookup"><span data-stu-id="fa38b-266">How to configure:</span></span>

<span data-ttu-id="fa38b-267">**Nel computer del gateway:**</span><span class="sxs-lookup"><span data-stu-id="fa38b-267">**On gateway machine:**</span></span>

1.  <span data-ttu-id="fa38b-268">Eseguire l'utilità **Ksetup** per configurare il server e l'area didi autenticazione di Kerberos KDC.</span><span class="sxs-lookup"><span data-stu-id="fa38b-268">Run the **Ksetup** utility to configure the Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="fa38b-269">Il computer deve essere configurato come membro di un gruppo di lavoro poiché un'area di autenticazione di Kerberos è diversa da un dominio di Windows.</span><span class="sxs-lookup"><span data-stu-id="fa38b-269">The machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="fa38b-270">È possibile farlo configurando l'area di autenticazione di Kerberos e aggiungendo un server KDC come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="fa38b-270">This can be achieved by setting the Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="fa38b-271">Sostituire *REALM.COM* con la propria area di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="fa38b-271">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="fa38b-272">**Riavviare** il computer dopo aver eseguito questi 2 comandi.</span><span class="sxs-lookup"><span data-stu-id="fa38b-272">**Restart** the machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="fa38b-273">Verificare la configurazione con il comando **Ksetup**.</span><span class="sxs-lookup"><span data-stu-id="fa38b-273">Verify the configuration with **Ksetup** command.</span></span> <span data-ttu-id="fa38b-274">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="fa38b-274">The output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="fa38b-275">**In Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="fa38b-275">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="fa38b-276">Configurare il connettore HDFS usando **l'autenticazione di Windows** con il nome e la password principali di Kerberos per connettersi all'origine dati HDFS.</span><span class="sxs-lookup"><span data-stu-id="fa38b-276">Configure the HDFS connector using **Windows authentication** together with your Kerberos principal name and password to connect to the HDFS data source.</span></span> <span data-ttu-id="fa38b-277">Controllare la sezione [Proprietà del servizio collegato HDFS](#linked-service-properties) per i dettagli di configurazione.</span><span class="sxs-lookup"><span data-stu-id="fa38b-277">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <span data-ttu-id="fa38b-278"><a name="kerberos-mutual-trust"></a>Opzione 2: Abilitare il trust reciproco tra il dominio di Windows e l'area di autenticazione di Kerberos</span><span class="sxs-lookup"><span data-stu-id="fa38b-278"><a name="kerberos-mutual-trust"></a>Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="fa38b-279">Requisito:</span><span class="sxs-lookup"><span data-stu-id="fa38b-279">Requirement:</span></span>
*   <span data-ttu-id="fa38b-280">Il computer del gateway deve essere aggiunto a un dominio di Windows.</span><span class="sxs-lookup"><span data-stu-id="fa38b-280">The gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="fa38b-281">È necessaria l'autorizzazione per aggiornare le impostazioni del controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="fa38b-281">You need permission to update the domain controller's settings.</span></span>

#### <a name="how-to-configure"></a><span data-ttu-id="fa38b-282">Come configurare:</span><span class="sxs-lookup"><span data-stu-id="fa38b-282">How to configure:</span></span>

> [!NOTE]
> <span data-ttu-id="fa38b-283">Sostituire REALM.COM e AD.COM nell'esercitazione di seguito con le rispettive aree di autenticazione e controller di dominio in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="fa38b-283">Replace REALM.COM and AD.COM in the following tutorial with your own respective realm and domain controller as needed.</span></span>

<span data-ttu-id="fa38b-284">**Nel server KDC:**</span><span class="sxs-lookup"><span data-stu-id="fa38b-284">**On KDC server:**</span></span>

1.  <span data-ttu-id="fa38b-285">Modificare la configurazione KDC nel file **krb5.conf** per far considerare attendibile a KDC il dominio di Windows che fa riferimento al modello di configurazione di seguito.</span><span class="sxs-lookup"><span data-stu-id="fa38b-285">Edit the KDC configuration in **krb5.conf** file to let KDC trust Windows Domain referring to the following configuration template.</span></span> <span data-ttu-id="fa38b-286">Per impostazione predefinita, la configurazione si trova in **/etc/krb5.conf**.</span><span class="sxs-lookup"><span data-stu-id="fa38b-286">By default, the configuration is located at **/etc/krb5.conf**.</span></span>

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  <span data-ttu-id="fa38b-287">**Riavviare** il servizio KDC dopo la configurazione.</span><span class="sxs-lookup"><span data-stu-id="fa38b-287">**Restart** the KDC service after configuration.</span></span>

2.  <span data-ttu-id="fa38b-288">Preparare un'entità denominata **krbtgt/REALM.COM@AD.COM** nel server KDC con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fa38b-288">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with the following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="fa38b-289">Nel file di configurazione del servizio HDFS **hadoop.security.auth_to_local** aggiungere `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span><span class="sxs-lookup"><span data-stu-id="fa38b-289">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="fa38b-290">**Nel controller di dominio:**</span><span class="sxs-lookup"><span data-stu-id="fa38b-290">**On domain controller:**</span></span>

1.  <span data-ttu-id="fa38b-291">Eseguire i comandi **Ksetup** seguenti per aggiungere una voce di area di autenticazione:</span><span class="sxs-lookup"><span data-stu-id="fa38b-291">Run the following **Ksetup** commands to add a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="fa38b-292">Stabilire una relazione di trust dal dominio di Windows all'area di autenticazione di Kerberos.</span><span class="sxs-lookup"><span data-stu-id="fa38b-292">Establish trust from Windows Domain to Kerberos Realm.</span></span> <span data-ttu-id="fa38b-293">[password] è la password per l'entità **krbtgt/REALM.COM@AD.COM**.</span><span class="sxs-lookup"><span data-stu-id="fa38b-293">[password] is the password for the principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="fa38b-294">Selezionare l'algoritmo di crittografia usato in Kerberos.</span><span class="sxs-lookup"><span data-stu-id="fa38b-294">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="fa38b-295">Passare a Server Manager > Gestione Criteri di gruppo > Dominio > Oggetti Criteri di gruppo > Criteri dominio attivi o predefiniti e selezionare Modifica.</span><span class="sxs-lookup"><span data-stu-id="fa38b-295">Go to Server Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="fa38b-296">Nella finestra popup **Editor Gestione criteri di gruppo**, passare a Configurazione computer > Criteri > Impostazioni di Windows > Impostazioni di sicurezza > Criteri locali > Opzioni di sicurezza e configurare **Sicurezza di rete: configura tipi di crittografia consentiti per Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="fa38b-296">In the **Group Policy Management Editor** popup window, go to Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="fa38b-297">Selezionare l'algoritmo di crittografia da usare per connettersi a KDC.</span><span class="sxs-lookup"><span data-stu-id="fa38b-297">Select the encryption algorithm you want to use when connect to KDC.</span></span> <span data-ttu-id="fa38b-298">In genere, è possibile selezionare semplicemente tutte le opzioni.</span><span class="sxs-lookup"><span data-stu-id="fa38b-298">Commonly, you can simply select all the options.</span></span>

        ![Configurare i tipi di crittografia per Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="fa38b-300">Utilizzare il comando **Ksetup** per specificare l'algoritmo di crittografia da usare nell'area di autenticazione specifica.</span><span class="sxs-lookup"><span data-stu-id="fa38b-300">Use **Ksetup** command to specify the encryption algorithm to be used on the specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="fa38b-301">Creare il mapping tra l'account di dominio e l'entità Kerberos per poter usare quest'ultima nel dominio di Windows.</span><span class="sxs-lookup"><span data-stu-id="fa38b-301">Create the mapping between the domain account and Kerberos principal, in order to use Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="fa38b-302">Avviare Strumenti di amministrazione > **Utenti e computer di Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fa38b-302">Start the Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="fa38b-303">Configurare funzionalità avanzate facendo clic su **Visualizza** > **Funzionalità avanzate**.</span><span class="sxs-lookup"><span data-stu-id="fa38b-303">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="fa38b-304">Individuare l'account per cui si desidera creare i mapping e fare clic con il tasto destor del mouse per visualizzare **Mapping nomi**. Fare clic sulla scheda **Nomi Kerberos**. </span><span class="sxs-lookup"><span data-stu-id="fa38b-304">Locate the account to which you want to create mappings, and right-click to view **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="fa38b-305">Aggiungere un'entità dall'area di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="fa38b-305">Add a principal from the realm.</span></span>

        ![Eseguire il mapping di sicurezza e identità](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="fa38b-307">**Nel computer del gateway:**</span><span class="sxs-lookup"><span data-stu-id="fa38b-307">**On gateway machine:**</span></span>

* <span data-ttu-id="fa38b-308">Eseguire i comandi **Ksetup** seguenti per aggiungere una voce di area di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="fa38b-308">Run the following **Ksetup** commands to add a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="fa38b-309">**In Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="fa38b-309">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="fa38b-310">Configurare il connettore HDFS usando **l'autenticazione di Windows** con l'account di dominio o l'entità Kerberos per connettersi all'origine dati HDFS.</span><span class="sxs-lookup"><span data-stu-id="fa38b-310">Configure the HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal to connect to the HDFS data source.</span></span> <span data-ttu-id="fa38b-311">Controllare la sezione [Proprietà del servizio collegato HDFS](#linked-service-properties) per i dettagli di configurazione.</span><span class="sxs-lookup"><span data-stu-id="fa38b-311">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> <span data-ttu-id="fa38b-312">Per eseguire il mapping dal set di dati di origine alle colonne del set di dati sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="fa38b-312">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="performance-and-tuning"></a><span data-ttu-id="fa38b-313">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="fa38b-313">Performance and Tuning</span></span>
<span data-ttu-id="fa38b-314">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="fa38b-314">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
