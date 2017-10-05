---
title: Distribuire e aggiornare localmente i microservizi di Azure | Documentazione Microsoft
description: Informazioni su come configurare un cluster di Service Fabric locale, distribuire un'applicazione esistente al suo interno e quindi aggiornare l'applicazione.
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
ms.openlocfilehash: 359677972c7e1fa3f7435052021ddfae5b1ed85e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a><span data-ttu-id="4f024-103">Introduzione alla distribuzione e all'aggiornamento di applicazioni nel cluster locale</span><span class="sxs-lookup"><span data-stu-id="4f024-103">Get started with deploying and upgrading applications on your local cluster</span></span>
<span data-ttu-id="4f024-104">Azure Service Fabric SDK include un ambiente di sviluppo locale completo che può essere usato per iniziare rapidamente a distribuire e gestire applicazioni in un cluster locale.</span><span class="sxs-lookup"><span data-stu-id="4f024-104">The Azure Service Fabric SDK includes a full local development environment that you can use to quickly get started with deploying and managing applications on a local cluster.</span></span> <span data-ttu-id="4f024-105">Questo articolo descrive come creare un cluster locale, distribuire un'applicazione esistente nel cluster e quindi aggiornare l'applicazione a una nuova versione usando Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4f024-105">In this article, you create a local cluster, deploy an existing application to it, and then upgrade that application to a new version, all from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="4f024-106">Questo articolo presuppone che l' [ambiente di sviluppo sia già stato configurato](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4f024-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span></span>
> 
> 

## <a name="create-a-local-cluster"></a><span data-ttu-id="4f024-107">Creare un cluster locale</span><span class="sxs-lookup"><span data-stu-id="4f024-107">Create a local cluster</span></span>
<span data-ttu-id="4f024-108">Un cluster di Service Fabric rappresenta un set di risorse hardware in cui è possibile distribuire le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4f024-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span></span> <span data-ttu-id="4f024-109">In genere un cluster è costituito da un minimo di 5 fino a diverse migliaia di macchine virtuali,</span><span class="sxs-lookup"><span data-stu-id="4f024-109">Typically, a cluster is made up of anywhere from five to many thousands of machines.</span></span> <span data-ttu-id="4f024-110">tuttavia Service Fabric SDK include una configurazione cluster che può essere eseguita in una singola macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4f024-110">However, the Service Fabric SDK includes a cluster configuration that can run on a single machine.</span></span>

<span data-ttu-id="4f024-111">È importante comprendere che il cluster locale di Service Fabric non è un emulatore o un simulatore.</span><span class="sxs-lookup"><span data-stu-id="4f024-111">It is important to understand that the Service Fabric local cluster is not an emulator or simulator.</span></span> <span data-ttu-id="4f024-112">Esegue lo stesso codice della piattaforma eseguito nei cluster costituiti da più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4f024-112">It runs the same platform code that is found on multi-machine clusters.</span></span> <span data-ttu-id="4f024-113">La differenza sta nel fatto che esegue in una sola macchina virtuale i processi della piattaforma che normalmente vengono eseguiti in cinque macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4f024-113">The only difference is that it runs the platform processes that are normally spread across five machines on one machine.</span></span>

<span data-ttu-id="4f024-114">L'SDK fornisce due modi per configurare un cluster locale: uno script di Windows PowerShell e l'app dell'area di notifica Local Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="4f024-114">The SDK provides two ways to set up a local cluster: a Windows PowerShell script and the Local Cluster Manager system tray app.</span></span> <span data-ttu-id="4f024-115">Per questa esercitazione si userà lo script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4f024-115">In this tutorial, we use the PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="4f024-116">Se è già stato creato un cluster locale con la distribuzione di un'applicazione da Visual Studio, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="4f024-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span></span>
> 
> 

