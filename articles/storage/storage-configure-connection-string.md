---
title: Configurare una stringa di connessione per Archiviazione di Azure | Microsoft Docs
description: Configurare una stringa di connessione per un account di archiviazione di Azure. Una stringa di connessione contiene le informazioni necessarie per autenticare l'accesso a un account di archiviazione dall'applicazione in fase di runtime.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: 01aa506e2b47fc29a70592e670a206a2b74248a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="79af8-104">Configurare le stringhe di connessione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="79af8-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="79af8-105">Una stringa di connessione include le informazioni necessarie all'applicazione per l'accesso ai dati di un account di Archiviazione di Azure in fase di runtime.</span><span class="sxs-lookup"><span data-stu-id="79af8-105">A connection string includes the authentication information required for your application to access data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="79af8-106">Le stringhe di connessione possono essere configurate per:</span><span class="sxs-lookup"><span data-stu-id="79af8-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="79af8-107">Connettersi all'emulatore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="79af8-107">Connect to the Azure storage emulator.</span></span>
* <span data-ttu-id="79af8-108">Accedere a un account di archiviazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="79af8-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="79af8-109">Accedere alle risorse specificate in Azure tramite una firma di accesso condiviso (SAS).</span><span class="sxs-lookup"><span data-stu-id="79af8-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="79af8-110">Recupero della stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="79af8-110">Storing your connection string</span></span>
<span data-ttu-id="79af8-111">L'applicazione deve accedere alla stringa di connessione in fase di runtime per autenticare le richieste inviate al servizio Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="79af8-111">Your application needs to access the connection string at runtime to authenticate requests made to Azure Storage.</span></span> <span data-ttu-id="79af8-112">Sono disponibili diverse opzioni per l'archiviazione della stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="79af8-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="79af8-113">Un'applicazione in esecuzione sul desktop o in un dispositivo può archiviare la stringa di connessione in un file **app.config** o in un file **web.config**.</span><span class="sxs-lookup"><span data-stu-id="79af8-113">An application running on the desktop or on a device can store the connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="79af8-114">Aggiungere la stringa di connessione alla sezione **AppSettings** in tali file.</span><span class="sxs-lookup"><span data-stu-id="79af8-114">Add the connection string to the **AppSettings** section in these files.</span></span>
* <span data-ttu-id="79af8-115">Un'applicazione in esecuzione in un servizio cloud di Azure può archiviare la stringa di connessione nel [file dello schema di configurazione dei servizi di Azure (.cscfg)](https://msdn.microsoft.com/library/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="79af8-115">An application running in an Azure cloud service can store the connection string in the [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="79af8-116">Aggiungere la stringa di connessione alla sezione **ConfigurationSettings** del file di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="79af8-116">Add the connection string to the **ConfigurationSettings** section of the service configuration file.</span></span>
* <span data-ttu-id="79af8-117">È possibile usare la stringa di connessione direttamente nel codice.</span><span class="sxs-lookup"><span data-stu-id="79af8-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="79af8-118">Per la maggior parte degli scenari è tuttavia consigliabile archiviare la stringa di connessione in un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="79af8-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="79af8-119">L'archiviazione della stringa di connessione in un file di configurazione renderà più semplice aggiornare la stringa per alternare tra l'emulatore di archiviazione e un account di archiviazione di Azure nel cloud.</span><span class="sxs-lookup"><span data-stu-id="79af8-119">Storing your connection string in a configuration file makes it easy to update the connection string to switch between the storage emulator and an Azure storage account in the cloud.</span></span> <span data-ttu-id="79af8-120">È sufficiente modificare la stringa di connessione in modo che faccia riferimento all'ambiente di destinazione.</span><span class="sxs-lookup"><span data-stu-id="79af8-120">You only need to edit the connection string to point to your target environment.</span></span>

