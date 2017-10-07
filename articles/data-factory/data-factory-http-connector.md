---
title: aaaMove dati da un'origine HTTP - Azure | Documenti Microsoft
description: Informazioni su come origine dei dati toomove da un locale o un cloud HTTP usando Azure Data Factory.
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
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="de6a0-103">Spostare i dati da un'origine HTTP usando Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="de6a0-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="de6a0-104">In questo articolo descrive come toouse hello attività di copia dei dati toomove Data Factory di Azure da un tooa di endpoint HTTP in locale/cloud supportato archivio dati sink.</span><span class="sxs-lookup"><span data-stu-id="de6a0-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud HTTP endpoint tooa supported sink data store.</span></span> <span data-ttu-id="de6a0-105">In questo articolo si basa su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo che presenta una panoramica generale di spostamento dei dati con l'elenco di attività e hello copia di archivi dati supportata come origine/sink.</span><span class="sxs-lookup"><span data-stu-id="de6a0-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="de6a0-106">Data factory di attualmente supporta solo lo spostamento di dati da un HTTP origine tooother archivi di dati, ma non lo spostamento dei dati da altri dati archivia destinazione tooan HTTP.</span><span class="sxs-lookup"><span data-stu-id="de6a0-106">Data factory currently supports only moving data from an HTTP source tooother data stores, but not moving data from other data stores tooan HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="de6a0-107">Scenari supportati e tipi di autenticazione</span><span class="sxs-lookup"><span data-stu-id="de6a0-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="de6a0-108">È possibile utilizzare HTTP connettore tooretrieve dati **sia in locale e cloud endpoint HTTP/s** mediante il protocollo HTTP **ottenere** o **POST** metodo.</span><span class="sxs-lookup"><span data-stu-id="de6a0-108">You can use this HTTP connector tooretrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="de6a0-109">è supportato i seguenti tipi di autenticazione Hello: **anonimo**, **base**, **Digest**, **Windows**, e  **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="de6a0-109">hello following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="de6a0-110">Si noti la differenza hello tra questo connettore e hello [connettore tabella Web](data-factory-web-table-connector.md) è: hello quest'ultimo è utilizzato tooextract tabella contenuta da una pagina web HTML.</span><span class="sxs-lookup"><span data-stu-id="de6a0-110">Note hello difference between this connector and hello [Web table connector](data-factory-web-table-connector.md) is: hello latter is used tooextract table content from web HTML page.</span></span>

<span data-ttu-id="de6a0-111">Quando si copiano dati da un endpoint HTTP locale, è necessario installare un Gateway di gestione di dati nell'ambiente locale hello/Azure VM.</span><span class="sxs-lookup"><span data-stu-id="de6a0-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="de6a0-112">Vedere [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn articolo sul Gateway di gestione dati e istruzioni dettagliate su come configurare il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="de6a0-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="de6a0-113">introduttiva</span><span class="sxs-lookup"><span data-stu-id="de6a0-113">Getting started</span></span>
<span data-ttu-id="de6a0-114">È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine HTTP usando diversi strumenti/API.</span><span class="sxs-lookup"><span data-stu-id="de6a0-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="de6a0-115">toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**.</span><span class="sxs-lookup"><span data-stu-id="de6a0-115">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="de6a0-116">Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.</span><span class="sxs-lookup"><span data-stu-id="de6a0-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="de6a0-117">È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="de6a0-117">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="de6a0-118">Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.</span><span class="sxs-lookup"><span data-stu-id="de6a0-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="de6a0-119">Per esempi di JSON dati toocopy tooAzure origine HTTP nell'archiviazione Blob, vedere [esempi JSON](#json-examples) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="de6a0-119">For JSON samples toocopy data from HTTP source tooAzure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="de6a0-120">Proprietà del servizio collegato</span><span class="sxs-lookup"><span data-stu-id="de6a0-120">Linked service properties</span></span>
<span data-ttu-id="de6a0-121">Hello nella tabella seguente fornisce una descrizione del servizio specifico tooHTTP collegati gli elementi JSON.</span><span class="sxs-lookup"><span data-stu-id="de6a0-121">hello following table provides description for JSON elements specific tooHTTP linked service.</span></span>

