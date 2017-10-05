---
title: Usare .NET SDK per i processi di Microsoft Azure StorSimple Data Manager | Documentazione Microsoft
description: Informazioni su come usare .NET SDK per avviare i processi di StorSimple Data Manager (anteprima privata)
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
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 44d243a034b20b99faf284c8615e470bc6f9d020
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-the-net-sdk-to-initiate-data-transformation-private-preview"></a><span data-ttu-id="9002b-103">Usare .Net SDK per avviare la trasformazione dei dati (anteprima privata)</span><span class="sxs-lookup"><span data-stu-id="9002b-103">Use the .Net SDK to initiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="9002b-104">Overview</span><span class="sxs-lookup"><span data-stu-id="9002b-104">Overview</span></span>

<span data-ttu-id="9002b-105">Questo articolo illustra come usare la funzione di trasformazione dei dati all'interno del servizio StorSimple Data Manager per trasformare i dati del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9002b-105">This article explains how you can use the data transformation feature within the StorSimple Data Manager service to transform StorSimple device data.</span></span> <span data-ttu-id="9002b-106">I dati trasformati vengono quindi usati da altri servizi di Azure nel cloud.</span><span class="sxs-lookup"><span data-stu-id="9002b-106">The transformed data is then consumed by other Azure services in the cloud.</span></span> <span data-ttu-id="9002b-107">L'articolo descrive anche una procedura dettagliata per creare un'applicazione console .NET di esempio allo scopo di avviare un processo di trasformazione dei dati e tenere traccia dei risultati per il completamento.</span><span class="sxs-lookup"><span data-stu-id="9002b-107">The article also has a walkthrough to help create a sample .NET console application to initiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9002b-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9002b-108">Prerequisites</span></span>