1. <span data-ttu-id="4f024-117">Avviare una nuova finestra di PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4f024-117">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="4f024-118">Eseguire lo script di installazione del cluster dalla cartella dell'SDK:</span><span class="sxs-lookup"><span data-stu-id="4f024-118">Run the cluster setup script from the SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    <span data-ttu-id="4f024-119">La configurazione del cluster richiede alcuni istanti.</span><span class="sxs-lookup"><span data-stu-id="4f024-119">Cluster setup takes a few moments.</span></span> <span data-ttu-id="4f024-120">Al termine, l'output visualizzato sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4f024-120">After setup is finished, you should see output similar to:</span></span>
   
    ![Output installazione del cluster][cluster-setup-success]
   
    <span data-ttu-id="4f024-122">A questo punto, è possibile provare a distribuire un'applicazione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="4f024-122">You are now ready to try deploying an application to your cluster.</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="4f024-123">Distribuire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="4f024-123">Deploy an application</span></span>
<span data-ttu-id="4f024-124">Service Fabric SDK include un set avanzato di framework e strumenti di sviluppo per la creazione di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4f024-124">The Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span></span> <span data-ttu-id="4f024-125">Per informazioni su come creare applicazioni in Visual Studio, vedere [Creare la prima applicazione di Service Fabric in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="4f024-125">If you are interested in learning how to create applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>

<span data-ttu-id="4f024-126">In questa esercitazione si userà un'applicazione di esempio esistente, denominata WordCount, per concentrare l'attenzione sugli aspetti di gestione della piattaforma: distribuzione, monitoraggio e aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="4f024-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on the management aspects of the platform: deployment, monitoring, and upgrade.</span></span>

