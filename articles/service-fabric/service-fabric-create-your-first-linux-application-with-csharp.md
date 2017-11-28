---
title: aaaCreate la prima app di Azure microservizi in Linux con c# | Documenti Microsoft
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
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="34bc6-103">Creare la prima applicazione di Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="34bc6-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="34bc6-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="34bc6-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="34bc6-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="34bc6-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="34bc6-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="34bc6-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="34bc6-107">Service Fabric mette a disposizione SDK per la compilazione di servizi su Linux in .NET Core e Java.</span><span class="sxs-lookup"><span data-stu-id="34bc6-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="34bc6-108">In questa esercitazione viene illustrato come toocreate un'applicazione per Linux e creazione di un servizio utilizzando il linguaggio c# (Core .NET).</span><span class="sxs-lookup"><span data-stu-id="34bc6-108">In this tutorial, we look at how toocreate an application for Linux and build a service using C# (.NET Core).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34bc6-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="34bc6-109">Prerequisites</span></span>
<span data-ttu-id="34bc6-110">Prima di iniziare, assicurarsi di avere [configurato l'ambiente di sviluppo di Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="34bc6-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="34bc6-111">Se si usa Mac OS X è possibile [configurare un ambiente con un solo computer Linux in una macchina virtuale usando Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="34bc6-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="34bc6-112">È anche possibile hello tooinstall [servizio infrastruttura CLI](service-fabric-cli.md)</span><span class="sxs-lookup"><span data-stu-id="34bc6-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md)</span></span>

### <a name="install-and-set-up-hello-generators-for-csharp"></a><span data-ttu-id="34bc6-113">Installare e configurare i generatori di hello per CSharp</span><span class="sxs-lookup"><span data-stu-id="34bc6-113">Install and set up hello generators for CSharp</span></span>
<span data-ttu-id="34bc6-114">Service Fabric offre gli strumenti di scaffolding che consentono di creare un'applicazione CSharp per Service Fabric dal terminale tramite il generatore di modelli Yeoman.</span><span class="sxs-lookup"><span data-stu-id="34bc6-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric CSharp application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="34bc6-115">Eseguire procedure hello sotto tooensure che si dispone di hello Service Fabric modello yeoman generatore per CSharp utilizzo nel computer.</span><span class="sxs-lookup"><span data-stu-id="34bc6-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for CSharp working on your machine.</span></span>
1. <span data-ttu-id="34bc6-116">Installare nodejs e NPM nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="34bc6-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="34bc6-117">Installare il generatore di modelli [Yeoman](http://yeoman.io/) nella macchina virtuale da NPM</span><span class="sxs-lookup"><span data-stu-id="34bc6-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="34bc6-118">Installare generatore di applicazione di servizio Fabric Yeo Java hello da NPM</span><span class="sxs-lookup"><span data-stu-id="34bc6-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a><span data-ttu-id="34bc6-119">Creare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="34bc6-119">Create hello application</span></span>
<span data-ttu-id="34bc6-120">Un'applicazione di Service Fabric può contenere uno o più servizi, ognuno con un ruolo specifico nell'offerta di funzionalità dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="34bc6-120">A Service Fabric application can contain one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="34bc6-121">Hello Service Fabric [Yeoman](http://yeoman.io/) toocreate facile rende generatore per CSharp, cui è installato nell'ultimo passaggio, il primo servizio e tooadd più avanti.</span><span class="sxs-lookup"><span data-stu-id="34bc6-121">hello Service Fabric [Yeoman](http://yeoman.io/) generator for CSharp, which you installed in last step, makes it easy toocreate your first service and tooadd more later.</span></span> <span data-ttu-id="34bc6-122">Consente di usare Yeoman toocreate un'applicazione con un singolo servizio.</span><span class="sxs-lookup"><span data-stu-id="34bc6-122">Let's use Yeoman toocreate an application with a single service.</span></span>

1. <span data-ttu-id="34bc6-123">In un terminale, digitare hello compilazione lo scaffolding hello toostart di comando seguente:`yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="34bc6-123">In a terminal, type hello following command toostart building hello scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="34bc6-124">Assegnare un nome all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="34bc6-124">Name your application.</span></span>
3. <span data-ttu-id="34bc6-125">Scegliere il tipo di hello del primo servizio e il nome.</span><span class="sxs-lookup"><span data-stu-id="34bc6-125">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="34bc6-126">Ai fini di hello di questa esercitazione, si sceglie un servizio Actor affidabile.</span><span class="sxs-lookup"><span data-stu-id="34bc6-126">For hello purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![Generatore Yeoman di Service Fabric per C#][sf-yeoman]

> [!NOTE]
> <span data-ttu-id="34bc6-128">Per ulteriori informazioni sulle opzioni di hello, vedere [Cenni preliminari sul modello di programmazione di Service Fabric](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="34bc6-128">For more information about hello options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
>
>

## <a name="build-hello-application"></a><span data-ttu-id="34bc6-129">Compilare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="34bc6-129">Build hello application</span></span>
<span data-ttu-id="34bc6-130">modelli di servizio dell'infrastruttura Yeoman Hello includono uno script di compilazione che è possibile utilizzare l'applicazione hello toobuild da hello terminal (dopo una navigazione toohello cartella dell'applicazione).</span><span class="sxs-lookup"><span data-stu-id="34bc6-130">hello Service Fabric Yeoman templates include a build script that you can use toobuild hello app from hello terminal (after navigating toohello application folder).</span></span>

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="34bc6-131">Distribuire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="34bc6-131">Deploy hello application</span></span>

<span data-ttu-id="34bc6-132">Una volta creata l'applicazione hello, è possibile distribuire cluster locale toohello.</span><span class="sxs-lookup"><span data-stu-id="34bc6-132">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="34bc6-133">Connettere il cluster di Service Fabric locale toohello.</span><span class="sxs-lookup"><span data-stu-id="34bc6-133">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="34bc6-134">Eseguire script di installazione di hello fornito in hello modello toocopy applicazione hello pacchetto archivio immagini toohello del cluster, registrare il tipo di applicazione hello e creare un'istanza di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="34bc6-134">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="34bc6-135">Distribuire un'applicazione hello compilato è hello stesso come qualsiasi altra applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="34bc6-135">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="34bc6-136">Vedere la documentazione di hello su [la gestione di un'applicazione di Service Fabric con hello servizio infrastruttura CLI](service-fabric-application-lifecycle-sfctl.md) per istruzioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="34bc6-136">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="34bc6-137">I parametri toothese comandi sono disponibili nei manifesti hello generato all'interno del pacchetto di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="34bc6-137">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="34bc6-138">Dopo la distribuzione di un'applicazione hello, aprire un browser e passare a [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) in [http://localhost:19080/Esplora](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="34bc6-138">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="34bc6-139">Espandere quindi hello **applicazioni** nodo e notare che è ora disponibile una voce per il tipo di applicazione e un altro per hello prima istanza di quel tipo.</span><span class="sxs-lookup"><span data-stu-id="34bc6-139">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="34bc6-140">Avviare il client di prova hello ed eseguire un failover</span><span class="sxs-lookup"><span data-stu-id="34bc6-140">Start hello test client and perform a failover</span></span>
<span data-ttu-id="34bc6-141">I progetti Actor non eseguono alcuna operazione in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="34bc6-141">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="34bc6-142">Un altro servizio o client di toosend richiedono tali messaggi.</span><span class="sxs-lookup"><span data-stu-id="34bc6-142">They require another service or client toosend them messages.</span></span> <span data-ttu-id="34bc6-143">modello attore Hello include uno script di test semplice che è possibile utilizzare toointeract con servizio actor hello.</span><span class="sxs-lookup"><span data-stu-id="34bc6-143">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="34bc6-144">Eseguire script hello utilizzando hello espressioni di controllo utilità toosee hello output del servizio actor hello.</span><span class="sxs-lookup"><span data-stu-id="34bc6-144">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="34bc6-145">In Service Fabric Explorer, individuare il nodo che ospita la replica primaria di hello per servizio actor hello.</span><span class="sxs-lookup"><span data-stu-id="34bc6-145">In Service Fabric Explorer, locate node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="34bc6-146">Nella schermata di hello riportata di seguito, è il nodo 3.</span><span class="sxs-lookup"><span data-stu-id="34bc6-146">In hello screenshot below, it is node 3.</span></span>

    ![Trovare la replica primaria hello in Service Fabric Explorer][sfx-primary]
3. <span data-ttu-id="34bc6-148">Fare clic sul nodo hello è stata individuata nel passaggio precedente hello, scegliere **Deactivate (riavvio)** dal menu Azioni hello.</span><span class="sxs-lookup"><span data-stu-id="34bc6-148">Click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="34bc6-149">Questa azione riavvia un nodo del cluster locale, forzando una replica secondaria tooa failover in esecuzione in un altro nodo.</span><span class="sxs-lookup"><span data-stu-id="34bc6-149">This action restarts one node in your local cluster forcing a failover tooa secondary replica running on another node.</span></span> <span data-ttu-id="34bc6-150">Come eseguire questa azione, si paga output toohello attenzione dal client di prova hello e annotare che tale contatore hello continua tooincrement nonostante hello failover.</span><span class="sxs-lookup"><span data-stu-id="34bc6-150">As you perform this action, pay attention toohello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="34bc6-151">Aggiunta di ulteriori servizi tooan esistente dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="34bc6-151">Adding more services tooan existing application</span></span>

<span data-ttu-id="34bc6-152">tooadd già un'altra applicazione tooan di servizio creato utilizzando `yo`, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="34bc6-152">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span>
1. <span data-ttu-id="34bc6-153">Cambiare directory toohello principale di un'applicazione hello esistente.</span><span class="sxs-lookup"><span data-stu-id="34bc6-153">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="34bc6-154">Ad esempio, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` è un'applicazione hello creata da Yeoman.</span><span class="sxs-lookup"><span data-stu-id="34bc6-154">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="34bc6-155">Eseguire `yo azuresfcsharp:AddService`</span><span class="sxs-lookup"><span data-stu-id="34bc6-155">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="migrating-from-projectjson-toocsproj"></a><span data-ttu-id="34bc6-156">La migrazione da Project too.csproj</span><span class="sxs-lookup"><span data-stu-id="34bc6-156">Migrating from project.json too.csproj</span></span>
1. <span data-ttu-id="34bc6-157">In esecuzione 'dotnet eseguire la migrazione' nella directory radice del progetto verrà eseguita la migrazione toocsproj formato JSON di tutti i hello.</span><span class="sxs-lookup"><span data-stu-id="34bc6-157">Running 'dotnet migrate' in project root directory will migrate all hello project.json toocsproj format.</span></span>
2. <span data-ttu-id="34bc6-158">Aggiornamento hello progetto fa riferimento a conseguenza toocsproj file nei file di progetto.</span><span class="sxs-lookup"><span data-stu-id="34bc6-158">Update hello project references accordingly toocsproj files in project files.</span></span>
3. <span data-ttu-id="34bc6-159">Aggiornare i file hello progetto file nomi toocsproj in build.sh.</span><span class="sxs-lookup"><span data-stu-id="34bc6-159">Update hello project file names toocsproj files in build.sh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34bc6-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="34bc6-160">Next steps</span></span>

* [<span data-ttu-id="34bc6-161">Altre informazioni su Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="34bc6-161">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="34bc6-162">L'interazione con i cluster di Service Fabric usando hello servizio infrastruttura CLI</span><span class="sxs-lookup"><span data-stu-id="34bc6-162">Interacting with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="34bc6-163">Informazioni sulle [opzioni di supporto di Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="34bc6-163">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="34bc6-164">Introduzione all'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="34bc6-164">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
