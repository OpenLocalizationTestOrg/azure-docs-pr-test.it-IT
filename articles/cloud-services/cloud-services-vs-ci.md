---
title: recapito aaaContinuous per cloud services con Visual Studio Online | Documenti Microsoft
description: Informazioni su come App tooset le opzioni di distribuzione continua per Azure cloud senza salvare i file di configurazione del servizio di archiviazione chiave toohello di diagnostica
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
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a><span data-ttu-id="cd1cc-103">Securely salvare servizi diagnostica chiave di archiviazione Cloud e di integrazione continua l'installazione e distribuzione tooAzure utilizzando Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="cd1cc-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment tooAzure using Visual Studio Online</span></span>
 <span data-ttu-id="cd1cc-104">Oggi è un progetto di origine tooopen pratica comune.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-104">It is a common practice tooopen source projects nowadays.</span></span> <span data-ttu-id="cd1cc-105">Il salvataggio dei segreti dell'applicazione nei file di configurazione non è più considerato sicuro, perché comporta l'esposizione di vulnerabilità della sicurezza a causa della diffusione dei segreti dai controlli di origine pubblica.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="cd1cc-106">Risorse nell'ambiente Cloud hello archiviazione segreto come testo normale in un file in una pipeline di integrazione continua non è sicuro uno poiché il server di compilazione, potrebbero essere condivise.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on hello Cloud environment.</span></span> <span data-ttu-id="cd1cc-107">In questo articolo viene illustrato come Visual Studio e Visual Studio Online, è possibile ridurre i problemi di sicurezza hello durante lo sviluppo e il processo di integrazione continua.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-107">This article explains how Visual Studio and Visual Studio Online mitigates hello security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="cd1cc-108">Rimuovere il segreto della chiave di archiviazione di diagnostica dal file di configurazione del progetto</span><span class="sxs-lookup"><span data-stu-id="cd1cc-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="cd1cc-109">L'estensione di diagnostica dei Servizi cloud richiede l'Archiviazione di Azure per il salvataggio dei risultati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="cd1cc-110">In precedenza stringa di connessione di archiviazione hello è specificata nei file di configurazione (. cscfg) di servizi Cloud hello e può essere selezionato nel controllo toosource.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-110">Formerly hello storage connection string is specified in hello Cloud Services configuration (.cscfg) files and could be checked in toosource control.</span></span> <span data-ttu-id="cd1cc-111">Nella versione più recente di Azure SDK hello archivio tooonly di comportamento hello una parziale stringa di connessione con la chiave di hello sostituito da un token è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-111">In hello latest Azure SDK release we changed hello behavior tooonly store a partial connection string with hello key replaced by a token.</span></span> <span data-ttu-id="cd1cc-112">Hello alla procedura seguente viene descritto il funzionamento degli strumenti di servizi Cloud nuovo hello:</span><span class="sxs-lookup"><span data-stu-id="cd1cc-112">hello following steps describe how hello new Cloud Services tooling works:</span></span>

### <a name="1-open-hello-role-designer"></a><span data-ttu-id="cd1cc-113">1. Aprire Progettazione ruoli hello</span><span class="sxs-lookup"><span data-stu-id="cd1cc-113">1. Open hello Role designer</span></span>
* <span data-ttu-id="cd1cc-114">Fare doppio clic oppure fare clic con il pulsante destro su una finestra di progettazione ruoli di tooopen ruolo di servizi Cloud</span><span class="sxs-lookup"><span data-stu-id="cd1cc-114">Double click or right click on a Cloud Services role tooopen Role designer</span></span>

