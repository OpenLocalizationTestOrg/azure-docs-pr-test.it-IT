---
title: dati aaaMove da HDFS locale | Documenti Microsoft
description: Informazioni su come dati toomove da on-premise HDFS usando Azure Data Factory.
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
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="047d5-103">Spostare dati da HDFS locale con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="047d5-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
<span data-ttu-id="047d5-104">Questo articolo spiega come toouse hello attività di copia dei dati toomove Data Factory di Azure da un HDFS locale.</span><span class="sxs-lookup"><span data-stu-id="047d5-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises HDFS.</span></span> <span data-ttu-id="047d5-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="047d5-106">È possibile copiare i dati dall'archivio dati HDFS tooany supportati sink.</span><span class="sxs-lookup"><span data-stu-id="047d5-106">You can copy data from HDFS tooany supported sink data store.</span></span> <span data-ttu-id="047d5-107">Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella.</span><span class="sxs-lookup"><span data-stu-id="047d5-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="047d5-108">Data factory di attualmente supporta solo lo spostamento dei dati da un archivi di dati tooother HDFS locale, ma non per lo spostamento dei dati da altri dati archivi tooan locale HDFS.</span><span class="sxs-lookup"><span data-stu-id="047d5-108">Data factory currently supports only moving data from an on-premises HDFS tooother data stores, but not for moving data from other data stores tooan on-premises HDFS.</span></span>

