---
title: aaaConfigure una stringa di connessione per l'archiviazione di Azure | Documenti Microsoft
description: Configurare una stringa di connessione per un account di archiviazione di Azure. Una stringa di connessione contiene informazioni hello necessari tooauthenticate accedere l'account di archiviazione tooa dall'applicazione in fase di esecuzione.
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
ms.openlocfilehash: 80c38a6f8f0d4f06b99e7c487647b984e01d1772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="fe300-104">Configurare le stringhe di connessione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="fe300-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="fe300-105">Una stringa di connessione include informazioni di autenticazione hello necessarie per i dati delle applicazioni tooaccess in un account di archiviazione di Azure in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fe300-105">A connection string includes hello authentication information required for your application tooaccess data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="fe300-106">Le stringhe di connessione possono essere configurate per:</span><span class="sxs-lookup"><span data-stu-id="fe300-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="fe300-107">Connettersi toohello emulatore di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="fe300-107">Connect toohello Azure storage emulator.</span></span>
* <span data-ttu-id="fe300-108">Accedere a un account di archiviazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="fe300-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="fe300-109">Accedere alle risorse specificate in Azure tramite una firma di accesso condiviso (SAS).</span><span class="sxs-lookup"><span data-stu-id="fe300-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="fe300-110">Recupero della stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="fe300-110">Storing your connection string</span></span>
<span data-ttu-id="fe300-111">L'applicazione richiede una stringa di connessione tooaccess hello in fase di esecuzione tooauthenticate le richieste effettuate tooAzure archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fe300-111">Your application needs tooaccess hello connection string at runtime tooauthenticate requests made tooAzure Storage.</span></span> <span data-ttu-id="fe300-112">Sono disponibili diverse opzioni per l'archiviazione della stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="fe300-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="fe300-113">Un'applicazione in esecuzione sul desktop hello o in un dispositivo può archiviare la stringa di connessione hello in un **app** o **Web. config** file.</span><span class="sxs-lookup"><span data-stu-id="fe300-113">An application running on hello desktop or on a device can store hello connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="fe300-114">Aggiungere toohello stringa di connessione hello **AppSettings** sezione in questi file.</span><span class="sxs-lookup"><span data-stu-id="fe300-114">Add hello connection string toohello **AppSettings** section in these files.</span></span>
* <span data-ttu-id="fe300-115">Un'applicazione in esecuzione in un servizio cloud di Azure è possibile archiviare la stringa di connessione hello in hello [file di schema (con estensione cscfg) configurazione del servizio Azure](https://msdn.microsoft.com/library/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe300-115">An application running in an Azure cloud service can store hello connection string in hello [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="fe300-116">Aggiungere toohello stringa di connessione hello **ConfigurationSettings** sezione del file di configurazione del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="fe300-116">Add hello connection string toohello **ConfigurationSettings** section of hello service configuration file.</span></span>
* <span data-ttu-id="fe300-117">È possibile usare la stringa di connessione direttamente nel codice.</span><span class="sxs-lookup"><span data-stu-id="fe300-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="fe300-118">Per la maggior parte degli scenari è tuttavia consigliabile archiviare la stringa di connessione in un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="fe300-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="fe300-119">Archiviare la stringa di connessione in un file di configurazione rende facile tooupdate hello connessione stringa tooswitch tra l'emulatore di archiviazione hello e un account di archiviazione di Azure nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="fe300-119">Storing your connection string in a configuration file makes it easy tooupdate hello connection string tooswitch between hello storage emulator and an Azure storage account in hello cloud.</span></span> <span data-ttu-id="fe300-120">È necessario solo l'ambiente di destinazione di tooedit hello connessione stringa toopoint tooyour.</span><span class="sxs-lookup"><span data-stu-id="fe300-120">You only need tooedit hello connection string toopoint tooyour target environment.</span></span>

