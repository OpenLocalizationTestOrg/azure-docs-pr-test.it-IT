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
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a><span data-ttu-id="46ffb-103">Modificare il percorso di un blob dal percorso predefinito di hello (anteprima privata)</span><span class="sxs-lookup"><span data-stu-id="46ffb-103">Change a blob path from hello default path (private preview)</span></span>

<span data-ttu-id="46ffb-104">Questo articolo descrive come tooset backup di Azure funzione toorename un percorso di file blob predefinito.</span><span class="sxs-lookup"><span data-stu-id="46ffb-104">This article describes how tooset up an Azure function toorename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="46ffb-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="46ffb-105">Prerequisites</span></span>

<span data-ttu-id="46ffb-106">È necessario disporre di una definizione del processo configurata correttamente in una risorsa dati ibrida all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="46ffb-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="46ffb-107">Creare una funzione di Azure</span><span class="sxs-lookup"><span data-stu-id="46ffb-107">Create an Azure function</span></span>

<span data-ttu-id="46ffb-108">una funzione di Azure, toocreate hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="46ffb-108">toocreate an Azure function, do hello following:</span></span>

1. <span data-ttu-id="46ffb-109">Passare toohello [portale di Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="46ffb-109">Go toohello [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="46ffb-110">Nella parte superiore di hello del riquadro di sinistra hello, fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="46ffb-110">At hello top of hello left pane, click **New**.</span></span> 

3. <span data-ttu-id="46ffb-111">In hello **ricerca** digitare **funzione App**, quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="46ffb-111">In hello **Search** box, type **Function App**, and then press Enter.</span></span>

    ![Digitare "Funzione App" nella casella di ricerca hello](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="46ffb-113">In hello **risultati** elenco, fare clic su **funzione App**.</span><span class="sxs-lookup"><span data-stu-id="46ffb-113">In hello **Results** list, click **Function App**.</span></span>

    ![Risorse di app di funzione hello selezionare nell'elenco risultati hello](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="46ffb-115">Hello **funzione App** verrà visualizzata la finestra.</span><span class="sxs-lookup"><span data-stu-id="46ffb-115">hello **Function App** window opens.</span></span>

5. <span data-ttu-id="46ffb-116">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="46ffb-116">Click **Create**.</span></span>

    ![pulsante "Crea" finestra di Hello App (funzione)](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="46ffb-118">In hello **funzione App** pannello configurazione hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="46ffb-118">On hello **Function App** configuration blade, do hello following:</span></span>

    <span data-ttu-id="46ffb-119">a.</span><span class="sxs-lookup"><span data-stu-id="46ffb-119">a.</span></span> <span data-ttu-id="46ffb-120">In hello **nome App** casella, il nome del tipo hello app.</span><span class="sxs-lookup"><span data-stu-id="46ffb-120">In hello **App name** box, type hello app name.</span></span>
    
    <span data-ttu-id="46ffb-121">b.</span><span class="sxs-lookup"><span data-stu-id="46ffb-121">b.</span></span> <span data-ttu-id="46ffb-122">In hello **sottoscrizione** casella, il nome hello del tipo di sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="46ffb-122">In hello **Subscription** box, type hello name of hello subscription.</span></span>

    <span data-ttu-id="46ffb-123">c.</span><span class="sxs-lookup"><span data-stu-id="46ffb-123">c.</span></span> <span data-ttu-id="46ffb-124">In **gruppo di risorse**, fare clic su **Crea nuovo**e quindi hello nome del tipo hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="46ffb-124">Under **Resource Group**, click **Create new**, and then type hello name of hello resource group.</span></span>

    <span data-ttu-id="46ffb-125">d.</span><span class="sxs-lookup"><span data-stu-id="46ffb-125">d.</span></span> <span data-ttu-id="46ffb-126">In hello **piano di Hosting** digitare **consumo pianificare**.</span><span class="sxs-lookup"><span data-stu-id="46ffb-126">In hello **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="46ffb-127">e.</span><span class="sxs-lookup"><span data-stu-id="46ffb-127">e.</span></span> <span data-ttu-id="46ffb-128">In hello **percorso** casella Tipo hello percorso.</span><span class="sxs-lookup"><span data-stu-id="46ffb-128">In hello **Location** box, type hello location.</span></span>

    <span data-ttu-id="46ffb-129">f.</span><span class="sxs-lookup"><span data-stu-id="46ffb-129">f.</span></span> <span data-ttu-id="46ffb-130">In **Account di archiviazione** selezionare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="46ffb-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="46ffb-131">Un account di archiviazione viene utilizzato internamente per la funzione hello.</span><span class="sxs-lookup"><span data-stu-id="46ffb-131">A storage account is used internally for hello function.</span></span>

    ![Immettere i dati per la configurazione della nuova app per le funzioni](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="46ffb-133">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="46ffb-133">Click **Create**.</span></span>  
    <span data-ttu-id="46ffb-134">app di funzione Hello viene creato.</span><span class="sxs-lookup"><span data-stu-id="46ffb-134">hello function app is created.</span></span>

8. <span data-ttu-id="46ffb-135">Nel riquadro di sinistra hello, fare clic su **più servizi**e quindi hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="46ffb-135">In hello left pane, click **More services**, and then do hello following:</span></span>
    
    <span data-ttu-id="46ffb-136">a.</span><span class="sxs-lookup"><span data-stu-id="46ffb-136">a.</span></span> <span data-ttu-id="46ffb-137">In hello **filtro** digitare **servizi App**.</span><span class="sxs-lookup"><span data-stu-id="46ffb-137">In hello **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="46ffb-138">b.</span><span class="sxs-lookup"><span data-stu-id="46ffb-138">b.</span></span> <span data-ttu-id="46ffb-139">Fare clic su **Servizi app**.</span><span class="sxs-lookup"><span data-stu-id="46ffb-139">Click **App Services**.</span></span> 

    ![Collegamento "Ulteriori servizi" nel riquadro di sinistra hello](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="46ffb-141">Nell'elenco di hello dei servizi di app, fare clic su nome hello di hello funzione app.</span><span class="sxs-lookup"><span data-stu-id="46ffb-141">In hello list of app services, click hello name of hello function app.</span></span>  
    <span data-ttu-id="46ffb-142">verrà visualizzata la pagina dell'app funzione Hello.</span><span class="sxs-lookup"><span data-stu-id="46ffb-142">hello function app page opens.</span></span>

10. <span data-ttu-id="46ffb-143">Nel riquadro di sinistra hello, fare clic su **nuova funzione**e quindi hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="46ffb-143">In hello left pane, click **New Function**, and then do hello following:</span></span> 

    <span data-ttu-id="46ffb-144">a.</span><span class="sxs-lookup"><span data-stu-id="46ffb-144">a.</span></span> <span data-ttu-id="46ffb-145">In hello **Language** elenco, selezionare **c#**.</span><span class="sxs-lookup"><span data-stu-id="46ffb-145">In hello **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="46ffb-146">b.</span><span class="sxs-lookup"><span data-stu-id="46ffb-146">b.</span></span> <span data-ttu-id="46ffb-147">Nella matrice di hello dei riquadri di modello, selezionare **QueueTrigger CSharp**.</span><span class="sxs-lookup"><span data-stu-id="46ffb-147">In hello array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="46ffb-148">c.</span><span class="sxs-lookup"><span data-stu-id="46ffb-148">c.</span></span> <span data-ttu-id="46ffb-149">In hello **nome alla funzione di** , digitare un nome per la funzione.</span><span class="sxs-lookup"><span data-stu-id="46ffb-149">In hello **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="46ffb-150">d.</span><span class="sxs-lookup"><span data-stu-id="46ffb-150">d.</span></span> <span data-ttu-id="46ffb-151">In hello **nome coda** , digitare il nome di definizione del processo di trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="46ffb-151">In hello **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="46ffb-152">e.</span><span class="sxs-lookup"><span data-stu-id="46ffb-152">e.</span></span> <span data-ttu-id="46ffb-153">In **connessione ad account di archiviazione**, fare clic su **nuova**e quindi selezionare account hello corrispondente toohello processo di trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="46ffb-153">Under **Storage account connection**, click **new**, and then select hello account that corresponds toohello data-transformation job.</span></span>  
        <span data-ttu-id="46ffb-154">Prendere nota del nome di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="46ffb-154">Make a note of hello connection name.</span></span> <span data-ttu-id="46ffb-155">nome Hello è necessario in un secondo momento hello Azure (funzione).</span><span class="sxs-lookup"><span data-stu-id="46ffb-155">hello name is required later in hello Azure function.</span></span>

       ![Creare una nuova funzione C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="46ffb-157">f.</span><span class="sxs-lookup"><span data-stu-id="46ffb-157">f.</span></span> <span data-ttu-id="46ffb-158">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="46ffb-158">Click **Create**.</span></span>  
    <span data-ttu-id="46ffb-159">Hello **funzione** verrà visualizzata la finestra.</span><span class="sxs-lookup"><span data-stu-id="46ffb-159">hello **Function** window opens.</span></span>

11. <span data-ttu-id="46ffb-160">In hello **funzione** finestra, eseguire _csx_ file e quindi hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="46ffb-160">In hello **Function** window, run _.csx_ file, and then do hello following:</span></span>

    <span data-ttu-id="46ffb-161">a.</span><span class="sxs-lookup"><span data-stu-id="46ffb-161">a.</span></span> <span data-ttu-id="46ffb-162">Incollare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="46ffb-162">Paste hello following code:</span></span>

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

    <span data-ttu-id="46ffb-163">b.</span><span class="sxs-lookup"><span data-stu-id="46ffb-163">b.</span></span> <span data-ttu-id="46ffb-164">Sostituire **STORAGE_CONNECTIONNAME** nella riga 11 con il nome della connessione all'account di archiviazione (vedere il punto 8c).</span><span class="sxs-lookup"><span data-stu-id="46ffb-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="46ffb-165">c.</span><span class="sxs-lookup"><span data-stu-id="46ffb-165">c.</span></span> <span data-ttu-id="46ffb-166">In alto a sinistra hello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="46ffb-166">At hello top left, click **Save**.</span></span>

    ![Salvare la funzione](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="46ffb-168">toocomplete hello (funzione), aggiungere un altro file eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="46ffb-168">toocomplete hello function, add one more file by doing hello following:</span></span>

    <span data-ttu-id="46ffb-169">a.</span><span class="sxs-lookup"><span data-stu-id="46ffb-169">a.</span></span> <span data-ttu-id="46ffb-170">Fare clic su **Visualizza file**.</span><span class="sxs-lookup"><span data-stu-id="46ffb-170">Click **View files**.</span></span>

       ![collegamento "Visualizza file" Hello](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="46ffb-172">b.</span><span class="sxs-lookup"><span data-stu-id="46ffb-172">b.</span></span> <span data-ttu-id="46ffb-173">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="46ffb-173">Click **Add**.</span></span>
    
    <span data-ttu-id="46ffb-174">c.</span><span class="sxs-lookup"><span data-stu-id="46ffb-174">c.</span></span> <span data-ttu-id="46ffb-175">Digitare **project.json** e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="46ffb-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="46ffb-176">d.</span><span class="sxs-lookup"><span data-stu-id="46ffb-176">d.</span></span> <span data-ttu-id="46ffb-177">In hello **Project** file, incollare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="46ffb-177">In hello **project.json** file, paste hello following code:</span></span>

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

    <span data-ttu-id="46ffb-178">e.</span><span class="sxs-lookup"><span data-stu-id="46ffb-178">e.</span></span> <span data-ttu-id="46ffb-179">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="46ffb-179">Click **Save**.</span></span>

<span data-ttu-id="46ffb-180">È stata creata una funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="46ffb-180">You have created an Azure function.</span></span> <span data-ttu-id="46ffb-181">Questa funzione viene attivata ogni volta che viene generato un nuovo blob dal processo di trasformazione dei dati hello.</span><span class="sxs-lookup"><span data-stu-id="46ffb-181">This function is triggered each time a new blob is generated by hello data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46ffb-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="46ffb-182">Next steps</span></span>

[<span data-ttu-id="46ffb-183">Utilizzare i dati di interfaccia utente di gestione dati di StorSimple tootransform</span><span class="sxs-lookup"><span data-stu-id="46ffb-183">Use StorSimple Data Manager UI tootransform your data</span></span>](storsimple-data-manager-ui.md)
