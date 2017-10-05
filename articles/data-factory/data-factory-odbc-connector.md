---
title: Spostare dati da archivi dati ODBC | Documentazione Microsoft
description: Informazioni su come spostare dati da archivi dati ODBC con Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 269d9802ca4a6a16dbf9021929fe21104cb431f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="d22ed-103">Spostare dati da archivi dati ODBC con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d22ed-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="d22ed-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da un archivio dati ODBC locale.</span><span class="sxs-lookup"><span data-stu-id="d22ed-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises ODBC data store.</span></span> <span data-ttu-id="d22ed-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="d22ed-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="d22ed-106">È possibile copiare dati da un archivio dati ODBC a qualsiasi archivio dati di sink supportato.</span><span class="sxs-lookup"><span data-stu-id="d22ed-106">You can copy data from an ODBC data store to any supported sink data store.</span></span> <span data-ttu-id="d22ed-107">Per un elenco degli archivi dati supportati come sink dall'attività di copia, vedere la tabella relativa agli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="d22ed-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="d22ed-108">Data Factory supporta attualmente solo lo spostamento dei dati da un archivio dati ODBC ad altri archivi dati, ma non da altri archivi dati a un archivio dati ODBC.</span><span class="sxs-lookup"><span data-stu-id="d22ed-108">Data factory currently supports only moving data from an ODBC data store to other data stores, but not for moving data from other data stores to an ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="d22ed-109">Abilitazione della connettività</span><span class="sxs-lookup"><span data-stu-id="d22ed-109">Enabling connectivity</span></span>
<span data-ttu-id="d22ed-110">Il servizio Data Factory supporta la connessione a origini ODBC locali tramite il Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="d22ed-110">Data Factory service supports connecting to on-premises ODBC sources using the Data Management Gateway.</span></span> <span data-ttu-id="d22ed-111">Vedere l'articolo sullo [spostamento di dati tra sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) per informazioni sul Gateway di gestione dati e per istruzioni dettagliate sulla configurazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="d22ed-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="d22ed-112">Usare il gateway per connettersi a un archivio dati ODBC anche se è ospitato in una macchina virtuale IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="d22ed-112">Use the gateway to connect to an ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="d22ed-113">È possibile installare il gateway nello stesso computer locale o macchina virtuale di Azure come archivio dati ODBC.</span><span class="sxs-lookup"><span data-stu-id="d22ed-113">You can install the gateway on the same on-premises machine or the Azure VM as the ODBC data store.</span></span> <span data-ttu-id="d22ed-114">Tuttavia, è consigliabile installare il gateway in un computer/macchina virtuale Iaas di Azure separati per evitare conflitti tra le risorse e ottenere prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="d22ed-114">However, we recommend that you install the gateway on a separate machine/Azure IaaS VM to avoid resource contention and for better performance.</span></span> <span data-ttu-id="d22ed-115">Quando si installa il gateway in un computer separato, questo deve poter accedere al computer l'archivio dati ODBC.</span><span class="sxs-lookup"><span data-stu-id="d22ed-115">When you install the gateway on a separate machine, the machine should be able to access the machine with the ODBC data store.</span></span>

<span data-ttu-id="d22ed-116">Oltre a Gateway di gestione dati, è necessario installare anche il driver ODBC per l'archivio dati nel computer del gateway.</span><span class="sxs-lookup"><span data-stu-id="d22ed-116">Apart from the Data Management Gateway, you also need to install the ODBC driver for the data store on the gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="d22ed-117">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="d22ed-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d22ed-118">Introduzione</span><span class="sxs-lookup"><span data-stu-id="d22ed-118">Getting started</span></span>
<span data-ttu-id="d22ed-119">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati ODBC usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="d22ed-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="d22ed-120">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="d22ed-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="d22ed-121">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="d22ed-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="d22ed-122">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="d22ed-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d22ed-123">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="d22ed-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="d22ed-124">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="d22ed-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="d22ed-125">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="d22ed-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="d22ed-126">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="d22ed-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="d22ed-127">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="d22ed-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="d22ed-128">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d22ed-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="d22ed-129">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di data factory.</span><span class="sxs-lookup"><span data-stu-id="d22ed-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="d22ed-130">Per un esempio con definizioni JSON per entità di data factory utilizzate per copiare dati da un archivio dati ODBC, vedere la sezione [Esempio JSON: Copiare dati da un archivio dati ODBC al BLOB di Azure](#json-example-copy-data-from-odbc-data-store-to-azure-blob) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d22ed-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an ODBC data store, see [JSON example: Copy data from ODBC data store to Azure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="d22ed-131">Nelle sezioni seguenti sono riportate le informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di data factory specifiche di un archivio dati ODBC:</span><span class="sxs-lookup"><span data-stu-id="d22ed-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to ODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d22ed-132">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="d22ed-132">Linked service properties</span></span>
<span data-ttu-id="d22ed-133">La tabella seguente contiene le descrizioni degli elementi JSON specifici del servizio collegato ODBC.</span><span class="sxs-lookup"><span data-stu-id="d22ed-133">The following table provides description for JSON elements specific to ODBC linked service.</span></span>

