---
title: aaaUse .NET SDK per i processi di gestione di dati di Microsoft Azure StorSimple | Documenti Microsoft
description: Informazioni su come i processi di toouse .NET SDK toolaunch StorSimple Data Manager (anteprima privata)
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
ms.openlocfilehash: b07fe64369574c994fd28d42786aa02dca435ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a><span data-ttu-id="67307-103">Utilizzare hello .net SDK tooinitiate la trasformazione dei dati (anteprima privata)</span><span class="sxs-lookup"><span data-stu-id="67307-103">Use hello .Net SDK tooinitiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="67307-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="67307-104">Overview</span></span>

<span data-ttu-id="67307-105">In questo articolo viene illustrato come utilizzare funzionalità di trasformazione dati hello all'interno di tootransform di servizio dati di StorSimple Manager hello dati del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="67307-105">This article explains how you can use hello data transformation feature within hello StorSimple Data Manager service tootransform StorSimple device data.</span></span> <span data-ttu-id="67307-106">Hello dati trasformati vengono quindi utilizzati da altri servizi Azure nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="67307-106">hello transformed data is then consumed by other Azure services in hello cloud.</span></span> <span data-ttu-id="67307-107">articolo Hello dispone inoltre toohelp una procedura dettagliata, creare un tooinitiate di applicazione console .NET esempio un processo di trasformazione dei dati e tenere traccia dei risultati per il completamento.</span><span class="sxs-lookup"><span data-stu-id="67307-107">hello article also has a walkthrough toohelp create a sample .NET console application tooinitiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67307-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="67307-108">Prerequisites</span></span>

