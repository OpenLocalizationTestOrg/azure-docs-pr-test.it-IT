---
title: aaaMove dati dagli archivi di dati ODBC | Documenti Microsoft
description: "Informazioni sulle modalità di archiviazione usando Azure Data Factory toomove dati da ODBC."
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
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="3a1d0-103">Spostare dati da archivi dati ODBC con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3a1d0-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="3a1d0-104">Questo articolo illustra in che modo toouse hello attività di copia nei dati di toomove Azure Data Factory di un dati ODBC locali archiviate.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises ODBC data store.</span></span> <span data-ttu-id="3a1d0-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="3a1d0-106">È possibile copiare dati da un archivio di dati ODBC dati archivio tooany supportati sink.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-106">You can copy data from an ODBC data store tooany supported sink data store.</span></span> <span data-ttu-id="3a1d0-107">Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="3a1d0-108">Data factory di attualmente supporta solo lo spostamento di dati da un ODBC archiviano tooother archivi di dati, ma non per lo spostamento dei dati da altro archivio dati ODBC tooan di archivi di dati.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-108">Data factory currently supports only moving data from an ODBC data store tooother data stores, but not for moving data from other data stores tooan ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="3a1d0-109">Abilitazione della connettività</span><span class="sxs-lookup"><span data-stu-id="3a1d0-109">Enabling connectivity</span></span>
<span data-ttu-id="3a1d0-110">Servizio Data Factory supporta la connessione delle origini ODBC tooon locale utilizzando hello Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-110">Data Factory service supports connecting tooon-premises ODBC sources using hello Data Management Gateway.</span></span> <span data-ttu-id="3a1d0-111">Vedere [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn articolo sul Gateway di gestione dati e istruzioni dettagliate su come configurare il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="3a1d0-112">Utilizzare l'archivio di dati ODBC hello gateway tooconnect tooan anche se è ospitato in una macchina virtuale IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-112">Use hello gateway tooconnect tooan ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="3a1d0-113">È possibile installare il gateway di hello in hello locale stesso computer o macchina virtuale di Azure come archivio di dati ODBC hello hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-113">You can install hello gateway on hello same on-premises machine or hello Azure VM as hello ODBC data store.</span></span> <span data-ttu-id="3a1d0-114">Tuttavia, si consiglia di installare gateway hello in un separato macchina/Azure VM IaaS tooavoid contesa delle risorse e per ottenere prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-114">However, we recommend that you install hello gateway on a separate machine/Azure IaaS VM tooavoid resource contention and for better performance.</span></span> <span data-ttu-id="3a1d0-115">Quando si installa il gateway hello in un computer separato, macchina hello deve essere in grado di tooaccess macchina di hello con archivio di dati ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-115">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello ODBC data store.</span></span>

<span data-ttu-id="3a1d0-116">Oltre a hello Gateway di gestione dati, è necessario anche driver ODBC di hello tooinstall per archivio dati hello nel computer gateway hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-116">Apart from hello Data Management Gateway, you also need tooinstall hello ODBC driver for hello data store on hello gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="3a1d0-117">Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .</span><span class="sxs-lookup"><span data-stu-id="3a1d0-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="3a1d0-118">Introduzione</span><span class="sxs-lookup"><span data-stu-id="3a1d0-118">Getting started</span></span>
<span data-ttu-id="3a1d0-119">È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati ODBC usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="3a1d0-120">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="3a1d0-121">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="3a1d0-122">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="3a1d0-123">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="3a1d0-124">Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="3a1d0-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="3a1d0-125">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="3a1d0-126">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="3a1d0-127">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="3a1d0-128">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="3a1d0-129">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="3a1d0-130">Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un archivio di dati ODBC, vedere [esempio JSON: tooAzure Blob di archiviazione dei dati di copia dei dati ODBC](#json-example-copy-data-from-odbc-data-store-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an ODBC data store, see [JSON example: Copy data from ODBC data store tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="3a1d0-131">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che sono l'archivio di dati utilizzati toodefine Data Factory entità tooODBC specifico:</span><span class="sxs-lookup"><span data-stu-id="3a1d0-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="3a1d0-132">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="3a1d0-132">Linked service properties</span></span>
<span data-ttu-id="3a1d0-133">Hello nella tabella seguente fornisce una descrizione del servizio specifico tooODBC collegati gli elementi JSON.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-133">hello following table provides description for JSON elements specific tooODBC linked service.</span></span>