<span data-ttu-id="79af8-121">È possibile usare [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) per accedere alla stringa di connessione in fase di runtime indipendentemente dall'ambiente in cui viene eseguita l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="79af8-121">You can use the [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) to access your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-the-storage-emulator"></a><span data-ttu-id="79af8-122">Creare una stringa di connessione per l'emulatore di archiviazione</span><span class="sxs-lookup"><span data-stu-id="79af8-122">Create a connection string for the storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="79af8-123">Per altre informazioni sull'emulatore di archiviazione, vedere [Usare l'emulatore di archiviazione di Azure per sviluppo e test](storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="79af8-123">For more information about the storage emulator, see [Use the Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="79af8-124">Creare una stringa di connessione per un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="79af8-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="79af8-125">Per creare una stringa di connessione per l'account di archiviazione di Azure, usare il seguente formato.</span><span class="sxs-lookup"><span data-stu-id="79af8-125">To create a connection string for your Azure storage account, use the following format.</span></span> <span data-ttu-id="79af8-126">Indicare se si vuole eseguire la connessione all'account di archiviazione tramite HTTPS (scelta consigliata) o HTTP, sostituire `myAccountName` con il nome dell'account di archiviazione e sostituire `myAccountKey` con la chiave di accesso dell'account:</span><span class="sxs-lookup"><span data-stu-id="79af8-126">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="79af8-127">Ad esempio, la stringa di connessione può essere simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="79af8-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="79af8-128">Anche se Archiviazione di Azure supporta sia HTTP che HTTPS in una stringa di connessione, *è consigliabile usare HTTPS*.</span><span class="sxs-lookup"><span data-stu-id="79af8-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="79af8-129">Le stringhe di connessione dell'account di archiviazione sono disponibili nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="79af8-129">You can find your storage account's connection strings in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="79af8-130">Accedere a **Impostazioni** > **Chiavi di accesso** nel pannello del menu dell'account di archiviazione per impostare stringhe di connessione per le chiavi di accesso primaria e secondaria.</span><span class="sxs-lookup"><span data-stu-id="79af8-130">Navigate to **SETTINGS** > **Access keys** in your storage account's menu blade to see connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="79af8-131">Creare una stringa di connessione usando una firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="79af8-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="79af8-132">Creare una stringa di connessione per un endpoint di archiviazione esplicito</span><span class="sxs-lookup"><span data-stu-id="79af8-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="79af8-133">Nella stringa di connessione è possibile specificare in modo esplicito endpoint di servizio anziché usare gli endpoint predefiniti.</span><span class="sxs-lookup"><span data-stu-id="79af8-133">You can specify explicit service endpoints in your connection string instead of using the default endpoints.</span></span> <span data-ttu-id="79af8-134">Per creare una stringa di connessione che specifica un endpoint esplicito, specificare l'endpoint di servizio completo per ogni servizio, inclusa la specifica del protocollo, ad esempio HTTPS (scelta consigliata) o HTTP, usando il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="79af8-134">To create a connection string that specifies an explicit endpoint, specify the complete service endpoint for each service, including the protocol specification (HTTPS (recommended) or HTTP), in the following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="79af8-135">Se l'endpoint di archiviazione BLOB è stato mappato su un [dominio personalizzato](storage-custom-domain-name.md) può risultare utile specificare un endpoint esplicito.</span><span class="sxs-lookup"><span data-stu-id="79af8-135">One scenario where you might wish to specify an explicit endpoint is when you've mapped your Blob storage endpoint to a [custom domain](storage-custom-domain-name.md).</span></span> <span data-ttu-id="79af8-136">In tal caso è possibile specificare l'endpoint personalizzato per l'archiviazione BLOB nella stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="79af8-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="79af8-137">Facoltativamente è possibile specificare gli endpoint predefiniti per gli altri servizi, se l'applicazione li usa.</span><span class="sxs-lookup"><span data-stu-id="79af8-137">You can optionally specify the default endpoints for the other services if your application uses them.</span></span>

<span data-ttu-id="79af8-138">Ecco un esempio di stringa di connessione che specifica un endpoint esplicito per il servizio BLOB:</span><span class="sxs-lookup"><span data-stu-id="79af8-138">Here is an example of a connection string that specifies an explicit endpoint for the Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="79af8-139">Questo esempio specifica endpoint espliciti per tutti i servizi, tra cui un dominio personalizzato per il servizio BLOB:</span><span class="sxs-lookup"><span data-stu-id="79af8-139">This example specifies explicit endpoints for all services, including a custom domain for the Blob service:</span></span>

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="79af8-140">I valori degli endpoint in una stringa di connessione vengono usati per costruire gli URI di richiesta per i servizi di archiviazione e per definire la struttura degli eventuali URI restituiti al codice.</span><span class="sxs-lookup"><span data-stu-id="79af8-140">The endpoint values in a connection string are used to construct the request URIs to the storage services, and dictate the form of any URIs that are returned to your code.</span></span>

<span data-ttu-id="79af8-141">Se un endpoint di archiviazione è stato mappato su un dominio personalizzato e tale endpoint viene omesso da una stringa di connessione, non sarà possibile usare la stringa di connessione per accedere ai dati in quel servizio dal codice.</span><span class="sxs-lookup"><span data-stu-id="79af8-141">If you've mapped a storage endpoint to a custom domain and omit that endpoint from a connection string, then you will not be able to use that connection string to access data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79af8-142">I valori degli endpoint di servizio nelle stringhe di connessione devono essere URI formulati correttamente e includere `https://` (opzione consigliata) o `http://`.</span><span class="sxs-lookup"><span data-stu-id="79af8-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="79af8-143">Dato che l'archiviazione di Azure non supporta ancora HTTPS per i domini personalizzati, *è necessario* specificare `http://` per gli URI di endpoint che fanno riferimento a domini personalizzati.</span><span class="sxs-lookup"><span data-stu-id="79af8-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points to a custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="79af8-144">Creare una stringa di connessione con un suffisso dell'endpoint</span><span class="sxs-lookup"><span data-stu-id="79af8-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="79af8-145">Per creare una stringa di connessione per un servizio di archiviazione in aree o istanze con suffissi dell'endpoint diversi, ad esempio per Azure Cina o Azure per enti pubblici, usare il seguente formato per la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="79af8-145">To create a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use the following connection string format.</span></span> <span data-ttu-id="79af8-146">Indicare se si vuole eseguire la connessione all'account di archiviazione tramite HTTPS (opzione consigliata) o HTTP, quindi sostituire `myAccountName` con il nome dell'account di archiviazione, sostituire `myAccountKey` con la chiave di accesso del proprio account e sostituire `mySuffix` con il suffisso URI:</span><span class="sxs-lookup"><span data-stu-id="79af8-146">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with the URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="79af8-147">Ecco una stringa di connessione di esempio per i servizi di archiviazione in Azure Cina:</span><span class="sxs-lookup"><span data-stu-id="79af8-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="79af8-148">Analisi di una stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="79af8-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="79af8-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="79af8-149">Next steps</span></span>
* [<span data-ttu-id="79af8-150">Usare l'emulatore di archiviazione di Azure per sviluppo e test</span><span class="sxs-lookup"><span data-stu-id="79af8-150">Use the Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="79af8-151">Strumenti di esplorazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="79af8-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="79af8-152">Uso delle firme di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="79af8-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

