---
title: Spostare dati da un'origine HTTP - Azure | Microsoft Docs
description: Informazioni su come spostare dati da un'origine HTTP locale o cloud mediante Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 3cc1bd293868b0bb093f617ac12e16c26780fc89
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="f16e3-103">Spostare i dati da un'origine HTTP usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f16e3-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="f16e3-104">Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare dati da un'origine HTTP locale o cloud a un archivio dati sink supportato.</span><span class="sxs-lookup"><span data-stu-id="f16e3-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from an on-premises/cloud HTTP endpoint to a supported sink data store.</span></span> <span data-ttu-id="f16e3-105">Questo articolo si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con attività di copia e l'elenco degli archivi dati supportati come origini/sink.</span><span class="sxs-lookup"><span data-stu-id="f16e3-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="f16e3-106">Data Factory supporta attualmente solo lo spostamento di dati da un'origine HTTP ad altri archivi dati, non da altri archivi dati a un'origine HTTP.</span><span class="sxs-lookup"><span data-stu-id="f16e3-106">Data factory currently supports only moving data from an HTTP source to other data stores, but not moving data from other data stores to an HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="f16e3-107">Scenari supportati e tipi di autenticazione</span><span class="sxs-lookup"><span data-stu-id="f16e3-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="f16e3-108">È possibile usare questo connettor eHTTP per recuperare dati da **endpoint HTTP/s cloud e locali** usando il metodo HTTP **GET** o **POST**.</span><span class="sxs-lookup"><span data-stu-id="f16e3-108">You can use this HTTP connector to retrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="f16e3-109">Sono supportati i seguenti tipi di autenticazione: **Anonymous**, **Basic**, **Digest**, **Windows** e **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="f16e3-109">The following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="f16e3-110">Si noti la differenza tra questo connettore e [il connettore tabella Web](data-factory-web-table-connector.md): quest'ultimo viene usato per estrarre il contenuto di una tabella da una pagina Web HTML.</span><span class="sxs-lookup"><span data-stu-id="f16e3-110">Note the difference between this connector and the [Web table connector](data-factory-web-table-connector.md) is: the latter is used to extract table content from web HTML page.</span></span>

<span data-ttu-id="f16e3-111">Quando si copiano dati da un endpoint HTTP locale, è necessario installare un gateway di gestione dati nella macchina virtuale di Azure o nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="f16e3-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in the on-premises environment/Azure VM.</span></span> <span data-ttu-id="f16e3-112">Vedere l'articolo sullo [spostamento di dati tra sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) per informazioni sul Gateway di gestione dati e per istruzioni dettagliate sulla configurazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="f16e3-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f16e3-113">Introduzione</span><span class="sxs-lookup"><span data-stu-id="f16e3-113">Getting started</span></span>
<span data-ttu-id="f16e3-114">È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine HTTP usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="f16e3-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="f16e3-115">Il modo più semplice per creare una pipeline è usare la **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="f16e3-115">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="f16e3-116">Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="f16e3-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

- <span data-ttu-id="f16e3-117">È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="f16e3-117">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f16e3-118">Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="f16e3-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> <span data-ttu-id="f16e3-119">Per gli esempi JSON per copiare i dati dall'origine HTTP in archiviazione BLOB di Azure, vedere la sezione degli [esempi JSON](#json-examples) in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f16e3-119">For JSON samples to copy data from HTTP source to Azure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f16e3-120">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="f16e3-120">Linked service properties</span></span>
<span data-ttu-id="f16e3-121">La tabella seguente contiene le descrizioni degli elementi JSON specifici del servizio collegato HTTP.</span><span class="sxs-lookup"><span data-stu-id="f16e3-121">The following table provides description for JSON elements specific to HTTP linked service.</span></span>

