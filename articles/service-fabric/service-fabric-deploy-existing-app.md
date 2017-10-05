---
title: Distribuire un eseguibile esistente in Azure Service Fabric | Documentazione Microsoft
description: Procedura dettagliata su come creare il pacchetto di un'applicazione esistente come eseguibile guest, in modo da consentirne la distribuzione in un cluster di Service Fabric
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
ms.openlocfilehash: a1db3dda674ffe43587333d88f3816549af3019c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-guest-executable-to-service-fabric"></a><span data-ttu-id="f0fd1-103">Distribuire un eseguibile guest in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f0fd1-103">Deploy a guest executable to Service Fabric</span></span>
<span data-ttu-id="f0fd1-104">In Azure Service Fabric distribuito come servizio è possibile eseguire qualsiasi tipo di codice, ad esempio Node.js, Java, e C++.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="f0fd1-105">Service Fabric fa riferimento a questi tipi di servizi come eseguibili guest.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-105">Service Fabric refers to these types of services as guest executables.</span></span>

<span data-ttu-id="f0fd1-106">Gli eseguibili guest vengono considerati da Service Fabric come servizi senza stato.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="f0fd1-107">Di conseguenza, vengono inseriti nei nodi di un cluster in base alla disponibilità e ad altre metriche.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="f0fd1-108">Questo articolo descrive come creare un pacchetto e distribuire un eseguibile guest in un cluster di Service Fabric, usando Visual Studio o un'utilità della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-108">This article describes how to package and deploy a guest executable to a Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="f0fd1-109">Questo articolo illustra i passaggi per creare il pacchetto di un eseguibile guest e distribuirlo in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-109">In this article, we cover the steps to package a guest executable and deploy it to Service Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="f0fd1-110">Vantaggi dell'esecuzione di un'eseguibile guest in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f0fd1-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="f0fd1-111">L'esecuzione di un eseguibile guest in un cluster di Service Fabric presenta numerosi vantaggi:</span><span class="sxs-lookup"><span data-stu-id="f0fd1-111">There are several advantages to running a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="f0fd1-112">Disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-112">High availability.</span></span> <span data-ttu-id="f0fd1-113">Le applicazioni eseguite in Service Fabric sono rese altamente disponibili.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="f0fd1-114">Service Fabric garantisce che siano in esecuzione istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="f0fd1-115">Monitoraggio dell’integrità.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-115">Health monitoring.</span></span> <span data-ttu-id="f0fd1-116">Il monitoraggio dell'integrità di Service Fabric rileva se un'applicazione è in esecuzione e fornisce informazioni di diagnostica in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="f0fd1-117">Gestione del ciclo di vita delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-117">Application lifecycle management.</span></span> <span data-ttu-id="f0fd1-118">Oltre a garantire aggiornamenti senza tempi di inattività, Service Fabric consente il ripristino automatico della versione precedente se durante un aggiornamento viene segnalato un evento di integrità negativo.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback to the previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="f0fd1-119">Densità.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-119">Density.</span></span> <span data-ttu-id="f0fd1-120">È possibile eseguire più applicazioni in un cluster, eliminando la necessità che ogni applicazione venga eseguita nel proprio hardware.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-120">You can run multiple applications in a cluster, which eliminates the need for each application to run on its own hardware.</span></span>
* <span data-ttu-id="f0fd1-121">Individuabilità. Usando REST è possibile chiamare il servizio Service Fabric Naming per trovare altri servizi nel cluster.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-121">Discoverability: Using REST you can call the Service Fabric Naming service to find other services in the cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="f0fd1-122">Esempi</span><span class="sxs-lookup"><span data-stu-id="f0fd1-122">Samples</span></span>
* [<span data-ttu-id="f0fd1-123">Esempio per la creazione di un pacchetto e distribuzione di un file guest eseguibile</span><span class="sxs-lookup"><span data-stu-id="f0fd1-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="f0fd1-124">Esempio di due eseguibili guest (C# e nodejs) che comunicano tramite il servizio Naming usando REST</span><span class="sxs-lookup"><span data-stu-id="f0fd1-124">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="f0fd1-125">Panoramica dei file manifesto dell'applicazione e del servizio</span><span class="sxs-lookup"><span data-stu-id="f0fd1-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="f0fd1-126">Nell'ambito della distribuzione di un eseguibile guest è utile comprendere il modello di creazione di pacchetti e di distribuzione di Service Fabric, descritto nel [modello applicativo](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="f0fd1-126">As part of deploying a guest executable, it is useful to understand the Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="f0fd1-127">Il modello di creazione di pacchetti di Service Fabric si basa su due file XML: il manifesto dell'applicazione e il manifesto del servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-127">The Service Fabric packaging model relies on two XML files: the application and service manifests.</span></span> <span data-ttu-id="f0fd1-128">La definizione dello schema per i file ApplicationManifest.xml e ServiceManifest.xml viene installata con Service Fabric SDK in *C:\Programmi\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-128">The schema definition for the ApplicationManifest.xml and ServiceManifest.xml files is installed with the Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="f0fd1-129">**Manifesto dell'applicazione**. Il manifesto dell'applicazione viene usato per descrivere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-129">**Application manifest** The application manifest is used to describe the application.</span></span> <span data-ttu-id="f0fd1-130">Elenca i servizi da cui è costituita e altri parametri usati per definire come dovranno essere distribuiti tali servizi, ad esempio il numero di istanze.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-130">It lists the services that compose it, and other parameters that are used to define how one or more services should be deployed, such as the number of instances.</span></span>

  <span data-ttu-id="f0fd1-131">In Service Fabric un'applicazione è un'unità di distribuzione e aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="f0fd1-132">Un'applicazione può essere aggiornata come una singola unità in cui vengono gestiti i potenziali errori e i potenziali ripristini dello stato precedente.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="f0fd1-133">Service Fabric garantisce che il processo di aggiornamento venga completato o, in caso di errore, che non lasci l'applicazione in uno stato sconosciuto o instabile.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-133">Service Fabric guarantees that the upgrade process is either successful, or, if the upgrade fails, does not leave the application in an unknown or unstable state.</span></span>
* <span data-ttu-id="f0fd1-134">**Manifesto del servizio** .</span><span class="sxs-lookup"><span data-stu-id="f0fd1-134">**Service manifest** The service manifest describes the components of a service.</span></span> <span data-ttu-id="f0fd1-135">Include dati come il nome e il tipo di servizio, nonché il codice e la configurazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-135">It includes data, such as the name and type of service, and its code and configuration.</span></span> <span data-ttu-id="f0fd1-136">Include dati come il nome e il tipo di servizio nonché il codice, la configurazione e i dati del servizio, più alcuni parametri aggiuntivi usati per configurare il servizio una volta distribuito.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-136">The service manifest also includes some additional parameters that can be used to configure the service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="f0fd1-137">Struttura del file del pacchetto dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f0fd1-137">Application package file structure</span></span>
<span data-ttu-id="f0fd1-138">Per distribuire un'applicazione in Service Fabric, l'applicazione deve seguire una struttura di directory predefinita.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-138">To deploy an application to Service Fabric, the application should follow a predefined directory structure.</span></span> <span data-ttu-id="f0fd1-139">Di seguito è riportato un esempio di tale struttura.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-139">The following is an example of that structure.</span></span>

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

<span data-ttu-id="f0fd1-140">ApplicationPackageRoot contiene il file ApplicationManifest.xml che definisce l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-140">The ApplicationPackageRoot contains the ApplicationManifest.xml file that defines the application.</span></span> <span data-ttu-id="f0fd1-141">Per contenere tutti gli elementi necessari per il servizio viene usata una sottodirectory per ogni servizio incluso nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-141">A subdirectory for each service included in the application is used to contain all the artifacts that the service requires.</span></span> <span data-ttu-id="f0fd1-142">Tali sottodirectory sono ServiceManifest.xml e, in genere, la seguente:</span><span class="sxs-lookup"><span data-stu-id="f0fd1-142">These subdirectories are the ServiceManifest.xml and, typically, the following:</span></span>

* <span data-ttu-id="f0fd1-143">*Code*.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-143">*Code*.</span></span> <span data-ttu-id="f0fd1-144">Contiene il codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-144">This directory contains the service code.</span></span>
* <span data-ttu-id="f0fd1-145">*Config*.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-145">*Config*.</span></span> <span data-ttu-id="f0fd1-146">Questa directory contiene un file Settings.xml (e altri file, se necessario) a cui il servizio può accedere in fase di esecuzione per recuperare specifiche impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-146">This directory contains a Settings.xml file (and other files if necessary) that the service can access at runtime to retrieve specific configuration settings.</span></span>
* <span data-ttu-id="f0fd1-147">*Dati*.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-147">*Data*.</span></span> <span data-ttu-id="f0fd1-148">Un'altra directory in cui archiviare dati locali aggiuntivi che potrebbero essere necessari al servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-148">This is an additional directory to store additional local data that the service may need.</span></span> <span data-ttu-id="f0fd1-149">I dati devono essere usati per archiviare solo dati temporanei.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-149">Data should be used to store only ephemeral data.</span></span> <span data-ttu-id="f0fd1-150">Service Fabric non copia o replica le modifiche alla directory dei dati se il servizio deve essere trasferito, ad esempio durante il failover.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-150">Service Fabric does not copy or replicate changes to the data directory if the service needs to be relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="f0fd1-151">Non è necessario creare le directory `config` e `data` se non sono necessarie.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-151">You don't have to create the `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="f0fd1-152">Creare il pacchetto di un eseguibile esistente</span><span class="sxs-lookup"><span data-stu-id="f0fd1-152">Package an existing executable</span></span>
<span data-ttu-id="f0fd1-153">Quando si crea il pacchetto di un eseguibile guest, è possibile scegliere di usare un modello di progetto di Visual Studio oppure di [creare manualmente il pacchetto dell'applicazione](#manually).</span><span class="sxs-lookup"><span data-stu-id="f0fd1-153">When packaging a guest executable, you can choose either to use a Visual Studio project template or to [create the application package manually](#manually).</span></span> <span data-ttu-id="f0fd1-154">Se si usa Visual Studio, la struttura del pacchetto dell'applicazione e i file manifesto vengono creati automaticamente dal nuovo modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-154">Using Visual Studio, the application package structure and manifest files are created by the new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="f0fd1-155">Il modo più semplice per creare il pacchetto di un eseguibile Windows esistente in un servizio consiste nell'usare Visual Studio (oppure Yeoman in Linux)</span><span class="sxs-lookup"><span data-stu-id="f0fd1-155">The easiest way to package an existing Windows executable into a service is to use Visual Studio and on Linux to use Yeoman</span></span>
>

## <a name="use-visual-studio-to-package-and-deploy-an-existing-executable"></a><span data-ttu-id="f0fd1-156">Usare Visual Studio per creare il pacchetto e distribuire un eseguibile esistente</span><span class="sxs-lookup"><span data-stu-id="f0fd1-156">Use Visual Studio to package and deploy an existing executable</span></span>
<span data-ttu-id="f0fd1-157">Visual Studio include un modello di servizio di Service Fabric che consente di distribuire un eseguibile guest in un cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-157">Visual Studio provides a Service Fabric service template to help you deploy a guest executable to a Service Fabric cluster.</span></span>

1. <span data-ttu-id="f0fd1-158">Scegliere **File** > **Nuovo progetto** e creare un'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-158">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="f0fd1-159">Scegliere **Eseguibile guest** come modello di servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-159">Choose **Guest Executable** as the service template.</span></span>
3. <span data-ttu-id="f0fd1-160">Fare clic su **Sfoglia** per selezionare la cartella contenente l'eseguibile e immettere i restanti parametri per creare il servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-160">Click **Browse** to select the folder with your executable and fill in the rest of the parameters to create the service.</span></span>
   * <span data-ttu-id="f0fd1-161">*Comportamento del pacchetto di codice*.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-161">*Code Package Behavior*.</span></span> <span data-ttu-id="f0fd1-162">È possibile impostare questa opzione per copiare tutto il contenuto della cartella nel progetto di Visual Studio. Questa scelta si rivela utile se il file eseguibile non viene modificato.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-162">Can be set to copy all the content of your folder to the Visual Studio Project, which is useful if the executable does not change.</span></span> <span data-ttu-id="f0fd1-163">Se si prevede che il file eseguibile venga modificato e si vuole avere la possibilità di selezionare nuove build in modo dinamico, si può scegliere invece di collegarsi alla cartella.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-163">If you expect the executable to change and want the ability to pick up new builds dynamically, you can choose to link to the folder instead.</span></span> <span data-ttu-id="f0fd1-164">Se si crea il progetto di applicazione in Visual Studio è possibile usare cartelle collegate.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-164">You can use linked folders when creating the application project in Visual Studio.</span></span> <span data-ttu-id="f0fd1-165">In questo modo si stabilisce il collegamento al percorso di origine dall'interno del progetto, rendendo possibile l'aggiornamento dell'eseguibile guest nella destinazione di origine.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-165">This links to the source location from within the project, making it possible for you to update the guest executable in its source destination.</span></span> <span data-ttu-id="f0fd1-166">Gli aggiornamenti diventano parte del pacchetto dell'applicazione in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-166">Those updates become part of the application package on build.</span></span>
   * <span data-ttu-id="f0fd1-167">*Programma*: specifica l'eseguibile da eseguire per avviare il servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-167">*Program* specifies the executable that should be run to start the service.</span></span>
   * <span data-ttu-id="f0fd1-168">*Argomenti*: specifica gli argomenti da passare all'eseguibile.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-168">*Arguments* specifies the arguments that should be passed to the executable.</span></span> <span data-ttu-id="f0fd1-169">Può essere un elenco di parametri con argomenti.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-169">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="f0fd1-170">*WorkingFolder*: specifica la directory di lavoro per il processo che verrà avviato.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-170">*WorkingFolder* specifies the working directory for the process that is going to be started.</span></span> <span data-ttu-id="f0fd1-171">È possibile specificare tre valori:</span><span class="sxs-lookup"><span data-stu-id="f0fd1-171">You can specify three values:</span></span>
     * <span data-ttu-id="f0fd1-172">`CodeBase` specifica che la directory di lavoro verrà impostata sulla directory del codice nel pacchetto dell'applicazione (directory `Code` nella struttura di file precedente).</span><span class="sxs-lookup"><span data-stu-id="f0fd1-172">`CodeBase` specifies that the working directory is going to be set to the code directory in the application package (`Code` directory shown in the preceding file structure).</span></span>
     * <span data-ttu-id="f0fd1-173">`CodePackage` specifica che la directory di lavoro verrà impostata sulla radice del pacchetto dell'applicazione (`GuestService1Pkg` nella struttura di file precedente).</span><span class="sxs-lookup"><span data-stu-id="f0fd1-173">`CodePackage` specifies that the working directory is going to be set to the root of the application package    (`GuestService1Pkg` shown in the preceding file structure).</span></span>
     * <span data-ttu-id="f0fd1-174">`Work` specifica che i file vengono inseriti in una sottodirectory denominata work.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-174">`Work` specifies that the files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="f0fd1-175">Assegnare un nome al servizio e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-175">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="f0fd1-176">Se il servizio richiede un endpoint per la comunicazione, è ora possibile aggiungere il protocollo, la porta e il tipo al file ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-176">If your service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="f0fd1-177">Ad esempio: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-177">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="f0fd1-178">È ora possibile usare l'azione di creazione del pacchetto e di pubblicazione sul cluster locale eseguendo il debug della soluzione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-178">You can now use the package and publish action against your local cluster by debugging the solution in Visual Studio.</span></span> <span data-ttu-id="f0fd1-179">Quando si è pronti, pubblicare l'applicazione in un cluster remoto o archiviare la soluzione nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-179">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span></span>
7. <span data-ttu-id="f0fd1-180">Per informazioni su come visualizzare il servizio dell'eseguibile guest in esecuzione in Service Fabric Explorer, andare alla fine di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-180">Go to the end of this article to see how to view your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-to-package-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="f0fd1-181">Usare Yoeman per creare il pacchetto e distribuire un eseguibile esistente in Linux</span><span class="sxs-lookup"><span data-stu-id="f0fd1-181">Use Yoeman to package and deploy an existing executable on Linux</span></span>

<span data-ttu-id="f0fd1-182">La procedura per la creazione e distribuzione di un eseguibile guest in Linux è analoga alla distribuzione di un'applicazione java o csharp.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-182">The procedure for creating and deploying a guest executable on Linux is the same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="f0fd1-183">In un terminale digitare `yo azuresfguest`.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-183">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="f0fd1-184">Assegnare un nome all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-184">Name your application.</span></span>
3. <span data-ttu-id="f0fd1-185">Assegnare un nome al servizio e specificarne i dettagli, ad esempio il percorso del file eseguibile e i parametri con cui deve essere richiamato.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-185">Name your service, and provide the details including path of the executable and the parameters it must be invoked with.</span></span>

<span data-ttu-id="f0fd1-186">Yeoman crea un pacchetto dell'applicazione con i file manifesto e dell'applicazione appropriati e con gli script di installazione e di disinstallazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-186">Yeoman creates an application package with the appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="f0fd1-187">Creare manualmente il pacchetto e distribuire un eseguibile esistente</span><span class="sxs-lookup"><span data-stu-id="f0fd1-187">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="f0fd1-188">Il processo per la creazione manuale del pacchetto di un eseguibile guest si basa sulla procedura generale seguente:</span><span class="sxs-lookup"><span data-stu-id="f0fd1-188">The process of manually packaging a guest executable is based on the following general steps:</span></span>

1. <span data-ttu-id="f0fd1-189">Creare la struttura di directory del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-189">Create the package directory structure.</span></span>
2. <span data-ttu-id="f0fd1-190">Aggiungere i file di codice e di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-190">Add the application's code and configuration files.</span></span>
3. <span data-ttu-id="f0fd1-191">Modificare il file manifesto del servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-191">Edit the service manifest file.</span></span>
4. <span data-ttu-id="f0fd1-192">Modificare il file manifesto dell’applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-192">Edit the application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you to create the ApplicationPackage automatically. The tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-the-package-directory-structure"></a><span data-ttu-id="f0fd1-193">Creare la struttura di directory del pacchetto</span><span class="sxs-lookup"><span data-stu-id="f0fd1-193">Create the package directory structure</span></span>
<span data-ttu-id="f0fd1-194">È possibile iniziare creando la struttura di directory come descritto nella sezione precedente "Struttura del file del pacchetto dell'applicazione".</span><span class="sxs-lookup"><span data-stu-id="f0fd1-194">You can start by creating the directory structure, as described in the preceding section, "Application package file structure."</span></span>

### <a name="add-the-applications-code-and-configuration-files"></a><span data-ttu-id="f0fd1-195">Aggiungere i file di codice e di configurazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f0fd1-195">Add the application's code and configuration files</span></span>
<span data-ttu-id="f0fd1-196">Dopo aver creato la struttura di directory, è possibile aggiungere i file di configurazione e di codice dell'applicazione nelle directory del codice e di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-196">After you have created the directory structure, you can add the application's code and configuration files under the code and config directories.</span></span> <span data-ttu-id="f0fd1-197">È inoltre possibile creare directory aggiuntive o sottodirectory nelle directory del codice e di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-197">You can also create additional directories or subdirectories under the code or config directories.</span></span>

<span data-ttu-id="f0fd1-198">Service Fabric esegue un'operazione `xcopy` del contenuto della radice della directory dell'applicazione in modo che non esista alcuna struttura predefinita da usare oltre alla creazione delle due directory principali relative a codice e impostazioni.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-198">Service Fabric does an `xcopy` of the content of the application root directory, so there is no predefined structure to use other than creating two top directories, code and settings.</span></span> <span data-ttu-id="f0fd1-199">(ma se si desidera, è possibile scegliere nomi diversi,</span><span class="sxs-lookup"><span data-stu-id="f0fd1-199">(You can pick different names if you want.</span></span> <span data-ttu-id="f0fd1-200">come illustrato in dettaglio nella sezione successiva).</span><span class="sxs-lookup"><span data-stu-id="f0fd1-200">More details are in the next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="f0fd1-201">Assicurarsi di includere tutti i file e le dipendenze necessari all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-201">Make sure that you include all the files and dependencies that the application needs.</span></span> <span data-ttu-id="f0fd1-202">Service Fabric copia il contenuto del pacchetto dell'applicazione in tutti i nodi del cluster in cui vengono distribuiti i servizi dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-202">Service Fabric copies the content of the application package on all nodes in the cluster where the application's services are going to be deployed.</span></span> <span data-ttu-id="f0fd1-203">Il pacchetto deve contenere tutto il codice necessario per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-203">The package should contain all the code that the application needs to run.</span></span> <span data-ttu-id="f0fd1-204">Non presupporre che le dipendenze siano già installate.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-204">Do not assume that the dependencies are already installed.</span></span>
>
>

### <a name="edit-the-service-manifest-file"></a><span data-ttu-id="f0fd1-205">Modificare il file manifesto del servizio</span><span class="sxs-lookup"><span data-stu-id="f0fd1-205">Edit the service manifest file</span></span>
<span data-ttu-id="f0fd1-206">Il passaggio successivo consiste nel modificare il file manifesto del servizio per includere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f0fd1-206">The next step is to edit the service manifest file to include the following information:</span></span>

* <span data-ttu-id="f0fd1-207">Il nome del tipo di servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-207">The name of the service type.</span></span> <span data-ttu-id="f0fd1-208">Si tratta di un ID usato da Service Fabric per identificare un servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-208">This is an ID that Service Fabric uses to identify a service.</span></span>
* <span data-ttu-id="f0fd1-209">Il comando da usare per avviare l'applicazione (ExeHost).</span><span class="sxs-lookup"><span data-stu-id="f0fd1-209">The command to use to launch the application (ExeHost).</span></span>
* <span data-ttu-id="f0fd1-210">Qualsiasi script da eseguire per installare l'applicazione (SetupEntrypoint).</span><span class="sxs-lookup"><span data-stu-id="f0fd1-210">Any script that needs to be run to set up the application (SetupEntrypoint).</span></span>

<span data-ttu-id="f0fd1-211">Di seguito è riportato un esempio di file `ServiceManifest.xml` :</span><span class="sxs-lookup"><span data-stu-id="f0fd1-211">The following is an example of a `ServiceManifest.xml` file:</span></span>

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

<span data-ttu-id="f0fd1-212">Nelle sezioni seguenti vengono esaminate le diverse parti del file che è necessario aggiornare.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-212">The following sections go over the different parts of the file that you need to update.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="f0fd1-213">Aggiornare ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="f0fd1-213">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="f0fd1-214">È possibile scegliere qualsiasi nome per `ServiceTypeName`.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-214">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="f0fd1-215">Il valore viene usato nel file `ApplicationManifest.xml` per identificare il servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-215">The value is used in the `ApplicationManifest.xml` file to identify the service.</span></span>
* <span data-ttu-id="f0fd1-216">Specificare `UseImplicitHost="true"`.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-216">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="f0fd1-217">Questo attributo indica a Service Fabric che il servizio si basa su un'applicazione autonoma, in modo che debba soltanto avviarla come processo e monitorarne l'integrità.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-217">This attribute tells Service Fabric that the service is based on a self-contained app, so all Service Fabric needs to do is to launch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="f0fd1-218">Aggiornare CodePackage</span><span class="sxs-lookup"><span data-stu-id="f0fd1-218">Update CodePackage</span></span>
<span data-ttu-id="f0fd1-219">L’elemento CodePackage specifica il percorso (e la versione) del codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-219">The CodePackage element specifies the location (and version) of the service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="f0fd1-220">L'elemento `Name` consente di specificare il nome della directory nel pacchetto dell'applicazione che contiene il codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-220">The `Name` element is used to specify the name of the directory in the application package that contains the service's code.</span></span> <span data-ttu-id="f0fd1-221">`CodePackage` include anche l'attributo `version`,</span><span class="sxs-lookup"><span data-stu-id="f0fd1-221">`CodePackage` also has the `version` attribute.</span></span> <span data-ttu-id="f0fd1-222">Questo consente di specificare la versione del codice e potenzialmente di aggiornare il codice del servizio mediante l'infrastruttura Application Lifecycle Management di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-222">This can be used to specify the version of the code, and can also potentially be used to upgrade the service's code by using the application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="f0fd1-223">Facoltativo: aggiornare SetupEntrypoint</span><span class="sxs-lookup"><span data-stu-id="f0fd1-223">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="f0fd1-224">L'elemento SetupEntryPoint consente di specificare un file eseguibile o un file batch da eseguire prima dell'avvio del codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-224">The SetupEntryPoint element is used to specify any executable or batch file that should be executed before the service's code is launched.</span></span> <span data-ttu-id="f0fd1-225">È un passaggio facoltativo e non deve pertanto essere necessariamente incluso se non è richiesta alcuna inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-225">It is an optional step, so it does not need to be included if there is no initialization required.</span></span> <span data-ttu-id="f0fd1-226">L'elemento SetupEntryPoint viene eseguito ogni volta che il servizio viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-226">The SetupEntryPoint is executed every time the service is restarted.</span></span>

<span data-ttu-id="f0fd1-227">Esiste un solo SetupEntryPoint, di conseguenza gli script di installazione devono essere raggruppati in un singolo file batch se l'installazione dell'applicazione richiede più script.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-227">There is only one SetupEntryPoint, so setup scripts need to be grouped in a single batch file if the application's setup requires multiple scripts.</span></span> <span data-ttu-id="f0fd1-228">SetupEntryPoint può eseguire qualsiasi tipo di file: file eseguibili, file batch e cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-228">The SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="f0fd1-229">Per altri dettagli, vedere l'articolo su come [configurare SetupEntryPoint](service-fabric-application-runas-security.md).</span><span class="sxs-lookup"><span data-stu-id="f0fd1-229">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="f0fd1-230">Nell'esempio precedente SetupEntryPoint esegue un file batch denominato `LaunchConfig.cmd` che si trova nella sottodirectory `scripts` della directory del codice, presupponendo che l'elemento WorkingFolder sia impostato su CodeBase.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-230">In the preceding example, the SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in the `scripts` subdirectory of the code directory (assuming the WorkingFolder element is set to CodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="f0fd1-231">Aggiornare EntryPoint</span><span class="sxs-lookup"><span data-stu-id="f0fd1-231">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="f0fd1-232">L'elemento `EntryPoint` nel manifesto del servizio consente di specificare la modalità di avvio del servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-232">The `EntryPoint` element in the service manifest file is used to specify how to launch the service.</span></span> <span data-ttu-id="f0fd1-233">L'elemento `ExeHost` specifica il file eseguibile e i relativi argomenti da usare per avviare il servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-233">The `ExeHost` element specifies the executable (and arguments) that should be used to launch the service.</span></span>

* <span data-ttu-id="f0fd1-234">`Program` specifica il nome dell'eseguibile che deve avviare il servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-234">`Program` specifies the name of the executable that should start the service.</span></span>
* <span data-ttu-id="f0fd1-235">`Arguments` specifica gli argomenti da passare al file eseguibile.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-235">`Arguments` specifies the arguments that should be passed to the executable.</span></span> <span data-ttu-id="f0fd1-236">Può essere un elenco di parametri con argomenti.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-236">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="f0fd1-237">`WorkingFolder` specifica la directory di lavoro per il processo che sta per essere avviato.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-237">`WorkingFolder` specifies the working directory for the process that is going to be started.</span></span> <span data-ttu-id="f0fd1-238">È possibile specificare tre valori:</span><span class="sxs-lookup"><span data-stu-id="f0fd1-238">You can specify three values:</span></span>
  * <span data-ttu-id="f0fd1-239">`CodeBase` specifica che la directory di lavoro verrà impostata sulla directory code nel pacchetto dell'applicazione (directory `Code` nella struttura di file precedente).</span><span class="sxs-lookup"><span data-stu-id="f0fd1-239">`CodeBase` specifies that the working directory is going to be set to the code directory in the application package (`Code` directory in the preceding file structure).</span></span>
  * <span data-ttu-id="f0fd1-240">`CodePackage` specifica che la directory di lavoro verrà impostata sulla radice del pacchetto dell'applicazione (`GuestService1Pkg` nella struttura di file precedente).</span><span class="sxs-lookup"><span data-stu-id="f0fd1-240">`CodePackage` specifies that the working directory is going to be set to the root of the application package    (`GuestService1Pkg` in the preceding file structure).</span></span>
    * <span data-ttu-id="f0fd1-241">`Work` specifica che i file vengono inseriti in una sottodirectory denominata work.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-241">`Work` specifies that the files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="f0fd1-242">WorkingFolder è utile per impostare la directory di lavoro corretta, in modo che i percorsi relativi possano essere usati dagli script di applicazione o da quelli di inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-242">The WorkingFolder is useful to set the correct working directory so that relative paths can be used by either the application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="f0fd1-243">Aggiornare gli endpoint e registrarli nel servizio di denominazione per la comunicazione</span><span class="sxs-lookup"><span data-stu-id="f0fd1-243">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="f0fd1-244">Nell'esempio precedente l'elemento `Endpoint` specifica gli endpoint sui quali l'applicazione può restare in ascolto.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-244">In the preceding example, the `Endpoint` element specifies the endpoints that the application can listen on.</span></span> <span data-ttu-id="f0fd1-245">In questo esempio, l'applicazione Node.js è in ascolto di HTTP sulla porta 3000.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-245">In this example, the Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="f0fd1-246">È anche possibile richiedere a Service Fabric di pubblicare l'endpoint nel servizio Naming in modo che altri servizi possano individuare l'indirizzo dell'endpoint per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-246">Furthermore you can ask Service Fabric to publish this endpoint to the Naming Service so other services can discover the endpoint address to this service.</span></span> <span data-ttu-id="f0fd1-247">Ciò consente la comunicazione tra servizi costituiti da eseguibili guest.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-247">This enables you to be able to communicate between services that are guest executables.</span></span>
<span data-ttu-id="f0fd1-248">L'indirizzo dell'endpoint pubblicato presenta il formato `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-248">The published endpoint address is of the form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="f0fd1-249">`UriScheme` e `PathSuffix` sono attributi facoltativi.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-249">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="f0fd1-250">`IPAddressOrFQDN` è l'indirizzo IP o il nome di dominio completo del nodo in cui viene inserito l'eseguibile e viene calcolato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-250">`IPAddressOrFQDN` is the IP address or fully qualified domain name of the node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="f0fd1-251">Nell'esempio seguente, dopo la distribuzione del servizio, in Service Fabric Explorer viene visualizzato un endpoint simile a `http://10.1.4.92:3000/myapp/` pubblicato per l'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-251">In the following example, once the service is deployed, in Service Fabric Explorer you see an endpoint similar to `http://10.1.4.92:3000/myapp/` published for the service instance.</span></span> <span data-ttu-id="f0fd1-252">Oppure, se si tratta di un computer locale, viene visualizzato `http://localhost:3000/myapp/`.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-252">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="f0fd1-253">È possibile usare questi indirizzi con il [proxy inverso](service-fabric-reverseproxy.md) per la comunicazione tra servizi.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-253">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) to communicate between services.</span></span>

### <a name="edit-the-application-manifest-file"></a><span data-ttu-id="f0fd1-254">Modificare il file manifesto dell’applicazione</span><span class="sxs-lookup"><span data-stu-id="f0fd1-254">Edit the application manifest file</span></span>
<span data-ttu-id="f0fd1-255">Dopo aver configurato il file `Servicemanifest.xml`, sarà necessario apportare alcune modifiche al file `ApplicationManifest.xml` per assicurarsi che vengano usati il tipo e il nome corretti per il servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-255">Once you have configured the `Servicemanifest.xml` file, you need to make some changes to the `ApplicationManifest.xml` file to ensure that the correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="f0fd1-256">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="f0fd1-256">ServiceManifestImport</span></span>
<span data-ttu-id="f0fd1-257">Nell'elemento `ServiceManifestImport` è possibile specificare uno o più servizi da includere nell'app.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-257">In the `ServiceManifestImport` element, you can specify one or more services that you want to include in the app.</span></span> <span data-ttu-id="f0fd1-258">Per fare riferimento ai servizi viene usato l'elemento `ServiceManifestName`, che specifica il nome della directory in cui è presente il file `ServiceManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-258">Services are referenced with `ServiceManifestName`, which specifies the name of the directory where the `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="f0fd1-259">Configurare la registrazione</span><span class="sxs-lookup"><span data-stu-id="f0fd1-259">Set up logging</span></span>
<span data-ttu-id="f0fd1-260">Per gli eseguibili guest è utile poter visualizzare i log di console per determinare la presenza di eventuali errori negli script di configurazione e di applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-260">For guest executables, it is useful to be able to see console logs to find out if the application and configuration scripts show any errors.</span></span>
<span data-ttu-id="f0fd1-261">Il reindirizzamento della console può essere configurato nel file `ServiceManifest.xml` tramite l'elemento `ConsoleRedirection`.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-261">Console redirection can be configured in the `ServiceManifest.xml` file using the `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="f0fd1-262">Non usare mai i criteri di reindirizzamento della console in un'applicazione distribuita nell'ambiente di produzione, perché ciò può incidere sul failover dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-262">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span></span> <span data-ttu-id="f0fd1-263">Usare questa opzione *solo* a scopo di sviluppo e debug locale.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-263">*Only* use this for local development and debugging purposes.</span></span>  
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

<span data-ttu-id="f0fd1-264">L'elemento `ConsoleRedirection` consente di reindirizzare l'output della console, di tipo stdout o stderr, a una directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-264">`ConsoleRedirection` can be used to redirect console output (both stdout and stderr) to a working directory.</span></span> <span data-ttu-id="f0fd1-265">In questo modo è possibile verificare che non siano presenti errori durante l'installazione o l'esecuzione dell'applicazione nel cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-265">This provides the ability to verify that there are no errors during the setup or execution of the application in the Service Fabric cluster.</span></span>

<span data-ttu-id="f0fd1-266">`FileRetentionCount` determina il numero di file salvati nella directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-266">`FileRetentionCount` determines how many files are saved in the working directory.</span></span> <span data-ttu-id="f0fd1-267">Un valore pari a 5, ad esempio, indica che i file di log per le cinque esecuzioni precedenti vengono archiviati nella directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-267">A value of 5, for example, means that the log files for the previous five executions are stored in the working directory.</span></span>

<span data-ttu-id="f0fd1-268">`FileMaxSizeInKb` specifica le dimensioni massime dei file di log.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-268">`FileMaxSizeInKb` specifies the maximum size of the log files.</span></span>

<span data-ttu-id="f0fd1-269">I file di log vengono salvati in una directory di lavoro del servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-269">Log files are saved in one of the service's working directories.</span></span> <span data-ttu-id="f0fd1-270">Per determinare dove si trovano i file, è necessario usare Service Fabric Explorer per stabilire il nodo in cui è in esecuzione il servizio e la directory di lavoro in uso.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-270">To determine where the files are located, use Service Fabric Explorer to determine which node the service is running on, and which working directory is being used.</span></span> <span data-ttu-id="f0fd1-271">Più avanti in questo articolo verrà illustrato questo processo.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-271">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="f0fd1-272">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="f0fd1-272">Deployment</span></span>
<span data-ttu-id="f0fd1-273">L'ultimo passaggio consiste nel [distribuire l'applicazione](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="f0fd1-273">The last step is to [deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="f0fd1-274">Lo script di PowerShell seguente illustra come distribuire l'applicazione nel cluster di sviluppo locale e avviare un nuovo servizio di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-274">The following PowerShell script shows how to deploy your application to the local development cluster, and start a new Service Fabric service.</span></span>

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
> <span data-ttu-id="f0fd1-275">[Comprimere il pacchetto](service-fabric-package-apps.md#compress-a-package) prima di copiarlo nell'archivio immagini se il pacchetto è grande o contiene molti file.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-275">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store if the package is large or has many files.</span></span> <span data-ttu-id="f0fd1-276">Per altre informazioni, leggere [qui](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span><span class="sxs-lookup"><span data-stu-id="f0fd1-276">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="f0fd1-277">Un servizio Service Fabric può essere distribuito in varie "configurazioni",</span><span class="sxs-lookup"><span data-stu-id="f0fd1-277">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="f0fd1-278">ad esempio può essere distribuito come istanza singola o come istanze multiple o può essere distribuito in modo tale che sia presente un'istanza del servizio in ogni nodo del cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-278">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of the service on each node of the Service Fabric cluster.</span></span>

<span data-ttu-id="f0fd1-279">Il parametro `InstanceCount` del cmdlet `New-ServiceFabricService` consente di specificare il numero di istanze del servizio da avviare nel cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-279">The `InstanceCount` parameter of the `New-ServiceFabricService` cmdlet is used to specify how many instances of the service should be launched in the Service Fabric cluster.</span></span> <span data-ttu-id="f0fd1-280">È possibile impostare il valore `InstanceCount` in base al tipo di applicazione da distribuire.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-280">You can set the `InstanceCount` value, depending on the type of application that you are deploying.</span></span> <span data-ttu-id="f0fd1-281">I due scenari più comuni sono:</span><span class="sxs-lookup"><span data-stu-id="f0fd1-281">The two most common scenarios are:</span></span>

* <span data-ttu-id="f0fd1-282">`InstanceCount = "1"`.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-282">`InstanceCount = "1"`.</span></span> <span data-ttu-id="f0fd1-283">In questo caso viene distribuita nel cluster una sola istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-283">In this case, only one instance of the service is deployed in the cluster.</span></span> <span data-ttu-id="f0fd1-284">L'utilità di pianificazione di Service Fabric determina il nodo in cui il servizio dovrà essere distribuito.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-284">Service Fabric's scheduler determines which node the service is going to be deployed on.</span></span>
* <span data-ttu-id="f0fd1-285">`InstanceCount ="-1"`.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-285">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="f0fd1-286">In questo caso viene distribuita un'istanza del servizio in ogni nodo del cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-286">In this case, one instance of the service is deployed on every node in the Service Fabric cluster.</span></span> <span data-ttu-id="f0fd1-287">Di conseguenza sarà presente un'unica istanza del servizio per ogni nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-287">The result is having one (and only one) instance of the service for each node in the cluster.</span></span>

<span data-ttu-id="f0fd1-288">Questa configurazione è utile per applicazioni front-end (ad esempio, un endpoint REST) perché le applicazioni client devono "connettersi" a qualsiasi nodo del cluster per usare l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-288">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need to "connect" to any of the nodes in the cluster to use the endpoint.</span></span> <span data-ttu-id="f0fd1-289">Questa configurazione può essere inoltre usata quando, ad esempio, tutti i nodi del cluster di Service Fabric sono connessi a un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-289">This configuration can also be used when, for example, all nodes of the Service Fabric cluster are connected to a load balancer.</span></span> <span data-ttu-id="f0fd1-290">Il traffico del client può quindi essere distribuito nel servizio in esecuzione su tutti i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-290">Client traffic can then be distributed across the service that is running on all nodes in the cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="f0fd1-291">Verificare l'applicazione in esecuzione</span><span class="sxs-lookup"><span data-stu-id="f0fd1-291">Check your running application</span></span>
<span data-ttu-id="f0fd1-292">In Esplora infrastruttura di servizi identificare il nodo in cui è in esecuzione il servizio.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-292">In Service Fabric Explorer, identify the node where the service is running.</span></span> <span data-ttu-id="f0fd1-293">In questo esempio è in esecuzione in Node1:</span><span class="sxs-lookup"><span data-stu-id="f0fd1-293">In this example, it runs on Node1:</span></span>

![Nodo in cui è in esecuzione il servizio](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="f0fd1-295">Se si passa al nodo e si accede all'applicazione, è possibile visualizzare le informazioni essenziali sul nodo, incluso il percorso sul disco.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-295">If you navigate to the node and browse to the application, you see the essential node information, including its location on disk.</span></span>

![Percorso sul disco](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="f0fd1-297">Se si passa alla directory usando Esplora server è possibile trovare la directory di lavoro e la cartella dei log del servizio, come illustrato nella schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="f0fd1-297">If you browse to the directory by using Server Explorer, you can find the working directory and the service's log folder, as shown in the following screenshot:</span></span> 

![Percorso del log](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="f0fd1-299">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f0fd1-299">Next steps</span></span>
<span data-ttu-id="f0fd1-300">In questo articolo si è appreso come creare il pacchetto di un eseguibile guest e come distribuirlo in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-300">In this article, you have learned how to package a guest executable and deploy it to Service Fabric.</span></span> <span data-ttu-id="f0fd1-301">Per informazioni e attività correlate, vedere gli articoli seguenti.</span><span class="sxs-lookup"><span data-stu-id="f0fd1-301">See the following articles for related information and tasks.</span></span>

* <span data-ttu-id="f0fd1-302">[Esempio per la creazione del pacchetto e la distribuzione di un file guest eseguibile ](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), con un collegamento alla versione preliminare dello strumento per la creazione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="f0fd1-302">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link to the prerelease of the packaging tool</span></span>
* [<span data-ttu-id="f0fd1-303">Esempio di due eseguibili guest (C# e nodejs) che comunicano tramite il servizio Naming usando REST</span><span class="sxs-lookup"><span data-stu-id="f0fd1-303">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="f0fd1-304">Distribuire più eseguibili guest</span><span class="sxs-lookup"><span data-stu-id="f0fd1-304">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="f0fd1-305">Creare la prima applicazione Service Fabric in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f0fd1-305">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