| <span data-ttu-id="de6a0-122">Proprietà</span><span class="sxs-lookup"><span data-stu-id="de6a0-122">Property</span></span> | <span data-ttu-id="de6a0-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="de6a0-123">Description</span></span> | <span data-ttu-id="de6a0-124">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="de6a0-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="de6a0-125">type</span><span class="sxs-lookup"><span data-stu-id="de6a0-125">type</span></span> | <span data-ttu-id="de6a0-126">proprietà di tipo Hello deve essere impostata su: `Http`.</span><span class="sxs-lookup"><span data-stu-id="de6a0-126">hello type property must be set to: `Http`.</span></span> | <span data-ttu-id="de6a0-127">Sì</span><span class="sxs-lookup"><span data-stu-id="de6a0-127">Yes</span></span> |
| <span data-ttu-id="de6a0-128">URL</span><span class="sxs-lookup"><span data-stu-id="de6a0-128">url</span></span> | <span data-ttu-id="de6a0-129">URL toohello Server Web di base</span><span class="sxs-lookup"><span data-stu-id="de6a0-129">Base URL toohello Web Server</span></span> | <span data-ttu-id="de6a0-130">Sì</span><span class="sxs-lookup"><span data-stu-id="de6a0-130">Yes</span></span> |
| <span data-ttu-id="de6a0-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="de6a0-131">authenticationType</span></span> | <span data-ttu-id="de6a0-132">Specifica il tipo di autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="de6a0-132">Specifies hello authentication type.</span></span> <span data-ttu-id="de6a0-133">I valori consentiti sono: **Anonymous**, **Basic**, **Digest**, **Windows** e **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="de6a0-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="de6a0-134">Vedere rispettivamente toosections riportata sotto questa tabella in più proprietà e gli esempi JSON per i tipi di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="de6a0-134">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="de6a0-135">Sì</span><span class="sxs-lookup"><span data-stu-id="de6a0-135">Yes</span></span> |
| <span data-ttu-id="de6a0-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="de6a0-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="de6a0-137">Specificare se il server tooenable SSL la convalida del certificato se l'origine è il Server Web HTTPS</span><span class="sxs-lookup"><span data-stu-id="de6a0-137">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="de6a0-138">No, il valore predefinito è true</span><span class="sxs-lookup"><span data-stu-id="de6a0-138">No, default is true</span></span> |
| <span data-ttu-id="de6a0-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="de6a0-139">gatewayName</span></span> | <span data-ttu-id="de6a0-140">Nome di hello Gateway di gestione dati tooconnect tooan locale origine HTTP.</span><span class="sxs-lookup"><span data-stu-id="de6a0-140">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="de6a0-141">Sì se si copiano i dati da un'origine HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="de6a0-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="de6a0-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="de6a0-142">encryptedCredential</span></span> | <span data-ttu-id="de6a0-143">Credenziali crittografate tooaccess hello endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="de6a0-143">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="de6a0-144">Generati automaticamente quando si configurano le informazioni di autenticazione hello in copia guidata o hello ClickOnce finestra di dialogo popup.</span><span class="sxs-lookup"><span data-stu-id="de6a0-144">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="de6a0-145">No.</span><span class="sxs-lookup"><span data-stu-id="de6a0-145">No.</span></span> <span data-ttu-id="de6a0-146">Applicare solo se si copiano i dati da un server HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="de6a0-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="de6a0-147">Vedere [spostare dati tra origini locali e cloud hello con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) per informazioni dettagliate sull'impostazione delle credenziali per l'origine dati di connettore HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="de6a0-147">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="de6a0-148">Usando l'autenticazione Basic, Digest o Windows</span><span class="sxs-lookup"><span data-stu-id="de6a0-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="de6a0-149">Impostare `authenticationType` come `Basic`, `Digest`, o `Windows`e specificare le proprietà seguenti, oltre alle hello generico connettore HTTP quelli illustrati in precedenza hello:</span><span class="sxs-lookup"><span data-stu-id="de6a0-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="de6a0-150">Proprietà</span><span class="sxs-lookup"><span data-stu-id="de6a0-150">Property</span></span> | <span data-ttu-id="de6a0-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="de6a0-151">Description</span></span> | <span data-ttu-id="de6a0-152">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="de6a0-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="de6a0-153">username</span><span class="sxs-lookup"><span data-stu-id="de6a0-153">username</span></span> | <span data-ttu-id="de6a0-154">Nome utente tooaccess hello endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="de6a0-154">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="de6a0-155">Sì</span><span class="sxs-lookup"><span data-stu-id="de6a0-155">Yes</span></span> |
| <span data-ttu-id="de6a0-156">password</span><span class="sxs-lookup"><span data-stu-id="de6a0-156">password</span></span> | <span data-ttu-id="de6a0-157">Password per l'utente di hello (nomeutente).</span><span class="sxs-lookup"><span data-stu-id="de6a0-157">Password for hello user (username).</span></span> | <span data-ttu-id="de6a0-158">Sì</span><span class="sxs-lookup"><span data-stu-id="de6a0-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="de6a0-159">Esempio: usando l'autenticazione Basic, Digest or Windows</span><span class="sxs-lookup"><span data-stu-id="de6a0-159">Example: using Basic, Digest, or Windows authentication</span></span>

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

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="de6a0-160">Usando l'autenticazione ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="de6a0-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="de6a0-161">impostare l'autenticazione di base toouse, `authenticationType` come `ClientCertificate`e specificare le proprietà seguenti, oltre alle hello generico connettore HTTP quelli illustrati in precedenza hello:</span><span class="sxs-lookup"><span data-stu-id="de6a0-161">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="de6a0-162">Proprietà</span><span class="sxs-lookup"><span data-stu-id="de6a0-162">Property</span></span> | <span data-ttu-id="de6a0-163">Descrizione</span><span class="sxs-lookup"><span data-stu-id="de6a0-163">Description</span></span> | <span data-ttu-id="de6a0-164">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="de6a0-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="de6a0-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="de6a0-165">embeddedCertData</span></span> | <span data-ttu-id="de6a0-166">Hello contenuto con codifica Base64 di dati binari del file di scambio di informazioni personali (PFX) hello.</span><span class="sxs-lookup"><span data-stu-id="de6a0-166">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="de6a0-167">Specificare entrambi hello `embeddedCertData` o `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="de6a0-167">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="de6a0-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="de6a0-168">certThumbprint</span></span> | <span data-ttu-id="de6a0-169">Hello identificazione personale del certificato hello che è stata installata nell'archivio certificati del computer gateway.</span><span class="sxs-lookup"><span data-stu-id="de6a0-169">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="de6a0-170">Applicare solo se si copiano i dati da un'origine HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="de6a0-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="de6a0-171">Specificare entrambi hello `embeddedCertData` o `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="de6a0-171">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="de6a0-172">password</span><span class="sxs-lookup"><span data-stu-id="de6a0-172">password</span></span> | <span data-ttu-id="de6a0-173">Password associata al certificato hello.</span><span class="sxs-lookup"><span data-stu-id="de6a0-173">Password associated with hello certificate.</span></span> | <span data-ttu-id="de6a0-174">No</span><span class="sxs-lookup"><span data-stu-id="de6a0-174">No</span></span> |