| <span data-ttu-id="f16e3-122">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f16e3-122">Property</span></span> | <span data-ttu-id="f16e3-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f16e3-123">Description</span></span> | <span data-ttu-id="f16e3-124">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="f16e3-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f16e3-125">type</span><span class="sxs-lookup"><span data-stu-id="f16e3-125">type</span></span> | <span data-ttu-id="f16e3-126">La proprietà type deve essere impostata su: `Http`.</span><span class="sxs-lookup"><span data-stu-id="f16e3-126">The type property must be set to: `Http`.</span></span> | <span data-ttu-id="f16e3-127">Sì</span><span class="sxs-lookup"><span data-stu-id="f16e3-127">Yes</span></span> |
| <span data-ttu-id="f16e3-128">URL</span><span class="sxs-lookup"><span data-stu-id="f16e3-128">url</span></span> | <span data-ttu-id="f16e3-129">URL di base al server Web</span><span class="sxs-lookup"><span data-stu-id="f16e3-129">Base URL to the Web Server</span></span> | <span data-ttu-id="f16e3-130">Sì</span><span class="sxs-lookup"><span data-stu-id="f16e3-130">Yes</span></span> |
| <span data-ttu-id="f16e3-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="f16e3-131">authenticationType</span></span> | <span data-ttu-id="f16e3-132">Specifica il tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f16e3-132">Specifies the authentication type.</span></span> <span data-ttu-id="f16e3-133">I valori consentiti sono: **Anonymous**, **Basic**, **Digest**, **Windows** e **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="f16e3-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="f16e3-134">Fare riferimento alle sezioni sotto questa tabella per altre proprietà e altri esempi JSON per questi tipi di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f16e3-134">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="f16e3-135">Sì</span><span class="sxs-lookup"><span data-stu-id="f16e3-135">Yes</span></span> |
| <span data-ttu-id="f16e3-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="f16e3-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="f16e3-137">Specificare se abilitare la convalida del certificato SSL del server se l'origine è un server Web HTTPS</span><span class="sxs-lookup"><span data-stu-id="f16e3-137">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="f16e3-138">No, il valore predefinito è true</span><span class="sxs-lookup"><span data-stu-id="f16e3-138">No, default is true</span></span> |
| <span data-ttu-id="f16e3-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="f16e3-139">gatewayName</span></span> | <span data-ttu-id="f16e3-140">Nome del gateway di gestione dati per connettersi a un'origine HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="f16e3-140">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="f16e3-141">Sì se si copiano i dati da un'origine HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="f16e3-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="f16e3-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="f16e3-142">encryptedCredential</span></span> | <span data-ttu-id="f16e3-143">Credenziali crittografate per accedere all'endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="f16e3-143">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="f16e3-144">Generate automaticamente quando si configurano le informazioni di autenticazione nella procedura di copia guidata o nella finestra di dialogo popup ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="f16e3-144">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="f16e3-145">No.</span><span class="sxs-lookup"><span data-stu-id="f16e3-145">No.</span></span> <span data-ttu-id="f16e3-146">Applicare solo se si copiano i dati da un server HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="f16e3-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="f16e3-147">Vedere [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) per informazioni dettagliate sull'impostazione delle credenziali per un'origine dati connettore HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="f16e3-147">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="f16e3-148">Usando l'autenticazione Basic, Digest o Windows</span><span class="sxs-lookup"><span data-stu-id="f16e3-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="f16e3-149">Impostare `authenticationType` come `Basic`, `Digest`, o `Windows` e specificare le proprietà seguenti oltre a quelle generiche del connettore HTTP illustrate in precedenza:</span><span class="sxs-lookup"><span data-stu-id="f16e3-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="f16e3-150">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f16e3-150">Property</span></span> | <span data-ttu-id="f16e3-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f16e3-151">Description</span></span> | <span data-ttu-id="f16e3-152">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="f16e3-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f16e3-153">username</span><span class="sxs-lookup"><span data-stu-id="f16e3-153">username</span></span> | <span data-ttu-id="f16e3-154">Nome utente per accedere all'endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="f16e3-154">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="f16e3-155">Sì</span><span class="sxs-lookup"><span data-stu-id="f16e3-155">Yes</span></span> |
| <span data-ttu-id="f16e3-156">password</span><span class="sxs-lookup"><span data-stu-id="f16e3-156">password</span></span> | <span data-ttu-id="f16e3-157">Password per l'utente (nome utente).</span><span class="sxs-lookup"><span data-stu-id="f16e3-157">Password for the user (username).</span></span> | <span data-ttu-id="f16e3-158">Sì</span><span class="sxs-lookup"><span data-stu-id="f16e3-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="f16e3-159">Esempio: usando l'autenticazione Basic, Digest or Windows</span><span class="sxs-lookup"><span data-stu-id="f16e3-159">Example: using Basic, Digest, or Windows authentication</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="f16e3-160">Usando l'autenticazione ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="f16e3-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="f16e3-161">Per usare l'autenticazione di base, impostare `authenticationType` come `ClientCertificate` e specificare le proprietà seguenti oltre a quelle generiche del connettore HTTP introdotte in precedenza:</span><span class="sxs-lookup"><span data-stu-id="f16e3-161">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="f16e3-162">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f16e3-162">Property</span></span> | <span data-ttu-id="f16e3-163">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f16e3-163">Description</span></span> | <span data-ttu-id="f16e3-164">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="f16e3-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f16e3-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="f16e3-165">embeddedCertData</span></span> | <span data-ttu-id="f16e3-166">Contenuto con codifica Base 64 dei dati binari del file di scambio di informazioni personali (PFX, Personal Information Exchange).</span><span class="sxs-lookup"><span data-stu-id="f16e3-166">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="f16e3-167">Specificare `embeddedCertData` o `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="f16e3-167">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="f16e3-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="f16e3-168">certThumbprint</span></span> | <span data-ttu-id="f16e3-169">L'identificazione personale del certificato installato nell'archivio certificati del computer gateway.</span><span class="sxs-lookup"><span data-stu-id="f16e3-169">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="f16e3-170">Applicare solo se si copiano i dati da un'origine HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="f16e3-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="f16e3-171">Specificare `embeddedCertData` o `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="f16e3-171">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="f16e3-172">password</span><span class="sxs-lookup"><span data-stu-id="f16e3-172">password</span></span> | <span data-ttu-id="f16e3-173">Password associata al certificato.</span><span class="sxs-lookup"><span data-stu-id="f16e3-173">Password associated with the certificate.</span></span> | <span data-ttu-id="f16e3-174">No</span><span class="sxs-lookup"><span data-stu-id="f16e3-174">No</span></span> |