| <span data-ttu-id="3a1d0-134">Proprietà</span><span class="sxs-lookup"><span data-stu-id="3a1d0-134">Property</span></span> | <span data-ttu-id="3a1d0-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3a1d0-135">Description</span></span> | <span data-ttu-id="3a1d0-136">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="3a1d0-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a1d0-137">type</span><span class="sxs-lookup"><span data-stu-id="3a1d0-137">type</span></span> |<span data-ttu-id="3a1d0-138">proprietà di tipo Hello deve essere impostata su: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="3a1d0-138">hello type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="3a1d0-139">Sì</span><span class="sxs-lookup"><span data-stu-id="3a1d0-139">Yes</span></span> |
| <span data-ttu-id="3a1d0-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="3a1d0-140">connectionString</span></span> |<span data-ttu-id="3a1d0-141">credenziale è crittografata da parte di credenziali di accesso non Hello di stringa di connessione hello e un parametro facoltativo.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-141">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="3a1d0-142">Vedere esempi in hello le sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-142">See examples in hello following sections.</span></span> |<span data-ttu-id="3a1d0-143">Sì</span><span class="sxs-lookup"><span data-stu-id="3a1d0-143">Yes</span></span> |
| <span data-ttu-id="3a1d0-144">credential</span><span class="sxs-lookup"><span data-stu-id="3a1d0-144">credential</span></span> |<span data-ttu-id="3a1d0-145">parte delle credenziali di accesso Hello hello della stringa di connessione specificato nel formato valore della proprietà specifiche del driver.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-145">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="3a1d0-146">Esempio: "Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;".</span><span class="sxs-lookup"><span data-stu-id="3a1d0-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="3a1d0-147">No</span><span class="sxs-lookup"><span data-stu-id="3a1d0-147">No</span></span> |
| <span data-ttu-id="3a1d0-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3a1d0-148">authenticationType</span></span> |<span data-ttu-id="3a1d0-149">Tipo di autenticazione utilizzato l'archivio di dati ODBC toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-149">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="3a1d0-150">I valori possibili sono: anonima e di base.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="3a1d0-151">Sì</span><span class="sxs-lookup"><span data-stu-id="3a1d0-151">Yes</span></span> |
| <span data-ttu-id="3a1d0-152">username</span><span class="sxs-lookup"><span data-stu-id="3a1d0-152">username</span></span> |<span data-ttu-id="3a1d0-153">Specificare il nome utente se si usa l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="3a1d0-154">No</span><span class="sxs-lookup"><span data-stu-id="3a1d0-154">No</span></span> |
| <span data-ttu-id="3a1d0-155">password</span><span class="sxs-lookup"><span data-stu-id="3a1d0-155">password</span></span> |<span data-ttu-id="3a1d0-156">Specificare la password per account utente di hello specificato per il nome utente hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-156">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="3a1d0-157">No</span><span class="sxs-lookup"><span data-stu-id="3a1d0-157">No</span></span> |
| <span data-ttu-id="3a1d0-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3a1d0-158">gatewayName</span></span> |<span data-ttu-id="3a1d0-159">Nome del gateway hello hello servizio Data Factory deve utilizzare l'archivio di dati ODBC toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="3a1d0-160">Sì</span><span class="sxs-lookup"><span data-stu-id="3a1d0-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="3a1d0-161">Uso dell'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="3a1d0-161">Using Basic authentication</span></span>

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
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="3a1d0-162">Uso dell'autenticazione di base con credenziali crittografate</span><span class="sxs-lookup"><span data-stu-id="3a1d0-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="3a1d0-163">È possibile crittografare le credenziali di hello utilizzando hello [New AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (1.0 versione di Azure PowerShell) o [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 o versioni precedenti di hello Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="3a1d0-163">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="3a1d0-164">Uso dell'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="3a1d0-164">Using Anonymous authentication</span></span>

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


