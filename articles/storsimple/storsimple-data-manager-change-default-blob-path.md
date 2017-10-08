---
title: percorso blob aaaChange da predefinito hello | Documenti Microsoft
description: Informazioni su come tooset backup di Azure funzione toorename un percorso di file di blob (anteprima privata)
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 2c414603514223c701ab1a3bd0b81ee18f1af666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a>Modificare il percorso di un blob dal percorso predefinito di hello (anteprima privata)

Questo articolo descrive come tooset backup di Azure funzione toorename un percorso di file blob predefinito. 

## <a name="prerequisites"></a>Prerequisiti

È necessario disporre di una definizione del processo configurata correttamente in una risorsa dati ibrida all'interno di un gruppo di risorse.

## <a name="create-an-azure-function"></a>Creare una funzione di Azure

una funzione di Azure, toocreate hello seguenti:

1. Passare toohello [portale di Azure](http://portal.azure.com/).

2. Nella parte superiore di hello del riquadro di sinistra hello, fare clic su **New**. 

3. In hello **ricerca** digitare **funzione App**, quindi premere INVIO.

    ![Digitare "Funzione App" nella casella di ricerca hello](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. In hello **risultati** elenco, fare clic su **funzione App**.

    ![Risorse di app di funzione hello selezionare nell'elenco risultati hello](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    Hello **funzione App** verrà visualizzata la finestra.

5. Fare clic su **Crea**.

    ![pulsante "Crea" finestra di Hello App (funzione)](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. In hello **funzione App** pannello configurazione hello seguenti:

    a. In hello **nome App** casella, il nome del tipo hello app.
    
    b. In hello **sottoscrizione** casella, il nome hello del tipo di sottoscrizione hello.

    c. In **gruppo di risorse**, fare clic su **Crea nuovo**e quindi hello nome del tipo hello del gruppo di risorse.

    d. In hello **piano di Hosting** digitare **consumo pianificare**.

    e. In hello **percorso** casella Tipo hello percorso.

    f. In **Account di archiviazione** selezionare un account di archiviazione esistente o crearne uno nuovo. Un account di archiviazione viene utilizzato internamente per la funzione hello.

    ![Immettere i dati per la configurazione della nuova app per le funzioni](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. Fare clic su **Crea**.  
    app di funzione Hello viene creato.

8. Nel riquadro di sinistra hello, fare clic su **più servizi**e quindi hello seguenti:
    
    a. In hello **filtro** digitare **servizi App**.
    
    b. Fare clic su **Servizi app**. 

    ![Collegamento "Ulteriori servizi" nel riquadro di sinistra hello](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. Nell'elenco di hello dei servizi di app, fare clic su nome hello di hello funzione app.  
    verrà visualizzata la pagina dell'app funzione Hello.

10. Nel riquadro di sinistra hello, fare clic su **nuova funzione**e quindi hello seguenti: 

    a. In hello **Language** elenco, selezionare **c#**.
    
    b. Nella matrice di hello dei riquadri di modello, selezionare **QueueTrigger CSharp**.

    c. In hello **nome alla funzione di** , digitare un nome per la funzione.

    d. In hello **nome coda** , digitare il nome di definizione del processo di trasformazione dei dati.

    e. In **connessione ad account di archiviazione**, fare clic su **nuova**e quindi selezionare account hello corrispondente toohello processo di trasformazione dei dati.  
        Prendere nota del nome di connessione hello. nome Hello è necessario in un secondo momento hello Azure (funzione).

       ![Creare una nuova funzione C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    f. Fare clic su **Crea**.  
    Hello **funzione** verrà visualizzata la finestra.

11. In hello **funzione** finestra, eseguire _csx_ file e quindi hello seguenti:

    a. Incollare hello seguente codice:

    ```
    using System;
    using System.Configuration;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Queue;
    using Microsoft.WindowsAzure.Storage;
    using System.Collections.Generic;
    using System.Linq;

    public static void Run(QueueItem myQueueItem, TraceWriter log)
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["STORAGE_CONNECTIONNAME"]);

        string storageAccUriEndswith = "windows.net/";
        string uri = myQueueItem.TargetLocation.Replace("%20", " ");
        log.Info($"Blob Uri: {uri}");

        // Remove storage account uri string
        uri = uri.Substring(uri.IndexOf(storageAccUriEndswith) + storageAccUriEndswith.Length);

        string containerName = uri.Substring(0, uri.IndexOf("/")); 

        // Remove container name string
        uri = uri.Substring(containerName.Length + 1);

        // Current blob path
        string blobName = uri; 

        string volumeName = uri.Substring(containerName.Length + 1);
        volumeName = uri.Substring(0, uri.IndexOf("/"));

        // Remove volume name string
        uri = uri.Substring(volumeName.Length + 1);

        string newContainerName = uri.Substring(0, uri.IndexOf("/")).ToLower();
        string newBlobName = uri.Substring(newContainerName.Length + 1);

        log.Info($"Container name: {containerName}");
        log.Info($"Volume name: {volumeName}");
        log.Info($"New container name: {newContainerName}");

        log.Info($"Blob name: {blobName}");
        log.Info($"New blob name: {newBlobName}");

        // Create hello blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Container reference
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlobContainer newContainer = blobClient.GetContainerReference(newContainerName);
        newContainer.CreateIfNotExists();

        if(!container.Exists())
        {
            log.Info($"Container - {containerName} not exists");
            return;
        }

        if(!newContainer.Exists())
        {
            log.Info($"Container - {newContainerName} not exists");
            return;
        }

        CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
        if (!blob.Exists())
        {
            // Skip toocopy hello blob toonew container, if source blob doesn't exist
            log.Info($"hello specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy toonew container
            blob.DeleteIfExists();
            log.Info($"Blob file path renamed completed successfully");
        }
        else
        {
            log.Info($"Blob file path renamed already done");
            // Delete old blob, if already exists.
            blob.DeleteIfExists();
        }
    }

    public class QueueItem
    {
        public string SourceLocation {get;set;}
        public long SizeInBytes {get;set;}
        public string Status {get;set;}
        public string JobID {get;set;}
        public string TargetLocation {get; set;}
    }

    ```

    b. Sostituire **STORAGE_CONNECTIONNAME** nella riga 11 con il nome della connessione all'account di archiviazione (vedere il punto 8c).

    c. In alto a sinistra hello, fare clic su **salvare**.

    ![Salvare la funzione](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. toocomplete hello (funzione), aggiungere un altro file eseguendo hello seguenti:

    a. Fare clic su **Visualizza file**.

       ![collegamento "Visualizza file" Hello](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    b. Fare clic su **Aggiungi**.
    
    c. Digitare **project.json** e quindi premere INVIO.
    
    d. In hello **Project** file, incollare hello seguente codice:

    ```
    {
    "frameworks": {
        "net46":{
        "dependencies": {
            "windowsazure.storage": "8.1.1"
        }
        }
    }
    }

    ```

    e. Fare clic su **Salva**.

È stata creata una funzione di Azure. Questa funzione viene attivata ogni volta che viene generato un nuovo blob dal processo di trasformazione dei dati hello.

## <a name="next-steps"></a>Passaggi successivi

[Utilizzare i dati di interfaccia utente di gestione dati di StorSimple tootransform](storsimple-data-manager-ui.md)
