---
title: Cambiare il percorso BLOB da quello predefinito | Microsoft Docs
description: Informazioni su come impostare una funzione di Azure per rinominare un percorso di file BLOB (anteprima privata)
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
ms.openlocfilehash: 057d4d7370207859617eb63238bf425bfa6d3e16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="change-a-blob-path-from-the-default-path-private-preview"></a><span data-ttu-id="3c613-103">Cambiare il percorso BLOB da quello predefinito (anteprima privata)</span><span class="sxs-lookup"><span data-stu-id="3c613-103">Change a blob path from the default path (private preview)</span></span>

<span data-ttu-id="3c613-104">L'articolo descrive come impostare una funzione di Azure per rinominare un percorso di file BLOB predefinito.</span><span class="sxs-lookup"><span data-stu-id="3c613-104">This article describes how to set up an Azure function to rename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3c613-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3c613-105">Prerequisites</span></span>

<span data-ttu-id="3c613-106">È necessario disporre di una definizione del processo configurata correttamente in una risorsa dati ibrida all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3c613-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="3c613-107">Creare una funzione di Azure</span><span class="sxs-lookup"><span data-stu-id="3c613-107">Create an Azure function</span></span>

<span data-ttu-id="3c613-108">Per creare una funzione di Azure, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3c613-108">To create an Azure function, do the following:</span></span>