## <a name="dataset-properties"></a><span data-ttu-id="3a1d0-165">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="3a1d0-165">Dataset properties</span></span>
<span data-ttu-id="3a1d0-166">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="3a1d0-167">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="3a1d0-168">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="3a1d0-169">sezione Hello typeProperties per set di dati di tipo **RelationalTable** (che include set di dati ODBC) ha le proprietà seguenti hello</span><span class="sxs-lookup"><span data-stu-id="3a1d0-169">hello typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has hello following properties</span></span>

| <span data-ttu-id="3a1d0-170">Proprietà</span><span class="sxs-lookup"><span data-stu-id="3a1d0-170">Property</span></span> | <span data-ttu-id="3a1d0-171">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3a1d0-171">Description</span></span> | <span data-ttu-id="3a1d0-172">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="3a1d0-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a1d0-173">tableName</span><span class="sxs-lookup"><span data-stu-id="3a1d0-173">tableName</span></span> |<span data-ttu-id="3a1d0-174">Nome della tabella hello nell'archivio di dati ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-174">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="3a1d0-175">Sì</span><span class="sxs-lookup"><span data-stu-id="3a1d0-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="3a1d0-176">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="3a1d0-176">Copy activity properties</span></span>
<span data-ttu-id="3a1d0-177">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-177">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="3a1d0-178">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="3a1d0-179">Le proprietà disponibili nella hello **typeProperties** sezione di attività hello hello invece variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-179">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="3a1d0-180">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-180">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="3a1d0-181">Nell'attività di copia, l'origine è di tipo **RelationalSource** (che include ODBC), hello le proprietà seguenti sono disponibile nella sezione typeProperties:</span><span class="sxs-lookup"><span data-stu-id="3a1d0-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="3a1d0-182">Proprietà</span><span class="sxs-lookup"><span data-stu-id="3a1d0-182">Property</span></span> | <span data-ttu-id="3a1d0-183">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3a1d0-183">Description</span></span> | <span data-ttu-id="3a1d0-184">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="3a1d0-184">Allowed values</span></span> | <span data-ttu-id="3a1d0-185">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="3a1d0-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3a1d0-186">query</span><span class="sxs-lookup"><span data-stu-id="3a1d0-186">query</span></span> |<span data-ttu-id="3a1d0-187">Utilizzare i dati di tooread hello query personalizzata.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-187">Use hello custom query tooread data.</span></span> |<span data-ttu-id="3a1d0-188">Stringa di query SQL.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-188">SQL query string.</span></span> <span data-ttu-id="3a1d0-189">Ad esempio: selezionare * da MyTable.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="3a1d0-190">Sì</span><span class="sxs-lookup"><span data-stu-id="3a1d0-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a><span data-ttu-id="3a1d0-191">Esempio JSON: tooAzure Blob di archiviazione dei dati di copia dei dati ODBC</span><span class="sxs-lookup"><span data-stu-id="3a1d0-191">JSON example: Copy data from ODBC data store tooAzure Blob</span></span>
<span data-ttu-id="3a1d0-192">In questo esempio vengono fornite le definizioni di JSON che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3a1d0-192">This example provides JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="3a1d0-193">Viene illustrato come origine dei dati di toocopy da un database ODBC tooan archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-193">It shows how toocopy data from an ODBC source tooan Azure Blob Storage.</span></span> <span data-ttu-id="3a1d0-194">Tuttavia, i dati possono essere copiati tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-194">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="3a1d0-195">esempio Hello è hello entità factory di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="3a1d0-195">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="3a1d0-196">Un servizio collegato di tipo [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3a1d0-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="3a1d0-197">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3a1d0-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="3a1d0-198">Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3a1d0-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="3a1d0-199">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3a1d0-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="3a1d0-200">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="3a1d0-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="3a1d0-201">esempio Hello copia dati da un risultato di query in un blob di tooa ODBC archivio dati ogni ora.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-201">hello sample copies data from a query result in an ODBC data store tooa blob every hour.</span></span> <span data-ttu-id="3a1d0-202">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-202">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="3a1d0-203">Innanzitutto, configurare il gateway di gestione dati hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-203">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="3a1d0-204">istruzioni di Hello presenti hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-204">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="3a1d0-205">**Servizio collegato ODBC** in questo esempio viene utilizzata l'autenticazione di base di hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-205">**ODBC linked service** This example uses hello Basic authentication.</span></span> <span data-ttu-id="3a1d0-206">Per i diversi tipi di autenticazione disponibili, vedere la sezione [Servizio collegato ODBC](#linked-service-properties) .</span><span class="sxs-lookup"><span data-stu-id="3a1d0-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="3a1d0-207">**Servizio collegato Archiviazione di Azure**</span><span class="sxs-lookup"><span data-stu-id="3a1d0-207">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="3a1d0-208">**Set di dati di input ODBC**</span><span class="sxs-lookup"><span data-stu-id="3a1d0-208">**ODBC input dataset**</span></span>

