---
title: Creare la prima app di microservizi di Azure in Linux con C# | Documentazione Microsoft
description: Creare e distribuire un'applicazione di Service Fabric con C#
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: adcafaa5522fcddc0a01eb1dc8deba04ebfc38f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="8438f-103">Creare la prima applicazione di Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8438f-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8438f-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="8438f-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="8438f-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="8438f-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="8438f-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="8438f-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="8438f-107">Service Fabric mette a disposizione SDK per la compilazione di servizi su Linux in .NET Core e Java.</span><span class="sxs-lookup"><span data-stu-id="8438f-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="8438f-108">In questa esercitazione verrà esaminata la creazione di un'applicazione per Linux e la compilazione di un servizio con C# (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="8438f-108">In this tutorial, we look at how to create an application for Linux and build a service using C# (.NET Core).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8438f-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8438f-109">Prerequisites</span></span>
<span data-ttu-id="8438f-110">Prima di iniziare, assicurarsi di avere [configurato l'ambiente di sviluppo di Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8438f-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="8438f-111">Se si usa Mac OS X è possibile [configurare un ambiente con un solo computer Linux in una macchina virtuale usando Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="8438f-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="8438f-112">È consigliabile installare anche l'[interfaccia della riga di comando di Service Fabric](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8438f-112">You will also want to install the [Service Fabric CLI](service-fabric-cli.md)</span></span>

### <a name="install-and-set-up-the-generators-for-csharp"></a><span data-ttu-id="8438f-113">Installare e configurare i generatori per CSharp</span><span class="sxs-lookup"><span data-stu-id="8438f-113">Install and set up the generators for CSharp</span></span>
<span data-ttu-id="8438f-114">Service Fabric offre gli strumenti di scaffolding che consentono di creare un'applicazione CSharp per Service Fabric dal terminale tramite il generatore di modelli Yeoman.</span><span class="sxs-lookup"><span data-stu-id="8438f-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric CSharp application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="8438f-115">Seguire questa procedura per assicurarsi che nella macchina virtuale sia disponibile il generatore di modelli Yeoman di Service Fabric per CSharp.</span><span class="sxs-lookup"><span data-stu-id="8438f-115">Please follow the steps below to ensure you have the Service Fabric yeoman template generator for CSharp working on your machine.</span></span>
1. <span data-ttu-id="8438f-116">Installare nodejs e NPM nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="8438f-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="8438f-117">Installare il generatore di modelli [Yeoman](http://yeoman.io/) nella macchina virtuale da NPM</span><span class="sxs-lookup"><span data-stu-id="8438f-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="8438f-118">Installare il generatore di applicazioni Java Yeo di Service Fabric da NPM</span><span class="sxs-lookup"><span data-stu-id="8438f-118">Install the Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-the-application"></a><span data-ttu-id="8438f-119">Creazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="8438f-119">Create the application</span></span>
<span data-ttu-id="8438f-120">Un'applicazione Infrastruttura di servizi può contenere uno o più servizi, ognuno dei quali contribuisce alle funzionalità dell'applicazione con un ruolo specifico.</span><span class="sxs-lookup"><span data-stu-id="8438f-120">A Service Fabric application can contain one or more services, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="8438f-121">Il generatore [Yeoman](http://yeoman.io/) di Service Fabric per CSharp, installato nell'ultimo passaggio, semplifica la creazione del primo servizio e l'aggiunta di altri servizi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="8438f-121">The Service Fabric [Yeoman](http://yeoman.io/) generator for CSharp, which you installed in last step, makes it easy to create your first service and to add more later.</span></span> <span data-ttu-id="8438f-122">Verrà usato Yeoman per creare un'applicazione con un solo servizio.</span><span class="sxs-lookup"><span data-stu-id="8438f-122">Let's use Yeoman to create an application with a single service.</span></span>

1. <span data-ttu-id="8438f-123">In un terminale, digitare il comando seguente per iniziare a creare lo scaffolding: `yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="8438f-123">In a terminal, type the following command to start building the scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="8438f-124">Assegnare un nome all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8438f-124">Name your application.</span></span>
3. <span data-ttu-id="8438f-125">Scegliere il tipo del primo servizio e assegnargli un nome.</span><span class="sxs-lookup"><span data-stu-id="8438f-125">Choose the type of your first service and name it.</span></span> <span data-ttu-id="8438f-126">Ai fini di questa esercitazione viene scelto un servizio Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="8438f-126">For the purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![Generatore Yeoman di Service Fabric per C#][sf-yeoman]

> [!NOTE]
> <span data-ttu-id="8438f-128">Per altre informazioni sulle opzioni, vedere [Panoramica dei modelli di programmazione di Service Fabric](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="8438f-128">For more information about the options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
>
>

## <a name="build-the-application"></a><span data-ttu-id="8438f-129">Compilare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8438f-129">Build the application</span></span>
<span data-ttu-id="8438f-130">I modelli Yeoman di Service Fabric includono uno script di compilazione che è possibile usare per compilare l'app dal terminale (dopo il passaggio alla cartella dell'applicazione).</span><span class="sxs-lookup"><span data-stu-id="8438f-130">The Service Fabric Yeoman templates include a build script that you can use to build the app from the terminal (after navigating to the application folder).</span></span>

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-the-application"></a><span data-ttu-id="8438f-131">Distribuire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="8438f-131">Deploy the application</span></span>

<span data-ttu-id="8438f-132">Dopo aver compilato l'applicazione, è possibile distribuirla nel cluster locale.</span><span class="sxs-lookup"><span data-stu-id="8438f-132">Once the application is built, you can deploy it to the local cluster.</span></span>

1. <span data-ttu-id="8438f-133">Connettersi al cluster locale di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8438f-133">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="8438f-134">Eseguire lo script di installazione messo a disposizione nel modello per copiare il pacchetto dell'applicazione nell'archivio immagini del cluster, registrare il tipo di applicazione e creare un'istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8438f-134">Run the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="8438f-135">La distribuzione dell'applicazione compilata è uguale a quella di qualsiasi altra applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8438f-135">Deploying the built application is the same as any other Service Fabric application.</span></span> <span data-ttu-id="8438f-136">Per istruzioni dettagliate, vedere la documentazione sulla [gestione di un'applicazione di Service Fabric con l'interfaccia della riga di comando di Service Fabric](service-fabric-application-lifecycle-sfctl.md).</span><span class="sxs-lookup"><span data-stu-id="8438f-136">See the documentation on [managing a Service Fabric application with the Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="8438f-137">I parametri per questi comandi si trovano nei manifesti generati nel pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8438f-137">Parameters to these commands can be found in the generated manifests inside the application package.</span></span>

<span data-ttu-id="8438f-138">Dopo la distribuzione dell'applicazione, aprire un browser e passare a [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) all'indirizzo [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="8438f-138">Once the application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="8438f-139">Espandere quindi il nodo **Applicazioni**, nel quale sarà ora presente una voce per il tipo di applicazione e un'altra per la prima istanza del tipo.</span><span class="sxs-lookup"><span data-stu-id="8438f-139">Then, expand the **Applications** node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

## <a name="start-the-test-client-and-perform-a-failover"></a><span data-ttu-id="8438f-140">Avviare il client di test ed eseguire un failover</span><span class="sxs-lookup"><span data-stu-id="8438f-140">Start the test client and perform a failover</span></span>
<span data-ttu-id="8438f-141">I progetti Actor non eseguono alcuna operazione in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="8438f-141">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="8438f-142">Richiedono un altro servizio o client per l'invio dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="8438f-142">They require another service or client to send them messages.</span></span> <span data-ttu-id="8438f-143">Il modello Actor include un semplice script di test che è possibile usare per interagire con il servizio Actor.</span><span class="sxs-lookup"><span data-stu-id="8438f-143">The actor template includes a simple test script that you can use to interact with the actor service.</span></span>

1. <span data-ttu-id="8438f-144">Eseguire lo script tramite l'utilità delle espressioni di controllo per visualizzare l'output del servizio Actor.</span><span class="sxs-lookup"><span data-stu-id="8438f-144">Run the script using the watch utility to see the output of the actor service.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="8438f-145">In Service Fabric Explorer individuare il nodo che ospita la replica primaria del servizio Actor.</span><span class="sxs-lookup"><span data-stu-id="8438f-145">In Service Fabric Explorer, locate node hosting the primary replica for the actor service.</span></span> <span data-ttu-id="8438f-146">Nello screenshot seguente si tratta del nodo 3.</span><span class="sxs-lookup"><span data-stu-id="8438f-146">In the screenshot below, it is node 3.</span></span>

    ![Ricerca della replica primaria in Service Fabric Explorer][sfx-primary]
3. <span data-ttu-id="8438f-148">Fare clic sul nodo trovato nel passaggio precedente, quindi selezionare **Disattiva (riavvio)** dal menu Azioni.</span><span class="sxs-lookup"><span data-stu-id="8438f-148">Click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span></span> <span data-ttu-id="8438f-149">Questa operazione consente di riavviare un nodo nel cluster locale forzando il failover in una replica secondaria in esecuzione in un altro nodo.</span><span class="sxs-lookup"><span data-stu-id="8438f-149">This action restarts one node in your local cluster forcing a failover to a secondary replica running on another node.</span></span> <span data-ttu-id="8438f-150">Durante l'operazione, prestare attenzione all'output del client di test e notare che l'incremento del contatore prosegue nonostante il failover.</span><span class="sxs-lookup"><span data-stu-id="8438f-150">As you perform this action, pay attention to the output from the test client and note that the counter continues to increment despite the failover.</span></span>

## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="8438f-151">Aggiunta di altri servizi a un'applicazione esistente</span><span class="sxs-lookup"><span data-stu-id="8438f-151">Adding more services to an existing application</span></span>

<span data-ttu-id="8438f-152">Per aggiungere un altro servizio a un'applicazione già creata mediante `yo`, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8438f-152">To add another service to an application already created using `yo`, perform the following steps:</span></span>
1. <span data-ttu-id="8438f-153">Modificare la directory impostandola sulla radice dell'applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="8438f-153">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="8438f-154">Ad esempio, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` è l'applicazione creata da Yeoman.</span><span class="sxs-lookup"><span data-stu-id="8438f-154">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="8438f-155">Eseguire `yo azuresfcsharp:AddService`</span><span class="sxs-lookup"><span data-stu-id="8438f-155">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="migrating-from-projectjson-to-csproj"></a><span data-ttu-id="8438f-156">Migrazione da project.json a .csproj</span><span class="sxs-lookup"><span data-stu-id="8438f-156">Migrating from project.json to .csproj</span></span>
1. <span data-ttu-id="8438f-157">L'esecuzione di "dotnet migrate" nella directory radice del progetto consentirà la migrazione di tutti i file project.json al formato csproj.</span><span class="sxs-lookup"><span data-stu-id="8438f-157">Running 'dotnet migrate' in project root directory will migrate all the project.json to csproj format.</span></span>
2. <span data-ttu-id="8438f-158">Aggiornare di conseguenza i riferimenti al progetto ai file in formato csproj nei file di progetto.</span><span class="sxs-lookup"><span data-stu-id="8438f-158">Update the project references accordingly to csproj files in project files.</span></span>
3. <span data-ttu-id="8438f-159">Aggiornare i nomi dei file di progetto ai file in formato csproj in build.sh.</span><span class="sxs-lookup"><span data-stu-id="8438f-159">Update the project file names to csproj files in build.sh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8438f-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8438f-160">Next steps</span></span>

* [<span data-ttu-id="8438f-161">Altre informazioni su Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="8438f-161">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="8438f-162">Interagire con un cluster di Service Fabric usando l'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8438f-162">Interacting with Service Fabric clusters using the Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="8438f-163">Informazioni sulle [opzioni di supporto di Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="8438f-163">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="8438f-164">Introduzione all'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8438f-164">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