<span data-ttu-id="fe300-121">È possibile utilizzare hello [Gestione configurazione di Microsoft Azure](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess stringa di connessione in fase di esecuzione indipendentemente dal fatto in cui l'applicazione è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fe300-121">You can use hello [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-hello-storage-emulator"></a><span data-ttu-id="fe300-122">Creare una stringa di connessione per l'emulatore di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="fe300-122">Create a connection string for hello storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="fe300-123">Per ulteriori informazioni sull'emulatore di archiviazione hello, vedere [Usa hello emulatore di archiviazione Azure per sviluppo e test](storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="fe300-123">For more information about hello storage emulator, see [Use hello Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="fe300-124">Creare una stringa di connessione per un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="fe300-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="fe300-125">toocreate una stringa di connessione per l'account di archiviazione di Azure, formattare seguente hello utilizzare.</span><span class="sxs-lookup"><span data-stu-id="fe300-125">toocreate a connection string for your Azure storage account, use hello following format.</span></span> <span data-ttu-id="fe300-126">Indicare se si desidera tooconnect toohello account di archiviazione tramite HTTPS (scelta consigliata) o HTTP, sostituire `myAccountName` con nome hello di account di archiviazione e sostituire `myAccountKey` con la chiave di accesso account:</span><span class="sxs-lookup"><span data-stu-id="fe300-126">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="fe300-127">Ad esempio, la stringa di connessione può essere simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="fe300-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="fe300-128">Anche se Archiviazione di Azure supporta sia HTTP che HTTPS in una stringa di connessione, *è consigliabile usare HTTPS*.</span><span class="sxs-lookup"><span data-stu-id="fe300-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="fe300-129">È possibile trovare stringhe di connessione dell'account di archiviazione in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fe300-129">You can find your storage account's connection strings in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fe300-130">Passare troppo**impostazioni** > **le chiavi di accesso** dell'account di archiviazione menu Pannello toosee le stringhe di connessione per entrambe le chiavi di accesso primarie e secondarie.</span><span class="sxs-lookup"><span data-stu-id="fe300-130">Navigate too**SETTINGS** > **Access keys** in your storage account's menu blade toosee connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="fe300-131">Creare una stringa di connessione usando una firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="fe300-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="fe300-132">Creare una stringa di connessione per un endpoint di archiviazione esplicito</span><span class="sxs-lookup"><span data-stu-id="fe300-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="fe300-133">È possibile specificare gli endpoint del servizio esplicita nella stringa di connessione anziché tramite endpoint predefiniti hello.</span><span class="sxs-lookup"><span data-stu-id="fe300-133">You can specify explicit service endpoints in your connection string instead of using hello default endpoints.</span></span> <span data-ttu-id="fe300-134">toocreate una stringa di connessione che specifica un endpoint esplicito, specificare endpoint servizio hello per ogni servizio, inclusi specifica del protocollo hello (HTTPS (scelta consigliata) o HTTP), in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="fe300-134">toocreate a connection string that specifies an explicit endpoint, specify hello complete service endpoint for each service, including hello protocol specification (HTTPS (recommended) or HTTP), in hello following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="fe300-135">Uno scenario in cui potrebbe essere opportuno toospecify un endpoint esplicito è quando è stato eseguito il mapping del tooa di endpoint di archiviazione Blob [dominio personalizzato](storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="fe300-135">One scenario where you might wish toospecify an explicit endpoint is when you've mapped your Blob storage endpoint tooa [custom domain](storage-custom-domain-name.md).</span></span> <span data-ttu-id="fe300-136">In tal caso è possibile specificare l'endpoint personalizzato per l'archiviazione BLOB nella stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="fe300-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="fe300-137">È possibile specificare facoltativamente endpoint predefiniti hello per hello altri servizi se l'applicazione li utilizza.</span><span class="sxs-lookup"><span data-stu-id="fe300-137">You can optionally specify hello default endpoints for hello other services if your application uses them.</span></span>

<span data-ttu-id="fe300-138">Di seguito è riportato un esempio di una stringa di connessione che specifica un endpoint esplicito per hello servizio Blob:</span><span class="sxs-lookup"><span data-stu-id="fe300-138">Here is an example of a connection string that specifies an explicit endpoint for hello Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="fe300-139">In questo esempio specifica endpoint espliciti per tutti i servizi, incluso un dominio personalizzato per hello servizio Blob:</span><span class="sxs-lookup"><span data-stu-id="fe300-139">This example specifies explicit endpoints for all services, including a custom domain for hello Blob service:</span></span>

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

<span data-ttu-id="fe300-140">valori endpoint Hello in una stringa di connessione utilizzato tooconstruct hello richiedono servizi di archiviazione toohello URI e determinano il formato di hello di qualsiasi URI restituito tooyour codice.</span><span class="sxs-lookup"><span data-stu-id="fe300-140">hello endpoint values in a connection string are used tooconstruct hello request URIs toohello storage services, and dictate hello form of any URIs that are returned tooyour code.</span></span>

<span data-ttu-id="fe300-141">Se è stato eseguito il mapping di un dominio personalizzato di archiviazione endpoint tooa e omettere tale endpoint da una stringa di connessione, quindi non sarà in grado di toouse tale connessione dati di tipo stringa tooaccess in quel servizio dal codice.</span><span class="sxs-lookup"><span data-stu-id="fe300-141">If you've mapped a storage endpoint tooa custom domain and omit that endpoint from a connection string, then you will not be able toouse that connection string tooaccess data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe300-142">I valori degli endpoint di servizio nelle stringhe di connessione devono essere URI formulati correttamente e includere `https://` (opzione consigliata) o `http://`.</span><span class="sxs-lookup"><span data-stu-id="fe300-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="fe300-143">Poiché l'archiviazione di Azure non supporta ancora HTTPS per i domini personalizzati, si *deve* specificare `http://` per un endpoint qualsiasi URI che punta tooa di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="fe300-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points tooa custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="fe300-144">Creare una stringa di connessione con un suffisso dell'endpoint</span><span class="sxs-lookup"><span data-stu-id="fe300-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="fe300-145">toocreate una stringa di connessione per un servizio di archiviazione in aree o le istanze con i suffissi endpoint diversi, ad esempio per la Cina di Azure o Azure per enti pubblici, utilizzare hello seguente formato di stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="fe300-145">toocreate a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use hello following connection string format.</span></span> <span data-ttu-id="fe300-146">Indicare se si desidera tooconnect toohello account di archiviazione tramite HTTPS (scelta consigliata) o HTTP, sostituire `myAccountName` con nome hello dell'account di archiviazione, sostituire `myAccountKey` con la chiave di accesso account, quindi sostituire `mySuffix` con hello URI suffisso:</span><span class="sxs-lookup"><span data-stu-id="fe300-146">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with hello URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="fe300-147">Ecco una stringa di connessione di esempio per i servizi di archiviazione in Azure Cina:</span><span class="sxs-lookup"><span data-stu-id="fe300-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="fe300-148">Analisi di una stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="fe300-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="fe300-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fe300-149">Next steps</span></span>
* [<span data-ttu-id="fe300-150">Utilizzare l'emulatore di archiviazione Azure hello per lo sviluppo e test</span><span class="sxs-lookup"><span data-stu-id="fe300-150">Use hello Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="fe300-151">Strumenti di esplorazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="fe300-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="fe300-152">Uso delle firme di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="fe300-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