<span data-ttu-id="3a1d0-209">esempio Hello presuppone una tabella "MyTable" è stato creato in un database ODBC e contiene una colonna denominata "timestampcolumn" per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-209">hello sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="3a1d0-210">L'impostazione "external": "true" informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-210">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="3a1d0-211">**Set di dati di output del BLOB di Azure**</span><span class="sxs-lookup"><span data-stu-id="3a1d0-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="3a1d0-212">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="3a1d0-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="3a1d0-213">percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="3a1d0-214">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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


<span data-ttu-id="3a1d0-215">**Attività di copia in una pipeline con origine ODBC (RelationalSource) e sink BLOB (BlobSink)**</span><span class="sxs-lookup"><span data-stu-id="3a1d0-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="3a1d0-216">pipeline di Hello contiene un'attività di copia che è configurato toouse questi set di dati di input e output e toorun pianificato ogni ora.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-216">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="3a1d0-217">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**RelationalSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="3a1d0-218">query SQL Hello specificata per hello **query** proprietà consente di selezionare dati hello hello oltre toocopy ora.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="3a1d0-219">Mapping dei tipi per ODBC</span><span class="sxs-lookup"><span data-stu-id="3a1d0-219">Type mapping for ODBC</span></span>
<span data-ttu-id="3a1d0-220">Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio in due passaggi:</span><span class="sxs-lookup"><span data-stu-id="3a1d0-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="3a1d0-221">Conversione dal tipo di origine nativa tipi too.NET</span><span class="sxs-lookup"><span data-stu-id="3a1d0-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="3a1d0-222">Eseguire la conversione da tipo di sink toonative tipo .NET</span><span class="sxs-lookup"><span data-stu-id="3a1d0-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="3a1d0-223">Quando si spostano dati da archivi dati ODBC, tipi di dati ODBC sono tipi di too.NET mappato come indicato in hello [mapping dei tipi di dati ODBC](https://msdn.microsoft.com/library/cc668763.aspx) argomento.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-223">When moving data from ODBC data stores, ODBC data types are mapped too.NET types as mentioned in hello [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="3a1d0-224">Eseguire il mapping di colonne di origine toosink</span><span class="sxs-lookup"><span data-stu-id="3a1d0-224">Map source toosink columns</span></span>
<span data-ttu-id="3a1d0-225">toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="3a1d0-225">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="3a1d0-226">Lettura ripetibile da origini relazionali</span><span class="sxs-lookup"><span data-stu-id="3a1d0-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="3a1d0-227">Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-227">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="3a1d0-228">In Azure Data Factory è possibile rieseguire una sezione manualmente.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="3a1d0-229">È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="3a1d0-230">Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-230">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="3a1d0-231">Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="3a1d0-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="3a1d0-232">Archivio GE Historian</span><span class="sxs-lookup"><span data-stu-id="3a1d0-232">GE Historian store</span></span>
<span data-ttu-id="3a1d0-233">Si crea un toolink servizio ODBC collegato un [consumo Proficy GE (ora consumo GE)](http://www.geautomation.com/products/proficy-historian) dati archiviano tooan data factory di Azure, come mostrato nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="3a1d0-233">You create an ODBC linked service toolink a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store tooan Azure data factory as shown in hello following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="3a1d0-234">Installare il Gateway di gestione di dati in un computer locale e registrare il gateway hello hello portale.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-234">Install Data Management Gateway on an on-premises machine and register hello gateway with hello portal.</span></span> <span data-ttu-id="3a1d0-235">gateway di Hello installato nel computer locale utilizza il driver ODBC hello per consumo GE tooconnect toohello archivio dati di consumo GE.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-235">hello gateway installed on your on-premises computer uses hello ODBC driver for GE Historian tooconnect toohello GE Historian data store.</span></span> <span data-ttu-id="3a1d0-236">Pertanto, installare i driver di hello se non è già installato nel computer gateway hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-236">Therefore, install hello driver if it is not already installed on hello gateway machine.</span></span> <span data-ttu-id="3a1d0-237">Per i dettagli, vedere [Abilitazione della connettività](#enabling-connectivity) .</span><span class="sxs-lookup"><span data-stu-id="3a1d0-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="3a1d0-238">Prima di utilizzare hello GE consumo archiviare in una soluzione di Data Factory, verificare se il gateway hello può connettersi archivio dati toohello seguendo le istruzioni nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-238">Before you use hello GE Historian store in a Data Factory solution, verify whether hello gateway can connect toohello data store using instructions in hello next section.</span></span>

<span data-ttu-id="3a1d0-239">Leggere l'articolo hello dall'inizio di hello per una panoramica dettagliata dell'utilizzo di dati ODBC vengono archiviate come archivi dati di origine in un'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-239">Read hello article from hello beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="3a1d0-240">Risoluzione dei problemi di connettività</span><span class="sxs-lookup"><span data-stu-id="3a1d0-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="3a1d0-241">problemi di connessione tootroubleshoot utilizzare hello **diagnostica** scheda **Gestione configurazione di Gateway di gestione di dati**.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-241">tootroubleshoot connection issues, use hello **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="3a1d0-242">Avviare **Gestione configurazione di Gateway di gestione dati**.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="3a1d0-243">È possibile eseguire "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" direttamente (o) ricerca per **Gateway** toofind un collegamento troppo**Gateway di gestione dati Microsoft** applicazione come mostrato nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** toofind a link too**Microsoft Data Management Gateway** application as shown in hello following image.</span></span>

    ![Ricerca nel gateway](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="3a1d0-245">Passare toohello **diagnostica** scheda.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-245">Switch toohello **Diagnostics** tab.</span></span>

    ![Diagnostica del gateway](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="3a1d0-247">Seleziona hello **tipo** dati di archivio (servizio collegato).</span><span class="sxs-lookup"><span data-stu-id="3a1d0-247">Select hello **type** of data store (linked service).</span></span>
4. <span data-ttu-id="3a1d0-248">Specificare **autenticazione** e immettere **credenziali** (o) immettere **stringa di connessione** che viene utilizzato tooconnect toohello dati archivio.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used tooconnect toohello data store.</span></span>
5. <span data-ttu-id="3a1d0-249">Fare clic su **Test della connessione** tootest hello connessione toohello dati archivio.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-249">Click **Test connection** tootest hello connection toohello data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="3a1d0-250">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="3a1d0-250">Performance and Tuning</span></span>
<span data-ttu-id="3a1d0-251">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="3a1d0-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
