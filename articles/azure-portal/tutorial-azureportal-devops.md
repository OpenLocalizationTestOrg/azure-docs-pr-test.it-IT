---
title: 'Esercitazione: DevOps con hello portale di Azure | Documenti Microsoft'
description: Informazioni su hello vari flussi di lavoro di DevOps in hello portale di Azure.
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a><span data-ttu-id="2d065-103">Esercitazione: DevOps con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2d065-103">Tutorial: DevOps with hello Azure Portal</span></span>
<span data-ttu-id="2d065-104">piattaforma Azure Hello è piena di flussi di lavoro DevOps flessibile.</span><span class="sxs-lookup"><span data-stu-id="2d065-104">hello Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="2d065-105">In questa esercitazione illustrato come funzionalità hello tooleverage di hello Azure Portal toodevelop, testare, distribuire, risolvere i problemi, monitorare e gestire applicazioni in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2d065-105">In this tutorial, you learn how tooleverage hello capabilities of hello Azure Portal toodevelop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="2d065-106">In questa esercitazione è incentrata sulla seguente hello:</span><span class="sxs-lookup"><span data-stu-id="2d065-106">This tutorial focuses on hello following:</span></span>

1. <span data-ttu-id="2d065-107">Creazione di un'app Web e abilitazione della distribuzione continua</span><span class="sxs-lookup"><span data-stu-id="2d065-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="2d065-108">Sviluppare e testare un'app</span><span class="sxs-lookup"><span data-stu-id="2d065-108">Develop and test an app</span></span>
3. <span data-ttu-id="2d065-109">Monitoraggio e risoluzione dei problemi di un'app</span><span class="sxs-lookup"><span data-stu-id="2d065-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="2d065-110">Attività di gestione di applicazioni generali</span><span class="sxs-lookup"><span data-stu-id="2d065-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="2d065-111">Creazione di un'app Web e abilitazione della distribuzione continua</span><span class="sxs-lookup"><span data-stu-id="2d065-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="2d065-112">Creare un'app Web con [Azure App Service](https://azure.microsoft.com/services/app-service/), che verranno usati nel resto di hello dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2d065-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in hello rest of this tutorial.</span></span> <span data-ttu-id="2d065-113">All'inizio si abiliterà la distribuzione continua dal repository di codice sorgente all'ambiente di Azure in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2d065-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="2d065-114">Accedere al portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="2d065-114">Sign into hello Azure Portal</span></span>
2. <span data-ttu-id="2d065-115">Scegliere **servizi App** &gt; **sull'icona Aggiungi** e immettere un nome, scegliere la sottoscrizione e creare un nuovo tooserve gruppo di risorse come contenitore hello per servizio hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group tooserve as hello container for hello service.</span></span>
   
   <span data-ttu-id="2d065-116">Gruppi di risorse consentono di toomanage vari aspetti della soluzione di hello, ad esempio fatturazione, distribuzioni e il monitoraggio come un singolo gruppo tramite [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2d065-116">Resource groups allow you toomanage various aspects of hello solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![Immagine1][image1]
3. <span data-ttu-id="2d065-118">Dopo pochi secondi, verrà creato il servizio app.</span><span class="sxs-lookup"><span data-stu-id="2d065-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="2d065-119">Richiedere hello di tooexplore pochi minuti diverse opzioni di menu per il servizio hello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-119">Take a few minutes tooexplore hello various menu options for hello service in hello portal.</span></span>
   
   ![Immagine2][image2]    
4. <span data-ttu-id="2d065-121">Fare clic su URL hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-121">Click hello URL.</span></span> <span data-ttu-id="2d065-122">Si noti diversi hello scelte disponibili per gli strumenti e repository.</span><span class="sxs-lookup"><span data-stu-id="2d065-122">Notice hello variety of available choices for tools and repositories.</span></span> <span data-ttu-id="2d065-123">È inoltre possibile utilizzare linguaggi hello e altri framework di propria scelta, tra cui .NET, Java e Ruby.</span><span class="sxs-lookup"><span data-stu-id="2d065-123">You can also use hello languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![Immagine3][image3]    
5. <span data-ttu-id="2d065-125">Hello portale di Azure effettua la distribuzione continua di un processo semplice che include solo pochi semplici passaggi.</span><span class="sxs-lookup"><span data-stu-id="2d065-125">hello Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="2d065-126">Nel portale di Azure hello, scegliere impostazioni dall'icona hello per il servizio app di hello che appena creato.</span><span class="sxs-lookup"><span data-stu-id="2d065-126">In hello Azure portal, choose settings from hello icon for hello app service you just created.</span></span>
   
   ![Immagine4][image4]
   
   <span data-ttu-id="2d065-128">Dal pannello hello che verrà visualizzato a destra di hello, scorrere toohello la pubblicazione di sezione.</span><span class="sxs-lookup"><span data-stu-id="2d065-128">From hello blade that opens on hello right, scroll toohello publishing section.</span></span>
   
   ![Immagine5][image5]
6. <span data-ttu-id="2d065-130">A questo punto, configurare alcune impostazioni tooenable la distribuzione continua per app hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-130">Next, configure some settings tooenable continuous deployment for hello app.</span></span> <span data-ttu-id="2d065-131">Fare clic su Origine distribuzione e quindi su Scegliere l'origine.</span><span class="sxs-lookup"><span data-stu-id="2d065-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="2d065-132">Si noti diversi hello opzioni che disponibili per le origini dei repository.</span><span class="sxs-lookup"><span data-stu-id="2d065-132">Notice hello variety of options you have for repository sources.</span></span>
   
   ![Immagine6][image6]
7. <span data-ttu-id="2d065-134">Per questo esempio scegliere GitHub.</span><span class="sxs-lookup"><span data-stu-id="2d065-134">For this example choose GitHub.</span></span> <span data-ttu-id="2d065-135">Facoltativamente, scegliere repository hello scelto dall'utente e credenziali di autorizzazione hello del programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="2d065-135">Optionally choose hello repository of your choice and setup hello authorization credentials.</span></span>
   
   ![Immagine7][image7]
8. <span data-ttu-id="2d065-137">Dopo aver repository tooyour di autorizzazione, è possibile scegliere un progetto e il ramo desiderato toodeploy.</span><span class="sxs-lookup"><span data-stu-id="2d065-137">After authorization tooyour repository, you can then choose a project and branch you wish toodeploy.</span></span> <span data-ttu-id="2d065-138">Sotto sono elencati diversi esempi fittizi.</span><span class="sxs-lookup"><span data-stu-id="2d065-138">There are several fictitious sample examples listed below.</span></span>
   
   ![Immagine8][image8]
9. <span data-ttu-id="2d065-140">Dopo avere scelto il progetto e il ramo, fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="2d065-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="2d065-141">È consigliabile iniziare toosee notifiche di una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="2d065-141">You should start toosee notifications of a deployment.</span></span>
   
   ![Immagine9][image9]
10. <span data-ttu-id="2d065-143">Spostarsi indietro tooGitHub toosee hello webhook che è stato creato un repository di controllo origine hello toointegrate con Azure.</span><span class="sxs-lookup"><span data-stu-id="2d065-143">Navigate back tooGitHub toosee hello webhook that was created toointegrate hello source control repo with Azure.</span></span> <span data-ttu-id="2d065-144">Hello portale di Azure consente l'integrazione con GitHub con solo pochi semplici passaggi.</span><span class="sxs-lookup"><span data-stu-id="2d065-144">hello Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![Immagine10][image10]
11. <span data-ttu-id="2d065-146">toodemonstrate la distribuzione continua, si aggiungere rapidamente alcuni repository toohello contenuto.</span><span class="sxs-lookup"><span data-stu-id="2d065-146">toodemonstrate continuous deployment, you quickly add some content toohello repository.</span></span> <span data-ttu-id="2d065-147">Per un esempio semplice, aggiungere un repository GitHub di tooa file di testo di esempio.</span><span class="sxs-lookup"><span data-stu-id="2d065-147">For a simple example, add a sample text file tooa GitHub repo.</span></span> <span data-ttu-id="2d065-148">Si è gratuita toouse .NET, Ruby, Python o un altro tipo di applicazione con il servizio App.</span><span class="sxs-lookup"><span data-stu-id="2d065-148">You are free toouse .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="2d065-149">Ritiene tooadd disponibile un file di testo, repository di toohello applicazione MVC ASP.NET, Java o Ruby di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="2d065-149">Feel free tooadd a text file, ASP.NET MVC, Java, or Ruby application toohello repo of your choice.</span></span>
    
    ![Immagine11][image11]
12. <span data-ttu-id="2d065-151">Dopo il commit del repository tooyour modifiche, viene visualizzato un nuovo avviare la distribuzione nell'area di notifica del portale hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-151">After committing changes tooyour repository, you see a new deployment initiate in hello portal notifications area.</span></span> <span data-ttu-id="2d065-152">Se non visualizzare rapidamente le modifiche apportate dopo il commit tooyour repository, fare clic su Sincronizza.</span><span class="sxs-lookup"><span data-stu-id="2d065-152">Click Sync if you do not quickly see changes after committing tooyour repository.</span></span>
    
    ![Immagine12][image12]
13. <span data-ttu-id="2d065-154">A questo punto, se si tenta di carica la pagina hello per il servizio app di hello, si potrebbe ricevere un errore 403.</span><span class="sxs-lookup"><span data-stu-id="2d065-154">At this point, if you try and load hello page for hello app service, you may receive a 403 error.</span></span> <span data-ttu-id="2d065-155">In questo esempio, è perché non prevede alcuna installazione documento predefinita tipica per la pagina di hello, ad esempio un file htm o default.</span><span class="sxs-lookup"><span data-stu-id="2d065-155">In this example, it is because there is no typical default document setup for hello page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="2d065-156">È possibile risolvere questo problema rapidamente con gli strumenti nel portale di Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-156">You can quickly remedy this with hello tooling in hello Azure Portal.</span></span>  <span data-ttu-id="2d065-157">Nel portale di Azure hello scegliere impostazioni &gt; le impostazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2d065-157">In hello Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![Immagine13][image13]
14. <span data-ttu-id="2d065-159">Viene aperto un pannello per le impostazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2d065-159">A blade opens for application settings.</span></span> <span data-ttu-id="2d065-160">Immettere il nome di hello della pagina di hello "SamplePage.html" e fare clic su Salva.</span><span class="sxs-lookup"><span data-stu-id="2d065-160">Enter hello name of hello page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="2d065-161">Richiedere altre impostazioni di hello di tooexplore pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="2d065-161">Take a few minutes tooexplore hello other settings.</span></span>
    
    ![Immagine14][image14]
15. <span data-ttu-id="2d065-163">Facoltativamente, aggiornare il tooensure URL browser vedrai modifiche hello previsto.</span><span class="sxs-lookup"><span data-stu-id="2d065-163">Optionally refresh your browser URL tooensure you see hello expected changes.</span></span> <span data-ttu-id="2d065-164">In questo caso, è ora la compilazione di pagina hello testo semplice.</span><span class="sxs-lookup"><span data-stu-id="2d065-164">In this case, there is some simple text now populating hello page.</span></span> <span data-ttu-id="2d065-165">Ogni repository toohello ulteriore modifica comporta una nuova distribuzione automatica.</span><span class="sxs-lookup"><span data-stu-id="2d065-165">Each additional change toohello repository would result in a new automatic deployment.</span></span>
    
    ![Immagine15][image15]
    
    <span data-ttu-id="2d065-167">Consente la distribuzione continua con hello portale di Azure è un'esperienza semplice.</span><span class="sxs-lookup"><span data-stu-id="2d065-167">Enabling continuous deployment with hello Azure Portal is an easy experience.</span></span> <span data-ttu-id="2d065-168">È anche possibile compilare pipeline di rilascio più complesse e utilizzare numerose altre tecniche di controllo del codice sorgente esistente e tooAzure toodeploy sistemi di integrazione continua, come l'uso di compilazione automatizzato e i sistemi di gestione di versione.</span><span class="sxs-lookup"><span data-stu-id="2d065-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems toodeploy tooAzure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="2d065-169">Sviluppare e testare un'app</span><span class="sxs-lookup"><span data-stu-id="2d065-169">Develop and test an app</span></span>
<span data-ttu-id="2d065-170">Successivamente, rendere il codice toohello alcune modifiche di base e distribuire rapidamente le modifiche.</span><span class="sxs-lookup"><span data-stu-id="2d065-170">Next, make some changes toohello code base and rapidly deploy those changes.</span></span> <span data-ttu-id="2d065-171">Installerà anche backup di alcuni test delle prestazioni per app Web hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-171">You will also setup up some performance testing for hello Web app.</span></span>

1. <span data-ttu-id="2d065-172">Nel portale di Azure hello scegliere Servizi App dal riquadro di spostamento hello e individuare il servizio App.</span><span class="sxs-lookup"><span data-stu-id="2d065-172">In hello Azure Portal choose App Services from hello navigation pane, and locate your App Service.</span></span>
   
   ![Immagine16][image16]
2. <span data-ttu-id="2d065-174">Fare clic su Strumenti.</span><span class="sxs-lookup"><span data-stu-id="2d065-174">Click Tools</span></span>
   
   ![Immagine17][image17]
3. <span data-ttu-id="2d065-176">Si noti hello categoria in strumenti di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="2d065-176">Notice hello develop category under Tools.</span></span> <span data-ttu-id="2d065-177">Sono disponibili diversi strumenti utili qui che consentono di toowork con App senza uscire hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d065-177">There are several useful tools here that allow us toowork with apps without leaving hello Azure Portal.</span></span> <span data-ttu-id="2d065-178">Fare clic su Console.</span><span class="sxs-lookup"><span data-stu-id="2d065-178">Click on Console.</span></span>
   
   ![Immagine18][image18]
4. <span data-ttu-id="2d065-180">Nella finestra di console hello, è possibile eseguire comandi in tempo reale per l'app.</span><span class="sxs-lookup"><span data-stu-id="2d065-180">In hello console window, you can issue live commands for your app.</span></span> <span data-ttu-id="2d065-181">Tipo hello dir comando e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="2d065-181">Type hello dir command and hit enter.</span></span> <span data-ttu-id="2d065-182">Si noti che i comandi che richiedono privilegi elevati non funzionano.</span><span class="sxs-lookup"><span data-stu-id="2d065-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![Immagine19][image19]
5. <span data-ttu-id="2d065-184">Spostare nuovamente toohello sviluppare categoria e scegliere Visual Studio Online.</span><span class="sxs-lookup"><span data-stu-id="2d065-184">Move back toohello Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="2d065-185">Nota: Visual Studio Online si chiama ora Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="2d065-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![Immagine20][image20]
6. <span data-ttu-id="2d065-187">Attivare l'esperienza di modifica nel browser hello per l'App.</span><span class="sxs-lookup"><span data-stu-id="2d065-187">Toggle on hello in-browser editing experience for your App.</span></span>
   
   ![Immagine21][image21]
7. <span data-ttu-id="2d065-189">Viene installata un'estensione Web per l'app.</span><span class="sxs-lookup"><span data-stu-id="2d065-189">A web extension installs for your app.</span></span> <span data-ttu-id="2d065-190">Estensioni di aggiungono rapidamente e facilmente funzionalità tooapps in Azure.</span><span class="sxs-lookup"><span data-stu-id="2d065-190">Extensions quickly and easily add functionality tooapps in Azure.</span></span> <span data-ttu-id="2d065-191">Si noti alcuni hello altri tipi di estensione disponibili nella schermata di hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="2d065-191">Notice some of hello other extension types available in hello screenshot below.</span></span>
   
   ![Immagine22][image22]
8. <span data-ttu-id="2d065-193">Una volta installato hello estensione Visual Studio Online, fare clic su Vai.</span><span class="sxs-lookup"><span data-stu-id="2d065-193">Once hello Visual Studio Online extension installs, click Go.</span></span>
   
   ![Immagine23][image23]
9. <span data-ttu-id="2d065-195">Verrà visualizzata la in cui si vedere sviluppo IDE direttamente nel browser hello di scheda di un browser.</span><span class="sxs-lookup"><span data-stu-id="2d065-195">A browser tab opens where you see a development IDE directly in hello browser.</span></span> <span data-ttu-id="2d065-196">Esperienza di hello avviso riportato di seguito è in Chrome.</span><span class="sxs-lookup"><span data-stu-id="2d065-196">Notice hello experience below is in Chrome.</span></span>
   
   ![Immagine24][image24]
10. <span data-ttu-id="2d065-198">È possibile eseguire diverse attività, ad esempio i file di modifica, aggiungere file e cartelle e scaricare contenuto dal sito in tempo reale di hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-198">You can perform several activities such as edit files, add files and folders, and download content from hello live site.</span></span> <span data-ttu-id="2d065-199">Apporta una modifica rapida toohello SamplePage.html al file.</span><span class="sxs-lookup"><span data-stu-id="2d065-199">Make a quick edit toohello SamplePage.html file.</span></span>
    
    ![Immagine25][image25]
11. <span data-ttu-id="2d065-201">Tra qualche minuto, hello modifiche vengono salvate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2d065-201">In a few moments, hello changes are automatically saved.</span></span> <span data-ttu-id="2d065-202">Se si passa indietro toohello pagina, è possibile visualizzare le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-202">If you navigate back toohello page, you can see hello changes.</span></span> <span data-ttu-id="2d065-203">Tenere presente che modifiche di questo tipo non sono per lo più adatte agli ambienti di produzione.</span><span class="sxs-lookup"><span data-stu-id="2d065-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="2d065-204">Tuttavia, gli strumenti di hello rendono toomake molto facilmente modifiche rapide per lo sviluppo e ambienti di test.</span><span class="sxs-lookup"><span data-stu-id="2d065-204">However, hello tools make it very easy toomake quick changes for dev and test environments.</span></span>
    
    ![Immagine26][image26]
    
    ![Immagine27][image27]
12. <span data-ttu-id="2d065-207">Spostare nuovamente pannello Strumenti toohello e nella categoria di sviluppare hello, fare clic sul Test delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="2d065-207">Move back toohello tools blade and under hello Develop category, click on Performance Test.</span></span>
    
    ![Immagine28][image28]
13. <span data-ttu-id="2d065-209">È necessario un account di team services tooset.</span><span class="sxs-lookup"><span data-stu-id="2d065-209">You need tooset a team services account.</span></span> <span data-ttu-id="2d065-210">Per altri dettagli, vedere [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span><span class="sxs-lookup"><span data-stu-id="2d065-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="2d065-211">Fare clic su Nuovo toocreate un test delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="2d065-211">Click on New toocreate a performance test.</span></span>
    
    ![Immagine29][image29]
    
    <span data-ttu-id="2d065-213">Configurare hello diversi valori e fare clic su Esegui Test nella parte inferiore di hello della finestra di dialogo di hello tooinitiate un test delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="2d065-213">Configure hello various values and click Run Test at hello bottom of hello dialogue tooinitiate a performance test.</span></span>
    
    ![Immagine30][image30]
    
    ![Immagine31][image31]
15. <span data-ttu-id="2d065-216">Una volta test hello viene avviata l'esecuzione, è possibile monitorare lo stato di hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-216">Once hello test starts running, you can monitor hello state.</span></span>
    
    ![Immagine32][image32]
    
    <span data-ttu-id="2d065-218">Al termine del test di hello, facendo clic sul risultato di hello Mostra ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="2d065-218">Once hello test finishes, clicking on hello result shows more details.</span></span>
    
    ![Immagine33][image33]
16. <span data-ttu-id="2d065-220">In questo esempio è stato creato un piccolo esecuzione dei test, pertanto è tooanalyze limitata dei dati, ma è possibile vedere diverse metriche, nonché eseguire nuovamente il test da questa visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="2d065-220">In this example, you created a small test run, so there is limited data tooanalyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="2d065-221">Hello portale di Azure semplifica la creazione, l'esecuzione e l'analisi di un processo semplice test delle prestazioni web.</span><span class="sxs-lookup"><span data-stu-id="2d065-221">hello Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="2d065-222">Hello schermate riportate di seguito visualizza i dati sulle prestazioni hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-222">hello screenshots below display hello performance data.</span></span>
    
    ![Immagine34][image34]
    
    ![Immagine35][image35]
    
    ![Immagine36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="2d065-226">Monitoraggio e risoluzione dei problemi di un'app</span><span class="sxs-lookup"><span data-stu-id="2d065-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="2d065-227">Azure offre diverse funzionalità per il monitoraggio e la risoluzione dei problemi delle applicazioni in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2d065-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="2d065-228">Scegliere gli strumenti di hello portale di Azure per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="2d065-228">In hello Azure Portal for our Web app choose Tools.</span></span>
   
   ![Immagine37][image37]
2. <span data-ttu-id="2d065-230">Nella categoria di risoluzione dei problemi di hello, si noti hello varie opzioni per l'utilizzo di potenziali problemi di strumenti tootroubleshoot con un'app in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2d065-230">Under hello Troubleshoot category, notice hello various choices for using tools tootroubleshoot potential issues with a running app.</span></span> <span data-ttu-id="2d065-231">È possibile, ad esempio, monitorare il traffico HTTP in tempo reale, abilitare la riparazione automatica, visualizzare log e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="2d065-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![Immagine38][image38]
3. <span data-ttu-id="2d065-233">Scegliere le metriche del sito tooquickly get di una visualizzazione di alcuni codici HTTP.</span><span class="sxs-lookup"><span data-stu-id="2d065-233">Choose Site Metrics tooquickly get a view of some HTTP codes.</span></span>
   
   ![Immagine39][image39]
4. <span data-ttu-id="2d065-235">Scegliere Diagnostica distribuita come servizio.</span><span class="sxs-lookup"><span data-stu-id="2d065-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="2d065-236">Scegliere il tipo di applicazione, quindi scegliere Esegui.</span><span class="sxs-lookup"><span data-stu-id="2d065-236">Choose your application type, then choose Run.</span></span>
   
   ![Immagine40][image40]
   
   <span data-ttu-id="2d065-238">Inizia una raccolta.</span><span class="sxs-lookup"><span data-stu-id="2d065-238">A collection begins.</span></span>
   
   ![Immagine41][image41]
5. <span data-ttu-id="2d065-240">È possibile scegliere i potenziali problemi di hello log appropriato toodiagnose.</span><span class="sxs-lookup"><span data-stu-id="2d065-240">You may choose hello appropriate log toodiagnose potential issues.</span></span> <span data-ttu-id="2d065-241">È necessario tooenable registrazione toosee tutti i dati disponibili hello opzioni, ad esempio log HTTP.</span><span class="sxs-lookup"><span data-stu-id="2d065-241">You need tooenable logging toosee all of hello available data options such as HTTP Logs.</span></span>
   
   ![Immagine42][image42]
   
   <span data-ttu-id="2d065-243">Facendo clic sul file di Dump di memoria hello è possibile scaricare e analizzare un DebugDiag toohelp report di analisi trovare problemi potenziali.</span><span class="sxs-lookup"><span data-stu-id="2d065-243">By clicking on hello Memory Dump file you can download and analyze a DebugDiag analysis report toohelp find potential issues.</span></span>
   
   ![Immagine43][image43]
6. <span data-ttu-id="2d065-245">tooview più dati, è necessario tooenable ulteriori opzioni di registrazione.</span><span class="sxs-lookup"><span data-stu-id="2d065-245">tooview more data, you need tooenable additional logging.</span></span> <span data-ttu-id="2d065-246">Nel portale di Azure hello, passare toohello Web app e scegliere le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="2d065-246">In hello Azure Portal, navigate toohello Web app and choose Settings.</span></span>
   
   ![Immagine44][image44]
7. <span data-ttu-id="2d065-248">Scorrere verso il basso categoria funzionalità toohello e scegliere i log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="2d065-248">Scroll down toohello features category, and choose Diagnostic logs.</span></span>
   
      ![Immagine45][image45]
8. <span data-ttu-id="2d065-250">Si noti hello varie opzioni per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="2d065-250">Notice hello various options for logging.</span></span> <span data-ttu-id="2d065-251">Attivare Registrazione server Web e fare clic su Salva.</span><span class="sxs-lookup"><span data-stu-id="2d065-251">Toggle on Web server logging and click save.</span></span>
   
   ![Immagine46][image46]
9. <span data-ttu-id="2d065-253">Spostare nuovamente toohello area di strumenti per app hello e scegliere diagnostica come servizio e fare clic su Esegui toorerun hello raccolta dei dati.</span><span class="sxs-lookup"><span data-stu-id="2d065-253">Move back toohello tools area for hello app and choose Diagnostics as a service and click Run toorerun hello data collection.</span></span>
   
   ![Immagine47][image47]
10. <span data-ttu-id="2d065-255">Impostazione registrazione hello HTTP è abilitata, è ora possibile visualizzare i dati raccolti per i log di HTTP.</span><span class="sxs-lookup"><span data-stu-id="2d065-255">With hello HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![Immagine48][image48]
11. <span data-ttu-id="2d065-257">Facendo clic sul file di log hello HTML, si produce un report di basate su browser completo per un'analisi più approfondita.</span><span class="sxs-lookup"><span data-stu-id="2d065-257">By clicking hello HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![Immagine49][image49]
12. <span data-ttu-id="2d065-259">Consente di tornare sezione Strumenti toohello hello portale di Azure per app hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-259">Move back toohello tools section in hello Azure Portal for hello app.</span></span> <span data-ttu-id="2d065-260">Scorrere sezione Strumenti toohello e scegliere Process Explorer.</span><span class="sxs-lookup"><span data-stu-id="2d065-260">Scroll toohello Tools section and choose Process Explorer.</span></span>
    
    ![Immagine50][image50]
13. <span data-ttu-id="2d065-262">Scegliendo Esplora processi, è possibile visualizzare i dettagli sui processi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2d065-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="2d065-263">Di seguito è possibile analizza i processi e anche terminare i processi di tutti gli elementi dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-263">Notice below you can drill into processes and even kill processes all from hello Azure Portal.</span></span>
    
    ![Immagine51][image51]
    
    ![Immagine52][image52]
14. <span data-ttu-id="2d065-266">Spostarsi all'indietro pannello impostazioni toohello di hello sinistra.</span><span class="sxs-lookup"><span data-stu-id="2d065-266">Move back toohello Settings blade on hello left.</span></span> <span data-ttu-id="2d065-267">Fare clic su Nuova richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="2d065-267">Click New support request.</span></span>
    
    ![Immagine53][image53]
15. <span data-ttu-id="2d065-269">Dal pannello hello in hello destra, può inserire le informazioni sui problemi di hello, immettere le informazioni di contatto e caricare anche dati di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="2d065-269">From hello blade on hello right, you can fill out details about hello issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="2d065-270">Hello portale di Azure consente l'utilizzo di un'esperienza di supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2d065-270">hello Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![Immagine54][image54]
    
    ![Immagine55][image55]
    
    <span data-ttu-id="2d065-273">Hello portale di Azure consente di fornire potente e familiare tooling esperienze toohelp monitoraggio e risoluzione dei problemi delle applicazioni in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2d065-273">hello Azure Portal helps provide powerful and familiar tooling experiences toohelp monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="2d065-274">Sono anche tootake in grado di azione rapidamente mediante l'esecuzione di attività, ad esempio riciclo dei processi, l'abilitazione e disabilitazione di varie raccolte di dati e anche l'integrazione con supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2d065-274">You are also able tootake action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="2d065-275">Gestione di applicazioni generale</span><span class="sxs-lookup"><span data-stu-id="2d065-275">General Application Management</span></span>
<span data-ttu-id="2d065-276">Quando la gestione delle applicazioni, è spesso necessario tooperform una vasta gamma di attività quali la configurazione di strategie di backup, l'implementazione e gestione dei provider di identità e la configurazione di controllo di accesso basato sui ruoli.</span><span class="sxs-lookup"><span data-stu-id="2d065-276">When managing applications, you often need tooperform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="2d065-277">Come con hello altre esperienze DevOps, hello piattaforma Azure integra queste operazioni direttamente nel portale hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-277">As with hello other DevOps experiences, hello Azure platform integrates these tasks directly into hello portal.</span></span>

1. <span data-ttu-id="2d065-278">viene sincronizzato tooensure hello App Web protetta da perdita di dati è necessario tooconfigure backup.</span><span class="sxs-lookup"><span data-stu-id="2d065-278">tooensure you are keeping hello Web App safe from data loss you need tooconfigure backups.</span></span> <span data-ttu-id="2d065-279">Passare toohello area di impostazioni per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="2d065-279">Navigate toohello Settings area for your Web app.</span></span>
   
   ![Immagine56][image56]
2. <span data-ttu-id="2d065-281">Nel Pannello di hello in hello destro, scorrere verso il basso toohello categoria di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2d065-281">In hello blade on hello right, scroll down toohello Features category.</span></span>
   
    ![Immagine57][image57]
3. <span data-ttu-id="2d065-283">Scegliere di backup. a destra hello verrà visualizzato un pannello.</span><span class="sxs-lookup"><span data-stu-id="2d065-283">Choose Backups; a blade opens on hello right.</span></span>
   
   ![Immagine58][image58]
4. <span data-ttu-id="2d065-285">Fare clic su Configura, scegliere un account di archiviazione dal pannello hello in hello destra.</span><span class="sxs-lookup"><span data-stu-id="2d065-285">Click Configure, choose a storage account from hello blade on hello right.</span></span>
   
   ![Immagine59][image59]
5. <span data-ttu-id="2d065-287">A questo punto, creare e scegliere un toohold contenitore di archiviazione dei backup.</span><span class="sxs-lookup"><span data-stu-id="2d065-287">Now create and choose a storage container toohold your backups.</span></span> <span data-ttu-id="2d065-288">Fare clic su Crea nella parte inferiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-288">Click create at hello bottom of hello blade.</span></span> <span data-ttu-id="2d065-289">Selezionare quindi il contenitore di hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-289">Then select hello container.</span></span>
   
   ![Immagine60][image60]
6. <span data-ttu-id="2d065-291">Una volta scelto il contenitore di hello, è possibile configurare le pianificazioni, nonché i backup di programma di installazione per i database.</span><span class="sxs-lookup"><span data-stu-id="2d065-291">Once you have chosen hello container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="2d065-292">Per questo scenario, fare clic su hello Salva icona.</span><span class="sxs-lookup"><span data-stu-id="2d065-292">For this scenario, click hello save icon.</span></span>
   
    ![Immagine61][image61]
7. <span data-ttu-id="2d065-294">Dopo il salvataggio, scorrere indietro toohello pannello a sinistra di hello per i backup.</span><span class="sxs-lookup"><span data-stu-id="2d065-294">After saving, scroll back toohello blade on hello left for Backups.</span></span> <span data-ttu-id="2d065-295">Fare clic su Esegui Backup ora un'applicazione hello tooback.</span><span class="sxs-lookup"><span data-stu-id="2d065-295">Click Backup Now tooback hello application.</span></span>
   
    ![Immagine62][image62]
8. <span data-ttu-id="2d065-297">Dopo alcuni istanti, viene creato un backup.</span><span class="sxs-lookup"><span data-stu-id="2d065-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="2d065-298">Hello avviso Ripristina ora opzione hello cattura di schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="2d065-298">Notice hello Restore Now option on hello screen-shot below.</span></span>
   
    ![Immagine63][image63]
9. <span data-ttu-id="2d065-300">Fare clic su Ripristina ora ed esaminare pannello toohello opzioni di hello in hello destra.</span><span class="sxs-lookup"><span data-stu-id="2d065-300">Click on Restore Now and examine hello options toohello blade on hello right.</span></span> <span data-ttu-id="2d065-301">È possibile scegliere che un backup appropriati e facilmente tooan ripristino precedente lo stato in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="2d065-301">You can choose an appropriate backup and easily restore tooan earlier state as necessary.</span></span> <span data-ttu-id="2d065-302">portale di Azure Hello ci ha consentito di abilitare facilmente una strategia di ripristino di emergenza semplice per l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-302">hello Azure portal has helped us easily enable a simple disaster recovery strategy for hello app.</span></span>
   
    ![Immagine64][image64]
10. <span data-ttu-id="2d065-304">Spostare nuovamente pannello impostazioni toohello a sinistra di hello e in funzioni e scegliere l'autenticazione/autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="2d065-304">Move back toohello Settings blade on hello left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![Immagine65][image65]
11. <span data-ttu-id="2d065-306">Nel pannello hello in hello destra scegliere l'autenticazione del servizio App.</span><span class="sxs-lookup"><span data-stu-id="2d065-306">In hello blade on hello right choose App Service Authentication.</span></span> <span data-ttu-id="2d065-307">Si noti diverse hello opzioni che è possibile configurare con i provider più diffusi.</span><span class="sxs-lookup"><span data-stu-id="2d065-307">Notice hello variety of options you can configure with popular providers.</span></span>
    
     ![Immagine66][image66]
12. <span data-ttu-id="2d065-309">Scegliere provider hello di propria scelta e notare le opzioni di hello per ambito hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-309">Choose hello provider of your choice and notice hello options for hello scope.</span></span> <span data-ttu-id="2d065-310">È possibile fornire un ID dell'App e il segreto dell'applicazione e abilitare rapidamente autenticazione Facebook per l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for hello app.</span></span> <span data-ttu-id="2d065-311">Portale di Azure Hello Abilita l'autenticazione come una soluzione completa per le app.</span><span class="sxs-lookup"><span data-stu-id="2d065-311">hello Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![Immagine67][image67]
13. <span data-ttu-id="2d065-313">Spostare nuovamente pannello impostazioni toohello e selezionare gli utenti nella categoria Gestione delle risorse hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-313">Move back toohello Settings blade and choose Users under hello Resource Management category.</span></span>
    
     ![Immagine68][image68]
14. <span data-ttu-id="2d065-315">Nel pannello hello in hello destro esaminare hello varie opzioni per l'aggiunta di ruoli e utenti.</span><span class="sxs-lookup"><span data-stu-id="2d065-315">In hello blade on hello right examine hello various options for adding roles and users.</span></span> <span data-ttu-id="2d065-316">Hello portale di Azure consente di controllare facilmente RBAC (controllo di accesso basato sui ruoli) per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2d065-316">hello Azure Portal lets you easily control RBAC (Role-based access control) for hello application.</span></span>
    
     ![Immagine69][image69]

## <a name="summary"></a><span data-ttu-id="2d065-318">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="2d065-318">Summary</span></span>
<span data-ttu-id="2d065-319">In questa esercitazione illustrati alcuni dei power hello con hello piattaforma Azure rapidamente consente la distribuzione continua per un'app web, l'esecuzione vari di sviluppo e le attività di test, il monitoraggio e risoluzione dei problemi di un'applicazione in tempo reale e infine Gestione chiave strategie, ad esempio il ripristino di emergenza, l'identità e controllo di accesso basato sui ruoli.</span><span class="sxs-lookup"><span data-stu-id="2d065-319">This tutorial demonstrated some of hello power with hello Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="2d065-320">Hello piattaforma Azure consente un'esperienza integrata per i flussi di lavoro di DevOps e possono lavorare in modo efficiente, rimanendo nel contesto per l'attività hello in questione.</span><span class="sxs-lookup"><span data-stu-id="2d065-320">hello Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for hello task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d065-321">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d065-321">Next steps</span></span>
* <span data-ttu-id="2d065-322">Gestione risorse di Azure è importante per l'abilitazione di DevOps su hello piattaforma Azure.</span><span class="sxs-lookup"><span data-stu-id="2d065-322">Azure Resource Manager is important for enabling DevOps on hello Azure platform.</span></span>  <span data-ttu-id="2d065-323">visitare più toolearn [Panoramica di gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2d065-323">toolearn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="2d065-324">informazioni sulla distribuzione di servizio App di Azure, visitare toolearn [distribuire il servizio App di tooAzure app](../app-service-web/web-sites-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="2d065-324">toolearn more about Azure App Service deployment visit [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md)</span></span>

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