<span data-ttu-id="67307-109">Prima di iniziare, assicurarsi di disporre di:</span><span class="sxs-lookup"><span data-stu-id="67307-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="67307-110">Un sistema con Visual Studio 2012, 2013, 2015 o 2017 installato.</span><span class="sxs-lookup"><span data-stu-id="67307-110">A system with Visual Studio 2012, 2013, 2015, or 2017 installed.</span></span>
*   <span data-ttu-id="67307-111">Azure Powershell installato.</span><span class="sxs-lookup"><span data-stu-id="67307-111">Azure Powershell installed.</span></span> <span data-ttu-id="67307-112">[Scaricare Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="67307-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="67307-113">Configurazione processo impostazioni di tooinitialize hello la trasformazione dei dati (istruzioni tooobtain queste impostazioni sono incluse in questo caso).</span><span class="sxs-lookup"><span data-stu-id="67307-113">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="67307-114">Una definizione di processo configurata correttamente in una risorsa dati ibridi all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="67307-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="67307-115">Tutte le DLL necessarie hello.</span><span class="sxs-lookup"><span data-stu-id="67307-115">All hello required dlls.</span></span> <span data-ttu-id="67307-116">Scaricare queste DLL da hello [repository GitHub](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span><span class="sxs-lookup"><span data-stu-id="67307-116">Download these dlls from hello [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="67307-117">`Get-ConfigurationParams.ps1`[script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) dal repository github hello.</span><span class="sxs-lookup"><span data-stu-id="67307-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="67307-118">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="67307-118">Step-by-step</span></span>

<span data-ttu-id="67307-119">Eseguire hello seguendo i passaggi toouse .NET toolaunch un processo di trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="67307-119">Perform hello following steps toouse .NET toolaunch a data transformation job.</span></span>

1. <span data-ttu-id="67307-120">parametri di configurazione tooretrieve hello, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="67307-120">tooretrieve hello configuration parameters, do hello following steps:</span></span>
    1. <span data-ttu-id="67307-121">Scaricare hello `Get-ConfigurationParams.ps1` dallo script di repository github hello in `C:\DataTransformation` percorso.</span><span class="sxs-lookup"><span data-stu-id="67307-121">Download hello `Get-ConfigurationParams.ps1` from hello github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="67307-122">Eseguire hello `Get-ConfigurationParams.ps1` script dal repository github hello.</span><span class="sxs-lookup"><span data-stu-id="67307-122">Run hello `Get-ConfigurationParams.ps1` script from hello github repository.</span></span> <span data-ttu-id="67307-123">Digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="67307-123">Type hello following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="67307-124">È possibile passare in uno qualsiasi dei valori hello ActiveDirectoryKey e AppName.</span><span class="sxs-lookup"><span data-stu-id="67307-124">You can pass in any values for hello ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="67307-125">Questo script restituisce hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="67307-125">This script outputs hello following values:</span></span>
    * <span data-ttu-id="67307-126">ID client</span><span class="sxs-lookup"><span data-stu-id="67307-126">Client ID</span></span>
    * <span data-ttu-id="67307-127">ID tenant</span><span class="sxs-lookup"><span data-stu-id="67307-127">Tenant ID</span></span>
    * <span data-ttu-id="67307-128">Chiave di Directory attiva (quella hello uno sopra specificato)</span><span class="sxs-lookup"><span data-stu-id="67307-128">Active Directory key (same as hello one entered above)</span></span>
    * <span data-ttu-id="67307-129">ID sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="67307-129">Subscription ID</span></span>

3. <span data-ttu-id="67307-130">Usando Visual Studio 2012, 2013 o 2015, creare un'applicazione console .NET in C#.</span><span class="sxs-lookup"><span data-stu-id="67307-130">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="67307-131">Avviare **Visual Studio 2012/2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="67307-131">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="67307-132">Fare clic su **File**, punto troppo**New**, fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="67307-132">Click **File**, point too**New**, and click **Project**.</span></span>
    2. <span data-ttu-id="67307-133">Espandere **Modelli** e quindi selezionare **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="67307-133">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="67307-134">Selezionare **applicazione Console** dall'elenco di hello dei tipi di progetto su hello destra.</span><span class="sxs-lookup"><span data-stu-id="67307-134">Select **Console Application** from hello list of project types on hello right.</span></span>
    4. <span data-ttu-id="67307-135">Immettere **DataTransformationApp** per hello **nome**.</span><span class="sxs-lookup"><span data-stu-id="67307-135">Enter **DataTransformationApp** for hello **Name**.</span></span>
    5. <span data-ttu-id="67307-136">Selezionare **C:\DataTransformation** per hello **percorso**.</span><span class="sxs-lookup"><span data-stu-id="67307-136">Select **C:\DataTransformation** for hello **Location**.</span></span>
    6. <span data-ttu-id="67307-137">Fare clic su **OK** progetto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="67307-137">Click **OK** toocreate hello project.</span></span>

4.  <span data-ttu-id="67307-138">A questo punto, aggiungere tutte le DLL presenti in hello [DLL](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) cartella **riferimenti** nel progetto hello creato.</span><span class="sxs-lookup"><span data-stu-id="67307-138">Now, add all DLLs present in hello [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in hello project that you created.</span></span> <span data-ttu-id="67307-139">file dll di hello toodownload, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="67307-139">toodownload hello dll files, do hello following:</span></span>

    1. <span data-ttu-id="67307-140">In Visual Studio, andare troppo**Vista > Esplora soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="67307-140">In Visual Studio, go too**View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="67307-141">Fare clic a sinistra di hello freccia toohello del progetto App di trasformazione di dati.</span><span class="sxs-lookup"><span data-stu-id="67307-141">Click hello arrow toohello left of Data Transformation App project.</span></span> <span data-ttu-id="67307-142">Fare clic su **riferimenti** e quindi fare doppio clic su troppo**Aggiungi riferimento**.</span><span class="sxs-lookup"><span data-stu-id="67307-142">Click **References** and then right-click too**Add Reference**.</span></span>
    2. <span data-ttu-id="67307-143">Cerca nel percorso della cartella di pacchetti hello toohello, selezionare tutte le DLL hello e fare clic su **Aggiungi**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="67307-143">Browse toohello location of hello packages folder, select all hello DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="67307-144">Aggiungere il seguente hello **utilizzando** istruzioni toohello file di origine (Program.cs) nel progetto hello.</span><span class="sxs-lookup"><span data-stu-id="67307-144">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="67307-145">Hello seguente codice inizializza l'istanza del processo di trasformazione dati hello.</span><span class="sxs-lookup"><span data-stu-id="67307-145">hello following code initializes hello data transformation job instance.</span></span> <span data-ttu-id="67307-146">Questo componente aggiuntivo hello **metodo Main**.</span><span class="sxs-lookup"><span data-stu-id="67307-146">Add this in hello **Main method**.</span></span> <span data-ttu-id="67307-147">Sostituire i valori hello dei parametri di configurazione come ottenuto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="67307-147">Replace hello values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="67307-148">Inserire i valori hello **nome gruppo di risorse** e **nome risorsa dati ibrido**.</span><span class="sxs-lookup"><span data-stu-id="67307-148">Plug in hello values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="67307-149">Hello **nome gruppo di risorse** è hello quello che ospita una risorsa di dati ibrido hello in cui hello definizione del processo è stato configurato.</span><span class="sxs-lookup"><span data-stu-id="67307-149">hello **Resource Group Name** is hello one that hosts hello Hybrid Data Resource on which hello job definition was configured.</span></span>

    ```
    // Setup hello configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize hello Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. <span data-ttu-id="67307-150">Specificare i parametri con cui hello definizione del processo deve toobe eseguire hello</span><span class="sxs-lookup"><span data-stu-id="67307-150">Specify hello parameters with which hello job definition needs toobe run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="67307-151">OPPURE</span><span class="sxs-lookup"><span data-stu-id="67307-151">(OR)</span></span>

    <span data-ttu-id="67307-152">Se si desidera che i parametri di definizione del processo di toochange hello in fase di esecuzione, aggiunta hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="67307-152">If you want toochange hello job definition parameters during run time, then add hello following code:</span></span>

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of hello volume on hello StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require hello latest existing backup toobe picked else use TakeNow tootrigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of hello StorSimple device.
        DeviceName = "device-name",
        // Name of hello container in Azure storage where hello files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) toobe applied on files under hello root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of hello volume on StorSimple device on which hello relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. <span data-ttu-id="67307-153">Dopo l'inizializzazione di hello, aggiungere il seguente codice tootrigger un processo di trasformazione dei dati nella definizione del processo hello hello.</span><span class="sxs-lookup"><span data-stu-id="67307-153">After hello initialization, add hello following code tootrigger a data transformation job on hello job definition.</span></span> <span data-ttu-id="67307-154">Plug-in hello appropriato **nome definizione di processo**.</span><span class="sxs-lookup"><span data-stu-id="67307-154">Plug in hello appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="67307-155">Questo processo Carica file hello corrispondenza presente nella directory radice dell'hello nel contenitore specificato toohello volume StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="67307-155">This job uploads hello matched files present under hello root directory on hello StorSimple volume toohello specified container.</span></span> <span data-ttu-id="67307-156">Quando viene caricato un file, viene eliminato un messaggio nella coda di hello (in hello stesso account di archiviazione come contenitore hello) con hello stesso nome come definizione del processo hello.</span><span class="sxs-lookup"><span data-stu-id="67307-156">When a file is uploaded, a message is dropped in hello queue (in hello same storage account as hello container) with hello same name as hello job definition.</span></span> <span data-ttu-id="67307-157">Questo messaggio può essere utilizzato come un tooinitiate trigger qualsiasi ulteriore elaborazione del file hello.</span><span class="sxs-lookup"><span data-stu-id="67307-157">This message can be used as a trigger tooinitiate any further processing of hello file.</span></span>

10. <span data-ttu-id="67307-158">Una volta processo hello è stato attivato, è possibile aggiungere hello seguente processo hello tootrack di codice per il completamento.</span><span class="sxs-lookup"><span data-stu-id="67307-158">Once hello job has been triggered, add hello following code tootrack hello job for completion.</span></span>

    ```
    Job jobDetails = null;

    // Poll hello job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for hello status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of hello job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // toohold hello console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a><span data-ttu-id="67307-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67307-159">Next steps</span></span>

<span data-ttu-id="67307-160">[Utilizzare i dati di interfaccia utente di gestione dati di StorSimple tootransform](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="67307-160">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
