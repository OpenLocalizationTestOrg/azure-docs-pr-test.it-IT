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
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a>Utilizzare hello .net SDK tooinitiate la trasformazione dei dati (anteprima privata)

## <a name="overview"></a>Panoramica

In questo articolo viene illustrato come utilizzare funzionalità di trasformazione dati hello all'interno di tootransform di servizio dati di StorSimple Manager hello dati del dispositivo StorSimple. Hello dati trasformati vengono quindi utilizzati da altri servizi Azure nel cloud hello. articolo Hello dispone inoltre toohelp una procedura dettagliata, creare un tooinitiate di applicazione console .NET esempio un processo di trasformazione dei dati e tenere traccia dei risultati per il completamento.

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare, assicurarsi di disporre di:
*   Un sistema con Visual Studio 2012, 2013, 2015 o 2017 installato.
*   Azure Powershell installato. [Scaricare Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   Configurazione processo impostazioni di tooinitialize hello la trasformazione dei dati (istruzioni tooobtain queste impostazioni sono incluse in questo caso).
*   Una definizione di processo configurata correttamente in una risorsa dati ibridi all'interno di un gruppo di risorse.
*   Tutte le DLL necessarie hello. Scaricare queste DLL da hello [repository GitHub](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).
*   `Get-ConfigurationParams.ps1`[script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) dal repository github hello.

## <a name="step-by-step"></a>Procedura dettagliata

Eseguire hello seguendo i passaggi toouse .NET toolaunch un processo di trasformazione dei dati.

1. parametri di configurazione tooretrieve hello, hello i passaggi seguenti:
    1. Scaricare hello `Get-ConfigurationParams.ps1` dallo script di repository github hello in `C:\DataTransformation` percorso.
    1. Eseguire hello `Get-ConfigurationParams.ps1` script dal repository github hello. Digitare hello comando seguente:

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        È possibile passare in uno qualsiasi dei valori hello ActiveDirectoryKey e AppName.


2. Questo script restituisce hello seguenti valori:
    * ID client
    * ID tenant
    * Chiave di Directory attiva (quella hello uno sopra specificato)
    * ID sottoscrizione

3. Usando Visual Studio 2012, 2013 o 2015, creare un'applicazione console .NET in C#.

    1. Avviare **Visual Studio 2012/2013/2015**.
    1. Fare clic su **File**, punto troppo**New**, fare clic su **progetto**.
    2. Espandere **Modelli** e quindi selezionare **Visual C#**.
    3. Selezionare **applicazione Console** dall'elenco di hello dei tipi di progetto su hello destra.
    4. Immettere **DataTransformationApp** per hello **nome**.
    5. Selezionare **C:\DataTransformation** per hello **percorso**.
    6. Fare clic su **OK** progetto hello toocreate.

4.  A questo punto, aggiungere tutte le DLL presenti in hello [DLL](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) cartella **riferimenti** nel progetto hello creato. file dll di hello toodownload, hello seguenti:

    1. In Visual Studio, andare troppo**Vista > Esplora soluzioni**.
    1. Fare clic a sinistra di hello freccia toohello del progetto App di trasformazione di dati. Fare clic su **riferimenti** e quindi fare doppio clic su troppo**Aggiungi riferimento**.
    2. Cerca nel percorso della cartella di pacchetti hello toohello, selezionare tutte le DLL hello e fare clic su **Aggiungi**, quindi fare clic su **OK**.

5. Aggiungere il seguente hello **utilizzando** istruzioni toohello file di origine (Program.cs) nel progetto hello.

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. Hello seguente codice inizializza l'istanza del processo di trasformazione dati hello. Questo componente aggiuntivo hello **metodo Main**. Sostituire i valori hello dei parametri di configurazione come ottenuto in precedenza. Inserire i valori hello **nome gruppo di risorse** e **nome risorsa dati ibrido**. Hello **nome gruppo di risorse** è hello quello che ospita una risorsa di dati ibrido hello in cui hello definizione del processo è stato configurato.

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

7. Specificare i parametri con cui hello definizione del processo deve toobe eseguire hello

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    OPPURE

    Se si desidera che i parametri di definizione del processo di toochange hello in fase di esecuzione, aggiunta hello seguente codice:

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

8. Dopo l'inizializzazione di hello, aggiungere il seguente codice tootrigger un processo di trasformazione dei dati nella definizione del processo hello hello. Plug-in hello appropriato **nome definizione di processo**.

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. Questo processo Carica file hello corrispondenza presente nella directory radice dell'hello nel contenitore specificato toohello volume StorSimple hello. Quando viene caricato un file, viene eliminato un messaggio nella coda di hello (in hello stesso account di archiviazione come contenitore hello) con hello stesso nome come definizione del processo hello. Questo messaggio può essere utilizzato come un tooinitiate trigger qualsiasi ulteriore elaborazione del file hello.

10. Una volta processo hello è stato attivato, è possibile aggiungere hello seguente processo hello tootrack di codice per il completamento.

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


## <a name="next-steps"></a>Passaggi successivi

[Utilizzare i dati di interfaccia utente di gestione dati di StorSimple tootransform](storsimple-data-manager-ui.md).
