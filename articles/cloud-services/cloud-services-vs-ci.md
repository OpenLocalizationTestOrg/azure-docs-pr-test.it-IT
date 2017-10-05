---
title: Recapito continuo per i Servizi cloud con Visual Studio Online | Documentazione Microsoft
description: Informazioni su come configurare il recapito continuo per app cloud di Azure senza salvare la chiave di archiviazione di diagnostica nei file di configurazione del servizio
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 7e70f92d4d1333ca6cbac5876e5ccbc763bd915c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-to-azure-using-visual-studio-online"></a><span data-ttu-id="aab93-103">Salvare in modo sicuro la chiave di archiviazione di diagnostica dei Servizi cloud e configurare l'integrazione e la distribuzione continue in Azure usando Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="aab93-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment to Azure using Visual Studio Online</span></span>
 <span data-ttu-id="aab93-104">L'uso di progetti open source è attualmente molto diffuso.</span><span class="sxs-lookup"><span data-stu-id="aab93-104">It is a common practice to open source projects nowadays.</span></span> <span data-ttu-id="aab93-105">Il salvataggio dei segreti dell'applicazione nei file di configurazione non è più considerato sicuro, perché comporta l'esposizione di vulnerabilità della sicurezza a causa della diffusione dei segreti dai controlli di origine pubblica.</span><span class="sxs-lookup"><span data-stu-id="aab93-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="aab93-106">L'archiviazione del segreto come testo normale in un file in una pipeline di integrazione continua non risulta sicura, perché i server di compilazione potrebbero essere risorse condivise nell'ambiente cloud.</span><span class="sxs-lookup"><span data-stu-id="aab93-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on the Cloud environment.</span></span> <span data-ttu-id="aab93-107">Questo articolo illustra il modo in cui Visual Studio e Visual Studio Online consentono di ridurre i problemi di sicurezza durante il processo di sviluppo e di integrazione continua.</span><span class="sxs-lookup"><span data-stu-id="aab93-107">This article explains how Visual Studio and Visual Studio Online mitigates the security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="aab93-108">Rimuovere il segreto della chiave di archiviazione di diagnostica dal file di configurazione del progetto</span><span class="sxs-lookup"><span data-stu-id="aab93-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="aab93-109">L'estensione di diagnostica dei Servizi cloud richiede l'Archiviazione di Azure per il salvataggio dei risultati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="aab93-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="aab93-110">La stringa di connessione di archiviazione veniva in precedenza specificata nei file di configurazione dei Servizi cloud (con estensione cscfg) e poteva essere archiviata nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="aab93-110">Formerly the storage connection string is specified in the Cloud Services configuration (.cscfg) files and could be checked in to source control.</span></span> <span data-ttu-id="aab93-111">Nella versione più recente di Azure SDK il comportamento è stato modificato, in modo che venga archiviata solo una stringa di connessione parziale e che la chiave venga sostituita da un token.</span><span class="sxs-lookup"><span data-stu-id="aab93-111">In the latest Azure SDK release we changed the behavior to only store a partial connection string with the key replaced by a token.</span></span> <span data-ttu-id="aab93-112">La procedura seguente illustra il funzionamento dei nuovi strumenti dei Servizi cloud:</span><span class="sxs-lookup"><span data-stu-id="aab93-112">The following steps describe how the new Cloud Services tooling works:</span></span>

### <a name="1-open-the-role-designer"></a><span data-ttu-id="aab93-113">1. Aprire la finestra di progettazione dei ruoli</span><span class="sxs-lookup"><span data-stu-id="aab93-113">1. Open the Role designer</span></span>
* <span data-ttu-id="aab93-114">Fare doppio clic o fare clic con il pulsante destro del mouse su un ruolo dei Servizi cloud per aprire la finestra di progettazione dei ruoli</span><span class="sxs-lookup"><span data-stu-id="aab93-114">Double click or right click on a Cloud Services role to open Role designer</span></span>

