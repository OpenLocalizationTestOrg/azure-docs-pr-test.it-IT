---
title: aaaDeploy ed eseguire l'aggiornamento di Azure microservizi localmente | Documenti Microsoft
description: Informazioni su come distribuire un esempio di applicazione esistente tooit tooset di un cluster di Service Fabric locale e quindi aggiornare l'applicazione.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a><span data-ttu-id="b12ad-103">Introduzione alla distribuzione e all'aggiornamento di applicazioni nel cluster locale</span><span class="sxs-lookup"><span data-stu-id="b12ad-103">Get started with deploying and upgrading applications on your local cluster</span></span>
<span data-ttu-id="b12ad-104">Hello Azure Service Fabric SDK include un ambiente di sviluppo locale completo che è possibile utilizzare tooquickly iniziare con la distribuzione e la gestione delle applicazioni in un cluster locale.</span><span class="sxs-lookup"><span data-stu-id="b12ad-104">hello Azure Service Fabric SDK includes a full local development environment that you can use tooquickly get started with deploying and managing applications on a local cluster.</span></span> <span data-ttu-id="b12ad-105">In questo articolo, creare un cluster locale, distribuire un tooit applicazione esistente e quindi aggiornare tale applicazione tooa nuova versione, tutte da Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b12ad-105">In this article, you create a local cluster, deploy an existing application tooit, and then upgrade that application tooa new version, all from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="b12ad-106">Questo articolo presuppone che l' [ambiente di sviluppo sia già stato configurato](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b12ad-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span></span>
> 
> 

## <a name="create-a-local-cluster"></a><span data-ttu-id="b12ad-107">Creare un cluster locale</span><span class="sxs-lookup"><span data-stu-id="b12ad-107">Create a local cluster</span></span>
<span data-ttu-id="b12ad-108">Un cluster di Service Fabric rappresenta un set di risorse hardware in cui è possibile distribuire le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b12ad-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span></span> <span data-ttu-id="b12ad-109">In genere, un cluster è costituito da un punto qualsiasi da cinque toomany migliaia di computer.</span><span class="sxs-lookup"><span data-stu-id="b12ad-109">Typically, a cluster is made up of anywhere from five toomany thousands of machines.</span></span> <span data-ttu-id="b12ad-110">Tuttavia, hello Service Fabric SDK include una configurazione del cluster che è possibile eseguire su un singolo computer.</span><span class="sxs-lookup"><span data-stu-id="b12ad-110">However, hello Service Fabric SDK includes a cluster configuration that can run on a single machine.</span></span>

<span data-ttu-id="b12ad-111">È importante toounderstand che hello cluster locale di Service Fabric non è un emulatore o simulatore.</span><span class="sxs-lookup"><span data-stu-id="b12ad-111">It is important toounderstand that hello Service Fabric local cluster is not an emulator or simulator.</span></span> <span data-ttu-id="b12ad-112">Viene eseguito hello stesso codice di piattaforma che si trova su un cluster con più computer.</span><span class="sxs-lookup"><span data-stu-id="b12ad-112">It runs hello same platform code that is found on multi-machine clusters.</span></span> <span data-ttu-id="b12ad-113">Hello unica differenza è che l'esecuzione di processi di piattaforma hello che sono in genere suddivisi in cinque macchine in un unico computer.</span><span class="sxs-lookup"><span data-stu-id="b12ad-113">hello only difference is that it runs hello platform processes that are normally spread across five machines on one machine.</span></span>

<span data-ttu-id="b12ad-114">Hello SDK fornisce due modi tooset di un cluster locale: un Windows PowerShell script e hello gestione Cluster locale sistema cassetto app.</span><span class="sxs-lookup"><span data-stu-id="b12ad-114">hello SDK provides two ways tooset up a local cluster: a Windows PowerShell script and hello Local Cluster Manager system tray app.</span></span> <span data-ttu-id="b12ad-115">In questa esercitazione, si usa uno script di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-115">In this tutorial, we use hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="b12ad-116">Se è già stato creato un cluster locale con la distribuzione di un'applicazione da Visual Studio, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="b12ad-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span></span>
> 
> 