<span data-ttu-id="f16e3-175">Se si usa `certThumbprint` per l'autenticazione e il certificato è installato nell'archivio personale del computer locale, è necessario concedere l'autorizzazione di lettura per il servizio gateway:</span><span class="sxs-lookup"><span data-stu-id="f16e3-175">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="f16e3-176">Avviare Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="f16e3-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="f16e3-177">Aggiungere lo snap-in **Certificati** con il **Computer locale** come destinazione.</span><span class="sxs-lookup"><span data-stu-id="f16e3-177">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="f16e3-178">Espandere **Certificati**, **Personali** e fare clic su **Certificati**.</span><span class="sxs-lookup"><span data-stu-id="f16e3-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="f16e3-179">Fare clic con il tasto destro del mouse sul certificato dall'archivio personale, quindi selezionare **Tutte le attività**->**Gestisci chiavi private...**</span><span class="sxs-lookup"><span data-stu-id="f16e3-179">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="f16e3-180">Nella scheda **Sicurezza** aggiungere l'account utente in cui è in esecuzione il Servizio host di Gateway di gestione dati con l'accesso in lettura al certificato.</span><span class="sxs-lookup"><span data-stu-id="f16e3-180">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="f16e3-181">Esempio: utilizzo di un certificato client</span><span class="sxs-lookup"><span data-stu-id="f16e3-181">Example: using client certificate</span></span>
<span data-ttu-id="f16e3-182">Questo servizio collegato collega la data factory a un server Web HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="f16e3-182">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="f16e3-183">Usa un file del certificato client installato nel computer che dispone del Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="f16e3-183">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="f16e3-184">Esempio: utilizzo di un certificato client in un file</span><span class="sxs-lookup"><span data-stu-id="f16e3-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="f16e3-185">Questo servizio collegato collega la data factory a un server Web HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="f16e3-185">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="f16e3-186">Usa un file del certificato client nel computer con installato il Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="f16e3-186">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="f16e3-187">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="f16e3-187">Dataset properties</span></span>
<span data-ttu-id="f16e3-188">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="f16e3-188">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f16e3-189">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="f16e3-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="f16e3-190">La sezione **typeProperties** è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="f16e3-190">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="f16e3-191">La sezione typeProperties per il set di dati di tipo **Http** presenta le proprietà seguenti</span><span class="sxs-lookup"><span data-stu-id="f16e3-191">The typeProperties section for dataset of type **Http** has the following properties</span></span>

