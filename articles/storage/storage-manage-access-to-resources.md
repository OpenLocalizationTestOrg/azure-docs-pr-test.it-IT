---
title: accesso in lettura pubblico aaaEnable per contenitori e BLOB nell'archiviazione Blob di Azure | Documenti Microsoft
description: Informazioni su come toomake contenitori e BLOB disponibili per l'accesso anonimo e come tooaccess li a livello di codice.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: 0675b5dc4d32a3a0a34376ae4c049542b07ba03a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a>Gestire BLOB e accesso in lettura anonimo toocontainers
È possibile abilitare l'accesso in lettura anonimo, pubblica tooa contenitore e i relativi BLOB nell'archiviazione Blob di Azure. In questo modo, è possibile concedere l'accesso di sola lettura alle risorse di toothese senza condividere la chiave dell'account e senza una firma di accesso condiviso (SAS).

Accesso in lettura pubblico è ideale per scenari in cui si desidera determinati tooalways BLOB sia disponibile per l'accesso in lettura anonimo. Per un controllo più accurato, è possibile creare una firma di accesso condiviso. Firme di accesso condiviso consentono di tooprovide limitato l'accesso con autorizzazioni diverse, per un periodo di tempo specifico. Per altre informazioni sulla creazione di firme di accesso condiviso, vedere [Uso delle firme di accesso condiviso](storage-dotnet-shared-access-signature-part-1.md).

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a>Concedere agli utenti anonimi le autorizzazioni toocontainers e BLOB
Per impostazione predefinita, un contenitore e tutti i BLOB in esso contenuti sono accessibili solo dal proprietario hello hello dell'account di archiviazione. toogive utenti anonimi le autorizzazioni di lettura tooa contenitore e nei relativi BLOB, è possibile impostare autorizzazioni contenitore di hello tooallow accesso pubblico. Gli utenti anonimi possono leggere i BLOB in un contenitore accessibile pubblicamente senza effettuare l'autenticazione richiesta hello.

È possibile configurare un contenitore con queste autorizzazioni hello:

* **Accesso in lettura non pubblico:** contenitore hello e nei relativi BLOB sono accessibili solo dal proprietario dell'account di archiviazione hello. Si tratta hello predefinita per tutti i contenitori di nuovo.
* **Solo per i BLOB l'accesso in lettura pubblico:** BLOB nel contenitore hello può essere letto da una richiesta anonima, ma i dati del contenitore non sono disponibili. I client anonimi non è possibile enumerare i BLOB di hello all'interno del contenitore di hello.
* **Accesso in lettura pubblico completo:** i dati del BLOB e del contenitore possono essere letti tramite richiesta anonima. I client possono enumerare i BLOB all'interno del contenitore hello da una richiesta anonima, ma non è possibile enumerare i contenitori nell'account di archiviazione hello.

È possibile utilizzare queste autorizzazioni contenitore tooset hello:

* [Portale di Azure](https://portal.azure.com)
* [Azure PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [Interfaccia della riga di comando di Azure 2.0](storage-azure-cli.md#create-and-manage-blobs)
* A livello di programmazione, utilizzando una delle librerie client di archiviazione hello o hello API REST

### <a name="set-container-permissions-in-hello-azure-portal"></a>Impostare le autorizzazioni del contenitore in hello portale di Azure
autorizzazioni del contenitore tooset in hello [portale di Azure](https://portal.azure.com), seguire questi passaggi:

1. Aprire il **account di archiviazione** pannello nel portale di hello. È possibile trovare l'account di archiviazione selezionando **gli account di archiviazione** nel Pannello di hello menu principale del portale.
1. In **servizio BLOB** nel Pannello di hello menu, selezionare **contenitori**.
1. Fare clic su una riga di hello contenitore o del contenitore di hello selezionare i puntini di sospensione tooopen hello **menu di scelta rapida**.
1. Selezionare **criterio di accesso** nel menu di scelta rapida hello.
1. Selezionare un **tipo di accesso** da hello menu a discesa.

    ![Finestra di dialogo Modifica metadati contenitore](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a>Impostare le autorizzazioni per il contenitore con .NET
tooset le autorizzazioni per un contenitore usando c# e hello libreria Client di archiviazione per .NET, recuperare innanzitutto le autorizzazioni esistenti del contenitore hello dal chiamante hello **GetPermissions** metodo. Quindi set hello **PublicAccess** proprietà hello **BlobContainerPermissions** oggetto restituito da hello **GetPermissions** metodo. Chiamare infine hello **SetPermissions** metodo con hello aggiornate le autorizzazioni.

Hello di esempio seguente imposta le autorizzazioni del contenitore hello toofull accesso in lettura pubblico. tooset toopublic di autorizzazioni di accesso in lettura per BLOB, impostare hello **PublicAccess** proprietà troppo**BlobContainerPublicAccessType.Blob**. impostare tutte le autorizzazioni per gli utenti anonimi, tooremove hello proprietà troppo**BlobContainerPublicAccessType.Off**.

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a>Accesso anonimo a contenitori e BLOB
Un client che accede a contenitori e BLOB in modo anonimo può usare costruttori che non richiedono credenziali. Hello seguono esempi mostra alcuni modi tooreference risorse del servizio Blob in modo anonimo.

### <a name="create-an-anonymous-client-object"></a>Creare un oggetto client anonimo
È possibile creare un nuovo oggetto client di servizio per l'accesso anonimo, fornendo l'endpoint del servizio Blob hello per conto di hello. Tuttavia, è inoltre necessario conoscere il nome di hello di un contenitore in tale account che è disponibile per l'accesso anonimo.

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a>Fare riferimento a un contenitore in modo anonimo
Se si dispone di hello URL tooa contenitore che è disponibile in modo anonimo, è possibile utilizzare il contenitore di hello tooreference direttamente.

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a>Fare riferimento a un BLOB in modo anonimo
Se si dispone di hello URL tooa blob disponibili per l'accesso anonimo, è possibile fare riferimento blob hello direttamente tramite URL:

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a>Utenti tooanonymous disponibili funzionalità
Hello nella tabella seguente mostra le operazioni che possono essere chiamate dagli utenti anonimi quando ACL di un contenitore è impostato l'accesso pubblico tooallow.

| Operazione REST | Autorizzazione con accesso in lettura pubblico completo | Autorizzazione con accesso in lettura pubblico solo per BLOB |
| --- | --- | --- |
| List Containers |Solo proprietario |Solo proprietario |
| Create Container |Solo proprietario |Solo proprietario |
| Get Container Properties |Tutti |Solo proprietario |
| Get Container Metadata |Tutti |Solo proprietario |
| Set Container Metadata |Solo proprietario |Solo proprietario |
| Get Container ACL |Solo proprietario |Solo proprietario |
| Set Container ACL |Solo proprietario |Solo proprietario |
| Delete Container |Solo proprietario |Solo proprietario |
| List Blobs |Tutti |Solo proprietario |
| Put Blob |Solo proprietario |Solo proprietario |
| Get Blob |Tutti |Tutti |
| Get Blob Properties |Tutti |Tutti |
| Set Blob Properties |Solo proprietario |Solo proprietario |
| Get Blob Metadata |Tutti |Tutti |
| Set Blob Metadata |Solo proprietario |Solo proprietario |
| Put Block |Solo proprietario |Solo proprietario |
| Get Block List (solo blocchi con commit) |Tutti |Tutti |
| Get Block List (solo blocchi senza commit o tutti i blocchi) |Solo proprietario |Solo proprietario |
| Put Block List |Solo proprietario |Solo proprietario |
| Delete Blob |Solo proprietario |Solo proprietario |
| Copy Blob |Solo proprietario |Solo proprietario |
| Snapshot Blob |Solo proprietario |Solo proprietario |
| Lease Blob |Solo proprietario |Solo proprietario |
| Put Page |Solo proprietario |Solo proprietario |
| Get Page Ranges |Tutti |Tutti |
| Append Blob |Solo proprietario |Solo proprietario |

## <a name="next-steps"></a>Passaggi successivi

* [Autenticazione per hello servizi di archiviazione di Azure](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [Uso delle firme di accesso condiviso](storage-dotnet-shared-access-signature-part-1.md)
* [Delega dell'accesso con una firma di accesso condiviso](https://msdn.microsoft.com/library/azure/ee395415.aspx)
