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
# <a name="configure-azure-storage-connection-strings"></a>Configurare le stringhe di connessione di Archiviazione di Azure

Una stringa di connessione include informazioni di autenticazione hello necessarie per i dati delle applicazioni tooaccess in un account di archiviazione di Azure in fase di esecuzione. Le stringhe di connessione possono essere configurate per:

* Connettersi toohello emulatore di archiviazione Azure.
* Accedere a un account di archiviazione in Azure.
* Accedere alle risorse specificate in Azure tramite una firma di accesso condiviso (SAS).

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a>Recupero della stringa di connessione
L'applicazione richiede una stringa di connessione tooaccess hello in fase di esecuzione tooauthenticate le richieste effettuate tooAzure archiviazione. Sono disponibili diverse opzioni per l'archiviazione della stringa di connessione:

* Un'applicazione in esecuzione sul desktop hello o in un dispositivo può archiviare la stringa di connessione hello in un **app** o **Web. config** file. Aggiungere toohello stringa di connessione hello **AppSettings** sezione in questi file.
* Un'applicazione in esecuzione in un servizio cloud di Azure è possibile archiviare la stringa di connessione hello in hello [file di schema (con estensione cscfg) configurazione del servizio Azure](https://msdn.microsoft.com/library/ee758710.aspx). Aggiungere toohello stringa di connessione hello **ConfigurationSettings** sezione del file di configurazione del servizio hello.
* È possibile usare la stringa di connessione direttamente nel codice. Per la maggior parte degli scenari è tuttavia consigliabile archiviare la stringa di connessione in un file di configurazione.

Archiviare la stringa di connessione in un file di configurazione rende facile tooupdate hello connessione stringa tooswitch tra l'emulatore di archiviazione hello e un account di archiviazione di Azure nel cloud hello. È necessario solo l'ambiente di destinazione di tooedit hello connessione stringa toopoint tooyour.

È possibile utilizzare hello [Gestione configurazione di Microsoft Azure](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess stringa di connessione in fase di esecuzione indipendentemente dal fatto in cui l'applicazione è in esecuzione.

## <a name="create-a-connection-string-for-hello-storage-emulator"></a>Creare una stringa di connessione per l'emulatore di archiviazione hello
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

Per ulteriori informazioni sull'emulatore di archiviazione hello, vedere [Usa hello emulatore di archiviazione Azure per sviluppo e test](storage-use-emulator.md).

## <a name="create-a-connection-string-for-an-azure-storage-account"></a>Creare una stringa di connessione per un account di archiviazione di Azure
toocreate una stringa di connessione per l'account di archiviazione di Azure, formattare seguente hello utilizzare. Indicare se si desidera tooconnect toohello account di archiviazione tramite HTTPS (scelta consigliata) o HTTP, sostituire `myAccountName` con nome hello di account di archiviazione e sostituire `myAccountKey` con la chiave di accesso account:

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

Ad esempio, la stringa di connessione può essere simile alla seguente:

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

Anche se Archiviazione di Azure supporta sia HTTP che HTTPS in una stringa di connessione, *è consigliabile usare HTTPS*.

> [!TIP]
> È possibile trovare stringhe di connessione dell'account di archiviazione in hello [portale di Azure](https://portal.azure.com). Passare troppo**impostazioni** > **le chiavi di accesso** dell'account di archiviazione menu Pannello toosee le stringhe di connessione per entrambe le chiavi di accesso primarie e secondarie.
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a>Creare una stringa di connessione usando una firma di accesso condiviso
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a>Creare una stringa di connessione per un endpoint di archiviazione esplicito
È possibile specificare gli endpoint del servizio esplicita nella stringa di connessione anziché tramite endpoint predefiniti hello. toocreate una stringa di connessione che specifica un endpoint esplicito, specificare endpoint servizio hello per ogni servizio, inclusi specifica del protocollo hello (HTTPS (scelta consigliata) o HTTP), in hello seguente formato:

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

Uno scenario in cui potrebbe essere opportuno toospecify un endpoint esplicito è quando è stato eseguito il mapping del tooa di endpoint di archiviazione Blob [dominio personalizzato](storage-custom-domain-name.md). In tal caso è possibile specificare l'endpoint personalizzato per l'archiviazione BLOB nella stringa di connessione. È possibile specificare facoltativamente endpoint predefiniti hello per hello altri servizi se l'applicazione li utilizza.

Di seguito è riportato un esempio di una stringa di connessione che specifica un endpoint esplicito per hello servizio Blob:

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

In questo esempio specifica endpoint espliciti per tutti i servizi, incluso un dominio personalizzato per hello servizio Blob:

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

valori endpoint Hello in una stringa di connessione utilizzato tooconstruct hello richiedono servizi di archiviazione toohello URI e determinano il formato di hello di qualsiasi URI restituito tooyour codice.

Se è stato eseguito il mapping di un dominio personalizzato di archiviazione endpoint tooa e omettere tale endpoint da una stringa di connessione, quindi non sarà in grado di toouse tale connessione dati di tipo stringa tooaccess in quel servizio dal codice.

> [!IMPORTANT]
> I valori degli endpoint di servizio nelle stringhe di connessione devono essere URI formulati correttamente e includere `https://` (opzione consigliata) o `http://`. Poiché l'archiviazione di Azure non supporta ancora HTTPS per i domini personalizzati, si *deve* specificare `http://` per un endpoint qualsiasi URI che punta tooa di dominio personalizzato.
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a>Creare una stringa di connessione con un suffisso dell'endpoint
toocreate una stringa di connessione per un servizio di archiviazione in aree o le istanze con i suffissi endpoint diversi, ad esempio per la Cina di Azure o Azure per enti pubblici, utilizzare hello seguente formato di stringa di connessione. Indicare se si desidera tooconnect toohello account di archiviazione tramite HTTPS (scelta consigliata) o HTTP, sostituire `myAccountName` con nome hello dell'account di archiviazione, sostituire `myAccountKey` con la chiave di accesso account, quindi sostituire `mySuffix` con hello URI suffisso:

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

Ecco una stringa di connessione di esempio per i servizi di archiviazione in Azure Cina:

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a>Analisi di una stringa di connessione
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a>Passaggi successivi
* [Utilizzare l'emulatore di archiviazione Azure hello per lo sviluppo e test](storage-use-emulator.md)
* [Strumenti di esplorazione di Archiviazione di Azure](storage-explorers.md)
* [Uso delle firme di accesso condiviso](storage-dotnet-shared-access-signature-part-1.md)