| <span data-ttu-id="f16e3-192">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f16e3-192">Property</span></span> | <span data-ttu-id="f16e3-193">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f16e3-193">Description</span></span> | <span data-ttu-id="f16e3-194">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="f16e3-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f16e3-195">type</span><span class="sxs-lookup"><span data-stu-id="f16e3-195">type</span></span> | <span data-ttu-id="f16e3-196">Specifica il tipo del set di dati.</span><span class="sxs-lookup"><span data-stu-id="f16e3-196">Specified the type of the dataset.</span></span> <span data-ttu-id="f16e3-197">deve essere impostato su `Http`.</span><span class="sxs-lookup"><span data-stu-id="f16e3-197">must be set to `Http`.</span></span> | <span data-ttu-id="f16e3-198">Sì</span><span class="sxs-lookup"><span data-stu-id="f16e3-198">Yes</span></span> |
| <span data-ttu-id="f16e3-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="f16e3-199">relativeUrl</span></span> | <span data-ttu-id="f16e3-200">URL relativo della risorsa che contiene i dati.</span><span class="sxs-lookup"><span data-stu-id="f16e3-200">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="f16e3-201">Quando non è specificato alcun percorso, viene usato solo l'URL specificato nella definizione del servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="f16e3-201">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="f16e3-202">Per creare un URL dinamico, è possibile usare [funzioni di Data Factory e variabili di sistema](data-factory-functions-variables.md), ad esempio "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span><span class="sxs-lookup"><span data-stu-id="f16e3-202">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="f16e3-203">No</span><span class="sxs-lookup"><span data-stu-id="f16e3-203">No</span></span> |
| <span data-ttu-id="f16e3-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="f16e3-204">requestMethod</span></span> | <span data-ttu-id="f16e3-205">Metodo HTTP.</span><span class="sxs-lookup"><span data-stu-id="f16e3-205">Http method.</span></span> <span data-ttu-id="f16e3-206">I valori consentiti sono **GET** o **POST**.</span><span class="sxs-lookup"><span data-stu-id="f16e3-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="f16e3-207">No.</span><span class="sxs-lookup"><span data-stu-id="f16e3-207">No.</span></span> <span data-ttu-id="f16e3-208">Il valore predefinito è `GET`.</span><span class="sxs-lookup"><span data-stu-id="f16e3-208">Default is `GET`.</span></span> |
| <span data-ttu-id="f16e3-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="f16e3-209">additionalHeaders</span></span> | <span data-ttu-id="f16e3-210">Intestazioni richiesta HTTP aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="f16e3-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="f16e3-211">No</span><span class="sxs-lookup"><span data-stu-id="f16e3-211">No</span></span> |
| <span data-ttu-id="f16e3-212">requestBody</span><span class="sxs-lookup"><span data-stu-id="f16e3-212">requestBody</span></span> | <span data-ttu-id="f16e3-213">Il corpo della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="f16e3-213">Body for HTTP request.</span></span> | <span data-ttu-id="f16e3-214">No</span><span class="sxs-lookup"><span data-stu-id="f16e3-214">No</span></span> |
| <span data-ttu-id="f16e3-215">format</span><span class="sxs-lookup"><span data-stu-id="f16e3-215">format</span></span> | <span data-ttu-id="f16e3-216">Se si desidera semplicemente **recuperare i dati dall'endpoint HTTP così come sono** senza analizzarli, ignorare questa impostazione di formato.</span><span class="sxs-lookup"><span data-stu-id="f16e3-216">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="f16e3-217">Se si desidera analizzare i contenuti di risposta HTTP durante la copia, sono supportati i tipi di formato seguenti: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="f16e3-217">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="f16e3-218">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="f16e3-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="f16e3-219">No</span><span class="sxs-lookup"><span data-stu-id="f16e3-219">No</span></span> |
| <span data-ttu-id="f16e3-220">compressione</span><span class="sxs-lookup"><span data-stu-id="f16e3-220">compression</span></span> | <span data-ttu-id="f16e3-221">Specificare il tipo e il livello di compressione dei dati.</span><span class="sxs-lookup"><span data-stu-id="f16e3-221">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="f16e3-222">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="f16e3-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="f16e3-223">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="f16e3-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="f16e3-224">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="f16e3-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="f16e3-225">No</span><span class="sxs-lookup"><span data-stu-id="f16e3-225">No</span></span> |