1. <span data-ttu-id="4f024-127">Avviare una nuova finestra di PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4f024-127">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="4f024-128">Importare il modulo PowerShell di Service Fabric SDK.</span><span class="sxs-lookup"><span data-stu-id="4f024-128">Import the Service Fabric SDK PowerShell module.</span></span>
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. <span data-ttu-id="4f024-129">Creare una directory per archiviare l'applicazione scaricata e distribuita, ad esempio C:\ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="4f024-129">Create a directory to store the application that you download and deploy, such as C:\ServiceFabric.</span></span>
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. <span data-ttu-id="4f024-130">[Scaricare l'applicazione WordCount](http://aka.ms/servicefabric-wordcountapp) nel percorso creato.</span><span class="sxs-lookup"><span data-stu-id="4f024-130">[Download the WordCount application](http://aka.ms/servicefabric-wordcountapp) to the location you created.</span></span>  <span data-ttu-id="4f024-131">Nota: il browser Microsoft Edge salva il file con l'estensione *zip* .</span><span class="sxs-lookup"><span data-stu-id="4f024-131">Note: the Microsoft Edge browser saves the file with a *.zip* extension.</span></span>  <span data-ttu-id="4f024-132">Modificare l'estensione di file in *sfpkg*.</span><span class="sxs-lookup"><span data-stu-id="4f024-132">Change the file extension to *.sfpkg*.</span></span>
5. <span data-ttu-id="4f024-133">Connettersi al cluster locale:</span><span class="sxs-lookup"><span data-stu-id="4f024-133">Connect to the local cluster:</span></span>
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. <span data-ttu-id="4f024-134">Creare una nuova applicazione con comando di distribuzione dell'SDK specificando il nome e il percorso del pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4f024-134">Create a new application using the SDK's deployment command with a name and a path to the application package.</span></span>
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="4f024-135">Se l'operazione viene eseguita correttamente, viene visualizzato l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="4f024-135">If all goes well, you should see the following output:</span></span>
   
    ![Distribuzione di un'applicazione nel cluster locale][deploy-app-to-local-cluster]
7. <span data-ttu-id="4f024-137">Per visualizzare l'applicazione in funzione, avviare il browser e passare a [http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span><span class="sxs-lookup"><span data-stu-id="4f024-137">To see the application in action, launch the browser and navigate to [http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span></span> <span data-ttu-id="4f024-138">Dovrebbe essere visualizzato:</span><span class="sxs-lookup"><span data-stu-id="4f024-138">You should see:</span></span>
   
    ![Interfaccia utente dell'applicazione distribuita][deployed-app-ui]
   
    <span data-ttu-id="4f024-140">L'applicazione WordCount è semplice.</span><span class="sxs-lookup"><span data-stu-id="4f024-140">The WordCount application is simple.</span></span> <span data-ttu-id="4f024-141">Include il codice JavaScript lato client per generare "parole" casuali di cinque caratteri, che vengono quindi inoltrate all'applicazione tramite l'API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4f024-141">It includes client-side JavaScript code to generate random five-character "words", which are then relayed to the application via ASP.NET Web API.</span></span> <span data-ttu-id="4f024-142">Un servizio con stato tiene traccia del numero di parole conteggiate,</span><span class="sxs-lookup"><span data-stu-id="4f024-142">A stateful service tracks the number of words counted.</span></span> <span data-ttu-id="4f024-143">che vengono partizionate in base al primo carattere della parola.</span><span class="sxs-lookup"><span data-stu-id="4f024-143">They are partitioned based on the first character of the word.</span></span> <span data-ttu-id="4f024-144">È possibile trovare il codice sorgente per l'app WordCount negli [esempi introduttivi classici](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span><span class="sxs-lookup"><span data-stu-id="4f024-144">You can find the source code for the WordCount app in the [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span></span>
   
    <span data-ttu-id="4f024-145">L'applicazione distribuita contiene quattro partizioni.</span><span class="sxs-lookup"><span data-stu-id="4f024-145">The application that we deployed contains four partitions.</span></span> <span data-ttu-id="4f024-146">Le parole che iniziano con le lettere dalla A alla G vengono archiviate nella prima partizione, quelle che iniziano con le lettere dalla H alla N nella seconda partizione e così via.</span><span class="sxs-lookup"><span data-stu-id="4f024-146">So words beginning with A through G are stored in the first partition, words beginning with H through N are stored in the second partition, and so on.</span></span>

## <a name="view-application-details-and-status"></a><span data-ttu-id="4f024-147">Visualizzare i dettagli e lo stato dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="4f024-147">View application details and status</span></span>
<span data-ttu-id="4f024-148">Una volta distribuita l'applicazione, si osserveranno alcuni dettagli dell'app in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4f024-148">Now that we have deployed the application, let's look at some of the app details in PowerShell.</span></span>

1. <span data-ttu-id="4f024-149">Eseguire una query per individuare tutte le applicazioni nel cluster:</span><span class="sxs-lookup"><span data-stu-id="4f024-149">Query all deployed applications on the cluster:</span></span>
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    <span data-ttu-id="4f024-150">Partendo dal presupposto che è stata distribuita solo l'app WordCount, verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4f024-150">Assuming that you have only deployed the WordCount app, you see something similar to:</span></span>
   
    ![Query per individuare tutte le applicazioni distribuite in PowerShell][ps-getsfapp]
2. <span data-ttu-id="4f024-152">Passare al livello successivo eseguendo una query per trovare il set di servizi inclusi nell'applicazione WordCount.</span><span class="sxs-lookup"><span data-stu-id="4f024-152">Go to the next level by querying the set of services that are included in the WordCount application.</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Elenco dei servizi per l'applicazione in PowerShell][ps-getsfsvc]
   
    <span data-ttu-id="4f024-154">L'applicazione è costituita da due servizi: il front-end Web e il servizio con stato che gestisce le parole.</span><span class="sxs-lookup"><span data-stu-id="4f024-154">The application is made up of two services, the web front end, and the stateful service that manages the words.</span></span>
3. <span data-ttu-id="4f024-155">Osservare infine l'elenco di partizioni per WordCountService:</span><span class="sxs-lookup"><span data-stu-id="4f024-155">Finally, look at the list of partitions for WordCountService:</span></span>
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Visualizzazione delle partizioni del servizio in PowerShell][ps-getsfpartitions]
   
    <span data-ttu-id="4f024-157">Il set di comandi usati, come tutti i comandi di PowerShell per Service Fabric, è disponibile per tutti i cluster a cui ci si connette, locali o remoti.</span><span class="sxs-lookup"><span data-stu-id="4f024-157">The set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span></span>
   
    <span data-ttu-id="4f024-158">Per un'interazione più visiva con il cluster, è possibile usare lo strumento basato sul Web Service Fabric Explorer, digitando l'indirizzo [http://localhost:19080/Explorer](http://localhost:19080/Explorer) nella barra degli indirizzi del browser.</span><span class="sxs-lookup"><span data-stu-id="4f024-158">For a more visual way to interact with the cluster, you can use the web-based Service Fabric Explorer tool by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer) in the browser.</span></span>
   
    ![Visualizzazione dei dettagli dell'applicazione in Service Fabric Explorer][sfx-service-overview]
   
   > [!NOTE]
   > <span data-ttu-id="4f024-160">Per altre informazioni su Service Fabric Explorer, vedere [Visualizzazione del cluster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="4f024-160">To learn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
   > 
   > 

## <a name="upgrade-an-application"></a><span data-ttu-id="4f024-161">Aggiornare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="4f024-161">Upgrade an application</span></span>
<span data-ttu-id="4f024-162">Con l'infrastruttura di servizi è possibile eseguire aggiornamenti senza tempi di inattività, grazie al monitoraggio dell'integrità dell'applicazione durante il rollout nel cluster.</span><span class="sxs-lookup"><span data-stu-id="4f024-162">Service Fabric provides no-downtime upgrades by monitoring the health of the application as it rolls out across the cluster.</span></span> <span data-ttu-id="4f024-163">Eseguire un aggiornamento dell'applicazione WordCount.</span><span class="sxs-lookup"><span data-stu-id="4f024-163">Perform an upgrade of the WordCount application.</span></span>

<span data-ttu-id="4f024-164">La nuova versione dell'applicazione ora conta solo le parole che iniziano con una vocale.</span><span class="sxs-lookup"><span data-stu-id="4f024-164">The new version of the application now counts only words that begin with a vowel.</span></span> <span data-ttu-id="4f024-165">Durante il rollout dell'aggiornamento si noteranno due variazioni nel comportamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4f024-165">As the upgrade rolls out, we see two changes in the application's behavior.</span></span> <span data-ttu-id="4f024-166">In primo luogo, l'incremento del conteggio dovrebbe rallentare, perché viene conteggiato un minor numero di parole.</span><span class="sxs-lookup"><span data-stu-id="4f024-166">First, the rate at which the count grows should slow, since fewer words are being counted.</span></span> <span data-ttu-id="4f024-167">Quindi, poiché la prima partizione contiene due vocali (A ed E) e tutte le altre ne contengono una, a un certo punto il conteggio della prima inizierà a superare quello delle altre.</span><span class="sxs-lookup"><span data-stu-id="4f024-167">Second, since the first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start to outpace the others.</span></span>

1. <span data-ttu-id="4f024-168">[Scaricare il pacchetto WordCount versione 2](http://aka.ms/servicefabric-wordcountappv2) e salvarlo nello stesso percorso in cui è stato scaricato il pacchetto versione 1.</span><span class="sxs-lookup"><span data-stu-id="4f024-168">[Download the WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) to the same location where you downloaded the version 1 package.</span></span>
2. <span data-ttu-id="4f024-169">Tornare alla finestra di PowerShell e usare il comando di aggiornamento dell'SDK per registrare la nuova versione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="4f024-169">Return to your PowerShell window and use the SDK's upgrade command to register the new version in the cluster.</span></span> <span data-ttu-id="4f024-170">Iniziare quindi ad aggiornare l'applicazione fabric:/WordCount.</span><span class="sxs-lookup"><span data-stu-id="4f024-170">Then begin upgrading the fabric:/WordCount application.</span></span>
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    <span data-ttu-id="4f024-171">Quando inizia l'aggiornamento, in PowerShell verrà visualizzato l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="4f024-171">You should see the following output in PowerShell as the upgrade begins.</span></span>
   
    ![Stato dell'aggiornamento in PowerShell][ps-appupgradeprogress]
3. <span data-ttu-id="4f024-173">Sarà più facile monitorare lo stato dell'aggiornamento da Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="4f024-173">While the upgrade is proceeding, you may find it easier to monitor its status from Service Fabric Explorer.</span></span> <span data-ttu-id="4f024-174">Avviare una finestra del browser e passare all'indirizzo [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="4f024-174">Launch a browser window and navigate to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="4f024-175">Espandere **Applicazioni** nell'albero a sinistra, quindi scegliere **WordCount** e infine **fabric:/WordCount**.</span><span class="sxs-lookup"><span data-stu-id="4f024-175">Expand **Applications** in the tree on the left, then choose **WordCount**, and finally **fabric:/WordCount**.</span></span> <span data-ttu-id="4f024-176">Nella scheda Informazioni di base viene visualizzato lo stato dell'operazione di aggiornamento nei domini di aggiornamento del cluster.</span><span class="sxs-lookup"><span data-stu-id="4f024-176">In the essentials tab, you see the status of the upgrade as it proceeds through the cluster's upgrade domains.</span></span>
   
    ![Stato dell'aggiornamento in Service Fabric Explorer][sfx-upgradeprogress]
   
    <span data-ttu-id="4f024-178">Durante l'operazione di aggiornamento in ogni dominio vengono eseguiti controlli di integrità, per garantire che il comportamento dell'applicazione risulti corretto.</span><span class="sxs-lookup"><span data-stu-id="4f024-178">As the upgrade proceeds through each domain, health checks are performed to ensure that the application is behaving properly.</span></span>
4. <span data-ttu-id="4f024-179">Se si esegue di nuovo la query precedente per il set di servizi nell'applicazione fabric:/WordCount, si noterà che la versione di WordCountService è cambiata, mentre la versione di WordCountWebService è rimasta la stessa:</span><span class="sxs-lookup"><span data-stu-id="4f024-179">If you rerun the earlier query for the set of services in the fabric:/WordCount application, notice that the WordCountService version changed but the WordCountWebService version did not:</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Query per individuare i servizi dell'applicazione dopo l'aggiornamento][ps-getsfsvc-postupgrade]
   
    <span data-ttu-id="4f024-181">Questo esempio illustra il modo in cui Service Fabric gestisce gli aggiornamenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4f024-181">This example highlights how Service Fabric manages application upgrades.</span></span> <span data-ttu-id="4f024-182">Agisce solo sul set di servizi, o sui pacchetti di codice o di configurazione all'interno di tali servizi, che sono stati modificati, accelerando il processo di aggiornamento e aumentandone l'affidabilità.</span><span class="sxs-lookup"><span data-stu-id="4f024-182">It touches only the set of services (or code/configuration packages within those services) that have changed, which makes the process of upgrading faster and more reliable.</span></span>
5. <span data-ttu-id="4f024-183">Infine, tornare di nuovo alla finestra del browser per osservare il comportamento della nuova versione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4f024-183">Finally, return to the browser to observe the behavior of the new application version.</span></span> <span data-ttu-id="4f024-184">Come previsto, il conteggio aumenta più lentamente e la prima partizione presenta un volume maggiore di quello delle altre.</span><span class="sxs-lookup"><span data-stu-id="4f024-184">As expected, the count progresses more slowly, and the first partition ends up with slightly more of the volume.</span></span>
   
    ![Visualizzazione della nuova versione dell'applicazione nel browser][deployed-app-ui-v2]

## <a name="cleaning-up"></a><span data-ttu-id="4f024-186">+ Cleaning up</span><span class="sxs-lookup"><span data-stu-id="4f024-186">Cleaning up</span></span>
<span data-ttu-id="4f024-187">Prima di concludere, è importante ricordare che il cluster locale è reale.</span><span class="sxs-lookup"><span data-stu-id="4f024-187">Before wrapping up, it's important to remember that the local cluster is real.</span></span> <span data-ttu-id="4f024-188">L'esecuzione delle applicazioni continua in background finché non vengono rimosse.</span><span class="sxs-lookup"><span data-stu-id="4f024-188">Applications continue to run in the background until you remove them.</span></span>  <span data-ttu-id="4f024-189">A seconda della natura delle app, un'app in esecuzione può richiedere risorse significative del computer.</span><span class="sxs-lookup"><span data-stu-id="4f024-189">Depending on the nature of your apps, a running app can take up significant resources on your machine.</span></span> <span data-ttu-id="4f024-190">Sono disponibili diverse opzioni per gestire le applicazioni e il cluster:</span><span class="sxs-lookup"><span data-stu-id="4f024-190">You have several options to manage applications and the cluster:</span></span>

1. <span data-ttu-id="4f024-191">Per rimuovere una singola applicazione con tutti i dati, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4f024-191">To remove an individual application and all it's data, run the following command:</span></span>
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="4f024-192">In alternativa, eliminare l'applicazione dal menu **AZIONI** in Service Fabric Explorer o dal menu di scelta rapida nella vista elenco sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4f024-192">Or, delete the application from the Service Fabric Explorer **ACTIONS** menu or the context menu in the left-hand application list view.</span></span>
   
    ![Eliminare un'applicazione in Service Fabric Explorer][sfe-delete-application]
2. <span data-ttu-id="4f024-194">Dopo aver eliminato l'applicazione dal cluster, annullare la registrazione delle versioni 1.0.0 e 2.0.0 del tipo di applicazione WordCount.</span><span class="sxs-lookup"><span data-stu-id="4f024-194">After deleting the application from the cluster, unregister versions 1.0.0 and 2.0.0 of the WordCount application type.</span></span> <span data-ttu-id="4f024-195">L'operazione di eliminazione rimuove i pacchetti dell'applicazione, inclusi il codice e la configurazione, dall'archivio immagini del cluster.</span><span class="sxs-lookup"><span data-stu-id="4f024-195">Deletion removes the application packages, including the code and configuration, from the cluster's image store.</span></span>
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    <span data-ttu-id="4f024-196">In alternativa, in Service Fabric Explorer scegliere **Unprovision Type** (Annulla provisioning del tipo) per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4f024-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for the application.</span></span>
3. <span data-ttu-id="4f024-197">Per arrestare il cluster mantenendo i dati applicazione e le tracce, fare clic su **Stop Local Cluster** (Arresta cluster locale) nell'app dell'area di notifica.</span><span class="sxs-lookup"><span data-stu-id="4f024-197">To shut down the cluster but keep the application data and traces, click **Stop Local Cluster** in the system tray app.</span></span>
4. <span data-ttu-id="4f024-198">Per eliminare completamente il cluster, fare clic su **Remove Local Cluster** (Rimuovi cluster locale) nell'app dell'area di notifica.</span><span class="sxs-lookup"><span data-stu-id="4f024-198">To delete the cluster entirely, click **Remove Local Cluster** in the system tray app.</span></span> <span data-ttu-id="4f024-199">Questa opzione comporterà un'altra distribuzione lenta la prossima volta che si preme F5 in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4f024-199">This option will result in another slow deployment the next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="4f024-200">Rimuovere il cluster locale solo se non si prevede di usarlo per un certo periodo o se è necessario recuperare risorse.</span><span class="sxs-lookup"><span data-stu-id="4f024-200">Remove the local cluster only if you don't intend to use it for some time or if you need to reclaim resources.</span></span>

## <a name="one-node-and-five-node-cluster-mode"></a><span data-ttu-id="4f024-201">Modalità cluster a un nodo e a cinque nodi</span><span class="sxs-lookup"><span data-stu-id="4f024-201">One-node and five-node cluster mode</span></span>
<span data-ttu-id="4f024-202">Quando si sviluppano applicazioni, ci si ritroverà spesso a eseguire rapide iterazioni di scrittura di codice, debug, modifica del codice e debug.</span><span class="sxs-lookup"><span data-stu-id="4f024-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span></span> <span data-ttu-id="4f024-203">Per ottimizzare questo processo, il cluster locale può essere eseguito in due modalità: a un nodo o a cinque nodi.</span><span class="sxs-lookup"><span data-stu-id="4f024-203">To help optimize this process, the local cluster can run in two modes: one-node or five-node.</span></span> <span data-ttu-id="4f024-204">Entrambe le modalità cluster presentano vantaggi.</span><span class="sxs-lookup"><span data-stu-id="4f024-204">Both cluster modes have their benefits.</span></span> <span data-ttu-id="4f024-205">La modalità cluster a cinque nodi consente di usare un vero cluster.</span><span class="sxs-lookup"><span data-stu-id="4f024-205">Five-node cluster mode enables you to work with a real cluster.</span></span> <span data-ttu-id="4f024-206">È possibile testare gli scenari di failover e usare più istanze e repliche dei servizi.</span><span class="sxs-lookup"><span data-stu-id="4f024-206">You can test failover scenarios, work with more instances and replicas of your services.</span></span> <span data-ttu-id="4f024-207">La modalità cluster a un nodo è ottimizzata per eseguire rapidamente la distribuzione e la registrazione dei servizi e convalidare quindi velocemente il codice usando il runtime di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4f024-207">One-node cluster mode is optimized to do quick deployment and registration of services, to help you quickly validate code using the Service Fabric runtime.</span></span>

<span data-ttu-id="4f024-208">Né la modalità cluster a un nodo, né quella a cinque è un emulatore o un simulatore.</span><span class="sxs-lookup"><span data-stu-id="4f024-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span></span> <span data-ttu-id="4f024-209">Il cluster di sviluppo locale esegue lo stesso codice della piattaforma eseguito nei cluster costituiti da più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4f024-209">The local development cluster runs the same platform code that is found on multi-machine clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="4f024-210">Quando si cambia la modalità cluster, il cluster corrente viene rimosso dal sistema e viene creato un nuovo cluster.</span><span class="sxs-lookup"><span data-stu-id="4f024-210">When you change the cluster mode, the current cluster is removed from your system and a new cluster is created.</span></span> <span data-ttu-id="4f024-211">Quando si cambia la modalità cluster, i dati archiviati nel cluster vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="4f024-211">The data stored in the cluster is deleted when you change cluster mode.</span></span>
> 
> 

<span data-ttu-id="4f024-212">Per cambiare la modalità cluster con un cluster a un nodo, selezionare **Switch Cluster Mode** (Cambia modalità cluster) in Local Cluster Manager (Gestione cluster locale) di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4f024-212">To change the mode to one-node cluster, select **Switch Cluster Mode** in the Service Fabric Local Cluster Manager.</span></span>

![Cambiare la modalità cluster][switch-cluster-mode]

<span data-ttu-id="4f024-214">In alternativa, modificare la modalità di cluster usando PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4f024-214">Or, change the cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="4f024-215">Avviare una nuova finestra di PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4f024-215">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="4f024-216">Eseguire lo script di installazione del cluster dalla cartella dell'SDK:</span><span class="sxs-lookup"><span data-stu-id="4f024-216">Run the cluster setup script from the SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="4f024-217">La configurazione del cluster richiede alcuni istanti.</span><span class="sxs-lookup"><span data-stu-id="4f024-217">Cluster setup takes a few moments.</span></span> <span data-ttu-id="4f024-218">Al termine, l'output visualizzato sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4f024-218">After setup is finished, you should see output similar to:</span></span>
   
    ![Output installazione del cluster][cluster-setup-success-1-node]

## <a name="next-steps"></a><span data-ttu-id="4f024-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4f024-220">Next steps</span></span>
* <span data-ttu-id="4f024-221">Dopo aver distribuito e aggiornato alcune applicazioni precompilate, è possibile [provare a creare un'applicazione personalizzata in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="4f024-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>
* <span data-ttu-id="4f024-222">Tutte le azioni eseguite nel cluster locale descritte in questo articolo possono essere eseguite anche in un [cluster di Azure](service-fabric-cluster-creation-via-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="4f024-222">All the actions performed on the local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span></span>
* <span data-ttu-id="4f024-223">L'aggiornamento eseguito in questo articolo è semplice.</span><span class="sxs-lookup"><span data-stu-id="4f024-223">The upgrade that we performed in this article was basic.</span></span> <span data-ttu-id="4f024-224">Per altre informazioni sulle potenzialità e sulla flessibilità degli aggiornamenti di Service Fabric, vedere la [documentazione relativa all'aggiornamento](service-fabric-application-upgrade.md) .</span><span class="sxs-lookup"><span data-stu-id="4f024-224">See the [upgrade documentation](service-fabric-application-upgrade.md) to learn more about the power and flexibility of Service Fabric upgrades.</span></span>

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