<span data-ttu-id="9002b-109">Prima di iniziare, assicurarsi di disporre di:</span><span class="sxs-lookup"><span data-stu-id="9002b-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="9002b-110">Un sistema con Visual Studio 2012, 2013, 2015 o 2017 installato.</span><span class="sxs-lookup"><span data-stu-id="9002b-110">A system with Visual Studio 2012, 2013, 2015, or 2017 installed.</span></span>
*   <span data-ttu-id="9002b-111">Azure Powershell installato.</span><span class="sxs-lookup"><span data-stu-id="9002b-111">Azure Powershell installed.</span></span> <span data-ttu-id="9002b-112">[Scaricare Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="9002b-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="9002b-113">Impostazioni di configurazione per l'inizializzazione del processo di trasformazione dei dati (le istruzioni per ottenere queste impostazioni sono incluse qui).</span><span class="sxs-lookup"><span data-stu-id="9002b-113">Configuration settings to initialize the Data Transformation job (instructions to obtain these settings are included here).</span></span>
*   <span data-ttu-id="9002b-114">Una definizione di processo configurata correttamente in una risorsa dati ibridi all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="9002b-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="9002b-115">Tutte le DLL necessarie.</span><span class="sxs-lookup"><span data-stu-id="9002b-115">All the required dlls.</span></span> <span data-ttu-id="9002b-116">Scaricare le DLL dal [repository GitHub](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span><span class="sxs-lookup"><span data-stu-id="9002b-116">Download these dlls from the [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="9002b-117">[Script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) `Get-ConfigurationParams.ps1` dal repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="9002b-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from the github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="9002b-118">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="9002b-118">Step-by-step</span></span>

<span data-ttu-id="9002b-119">Eseguire la procedura seguente per usare .NET allo scopo di avviare un processo di trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="9002b-119">Perform the following steps to use .NET to launch a data transformation job.</span></span>

1. <span data-ttu-id="9002b-120">Per recuperare i parametri di configurazione, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9002b-120">To retrieve the configuration parameters, do the following steps:</span></span>
    1. <span data-ttu-id="9002b-121">Scaricare lo script `Get-ConfigurationParams.ps1` dal repository GitHub nel percorso `C:\DataTransformation`.</span><span class="sxs-lookup"><span data-stu-id="9002b-121">Download the `Get-ConfigurationParams.ps1` from the github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="9002b-122">Eseguire lo script `Get-ConfigurationParams.ps1` dal repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="9002b-122">Run the `Get-ConfigurationParams.ps1` script from the github repository.</span></span> <span data-ttu-id="9002b-123">Digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9002b-123">Type the following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="9002b-124">È possibile trasmettere qualsiasi valore per ActiveDirectoryKey e AppName.</span><span class="sxs-lookup"><span data-stu-id="9002b-124">You can pass in any values for the ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="9002b-125">Questo script restituisce i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="9002b-125">This script outputs the following values:</span></span>
    * <span data-ttu-id="9002b-126">ID Client</span><span class="sxs-lookup"><span data-stu-id="9002b-126">Client ID</span></span>
    * <span data-ttu-id="9002b-127">ID tenant</span><span class="sxs-lookup"><span data-stu-id="9002b-127">Tenant ID</span></span>
    * <span data-ttu-id="9002b-128">Chiave di Active Directory (uguale a quella immessa in precedenza)</span><span class="sxs-lookup"><span data-stu-id="9002b-128">Active Directory key (same as the one entered above)</span></span>
    * <span data-ttu-id="9002b-129">ID sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="9002b-129">Subscription ID</span></span>

3. <span data-ttu-id="9002b-130">Usando Visual Studio 2012, 2013 o 2015, creare un'applicazione console .NET in C#.</span><span class="sxs-lookup"><span data-stu-id="9002b-130">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="9002b-131">Avviare **Visual Studio 2012/2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="9002b-131">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="9002b-132">Fare clic su **File**, scegliere **Nuovo** e quindi fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="9002b-132">Click **File**, point to **New**, and click **Project**.</span></span>
    2. <span data-ttu-id="9002b-133">Espandere **Modelli** e quindi selezionare **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="9002b-133">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="9002b-134">Selezionare **Applicazione console** dall'elenco dei tipi di progetto a destra.</span><span class="sxs-lookup"><span data-stu-id="9002b-134">Select **Console Application** from the list of project types on the right.</span></span>
    4. <span data-ttu-id="9002b-135">Immettere **DataTransformationApp** per il **Nome**.</span><span class="sxs-lookup"><span data-stu-id="9002b-135">Enter **DataTransformationApp** for the **Name**.</span></span>
    5. <span data-ttu-id="9002b-136">Selezionare **C:\DataTransformation** per il **Percorso**.</span><span class="sxs-lookup"><span data-stu-id="9002b-136">Select **C:\DataTransformation** for the **Location**.</span></span>
    6. <span data-ttu-id="9002b-137">Fare clic su **OK** per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="9002b-137">Click **OK** to create the project.</span></span>

4.  <span data-ttu-id="9002b-138">Aggiungere quindi tutte le DLL presenti nella cartella [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) come **Riferimenti** nel progetto creato.</span><span class="sxs-lookup"><span data-stu-id="9002b-138">Now, add all DLLs present in the [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in the project that you created.</span></span> <span data-ttu-id="9002b-139">Per scaricare i file DLL, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9002b-139">To download the dll files, do the following:</span></span>

    1. <span data-ttu-id="9002b-140">In Visual Studio passare a **Visualizza > Esplora soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="9002b-140">In Visual Studio, go to **View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="9002b-141">Fare clic sulla freccia a sinistra del progetto Data Transformation App.</span><span class="sxs-lookup"><span data-stu-id="9002b-141">Click the arrow to the left of Data Transformation App project.</span></span> <span data-ttu-id="9002b-142">Fare clic su **Riferimenti** e quindi fare clic con il pulsante destro del mouse su **Aggiungi riferimento**.</span><span class="sxs-lookup"><span data-stu-id="9002b-142">Click **References** and then right-click to **Add Reference**.</span></span>
    2. <span data-ttu-id="9002b-143">Passare al percorso della cartella dei pacchetti, selezionare tutte le DLL e fare clic su **Aggiungi**, quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9002b-143">Browse to the location of the packages folder, select all the DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="9002b-144">Aggiungere le istruzioni **using** seguenti al file di origine (Program.cs) nel progetto.</span><span class="sxs-lookup"><span data-stu-id="9002b-144">Add the following **using** statements to the source file (Program.cs) in the project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="9002b-145">Il codice seguente consente di inizializzare l'istanza di processo di trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="9002b-145">The following code initializes the data transformation job instance.</span></span> <span data-ttu-id="9002b-146">Aggiungerlo nel **metodo Main**.</span><span class="sxs-lookup"><span data-stu-id="9002b-146">Add this in the **Main method**.</span></span> <span data-ttu-id="9002b-147">Sostituire i valori dei parametri di configurazione ottenuti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9002b-147">Replace the values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="9002b-148">Immettere i valori del **nome del gruppo di risorse** e del **nome della risorsa dati ibridi**.</span><span class="sxs-lookup"><span data-stu-id="9002b-148">Plug in the values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="9002b-149">Il **nome del gruppo di risorse** ospita la risorsa dati ibridi in cui era stata configurata la definizione del processo.</span><span class="sxs-lookup"><span data-stu-id="9002b-149">The **Resource Group Name** is the one that hosts the Hybrid Data Resource on which the job definition was configured.</span></span>

    ```
    // Setup the configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize the Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. <span data-ttu-id="9002b-150">Specificare i parametri con cui deve essere eseguita la definizione del processo</span><span class="sxs-lookup"><span data-stu-id="9002b-150">Specify the parameters with which the job definition needs to be run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="9002b-151">OPPURE</span><span class="sxs-lookup"><span data-stu-id="9002b-151">(OR)</span></span>

    <span data-ttu-id="9002b-152">Se si desidera modificare i parametri della definizione del processo in fase di esecuzione, aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="9002b-152">If you want to change the job definition parameters during run time, then add the following code:</span></span>

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of the volume on the StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require the latest existing backup to be picked else use TakeNow to trigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of the StorSimple device.
        DeviceName = "device-name",
        // Name of the container in Azure storage where the files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) to be applied on files under the root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of the volume on StorSimple device on which the relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. <span data-ttu-id="9002b-153">Dopo l'inizializzazione, aggiungere il codice seguente per attivare un processo di trasformazione dati sulla definizione del processo.</span><span class="sxs-lookup"><span data-stu-id="9002b-153">After the initialization, add the following code to trigger a data transformation job on the job definition.</span></span> <span data-ttu-id="9002b-154">Immettere il **nome della definizione processo**.</span><span class="sxs-lookup"><span data-stu-id="9002b-154">Plug in the appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve the jobId and the retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="9002b-155">Questo processo carica i file corrispondenti presenti nella directory radice del volume di StorSimple nel contenitore specificato.</span><span class="sxs-lookup"><span data-stu-id="9002b-155">This job uploads the matched files present under the root directory on the StorSimple volume to the specified container.</span></span> <span data-ttu-id="9002b-156">Quando viene caricato un file, viene rilasciato un messaggio nella coda (nello stesso account di archiviazione del contenitore) con lo stesso nome della definizione del processo.</span><span class="sxs-lookup"><span data-stu-id="9002b-156">When a file is uploaded, a message is dropped in the queue (in the same storage account as the container) with the same name as the job definition.</span></span> <span data-ttu-id="9002b-157">Questo messaggio può essere usato come trigger per avviare un'ulteriore elaborazione del file.</span><span class="sxs-lookup"><span data-stu-id="9002b-157">This message can be used as a trigger to initiate any further processing of the file.</span></span>

10. <span data-ttu-id="9002b-158">Dopo l'attivazione del processo, aggiungere il codice seguente per tenere traccia dei risultati per il completamento.</span><span class="sxs-lookup"><span data-stu-id="9002b-158">Once the job has been triggered, add the following code to track the job for completion.</span></span>

    ```
    Job jobDetails = null;

    // Poll the job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for the status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of the job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // To hold the console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a><span data-ttu-id="9002b-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9002b-159">Next steps</span></span>

<span data-ttu-id="9002b-160">[Usare l'interfaccia utente di StorSimple Data Manager per la trasformazione dei dati](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="9002b-160">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>