> [!NOTE]
> <span data-ttu-id="047d5-109">Attività di copia non elimina i file di origine hello dopo che è la destinazione toohello copiati correttamente.</span><span class="sxs-lookup"><span data-stu-id="047d5-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="047d5-110">Se è necessario toodelete file di origine hello dopo una copia ha esito positivo, creare un file di hello toodelete di attività personalizzata e utilizzare attività hello nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="047d5-111">Abilitazione della connettività</span><span class="sxs-lookup"><span data-stu-id="047d5-111">Enabling connectivity</span></span>
<span data-ttu-id="047d5-112">Servizio Data Factory supporta connessione HDFS tooon locale utilizzando hello Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="047d5-112">Data Factory service supports connecting tooon-premises HDFS using hello Data Management Gateway.</span></span> <span data-ttu-id="047d5-113">Vedere [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn articolo sul Gateway di gestione dati e istruzioni dettagliate su come configurare il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="047d5-114">Utilizzare hello gateway tooconnect tooHDFS anche se è ospitato in una macchina virtuale IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="047d5-114">Use hello gateway tooconnect tooHDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="047d5-115">Hello di assicurarsi che Gateway di gestione dati è possibile accedere troppo**tutti** hello [server dei nomi nodo]: [nome porta nodo] e [server dei nodi di dati]: [porta nodo di dati] del cluster Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-115">Make sure hello Data Management Gateway can access too**ALL** hello [name node server]:[name node port] and [data node servers]:[data node port] of hello Hadoop cluster.</span></span> <span data-ttu-id="047d5-116">La [porta del nodo dei nomi] predefinita è 50070 e la [porta del nodo dati] predefinita è 50075.</span><span class="sxs-lookup"><span data-stu-id="047d5-116">Default [name node port] is 50070, and default [data node port] is 50075.</span></span>

<span data-ttu-id="047d5-117">Sebbene sia possibile installare un gateway in hello stesso locale macchina o hello macchina virtuale di Azure come hello HDFS, si consiglia di installare gateway hello in un separato macchina/Azure VM IaaS.</span><span class="sxs-lookup"><span data-stu-id="047d5-117">While you can install gateway on hello same on-premises machine or hello Azure VM as hello HDFS, we recommend that you install hello gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="047d5-118">La presenza del gateway su un computer separato riduce i conflitti di risorse e consente di ottenere prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="047d5-118">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="047d5-119">Quando si installa il gateway hello in un computer separato, macchina hello deve essere in grado di tooaccess macchina di hello con hello HDFS.</span><span class="sxs-lookup"><span data-stu-id="047d5-119">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="047d5-120">introduttiva</span><span class="sxs-lookup"><span data-stu-id="047d5-120">Getting started</span></span>
<span data-ttu-id="047d5-121">È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine HDFS usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="047d5-121">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="047d5-122">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="047d5-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="047d5-123">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="047d5-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="047d5-124">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="047d5-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="047d5-125">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="047d5-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="047d5-126">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="047d5-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="047d5-127">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="047d5-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="047d5-128">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="047d5-129">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="047d5-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="047d5-130">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="047d5-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="047d5-131">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="047d5-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="047d5-132">Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un archivio dati HDFS, vedere [esempio JSON: copiare i dati da tooAzure HDFS locale Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="047d5-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS tooAzure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="047d5-133">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooHDFS:</span><span class="sxs-lookup"><span data-stu-id="047d5-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooHDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="047d5-134">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="047d5-134">Linked service properties</span></span>
<span data-ttu-id="047d5-135">Un servizio collegato di collegare una data factory tooa archivio di dati.</span><span class="sxs-lookup"><span data-stu-id="047d5-135">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="047d5-136">Creare un servizio collegato di tipo **Hdfs** toolink una data factory di tooyour HDFS locale.</span><span class="sxs-lookup"><span data-stu-id="047d5-136">You create a linked service of type **Hdfs** toolink an on-premises HDFS tooyour data factory.</span></span> <span data-ttu-id="047d5-137">Hello nella tabella seguente fornisce una descrizione del servizio specifico tooHDFS collegati gli elementi JSON.</span><span class="sxs-lookup"><span data-stu-id="047d5-137">hello following table provides description for JSON elements specific tooHDFS linked service.</span></span>

| <span data-ttu-id="047d5-138">Proprietà</span><span class="sxs-lookup"><span data-stu-id="047d5-138">Property</span></span> | <span data-ttu-id="047d5-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="047d5-139">Description</span></span> | <span data-ttu-id="047d5-140">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="047d5-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="047d5-141">type</span><span class="sxs-lookup"><span data-stu-id="047d5-141">type</span></span> |<span data-ttu-id="047d5-142">proprietà di tipo Hello deve essere impostata su: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="047d5-142">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="047d5-143">Sì</span><span class="sxs-lookup"><span data-stu-id="047d5-143">Yes</span></span> |
| <span data-ttu-id="047d5-144">Url</span><span class="sxs-lookup"><span data-stu-id="047d5-144">Url</span></span> |<span data-ttu-id="047d5-145">URL toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="047d5-145">URL toohello HDFS</span></span> |<span data-ttu-id="047d5-146">Sì</span><span class="sxs-lookup"><span data-stu-id="047d5-146">Yes</span></span> |
| <span data-ttu-id="047d5-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="047d5-147">authenticationType</span></span> |<span data-ttu-id="047d5-148">Anonima o Windows.</span><span class="sxs-lookup"><span data-stu-id="047d5-148">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="047d5-149">toouse **l'autenticazione Kerberos** per connettore HDFS, fare riferimento troppo[in questa sezione](#use-kerberos-authentication-for-hdfs-connector) tooset l'ambiente locale di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="047d5-149">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="047d5-150">Sì</span><span class="sxs-lookup"><span data-stu-id="047d5-150">Yes</span></span> |
| <span data-ttu-id="047d5-151">userName</span><span class="sxs-lookup"><span data-stu-id="047d5-151">userName</span></span> |<span data-ttu-id="047d5-152">Nome utente per l'autenticazione di Windows</span><span class="sxs-lookup"><span data-stu-id="047d5-152">Username for Windows authentication.</span></span> |<span data-ttu-id="047d5-153">Sì (per l'autenticazione di Windows)</span><span class="sxs-lookup"><span data-stu-id="047d5-153">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="047d5-154">password</span><span class="sxs-lookup"><span data-stu-id="047d5-154">password</span></span> |<span data-ttu-id="047d5-155">Password per l'autenticazione di Windows</span><span class="sxs-lookup"><span data-stu-id="047d5-155">Password for Windows authentication.</span></span> |<span data-ttu-id="047d5-156">Sì (per l'autenticazione di Windows)</span><span class="sxs-lookup"><span data-stu-id="047d5-156">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="047d5-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="047d5-157">gatewayName</span></span> |<span data-ttu-id="047d5-158">Nome del gateway hello hello servizio Data Factory deve usare tooconnect toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="047d5-158">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="047d5-159">Sì</span><span class="sxs-lookup"><span data-stu-id="047d5-159">Yes</span></span> |
| <span data-ttu-id="047d5-160">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="047d5-160">encryptedCredential</span></span> |<span data-ttu-id="047d5-161">[Nuovo AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output delle credenziali di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="047d5-162">No</span><span class="sxs-lookup"><span data-stu-id="047d5-162">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="047d5-163">Uso dell'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="047d5-163">Using Anonymous authentication</span></span>

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

### <a name="using-windows-authentication"></a><span data-ttu-id="047d5-164">Uso dell'autenticazione di Windows</span><span class="sxs-lookup"><span data-stu-id="047d5-164">Using Windows authentication</span></span>

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
## <a name="dataset-properties"></a><span data-ttu-id="047d5-165">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="047d5-165">Dataset properties</span></span>
<span data-ttu-id="047d5-166">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="047d5-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="047d5-167">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="047d5-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="047d5-168">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="047d5-169">sezione Hello typeProperties per set di dati di tipo **FileShare** (che include set di dati HDFS) ha le proprietà seguenti hello</span><span class="sxs-lookup"><span data-stu-id="047d5-169">hello typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has hello following properties</span></span>

| <span data-ttu-id="047d5-170">Proprietà</span><span class="sxs-lookup"><span data-stu-id="047d5-170">Property</span></span> | <span data-ttu-id="047d5-171">Descrizione</span><span class="sxs-lookup"><span data-stu-id="047d5-171">Description</span></span> | <span data-ttu-id="047d5-172">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="047d5-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="047d5-173">folderPath</span><span class="sxs-lookup"><span data-stu-id="047d5-173">folderPath</span></span> |<span data-ttu-id="047d5-174">Cartella toohello percorso.</span><span class="sxs-lookup"><span data-stu-id="047d5-174">Path toohello folder.</span></span> <span data-ttu-id="047d5-175">Esempio: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="047d5-175">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="047d5-176">Utilizzare il carattere di escape ' \ ' per i caratteri speciali nella stringa hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-176">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="047d5-177">Ad esempio: per cartella\sottocartella specificare cartella\\\\sottocartella e per d:\cartellaesempio specificare l'unità d:\\\\cartellaesempio.</span><span class="sxs-lookup"><span data-stu-id="047d5-177">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="047d5-178">È possibile combinare questa proprietà con **partitionBy** toohave i percorsi delle cartelle in base a intervallo iniziale o finale data e ora.</span><span class="sxs-lookup"><span data-stu-id="047d5-178">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="047d5-179">Sì</span><span class="sxs-lookup"><span data-stu-id="047d5-179">Yes</span></span> |
| <span data-ttu-id="047d5-180">fileName</span><span class="sxs-lookup"><span data-stu-id="047d5-180">fileName</span></span> |<span data-ttu-id="047d5-181">Specificare il nome di hello del file hello in hello **folderPath** se si desidera hello tabella toorefer tooa specifici file nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-181">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="047d5-182">Se non si specifica alcun valore per questa proprietà, la tabella hello punta tooall file nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-182">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="047d5-183">Quando il nome di file non viene specificato per un set di dati di output, il nome di hello del file hello generato sarebbe in hello segue questo formato:</span><span class="sxs-lookup"><span data-stu-id="047d5-183">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="047d5-184">Data<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="047d5-184">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="047d5-185">No</span><span class="sxs-lookup"><span data-stu-id="047d5-185">No</span></span> |
| <span data-ttu-id="047d5-186">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="047d5-186">partitionedBy</span></span> |<span data-ttu-id="047d5-187">partitionedBy può essere utilizzato toospecify un folderPath dinamica, il nome file per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="047d5-187">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="047d5-188">Ad esempio, folderPath con parametri per ogni ora di dati.</span><span class="sxs-lookup"><span data-stu-id="047d5-188">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="047d5-189">No</span><span class="sxs-lookup"><span data-stu-id="047d5-189">No</span></span> |
| <span data-ttu-id="047d5-190">format</span><span class="sxs-lookup"><span data-stu-id="047d5-190">format</span></span> | <span data-ttu-id="047d5-191">è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="047d5-191">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="047d5-192">Set hello **tipo** proprietà in formato tooone di questi valori.</span><span class="sxs-lookup"><span data-stu-id="047d5-192">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="047d5-193">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="047d5-193">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="047d5-194">Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="047d5-194">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="047d5-195">No</span><span class="sxs-lookup"><span data-stu-id="047d5-195">No</span></span> |
| <span data-ttu-id="047d5-196">compressione</span><span class="sxs-lookup"><span data-stu-id="047d5-196">compression</span></span> | <span data-ttu-id="047d5-197">Specificare il tipo di hello e livello di compressione per dati hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-197">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="047d5-198">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="047d5-198">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="047d5-199">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="047d5-199">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="047d5-200">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="047d5-200">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="047d5-201">No</span><span class="sxs-lookup"><span data-stu-id="047d5-201">No</span></span> |

> [!NOTE]
> <span data-ttu-id="047d5-202">filename e fileFilter non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="047d5-202">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="047d5-203">Uso della proprietà partionedBy</span><span class="sxs-lookup"><span data-stu-id="047d5-203">Using partionedBy property</span></span>
<span data-ttu-id="047d5-204">Come indicato nella sezione precedente di hello, è possibile specificare un folderPath dinamico e il nome di dati della serie temporale con hello **partitionedBy** proprietà [funzioni di Data Factory e le variabili di sistema hello](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="047d5-204">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="047d5-205">toolearn ulteriori informazioni sui set di dati serie ora, la pianificazione e le sezioni, vedere [la creazione di DataSet](data-factory-create-datasets.md), [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md), e [la creazione di pipeline](data-factory-create-pipelines.md) articoli.</span><span class="sxs-lookup"><span data-stu-id="047d5-205">toolearn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="047d5-206">Esempio 1.</span><span class="sxs-lookup"><span data-stu-id="047d5-206">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="047d5-207">In questo esempio {Slice} viene sostituito con valore hello della variabile di sistema di Data Factory SliceStart nel formato hello (YYYYMMDDHH) specificato.</span><span class="sxs-lookup"><span data-stu-id="047d5-207">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="047d5-208">Hello SliceStart fa riferimento l'ora toostart sezione hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-208">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="047d5-209">Hello folderPath è diversa per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="047d5-209">hello folderPath is different for each slice.</span></span> <span data-ttu-id="047d5-210">Ad esempio: wikisampledataout/wikidatagateway/2014100103 o wikisampledataout/wikidatagateway/2014100104.</span><span class="sxs-lookup"><span data-stu-id="047d5-210">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="047d5-211">Esempio 2:</span><span class="sxs-lookup"><span data-stu-id="047d5-211">Sample 2:</span></span>

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
<span data-ttu-id="047d5-212">In questo esempio l'anno, il mese, il giorno e l'ora di SliceStart vengono estratti in variabili separate che vengono usate dalle proprietà folderPath e fileName.</span><span class="sxs-lookup"><span data-stu-id="047d5-212">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="047d5-213">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="047d5-213">Copy activity properties</span></span>
<span data-ttu-id="047d5-214">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="047d5-214">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="047d5-215">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="047d5-215">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="047d5-216">Mentre le proprietà disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="047d5-216">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="047d5-217">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="047d5-217">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="047d5-218">Per attività di copia, l'origine è di tipo **FileSystemSource** hello le proprietà seguenti sono disponibile nella sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="047d5-218">For Copy Activity, when source is of type **FileSystemSource** hello following properties are available in typeProperties section:</span></span>

<span data-ttu-id="047d5-219">**FileSystemSource** supporta hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="047d5-219">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="047d5-220">Proprietà</span><span class="sxs-lookup"><span data-stu-id="047d5-220">Property</span></span> | <span data-ttu-id="047d5-221">Descrizione</span><span class="sxs-lookup"><span data-stu-id="047d5-221">Description</span></span> | <span data-ttu-id="047d5-222">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="047d5-222">Allowed values</span></span> | <span data-ttu-id="047d5-223">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="047d5-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="047d5-224">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="047d5-224">recursive</span></span> |<span data-ttu-id="047d5-225">Indica se hello i dati letti in modo ricorsivo dal sottocartelle hello o solo dalla cartella specificata hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-225">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="047d5-226">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="047d5-226">True, False (default)</span></span> |<span data-ttu-id="047d5-227">No</span><span class="sxs-lookup"><span data-stu-id="047d5-227">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="047d5-228">Formati di file e di compressione supportati</span><span class="sxs-lookup"><span data-stu-id="047d5-228">Supported file and compression formats</span></span>
<span data-ttu-id="047d5-229">Per i dettagli, vedere l'articolo relativo ai [file e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="047d5-229">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a><span data-ttu-id="047d5-230">Esempio JSON: copiare i dati da tooAzure HDFS locale Blob</span><span class="sxs-lookup"><span data-stu-id="047d5-230">JSON example: Copy data from on-premises HDFS tooAzure Blob</span></span>
<span data-ttu-id="047d5-231">Questo esempio viene illustrato come toocopy dati da un tooAzure HDFS locale nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="047d5-231">This sample shows how toocopy data from an on-premises HDFS tooAzure Blob Storage.</span></span> <span data-ttu-id="047d5-232">Tuttavia, i dati possono essere copiati **direttamente** tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="047d5-232">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="047d5-233">esempio Hello fornisce definizioni di JSON per hello seguenti entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="047d5-233">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="047d5-234">È possibile utilizzare questi toocreate definizioni una pipeline di dati da HDFS tooAzure nell'archiviazione Blob toocopy utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="047d5-234">You can use these definitions toocreate a pipeline toocopy data from HDFS tooAzure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="047d5-235">Un servizio collegato di tipo [OnPremisesHdfs](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="047d5-235">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="047d5-236">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="047d5-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="047d5-237">Un [set di dati](data-factory-create-datasets.md) di input di tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="047d5-237">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="047d5-238">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="047d5-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="047d5-239">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="047d5-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="047d5-240">esempio Hello copia dati da un tooan HDFS locale blob di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="047d5-240">hello sample copies data from an on-premises HDFS tooan Azure blob every hour.</span></span> <span data-ttu-id="047d5-241">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-241">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="047d5-242">Innanzitutto, configurare il gateway di gestione dati hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-242">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="047d5-243">Hello istruzioni hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="047d5-243">hello instructions in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="047d5-244">**Servizio collegato HDFS:** in questo esempio viene utilizzata l'autenticazione di Windows di hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-244">**HDFS linked service:** This example uses hello Windows authentication.</span></span> <span data-ttu-id="047d5-245">Per i diversi tipi di autenticazione disponibili, vedere la sezione [Proprietà del servizio collegato HDFS](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="047d5-245">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="047d5-246">**Servizio collegato Archiviazione di Azure:**</span><span class="sxs-lookup"><span data-stu-id="047d5-246">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="047d5-247">**Set di dati di input HDFS:** questo set di dati si riferisce cartella HDFS toohello DataTransfer/UnitTest /.</span><span class="sxs-lookup"><span data-stu-id="047d5-247">**HDFS input dataset:** This dataset refers toohello HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="047d5-248">pipeline Hello copia tutti i file hello toohello questa cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="047d5-248">hello pipeline copies all hello files in this folder toohello destination.</span></span>

<span data-ttu-id="047d5-249">L'impostazione "external": "true" informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-249">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="047d5-250">**Set di dati di output del BLOB di Azure:**</span><span class="sxs-lookup"><span data-stu-id="047d5-250">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="047d5-251">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="047d5-251">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="047d5-252">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="047d5-252">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="047d5-253">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-253">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="047d5-254">**Un'attività di copia in una pipeline con un'origine su file system e un sink BLOB:**</span><span class="sxs-lookup"><span data-stu-id="047d5-254">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="047d5-255">pipeline di Hello contiene un'attività di copia che è configurato toouse questi set di dati di input e output e toorun pianificato ogni ora.</span><span class="sxs-lookup"><span data-stu-id="047d5-255">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="047d5-256">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**FileSystemSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="047d5-256">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="047d5-257">query SQL Hello specificata per hello **query** proprietà consente di selezionare dati hello hello oltre toocopy ora.</span><span class="sxs-lookup"><span data-stu-id="047d5-257">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="047d5-258">Uso dell'autenticazione Kerberos per il connettore HDFS</span><span class="sxs-lookup"><span data-stu-id="047d5-258">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="047d5-259">Esistono due opzioni tooset backup hello nell'ambiente locale in modo da toouse l'autenticazione Kerberos nel connettore HDFS.</span><span class="sxs-lookup"><span data-stu-id="047d5-259">There are two options tooset up hello on-premises environment so as toouse Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="047d5-260">È possibile scegliere hello uno meglio si adatta al caso.</span><span class="sxs-lookup"><span data-stu-id="047d5-260">You can choose hello one better fits your case.</span></span>
* <span data-ttu-id="047d5-261">Opzione 1: [aggiungere un computer gateway all'area di autenticazione di Kerberos](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="047d5-261">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="047d5-262">Opzione 2: [Abilitare il trust reciproco tra il dominio di Windows e l'area di autenticazione di Kerberos](#kerberos-mutual-trust)</span><span class="sxs-lookup"><span data-stu-id="047d5-262">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <span data-ttu-id="047d5-263"><a name="kerberos-join-realm"></a>Opzione 1: aggiungere un computer gateway all'area di autenticazione di Kerberos</span><span class="sxs-lookup"><span data-stu-id="047d5-263"><a name="kerberos-join-realm"></a>Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="047d5-264">Requisito:</span><span class="sxs-lookup"><span data-stu-id="047d5-264">Requirement:</span></span>

* <span data-ttu-id="047d5-265">computer del gateway Hello necessita di autenticazione Kerberos hello toojoin e non può partecipare a qualsiasi dominio di Windows.</span><span class="sxs-lookup"><span data-stu-id="047d5-265">hello gateway machine needs toojoin hello Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="047d5-266">Come tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="047d5-266">How tooconfigure:</span></span>

<span data-ttu-id="047d5-267">**Nel computer del gateway:**</span><span class="sxs-lookup"><span data-stu-id="047d5-267">**On gateway machine:**</span></span>

1.  <span data-ttu-id="047d5-268">Eseguire hello **che Ksetup** tooconfigure utilità hello server Kerberos KDC e area di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="047d5-268">Run hello **Ksetup** utility tooconfigure hello Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="047d5-269">computer di Hello deve essere configurato come membro del gruppo di lavoro poiché un'area di autenticazione Kerberos è diversa da un dominio di Windows.</span><span class="sxs-lookup"><span data-stu-id="047d5-269">hello machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="047d5-270">Ciò può essere ottenuto impostando l'area di autenticazione Kerberos hello e aggiungendo un server KDC come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="047d5-270">This can be achieved by setting hello Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="047d5-271">Sostituire *REALM.COM* con la propria area di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="047d5-271">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="047d5-272">**Riavviare** macchina hello dopo l'esecuzione di questi 2 comandi.</span><span class="sxs-lookup"><span data-stu-id="047d5-272">**Restart** hello machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="047d5-273">Verificare la configurazione di hello con **che Ksetup** comando.</span><span class="sxs-lookup"><span data-stu-id="047d5-273">Verify hello configuration with **Ksetup** command.</span></span> <span data-ttu-id="047d5-274">output di Hello deve essere ad esempio:</span><span class="sxs-lookup"><span data-stu-id="047d5-274">hello output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="047d5-275">**In Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="047d5-275">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="047d5-276">Configurazione connettore di hello HDFS mediante **l'autenticazione di Windows** con Kerberos principale nome e la password tooconnect toohello HDFS origine dati.</span><span class="sxs-lookup"><span data-stu-id="047d5-276">Configure hello HDFS connector using **Windows authentication** together with your Kerberos principal name and password tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="047d5-277">Controllare la sezione [Proprietà del servizio collegato HDFS](#linked-service-properties) per i dettagli di configurazione.</span><span class="sxs-lookup"><span data-stu-id="047d5-277">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <span data-ttu-id="047d5-278"><a name="kerberos-mutual-trust"></a>Opzione 2: Abilitare il trust reciproco tra il dominio di Windows e l'area di autenticazione di Kerberos</span><span class="sxs-lookup"><span data-stu-id="047d5-278"><a name="kerberos-mutual-trust"></a>Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="047d5-279">Requisito:</span><span class="sxs-lookup"><span data-stu-id="047d5-279">Requirement:</span></span>
*   <span data-ttu-id="047d5-280">computer del gateway Hello è necessario aggiungere un dominio Windows.</span><span class="sxs-lookup"><span data-stu-id="047d5-280">hello gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="047d5-281">Sono necessarie impostazioni di autorizzazione tooupdate hello controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="047d5-281">You need permission tooupdate hello domain controller's settings.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="047d5-282">Come tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="047d5-282">How tooconfigure:</span></span>

> [!NOTE]
> <span data-ttu-id="047d5-283">Sostituire area-di autenticazione.com e AD.COM hello segue l'esercitazione con il propria rispettivo area di autenticazione e controller di dominio in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="047d5-283">Replace REALM.COM and AD.COM in hello following tutorial with your own respective realm and domain controller as needed.</span></span>

<span data-ttu-id="047d5-284">**Nel server KDC:**</span><span class="sxs-lookup"><span data-stu-id="047d5-284">**On KDC server:**</span></span>

1.  <span data-ttu-id="047d5-285">Modifica configurazione KDC hello in **krb5** toolet file KDC di considerare attendibile il dominio di Windows che fa riferimento toohello seguente modello di configurazione.</span><span class="sxs-lookup"><span data-stu-id="047d5-285">Edit hello KDC configuration in **krb5.conf** file toolet KDC trust Windows Domain referring toohello following configuration template.</span></span> <span data-ttu-id="047d5-286">Per impostazione predefinita, si trova in configurazione hello **/etc/krb5.conf**.</span><span class="sxs-lookup"><span data-stu-id="047d5-286">By default, hello configuration is located at **/etc/krb5.conf**.</span></span>

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

  <span data-ttu-id="047d5-287">**Riavviare** hello servizio KDC dopo la configurazione.</span><span class="sxs-lookup"><span data-stu-id="047d5-287">**Restart** hello KDC service after configuration.</span></span>

2.  <span data-ttu-id="047d5-288">Preparare un'entità denominata  **krbtgt/REALM.COM@AD.COM**  in server KDC con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="047d5-288">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with hello following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="047d5-289">Nel file di configurazione del servizio HDFS **hadoop.security.auth_to_local** aggiungere `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span><span class="sxs-lookup"><span data-stu-id="047d5-289">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="047d5-290">**Nel controller di dominio:**</span><span class="sxs-lookup"><span data-stu-id="047d5-290">**On domain controller:**</span></span>

1.  <span data-ttu-id="047d5-291">Eseguire il seguente hello **che Ksetup** comandi tooadd una voce dell'area di autenticazione:</span><span class="sxs-lookup"><span data-stu-id="047d5-291">Run hello following **Ksetup** commands tooadd a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="047d5-292">Stabilire relazioni di trust dal dominio di Windows tooKerberos dell'area di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="047d5-292">Establish trust from Windows Domain tooKerberos Realm.</span></span> <span data-ttu-id="047d5-293">[password] è hello per le entità di hello  **krbtgt/REALM.COM@AD.COM** .</span><span class="sxs-lookup"><span data-stu-id="047d5-293">[password] is hello password for hello principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="047d5-294">Selezionare l'algoritmo di crittografia usato in Kerberos.</span><span class="sxs-lookup"><span data-stu-id="047d5-294">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="047d5-295">Passare tooServer Manager > Gestione criteri di gruppo > dominio > oggetti Criteri di gruppo > predefinito o criteri di dominio Active e modifica.</span><span class="sxs-lookup"><span data-stu-id="047d5-295">Go tooServer Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="047d5-296">In hello **Editor Gestione criteri di gruppo** finestra popup, andare tooComputer configurazione > Criteri > Impostazioni di Windows > Impostazioni di sicurezza > Criteri locali > Opzioni di sicurezza e configurare **rete sicurezza: configurare i tipi di crittografia consentiti per Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="047d5-296">In hello **Group Policy Management Editor** popup window, go tooComputer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="047d5-297">Algoritmo di crittografia hello selezionare da toouse tooKDC quando esegue la connessione.</span><span class="sxs-lookup"><span data-stu-id="047d5-297">Select hello encryption algorithm you want toouse when connect tooKDC.</span></span> <span data-ttu-id="047d5-298">In genere, è possibile selezionare semplicemente tutte le opzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-298">Commonly, you can simply select all hello options.</span></span>

        ![Configurare i tipi di crittografia per Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="047d5-300">Utilizzare **che Ksetup** comando toospecify hello crittografia algoritmo toobe utilizzato su hello specifico dell'area di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="047d5-300">Use **Ksetup** command toospecify hello encryption algorithm toobe used on hello specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="047d5-301">Creare mapping hello tra account di dominio hello e Kerberos dell'entità, in ordine toouse Kerberos dell'entità di dominio di Windows.</span><span class="sxs-lookup"><span data-stu-id="047d5-301">Create hello mapping between hello domain account and Kerberos principal, in order toouse Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="047d5-302">Avviare strumenti di amministrazione di hello > **Active Directory Users and Computers**.</span><span class="sxs-lookup"><span data-stu-id="047d5-302">Start hello Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="047d5-303">Configurare funzionalità avanzate facendo clic su **Visualizza** > **Funzionalità avanzate**.</span><span class="sxs-lookup"><span data-stu-id="047d5-303">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="047d5-304">Individuare hello account toowhich toocreate mapping desiderato e fare doppio clic su tooview **i mapping dei nomi** > fare clic su **nomi Kerberos** scheda.</span><span class="sxs-lookup"><span data-stu-id="047d5-304">Locate hello account toowhich you want toocreate mappings, and right-click tooview **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="047d5-305">Aggiungere un'entità dall'area di autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="047d5-305">Add a principal from hello realm.</span></span>

        ![Eseguire il mapping di sicurezza e identità](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="047d5-307">**Nel computer del gateway:**</span><span class="sxs-lookup"><span data-stu-id="047d5-307">**On gateway machine:**</span></span>

* <span data-ttu-id="047d5-308">Eseguire il seguente hello **che Ksetup** comandi tooadd una voce dell'area di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="047d5-308">Run hello following **Ksetup** commands tooadd a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="047d5-309">**In Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="047d5-309">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="047d5-310">Configurazione connettore di hello HDFS mediante **l'autenticazione di Windows** con Account di dominio o l'origine dati di entità Kerberos tooconnect toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="047d5-310">Configure hello HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="047d5-311">Controllare la sezione [Proprietà del servizio collegato HDFS](#linked-service-properties) per i dettagli di configurazione.</span><span class="sxs-lookup"><span data-stu-id="047d5-311">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> <span data-ttu-id="047d5-312">colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="047d5-312">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="performance-and-tuning"></a><span data-ttu-id="047d5-313">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="047d5-313">Performance and Tuning</span></span>
<span data-ttu-id="047d5-314">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="047d5-314">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