![Aprire la finestra di progettazione dei ruoli][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="cd1cc-116">2. Nella sezione relativa alla diagnostica è stata aggiunta una nuova casella di controllo "Non rimuovere il segreto della chiave di archiviazione dal file di configurazione del progetto (.cscfg)"</span><span class="sxs-lookup"><span data-stu-id="cd1cc-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="cd1cc-117">Se si utilizza l'emulatore di archiviazione locale di hello, questa casella di controllo è disabilitata perché non esiste alcun toomanage secret hello locale stringa di connessione, ovvero UseDevelopmentStorage = true.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-117">If you are using hello local storage emulator, this checkbox is disabled because there is no secret toomanage for hello local connection string, which is UseDevelopmentStorage=true.</span></span>

![La stringa di connessione dell'emulatore di archiviazione locale non è segreta][1]

* <span data-ttu-id="cd1cc-119">Se si crea un nuovo progetto, questa casella di controllo è deselezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="cd1cc-120">Di conseguenza, nella sezione chiave hello di archiviazione della stringa di connessione di archiviazione hello selezionato verrà sostituito con un token.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-120">This results in hello storage key section of hello selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="cd1cc-121">Hello valore del token hello verrà trovato nella cartella AppData Roaming dell'utente corrente hello, ad esempio: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="cd1cc-121">hello value of hello token will be found under hello current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="cd1cc-122">Si noti cartella user\AppData hello è l'accesso controllato dall'account utente e viene considerato segreti di sviluppo toostore un posto sicuro.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-122">Note that hello user\AppData folder is Access Controlled by user sign-in and is considered a secure place toostore development secrets.</span></span>
> 
> 

![La chiave di archiviazione viene salvata nella cartella del profilo utente][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="cd1cc-124">3. Selezionare un account di archiviazione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="cd1cc-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="cd1cc-125">Selezionare un account di archiviazione dalla finestra di dialogo hello avviata facendo hello "..."</span><span class="sxs-lookup"><span data-stu-id="cd1cc-125">Select a storage account from hello dialog launched by clicking hello “…”</span></span> <span data-ttu-id="cd1cc-126">.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-126">button.</span></span> <span data-ttu-id="cd1cc-127">Si noti come stringa di connessione di archiviazione hello generato avrà non chiave dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-127">Notice how hello storage connection string generated will not have hello storage account key.</span></span>
* <span data-ttu-id="cd1cc-128">Ad esempio: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="cd1cc-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-hello-project"></a><span data-ttu-id="cd1cc-129">4.    Debug di hello progetto</span><span class="sxs-lookup"><span data-stu-id="cd1cc-129">4.    Debugging hello project</span></span>
* <span data-ttu-id="cd1cc-130">F5 toostart debug in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-130">F5 toostart debugging in Visual Studio.</span></span> <span data-ttu-id="cd1cc-131">Tutto dovrebbe funzionare in hello stesso modo come prima.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-131">Everything should work in hello same way as before.</span></span>
  <span data-ttu-id="cd1cc-132">![Avviare il debug localmente][3]</span><span class="sxs-lookup"><span data-stu-id="cd1cc-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="cd1cc-133">5. Pubblicare il progetto da Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cd1cc-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="cd1cc-134">Avvio hello finestra di dialogo pubblicazione e procedere con le istruzioni Accedi toopublish hello applicaion tooAzure.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-134">Launch hello publish dialog and proceed with sign-in instructions toopublish hello applicaion tooAzure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="cd1cc-135">6. Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cd1cc-135">6. Additional information</span></span>
> <span data-ttu-id="cd1cc-136">Nota: il pannello impostazioni hello in Progettazione ruoli hello viene mantenuta come nel caso di ora.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-136">Note: hello Settings panel in hello role designer will stay as it is for now.</span></span> <span data-ttu-id="cd1cc-137">Se si desidera che la funzionalità di gestione di informazioni segrete hello toouse per la diagnostica, passare scheda configurazioni toohello.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-137">If you want toouse hello secret management feature for diagnostics, go toohello Configurations tab.</span></span>
> 
> 

![Aggiungere le impostazioni][4]

> <span data-ttu-id="cd1cc-139">Nota: Se abilitato, la chiave di Application Insights hello verrà archiviata come testo normale.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-139">Note: If enabled, hello Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="cd1cc-140">chiave di Hello viene utilizzata solo per caricare contenuto in modo che non contiene dati sensibili sia a rischio di compromissione.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-140">hello key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="cd1cc-141">Compilare e pubblicare un progetto di Servizi cloud usando i modelli di attività di Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="cd1cc-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="cd1cc-142">Hello alla procedura seguente viene illustrato come integrazione continua per i servizi Cloud toosetup progetto utilizzando l'attività di Visual Studio online:</span><span class="sxs-lookup"><span data-stu-id="cd1cc-142">hello following steps illustrates how toosetup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="cd1cc-143">1.    Ottenere un account VSO</span><span class="sxs-lookup"><span data-stu-id="cd1cc-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="cd1cc-144">[Creare account di Visual Studio Online] [ Create Visual Studio Online account] se non hai già</span><span class="sxs-lookup"><span data-stu-id="cd1cc-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="cd1cc-145">[Creazione del progetto team] [ Create team project] nell'account Visual Studio online</span><span class="sxs-lookup"><span data-stu-id="cd1cc-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="cd1cc-146">2.    Configurare il controllo del codice sorgente in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cd1cc-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="cd1cc-147">Connettere il progetto di team tooa</span><span class="sxs-lookup"><span data-stu-id="cd1cc-147">Connect tooa team project</span></span>

![Connettere il progetto tooteam][5]

![Selezionare tooconnect progetto team a][6]

* <span data-ttu-id="cd1cc-150">Aggiungere il controllo toosource progetto</span><span class="sxs-lookup"><span data-stu-id="cd1cc-150">Add your project toosource control</span></span>

![Aggiungere il controllo toosource progetto][7]

![Cartella del codice sorgente di mappa progetto tooa][8]

* <span data-ttu-id="cd1cc-153">Archiviare il progetto da Team Explorer</span><span class="sxs-lookup"><span data-stu-id="cd1cc-153">Check in your project from Team Explorer</span></span>

![Controllare nel controllo toosource progetto][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="cd1cc-155">3.    Configurare il processo di configurazione</span><span class="sxs-lookup"><span data-stu-id="cd1cc-155">3.    Configure Build process</span></span>
* <span data-ttu-id="cd1cc-156">Progetto team tooyour di individuare e aggiungere un nuovo processo di compilazione di modelli</span><span class="sxs-lookup"><span data-stu-id="cd1cc-156">Browse tooyour team project and add a new build process Templates</span></span>

![Aggiungere una nuova compilazione][10]

* <span data-ttu-id="cd1cc-158">Selezionare un'attività di compilazione</span><span class="sxs-lookup"><span data-stu-id="cd1cc-158">Select build task</span></span>

![Aggiungere un'attività di compilazione][11]

![Selezionare il modello di attività di compilazione di Visual Studio][12]

* <span data-ttu-id="cd1cc-161">Modificare l'input dell'attività di compilazione.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-161">Edit build task input.</span></span> <span data-ttu-id="cd1cc-162">Personalizzare compilazione hello parametri in base tooyour</span><span class="sxs-lookup"><span data-stu-id="cd1cc-162">Please customize hello build parameters according tooyour need</span></span>

![Configurare l'attività di compilazione][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="cd1cc-164">Configurare le variabili di compilazione</span><span class="sxs-lookup"><span data-stu-id="cd1cc-164">Configure build variables</span></span>

![Configurare le variabili di compilazione][14]

* <span data-ttu-id="cd1cc-166">Aggiungere una destinazione della compilazione tooupload di attività</span><span class="sxs-lookup"><span data-stu-id="cd1cc-166">Add a task tooupload build drop</span></span>

![Scegliere l'attività di pubblicazione della destinazione finale della compilazione][15]

![Configurare l'attività di pubblicazione della destinazione finale della compilazione][16]

* <span data-ttu-id="cd1cc-169">Eseguire la compilazione hello</span><span class="sxs-lookup"><span data-stu-id="cd1cc-169">Run hello build</span></span>

![Accodare la nuova compilazione][17]

![Visualizzare il riepilogo della compilazione][18]

* <span data-ttu-id="cd1cc-172">Se hello compilazione viene completata correttamente verrà visualizzato un toobelow simile risultato</span><span class="sxs-lookup"><span data-stu-id="cd1cc-172">if hello build is successful you will see a result similar toobelow</span></span>

![Risultato della compilazione][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="cd1cc-174">4.    Configurare il processo di rilascio</span><span class="sxs-lookup"><span data-stu-id="cd1cc-174">4.    Configure Release process</span></span>
* <span data-ttu-id="cd1cc-175">Creare una nuova versione</span><span class="sxs-lookup"><span data-stu-id="cd1cc-175">Create a new release</span></span>

![Creare una nuova versione][20]

* <span data-ttu-id="cd1cc-177">Selezionare l'attività di distribuzione di servizi Cloud di Azure hello</span><span class="sxs-lookup"><span data-stu-id="cd1cc-177">Select hello Azure Cloud Services Deployment task</span></span>

![Selezionare l'attività di distribuzione dei Servizi cloud di Azure][21]

* <span data-ttu-id="cd1cc-179">Come chiave dell'account di archiviazione hello non è selezionata nel controllo toosource, una chiave privata toospecify hello è necessario per l'impostazione delle estensioni di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-179">As hello storage account key is not checked in toosource control, we need toospecify hello secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="cd1cc-180">Espandere hello **opzioni avanzate per la creazione di un nuovo servizio** sezione e modificare hello **chiavi dell'Account di archiviazione diagnostica** input del parametro.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-180">Expand hello **Advanced Options for Creating New Service** section and edit hello **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="cd1cc-181">Accetta l'input in più righe di una coppia chiave-valore nel formato hello **[RoleName]:$(StorageAccountKey)**</span><span class="sxs-lookup"><span data-stu-id="cd1cc-181">This input takes in multiple lines of key value pair in hello format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="cd1cc-182">Nota: se i dati di diagnostica in account di archiviazione hello stessa sottoscrizione in cui verrà pubblicata l'applicazione di servizi Cloud hello, non si dispone tooenter hello chiave nell'input di attività di distribuzione hello; distribuzione Hello a livello di codice ottiene informazioni sull'archiviazione hello dalla sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="cd1cc-182">Note: if your diagnostics storage account is under hello same subscription as where you will publish hello Cloud Services application, you don't have tooenter hello key in hello deployment task input; hello deployment will programmatically obtain hello storage information from your subscription</span></span>
> 
> 

![Configurare l'attività di distribuzione dei Servizi cloud di Azure][22]

* <span data-ttu-id="cd1cc-184">Segreto utilizzare compilazione variabili toosave chiavi per l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="cd1cc-184">Use secret build variables toosave storage Keys.</span></span> <span data-ttu-id="cd1cc-185">una variabile come segreto fare clic sull'icona di blocco hello sul lato destro hello di hello toomask variabili di input</span><span class="sxs-lookup"><span data-stu-id="cd1cc-185">toomask a variable as secret click on hello lock icon on hello right side of hello Variables input</span></span>

![Salvare le chiavi di archiviazione nelle variabili di compilazione del segreto][23]

* <span data-ttu-id="cd1cc-187">Creare una versione e distribuire il progetto tooAzure</span><span class="sxs-lookup"><span data-stu-id="cd1cc-187">Create a release and deploy your project tooAzure</span></span>

![Creare una nuova versione][24]

## <a name="next-steps"></a><span data-ttu-id="cd1cc-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cd1cc-189">Next steps</span></span>
<span data-ttu-id="cd1cc-190">toolearn più sull'impostazione di estensioni di diagnostica per i servizi Cloud di Azure, vedere [abilitare la diagnostica nei servizi Cloud di Azure tramite PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="cd1cc-190">toolearn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

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
