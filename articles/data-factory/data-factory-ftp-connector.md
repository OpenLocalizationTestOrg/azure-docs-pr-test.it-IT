---
title: Spostare dati da un server FTP usando Azure Data Factory | Microsoft Docs
description: Informazioni su come spostare dati da un server FTP usando Azure Data Factory.
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
ms.openlocfilehash: f8f31f3a2ee02c964737dd32145499f3dcfd0624
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="2455f-103">Spostare dati da un server FTP usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2455f-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="2455f-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da un server FTP.</span><span class="sxs-lookup"><span data-stu-id="2455f-104">This article explains how to use the copy activity in Azure Data Factory to move data from an FTP server.</span></span> <span data-ttu-id="2455f-105">Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="2455f-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="2455f-106">È possibile copiare dati da un server FTP a qualsiasi archivio dati di sink supportato.</span><span class="sxs-lookup"><span data-stu-id="2455f-106">You can copy data from an FTP server to any supported sink data store.</span></span> <span data-ttu-id="2455f-107">Per un elenco degli archivi dati supportati come sink dall'attività di copia, vedere la tabella relativa agli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="2455f-107">For a list of data stores supported as sinks by the copy activity, see the [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="2455f-108">Data Factory supporta attualmente solo lo spostamento di dati da un server FTP ad altri archivi dati, non da altri archivi dati a un server FTP.</span><span class="sxs-lookup"><span data-stu-id="2455f-108">Data Factory currently supports only moving data from an FTP server to other data stores, but not moving data from other data stores to an FTP server.</span></span> <span data-ttu-id="2455f-109">Supporta i server FTP locali e cloud.</span><span class="sxs-lookup"><span data-stu-id="2455f-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="2455f-110">L'attività di copia non elimina il file di origine dopo che è stato correttamente copiato nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="2455f-110">The copy activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="2455f-111">Se è necessario eliminare il file di origine dopo una copia con esito positivo, creare un'attività personalizzata per eliminare il file e usare l'attività nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="2455f-111">If you need to delete the source file after a successful copy, create a custom activity to delete the file, and use the activity in the pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="2455f-112">Abilitare la connettività</span><span class="sxs-lookup"><span data-stu-id="2455f-112">Enable connectivity</span></span>
<span data-ttu-id="2455f-113">Se si spostano dati da un server FTP **locale** in un archivio dati cloud, ad esempio in Archiviazione BLOB di Azure, installare e usare Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="2455f-113">If you are moving data from an **on-premises** FTP server to a cloud data store (for example, to Azure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="2455f-114">Gateway di gestione dati è un agente client installato nel computer locale, che consente ai servizi cloud di connettersi alla risorsa locale.</span><span class="sxs-lookup"><span data-stu-id="2455f-114">The Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services to connect to an on-premises resource.</span></span> <span data-ttu-id="2455f-115">Per informazioni dettagliate, vedere [Gateway di gestione dati](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="2455f-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="2455f-116">Per istruzioni dettagliate sulla configurazione e sull'uso del gateway, vedere [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="2455f-116">For step-by-step instructions on setting up the gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="2455f-117">Il gateway consente di connettersi a un server FTP anche se il server si trova in una macchina virtuale (VM) di infrastruttura distribuita come servizio (IaaS) di Azure.</span><span class="sxs-lookup"><span data-stu-id="2455f-117">You use the gateway to connect to an FTP server, even if the server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="2455f-118">È possibile installare il gateway nello stesso computer locale o nella VM IaaS come server FTP.</span><span class="sxs-lookup"><span data-stu-id="2455f-118">It is possible to install the gateway on the same on-premises machine or IaaS VM as the FTP server.</span></span> <span data-ttu-id="2455f-119">È tuttavia consigliabile installare il gateway in un computer separato o in una macchina virtuale IaaS distinta per evitare conflitti tra le risorse e ottenere prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="2455f-119">However, we recommend that you install the gateway on a separate machine or IaaS VM to avoid resource contention, and for better performance.</span></span> <span data-ttu-id="2455f-120">Quando si installa il gateway in un computer separato, questo deve poter accedere al server FTP.</span><span class="sxs-lookup"><span data-stu-id="2455f-120">When you install the gateway on a separate machine, the machine should be able to access the FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="2455f-121">Introduzione</span><span class="sxs-lookup"><span data-stu-id="2455f-121">Get started</span></span>
<span data-ttu-id="2455f-122">È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine FTP usando diversi strumenti o API.</span><span class="sxs-lookup"><span data-stu-id="2455f-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="2455f-123">Il modo più semplice per creare una pipeline è usare la **Copia guidata di Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="2455f-123">The easiest way to create a pipeline is to use the **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="2455f-124">Per una procedura dettagliata, vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="2455f-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="2455f-125">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="2455f-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2455f-126">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="2455f-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="2455f-127">Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink:</span><span class="sxs-lookup"><span data-stu-id="2455f-127">Whether you use the tools or APIs, perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="2455f-128">Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.</span><span class="sxs-lookup"><span data-stu-id="2455f-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="2455f-129">Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="2455f-129">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="2455f-130">Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="2455f-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="2455f-131">Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2455f-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="2455f-132">Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2455f-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="2455f-133">Per un esempio con definizioni JSON per entità di Data Factory usate per copiare dati da un archivio dati FTP, vedere la sezione [Esempio JSON: copiare dati da un server FTP al BLOB di Azure](#json-example-copy-data-from-ftp-server-to-azure-blob) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="2455f-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an FTP data store, see the [JSON example: Copy data from FTP server to Azure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="2455f-134">Per altre informazioni sui formati di compressione e i file e supportati da usare, vedere [Informazioni sui formati di compressione e sui file supportati da Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="2455f-134">For details about supported file and compression formats to use, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="2455f-135">Le sezioni seguenti riportano informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di Data Factory specifiche di FTP.</span><span class="sxs-lookup"><span data-stu-id="2455f-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to FTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2455f-136">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="2455f-136">Linked service properties</span></span>
<span data-ttu-id="2455f-137">La tabella seguente descrive gli elementi JSON specifici di un servizio collegato FTP.</span><span class="sxs-lookup"><span data-stu-id="2455f-137">The following table describes JSON elements specific to an FTP linked service.</span></span>

| <span data-ttu-id="2455f-138">Proprietà</span><span class="sxs-lookup"><span data-stu-id="2455f-138">Property</span></span> | <span data-ttu-id="2455f-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2455f-139">Description</span></span> | <span data-ttu-id="2455f-140">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2455f-140">Required</span></span> | <span data-ttu-id="2455f-141">Predefinito</span><span class="sxs-lookup"><span data-stu-id="2455f-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2455f-142">type</span><span class="sxs-lookup"><span data-stu-id="2455f-142">type</span></span> |<span data-ttu-id="2455f-143">Impostare su FtpServer.</span><span class="sxs-lookup"><span data-stu-id="2455f-143">Set this to FtpServer.</span></span> |<span data-ttu-id="2455f-144">Sì</span><span class="sxs-lookup"><span data-stu-id="2455f-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="2455f-145">host</span><span class="sxs-lookup"><span data-stu-id="2455f-145">host</span></span> |<span data-ttu-id="2455f-146">Specificare il nome o indirizzo IP del server FTP.</span><span class="sxs-lookup"><span data-stu-id="2455f-146">Specify the name or IP address of the FTP server.</span></span> |<span data-ttu-id="2455f-147">Sì</span><span class="sxs-lookup"><span data-stu-id="2455f-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="2455f-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="2455f-148">authenticationType</span></span> |<span data-ttu-id="2455f-149">Specificare il tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="2455f-149">Specify the authentication type.</span></span> |<span data-ttu-id="2455f-150">Sì</span><span class="sxs-lookup"><span data-stu-id="2455f-150">Yes</span></span> |<span data-ttu-id="2455f-151">Di base, anonimo</span><span class="sxs-lookup"><span data-stu-id="2455f-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="2455f-152">username</span><span class="sxs-lookup"><span data-stu-id="2455f-152">username</span></span> |<span data-ttu-id="2455f-153">Specificare l'utente che ha accesso al server FTP.</span><span class="sxs-lookup"><span data-stu-id="2455f-153">Specify the user who has access to the FTP server.</span></span> |<span data-ttu-id="2455f-154">No</span><span class="sxs-lookup"><span data-stu-id="2455f-154">No</span></span> |&nbsp; |
| <span data-ttu-id="2455f-155">password</span><span class="sxs-lookup"><span data-stu-id="2455f-155">password</span></span> |<span data-ttu-id="2455f-156">Specificare la password per l'utente (nome utente).</span><span class="sxs-lookup"><span data-stu-id="2455f-156">Specify the password for the user (username).</span></span> |<span data-ttu-id="2455f-157">No</span><span class="sxs-lookup"><span data-stu-id="2455f-157">No</span></span> |&nbsp; |
| <span data-ttu-id="2455f-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="2455f-158">encryptedCredential</span></span> |<span data-ttu-id="2455f-159">Specificare le credenziali crittografate per accedere al server FTP.</span><span class="sxs-lookup"><span data-stu-id="2455f-159">Specify the encrypted credential to access the FTP server.</span></span> |<span data-ttu-id="2455f-160">No</span><span class="sxs-lookup"><span data-stu-id="2455f-160">No</span></span> |&nbsp; |
| <span data-ttu-id="2455f-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="2455f-161">gatewayName</span></span> |<span data-ttu-id="2455f-162">Specificare il nome del gateway in Gateway di gestione dati per connettersi a un server FTP locale.</span><span class="sxs-lookup"><span data-stu-id="2455f-162">Specify the name of the gateway in Data Management Gateway to connect to an on-premises FTP server.</span></span> |<span data-ttu-id="2455f-163">No</span><span class="sxs-lookup"><span data-stu-id="2455f-163">No</span></span> |&nbsp; |
| <span data-ttu-id="2455f-164">port</span><span class="sxs-lookup"><span data-stu-id="2455f-164">port</span></span> |<span data-ttu-id="2455f-165">Specificare la porta su cui è in ascolto il server FTP.</span><span class="sxs-lookup"><span data-stu-id="2455f-165">Specify the port on which the FTP server is listening.</span></span> |<span data-ttu-id="2455f-166">No</span><span class="sxs-lookup"><span data-stu-id="2455f-166">No</span></span> |<span data-ttu-id="2455f-167">21</span><span class="sxs-lookup"><span data-stu-id="2455f-167">21</span></span> |
| <span data-ttu-id="2455f-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="2455f-168">enableSsl</span></span> |<span data-ttu-id="2455f-169">Specificare se usare FTP su un canale SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="2455f-169">Specify whether to use FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="2455f-170">No</span><span class="sxs-lookup"><span data-stu-id="2455f-170">No</span></span> |<span data-ttu-id="2455f-171">true</span><span class="sxs-lookup"><span data-stu-id="2455f-171">true</span></span> |
| <span data-ttu-id="2455f-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="2455f-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="2455f-173">Specificare se abilitare la convalida del certificato SSL del server quando si usa FTP sul canale SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="2455f-173">Specify whether to enable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="2455f-174">No</span><span class="sxs-lookup"><span data-stu-id="2455f-174">No</span></span> |<span data-ttu-id="2455f-175">true</span><span class="sxs-lookup"><span data-stu-id="2455f-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="2455f-176">Usare l'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="2455f-176">Use Anonymous authentication</span></span>

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

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="2455f-177">Usare nome utente e password in testo normale per l'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="2455f-177">Use username and password in plain text for basic authentication</span></span>

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

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="2455f-178">Usare port, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="2455f-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

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

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="2455f-179">Usare encryptedCredential per autenticazione e gateway</span><span class="sxs-lookup"><span data-stu-id="2455f-179">Use encryptedCredential for authentication and gateway</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="2455f-180">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="2455f-180">Dataset properties</span></span>
<span data-ttu-id="2455f-181">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="2455f-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="2455f-182">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati.</span><span class="sxs-lookup"><span data-stu-id="2455f-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="2455f-183">La sezione **typeProperties** è diversa per ogni tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="2455f-183">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="2455f-184">Fornisce informazioni specifiche del tipo di set di dati.</span><span class="sxs-lookup"><span data-stu-id="2455f-184">It provides information that is specific to the dataset type.</span></span> <span data-ttu-id="2455f-185">La sezione **typeProperties** per un set di dati di tipo **FileShare** presenta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="2455f-185">The **typeProperties** section for a dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="2455f-186">Proprietà</span><span class="sxs-lookup"><span data-stu-id="2455f-186">Property</span></span> | <span data-ttu-id="2455f-187">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2455f-187">Description</span></span> | <span data-ttu-id="2455f-188">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2455f-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2455f-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="2455f-189">folderPath</span></span> |<span data-ttu-id="2455f-190">Sottopercorso alla cartella.</span><span class="sxs-lookup"><span data-stu-id="2455f-190">Subpath to the folder.</span></span> <span data-ttu-id="2455f-191">Usare il carattere di escape "\" per i caratteri speciali nella stringa.</span><span class="sxs-lookup"><span data-stu-id="2455f-191">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="2455f-192">Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .</span><span class="sxs-lookup"><span data-stu-id="2455f-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="2455f-193">È possibile combinare questa proprietà con **partitionBy** per ottenere percorsi di cartelle basati su data e ora di inizio e fine delle sezioni.</span><span class="sxs-lookup"><span data-stu-id="2455f-193">You can combine this property with **partitionBy** to have folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="2455f-194">Sì</span><span class="sxs-lookup"><span data-stu-id="2455f-194">Yes</span></span> |
| <span data-ttu-id="2455f-195">fileName</span><span class="sxs-lookup"><span data-stu-id="2455f-195">fileName</span></span> |<span data-ttu-id="2455f-196">Specificare il nome del file in **folderPath** se si vuole che la tabella faccia riferimento a un file specifico nella cartella.</span><span class="sxs-lookup"><span data-stu-id="2455f-196">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="2455f-197">Se non si specifica alcun valore per questa proprietà, la tabella punta a tutti i file nella cartella.</span><span class="sxs-lookup"><span data-stu-id="2455f-197">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="2455f-198">Quando **fileName** non viene specificato per un set di dati di output, il formato del nome del file generato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="2455f-198">When **fileName** is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="2455f-199">Data<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="2455f-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="2455f-200">No</span><span class="sxs-lookup"><span data-stu-id="2455f-200">No</span></span> |
| <span data-ttu-id="2455f-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="2455f-201">fileFilter</span></span> |<span data-ttu-id="2455f-202">Specificare un filtro da usare per selezionare un sottoinsieme di file in **folderPath** anziché tutti i file.</span><span class="sxs-lookup"><span data-stu-id="2455f-202">Specify a filter to be used to select a subset of files in the **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="2455f-203">I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).</span><span class="sxs-lookup"><span data-stu-id="2455f-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="2455f-204">Esempio 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="2455f-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="2455f-205">Esempio 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="2455f-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="2455f-206">**fileFilter** è applicabile per un set di dati di input FileShare.</span><span class="sxs-lookup"><span data-stu-id="2455f-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="2455f-207">Questa proprietà non è supportata con Hadoop Distributed File System (HDFS).</span><span class="sxs-lookup"><span data-stu-id="2455f-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="2455f-208">No</span><span class="sxs-lookup"><span data-stu-id="2455f-208">No</span></span> |
| <span data-ttu-id="2455f-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="2455f-209">partitionedBy</span></span> |<span data-ttu-id="2455f-210">Usata per specificare una proprietà **folderPath** e **fileName** dinamica per i dati della serie temporale.</span><span class="sxs-lookup"><span data-stu-id="2455f-210">Used to specify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="2455f-211">È ad esempio possibile specificare un **folderPath** contenente i parametri per ogni ora di dati.</span><span class="sxs-lookup"><span data-stu-id="2455f-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="2455f-212">No</span><span class="sxs-lookup"><span data-stu-id="2455f-212">No</span></span> |
| <span data-ttu-id="2455f-213">format</span><span class="sxs-lookup"><span data-stu-id="2455f-213">format</span></span> | <span data-ttu-id="2455f-214">Sono supportati i tipi di formato seguenti: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="2455f-214">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="2455f-215">Impostare la proprietà **type** nell'area format su uno di questi valori.</span><span class="sxs-lookup"><span data-stu-id="2455f-215">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="2455f-216">Per altre informazioni, vedere le sezioni [Formato testo](data-factory-supported-file-and-compression-formats.md#text-format), [Formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [Formato AVRO](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato OCR](data-factory-supported-file-and-compression-formats.md#orc-format) e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="2455f-216">For more information, see the [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="2455f-217">Per copiare i file così come sono tra archivi basati su file (copia binaria), è possibile ignorare la sezione del formato nelle definizioni dei set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="2455f-217">If you want to copy files as they are between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="2455f-218">No</span><span class="sxs-lookup"><span data-stu-id="2455f-218">No</span></span> |
| <span data-ttu-id="2455f-219">compressione</span><span class="sxs-lookup"><span data-stu-id="2455f-219">compression</span></span> | <span data-ttu-id="2455f-220">Specificare il tipo e il livello di compressione dei dati.</span><span class="sxs-lookup"><span data-stu-id="2455f-220">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="2455f-221">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**, mentre i livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="2455f-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="2455f-222">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="2455f-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="2455f-223">No</span><span class="sxs-lookup"><span data-stu-id="2455f-223">No</span></span> |
| <span data-ttu-id="2455f-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="2455f-224">useBinaryTransfer</span></span> |<span data-ttu-id="2455f-225">Specificare se usare la modalità di trasferimento binario.</span><span class="sxs-lookup"><span data-stu-id="2455f-225">Specify whether to use the binary transfer mode.</span></span> <span data-ttu-id="2455f-226">I valori sono true per la modalità binaria (valore predefinito) e false per ASCII.</span><span class="sxs-lookup"><span data-stu-id="2455f-226">The values are true for binary mode (this is the default value), and false for ASCII.</span></span> <span data-ttu-id="2455f-227">Questa proprietà può essere usata solo quando il tipo di servizio collegato associato è di tipo: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="2455f-227">This property can only be used when the associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="2455f-228">No</span><span class="sxs-lookup"><span data-stu-id="2455f-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="2455f-229">**fileName** e **fileFilter** non possono essere usati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="2455f-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-the-partionedby-property"></a><span data-ttu-id="2455f-230">Usare la proprietà partionedBy</span><span class="sxs-lookup"><span data-stu-id="2455f-230">Use the partionedBy property</span></span>
<span data-ttu-id="2455f-231">Come indicato nella sezione precedente, è possibile specificare un valore **folderPath** e **fileName** dinamico per i dati delle serie temporali con la proprietà **partitionedBy**.</span><span class="sxs-lookup"><span data-stu-id="2455f-231">As mentioned in the previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with the **partitionedBy** property.</span></span>

<span data-ttu-id="2455f-232">Per informazioni sui set di dati delle serie temporali, sulla pianificazione e sulle sezioni, vedere gli articoli relativi a [creazione di set di dati](data-factory-create-datasets.md), [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md) e [creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="2455f-232">To learn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="2455f-233">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="2455f-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="2455f-234">In questo esempio {Slice} viene sostituito con il valore della variabile di sistema SliceStart di Data Factory nel formato specificato (AAAAMMGGHH).</span><span class="sxs-lookup"><span data-stu-id="2455f-234">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart, in the format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="2455f-235">SliceStart fa riferimento all'ora di inizio della sezione.</span><span class="sxs-lookup"><span data-stu-id="2455f-235">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="2455f-236">Il percorso cartella è diverso per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="2455f-236">The folder path is different for each slice.</span></span> <span data-ttu-id="2455f-237">Ad esempio: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="2455f-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="2455f-238">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="2455f-238">Sample 2</span></span>

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
<span data-ttu-id="2455f-239">In questo esempio l'anno, il mese, il giorno e l'ora di SliceStart vengono estratti in variabili separate che vengono usate dalle proprietà **folderPath** e **fileName**.</span><span class="sxs-lookup"><span data-stu-id="2455f-239">In this example, the year, month, day, and time of SliceStart are extracted into separate variables that are used by the **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="2455f-240">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="2455f-240">Copy activity properties</span></span>
<span data-ttu-id="2455f-241">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, vedere l'articolo sulla [creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="2455f-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="2455f-242">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="2455f-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="2455f-243">D'altra parte, le proprietà disponibili nella sezione **typeProperties** dell'attività variano in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="2455f-243">Properties available in the **typeProperties** section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="2455f-244">Per l'attività di copia, le proprietà del tipo variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="2455f-244">For the copy activity, the type properties vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="2455f-245">Nell'attività di copia con origine di tipo **FileSystemSource**, nella sezione **typeProperties** sono disponibili le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="2455f-245">In copy activity, when the source is of type **FileSystemSource**, the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="2455f-246">Proprietà</span><span class="sxs-lookup"><span data-stu-id="2455f-246">Property</span></span> | <span data-ttu-id="2455f-247">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2455f-247">Description</span></span> | <span data-ttu-id="2455f-248">Valori consentiti</span><span class="sxs-lookup"><span data-stu-id="2455f-248">Allowed values</span></span> | <span data-ttu-id="2455f-249">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2455f-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2455f-250">ricorsiva</span><span class="sxs-lookup"><span data-stu-id="2455f-250">recursive</span></span> |<span data-ttu-id="2455f-251">Indica se i dati vengono letti in modo ricorsivo dalle cartelle secondarie o solo dalla cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="2455f-251">Indicates whether the data is read recursively from the subfolders, or only from the specified folder.</span></span> |<span data-ttu-id="2455f-252">True, False (valore predefinito)</span><span class="sxs-lookup"><span data-stu-id="2455f-252">True, False (default)</span></span> |<span data-ttu-id="2455f-253">No</span><span class="sxs-lookup"><span data-stu-id="2455f-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-to-azure-blob"></a><span data-ttu-id="2455f-254">Esempio JSON: copiare i dati dal server FTP in BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="2455f-254">JSON example: Copy data from FTP server to Azure Blob</span></span>
<span data-ttu-id="2455f-255">Questo esempio illustra come copiare dati dal server FTP in Archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="2455f-255">This sample shows how to copy data from an FTP server to Azure Blob storage.</span></span> <span data-ttu-id="2455f-256">I dati possono tuttavia essere copiati direttamente in uno qualsiasi dei sink indicati nella sezione [Archivi dati e formati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats), usando l'attività di copia in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2455f-256">However, data can be copied directly to any of the sinks stated in the [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using the copy activity in Data Factory.</span></span>  

<span data-ttu-id="2455f-257">Gli esempi seguenti specificano le definizioni JSON di esempio da usare per creare una pipeline con il [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="2455f-257">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="2455f-258">Un servizio collegato di tipo [FtpServer](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="2455f-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="2455f-259">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="2455f-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="2455f-260">Un [set di dati](data-factory-create-datasets.md) di input di tipo [FileShare](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="2455f-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="2455f-261">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="2455f-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="2455f-262">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="2455f-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="2455f-263">Nell'esempio i dati vengono copiati da un server FTP a un BLOB di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="2455f-263">The sample copies data from an FTP server to an Azure blob every hour.</span></span> <span data-ttu-id="2455f-264">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="2455f-264">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="2455f-265">Servizio collegato FTP</span><span class="sxs-lookup"><span data-stu-id="2455f-265">FTP linked service</span></span>

<span data-ttu-id="2455f-266">Questo esempio usa l'autenticazione di base con il nome utente e la password in testo normale.</span><span class="sxs-lookup"><span data-stu-id="2455f-266">This example uses basic authentication, with the user name and password in plain text.</span></span> <span data-ttu-id="2455f-267">È possibile anche usare uno dei tre metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2455f-267">You can also use one of the following ways:</span></span>

* <span data-ttu-id="2455f-268">Autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="2455f-268">Anonymous authentication</span></span>
* <span data-ttu-id="2455f-269">Autenticazione di base con credenziali crittografate</span><span class="sxs-lookup"><span data-stu-id="2455f-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="2455f-270">FTP su SSL/TLS (FTPS)</span><span class="sxs-lookup"><span data-stu-id="2455f-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="2455f-271">Per i diversi tipi di autenticazione disponibili, vedere la sezione relativa al [servizio collegato FTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2455f-271">See the [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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
### <a name="azure-storage-linked-service"></a><span data-ttu-id="2455f-272">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2455f-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="2455f-273">Set di dati di input FTP</span><span class="sxs-lookup"><span data-stu-id="2455f-273">FTP input dataset</span></span>

<span data-ttu-id="2455f-274">Questo set di dati fa riferimento alla cartella FTP `mysharedfolder` e al file `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="2455f-274">This dataset refers to the FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="2455f-275">La pipeline copia il file nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="2455f-275">The pipeline copies the file to the destination.</span></span>

<span data-ttu-id="2455f-276">Impostando **external** su **true** si comunica al servizio data factory che il set di dati è esterno alla data factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="2455f-276">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory, and is not produced by an activity in the data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="2455f-277">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="2455f-277">Azure Blob output dataset</span></span>

<span data-ttu-id="2455f-278">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="2455f-278">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="2455f-279">Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="2455f-279">The folder path for the blob is dynamically evaluated, based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="2455f-280">Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="2455f-280">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="2455f-281">Un'attività di copia in una pipeline con un'origine su file system e un sink BLOB</span><span class="sxs-lookup"><span data-stu-id="2455f-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="2455f-282">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="2455f-282">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="2455f-283">Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **FileSystemSource** e il tipo di **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2455f-283">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and the **sink** type is set to **BlobSink**.</span></span>

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
> <span data-ttu-id="2455f-284">Per eseguire il mapping dal set di dati di origine alle colonne del set di dati sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2455f-284">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2455f-285">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2455f-285">Next steps</span></span>
<span data-ttu-id="2455f-286">Vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="2455f-286">See the following articles:</span></span>

* <span data-ttu-id="2455f-287">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md) .</span><span class="sxs-lookup"><span data-stu-id="2455f-287">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="2455f-288">Per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia, vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="2455f-288">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