### <a name="example-using-the-get-default-method"></a><span data-ttu-id="f16e3-226">Esempio: usando il metodo GET (predefinito)</span><span class="sxs-lookup"><span data-stu-id="f16e3-226">Example: using the GET (default) method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-the-post-method"></a><span data-ttu-id="f16e3-227">Esempio: usando il metodo POST</span><span class="sxs-lookup"><span data-stu-id="f16e3-227">Example: using the POST method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="f16e3-228">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="f16e3-228">Copy activity properties</span></span>
<span data-ttu-id="f16e3-229">Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="f16e3-229">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f16e3-230">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="f16e3-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="f16e3-231">D'altra parte, le proprietà disponibili nella sezione **typeProperties** dell'attività variano in base al tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="f16e3-231">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="f16e3-232">Per l'attività di copia variano in base ai tipi di origine e sink.</span><span class="sxs-lookup"><span data-stu-id="f16e3-232">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="f16e3-233">Quando l'origine nell'attività di copia è di tipo **HttpSource**, sono supportate le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="f16e3-233">Currently, when the source in copy activity is of type **HttpSource**, the following properties are supported.</span></span>

| <span data-ttu-id="f16e3-234">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f16e3-234">Property</span></span> | <span data-ttu-id="f16e3-235">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f16e3-235">Description</span></span> | <span data-ttu-id="f16e3-236">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="f16e3-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="f16e3-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="f16e3-237">httpRequestTimeout</span></span> | <span data-ttu-id="f16e3-238">Il timeout (TimeSpan) durante il quale la richiesta HTTP attende una risposta.</span><span class="sxs-lookup"><span data-stu-id="f16e3-238">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="f16e3-239">Si tratta del timeout per ottenere una risposta, non per leggere i dati della risposta stessa.</span><span class="sxs-lookup"><span data-stu-id="f16e3-239">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="f16e3-240">No.</span><span class="sxs-lookup"><span data-stu-id="f16e3-240">No.</span></span> <span data-ttu-id="f16e3-241">Valore predefinito: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="f16e3-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="f16e3-242">Formati di file e di compressione supportati</span><span class="sxs-lookup"><span data-stu-id="f16e3-242">Supported file and compression formats</span></span>
<span data-ttu-id="f16e3-243">Per i dettagli, vedere l'articolo relativo ai [file e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="f16e3-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="f16e3-244">Esempi JSON</span><span class="sxs-lookup"><span data-stu-id="f16e3-244">JSON examples</span></span>
<span data-ttu-id="f16e3-245">L'esempio seguente fornisce le definizioni JSON campione da usare per creare una pipeline con il [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f16e3-245">The following example provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f16e3-246">Illustrano come copiare dati da un'origine HTTP in un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="f16e3-246">They show how to copy data from HTTP source to Azure Blob Storage.</span></span> <span data-ttu-id="f16e3-247">Tuttavia, i dati possono essere copiati **direttamente** da una delle origini in qualsiasi sink dichiarato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando l'attività di copia in Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="f16e3-247">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-to-azure-blob-storage"></a><span data-ttu-id="f16e3-248">Esempio: copiare dati da un'origine HTTP in un archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="f16e3-248">Example: Copy data from HTTP source to Azure Blob Storage</span></span>
<span data-ttu-id="f16e3-249">La soluzione di Data Factory per questo esempio contiene le entità Data Factory seguenti:</span><span class="sxs-lookup"><span data-stu-id="f16e3-249">The Data Factory solution for this sample contains the following Data Factory entities:</span></span>