![Aprire la finestra di progettazione dei ruoli][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="aab93-116">2. Nella sezione relativa alla diagnostica è stata aggiunta una nuova casella di controllo "Non rimuovere il segreto della chiave di archiviazione dal file di configurazione del progetto (.cscfg)"</span><span class="sxs-lookup"><span data-stu-id="aab93-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="aab93-117">Se si usa l'emulatore di archiviazione locale, questa casella di controllo è disabilitata perché non sono presenti segreti da gestire per la stringa di connessione locale, ovvero UseDevelopmentStorage=true.</span><span class="sxs-lookup"><span data-stu-id="aab93-117">If you are using the local storage emulator, this checkbox is disabled because there is no secret to manage for the local connection string, which is UseDevelopmentStorage=true.</span></span>

![La stringa di connessione dell'emulatore di archiviazione locale non è segreta][1]

* <span data-ttu-id="aab93-119">Se si crea un nuovo progetto, questa casella di controllo è deselezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="aab93-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="aab93-120">La sezione relativa alla chiave di archiviazione della stringa di connessione selezionata viene quindi sostituita da un token.</span><span class="sxs-lookup"><span data-stu-id="aab93-120">This results in the storage key section of the selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="aab93-121">Il valore del token sarà disponibile nella cartella AppData\Roaming dell'utente corrente, ad esempio: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="aab93-121">The value of the token will be found under the current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="aab93-122">Si noti che l'accesso alla cartella user\AppData è controllato tramite gli accessi utente e la cartella viene considerata una posizione sicura per l'archiviazione dei segreti di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="aab93-122">Note that the user\AppData folder is Access Controlled by user sign-in and is considered a secure place to store development secrets.</span></span>
> 
> 

![La chiave di archiviazione viene salvata nella cartella del profilo utente][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="aab93-124">3. Selezionare un account di archiviazione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="aab93-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="aab93-125">Selezionare un account di archiviazione dalla finestra di dialogo visualizzata quando si fa clic sui puntini di sospensione "…"</span><span class="sxs-lookup"><span data-stu-id="aab93-125">Select a storage account from the dialog launched by clicking the “…”</span></span> <span data-ttu-id="aab93-126">.</span><span class="sxs-lookup"><span data-stu-id="aab93-126">button.</span></span> <span data-ttu-id="aab93-127">Si noti che la stringa di connessione di archiviazione generata non avrà la chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="aab93-127">Notice how the storage connection string generated will not have the storage account key.</span></span>
* <span data-ttu-id="aab93-128">Ad esempio: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="aab93-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-the-project"></a><span data-ttu-id="aab93-129">4.    Debug del progetto</span><span class="sxs-lookup"><span data-stu-id="aab93-129">4.    Debugging the project</span></span>
* <span data-ttu-id="aab93-130">Premere F5 per avviare il debug in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aab93-130">F5 to start debugging in Visual Studio.</span></span> <span data-ttu-id="aab93-131">Non sono state apportate modifiche rispetto al comportamento precedente.</span><span class="sxs-lookup"><span data-stu-id="aab93-131">Everything should work in the same way as before.</span></span>
  <span data-ttu-id="aab93-132">![Avviare il debug localmente][3]</span><span class="sxs-lookup"><span data-stu-id="aab93-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="aab93-133">5. Pubblicare il progetto da Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aab93-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="aab93-134">Avviare la finestra di dialogo di pubblicazione e seguire le istruzioni di accesso per pubblicare l'applicazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="aab93-134">Launch the publish dialog and proceed with sign-in instructions to publish the applicaion to Azure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="aab93-135">6. Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="aab93-135">6. Additional information</span></span>
> <span data-ttu-id="aab93-136">Nota: il pannello Impostazioni nella finestra di progettazione dei ruoli non viene modificato, per il momento.</span><span class="sxs-lookup"><span data-stu-id="aab93-136">Note: The Settings panel in the role designer will stay as it is for now.</span></span> <span data-ttu-id="aab93-137">Se si vuole usare la funzionalità di gestione dei segreti per la diagnostica, passare alla scheda Configurazioni.</span><span class="sxs-lookup"><span data-stu-id="aab93-137">If you want to use the secret management feature for diagnostics, go to the Configurations tab.</span></span>
> 
> 

![Aggiungere le impostazioni][4]

> <span data-ttu-id="aab93-139">Nota: se abilitata, la chiave di Application Insights verrà archiviata come testo normale.</span><span class="sxs-lookup"><span data-stu-id="aab93-139">Note: If enabled, the Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="aab93-140">La chiave viene usata solo per caricare contenuti, quindi non si correrà alcun rischio di compromissione di dati sensibili.</span><span class="sxs-lookup"><span data-stu-id="aab93-140">The key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="aab93-141">Compilare e pubblicare un progetto di Servizi cloud usando i modelli di attività di Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="aab93-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="aab93-142">La procedura seguente illustra come configurare l'integrazione continua per un progetto di Servizi cloud usando le attività di Visual Studio Online:</span><span class="sxs-lookup"><span data-stu-id="aab93-142">The following steps illustrates how to setup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="aab93-143">1.    Ottenere un account VSO</span><span class="sxs-lookup"><span data-stu-id="aab93-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="aab93-144">[Creare account di Visual Studio Online] [ Create Visual Studio Online account] se non hai già</span><span class="sxs-lookup"><span data-stu-id="aab93-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="aab93-145">[Creazione del progetto team] [ Create team project] nell'account Visual Studio online</span><span class="sxs-lookup"><span data-stu-id="aab93-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="aab93-146">2.    Configurare il controllo del codice sorgente in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aab93-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="aab93-147">Connettersi a un progetto team</span><span class="sxs-lookup"><span data-stu-id="aab93-147">Connect to a team project</span></span>

![Connettersi a un progetto team][5]

![Selezionare il progetto team a cui connettersi][6]

* <span data-ttu-id="aab93-150">Aggiungere il progetto al controllo del codice sorgente</span><span class="sxs-lookup"><span data-stu-id="aab93-150">Add your project to source control</span></span>

![Aggiungere il progetto al controllo del codice sorgente][7]

![Eseguire il mapping del progetto a una cartella del controllo del codice sorgente][8]

* <span data-ttu-id="aab93-153">Archiviare il progetto da Team Explorer</span><span class="sxs-lookup"><span data-stu-id="aab93-153">Check in your project from Team Explorer</span></span>

![Archiviare il progetto nel controllo del codice sorgente][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="aab93-155">3.    Configurare il processo di configurazione</span><span class="sxs-lookup"><span data-stu-id="aab93-155">3.    Configure Build process</span></span>
* <span data-ttu-id="aab93-156">Passare al progetto team e aggiungere un nuovo processo di compilazione ai modelli</span><span class="sxs-lookup"><span data-stu-id="aab93-156">Browse to your team project and add a new build process Templates</span></span>

![Aggiungere una nuova compilazione][10]

* <span data-ttu-id="aab93-158">Selezionare un'attività di compilazione</span><span class="sxs-lookup"><span data-stu-id="aab93-158">Select build task</span></span>

![Aggiungere un'attività di compilazione][11]

![Selezionare il modello di attività di compilazione di Visual Studio][12]

* <span data-ttu-id="aab93-161">Modificare l'input dell'attività di compilazione.</span><span class="sxs-lookup"><span data-stu-id="aab93-161">Edit build task input.</span></span> <span data-ttu-id="aab93-162">Personalizzare i parametri di compilazione in base alle esigenze specifiche</span><span class="sxs-lookup"><span data-stu-id="aab93-162">Please customize the build parameters according to your need</span></span>

![Configurare l'attività di compilazione][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="aab93-164">Configurare le variabili di compilazione</span><span class="sxs-lookup"><span data-stu-id="aab93-164">Configure build variables</span></span>

![Configurare le variabili di compilazione][14]

* <span data-ttu-id="aab93-166">Aggiungere un'attività per caricare la destinazione finale della compilazione</span><span class="sxs-lookup"><span data-stu-id="aab93-166">Add a task to upload build drop</span></span>

![Scegliere l'attività di pubblicazione della destinazione finale della compilazione][15]

![Configurare l'attività di pubblicazione della destinazione finale della compilazione][16]

* <span data-ttu-id="aab93-169">Eseguire la compilazione</span><span class="sxs-lookup"><span data-stu-id="aab93-169">Run the build</span></span>

![Accodare la nuova compilazione][17]

![Visualizzare il riepilogo della compilazione][18]

* <span data-ttu-id="aab93-172">se la compilazione viene completata correttamente, verrà visualizzato un risultato simile a questo</span><span class="sxs-lookup"><span data-stu-id="aab93-172">if the build is successful you will see a result similar to below</span></span>

![Risultato della compilazione][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="aab93-174">4.    Configurare il processo di rilascio</span><span class="sxs-lookup"><span data-stu-id="aab93-174">4.    Configure Release process</span></span>
* <span data-ttu-id="aab93-175">Creare una nuova versione</span><span class="sxs-lookup"><span data-stu-id="aab93-175">Create a new release</span></span>

![Creare una nuova versione][20]

* <span data-ttu-id="aab93-177">Selezionare l'attività di distribuzione dei Servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="aab93-177">Select the Azure Cloud Services Deployment task</span></span>

![Selezionare l'attività di distribuzione dei Servizi cloud di Azure][21]

* <span data-ttu-id="aab93-179">Poiché la chiave dell'account di archiviazione non viene archiviata nel controllo del codice sorgente,è necessario specificare la chiave privata per la configurazione delle estensioni di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="aab93-179">As the storage account key is not checked in to source control, we need to specify the secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="aab93-180">Espandere la sezione **Opzioni avanzate per la creazione del nuovo servizio** e modificare l'input del parametro **Chiavi dell'account di archiviazione di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="aab93-180">Expand the **Advanced Options for Creating New Service** section and edit the **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="aab93-181">L'input accetta più righe della coppia chiave-valore con formato **[NomeRuolo]:$(ChiaveAccountArchiviazione)**</span><span class="sxs-lookup"><span data-stu-id="aab93-181">This input takes in multiple lines of key value pair in the format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="aab93-182">Nota: se l'account di archiviazione di diagnostica si trova nella stessa sottoscrizione in cui verrà pubblicata l'applicazione di Servizi cloud, non è necessario immettere la chiave nell'input dell'attività di distribuzione. La distribuzione otterrà le informazioni di archiviazione a livello di codice dalla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="aab93-182">Note: if your diagnostics storage account is under the same subscription as where you will publish the Cloud Services application, you don't have to enter the key in the deployment task input; the deployment will programmatically obtain the storage information from your subscription</span></span>
> 
> 

![Configurare l'attività di distribuzione dei Servizi cloud di Azure][22]

* <span data-ttu-id="aab93-184">Usare le variabili di compilazione del segreto per salvare le chiavi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="aab93-184">Use secret build variables to save storage Keys.</span></span> <span data-ttu-id="aab93-185">Per mascherare una variabile come segreto, fare clic sull'icona a forma di lucchetto a destra dell'input Variabili</span><span class="sxs-lookup"><span data-stu-id="aab93-185">To mask a variable as secret click on the lock icon on the right side of the Variables input</span></span>

![Salvare le chiavi di archiviazione nelle variabili di compilazione del segreto][23]

* <span data-ttu-id="aab93-187">Creare una versione e distribuire il progetto in Azure</span><span class="sxs-lookup"><span data-stu-id="aab93-187">Create a release and deploy your project to Azure</span></span>

![Creare una nuova versione][24]

## <a name="next-steps"></a><span data-ttu-id="aab93-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aab93-189">Next steps</span></span>
<span data-ttu-id="aab93-190">Per ulteriori informazioni sull'impostazione delle estensioni di diagnostica per servizi Cloud di Azure, vedere [abilitare la diagnostica nei servizi Cloud di Azure tramite PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="aab93-190">To learn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