<span data-ttu-id="de6a0-175">Se si utilizza `certThumbprint` per hello e autenticazione il certificato è installato nell'archivio personale di hello del computer locale hello, è necessario che il servizio gateway toogrant hello autorizzazione di lettura toohello:</span><span class="sxs-lookup"><span data-stu-id="de6a0-175">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="de6a0-176">Avviare Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="de6a0-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="de6a0-177">Aggiungere hello **certificati** snap-in tale hello destinazioni **Computer locale**.</span><span class="sxs-lookup"><span data-stu-id="de6a0-177">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="de6a0-178">Espandere **Certificati**, **Personali** e fare clic su **Certificati**.</span><span class="sxs-lookup"><span data-stu-id="de6a0-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="de6a0-179">Certificato hello dall'archivio personale hello e scegliere **tutte le attività**->**Gestisci chiavi Private...**</span><span class="sxs-lookup"><span data-stu-id="de6a0-179">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="de6a0-180">In hello **sicurezza** scheda, aggiungere l'account utente di hello in cui è in esecuzione servizio Host di Gateway di gestione di dati con certificato toohello di hello accesso in lettura.</span><span class="sxs-lookup"><span data-stu-id="de6a0-180">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="de6a0-181">Esempio: utilizzo di un certificato client</span><span class="sxs-lookup"><span data-stu-id="de6a0-181">Example: using client certificate</span></span>
<span data-ttu-id="de6a0-182">Questo collegato collegamenti al servizio data factory tooan locale HTTP server web.</span><span class="sxs-lookup"><span data-stu-id="de6a0-182">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="de6a0-183">Usa un certificato client è installato nel computer di hello con Gateway di gestione di dati installati.</span><span class="sxs-lookup"><span data-stu-id="de6a0-183">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="de6a0-184">Esempio: utilizzo di un certificato client in un file</span><span class="sxs-lookup"><span data-stu-id="de6a0-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="de6a0-185">Questo collegato collegamenti al servizio data factory tooan locale HTTP server web.</span><span class="sxs-lookup"><span data-stu-id="de6a0-185">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="de6a0-186">Usa un file del certificato client nel computer di hello con Gateway di gestione di dati installati.</span><span class="sxs-lookup"><span data-stu-id="de6a0-186">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="de6a0-187">Proprietà dei set di dati</span><span class="sxs-lookup"><span data-stu-id="de6a0-187">Dataset properties</span></span>
<span data-ttu-id="de6a0-188">Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="de6a0-188">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="de6a0-189">Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.</span><span class="sxs-lookup"><span data-stu-id="de6a0-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="de6a0-190">Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello.</span><span class="sxs-lookup"><span data-stu-id="de6a0-190">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="de6a0-191">sezione Hello typeProperties per set di dati di tipo **Http** ha hello seguenti proprietà</span><span class="sxs-lookup"><span data-stu-id="de6a0-191">hello typeProperties section for dataset of type **Http** has hello following properties</span></span>

