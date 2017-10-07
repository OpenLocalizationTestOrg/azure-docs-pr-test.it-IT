---
title: scadenza aaaManage di BLOB di archiviazione di Azure nella rete CDN di Azure | Documenti Microsoft
description: Informazioni sulle opzioni di hello per il controllo time-to-live per BLOB nella rete CDN di Azure la memorizzazione nella cache.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ad4801e9-d09a-49bf-b35c-efdc4e6034e8
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9fecae9639deb28977da7f851e1da4a823ddc4e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a>Gestire la scadenza di BLOB del servizio di archiviazione di Azure nella rete CDN di Azure
> [!div class="op_single_selector"]
> * [App Web/Servizi cloud di Azure, ASP.NET o IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Servizio BLOB del servizio di archiviazione di Azure](cdn-manage-expiration-of-blob-content.md)
> 
> 

Hello [servizio blob](../storage/common/storage-introduction.md#blob-storage) in [di archiviazione di Azure](../storage/common/storage-introduction.md) una delle diverse origini basato su Azure è integrata con la rete CDN Azure.  Qualsiasi contenuto BLOB accessibile pubblicamente può essere memorizzato nella cache della rete CDN di Azure fino allo scadere della relativa durata (TTL).  Hello durata (TTL) è determinato dal hello [ *Cache-Control* intestazione](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) nella risposta HTTP hello dall'archiviazione di Azure.

> [!TIP]
> È non possibile scegliere tooset alcuna durata (TTL) su un blob.  In tal caso, la rete CDN di Azure applica automaticamente una durata (TTL) predefinita di sette giorni.
> 
> Per ulteriori informazioni sul funzionamento di toospeed tooblobs di accesso e altri file di rete CDN di Azure, vedere hello [Panoramica della rete CDN di Azure](cdn-overview.md).
> 
> Per ulteriori informazioni su hello servizio blob di archiviazione di Azure, vedere [concetti relativi al servizio Blob](https://msdn.microsoft.com/library/dd179376.aspx). 
> 
> 

Questa esercitazione illustra diversi modi, che è possibile impostare hello durata (TTL) su un blob in archiviazione di Azure.  

## <a name="azure-powershell"></a>Azure PowerShell
[Azure PowerShell](/powershell/azure/overview) è uno dei hello modi più rapido ed efficiente tooadminister i servizi di Azure.  Hello utilizzare `Get-AzureStorageBlob` tooget cmdlet un blob toohello di riferimento, quindi impostare hello `.ICloudBlob.Properties.CacheControl` proprietà. 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference toohello blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send hello update toohello cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> È inoltre possibile utilizzare PowerShell troppo[gestire i profili di rete CDN e l'endpoint](cdn-manage-powershell.md).
> 
> 

## <a name="azure-storage-client-library-for-net"></a>Libreria client di archiviazione di Azure per .NET
tooset un blob di durata (TTL) utilizzando .NET, usare hello [Azure Storage Client Library per .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) proprietà.

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with hello blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference toohello container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference toohello blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update hello blob's properties in hello cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> Sono disponibili molti altri esempi di codice .NET in hello [esempi di archiviazione Blob di Azure per .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).
> 
> 

## <a name="other-methods"></a>Altri metodi
* [Interfaccia della riga di comando di Azure](../cli-install-nodejs.md)
  
    Quando si carica blob hello, impostare hello *cacheControl* proprietà utilizzando hello `-p` passare.  In questo esempio hello TTL tooone ora (3600 secondi).
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [API REST dei servizi di archiviazione di Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    In modo esplicito il set di hello *x-ms-blob-cache-control* proprietà in un [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [inserire elenco Blocca](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), o [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) richiesta.
* Strumenti di gestione dell'archiviazione di terze parti
  
    Alcuni strumenti di gestione archiviazione di Azure di terze parti consentono di hello tooset *CacheControl* proprietà BLOB. 

## <a name="testing-hello-cache-control-header"></a>Test hello *Cache-Control* intestazione
È possibile verificare facilmente hello durata (TTL) del BLOB.  Tramite il browser [gli strumenti di sviluppo](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), verificare che il blob è incluso hello *Cache-Control* intestazione della risposta.  È inoltre possibile utilizzare uno strumento come **wget**, [Postman](https://www.getpostman.com/), o [Fiddler](http://www.telerik.com/fiddler) intestazioni di risposta tooexamine hello.

## <a name="next-steps"></a>Passaggi successivi
* [Conoscenza hello *Cache-Control* intestazione](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [Informazioni su come toomanage scadenza del contenuto del servizio Cloud nella rete CDN di Azure](cdn-manage-expiration-of-cloud-service-content.md)