1. <span data-ttu-id="b12ad-117">Avviare una nuova finestra di PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b12ad-117">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="b12ad-118">Eseguire lo script di installazione di cluster hello dalla cartella SDK hello:</span><span class="sxs-lookup"><span data-stu-id="b12ad-118">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    <span data-ttu-id="b12ad-119">La configurazione del cluster richiede alcuni istanti.</span><span class="sxs-lookup"><span data-stu-id="b12ad-119">Cluster setup takes a few moments.</span></span> <span data-ttu-id="b12ad-120">Al termine, l'output visualizzato sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b12ad-120">After setup is finished, you should see output similar to:</span></span>
   
    ![Output installazione del cluster][cluster-setup-success]
   
    <span data-ttu-id="b12ad-122">Si è ora pronto tootry distribuzione di un cluster di tooyour dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b12ad-122">You are now ready tootry deploying an application tooyour cluster.</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="b12ad-123">Distribuire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="b12ad-123">Deploy an application</span></span>
<span data-ttu-id="b12ad-124">Hello Service Fabric SDK include una vasta gamma di strumenti per la creazione di applicazioni per sviluppatori e ai Framework.</span><span class="sxs-lookup"><span data-stu-id="b12ad-124">hello Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span></span> <span data-ttu-id="b12ad-125">Se è interessati a ottenere applicazioni toocreate in Visual Studio, vedere [creare la prima applicazione di Service Fabric in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="b12ad-125">If you are interested in learning how toocreate applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>

<span data-ttu-id="b12ad-126">In questa esercitazione, si utilizza un'applicazione di esempio esistente (denominata WordCount) in modo che sia possibile concentrarsi sugli aspetti di hello gestione della piattaforma hello: la distribuzione, monitoraggio e aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="b12ad-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on hello management aspects of hello platform: deployment, monitoring, and upgrade.</span></span>

1. <span data-ttu-id="b12ad-127">Avviare una nuova finestra di PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b12ad-127">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="b12ad-128">Importare il modulo di PowerShell di Service Fabric SDK hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-128">Import hello Service Fabric SDK PowerShell module.</span></span>
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. <span data-ttu-id="b12ad-129">Creare un'applicazione hello toostore di directory disponibili per download e distribuzione, ad esempio C:\ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="b12ad-129">Create a directory toostore hello application that you download and deploy, such as C:\ServiceFabric.</span></span>
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. <span data-ttu-id="b12ad-130">[Scaricare l'applicazione WordCount hello](http://aka.ms/servicefabric-wordcountapp) toohello percorso è stato creato.</span><span class="sxs-lookup"><span data-stu-id="b12ad-130">[Download hello WordCount application](http://aka.ms/servicefabric-wordcountapp) toohello location you created.</span></span>  <span data-ttu-id="b12ad-131">Nota: browser Microsoft Edge hello Salva file hello con un *zip* estensione.</span><span class="sxs-lookup"><span data-stu-id="b12ad-131">Note: hello Microsoft Edge browser saves hello file with a *.zip* extension.</span></span>  <span data-ttu-id="b12ad-132">Modificare anche l'estensione del file hello*.sfpkg*.</span><span class="sxs-lookup"><span data-stu-id="b12ad-132">Change hello file extension too*.sfpkg*.</span></span>
5. <span data-ttu-id="b12ad-133">Connettersi cluster locale toohello:</span><span class="sxs-lookup"><span data-stu-id="b12ad-133">Connect toohello local cluster:</span></span>
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. <span data-ttu-id="b12ad-134">Creare una nuova applicazione utilizzando il comando di distribuzione del SDK di hello con un nome e un pacchetto di applicazione toohello percorso.</span><span class="sxs-lookup"><span data-stu-id="b12ad-134">Create a new application using hello SDK's deployment command with a name and a path toohello application package.</span></span>
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="b12ad-135">Se tutto va bene, dovrebbe essere hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="b12ad-135">If all goes well, you should see hello following output:</span></span>
   
    ![Distribuire un cluster locale toohello di applicazione][deploy-app-to-local-cluster]
7. <span data-ttu-id="b12ad-137">un'applicazione hello toosee in azione, avviare il browser hello e passare troppo[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span><span class="sxs-lookup"><span data-stu-id="b12ad-137">toosee hello application in action, launch hello browser and navigate too[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span></span> <span data-ttu-id="b12ad-138">Dovrebbe essere visualizzato:</span><span class="sxs-lookup"><span data-stu-id="b12ad-138">You should see:</span></span>
   
    ![Interfaccia utente dell'applicazione distribuita][deployed-app-ui]
   
    <span data-ttu-id="b12ad-140">applicazione WordCount Hello è semplice.</span><span class="sxs-lookup"><span data-stu-id="b12ad-140">hello WordCount application is simple.</span></span> <span data-ttu-id="b12ad-141">Include sul lato client JavaScript toogenerate casuale cinque caratteri "parole chiave", che vengono quindi inoltrate toohello applicazione tramite l'API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b12ad-141">It includes client-side JavaScript code toogenerate random five-character "words", which are then relayed toohello application via ASP.NET Web API.</span></span> <span data-ttu-id="b12ad-142">Un servizio con stato registra il numero di hello di parole conteggiati.</span><span class="sxs-lookup"><span data-stu-id="b12ad-142">A stateful service tracks hello number of words counted.</span></span> <span data-ttu-id="b12ad-143">Devono essere partizionati in base hello primo carattere della parola hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-143">They are partitioned based on hello first character of hello word.</span></span> <span data-ttu-id="b12ad-144">È possibile trovare il codice sorgente hello per applicazione WordCount hello in hello [classico introduzione esempi](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span><span class="sxs-lookup"><span data-stu-id="b12ad-144">You can find hello source code for hello WordCount app in hello [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span></span>
   
    <span data-ttu-id="b12ad-145">l'applicazione Hello che sono stati distribuiti contiene quattro partizioni.</span><span class="sxs-lookup"><span data-stu-id="b12ad-145">hello application that we deployed contains four partitions.</span></span> <span data-ttu-id="b12ad-146">In modo da parole che iniziano con una lettera e G vengono archiviate nella partizione prima di hello, le parole che iniziano con H a N vengono archiviate nella seconda partizione hello e così via.</span><span class="sxs-lookup"><span data-stu-id="b12ad-146">So words beginning with A through G are stored in hello first partition, words beginning with H through N are stored in hello second partition, and so on.</span></span>

## <a name="view-application-details-and-status"></a><span data-ttu-id="b12ad-147">Visualizzare i dettagli e lo stato dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="b12ad-147">View application details and status</span></span>
<span data-ttu-id="b12ad-148">Ora che è stata distribuita un'applicazione hello, ecco alcuni dei dettagli dell'app hello in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b12ad-148">Now that we have deployed hello application, let's look at some of hello app details in PowerShell.</span></span>

1. <span data-ttu-id="b12ad-149">Eseguire una query tutte le applicazioni distribuite in cluster hello:</span><span class="sxs-lookup"><span data-stu-id="b12ad-149">Query all deployed applications on hello cluster:</span></span>
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    <span data-ttu-id="b12ad-150">Supponendo che è stato distribuito solo app WordCount hello, viene visualizzato qualcosa di simile a:</span><span class="sxs-lookup"><span data-stu-id="b12ad-150">Assuming that you have only deployed hello WordCount app, you see something similar to:</span></span>
   
    ![Query per individuare tutte le applicazioni distribuite in PowerShell][ps-getsfapp]
2. <span data-ttu-id="b12ad-152">Passare livello successivo toohello eseguendo una query su set hello dei servizi inclusi in un'applicazione WordCount hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-152">Go toohello next level by querying hello set of services that are included in hello WordCount application.</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Elencare i servizi per un'applicazione hello in PowerShell][ps-getsfsvc]
   
    <span data-ttu-id="b12ad-154">un'applicazione Hello è costituita da due servizi front-end web hello e servizio con stato hello che gestisce le parole hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-154">hello application is made up of two services, hello web front end, and hello stateful service that manages hello words.</span></span>
3. <span data-ttu-id="b12ad-155">Infine, esaminare l'elenco di hello delle partizioni per WordCountService:</span><span class="sxs-lookup"><span data-stu-id="b12ad-155">Finally, look at hello list of partitions for WordCountService:</span></span>
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Visualizzare le partizioni servizio hello in PowerShell][ps-getsfpartitions]
   
    <span data-ttu-id="b12ad-157">set di comandi che è stata utilizzata, come tutti i comandi di PowerShell di Service Fabric Hello, sono disponibili per qualsiasi cluster che è possibile connettersi a, locale o remoto.</span><span class="sxs-lookup"><span data-stu-id="b12ad-157">hello set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span></span>
   
    <span data-ttu-id="b12ad-158">Per più visual toointeract un modo con cluster hello, è possibile utilizzare lo strumento hello di Service Fabric Explorer basata sul web passando troppo[http://localhost:19080/Esplora](http://localhost:19080/Explorer) nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-158">For a more visual way toointeract with hello cluster, you can use hello web-based Service Fabric Explorer tool by navigating too[http://localhost:19080/Explorer](http://localhost:19080/Explorer) in hello browser.</span></span>
   
    ![Visualizzazione dei dettagli dell'applicazione in Service Fabric Explorer][sfx-service-overview]
   
   > [!NOTE]
   > <span data-ttu-id="b12ad-160">toolearn informazioni su Service Fabric Explorer, vedere [visualizzazione cluster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b12ad-160">toolearn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
   > 
   > 

## <a name="upgrade-an-application"></a><span data-ttu-id="b12ad-161">Aggiornare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="b12ad-161">Upgrade an application</span></span>
<span data-ttu-id="b12ad-162">Service Fabric fornisce gli aggiornamenti senza tempo di inattività dal monitoraggio dell'integrità di hello di un'applicazione hello come viene eseguito il rollback cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-162">Service Fabric provides no-downtime upgrades by monitoring hello health of hello application as it rolls out across hello cluster.</span></span> <span data-ttu-id="b12ad-163">Eseguire un aggiornamento dell'applicazione WordCount hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-163">Perform an upgrade of hello WordCount application.</span></span>

<span data-ttu-id="b12ad-164">nuova versione di Hello di un'applicazione hello ora conta solo le parole che iniziano con una vocale.</span><span class="sxs-lookup"><span data-stu-id="b12ad-164">hello new version of hello application now counts only words that begin with a vowel.</span></span> <span data-ttu-id="b12ad-165">Come l'aggiornamento di hello implementa, vediamo due modifiche del comportamento dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-165">As hello upgrade rolls out, we see two changes in hello application's behavior.</span></span> <span data-ttu-id="b12ad-166">In primo luogo, deve rallentare frequenza hello in corrispondenza del quale il conteggio di hello cresce, poiché viene contate minor numero di parole.</span><span class="sxs-lookup"><span data-stu-id="b12ad-166">First, hello rate at which hello count grows should slow, since fewer words are being counted.</span></span> <span data-ttu-id="b12ad-167">In secondo luogo, poiché la prima partizione hello ha due vocali (ed E) e tutte le altre partizioni contengano solo uno, il conteggio deve infine avviare toooutpace hello altri.</span><span class="sxs-lookup"><span data-stu-id="b12ad-167">Second, since hello first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start toooutpace hello others.</span></span>

1. <span data-ttu-id="b12ad-168">[Download del pacchetto versione 2 WordCount hello](http://aka.ms/servicefabric-wordcountappv2) toohello stessa posizione in cui è stato scaricato il pacchetto di versione 1 hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-168">[Download hello WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) toohello same location where you downloaded hello version 1 package.</span></span>
2. <span data-ttu-id="b12ad-169">Restituire tooyour finestra di PowerShell e utilizzare il comando di aggiornamento del SDK di hello tooregister hello nuova versione nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-169">Return tooyour PowerShell window and use hello SDK's upgrade command tooregister hello new version in hello cluster.</span></span> <span data-ttu-id="b12ad-170">Quindi iniziare l'aggiornamento dell'infrastruttura di hello: / applicazione WordCount.</span><span class="sxs-lookup"><span data-stu-id="b12ad-170">Then begin upgrading hello fabric:/WordCount application.</span></span>
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    <span data-ttu-id="b12ad-171">Dovrebbe essere hello output seguente nel PowerShell come hello aggiornamento inizia.</span><span class="sxs-lookup"><span data-stu-id="b12ad-171">You should see hello following output in PowerShell as hello upgrade begins.</span></span>
   
    ![Stato dell'aggiornamento in PowerShell][ps-appupgradeprogress]
3. <span data-ttu-id="b12ad-173">Durante l'aggiornamento di hello procedere, può risultare più semplice toomonitor lo stato da Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b12ad-173">While hello upgrade is proceeding, you may find it easier toomonitor its status from Service Fabric Explorer.</span></span> <span data-ttu-id="b12ad-174">Avviare una finestra del browser e passare troppo[http://localhost:19080/Esplora](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="b12ad-174">Launch a browser window and navigate too[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="b12ad-175">Espandere **applicazioni** albero hello hello sinistra, quindi scegliere **WordCount**e infine **fabric: / WordCount**.</span><span class="sxs-lookup"><span data-stu-id="b12ad-175">Expand **Applications** in hello tree on hello left, then choose **WordCount**, and finally **fabric:/WordCount**.</span></span> <span data-ttu-id="b12ad-176">Nella scheda essentials hello, vedere lo stato di hello dell'aggiornamento hello durante il trasferimento tramite domini di aggiornamento del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-176">In hello essentials tab, you see hello status of hello upgrade as it proceeds through hello cluster's upgrade domains.</span></span>
   
    ![Stato dell'aggiornamento in Service Fabric Explorer][sfx-upgradeprogress]
   
    <span data-ttu-id="b12ad-178">Come avviare l'aggiornamento di hello tramite ogni dominio, controlli di integrità sono eseguite tooensure che un'applicazione hello è funziona correttamente.</span><span class="sxs-lookup"><span data-stu-id="b12ad-178">As hello upgrade proceeds through each domain, health checks are performed tooensure that hello application is behaving properly.</span></span>
4. <span data-ttu-id="b12ad-179">Se si esegue nuovamente hello in precedenza eseguire una query per il set di hello di servizi nell'infrastruttura hello: / applicazione WordCount, si noti che hello versione WordCountService modificato ma hello WordCountWebService versione non è stato eseguito:</span><span class="sxs-lookup"><span data-stu-id="b12ad-179">If you rerun hello earlier query for hello set of services in hello fabric:/WordCount application, notice that hello WordCountService version changed but hello WordCountWebService version did not:</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Query per individuare i servizi dell'applicazione dopo l'aggiornamento][ps-getsfsvc-postupgrade]
   
    <span data-ttu-id="b12ad-181">Questo esempio illustra il modo in cui Service Fabric gestisce gli aggiornamenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b12ad-181">This example highlights how Service Fabric manages application upgrades.</span></span> <span data-ttu-id="b12ad-182">Tocca solo hello set di servizi (o pacchetti di configurazione o codice all'interno di tali servizi) che sono stati modificati, che consente al processo di aggiornamento più veloce e affidabile hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-182">It touches only hello set of services (or code/configuration packages within those services) that have changed, which makes hello process of upgrading faster and more reliable.</span></span>
5. <span data-ttu-id="b12ad-183">Infine, restituire toohello il comportamento della nuova versione dell'applicazione hello di browser tooobserve hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-183">Finally, return toohello browser tooobserve hello behavior of hello new application version.</span></span> <span data-ttu-id="b12ad-184">Come previsto, hello conteggio avanza più lenta e hello prima partizione termina con leggermente più del volume hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-184">As expected, hello count progresses more slowly, and hello first partition ends up with slightly more of hello volume.</span></span>
   
    ![Nuova versione hello visualizzazione di un'applicazione hello nel browser hello][deployed-app-ui-v2]

## <a name="cleaning-up"></a><span data-ttu-id="b12ad-186">+ Cleaning up</span><span class="sxs-lookup"><span data-stu-id="b12ad-186">Cleaning up</span></span>
<span data-ttu-id="b12ad-187">Prima di concludere, è importante tooremember che hello cluster locale è di tipo real.</span><span class="sxs-lookup"><span data-stu-id="b12ad-187">Before wrapping up, it's important tooremember that hello local cluster is real.</span></span> <span data-ttu-id="b12ad-188">Le applicazioni continuano toorun in background hello fino alla rimozione.</span><span class="sxs-lookup"><span data-stu-id="b12ad-188">Applications continue toorun in hello background until you remove them.</span></span>  <span data-ttu-id="b12ad-189">A seconda della natura hello delle App, un'app in esecuzione può richiedere notevoli risorse del computer.</span><span class="sxs-lookup"><span data-stu-id="b12ad-189">Depending on hello nature of your apps, a running app can take up significant resources on your machine.</span></span> <span data-ttu-id="b12ad-190">Si dispone di vari opzioni toomanage e applicazioni cluster hello:</span><span class="sxs-lookup"><span data-stu-id="b12ad-190">You have several options toomanage applications and hello cluster:</span></span>

1. <span data-ttu-id="b12ad-191">tooremove una singola applicazione e tutte di dati, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b12ad-191">tooremove an individual application and all it's data, run hello following command:</span></span>
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="b12ad-192">In alternativa, eliminare un'applicazione hello hello Service Fabric Explorer **azioni** menu o i menu di scelta rapida hello nella visualizzazione elenco a sinistra dell'applicazione di hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-192">Or, delete hello application from hello Service Fabric Explorer **ACTIONS** menu or hello context menu in hello left-hand application list view.</span></span>
   
    ![Eliminare un'applicazione in Service Fabric Explorer][sfe-delete-application]
2. <span data-ttu-id="b12ad-194">Dopo l'eliminazione di un'applicazione hello dal cluster hello, annullare la registrazione di versioni 1.0.0 e 2.0.0 del tipo di applicazione WordCount hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-194">After deleting hello application from hello cluster, unregister versions 1.0.0 and 2.0.0 of hello WordCount application type.</span></span> <span data-ttu-id="b12ad-195">L'eliminazione rimuove i pacchetti di applicazione hello, inclusi codice hello e la configurazione, dall'archivio di immagini del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-195">Deletion removes hello application packages, including hello code and configuration, from hello cluster's image store.</span></span>
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    <span data-ttu-id="b12ad-196">In alternativa, in Service Fabric Explorer, scegliere **tipo annullamento del provisioning** per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for hello application.</span></span>
3. <span data-ttu-id="b12ad-197">tooshut cluster hello ma Mantieni dati dell'applicazione hello e tracce, fare clic su **arrestare Cluster locale** nell'app di area di notifica di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-197">tooshut down hello cluster but keep hello application data and traces, click **Stop Local Cluster** in hello system tray app.</span></span>
4. <span data-ttu-id="b12ad-198">cluster hello toodelete interamente, fare clic su **rimuovere Cluster locale** nell'app di area di notifica di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-198">toodelete hello cluster entirely, click **Remove Local Cluster** in hello system tray app.</span></span> <span data-ttu-id="b12ad-199">Questa opzione comporterà un altro hello lenta distribuzione quando che si preme F5 in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b12ad-199">This option will result in another slow deployment hello next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="b12ad-200">Rimuovi cluster locale hello solo se non si prevede di toouse per un certo tempo oppure se è necessario tooreclaim risorse.</span><span class="sxs-lookup"><span data-stu-id="b12ad-200">Remove hello local cluster only if you don't intend toouse it for some time or if you need tooreclaim resources.</span></span>

## <a name="one-node-and-five-node-cluster-mode"></a><span data-ttu-id="b12ad-201">Modalità cluster a un nodo e a cinque nodi</span><span class="sxs-lookup"><span data-stu-id="b12ad-201">One-node and five-node cluster mode</span></span>
<span data-ttu-id="b12ad-202">Quando si sviluppano applicazioni, ci si ritroverà spesso a eseguire rapide iterazioni di scrittura di codice, debug, modifica del codice e debug.</span><span class="sxs-lookup"><span data-stu-id="b12ad-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span></span> <span data-ttu-id="b12ad-203">toohelp ottimizzare questo processo, cluster locale di hello può essere eseguito in due modalità: uno o cinque nodi.</span><span class="sxs-lookup"><span data-stu-id="b12ad-203">toohelp optimize this process, hello local cluster can run in two modes: one-node or five-node.</span></span> <span data-ttu-id="b12ad-204">Entrambe le modalità cluster presentano vantaggi.</span><span class="sxs-lookup"><span data-stu-id="b12ad-204">Both cluster modes have their benefits.</span></span> <span data-ttu-id="b12ad-205">Modalità di cinque nodi cluster consente toowork con un cluster reale.</span><span class="sxs-lookup"><span data-stu-id="b12ad-205">Five-node cluster mode enables you toowork with a real cluster.</span></span> <span data-ttu-id="b12ad-206">È possibile testare gli scenari di failover e usare più istanze e repliche dei servizi.</span><span class="sxs-lookup"><span data-stu-id="b12ad-206">You can test failover scenarios, work with more instances and replicas of your services.</span></span> <span data-ttu-id="b12ad-207">Modalità di cluster a un nodo è la distribuzione rapida toodo ottimizzato e la registrazione dei servizi, toohelp è convalidare rapidamente il codice mediante il runtime di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-207">One-node cluster mode is optimized toodo quick deployment and registration of services, toohelp you quickly validate code using hello Service Fabric runtime.</span></span>

<span data-ttu-id="b12ad-208">Né la modalità cluster a un nodo, né quella a cinque è un emulatore o un simulatore.</span><span class="sxs-lookup"><span data-stu-id="b12ad-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span></span> <span data-ttu-id="b12ad-209">cluster di sviluppo locale Hello esecuzioni hello stesso codice di piattaforma che si trova su un cluster con più computer.</span><span class="sxs-lookup"><span data-stu-id="b12ad-209">hello local development cluster runs hello same platform code that is found on multi-machine clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="b12ad-210">Quando si modifica la modalità di hello cluster, il cluster corrente hello viene rimosso dal sistema e viene creato un nuovo cluster.</span><span class="sxs-lookup"><span data-stu-id="b12ad-210">When you change hello cluster mode, hello current cluster is removed from your system and a new cluster is created.</span></span> <span data-ttu-id="b12ad-211">dati Hello archiviati in hello cluster viene eliminati quando si modifica la modalità del cluster.</span><span class="sxs-lookup"><span data-stu-id="b12ad-211">hello data stored in hello cluster is deleted when you change cluster mode.</span></span>
> 
> 

<span data-ttu-id="b12ad-212">toochange hello modalità tooone nodo cluster, selezionare **cambia modalità Cluster** in Gestione Cluster di Service Fabric locale hello.</span><span class="sxs-lookup"><span data-stu-id="b12ad-212">toochange hello mode tooone-node cluster, select **Switch Cluster Mode** in hello Service Fabric Local Cluster Manager.</span></span>

![Cambiare la modalità cluster][switch-cluster-mode]

<span data-ttu-id="b12ad-214">In alternativa, modificare la modalità di cluster hello con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b12ad-214">Or, change hello cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="b12ad-215">Avviare una nuova finestra di PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b12ad-215">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="b12ad-216">Eseguire lo script di installazione di cluster hello dalla cartella SDK hello:</span><span class="sxs-lookup"><span data-stu-id="b12ad-216">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="b12ad-217">La configurazione del cluster richiede alcuni istanti.</span><span class="sxs-lookup"><span data-stu-id="b12ad-217">Cluster setup takes a few moments.</span></span> <span data-ttu-id="b12ad-218">Al termine, l'output visualizzato sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b12ad-218">After setup is finished, you should see output similar to:</span></span>
   
    ![Output installazione del cluster][cluster-setup-success-1-node]

## <a name="next-steps"></a><span data-ttu-id="b12ad-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b12ad-220">Next steps</span></span>
* <span data-ttu-id="b12ad-221">Dopo aver distribuito e aggiornato alcune applicazioni precompilate, è possibile [provare a creare un'applicazione personalizzata in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="b12ad-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>
* <span data-ttu-id="b12ad-222">Tutte le azioni eseguite nel cluster locale di hello in questo articolo hello possono essere eseguite su un [cluster Azure](service-fabric-cluster-creation-via-portal.md) anche.</span><span class="sxs-lookup"><span data-stu-id="b12ad-222">All hello actions performed on hello local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span></span>
* <span data-ttu-id="b12ad-223">aggiornamento di Hello effettuate in questo articolo è stato base.</span><span class="sxs-lookup"><span data-stu-id="b12ad-223">hello upgrade that we performed in this article was basic.</span></span> <span data-ttu-id="b12ad-224">Vedere hello [documentazione relativa all'aggiornamento](service-fabric-application-upgrade.md) toolearn ulteriori informazioni sulla hello potenza e flessibilità di aggiornamento di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b12ad-224">See hello [upgrade documentation](service-fabric-application-upgrade.md) toolearn more about hello power and flexibility of Service Fabric upgrades.</span></span>

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