1. <span data-ttu-id="f16e3-250">Un servizio collegato di tipo [HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f16e3-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="f16e3-251">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f16e3-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f16e3-252">Un [set di dati](data-factory-create-datasets.md) di input di tipo [HTTP](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f16e3-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="f16e3-253">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f16e3-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="f16e3-254">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [HttpSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f16e3-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f16e3-255">Nell'esempio i dati vengono copiati da un'origine HTTP a un BLOB di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="f16e3-255">The sample copies data from an HTTP source to an Azure blob every hour.</span></span> <span data-ttu-id="f16e3-256">Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="f16e3-256">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="f16e3-257">Servizio collegato HTTP</span><span class="sxs-lookup"><span data-stu-id="f16e3-257">HTTP linked service</span></span>
<span data-ttu-id="f16e3-258">Questo esempio usa il servizio collegato HTTP con l'autenticazione anonima.</span><span class="sxs-lookup"><span data-stu-id="f16e3-258">This example uses the HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="f16e3-259">Per i diversi tipi di autenticazione disponibili, vedere la sezione relativa al [servizio collegato HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f16e3-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="f16e3-260">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="f16e3-260">Azure Storage linked service</span></span>

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

### <a name="http-input-dataset"></a><span data-ttu-id="f16e3-261">Set di dati di input HTTP</span><span class="sxs-lookup"><span data-stu-id="f16e3-261">HTTP input dataset</span></span>
<span data-ttu-id="f16e3-262">Impostando **external** su **true** si comunica al servizio Data Factory che il set di dati è esterno alla data factory e non è prodotto da un'attività al suo interno.</span><span class="sxs-lookup"><span data-stu-id="f16e3-262">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="f16e3-263">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="f16e3-263">Azure Blob output dataset</span></span>

<span data-ttu-id="f16e3-264">I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="f16e3-264">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="f16e3-265">Pipeline con attività di copia</span><span class="sxs-lookup"><span data-stu-id="f16e3-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="f16e3-266">La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="f16e3-266">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="f16e3-267">Nella definizione JSON della pipeline, il tipo **source** è impostato su **HttpSource** e il tipo **sink** è impostato su **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f16e3-267">In the pipeline JSON definition, the **source** type is set to **HttpSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="f16e3-268">Vedere [HttpSource](#copy-activity-properties) per l'elenco delle proprietà supportate da HttpSource.</span><span class="sxs-lookup"><span data-stu-id="f16e3-268">See [HttpSource](#copy-activity-properties) for the list of properties supported by the HttpSource.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source to an Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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

> [!NOTE]
> <span data-ttu-id="f16e3-269">Per eseguire il mapping dal set di dati di origine alle colonne del set di dati sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f16e3-269">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f16e3-270">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="f16e3-270">Performance and Tuning</span></span>
<span data-ttu-id="f16e3-271">Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni delle attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="f16e3-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