| <span data-ttu-id="d22ed-134">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d22ed-134">Property</span></span> | <span data-ttu-id="d22ed-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d22ed-135">Description</span></span> | <span data-ttu-id="d22ed-136">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d22ed-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d22ed-137">type</span><span class="sxs-lookup"><span data-stu-id="d22ed-137">type</span></span> |<span data-ttu-id="d22ed-138">La proprietà type deve essere impostata su: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="d22ed-138">The type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="d22ed-139">Sì</span><span class="sxs-lookup"><span data-stu-id="d22ed-139">Yes</span></span> |
| <span data-ttu-id="d22ed-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="d22ed-140">connectionString</span></span> |<span data-ttu-id="d22ed-141">La parte delle credenziali non di accesso della stringa di connessione e una credenziale crittografata facoltativa.</span><span class="sxs-lookup"><span data-stu-id="d22ed-141">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="d22ed-142">Vedere gli esempi nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="d22ed-142">See examples in the following sections.</span></span> |<span data-ttu-id="d22ed-143">Sì</span><span class="sxs-lookup"><span data-stu-id="d22ed-143">Yes</span></span> |
| <span data-ttu-id="d22ed-144">credential</span><span class="sxs-lookup"><span data-stu-id="d22ed-144">credential</span></span> |<span data-ttu-id="d22ed-145">La parte delle credenziali di accesso della stringa di connessione specificata nel formato di valore della proprietà specifico del driver.</span><span class="sxs-lookup"><span data-stu-id="d22ed-145">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="d22ed-146">Esempio: "Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;".</span><span class="sxs-lookup"><span data-stu-id="d22ed-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="d22ed-147">No</span><span class="sxs-lookup"><span data-stu-id="d22ed-147">No</span></span> |
| <span data-ttu-id="d22ed-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="d22ed-148">authenticationType</span></span> |<span data-ttu-id="d22ed-149">Tipo di autenticazione usato per connettersi all'archivio dati ODBC.</span><span class="sxs-lookup"><span data-stu-id="d22ed-149">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="d22ed-150">I valori possibili sono: anonima e di base.</span><span class="sxs-lookup"><span data-stu-id="d22ed-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="d22ed-151">Sì</span><span class="sxs-lookup"><span data-stu-id="d22ed-151">Yes</span></span> |
| <span data-ttu-id="d22ed-152">username</span><span class="sxs-lookup"><span data-stu-id="d22ed-152">username</span></span> |<span data-ttu-id="d22ed-153">Specificare il nome utente se si usa l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="d22ed-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="d22ed-154">No</span><span class="sxs-lookup"><span data-stu-id="d22ed-154">No</span></span> |
| <span data-ttu-id="d22ed-155">password</span><span class="sxs-lookup"><span data-stu-id="d22ed-155">password</span></span> |<span data-ttu-id="d22ed-156">Specificare la password per l'account utente specificato per il nome utente.</span><span class="sxs-lookup"><span data-stu-id="d22ed-156">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="d22ed-157">No</span><span class="sxs-lookup"><span data-stu-id="d22ed-157">No</span></span> |
| <span data-ttu-id="d22ed-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d22ed-158">gatewayName</span></span> |<span data-ttu-id="d22ed-159">Nome del gateway che il servizio Data Factory deve usare per connettersi all'archivio dati ODBC.</span><span class="sxs-lookup"><span data-stu-id="d22ed-159">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="d22ed-160">Sì</span><span class="sxs-lookup"><span data-stu-id="d22ed-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="d22ed-161">Uso dell'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="d22ed-161">Using Basic authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="d22ed-162">Uso dell'autenticazione di base con credenziali crittografate</span><span class="sxs-lookup"><span data-stu-id="d22ed-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="d22ed-163">È possibile crittografare le credenziali usando il cmdlet [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx), in Azure PowerShell versione 1.0, oppure [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx), in Azure PowerShell versione 0.9 o precedente.</span><span class="sxs-lookup"><span data-stu-id="d22ed-163">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="d22ed-164">Uso dell'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="d22ed-164">Using Anonymous authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a><span data-ttu-id="d22ed-165">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="d22ed-165">Dataset properties</span></span>
<span data-ttu-id="d22ed-166">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="d22ed-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d22ed-167">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="d22ed-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="d22ed-168">La sezione **typeProperties** è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="d22ed-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="d22ed-169">La sezione typeProperties per il set di dati di tipo **RelationalTable** , che include il set di dati ODBC, presenta le proprietà seguenti</span><span class="sxs-lookup"><span data-stu-id="d22ed-169">The typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has the following properties</span></span>

