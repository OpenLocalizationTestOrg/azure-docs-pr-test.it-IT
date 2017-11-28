---
title: aaaMove dati da un server FTP tramite Data Factory di Azure | Documenti Microsoft
description: Per ulteriori informazioni vedere toomove dati da un server FTP con Data Factory di Azure.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="34651-103">Spostare dati da un server FTP usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="34651-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="34651-104">Questo articolo spiega come hello toouse attività di copia dei dati toomove Data Factory di Azure da un server FTP.</span><span class="sxs-lookup"><span data-stu-id="34651-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from an FTP server.</span></span> <span data-ttu-id="34651-105">È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="34651-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="34651-106">È possibile copiare dati da un archivio dati di sink FTP server tooany è supportato.</span><span class="sxs-lookup"><span data-stu-id="34651-106">You can copy data from an FTP server tooany supported sink data store.</span></span> <span data-ttu-id="34651-107">Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella.</span><span class="sxs-lookup"><span data-stu-id="34651-107">For a list of data stores supported as sinks by hello copy activity, see hello [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="34651-108">Data Factory supporta attualmente solo archivia dati mobili da tooother un server FTP, ma non lo spostamento dei dati da altri dati archivia server tooan FTP.</span><span class="sxs-lookup"><span data-stu-id="34651-108">Data Factory currently supports only moving data from an FTP server tooother data stores, but not moving data from other data stores tooan FTP server.</span></span> <span data-ttu-id="34651-109">Supporta i server FTP locali e cloud.</span><span class="sxs-lookup"><span data-stu-id="34651-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="34651-110">attività di copia Hello non elimina i file di origine hello dopo che è la destinazione toohello copiati correttamente.</span><span class="sxs-lookup"><span data-stu-id="34651-110">hello copy activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="34651-111">Se è necessario toodelete file di origine hello dopo una copia ha esito positivo, creare un file hello toodelete di attività personalizzata e utilizzare attività hello nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="34651-111">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file, and use hello activity in hello pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="34651-112">Abilitare la connettività</span><span class="sxs-lookup"><span data-stu-id="34651-112">Enable connectivity</span></span>
<span data-ttu-id="34651-113">Se si stanno spostando i dati da un **locale** archivio dati di cloud tooa server FTP (ad esempio, tooAzure nell'archiviazione Blob), installare e usare Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="34651-113">If you are moving data from an **on-premises** FTP server tooa cloud data store (for example, tooAzure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="34651-114">Hello Gateway di gestione dati è un agente client installato nel computer locale e consente una risorsa locale tooan tooconnect dei servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="34651-114">hello Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services tooconnect tooan on-premises resource.</span></span> <span data-ttu-id="34651-115">Per informazioni dettagliate, vedere [Gateway di gestione dati](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="34651-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="34651-116">Per istruzioni dettagliate sulla configurazione di gateway hello e l'uso, vedere [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="34651-116">For step-by-step instructions on setting up hello gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="34651-117">Si utilizza server di tooan FTP di hello gateway tooconnect, anche se il server di hello in un'infrastruttura di Azure come servizio (IaaS) macchina virtuale (VM).</span><span class="sxs-lookup"><span data-stu-id="34651-117">You use hello gateway tooconnect tooan FTP server, even if hello server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="34651-118">È possibile tooinstall hello gateway hello stesso in locale macchina o VM IaaS come hello server FTP.</span><span class="sxs-lookup"><span data-stu-id="34651-118">It is possible tooinstall hello gateway on hello same on-premises machine or IaaS VM as hello FTP server.</span></span> <span data-ttu-id="34651-119">Tuttavia, si consiglia di installare gateway hello in un computer distinto o contesa delle risorse tooavoid VM IaaS e per ottenere prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="34651-119">However, we recommend that you install hello gateway on a separate machine or IaaS VM tooavoid resource contention, and for better performance.</span></span> <span data-ttu-id="34651-120">Quando si installa il gateway hello in un computer separato, macchina hello debba essere server FTP di hello tooaccess in grado di.</span><span class="sxs-lookup"><span data-stu-id="34651-120">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="34651-121">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="34651-121">Get started</span></span>
<span data-ttu-id="34651-122">È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine FTP usando diversi strumenti o API.</span><span class="sxs-lookup"><span data-stu-id="34651-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="34651-123">toocreate modo più semplice di Hello una pipeline è hello toouse **Data Factory Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="34651-123">hello easiest way toocreate a pipeline is toouse hello **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="34651-124">Per una procedura dettagliata, vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="34651-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="34651-125">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **PowerShell**, **modellodigestionerisorsediAzure**, **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="34651-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="34651-126">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="34651-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="34651-127">Se si utilizza hello o le API, eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:</span><span class="sxs-lookup"><span data-stu-id="34651-127">Whether you use hello tools or APIs, perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="34651-128">Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="34651-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="34651-129">Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.</span><span class="sxs-lookup"><span data-stu-id="34651-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="34651-130">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="34651-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="34651-131">Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="34651-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="34651-132">Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.</span><span class="sxs-lookup"><span data-stu-id="34651-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="34651-133">Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un archivio dati FTP, vedere hello [esempio JSON: copiare i dati da blob tooAzure di server FTP](#json-example-copy-data-from-ftp-server-to-azure-blob) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="34651-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an FTP data store, see hello [JSON example: Copy data from FTP server tooAzure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="34651-134">Per informazioni dettagliate su toouse di formati di file e compressione supportati, vedere [formati di File e la compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="34651-134">For details about supported file and compression formats toouse, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="34651-135">Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooFTP.</span><span class="sxs-lookup"><span data-stu-id="34651-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooFTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="34651-136">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="34651-136">Linked service properties</span></span>
<span data-ttu-id="34651-137">Hello nella tabella seguente descrive servizio FTP collegato tooan specifico di elementi JSON.</span><span class="sxs-lookup"><span data-stu-id="34651-137">hello following table describes JSON elements specific tooan FTP linked service.</span></span>

| <span data-ttu-id="34651-138">Proprietà</span><span class="sxs-lookup"><span data-stu-id="34651-138">Property</span></span> | <span data-ttu-id="34651-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="34651-139">Description</span></span> | <span data-ttu-id="34651-140">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="34651-140">Required</span></span> | <span data-ttu-id="34651-141">Predefinito</span><span class="sxs-lookup"><span data-stu-id="34651-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34651-142">type</span><span class="sxs-lookup"><span data-stu-id="34651-142">type</span></span> |<span data-ttu-id="34651-143">Impostare questo tooFtpServer.</span><span class="sxs-lookup"><span data-stu-id="34651-143">Set this tooFtpServer.</span></span> |<span data-ttu-id="34651-144">Sì</span><span class="sxs-lookup"><span data-stu-id="34651-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="34651-145">host</span><span class="sxs-lookup"><span data-stu-id="34651-145">host</span></span> |<span data-ttu-id="34651-146">Specifica il nome di hello o indirizzo IP del server FTP hello.</span><span class="sxs-lookup"><span data-stu-id="34651-146">Specify hello name or IP address of hello FTP server.</span></span> |<span data-ttu-id="34651-147">Sì</span><span class="sxs-lookup"><span data-stu-id="34651-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="34651-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="34651-148">authenticationType</span></span> |<span data-ttu-id="34651-149">Specificare il tipo di autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="34651-149">Specify hello authentication type.</span></span> |<span data-ttu-id="34651-150">Sì</span><span class="sxs-lookup"><span data-stu-id="34651-150">Yes</span></span> |<span data-ttu-id="34651-151">Di base, anonimo</span><span class="sxs-lookup"><span data-stu-id="34651-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="34651-152">username</span><span class="sxs-lookup"><span data-stu-id="34651-152">username</span></span> |<span data-ttu-id="34651-153">Specificare gli utenti hello con server di accesso toohello FTP.</span><span class="sxs-lookup"><span data-stu-id="34651-153">Specify hello user who has access toohello FTP server.</span></span> |<span data-ttu-id="34651-154">No</span><span class="sxs-lookup"><span data-stu-id="34651-154">No</span></span> |&nbsp; |
| <span data-ttu-id="34651-155">password</span><span class="sxs-lookup"><span data-stu-id="34651-155">password</span></span> |<span data-ttu-id="34651-156">Specificare la password hello per l'utente di hello (nomeutente).</span><span class="sxs-lookup"><span data-stu-id="34651-156">Specify hello password for hello user (username).</span></span> |<span data-ttu-id="34651-157">No</span><span class="sxs-lookup"><span data-stu-id="34651-157">No</span></span> |&nbsp; |
| <span data-ttu-id="34651-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="34651-158">encryptedCredential</span></span> |<span data-ttu-id="34651-159">Specificare crittografato hello credenziali tooaccess hello FTP server.</span><span class="sxs-lookup"><span data-stu-id="34651-159">Specify hello encrypted credential tooaccess hello FTP server.</span></span> |<span data-ttu-id="34651-160">No</span><span class="sxs-lookup"><span data-stu-id="34651-160">No</span></span> |&nbsp; |
| <span data-ttu-id="34651-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34651-161">gatewayName</span></span> |<span data-ttu-id="34651-162">Specificare il nome di hello del gateway hello nel server FTP di Gateway di gestione dati tooconnect tooan locale.</span><span class="sxs-lookup"><span data-stu-id="34651-162">Specify hello name of hello gateway in Data Management Gateway tooconnect tooan on-premises FTP server.</span></span> |<span data-ttu-id="34651-163">No</span><span class="sxs-lookup"><span data-stu-id="34651-163">No</span></span> |&nbsp; |
| <span data-ttu-id="34651-164">port</span><span class="sxs-lookup"><span data-stu-id="34651-164">port</span></span> |<span data-ttu-id="34651-165">Specificare hello porta su cui hello FTP server è in ascolto.</span><span class="sxs-lookup"><span data-stu-id="34651-165">Specify hello port on which hello FTP server is listening.</span></span> |<span data-ttu-id="34651-166">No</span><span class="sxs-lookup"><span data-stu-id="34651-166">No</span></span> |<span data-ttu-id="34651-167">21</span><span class="sxs-lookup"><span data-stu-id="34651-167">21</span></span> |
| <span data-ttu-id="34651-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="34651-168">enableSsl</span></span> |<span data-ttu-id="34651-169">Specificare se toouse FTP su un canale SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="34651-169">Specify whether toouse FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="34651-170">No</span><span class="sxs-lookup"><span data-stu-id="34651-170">No</span></span> |<span data-ttu-id="34651-171">true</span><span class="sxs-lookup"><span data-stu-id="34651-171">true</span></span> |
| <span data-ttu-id="34651-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="34651-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="34651-173">Specificare se il server tooenable SSL la convalida del certificato quando si utilizza FTP tramite il canale SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="34651-173">Specify whether tooenable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="34651-174">No</span><span class="sxs-lookup"><span data-stu-id="34651-174">No</span></span> |<span data-ttu-id="34651-175">true</span><span class="sxs-lookup"><span data-stu-id="34651-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="34651-176">Usare l'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="34651-176">Use Anonymous authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="34651-177">Usare nome utente e password in testo normale per l'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="34651-177">Use username and password in plain text for basic authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="34651-178">Usare port, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="34651-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="34651-179">Usare encryptedCredential per autenticazione e gateway</span><span class="sxs-lookup"><span data-stu-id="34651-179">Use encryptedCredential for authentication and gateway</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="34651-180">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="34651-180">Dataset properties</span></span>
<span data-ttu-id="34651-181">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="34651-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="34651-182">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati.</span><span class="sxs-lookup"><span data-stu-id="34651-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="34651-183">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="34651-183">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="34651-184">Fornisce informazioni che sono il tipo di set di dati toohello specifico.</span><span class="sxs-lookup"><span data-stu-id="34651-184">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="34651-185">Hello **typeProperties** sezione per un set di dati di tipo **FileShare** ha hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="34651-185">hello **typeProperties** section for a dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="34651-186">Proprietà</span><span class="sxs-lookup"><span data-stu-id="34651-186">Property</span></span> | <span data-ttu-id="34651-187">Descrizione</span><span class="sxs-lookup"><span data-stu-id="34651-187">Description</span></span> | <span data-ttu-id="34651-188">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="34651-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34651-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="34651-189">folderPath</span></span> |<span data-ttu-id="34651-190">Cartella toohello sottopercorso.</span><span class="sxs-lookup"><span data-stu-id="34651-190">Subpath toohello folder.</span></span> <span data-ttu-id="34651-191">Utilizzare il carattere di escape ' \ ' per i caratteri speciali nella stringa hello.</span><span class="sxs-lookup"><span data-stu-id="34651-191">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="34651-192">Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="34651-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="34651-193">È possibile combinare questa proprietà con **partitionBy** toohave i percorsi delle cartelle in base alle sezioni di inizio e fine di data e ora.</span><span class="sxs-lookup"><span data-stu-id="34651-193">You can combine this property with **partitionBy** toohave folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="34651-194">Sì</span><span class="sxs-lookup"><span data-stu-id="34651-194">Yes</span></span> |
| <span data-ttu-id="34651-195">fileName</span><span class="sxs-lookup"><span data-stu-id="34651-195">fileName</span></span> |<span data-ttu-id="34651-196">Specificare il nome di hello del file hello in hello **folderPath** se si desidera hello tabella toorefer tooa specifici file nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="34651-196">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="34651-197">Se non si specifica alcun valore per questa proprietà, la tabella hello punta tooall file nella cartella hello.</span><span class="sxs-lookup"><span data-stu-id="34651-197">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="34651-198">Quando **fileName** non specificato per un set di dati di output, hello nome del file hello generato è hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="34651-198">When **fileName** is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="34651-199">Data<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="34651-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="34651-200">No</span><span class="sxs-lookup"><span data-stu-id="34651-200">No</span></span> |
| <span data-ttu-id="34651-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="34651-201">fileFilter</span></span> |<span data-ttu-id="34651-202">Specificare un tooselect toobe utilizzato filtro un subset di file in hello **folderPath**, anziché tutti i file.</span><span class="sxs-lookup"><span data-stu-id="34651-202">Specify a filter toobe used tooselect a subset of files in hello **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="34651-203">I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).</span><span class="sxs-lookup"><span data-stu-id="34651-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="34651-204">Esempio 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="34651-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="34651-205">Esempio 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="34651-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="34651-206">**fileFilter** è applicabile per un set di dati di input FileShare.</span><span class="sxs-lookup"><span data-stu-id="34651-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="34651-207">Questa proprietà non è supportata con Hadoop Distributed File System (HDFS).</span><span class="sxs-lookup"><span data-stu-id="34651-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="34651-208">No</span><span class="sxs-lookup"><span data-stu-id="34651-208">No</span></span> |
| <span data-ttu-id="34651-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="34651-209">partitionedBy</span></span> |<span data-ttu-id="34651-210">Utilizzato toospecify dinamico **folderPath** e **fileName** per dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="34651-210">Used toospecify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="34651-211">È ad esempio possibile specificare un **folderPath** contenente i parametri per ogni ora di dati.</span><span class="sxs-lookup"><span data-stu-id="34651-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="34651-212">No</span><span class="sxs-lookup"><span data-stu-id="34651-212">No</span></span> |
| <span data-ttu-id="34651-213">format</span><span class="sxs-lookup"><span data-stu-id="34651-213">format</span></span> | <span data-ttu-id="34651-214">è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="34651-214">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="34651-215">Set hello **tipo** proprietà in formato tooone di questi valori.</span><span class="sxs-lookup"><span data-stu-id="34651-215">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="34651-216">Per ulteriori informazioni, vedere hello [formato testo](data-factory-supported-file-and-compression-formats.md#text-format), [formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Parquet formato ](data-factory-supported-file-and-compression-formats.md#parquet-format) sezioni.</span><span class="sxs-lookup"><span data-stu-id="34651-216">For more information, see hello [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="34651-217">Se si desidera che il file toocopy come se fossero tra archivi basati su file (copia binaria), ignorare sezione formato hello in entrambe le definizioni di set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="34651-217">If you want toocopy files as they are between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="34651-218">No</span><span class="sxs-lookup"><span data-stu-id="34651-218">No</span></span> |
| <span data-ttu-id="34651-219">compressione</span><span class="sxs-lookup"><span data-stu-id="34651-219">compression</span></span> | <span data-ttu-id="34651-220">Specificare il tipo di hello e livello di compressione per dati hello.</span><span class="sxs-lookup"><span data-stu-id="34651-220">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="34651-221">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**, mentre i livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="34651-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="34651-222">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="34651-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="34651-223">No</span><span class="sxs-lookup"><span data-stu-id="34651-223">No</span></span> |
| <span data-ttu-id="34651-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="34651-224">useBinaryTransfer</span></span> |<span data-ttu-id="34651-225">Specificare se binario hello toouse modalità di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="34651-225">Specify whether toouse hello binary transfer mode.</span></span> <span data-ttu-id="34651-226">Hello valori sono true per la modalità binaria (si tratta di valore predefinito di hello) e false per ASCII.</span><span class="sxs-lookup"><span data-stu-id="34651-226">hello values are true for binary mode (this is hello default value), and false for ASCII.</span></span> <span data-ttu-id="34651-227">Questa proprietà può essere utilizzata solo quando hello tipo di servizio collegato associata è di tipo: server FTP.</span><span class="sxs-lookup"><span data-stu-id="34651-227">This property can only be used when hello associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="34651-228">No</span><span class="sxs-lookup"><span data-stu-id="34651-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="34651-229">**fileName** e **fileFilter** non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="34651-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-hello-partionedby-property"></a><span data-ttu-id="34651-230">Utilizzare proprietà partionedBy hello</span><span class="sxs-lookup"><span data-stu-id="34651-230">Use hello partionedBy property</span></span>
<span data-ttu-id="34651-231">Come indicato nella sezione precedente di hello, è possibile specificare un dinamico **folderPath** e **fileName** per dati della serie temporale con hello **partitionedBy** proprietà.</span><span class="sxs-lookup"><span data-stu-id="34651-231">As mentioned in hello previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with hello **partitionedBy** property.</span></span>

<span data-ttu-id="34651-232">toolearn sui set di dati serie ora, la pianificazione e le sezioni, vedere [creazione dei DataSet](data-factory-create-datasets.md), [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md), e [creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="34651-232">toolearn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="34651-233">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="34651-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="34651-234">In questo esempio, {Slice} viene sostituito con il valore di hello della variabile di sistema di Data Factory SliceStart, in hello formato (YYYYMMDDHH) specificato.</span><span class="sxs-lookup"><span data-stu-id="34651-234">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart, in hello format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="34651-235">Hello SliceStart fa riferimento l'ora toostart sezione hello.</span><span class="sxs-lookup"><span data-stu-id="34651-235">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="34651-236">percorso della cartella Hello è diversa per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="34651-236">hello folder path is different for each slice.</span></span> <span data-ttu-id="34651-237">Ad esempio: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="34651-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="34651-238">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="34651-238">Sample 2</span></span>

```json
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
<span data-ttu-id="34651-239">In questo esempio hello anno, mese, giorno e ora della proprietà SliceStart vengono estratti in variabili distinte che vengono utilizzate da hello **folderPath** e **fileName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="34651-239">In this example, hello year, month, day, and time of SliceStart are extracted into separate variables that are used by hello **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="34651-240">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="34651-240">Copy activity properties</span></span>
<span data-ttu-id="34651-241">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, vedere l'articolo sulla [creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="34651-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="34651-242">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="34651-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="34651-243">Le proprietà disponibili nella hello **typeProperties** sezione di hello hello attività, invece, variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="34651-243">Properties available in hello **typeProperties** section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="34651-244">Per attività di copia hello, le proprietà del tipo hello variano a seconda di hello tipi di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="34651-244">For hello copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="34651-245">Nell'attività di copia, l'origine hello è di tipo **FileSystemSource**, hello seguenti proprietà è disponibile in **typeProperties** sezione:</span><span class="sxs-lookup"><span data-stu-id="34651-245">In copy activity, when hello source is of type **FileSystemSource**, hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="34651-246">Proprietà</span><span class="sxs-lookup"><span data-stu-id="34651-246">Property</span></span> | <span data-ttu-id="34651-247">Descrizione</span><span class="sxs-lookup"><span data-stu-id="34651-247">Description</span></span> | <span data-ttu-id="34651-248">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="34651-248">Allowed values</span></span> | <span data-ttu-id="34651-249">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="34651-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34651-250">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="34651-250">recursive</span></span> |<span data-ttu-id="34651-251">Indica se hello i dati letti in modo ricorsivo dalle sottocartelle di hello o solo dalla cartella specificata hello.</span><span class="sxs-lookup"><span data-stu-id="34651-251">Indicates whether hello data is read recursively from hello subfolders, or only from hello specified folder.</span></span> |<span data-ttu-id="34651-252">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="34651-252">True, False (default)</span></span> |<span data-ttu-id="34651-253">No</span><span class="sxs-lookup"><span data-stu-id="34651-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a><span data-ttu-id="34651-254">Esempio JSON: copiare i dati da tooAzure server FTP Blob</span><span class="sxs-lookup"><span data-stu-id="34651-254">JSON example: Copy data from FTP server tooAzure Blob</span></span>
<span data-ttu-id="34651-255">Questo esempio viene illustrato come toocopy dati da un tooAzure server FTP nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="34651-255">This sample shows how toocopy data from an FTP server tooAzure Blob storage.</span></span> <span data-ttu-id="34651-256">Tuttavia, i dati possono essere copiati direttamente tooany di hello sink hello dichiarato nella [archivi dati e formati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats), utilizzando attività di copia hello in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="34651-256">However, data can be copied directly tooany of hello sinks stated in hello [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using hello copy activity in Data Factory.</span></span>  

<span data-ttu-id="34651-257">Negli esempi seguenti Hello forniscono definizioni JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="34651-257">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="34651-258">Un servizio collegato di tipo [FtpServer](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="34651-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="34651-259">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="34651-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="34651-260">Un [set di dati](data-factory-create-datasets.md) di input di tipo [FileShare](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="34651-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="34651-261">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="34651-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="34651-262">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="34651-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="34651-263">esempio Hello copia dati da un tooan server FTP blob di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="34651-263">hello sample copies data from an FTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="34651-264">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="34651-264">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="34651-265">Servizio collegato FTP</span><span class="sxs-lookup"><span data-stu-id="34651-265">FTP linked service</span></span>

<span data-ttu-id="34651-266">In questo esempio viene utilizzata l'autenticazione di base, con nome utente hello e una password in testo normale.</span><span class="sxs-lookup"><span data-stu-id="34651-266">This example uses basic authentication, with hello user name and password in plain text.</span></span> <span data-ttu-id="34651-267">È inoltre possibile utilizzare uno dei seguenti modi hello:</span><span class="sxs-lookup"><span data-stu-id="34651-267">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="34651-268">Autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="34651-268">Anonymous authentication</span></span>
* <span data-ttu-id="34651-269">Autenticazione di base con credenziali crittografate</span><span class="sxs-lookup"><span data-stu-id="34651-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="34651-270">FTP su SSL/TLS (FTPS)</span><span class="sxs-lookup"><span data-stu-id="34651-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="34651-271">Vedere hello [servizio collegato FTP](#linked-service-properties) sezione per diversi tipi di autenticazione è possibile utilizzare.</span><span class="sxs-lookup"><span data-stu-id="34651-271">See hello [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a><span data-ttu-id="34651-272">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="34651-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="34651-273">Set di dati di input FTP</span><span class="sxs-lookup"><span data-stu-id="34651-273">FTP input dataset</span></span>

<span data-ttu-id="34651-274">Questo set di dati fa riferimento la cartella FTP toohello `mysharedfolder` e file `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="34651-274">This dataset refers toohello FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="34651-275">Hello pipeline copie hello toohello destinazione file.</span><span class="sxs-lookup"><span data-stu-id="34651-275">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="34651-276">Impostazione **esterno** troppo**true** informa il servizio di Data Factory hello hello set di dati è esterno toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="34651-276">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory, and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="34651-277">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="34651-277">Azure Blob output dataset</span></span>

<span data-ttu-id="34651-278">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="34651-278">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="34651-279">percorso della cartella Hello per blob hello viene valutato dinamicamente, in base a ora di inizio hello della sezione hello che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="34651-279">hello folder path for hello blob is dynamically evaluated, based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="34651-280">percorso della cartella Hello Usa le parti di anno, mese, giorno e ore hello hello ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="34651-280">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="34651-281">Un'attività di copia in una pipeline con un'origine su file system e un sink BLOB</span><span class="sxs-lookup"><span data-stu-id="34651-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="34651-282">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output, senza che sia pianificato toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="34651-282">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="34651-283">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**FileSystemSource**, hello e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="34651-283">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and hello **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="34651-284">colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="34651-284">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="34651-285">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="34651-285">Next steps</span></span>
<span data-ttu-id="34651-286">Vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="34651-286">See hello following articles:</span></span>

* <span data-ttu-id="34651-287">toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento (attività di copia) dei dati in Data Factory e toooptimize modi diversi, vedere hello [copiare ottimizzazione Guida e alle prestazioni di attività](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="34651-287">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="34651-288">Per istruzioni dettagliate per la creazione di una pipeline con attività di copia, vedere hello [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="34651-288">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
