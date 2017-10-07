---
title: aaaDeploy un tooAzure eseguibile esistente Service Fabric | Documenti Microsoft
description: "Procedura dettagliata sulla modalità di distribuzione di cluster di Service Fabric tooa toopackage un'applicazione esistente come un eseguibile guest, pertanto può essere"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a><span data-ttu-id="381b3-103">Distribuire un tooService eseguibile guest dell'infrastruttura</span><span class="sxs-lookup"><span data-stu-id="381b3-103">Deploy a guest executable tooService Fabric</span></span>
<span data-ttu-id="381b3-104">In Azure Service Fabric distribuito come servizio è possibile eseguire qualsiasi tipo di codice, ad esempio Node.js, Java, e C++.</span><span class="sxs-lookup"><span data-stu-id="381b3-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="381b3-105">Service Fabric si riferisce tipi toothese di servizi come file eseguibili di guest.</span><span class="sxs-lookup"><span data-stu-id="381b3-105">Service Fabric refers toothese types of services as guest executables.</span></span>

<span data-ttu-id="381b3-106">Gli eseguibili guest vengono considerati da Service Fabric come servizi senza stato.</span><span class="sxs-lookup"><span data-stu-id="381b3-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="381b3-107">Di conseguenza, vengono inseriti nei nodi di un cluster in base alla disponibilità e ad altre metriche.</span><span class="sxs-lookup"><span data-stu-id="381b3-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="381b3-108">Questo articolo viene descritto come toopackage e distribuire un cluster di Service Fabric tooa eseguibile guest, tramite Visual Studio o un'utilità della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="381b3-108">This article describes how toopackage and deploy a guest executable tooa Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="381b3-109">In questo articolo è coprire hello passaggi toopackage un eseguibile guest e distribuirlo tooService dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="381b3-109">In this article, we cover hello steps toopackage a guest executable and deploy it tooService Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="381b3-110">Vantaggi dell'esecuzione di un'eseguibile guest in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="381b3-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="381b3-111">Esistono diversi vantaggi toorunning un eseguibile in un cluster di Service Fabric guest:</span><span class="sxs-lookup"><span data-stu-id="381b3-111">There are several advantages toorunning a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="381b3-112">Disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="381b3-112">High availability.</span></span> <span data-ttu-id="381b3-113">Le applicazioni eseguite in Service Fabric sono rese altamente disponibili.</span><span class="sxs-lookup"><span data-stu-id="381b3-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="381b3-114">Service Fabric garantisce che siano in esecuzione istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="381b3-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="381b3-115">Monitoraggio dell’integrità.</span><span class="sxs-lookup"><span data-stu-id="381b3-115">Health monitoring.</span></span> <span data-ttu-id="381b3-116">Il monitoraggio dell'integrità di Service Fabric rileva se un'applicazione è in esecuzione e fornisce informazioni di diagnostica in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="381b3-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="381b3-117">Gestione del ciclo di vita delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="381b3-117">Application lifecycle management.</span></span> <span data-ttu-id="381b3-118">Oltre a fornire gli aggiornamenti senza tempi di inattività, Service Fabric fornisce una versione precedente di rollback automatico toohello se è presente un evento di stato errato segnalato durante un aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="381b3-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback toohello previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="381b3-119">Densità.</span><span class="sxs-lookup"><span data-stu-id="381b3-119">Density.</span></span> <span data-ttu-id="381b3-120">È possibile eseguire più applicazioni in un cluster, non è più necessario hello per ogni applicazione di toorun il proprio hardware.</span><span class="sxs-lookup"><span data-stu-id="381b3-120">You can run multiple applications in a cluster, which eliminates hello need for each application toorun on its own hardware.</span></span>
* <span data-ttu-id="381b3-121">Individuabilità: Tramite REST è possibile chiamare toofind servizio di Service Fabric denominazione hello altri servizi in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-121">Discoverability: Using REST you can call hello Service Fabric Naming service toofind other services in hello cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="381b3-122">Esempi</span><span class="sxs-lookup"><span data-stu-id="381b3-122">Samples</span></span>
* [<span data-ttu-id="381b3-123">Esempio per la creazione di un pacchetto e distribuzione di un file guest eseguibile</span><span class="sxs-lookup"><span data-stu-id="381b3-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="381b3-124">Esempio di guest due file eseguibili (c# e nodejs) comunicano tramite il servizio di denominazione hello tramite REST</span><span class="sxs-lookup"><span data-stu-id="381b3-124">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="381b3-125">Panoramica dei file manifesto dell'applicazione e del servizio</span><span class="sxs-lookup"><span data-stu-id="381b3-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="381b3-126">Come parte della distribuzione di un eseguibile guest, è sui pacchetti di Service Fabric toounderstand utile hello e modello di distribuzione come descritto in [modello applicativo](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="381b3-126">As part of deploying a guest executable, it is useful toounderstand hello Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="381b3-127">un modello di Service Fabric pacchetti Hello si basa su due file XML: hello manifesti dell'applicazione e servizi.</span><span class="sxs-lookup"><span data-stu-id="381b3-127">hello Service Fabric packaging model relies on two XML files: hello application and service manifests.</span></span> <span data-ttu-id="381b3-128">Hello definizione dello schema per hello ServiceManifest.xml e ApplicationManifest.xml file viene installata con hello Service Fabric SDK in *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="381b3-128">hello schema definition for hello ApplicationManifest.xml and ServiceManifest.xml files is installed with hello Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="381b3-129">**Manifesto dell'applicazione** manifesto dell'applicazione hello è un'applicazione hello toodescribe utilizzato.</span><span class="sxs-lookup"><span data-stu-id="381b3-129">**Application manifest** hello application manifest is used toodescribe hello application.</span></span> <span data-ttu-id="381b3-130">Elenca servizi hello che lo compongono e altri parametri che vengono utilizzati toodefine devono essere distribuiti come uno o più servizi, ad esempio il numero di hello di istanze.</span><span class="sxs-lookup"><span data-stu-id="381b3-130">It lists hello services that compose it, and other parameters that are used toodefine how one or more services should be deployed, such as hello number of instances.</span></span>

  <span data-ttu-id="381b3-131">In Service Fabric un'applicazione è un'unità di distribuzione e aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="381b3-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="381b3-132">Un'applicazione può essere aggiornata come una singola unità in cui vengono gestiti i potenziali errori e i potenziali ripristini dello stato precedente.</span><span class="sxs-lookup"><span data-stu-id="381b3-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="381b3-133">Service Fabric garantisce che il processo di aggiornamento hello sia l'esito è positivo, in alternativa, se l'aggiornamento di hello non riesce, non lasciare applicazione hello in uno stato sconosciuto o instabile.</span><span class="sxs-lookup"><span data-stu-id="381b3-133">Service Fabric guarantees that hello upgrade process is either successful, or, if hello upgrade fails, does not leave hello application in an unknown or unstable state.</span></span>
* <span data-ttu-id="381b3-134">**Manifesto del servizio** manifesto del servizio hello descrive i componenti di hello di un servizio.</span><span class="sxs-lookup"><span data-stu-id="381b3-134">**Service manifest** hello service manifest describes hello components of a service.</span></span> <span data-ttu-id="381b3-135">Include i dati, ad esempio hello nome e tipo di servizio e il codice e la configurazione.</span><span class="sxs-lookup"><span data-stu-id="381b3-135">It includes data, such as hello name and type of service, and its code and configuration.</span></span> <span data-ttu-id="381b3-136">Hello manifesto del servizio sono inclusi alcuni parametri aggiuntivi che possono essere utilizzati servizio hello tooconfigure dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="381b3-136">hello service manifest also includes some additional parameters that can be used tooconfigure hello service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="381b3-137">Struttura del file del pacchetto dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="381b3-137">Application package file structure</span></span>
<span data-ttu-id="381b3-138">toodeploy un tooService applicazione Fabric, un'applicazione hello deve seguire una struttura di directory predefinito.</span><span class="sxs-lookup"><span data-stu-id="381b3-138">toodeploy an application tooService Fabric, hello application should follow a predefined directory structure.</span></span> <span data-ttu-id="381b3-139">Hello Ecco un esempio di tale struttura.</span><span class="sxs-lookup"><span data-stu-id="381b3-139">hello following is an example of that structure.</span></span>

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

<span data-ttu-id="381b3-140">Hello ApplicationPackageRoot contiene file ApplicationManifest XML hello che definisce un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-140">hello ApplicationPackageRoot contains hello ApplicationManifest.xml file that defines hello application.</span></span> <span data-ttu-id="381b3-141">Una sottodirectory per ogni servizio incluso in un'applicazione hello è toocontain utilizzati tutti gli elementi necessari per il servizio hello di hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-141">A subdirectory for each service included in hello application is used toocontain all hello artifacts that hello service requires.</span></span> <span data-ttu-id="381b3-142">Le sottodirectory sono hello ServiceManifest.xml e, in genere, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="381b3-142">These subdirectories are hello ServiceManifest.xml and, typically, hello following:</span></span>

* <span data-ttu-id="381b3-143">*Code*.</span><span class="sxs-lookup"><span data-stu-id="381b3-143">*Code*.</span></span> <span data-ttu-id="381b3-144">Questa directory contiene codice hello del servizio.</span><span class="sxs-lookup"><span data-stu-id="381b3-144">This directory contains hello service code.</span></span>
* <span data-ttu-id="381b3-145">*Config*. Questa directory contiene un file Settings (e altri file, se necessario) che il servizio di hello può accedere al runtime tooretrieve specifiche impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="381b3-145">*Config*. This directory contains a Settings.xml file (and other files if necessary) that hello service can access at runtime tooretrieve specific configuration settings.</span></span>
* <span data-ttu-id="381b3-146">*Dati*.</span><span class="sxs-lookup"><span data-stu-id="381b3-146">*Data*.</span></span> <span data-ttu-id="381b3-147">Si tratta di un'ulteriore directory toostore locale dati aggiuntivi che potrebbe essere necessario servizio hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-147">This is an additional directory toostore additional local data that hello service may need.</span></span> <span data-ttu-id="381b3-148">Dati dovrebbero essere utilizzati toostore temporaneo solo dati.</span><span class="sxs-lookup"><span data-stu-id="381b3-148">Data should be used toostore only ephemeral data.</span></span> <span data-ttu-id="381b3-149">Service Fabric non directory dei dati toohello le modifiche non copia o di replica se il servizio di hello deve toobe ripristinato (ad esempio, durante il failover).</span><span class="sxs-lookup"><span data-stu-id="381b3-149">Service Fabric does not copy or replicate changes toohello data directory if hello service needs toobe relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="381b3-150">Non si dispone di hello toocreate `config` e `data` directory se non sono necessarie.</span><span class="sxs-lookup"><span data-stu-id="381b3-150">You don't have toocreate hello `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="381b3-151">Creare il pacchetto di un eseguibile esistente</span><span class="sxs-lookup"><span data-stu-id="381b3-151">Package an existing executable</span></span>
<span data-ttu-id="381b3-152">Quando il pacchetto di un eseguibile guest, è possibile scegliere entrambi toouse un modello di progetto di Visual Studio o troppo[creare manualmente il pacchetto di applicazione hello](#manually).</span><span class="sxs-lookup"><span data-stu-id="381b3-152">When packaging a guest executable, you can choose either toouse a Visual Studio project template or too[create hello application package manually](#manually).</span></span> <span data-ttu-id="381b3-153">Utilizzando Visual Studio, hello struttura del pacchetto dell'applicazione e i file manifesto vengono creati per il nuovo modello di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-153">Using Visual Studio, hello application package structure and manifest files are created by hello new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="381b3-154">toopackage modo più semplice di Hello un eseguibile in un servizio di Windows esistente è toouse Visual Studio e su Linux toouse Yeoman</span><span class="sxs-lookup"><span data-stu-id="381b3-154">hello easiest way toopackage an existing Windows executable into a service is toouse Visual Studio and on Linux toouse Yeoman</span></span>
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a><span data-ttu-id="381b3-155">Utilizzare Visual Studio toopackage e distribuire un eseguibile esistente</span><span class="sxs-lookup"><span data-stu-id="381b3-155">Use Visual Studio toopackage and deploy an existing executable</span></span>
<span data-ttu-id="381b3-156">Visual Studio fornisce un'infrastruttura a servizio toohelp modello di servizio si distribuisce un cluster di Service Fabric tooa eseguibile guest.</span><span class="sxs-lookup"><span data-stu-id="381b3-156">Visual Studio provides a Service Fabric service template toohelp you deploy a guest executable tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="381b3-157">Scegliere **File** > **Nuovo progetto** e creare un'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="381b3-157">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="381b3-158">Scegliere **eseguibile Guest** come modello di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-158">Choose **Guest Executable** as hello service template.</span></span>
3. <span data-ttu-id="381b3-159">Fare clic su **Sfoglia** cartella hello tooselect e compilare il resto di hello del servizio di hello parametri toocreate hello eseguibile.</span><span class="sxs-lookup"><span data-stu-id="381b3-159">Click **Browse** tooselect hello folder with your executable and fill in hello rest of hello parameters toocreate hello service.</span></span>
   * <span data-ttu-id="381b3-160">*Comportamento del pacchetto di codice*.</span><span class="sxs-lookup"><span data-stu-id="381b3-160">*Code Package Behavior*.</span></span> <span data-ttu-id="381b3-161">È possibile toocopy set tutto il contenuto hello del toohello cartella progetto di Visual Studio, questa opzione è utile se hello eseguibile non cambia.</span><span class="sxs-lookup"><span data-stu-id="381b3-161">Can be set toocopy all hello content of your folder toohello Visual Studio Project, which is useful if hello executable does not change.</span></span> <span data-ttu-id="381b3-162">Se si prevede che toochange eseguibile hello e si desidera hello possibilità toopick le nuove compilazioni in modo dinamico, è possibile scegliere invece toolink toohello cartella.</span><span class="sxs-lookup"><span data-stu-id="381b3-162">If you expect hello executable toochange and want hello ability toopick up new builds dynamically, you can choose toolink toohello folder instead.</span></span> <span data-ttu-id="381b3-163">Quando si crea il progetto di applicazione hello in Visual Studio, è possibile utilizzare cartelle collegate.</span><span class="sxs-lookup"><span data-stu-id="381b3-163">You can use linked folders when creating hello application project in Visual Studio.</span></span> <span data-ttu-id="381b3-164">Questo collega toohello un percorso di origine dal progetto hello, rendendo possibile il si tooupdate hello guest eseguibile di destinazione di origine.</span><span class="sxs-lookup"><span data-stu-id="381b3-164">This links toohello source location from within hello project, making it possible for you tooupdate hello guest executable in its source destination.</span></span> <span data-ttu-id="381b3-165">Tali aggiornamenti diventano parte del pacchetto di applicazione hello in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="381b3-165">Those updates become part of hello application package on build.</span></span>
   * <span data-ttu-id="381b3-166">*Programma* eseguibile hello che deve essere eseguito il servizio di hello toostart specifica.</span><span class="sxs-lookup"><span data-stu-id="381b3-166">*Program* specifies hello executable that should be run toostart hello service.</span></span>
   * <span data-ttu-id="381b3-167">*Argomenti* specifica gli argomenti di hello che devono essere passati toohello eseguibile.</span><span class="sxs-lookup"><span data-stu-id="381b3-167">*Arguments* specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="381b3-168">Può essere un elenco di parametri con argomenti.</span><span class="sxs-lookup"><span data-stu-id="381b3-168">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="381b3-169">*Cartella di lavoro* specifica cartella di lavoro hello per processo hello che verrà avviato toobe.</span><span class="sxs-lookup"><span data-stu-id="381b3-169">*WorkingFolder* specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="381b3-170">È possibile specificare tre valori:</span><span class="sxs-lookup"><span data-stu-id="381b3-170">You can specify three values:</span></span>
     * <span data-ttu-id="381b3-171">`CodeBase`Specifica la directory di lavoro hello toobe impostare toohello directory del codice nel pacchetto di applicazione hello (`Code` directory visualizzata nella hello precedente struttura di file).</span><span class="sxs-lookup"><span data-stu-id="381b3-171">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="381b3-172">`CodePackage`Specifica la directory di lavoro hello toobe impostare toohello radice del pacchetto di applicazione hello (`GuestService1Pkg` mostrato nella precedente struttura di file hello).</span><span class="sxs-lookup"><span data-stu-id="381b3-172">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="381b3-173">`Work`Specifica che il file hello vengono inserito in una sottodirectory denominata lavoro.</span><span class="sxs-lookup"><span data-stu-id="381b3-173">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="381b3-174">Assegnare un nome al servizio e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="381b3-174">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="381b3-175">Se il servizio deve disporre di un endpoint per la comunicazione, è ora possibile aggiungere hello protocollo, porta e il file ServiceManifest.xml toohello del tipo.</span><span class="sxs-lookup"><span data-stu-id="381b3-175">If your service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="381b3-176">Ad esempio: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span><span class="sxs-lookup"><span data-stu-id="381b3-176">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="381b3-177">È possibile utilizzare il pacchetto di hello e azione di pubblicazione sul cluster locale eseguendo il debug delle soluzioni di hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="381b3-177">You can now use hello package and publish action against your local cluster by debugging hello solution in Visual Studio.</span></span> <span data-ttu-id="381b3-178">Quando si è pronti, è possibile pubblicare hello applicazione tooa remota del cluster o archiviare hello soluzione toosource controllo del codice.</span><span class="sxs-lookup"><span data-stu-id="381b3-178">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span>
7. <span data-ttu-id="381b3-179">Passare come toohello fine di questo articolo di toosee tooview il servizio eseguibile guest in esecuzione in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="381b3-179">Go toohello end of this article toosee how tooview your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="381b3-180">Utilizzare Yoeman toopackage e distribuire un eseguibile esistente in Linux</span><span class="sxs-lookup"><span data-stu-id="381b3-180">Use Yoeman toopackage and deploy an existing executable on Linux</span></span>

<span data-ttu-id="381b3-181">procedura di Hello per la creazione e distribuzione di un eseguibile in Linux guest è hello come distribuzione di un'applicazione csharp o java.</span><span class="sxs-lookup"><span data-stu-id="381b3-181">hello procedure for creating and deploying a guest executable on Linux is hello same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="381b3-182">In un terminale digitare `yo azuresfguest`.</span><span class="sxs-lookup"><span data-stu-id="381b3-182">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="381b3-183">Assegnare un nome all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="381b3-183">Name your application.</span></span>
3. <span data-ttu-id="381b3-184">Nome del servizio e fornire dettagli hello, incluso il percorso dell'eseguibile hello e devono essere richiamato con i parametri di hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-184">Name your service, and provide hello details including path of hello executable and hello parameters it must be invoked with.</span></span>

<span data-ttu-id="381b3-185">Yeoman crea un pacchetto di applicazione con un'applicazione hello appropriato e i file manifesto insieme a installare e disinstallare gli script.</span><span class="sxs-lookup"><span data-stu-id="381b3-185">Yeoman creates an application package with hello appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="381b3-186">Creare manualmente il pacchetto e distribuire un eseguibile esistente</span><span class="sxs-lookup"><span data-stu-id="381b3-186">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="381b3-187">il processo di Hello di assemblaggio manualmente un eseguibile guest è basato su hello seguendo i passaggi generali:</span><span class="sxs-lookup"><span data-stu-id="381b3-187">hello process of manually packaging a guest executable is based on hello following general steps:</span></span>

1. <span data-ttu-id="381b3-188">Creare una struttura di directory hello del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="381b3-188">Create hello package directory structure.</span></span>
2. <span data-ttu-id="381b3-189">Aggiungere il file di codice e la configurazione dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-189">Add hello application's code and configuration files.</span></span>
3. <span data-ttu-id="381b3-190">Modificare i file manifesto del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-190">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="381b3-191">Modificare i file manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-191">Edit hello application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a><span data-ttu-id="381b3-192">Creare una struttura di directory del pacchetto hello</span><span class="sxs-lookup"><span data-stu-id="381b3-192">Create hello package directory structure</span></span>
<span data-ttu-id="381b3-193">Iniziare creando una struttura di directory hello, come descritto nella precedente sezione hello "Struttura di file del pacchetto di applicazione."</span><span class="sxs-lookup"><span data-stu-id="381b3-193">You can start by creating hello directory structure, as described in hello preceding section, "Application package file structure."</span></span>

### <a name="add-hello-applications-code-and-configuration-files"></a><span data-ttu-id="381b3-194">Aggiungere il file di codice e la configurazione dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="381b3-194">Add hello application's code and configuration files</span></span>
<span data-ttu-id="381b3-195">Dopo aver creato la struttura di directory hello, è possibile aggiungere file di codice e la configurazione dell'applicazione hello nella directory di codice e configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-195">After you have created hello directory structure, you can add hello application's code and configuration files under hello code and config directories.</span></span> <span data-ttu-id="381b3-196">È anche possibile creare directory aggiuntive o più sottodirectory nella directory di configurazione o del codice hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-196">You can also create additional directories or subdirectories under hello code or config directories.</span></span>

<span data-ttu-id="381b3-197">Service Fabric un `xcopy` del contenuto di hello di hello directory radice dell'applicazione pertanto non c'è nessun toouse struttura predefinita diversa da creare due directory superiore, codice e le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="381b3-197">Service Fabric does an `xcopy` of hello content of hello application root directory, so there is no predefined structure toouse other than creating two top directories, code and settings.</span></span> <span data-ttu-id="381b3-198">(ma se si desidera, è possibile scegliere nomi diversi,</span><span class="sxs-lookup"><span data-stu-id="381b3-198">(You can pick different names if you want.</span></span> <span data-ttu-id="381b3-199">Altri dettagli sono nella sezione successiva hello.)</span><span class="sxs-lookup"><span data-stu-id="381b3-199">More details are in hello next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="381b3-200">Assicurarsi di includere tutti i file hello e le dipendenze che hello esigenze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="381b3-200">Make sure that you include all hello files and dependencies that hello application needs.</span></span> <span data-ttu-id="381b3-201">Service Fabric copia hello contenuto del pacchetto di applicazione hello in tutti i nodi nel cluster hello in cui i servizi dell'applicazione hello sono toobe corso distribuito.</span><span class="sxs-lookup"><span data-stu-id="381b3-201">Service Fabric copies hello content of hello application package on all nodes in hello cluster where hello application's services are going toobe deployed.</span></span> <span data-ttu-id="381b3-202">pacchetto di Hello contiene tutto il codice hello che un'applicazione hello deve toorun.</span><span class="sxs-lookup"><span data-stu-id="381b3-202">hello package should contain all hello code that hello application needs toorun.</span></span> <span data-ttu-id="381b3-203">Non presupporre che le dipendenze di hello siano già installate.</span><span class="sxs-lookup"><span data-stu-id="381b3-203">Do not assume that hello dependencies are already installed.</span></span>
>
>

### <a name="edit-hello-service-manifest-file"></a><span data-ttu-id="381b3-204">Modificare i file manifesto del servizio hello</span><span class="sxs-lookup"><span data-stu-id="381b3-204">Edit hello service manifest file</span></span>
<span data-ttu-id="381b3-205">passaggio successivo Hello è hello tooedit hello servizio file manifesto tooinclude con le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="381b3-205">hello next step is tooedit hello service manifest file tooinclude hello following information:</span></span>

* <span data-ttu-id="381b3-206">nome Hello hello del tipo di servizio.</span><span class="sxs-lookup"><span data-stu-id="381b3-206">hello name of hello service type.</span></span> <span data-ttu-id="381b3-207">Questo è un ID di Service Fabric utilizzato tooidentify un servizio.</span><span class="sxs-lookup"><span data-stu-id="381b3-207">This is an ID that Service Fabric uses tooidentify a service.</span></span>
* <span data-ttu-id="381b3-208">comando toouse toolaunch hello applicazione Hello (ExeHost).</span><span class="sxs-lookup"><span data-stu-id="381b3-208">hello command toouse toolaunch hello application (ExeHost).</span></span>
* <span data-ttu-id="381b3-209">Tutti gli script che deve eseguire toobe tooset di un'applicazione hello (SetupEntrypoint).</span><span class="sxs-lookup"><span data-stu-id="381b3-209">Any script that needs toobe run tooset up hello application (SetupEntrypoint).</span></span>

<span data-ttu-id="381b3-210">Hello seguito è riportato un esempio di un `ServiceManifest.xml` file:</span><span class="sxs-lookup"><span data-stu-id="381b3-210">hello following is an example of a `ServiceManifest.xml` file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

<span data-ttu-id="381b3-211">Nelle sezioni che seguono Hello prese in parti diverse di hello del file hello che è necessario tooupdate.</span><span class="sxs-lookup"><span data-stu-id="381b3-211">hello following sections go over hello different parts of hello file that you need tooupdate.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="381b3-212">Aggiornare ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="381b3-212">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="381b3-213">È possibile scegliere qualsiasi nome per `ServiceTypeName`.</span><span class="sxs-lookup"><span data-stu-id="381b3-213">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="381b3-214">viene utilizzato il valore di Hello in hello `ApplicationManifest.xml` tooidentify hello servizio file.</span><span class="sxs-lookup"><span data-stu-id="381b3-214">hello value is used in hello `ApplicationManifest.xml` file tooidentify hello service.</span></span>
* <span data-ttu-id="381b3-215">Specificare `UseImplicitHost="true"`.</span><span class="sxs-lookup"><span data-stu-id="381b3-215">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="381b3-216">Questo attributo indica a Service Fabric che servizio hello è basato su un'app autonoma, quindi tutti i Service Fabric deve toodo toolaunch come un processo e monitorare l'integrità.</span><span class="sxs-lookup"><span data-stu-id="381b3-216">This attribute tells Service Fabric that hello service is based on a self-contained app, so all Service Fabric needs toodo is toolaunch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="381b3-217">Aggiornare CodePackage</span><span class="sxs-lookup"><span data-stu-id="381b3-217">Update CodePackage</span></span>
<span data-ttu-id="381b3-218">elemento CodePackage Hello Specifica percorso hello (e versione) del codice del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-218">hello CodePackage element specifies hello location (and version) of hello service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="381b3-219">Hello `Name` elemento è utilizzato toospecify hello nome della directory hello nel pacchetto di applicazione hello che contiene il codice del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-219">hello `Name` element is used toospecify hello name of hello directory in hello application package that contains hello service's code.</span></span> <span data-ttu-id="381b3-220">`CodePackage`dispone anche di hello `version` attributo.</span><span class="sxs-lookup"><span data-stu-id="381b3-220">`CodePackage` also has hello `version` attribute.</span></span> <span data-ttu-id="381b3-221">Questo può essere utilizzato toospecify hello versione del codice hello e possono anche essere utilizzato il codice del servizio di hello tooupgrade tramite l'infrastruttura di gestione del ciclo di vita dell'applicazione hello in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="381b3-221">This can be used toospecify hello version of hello code, and can also potentially be used tooupgrade hello service's code by using hello application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="381b3-222">Facoltativo: aggiornare SetupEntrypoint</span><span class="sxs-lookup"><span data-stu-id="381b3-222">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="381b3-223">elemento SetupEntryPoint Hello è toospecify usato qualsiasi file eseguibile o batch che deve essere eseguito prima che il codice del servizio hello viene avviato.</span><span class="sxs-lookup"><span data-stu-id="381b3-223">hello SetupEntryPoint element is used toospecify any executable or batch file that should be executed before hello service's code is launched.</span></span> <span data-ttu-id="381b3-224">È un passaggio facoltativo, in modo che non sia toobe inclusa se non esiste alcuna inizializzazione necessaria.</span><span class="sxs-lookup"><span data-stu-id="381b3-224">It is an optional step, so it does not need toobe included if there is no initialization required.</span></span> <span data-ttu-id="381b3-225">Hello SetupEntryPoint viene eseguita ogni volta che viene riavviato il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-225">hello SetupEntryPoint is executed every time hello service is restarted.</span></span>

<span data-ttu-id="381b3-226">Non è un solo SetupEntryPoint, gli script di installazione necessario toobe raggruppati in un file batch solo se il programma di installazione dell'applicazione hello richiede più script.</span><span class="sxs-lookup"><span data-stu-id="381b3-226">There is only one SetupEntryPoint, so setup scripts need toobe grouped in a single batch file if hello application's setup requires multiple scripts.</span></span> <span data-ttu-id="381b3-227">Hello SetupEntryPoint può eseguire qualsiasi tipo di file: file eseguibili, file batch e i cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="381b3-227">hello SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="381b3-228">Per altri dettagli, vedere l'articolo su come [configurare SetupEntryPoint](service-fabric-application-runas-security.md).</span><span class="sxs-lookup"><span data-stu-id="381b3-228">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="381b3-229">In hello sopra riportato, hello SetupEntryPoint viene eseguito un file batch denominato `LaunchConfig.cmd` che è situato nella hello `scripts` sottodirectory della directory di codice hello (presupponendo che hello cartella di lavoro viene impostato tooCodeBase).</span><span class="sxs-lookup"><span data-stu-id="381b3-229">In hello preceding example, hello SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in hello `scripts` subdirectory of hello code directory (assuming hello WorkingFolder element is set tooCodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="381b3-230">Aggiornare EntryPoint</span><span class="sxs-lookup"><span data-stu-id="381b3-230">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="381b3-231">Hello `EntryPoint` elemento nel file manifesto del servizio hello è toospecify utilizzati come servizio hello toolaunch.</span><span class="sxs-lookup"><span data-stu-id="381b3-231">hello `EntryPoint` element in hello service manifest file is used toospecify how toolaunch hello service.</span></span> <span data-ttu-id="381b3-232">Hello `ExeHost` elemento specifica hello eseguibile (e argomenti) che deve essere utilizzato il servizio di hello toolaunch.</span><span class="sxs-lookup"><span data-stu-id="381b3-232">hello `ExeHost` element specifies hello executable (and arguments) that should be used toolaunch hello service.</span></span>

* <span data-ttu-id="381b3-233">`Program`Specifica il nome di hello del file eseguibile hello che deve avviare il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-233">`Program` specifies hello name of hello executable that should start hello service.</span></span>
* <span data-ttu-id="381b3-234">`Arguments`Specifica gli argomenti di hello che devono essere passati toohello eseguibile.</span><span class="sxs-lookup"><span data-stu-id="381b3-234">`Arguments` specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="381b3-235">Può essere un elenco di parametri con argomenti.</span><span class="sxs-lookup"><span data-stu-id="381b3-235">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="381b3-236">`WorkingFolder`Specifica la directory di lavoro hello per processo hello che verrà avviato toobe.</span><span class="sxs-lookup"><span data-stu-id="381b3-236">`WorkingFolder` specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="381b3-237">È possibile specificare tre valori:</span><span class="sxs-lookup"><span data-stu-id="381b3-237">You can specify three values:</span></span>
  * <span data-ttu-id="381b3-238">`CodeBase`Specifica la directory di lavoro hello toobe impostare toohello directory del codice nel pacchetto di applicazione hello (`Code` directory hello precedente struttura di file).</span><span class="sxs-lookup"><span data-stu-id="381b3-238">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory in hello preceding file structure).</span></span>
  * <span data-ttu-id="381b3-239">`CodePackage`Specifica la directory di lavoro hello toobe impostare toohello radice del pacchetto di applicazione hello (`GuestService1Pkg` in hello precedente struttura di file).</span><span class="sxs-lookup"><span data-stu-id="381b3-239">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` in hello preceding file structure).</span></span>
    * <span data-ttu-id="381b3-240">`Work`Specifica che il file hello vengono inserito in una sottodirectory denominata lavoro.</span><span class="sxs-lookup"><span data-stu-id="381b3-240">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="381b3-241">cartella di lavoro Hello è directory di lavoro utile tooset hello corretto in modo che i percorsi relativi possono essere utilizzati da uno script di inizializzazione o di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-241">hello WorkingFolder is useful tooset hello correct working directory so that relative paths can be used by either hello application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="381b3-242">Aggiornare gli endpoint e registrarli nel servizio di denominazione per la comunicazione</span><span class="sxs-lookup"><span data-stu-id="381b3-242">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="381b3-243">In hello sopra riportato, hello `Endpoint` elemento specifica endpoint hello che un'applicazione hello può restare in ascolto.</span><span class="sxs-lookup"><span data-stu-id="381b3-243">In hello preceding example, hello `Endpoint` element specifies hello endpoints that hello application can listen on.</span></span> <span data-ttu-id="381b3-244">In questo esempio hello applicazione Node.js è in ascolto sul protocollo http sulla porta 3000.</span><span class="sxs-lookup"><span data-stu-id="381b3-244">In this example, hello Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="381b3-245">Inoltre è possibile chiedere toopublish Service Fabric questo toohello endpoint servizio di denominazione in modo da altri servizi possono individuare servizio toothis indirizzo endpoint di hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-245">Furthermore you can ask Service Fabric toopublish this endpoint toohello Naming Service so other services can discover hello endpoint address toothis service.</span></span> <span data-ttu-id="381b3-246">In questo modo toocommunicate in grado di toobe tra i servizi che sono file eseguibili di guest.</span><span class="sxs-lookup"><span data-stu-id="381b3-246">This enables you toobe able toocommunicate between services that are guest executables.</span></span>
<span data-ttu-id="381b3-247">Hello pubblicato indirizzo dell'endpoint è formato hello `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span><span class="sxs-lookup"><span data-stu-id="381b3-247">hello published endpoint address is of hello form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="381b3-248">`UriScheme` e `PathSuffix` sono attributi facoltativi.</span><span class="sxs-lookup"><span data-stu-id="381b3-248">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="381b3-249">`IPAddressOrFQDN`è hello indirizzo IP o nome di dominio completo del nodo hello questo eseguibile vengono inserito in e viene calcolato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="381b3-249">`IPAddressOrFQDN` is hello IP address or fully qualified domain name of hello node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="381b3-250">In hello riportato di seguito, una volta i servizi di hello viene distribuito, in Service Fabric Explorer visualizzato un endpoint simile troppo`http://10.1.4.92:3000/myapp/` pubblicati per l'istanza del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-250">In hello following example, once hello service is deployed, in Service Fabric Explorer you see an endpoint similar too`http://10.1.4.92:3000/myapp/` published for hello service instance.</span></span> <span data-ttu-id="381b3-251">Oppure, se si tratta di un computer locale, viene visualizzato `http://localhost:3000/myapp/`.</span><span class="sxs-lookup"><span data-stu-id="381b3-251">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="381b3-252">È possibile utilizzare questi indirizzi con [proxy inverso](service-fabric-reverseproxy.md) toocommunicate tra servizi.</span><span class="sxs-lookup"><span data-stu-id="381b3-252">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) toocommunicate between services.</span></span>

### <a name="edit-hello-application-manifest-file"></a><span data-ttu-id="381b3-253">Modificare i file manifesto dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="381b3-253">Edit hello application manifest file</span></span>
<span data-ttu-id="381b3-254">Dopo aver configurato hello `Servicemanifest.xml` file, è necessario toomake toohello alcune modifiche `ApplicationManifest.xml` file tooensure che hello vengono utilizzati il tipo di servizio e il nome corretto.</span><span class="sxs-lookup"><span data-stu-id="381b3-254">Once you have configured hello `Servicemanifest.xml` file, you need toomake some changes toohello `ApplicationManifest.xml` file tooensure that hello correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="381b3-255">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="381b3-255">ServiceManifestImport</span></span>
<span data-ttu-id="381b3-256">In hello `ServiceManifestImport` elemento, è possibile specificare uno o più servizi che si desidera tooinclude nell'app hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-256">In hello `ServiceManifestImport` element, you can specify one or more services that you want tooinclude in hello app.</span></span> <span data-ttu-id="381b3-257">Con cui vengono fatto riferimento servizi `ServiceManifestName`, che specifica il nome di hello della directory hello dove hello `ServiceManifest.xml` file si trova.</span><span class="sxs-lookup"><span data-stu-id="381b3-257">Services are referenced with `ServiceManifestName`, which specifies hello name of hello directory where hello `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="381b3-258">Configurare la registrazione</span><span class="sxs-lookup"><span data-stu-id="381b3-258">Set up logging</span></span>
<span data-ttu-id="381b3-259">Per gli eseguibili di guest, è utile toobe toosee in grado di console registri toofind out se gli script di configurazione e applicazione hello mostrano eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="381b3-259">For guest executables, it is useful toobe able toosee console logs toofind out if hello application and configuration scripts show any errors.</span></span>
<span data-ttu-id="381b3-260">È possibile configurare il reindirizzamento della console in hello `ServiceManifest.xml` file utilizzando hello `ConsoleRedirection` elemento.</span><span class="sxs-lookup"><span data-stu-id="381b3-260">Console redirection can be configured in hello `ServiceManifest.xml` file using hello `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="381b3-261">Non utilizzare mai criterio di reindirizzamento console hello in un'applicazione che viene distribuita nell'ambiente di produzione, perché ciò può influire sul failover dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-261">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="381b3-262">Usare questa opzione *solo* a scopo di sviluppo e debug locale.</span><span class="sxs-lookup"><span data-stu-id="381b3-262">*Only* use this for local development and debugging purposes.</span></span>  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="381b3-263">`ConsoleRedirection`può essere una directory di lavoro tooa tooredirect utilizzato console output (stdout e stderr).</span><span class="sxs-lookup"><span data-stu-id="381b3-263">`ConsoleRedirection` can be used tooredirect console output (both stdout and stderr) tooa working directory.</span></span> <span data-ttu-id="381b3-264">In questo modo che non siano presenti errori durante l'installazione di hello o l'esecuzione di un'applicazione hello in cluster di Service Fabric hello tooverify possibilità hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-264">This provides hello ability tooverify that there are no errors during hello setup or execution of hello application in hello Service Fabric cluster.</span></span>

<span data-ttu-id="381b3-265">`FileRetentionCount`Determina il numero di file viene salvato nella directory di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-265">`FileRetentionCount` determines how many files are saved in hello working directory.</span></span> <span data-ttu-id="381b3-266">Un valore pari a 5, ad esempio, significa che i file di log hello per le esecuzioni precedenti cinque hello vengono archiviati nella directory di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-266">A value of 5, for example, means that hello log files for hello previous five executions are stored in hello working directory.</span></span>

<span data-ttu-id="381b3-267">`FileMaxSizeInKb`Specifica dimensioni massime di hello hello dei file di log.</span><span class="sxs-lookup"><span data-stu-id="381b3-267">`FileMaxSizeInKb` specifies hello maximum size of hello log files.</span></span>

<span data-ttu-id="381b3-268">File di log vengono salvati in una directory di lavoro del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-268">Log files are saved in one of hello service's working directories.</span></span> <span data-ttu-id="381b3-269">toodetermine dove hello trovano i file, utilizzare toodetermine Service Fabric Explorer sia in esecuzione il servizio di hello nodo e la directory di lavoro viene utilizzata.</span><span class="sxs-lookup"><span data-stu-id="381b3-269">toodetermine where hello files are located, use Service Fabric Explorer toodetermine which node hello service is running on, and which working directory is being used.</span></span> <span data-ttu-id="381b3-270">Più avanti in questo articolo verrà illustrato questo processo.</span><span class="sxs-lookup"><span data-stu-id="381b3-270">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="381b3-271">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="381b3-271">Deployment</span></span>
<span data-ttu-id="381b3-272">ultimo passaggio Hello è troppo[distribuire l'applicazione](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="381b3-272">hello last step is too[deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="381b3-273">Hello seguente mostra uno script di PowerShell come toodeploy il cluster di sviluppo locale toohello applicazione, quindi avviare un nuovo servizio Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="381b3-273">hello following PowerShell script shows how toodeploy your application toohello local development cluster, and start a new Service Fabric service.</span></span>

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> <span data-ttu-id="381b3-274">[Comprimere il pacchetto di hello](service-fabric-package-apps.md#compress-a-package) prima della copia di archivio di immagini toohello se il pacchetto di hello è grande o dispone di molti file.</span><span class="sxs-lookup"><span data-stu-id="381b3-274">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store if hello package is large or has many files.</span></span> <span data-ttu-id="381b3-275">Per altre informazioni, leggere [qui](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span><span class="sxs-lookup"><span data-stu-id="381b3-275">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="381b3-276">Un servizio Service Fabric può essere distribuito in varie "configurazioni",</span><span class="sxs-lookup"><span data-stu-id="381b3-276">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="381b3-277">Ad esempio, può essere distribuito come una o più istanze, o può essere distribuito in modo che vi è un'istanza del servizio hello in ogni nodo del cluster di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-277">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of hello service on each node of hello Service Fabric cluster.</span></span>

<span data-ttu-id="381b3-278">Hello `InstanceCount` parametro di hello `New-ServiceFabricService` cmdlet viene utilizzato toospecify il numero di istanze del servizio hello deve essere avviato nel cluster di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-278">hello `InstanceCount` parameter of hello `New-ServiceFabricService` cmdlet is used toospecify how many instances of hello service should be launched in hello Service Fabric cluster.</span></span> <span data-ttu-id="381b3-279">È possibile impostare hello `InstanceCount` valore, a seconda di tipo hello dell'applicazione che si desidera distribuire.</span><span class="sxs-lookup"><span data-stu-id="381b3-279">You can set hello `InstanceCount` value, depending on hello type of application that you are deploying.</span></span> <span data-ttu-id="381b3-280">gli scenari più comuni di Hello due sono:</span><span class="sxs-lookup"><span data-stu-id="381b3-280">hello two most common scenarios are:</span></span>

* <span data-ttu-id="381b3-281">`InstanceCount = "1"`.</span><span class="sxs-lookup"><span data-stu-id="381b3-281">`InstanceCount = "1"`.</span></span> <span data-ttu-id="381b3-282">In questo caso, solo un'istanza del servizio hello viene distribuita in cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-282">In this case, only one instance of hello service is deployed in hello cluster.</span></span> <span data-ttu-id="381b3-283">Utilità di pianificazione dell'infrastruttura servizio determina quale servizio hello nodo verrà distribuita in toobe.</span><span class="sxs-lookup"><span data-stu-id="381b3-283">Service Fabric's scheduler determines which node hello service is going toobe deployed on.</span></span>
* <span data-ttu-id="381b3-284">`InstanceCount ="-1"`.</span><span class="sxs-lookup"><span data-stu-id="381b3-284">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="381b3-285">In questo caso, un'istanza del servizio hello viene distribuita in ogni nodo nel cluster di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-285">In this case, one instance of hello service is deployed on every node in hello Service Fabric cluster.</span></span> <span data-ttu-id="381b3-286">risultato Hello è la presenza di istanze (un unico) del servizio di hello per ogni nodo nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-286">hello result is having one (and only one) instance of hello service for each node in hello cluster.</span></span>

<span data-ttu-id="381b3-287">Infatti un'utile configurazione per le applicazioni front-end (ad esempio, un endpoint REST), le applicazioni client necessitano troppo "connettersi" tooany dei nodi di hello nell'endpoint di hello cluster toouse hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-287">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need too"connect" tooany of hello nodes in hello cluster toouse hello endpoint.</span></span> <span data-ttu-id="381b3-288">Questa configurazione è utilizzabile anche quando, ad esempio, tutti i nodi del cluster di Service Fabric hello sono connessi tooa bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="381b3-288">This configuration can also be used when, for example, all nodes of hello Service Fabric cluster are connected tooa load balancer.</span></span> <span data-ttu-id="381b3-289">Il traffico client può quindi essere distribuito in servizio hello in esecuzione in tutti i nodi del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-289">Client traffic can then be distributed across hello service that is running on all nodes in hello cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="381b3-290">Verificare l'applicazione in esecuzione</span><span class="sxs-lookup"><span data-stu-id="381b3-290">Check your running application</span></span>
<span data-ttu-id="381b3-291">In Service Fabric Explorer, identificare il nodo hello in cui è in esecuzione il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-291">In Service Fabric Explorer, identify hello node where hello service is running.</span></span> <span data-ttu-id="381b3-292">In questo esempio è in esecuzione in Node1:</span><span class="sxs-lookup"><span data-stu-id="381b3-292">In this example, it runs on Node1:</span></span>

![Nodo in cui è in esecuzione il servizio](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="381b3-294">Se si passa toohello nodo e passare toohello applicazione, viene visualizzato informazioni essenziali nodo hello, incluso il percorso su disco.</span><span class="sxs-lookup"><span data-stu-id="381b3-294">If you navigate toohello node and browse toohello application, you see hello essential node information, including its location on disk.</span></span>

![Percorso sul disco](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="381b3-296">Se si seleziona toohello directory tramite Esplora Server, è possibile trovare la directory di lavoro hello e la cartella di registro del servizio di hello, come illustrato nella seguente schermata hello:</span><span class="sxs-lookup"><span data-stu-id="381b3-296">If you browse toohello directory by using Server Explorer, you can find hello working directory and hello service's log folder, as shown in hello following screenshot:</span></span> 

![Percorso del log](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="381b3-298">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="381b3-298">Next steps</span></span>
<span data-ttu-id="381b3-299">In questo articolo, si è appreso come toopackage un eseguibile guest e distribuirlo tooService dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="381b3-299">In this article, you have learned how toopackage a guest executable and deploy it tooService Fabric.</span></span> <span data-ttu-id="381b3-300">Vedere i seguenti articoli per le informazioni correlate e attività hello.</span><span class="sxs-lookup"><span data-stu-id="381b3-300">See hello following articles for related information and tasks.</span></span>

* <span data-ttu-id="381b3-301">[Esempio per la creazione del package e distribuzione di un eseguibile guest](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), tra cui una versione preliminare toohello collegamento dello strumento di creazione di pacchetti hello</span><span class="sxs-lookup"><span data-stu-id="381b3-301">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link toohello prerelease of hello packaging tool</span></span>
* [<span data-ttu-id="381b3-302">Esempio di guest due file eseguibili (c# e nodejs) comunicano tramite il servizio di denominazione hello tramite REST</span><span class="sxs-lookup"><span data-stu-id="381b3-302">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="381b3-303">Distribuire più eseguibili guest</span><span class="sxs-lookup"><span data-stu-id="381b3-303">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="381b3-304">Creare la prima applicazione Service Fabric in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="381b3-304">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