| <span data-ttu-id="d22ed-170">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d22ed-170">Property</span></span> | <span data-ttu-id="d22ed-171">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d22ed-171">Description</span></span> | <span data-ttu-id="d22ed-172">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d22ed-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d22ed-173">tableName</span><span class="sxs-lookup"><span data-stu-id="d22ed-173">tableName</span></span> |<span data-ttu-id="d22ed-174">Nome della tabella nell'archivio dati ODBC.</span><span class="sxs-lookup"><span data-stu-id="d22ed-174">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="d22ed-175">Sì</span><span class="sxs-lookup"><span data-stu-id="d22ed-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="d22ed-176">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="d22ed-176">Copy activity properties</span></span>
<span data-ttu-id="d22ed-177">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="d22ed-177">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d22ed-178">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="d22ed-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="d22ed-179">D'altra parte, le proprietà disponibili nella sezione **typeProperties** dell'attività variano in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="d22ed-179">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="d22ed-180">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="d22ed-180">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="d22ed-181">Nell'attività di copia con origine di tipo **RelationalSource** , incluso ODBC, sono disponibili le proprietà seguenti nella sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="d22ed-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="d22ed-182">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d22ed-182">Property</span></span> | <span data-ttu-id="d22ed-183">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d22ed-183">Description</span></span> | <span data-ttu-id="d22ed-184">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="d22ed-184">Allowed values</span></span> | <span data-ttu-id="d22ed-185">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d22ed-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d22ed-186">query</span><span class="sxs-lookup"><span data-stu-id="d22ed-186">query</span></span> |<span data-ttu-id="d22ed-187">Usare la query personalizzata per leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="d22ed-187">Use the custom query to read data.</span></span> |<span data-ttu-id="d22ed-188">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="d22ed-188">SQL query string.</span></span> <span data-ttu-id="d22ed-189">Ad esempio: selezionare * da MyTable.</span><span class="sxs-lookup"><span data-stu-id="d22ed-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="d22ed-190">Sì</span><span class="sxs-lookup"><span data-stu-id="d22ed-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-to-azure-blob"></a><span data-ttu-id="d22ed-191">Esempio JSON: Copiare dati da un archivio dati ODBC al BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="d22ed-191">JSON example: Copy data from ODBC data store to Azure Blob</span></span>
<span data-ttu-id="d22ed-192">Questo esempio fornisce le definizioni JSON da usare per creare una pipeline con il [Portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d22ed-192">This example provides JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d22ed-193">Illustra come copiare dati da un'origine ODBC in un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="d22ed-193">It shows how to copy data from an ODBC source to an Azure Blob Storage.</span></span> <span data-ttu-id="d22ed-194">Tuttavia, i dati possono essere copiati in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d22ed-194">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="d22ed-195">L'esempio include le entità di Data factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="d22ed-195">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="d22ed-196">Un servizio collegato di tipo [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d22ed-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="d22ed-197">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d22ed-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d22ed-198">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d22ed-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="d22ed-199">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d22ed-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="d22ed-200">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d22ed-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d22ed-201">L'esempio copia i dati dai risultati della query in un archivio dati ODBC a un BLOB ogni ora.</span><span class="sxs-lookup"><span data-stu-id="d22ed-201">The sample copies data from a query result in an ODBC data store to a blob every hour.</span></span> <span data-ttu-id="d22ed-202">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="d22ed-202">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="d22ed-203">Come primo passaggio, impostare il gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="d22ed-203">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="d22ed-204">Le istruzioni sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="d22ed-204">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="d22ed-205">**Servizio collegato ODBC** : questo esempio usa l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="d22ed-205">**ODBC linked service** This example uses the Basic authentication.</span></span> <span data-ttu-id="d22ed-206">Per i diversi tipi di autenticazione disponibili, vedere la sezione [Servizio collegato ODBC](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="d22ed-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="d22ed-207">**Servizio collegato Archiviazione di Azure**</span><span class="sxs-lookup"><span data-stu-id="d22ed-207">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="d22ed-208">**Set di dati di input ODBC**</span><span class="sxs-lookup"><span data-stu-id="d22ed-208">**ODBC input dataset**</span></span>

<span data-ttu-id="d22ed-209">L'esempio presuppone che sia stata creata una tabella "MyTable" in un archivio dati ODBC e che contenga una colonna denominata "timestampcolumn" per i dati di una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="d22ed-209">The sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="d22ed-210">Impostando "external" su "true" si comunica al servizio Data Factory che il set di dati è esterno alla data factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="d22ed-210">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
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

<span data-ttu-id="d22ed-211">**Set di dati di output del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="d22ed-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="d22ed-212">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="d22ed-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d22ed-213">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="d22ed-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="d22ed-214">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="d22ed-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="d22ed-215">**Attività di copia in una pipeline con origine ODBC (RelationalSource) e sink BLOB (BlobSink)**</span><span class="sxs-lookup"><span data-stu-id="d22ed-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="d22ed-216">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="d22ed-216">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="d22ed-217">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **RelationalSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d22ed-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="d22ed-218">La query SQL specificata per la proprietà **query** consente di selezionare i dati da copiare nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="d22ed-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
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
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="d22ed-219">Mapping dei tipi per ODBC</span><span class="sxs-lookup"><span data-stu-id="d22ed-219">Type mapping for ODBC</span></span>
<span data-ttu-id="d22ed-220">Come accennato nell'articolo [Attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni di tipi automatiche da tipi di origine a tipi di sink con l'approccio seguente in due passaggi:</span><span class="sxs-lookup"><span data-stu-id="d22ed-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="d22ed-221">Conversione dai tipi di origine nativi al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="d22ed-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="d22ed-222">Conversione dal tipo .NET al tipo di sink nativo</span><span class="sxs-lookup"><span data-stu-id="d22ed-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="d22ed-223">Quando si spostano dati da archivi dati ODBC, viene eseguito il mapping dei tipi di dati ODBC ai tipi .NET, come riportato nell'argomento [Mapping dei tipi di dati ODBC](https://msdn.microsoft.com/library/cc668763.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d22ed-223">When moving data from ODBC data stores, ODBC data types are mapped to .NET types as mentioned in the [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="d22ed-224">Eseguire il mapping delle colonne dell'origine alle colonne del sink</span><span class="sxs-lookup"><span data-stu-id="d22ed-224">Map source to sink columns</span></span>
<span data-ttu-id="d22ed-225">Per informazioni sul mapping delle colonne del set di dati di origine alle colonne del set di dati del sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d22ed-225">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="d22ed-226">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="d22ed-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="d22ed-227">Quando si copiano dati da archivi dati relazionali, è necessario tenere presente la ripetibilità per evitare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="d22ed-227">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="d22ed-228">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="d22ed-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="d22ed-229">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="d22ed-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="d22ed-230">Quando una sezione viene rieseguita in uno dei due modi, è necessario assicurarsi che non vengano letti gli stessi dati, indipendentemente da quante volte viene eseguita la sezione.</span><span class="sxs-lookup"><span data-stu-id="d22ed-230">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="d22ed-231">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="d22ed-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="d22ed-232">Archivio GE Historian</span><span class="sxs-lookup"><span data-stu-id="d22ed-232">GE Historian store</span></span>
<span data-ttu-id="d22ed-233">Creare un servizio collegato ODBC per collegare un archivio dati [GE Proficy Historian (ora GE Historian)](http://www.geautomation.com/products/proficy-historian) a un'istanza di Azure Data Factory, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d22ed-233">You create an ODBC linked service to link a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store to an Azure data factory as shown in the following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of the GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="d22ed-234">Installare il Gateway di gestione dati in un computer locale e registrare il gateway con il portale.</span><span class="sxs-lookup"><span data-stu-id="d22ed-234">Install Data Management Gateway on an on-premises machine and register the gateway with the portal.</span></span> <span data-ttu-id="d22ed-235">Il gateway installato nel computer locale usa il driver ODBC per GE Historian per la connessione all'archivio dati GE Historian.</span><span class="sxs-lookup"><span data-stu-id="d22ed-235">The gateway installed on your on-premises computer uses the ODBC driver for GE Historian to connect to the GE Historian data store.</span></span> <span data-ttu-id="d22ed-236">Installare quindi il driver se non è già installato nel computer del gateway.</span><span class="sxs-lookup"><span data-stu-id="d22ed-236">Therefore, install the driver if it is not already installed on the gateway machine.</span></span> <span data-ttu-id="d22ed-237">Per i dettagli, vedere [Abilitazione della connettività](#enabling-connectivity) .</span><span class="sxs-lookup"><span data-stu-id="d22ed-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="d22ed-238">Prima di usare l'archivio GE Historian in una soluzione Data Factory, verificare se il gateway è in grado di connettersi all'archivio dati usando le istruzioni indicate nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="d22ed-238">Before you use the GE Historian store in a Data Factory solution, verify whether the gateway can connect to the data store using instructions in the next section.</span></span>

<span data-ttu-id="d22ed-239">Leggere l'articolo dall'inizio per una panoramica dettagliata dell'uso degli archivi dati ODBC come archivi dati di origine in un'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="d22ed-239">Read the article from the beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="d22ed-240">Risoluzione dei problemi di connettività</span><span class="sxs-lookup"><span data-stu-id="d22ed-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="d22ed-241">Per risolvere i problemi di connessione, usare la scheda **Diagnostica** di **Gestione configurazione di Gateway di gestione dati**.</span><span class="sxs-lookup"><span data-stu-id="d22ed-241">To troubleshoot connection issues, use the **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="d22ed-242">Avviare **Gestione configurazione di Gateway di gestione dati**.</span><span class="sxs-lookup"><span data-stu-id="d22ed-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="d22ed-243">È possibile eseguire direttamente "C:\Programmi\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" o eseguire una ricerca di **Gateway** per trovare un collegamento all'applicazione **Gateway di gestione dati di Microsoft**, come mostrato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="d22ed-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** to find a link to **Microsoft Data Management Gateway** application as shown in the following image.</span></span>

    ![Ricerca nel gateway](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="d22ed-245">Passare alla scheda **Diagnostica** .</span><span class="sxs-lookup"><span data-stu-id="d22ed-245">Switch to the **Diagnostics** tab.</span></span>

    ![Diagnostica del gateway](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="d22ed-247">Selezionare il **tipo** di dati archiviati (servizio collegato).</span><span class="sxs-lookup"><span data-stu-id="d22ed-247">Select the **type** of data store (linked service).</span></span>
4. <span data-ttu-id="d22ed-248">Specificare l'**autenticazione** e immettere le **credenziali** o la **stringa di connessione** usati per la connessione all'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="d22ed-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used to connect to the data store.</span></span>
5. <span data-ttu-id="d22ed-249">Fare clic su **Test connessione** per testare la connessione all'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="d22ed-249">Click **Test connection** to test the connection to the data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d22ed-250">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="d22ed-250">Performance and Tuning</span></span>
<span data-ttu-id="d22ed-251">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="d22ed-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