1. <span data-ttu-id="3c613-109">Accedere al [portale di Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3c613-109">Go to the [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="3c613-110">Nella parte superiore del riquadro sinistro fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="3c613-110">At the top of the left pane, click **New**.</span></span> 

3. <span data-ttu-id="3c613-111">Digitare **App per le funzioni** nella casella **Cerca** e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="3c613-111">In the **Search** box, type **Function App**, and then press Enter.</span></span>

    ![Digitare "App per le funzioni" nella casella Cerca](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="3c613-113">Fare clic su **App per le funzioni** nell'elenco **Risultati**.</span><span class="sxs-lookup"><span data-stu-id="3c613-113">In the **Results** list, click **Function App**.</span></span>

    ![Selezionare la risorsa app per le funzioni nell'elenco dei risultati](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="3c613-115">Verrà visualizzata la finestra **App per le funzioni**.</span><span class="sxs-lookup"><span data-stu-id="3c613-115">The **Function App** window opens.</span></span>

5. <span data-ttu-id="3c613-116">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3c613-116">Click **Create**.</span></span>

    ![Pulsante "Crea" della finestra App per le funzioni](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="3c613-118">Nel pannello di configurazione **App per le funzioni** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3c613-118">On the **Function App** configuration blade, do the following:</span></span>

    <span data-ttu-id="3c613-119">a.</span><span class="sxs-lookup"><span data-stu-id="3c613-119">a.</span></span> <span data-ttu-id="3c613-120">Nella casella **Nome app** digitare il nome dell'app.</span><span class="sxs-lookup"><span data-stu-id="3c613-120">In the **App name** box, type the app name.</span></span>
    
    <span data-ttu-id="3c613-121">b.</span><span class="sxs-lookup"><span data-stu-id="3c613-121">b.</span></span> <span data-ttu-id="3c613-122">Nella casella **Sottoscrizione** digitare il nome della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3c613-122">In the **Subscription** box, type the name of the subscription.</span></span>

    <span data-ttu-id="3c613-123">c.</span><span class="sxs-lookup"><span data-stu-id="3c613-123">c.</span></span> <span data-ttu-id="3c613-124">In **Gruppo di risorse** fare clic su **Crea nuovo** e quindi digitare il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3c613-124">Under **Resource Group**, click **Create new**, and then type the name of the resource group.</span></span>

    <span data-ttu-id="3c613-125">d.</span><span class="sxs-lookup"><span data-stu-id="3c613-125">d.</span></span> <span data-ttu-id="3c613-126">Nella casella **Piano di hosting** digitare **Piano a consumo**.</span><span class="sxs-lookup"><span data-stu-id="3c613-126">In the **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="3c613-127">e.</span><span class="sxs-lookup"><span data-stu-id="3c613-127">e.</span></span> <span data-ttu-id="3c613-128">Nella casella **Percorso** digitare il percorso.</span><span class="sxs-lookup"><span data-stu-id="3c613-128">In the **Location** box, type the location.</span></span>

    <span data-ttu-id="3c613-129">f.</span><span class="sxs-lookup"><span data-stu-id="3c613-129">f.</span></span> <span data-ttu-id="3c613-130">In **Account di archiviazione** selezionare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="3c613-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="3c613-131">Un account di archiviazione viene usato internamente per la funzione.</span><span class="sxs-lookup"><span data-stu-id="3c613-131">A storage account is used internally for the function.</span></span>

    ![Immettere i dati per la configurazione della nuova app per le funzioni](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="3c613-133">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3c613-133">Click **Create**.</span></span>  
    <span data-ttu-id="3c613-134">Verrà creata l'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="3c613-134">The function app is created.</span></span>

8. <span data-ttu-id="3c613-135">Nel riquadro sinistro fare clic su **Altri servizi** e quindi seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3c613-135">In the left pane, click **More services**, and then do the following:</span></span>
    
    <span data-ttu-id="3c613-136">a.</span><span class="sxs-lookup"><span data-stu-id="3c613-136">a.</span></span> <span data-ttu-id="3c613-137">Nella casella **Filtro** digitare **Servizi app**.</span><span class="sxs-lookup"><span data-stu-id="3c613-137">In the **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="3c613-138">b.</span><span class="sxs-lookup"><span data-stu-id="3c613-138">b.</span></span> <span data-ttu-id="3c613-139">Fare clic su **Servizi app**.</span><span class="sxs-lookup"><span data-stu-id="3c613-139">Click **App Services**.</span></span> 

    ![Collegamento "Altri servizi" nel riquadro sinistro](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="3c613-141">Nell'elenco dei servizi app fare clic sul nome dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="3c613-141">In the list of app services, click the name of the function app.</span></span>  
    <span data-ttu-id="3c613-142">Verrà visualizzata la pagina dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="3c613-142">The function app page opens.</span></span>

10. <span data-ttu-id="3c613-143">Nel riquadro sinistro fare clic su **Nuova funzione** e quindi seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3c613-143">In the left pane, click **New Function**, and then do the following:</span></span> 

    <span data-ttu-id="3c613-144">a.</span><span class="sxs-lookup"><span data-stu-id="3c613-144">a.</span></span> <span data-ttu-id="3c613-145">Nell'elenco **Linguaggio** selezionare **C#**.</span><span class="sxs-lookup"><span data-stu-id="3c613-145">In the **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="3c613-146">b.</span><span class="sxs-lookup"><span data-stu-id="3c613-146">b.</span></span> <span data-ttu-id="3c613-147">Nella matrice di riquadri di modello selezionare **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="3c613-147">In the array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="3c613-148">c.</span><span class="sxs-lookup"><span data-stu-id="3c613-148">c.</span></span> <span data-ttu-id="3c613-149">Nella casella **Assegnare un nome alla funzione** digitare un nome per la funzione.</span><span class="sxs-lookup"><span data-stu-id="3c613-149">In the **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="3c613-150">d.</span><span class="sxs-lookup"><span data-stu-id="3c613-150">d.</span></span> <span data-ttu-id="3c613-151">Nella casella **Nome coda** digitare in nome della definizione del processo di trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="3c613-151">In the **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="3c613-152">e.</span><span class="sxs-lookup"><span data-stu-id="3c613-152">e.</span></span> <span data-ttu-id="3c613-153">In **Connessione dell'account di archiviazione** fare clic su **Nuova** e quindi selezionare l'account che corrisponde al processo di trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="3c613-153">Under **Storage account connection**, click **new**, and then select the account that corresponds to the data-transformation job.</span></span>  
        <span data-ttu-id="3c613-154">Prendere nota del nome della connessione.</span><span class="sxs-lookup"><span data-stu-id="3c613-154">Make a note of the connection name.</span></span> <span data-ttu-id="3c613-155">Questo nome è necessario in seguito nella funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c613-155">The name is required later in the Azure function.</span></span>

       ![Creare una nuova funzione C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="3c613-157">f.</span><span class="sxs-lookup"><span data-stu-id="3c613-157">f.</span></span> <span data-ttu-id="3c613-158">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3c613-158">Click **Create**.</span></span>  
    <span data-ttu-id="3c613-159">Verrà visualizzata la finestra **Funzione**.</span><span class="sxs-lookup"><span data-stu-id="3c613-159">The **Function** window opens.</span></span>

11. <span data-ttu-id="3c613-160">Nella finestra **Funzione** eseguire il file con estensione _csx_ e quindi seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3c613-160">In the **Function** window, run _.csx_ file, and then do the following:</span></span>

    <span data-ttu-id="3c613-161">a.</span><span class="sxs-lookup"><span data-stu-id="3c613-161">a.</span></span> <span data-ttu-id="3c613-162">Incollare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="3c613-162">Paste the following code:</span></span>

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

        // Create the blob client.
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
            // Skip to copy the blob to new container, if source blob doesn't exist
            log.Info($"The specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy to new container
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

    <span data-ttu-id="3c613-163">b.</span><span class="sxs-lookup"><span data-stu-id="3c613-163">b.</span></span> <span data-ttu-id="3c613-164">Sostituire **STORAGE_CONNECTIONNAME** nella riga 11 con il nome della connessione all'account di archiviazione (vedere il punto 8c).</span><span class="sxs-lookup"><span data-stu-id="3c613-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="3c613-165">c.</span><span class="sxs-lookup"><span data-stu-id="3c613-165">c.</span></span> <span data-ttu-id="3c613-166">Nella parte superiore sinistra fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3c613-166">At the top left, click **Save**.</span></span>

    ![Salvare la funzione](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="3c613-168">Per completare la funzione, aggiungere un altro file seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3c613-168">To complete the function, add one more file by doing the following:</span></span>

    <span data-ttu-id="3c613-169">a.</span><span class="sxs-lookup"><span data-stu-id="3c613-169">a.</span></span> <span data-ttu-id="3c613-170">Fare clic su **Visualizza file**.</span><span class="sxs-lookup"><span data-stu-id="3c613-170">Click **View files**.</span></span>

       ![Collegamento "Visualizza file"](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="3c613-172">b.</span><span class="sxs-lookup"><span data-stu-id="3c613-172">b.</span></span> <span data-ttu-id="3c613-173">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3c613-173">Click **Add**.</span></span>
    
    <span data-ttu-id="3c613-174">c.</span><span class="sxs-lookup"><span data-stu-id="3c613-174">c.</span></span> <span data-ttu-id="3c613-175">Digitare **project.json** e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="3c613-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="3c613-176">d.</span><span class="sxs-lookup"><span data-stu-id="3c613-176">d.</span></span> <span data-ttu-id="3c613-177">Incollare il codice seguente nel file **project.json**:</span><span class="sxs-lookup"><span data-stu-id="3c613-177">In the **project.json** file, paste the following code:</span></span>

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

    <span data-ttu-id="3c613-178">e.</span><span class="sxs-lookup"><span data-stu-id="3c613-178">e.</span></span> <span data-ttu-id="3c613-179">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3c613-179">Click **Save**.</span></span>

<span data-ttu-id="3c613-180">È stata creata una funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c613-180">You have created an Azure function.</span></span> <span data-ttu-id="3c613-181">Questa funzione viene attivata ogni volta che il processo di trasformazione dei dati genera un nuovo BLOB.</span><span class="sxs-lookup"><span data-stu-id="3c613-181">This function is triggered each time a new blob is generated by the data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c613-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c613-182">Next steps</span></span>

[<span data-ttu-id="3c613-183">Usare l'interfaccia utente di StorSimple Data Manager per la trasformazione dei dati</span><span class="sxs-lookup"><span data-stu-id="3c613-183">Use StorSimple Data Manager UI to transform your data</span></span>](storsimple-data-manager-ui.md)
