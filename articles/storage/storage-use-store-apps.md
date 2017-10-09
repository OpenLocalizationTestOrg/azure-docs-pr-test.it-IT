---
title: archiviazione di Azure in applicazioni Windows Store aaaUse | Documenti Microsoft
description: Informazioni su come toocreate un di Windows Store app che utilizza l'archiviazione Blob di Azure, coda, tabella o File.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 63c4b29d-b2f2-4d7c-b164-a0d38f4d14f6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: ac21b0695c0d77c1d81c1b921718fb929945d45e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a>Come toouse di archiviazione di Azure in applicazioni Windows Store
## <a name="overview"></a>Panoramica
Questa guida viene illustrata la modalità di avvio tooget con lo sviluppo di un'applicazione Windows Store che utilizza spazio di archiviazione di Azure.

## <a name="download-required-tools"></a>Download degli strumenti richiesti
* [Visual Studio](https://www.visualstudio.com/downloads/) rende facile toobuild, eseguire il debug, localizzare, creare un pacchetto e distribuire applicazioni Windows Store. È richiesto Visual Studio 2012 o versione successiva.
* Hello [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) fornisce una libreria di classi Windows Runtime per l'utilizzo di archiviazione di Azure.
* [WCF Data Services strumenti per App di Windows Store](http://www.microsoft.com/download/details.aspx?id=30714) estende l'esperienza di Aggiungi riferimento al servizio hello con supporto per OData sul lato client per applicazioni Windows Store in Visual Studio.

## <a name="develop-apps"></a>Sviluppo di applicazioni
### <a name="getting-ready"></a>Preparazione
Creare un nuovo progetto di app di Windows Store in Visual Studio 2012 o versione successiva:

![store-apps-storage-vs-project][store-apps-storage-vs-project]

Successivamente, aggiungere un toohello riferimento Azure Storage Client Library facendo **riferimenti**, facendo clic su **Aggiungi riferimento**e quindi esplorare toohello Storage Client Library per Windows Runtime che si download:

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a>Tramite i servizi di coda e di libreria hello con hello Blob
A questo punto, l'app è servizi di accodamento e Blob di Azure di hello toocall pronto. Aggiungere il seguente hello **utilizzando** istruzioni in modo da fare riferimento direttamente a tipi di archiviazione di Azure:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

Successivamente, aggiungere una pagina di tooyour pulsante. Aggiungere hello seguente codice tooits **fare clic su** eventi e modificare il metodo del gestore eventi tramite hello [parola chiave async](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

Questo codice presuppone che si abbiano due variabili di stringa, *accountName* e *accountKey*. Rappresentano nome hello dell'account e hello chiave account di archiviazione associato a tale account.

Compilare ed eseguire un'applicazione hello. Facendo clic su pulsante hello controllerà se un contenitore denominato *container1* esista nell'account e quindi crearlo se non.

### <a name="using-hello-library-with-hello-table-service"></a>Utilizzo della libreria hello con hello del servizio tabelle
Tipi che sono utilizzati toocommunicate con il servizio tabelle di Azure hello dipendono da WCF Data Services per la libreria di app Windows Store hello. Successivamente, aggiungere che un riferimento toohello necessarie librerie WCF utilizzando hello Console di gestione pacchetti:

![store-apps-storage-package-manager][store-apps-storage-package-manager]

Comando che segue di hello utilizzare toopoint percorso toohello Package Manager nel computer:

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

Questo comando aggiungerà automaticamente tutti i riferimenti richiesti tooyour progetto. Se non si desidera toouse hello Console di gestione pacchetti, è possibile aggiungere la cartella di hello NuGet WCF Data Services nell'elenco delle origini pacchetto toohello computer locale e quindi aggiungere il riferimento di hello tramite hello dell'interfaccia utente, come descritto in [gestione utilizzando pacchetti NuGet finestra di dialogo Hello](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).

Quando si è fatto riferimento pacchetto NuGet WCF Data Services hello, modificare codice hello del pulsante **fare clic su** evento:

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

Questo codice verifica se esiste una tabella denominata *table1* nell'account, creandone una se non esiste.

È inoltre possibile aggiungere un tooMicrosoft.WindowsAzure.Storage.Table.dll di riferimento, che è disponibile in hello stesso pacchetto scaricato in precedenza. Questa libreria contiene funzionalità aggiuntive, come la serializzazione basata su reflection e le query generiche. Si noti che questa libreria non supporta JavaScript.

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