| <span data-ttu-id="de6a0-192">Proprietà</span><span class="sxs-lookup"><span data-stu-id="de6a0-192">Property</span></span> | <span data-ttu-id="de6a0-193">Descrizione</span><span class="sxs-lookup"><span data-stu-id="de6a0-193">Description</span></span> | <span data-ttu-id="de6a0-194">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="de6a0-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="de6a0-195">type</span><span class="sxs-lookup"><span data-stu-id="de6a0-195">type</span></span> | <span data-ttu-id="de6a0-196">Tipo di hello di hello set di dati specificato.</span><span class="sxs-lookup"><span data-stu-id="de6a0-196">Specified hello type of hello dataset.</span></span> <span data-ttu-id="de6a0-197">deve essere impostato troppo`Http`.</span><span class="sxs-lookup"><span data-stu-id="de6a0-197">must be set too`Http`.</span></span> | <span data-ttu-id="de6a0-198">Sì</span><span class="sxs-lookup"><span data-stu-id="de6a0-198">Yes</span></span> |
| <span data-ttu-id="de6a0-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="de6a0-199">relativeUrl</span></span> | <span data-ttu-id="de6a0-200">Una risorsa relativa di URL toohello che contiene dati hello.</span><span class="sxs-lookup"><span data-stu-id="de6a0-200">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="de6a0-201">Quando non viene specificato alcun percorso, viene utilizzato solo URL hello specificato nella definizione di servizio collegato hello.</span><span class="sxs-lookup"><span data-stu-id="de6a0-201">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="de6a0-202">tooconstruct URL dinamico, è possibile utilizzare [funzioni di Data Factory e le variabili di sistema](data-factory-functions-variables.md), ad esempio, "URL relativo": "$$Text.Format ('/ my/report? mese = {0:yyyy}-{0:MM} & fmt = csv', SliceStart)".</span><span class="sxs-lookup"><span data-stu-id="de6a0-202">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="de6a0-203">No</span><span class="sxs-lookup"><span data-stu-id="de6a0-203">No</span></span> |
| <span data-ttu-id="de6a0-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="de6a0-204">requestMethod</span></span> | <span data-ttu-id="de6a0-205">Metodo HTTP.</span><span class="sxs-lookup"><span data-stu-id="de6a0-205">Http method.</span></span> <span data-ttu-id="de6a0-206">I valori consentiti sono **GET** o **POST**.</span><span class="sxs-lookup"><span data-stu-id="de6a0-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="de6a0-207">No.</span><span class="sxs-lookup"><span data-stu-id="de6a0-207">No.</span></span> <span data-ttu-id="de6a0-208">Il valore predefinito è `GET`.</span><span class="sxs-lookup"><span data-stu-id="de6a0-208">Default is `GET`.</span></span> |
| <span data-ttu-id="de6a0-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="de6a0-209">additionalHeaders</span></span> | <span data-ttu-id="de6a0-210">Intestazioni richiesta HTTP aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="de6a0-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="de6a0-211">No</span><span class="sxs-lookup"><span data-stu-id="de6a0-211">No</span></span> |
| <span data-ttu-id="de6a0-212">requestBody</span><span class="sxs-lookup"><span data-stu-id="de6a0-212">requestBody</span></span> | <span data-ttu-id="de6a0-213">Il corpo della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="de6a0-213">Body for HTTP request.</span></span> | <span data-ttu-id="de6a0-214">No</span><span class="sxs-lookup"><span data-stu-id="de6a0-214">No</span></span> |
| <span data-ttu-id="de6a0-215">format</span><span class="sxs-lookup"><span data-stu-id="de6a0-215">format</span></span> | <span data-ttu-id="de6a0-216">Se si desidera toosimply **recuperare i dati di hello da endpoint HTTP come-è** senza analizzarlo, ignorare questa impostazione di formato.</span><span class="sxs-lookup"><span data-stu-id="de6a0-216">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="de6a0-217">Se si desidera tooparse hello HTTP risposta contenuto durante la copia, è supportato i seguenti tipi di formato hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="de6a0-217">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="de6a0-218">Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="de6a0-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="de6a0-219">No</span><span class="sxs-lookup"><span data-stu-id="de6a0-219">No</span></span> |
| <span data-ttu-id="de6a0-220">compressione</span><span class="sxs-lookup"><span data-stu-id="de6a0-220">compression</span></span> | <span data-ttu-id="de6a0-221">Specificare il tipo di hello e livello di compressione per dati hello.</span><span class="sxs-lookup"><span data-stu-id="de6a0-221">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="de6a0-222">I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="de6a0-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="de6a0-223">I livelli supportati sono **Ottimale** e **Più veloce**.</span><span class="sxs-lookup"><span data-stu-id="de6a0-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="de6a0-224">Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="de6a0-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="de6a0-225">No</span><span class="sxs-lookup"><span data-stu-id="de6a0-225">No</span></span> |

### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="de6a0-226">Esempio: hello metodo GET (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="de6a0-226">Example: using hello GET (default) method</span></span>

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

### <a name="example-using-hello-post-method"></a><span data-ttu-id="de6a0-227">Esempio: utilizzo di metodo POST hello</span><span class="sxs-lookup"><span data-stu-id="de6a0-227">Example: using hello POST method</span></span>

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

## <a name="copy-activity-properties"></a><span data-ttu-id="de6a0-228">Proprietà dell'attività di copia</span><span class="sxs-lookup"><span data-stu-id="de6a0-228">Copy activity properties</span></span>
<span data-ttu-id="de6a0-229">Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="de6a0-229">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="de6a0-230">Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.</span><span class="sxs-lookup"><span data-stu-id="de6a0-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="de6a0-231">Le proprietà disponibili nella hello **typeProperties** sezione di attività hello hello invece variano in base a ogni tipo di attività.</span><span class="sxs-lookup"><span data-stu-id="de6a0-231">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="de6a0-232">Per attività di copia, variano a seconda dei tipi di hello di origini e sink.</span><span class="sxs-lookup"><span data-stu-id="de6a0-232">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="de6a0-233">Attualmente, quando origine hello in attività di copia è di tipo **HttpSource**, hello le proprietà seguenti è supportato.</span><span class="sxs-lookup"><span data-stu-id="de6a0-233">Currently, when hello source in copy activity is of type **HttpSource**, hello following properties are supported.</span></span>

| <span data-ttu-id="de6a0-234">Proprietà</span><span class="sxs-lookup"><span data-stu-id="de6a0-234">Property</span></span> | <span data-ttu-id="de6a0-235">Descrizione</span><span class="sxs-lookup"><span data-stu-id="de6a0-235">Description</span></span> | <span data-ttu-id="de6a0-236">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="de6a0-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="de6a0-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="de6a0-237">httpRequestTimeout</span></span> | <span data-ttu-id="de6a0-238">Hello timeout (TimeSpan) per hello HTTP richiesta tooget una risposta.</span><span class="sxs-lookup"><span data-stu-id="de6a0-238">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="de6a0-239">È hello timeout tooget una risposta, dati di risposta non hello timeout tooread.</span><span class="sxs-lookup"><span data-stu-id="de6a0-239">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="de6a0-240">No.</span><span class="sxs-lookup"><span data-stu-id="de6a0-240">No.</span></span> <span data-ttu-id="de6a0-241">Valore predefinito: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="de6a0-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="de6a0-242">Formati di file e di compressione supportati</span><span class="sxs-lookup"><span data-stu-id="de6a0-242">Supported file and compression formats</span></span>
<span data-ttu-id="de6a0-243">Per i dettagli, vedere l'articolo relativo ai [file e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="de6a0-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="de6a0-244">Esempi JSON</span><span class="sxs-lookup"><span data-stu-id="de6a0-244">JSON examples</span></span>
<span data-ttu-id="de6a0-245">Hello di esempio seguente fornisce una definizione JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="de6a0-245">hello following example provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="de6a0-246">Visualizzano come origine dei dati di toocopy da HTTP tooAzure nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="de6a0-246">They show how toocopy data from HTTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="de6a0-247">Tuttavia, i dati possono essere copiati **direttamente** da una qualsiasi delle origini tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="de6a0-247">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a><span data-ttu-id="de6a0-248">Esempio: Copiare i dati da tooAzure origine HTTP nell'archiviazione Blob</span><span class="sxs-lookup"><span data-stu-id="de6a0-248">Example: Copy data from HTTP source tooAzure Blob Storage</span></span>
<span data-ttu-id="de6a0-249">soluzione di Data Factory per l'esempio Hello contiene hello entità Data Factory di seguito:</span><span class="sxs-lookup"><span data-stu-id="de6a0-249">hello Data Factory solution for this sample contains hello following Data Factory entities:</span></span>

1. <span data-ttu-id="de6a0-250">Un servizio collegato di tipo [HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="de6a0-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="de6a0-251">Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="de6a0-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="de6a0-252">Un [set di dati](data-factory-create-datasets.md) di input di tipo [HTTP](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="de6a0-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="de6a0-253">Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="de6a0-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="de6a0-254">Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [HttpSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="de6a0-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="de6a0-255">esempio Hello copia dati da un tooan origine HTTP blob di Azure ogni ora.</span><span class="sxs-lookup"><span data-stu-id="de6a0-255">hello sample copies data from an HTTP source tooan Azure blob every hour.</span></span> <span data-ttu-id="de6a0-256">proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="de6a0-256">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="de6a0-257">Servizio collegato HTTP</span><span class="sxs-lookup"><span data-stu-id="de6a0-257">HTTP linked service</span></span>
<span data-ttu-id="de6a0-258">In questo esempio utilizza hello HTTP collegato del servizio con l'autenticazione anonima.</span><span class="sxs-lookup"><span data-stu-id="de6a0-258">This example uses hello HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="de6a0-259">Per i diversi tipi di autenticazione disponibili, vedere la sezione relativa al [servizio collegato HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="de6a0-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="de6a0-260">Servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="de6a0-260">Azure Storage linked service</span></span>

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

### <a name="http-input-dataset"></a><span data-ttu-id="de6a0-261">Set di dati di input HTTP</span><span class="sxs-lookup"><span data-stu-id="de6a0-261">HTTP input dataset</span></span>
<span data-ttu-id="de6a0-262">Impostazione **esterno** troppo**true** informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="de6a0-262">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="de6a0-263">Set di dati di output del BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="de6a0-263">Azure Blob output dataset</span></span>

<span data-ttu-id="de6a0-264">I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).</span><span class="sxs-lookup"><span data-stu-id="de6a0-264">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="de6a0-265">Pipeline con attività di copia</span><span class="sxs-lookup"><span data-stu-id="de6a0-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="de6a0-266">pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora.</span><span class="sxs-lookup"><span data-stu-id="de6a0-266">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="de6a0-267">Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**HttpSource** e **sink** tipo è stato impostato troppo**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="de6a0-267">In hello pipeline JSON definition, hello **source** type is set too**HttpSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="de6a0-268">Vedere [HttpSource](#copy-activity-properties) per elenco hello delle proprietà supportate da hello HttpSource.</span><span class="sxs-lookup"><span data-stu-id="de6a0-268">See [HttpSource](#copy-activity-properties) for hello list of properties supported by hello HttpSource.</span></span>

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
        "description": "Copy from an HTTP source tooan Azure blob",
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
> <span data-ttu-id="de6a0-269">colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="de6a0-269">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="de6a0-270">Ottimizzazione delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="de6a0-270">Performance and Tuning</span></span>
<span data-ttu-id="de6a0-271">Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.</span><span class="sxs-lookup"><span data-stu-id="de6a0-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
