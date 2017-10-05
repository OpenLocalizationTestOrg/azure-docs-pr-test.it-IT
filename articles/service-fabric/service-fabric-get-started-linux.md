---
title: Configurare l'ambiente di sviluppo in Linux | Microsoft Docs
description: "Installare il runtime e l'SDK e creare un cluster di sviluppo locale in Linux. Al termine della configurazione, sarà possibile iniziare a sviluppare applicazioni."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 58c6bbbb16d7008e6b573cf8dbc8cf62da9789f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="1abd5-104">Preparare l'ambiente di sviluppo in Linux</span><span class="sxs-lookup"><span data-stu-id="1abd5-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1abd5-105">Windows</span><span class="sxs-lookup"><span data-stu-id="1abd5-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="1abd5-106">Linux</span><span class="sxs-lookup"><span data-stu-id="1abd5-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="1abd5-107">OSX</span><span class="sxs-lookup"><span data-stu-id="1abd5-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="1abd5-108">Per distribuire ed eseguire [applicazioni di Azure Service Fabric](service-fabric-application-model.md) in un computer di sviluppo Linux, installare il runtime e l'SDK comune.</span><span class="sxs-lookup"><span data-stu-id="1abd5-108">To deploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install the runtime and common SDK.</span></span> <span data-ttu-id="1abd5-109">È anche possibile installare SDK facoltativi per Java e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="1abd5-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1abd5-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1abd5-110">Prerequisites</span></span>

<span data-ttu-id="1abd5-111">Per lo sviluppo, sono supportati i sistemi operativi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1abd5-111">The following operating system versions are supported for development:</span></span>

* <span data-ttu-id="1abd5-112">Ubuntu 16.04 (`Xenial Xerus`)</span><span class="sxs-lookup"><span data-stu-id="1abd5-112">Ubuntu 16.04 (`Xenial Xerus`)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="1abd5-113">Aggiornare le origini APT</span><span class="sxs-lookup"><span data-stu-id="1abd5-113">Update your APT sources</span></span>
<span data-ttu-id="1abd5-114">Per installare l'SDK e il pacchetto di runtime associato tramite lo strumento da riga di comando apt-get, è prima necessario aggiornare le origini APT (Advanced Packaging Tool).</span><span class="sxs-lookup"><span data-stu-id="1abd5-114">To install the SDK and the associated runtime package via the apt-get command-line tool, you must first update your Advanced Packaging Tool (APT) sources.</span></span>

1. <span data-ttu-id="1abd5-115">Aprire un terminale.</span><span class="sxs-lookup"><span data-stu-id="1abd5-115">Open a terminal.</span></span>
2. <span data-ttu-id="1abd5-116">Aggiungere il repository di Service Fabric all'elenco di origini.</span><span class="sxs-lookup"><span data-stu-id="1abd5-116">Add the Service Fabric repo to your sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. <span data-ttu-id="1abd5-117">Aggiungere il repository `dotnet` all'elenco di origini.</span><span class="sxs-lookup"><span data-stu-id="1abd5-117">Add the `dotnet` repo to your sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. <span data-ttu-id="1abd5-118">Aggiungere la nuova chiave Gnu Privacy Guard (GnuPG o GPG) al keyring di APT.</span><span class="sxs-lookup"><span data-stu-id="1abd5-118">Add the new Gnu Privacy Guard (GnuPG, or GPG) key to your APT keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="1abd5-119">Aggiungere la chiave GPG Docker ufficiale al keyring di APT.</span><span class="sxs-lookup"><span data-stu-id="1abd5-119">Add the official Docker GPG key to your APT keyring.</span></span>

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. <span data-ttu-id="1abd5-120">Configurare il repository di Docker.</span><span class="sxs-lookup"><span data-stu-id="1abd5-120">Set up the Docker repository.</span></span>

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. <span data-ttu-id="1abd5-121">Aggiornare l'elenco dei pacchetti in base ai repository appena aggiunti.</span><span class="sxs-lookup"><span data-stu-id="1abd5-121">Refresh your package lists based on the newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-the-sdk-for-local-cluster-setup"></a><span data-ttu-id="1abd5-122">Installare e configurare l'SDK per la configurazione del cluster locale</span><span class="sxs-lookup"><span data-stu-id="1abd5-122">Install and set up the SDK for local cluster setup</span></span>

<span data-ttu-id="1abd5-123">Dopo aver aggiornato le origini, è possibile installare l'SDK.</span><span class="sxs-lookup"><span data-stu-id="1abd5-123">After you have updated your sources, you can install the SDK.</span></span> <span data-ttu-id="1abd5-124">Installare il pacchetto Service Fabric SDK, confermare l'installazione e accettare il contratto di licenza.</span><span class="sxs-lookup"><span data-stu-id="1abd5-124">Install the Service Fabric SDK package, confirm the installation, and agree to the license agreement.</span></span>

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   <span data-ttu-id="1abd5-125">I comandi seguenti permettono di automatizzare l'accettazione della licenza per i pacchetti di Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="1abd5-125">The following commands automate accepting the license for Service Fabric packages:</span></span>
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a><span data-ttu-id="1abd5-126">Configurare un cluster locale</span><span class="sxs-lookup"><span data-stu-id="1abd5-126">Set up a local cluster</span></span>
  <span data-ttu-id="1abd5-127">Se l'installazione ha esito positivo, sarà possibile avviare un cluster locale.</span><span class="sxs-lookup"><span data-stu-id="1abd5-127">If the installation is successful, you should be able to start a local cluster.</span></span>

  1. <span data-ttu-id="1abd5-128">Eseguire lo script di configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="1abd5-128">Run the cluster setup script.</span></span>

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. <span data-ttu-id="1abd5-129">Aprire un Web browser e passare a [Service Fabric Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="1abd5-129">Open a web browser and go to [Service Fabric Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="1abd5-130">Se il cluster è stato avviato, verrà visualizzato il dashboard di Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="1abd5-130">If the cluster has started, you should see the Service Fabric Explorer dashboard.</span></span>

      ![Service Fabric Explorer in Linux][sfx-linux]

  <span data-ttu-id="1abd5-132">A questo punto, è possibile distribuire pacchetti di applicazione di Service Fabric predefiniti o nuovi pacchetti basati su contenitori o eseguibili guest.</span><span class="sxs-lookup"><span data-stu-id="1abd5-132">At this point, you can deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="1abd5-133">Per creare nuovi servizi usando gli SDK per Java o .NET Core, seguire le procedure di configurazione facoltative riportate nelle sezioni successive.</span><span class="sxs-lookup"><span data-stu-id="1abd5-133">To build new services by using the Java or .NET Core SDKs, follow the optional setup steps that are provided in subsequent sections.</span></span>


  > [!NOTE]
  > <span data-ttu-id="1abd5-134">I cluster autonomi non sono supportati in Linux.</span><span class="sxs-lookup"><span data-stu-id="1abd5-134">Standalone clusters aren't supported in Linux.</span></span> <span data-ttu-id="1abd5-135">L'anteprima supporta solo cluster con un solo computer e più computer Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="1abd5-135">The preview supports only one-box and Azure Linux multi-machine clusters.</span></span>
  >

## <a name="set-up-the-service-fabric-cli"></a><span data-ttu-id="1abd5-136">Configurare l'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1abd5-136">Set up the Service Fabric CLI</span></span>

<span data-ttu-id="1abd5-137">L'[interfaccia della riga di comando di Service Fabric](service-fabric-cli.md) include comandi per l'interazione con entità di Service Fabric, come cluster e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1abd5-137">The [Service Fabric CLI](service-fabric-cli.md) has commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="1abd5-138">È basato su python, quindi occorre assicurarsi che python e pip siano installati prima di continuare con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1abd5-138">It is based on python, so be sure to have python and pip installed before you proceed with the following command:</span></span>

```bash
pip install sfctl
```

## <a name="install-and-set-up-the-generators-for-containers-and-guest-executables"></a><span data-ttu-id="1abd5-139">Installare e configurare i generatori per contenitori ed eseguibili guest</span><span class="sxs-lookup"><span data-stu-id="1abd5-139">Install and set up the generators for containers and guest-executables</span></span>
<span data-ttu-id="1abd5-140">Service Fabric offre gli strumenti di scaffolding che consentono di creare applicazioni Service Fabric dal terminale tramite il generatore di modelli Yeoman.</span><span class="sxs-lookup"><span data-stu-id="1abd5-140">Service Fabric provides scaffolding tools which will help you create a Service Fabric applications from terminal using Yeoman template generator.</span></span> <span data-ttu-id="1abd5-141">Seguire questa procedura per assicurarsi che nella macchina virtuale sia disponibile il generatore di modelli Yeoman di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1abd5-141">Please follow the steps below to ensure you have the Service Fabric yeoman template generator for working on your machine.</span></span>

1. <span data-ttu-id="1abd5-142">Installare nodejs e NPM nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="1abd5-142">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="1abd5-143">Installare il generatore di modelli [Yeoman](http://yeoman.io/) nella macchina virtuale da NPM</span><span class="sxs-lookup"><span data-stu-id="1abd5-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="1abd5-144">Installare il generatore di contenitori Yeo per Service Fabric e il generatore di eseguibili guest da NPM</span><span class="sxs-lookup"><span data-stu-id="1abd5-144">Install the Service Fabric Yeo container generator and guest execuatble generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

<span data-ttu-id="1abd5-145">Al termine dell'installazione dei generatori precedenti, dovrebbe essere possibile creare app con eseguibili guest o servizi contenitore eseguendo `yo azuresfguest` o `yo azuresfcontainer` rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="1abd5-145">After you have installed the above generators, you should be able to create apps with guest executable or container services by running `yo azuresfguest` or `yo azuresfcontainer` respectively.</span></span>

## <a name="install-the-necessary-java-artifacts-optional-if-you-want-to-use-the-java-programming-models"></a><span data-ttu-id="1abd5-146">Installare gli elementi Java necessari (facoltativo se si vogliono usare i modelli di programmazione Java)</span><span class="sxs-lookup"><span data-stu-id="1abd5-146">Install the necessary Java artifacts (optional, if you want to use the Java programming models)</span></span>

<span data-ttu-id="1abd5-147">Per creare servizi di Service Fabric usando Java, assicurarsi che JDK 1.8 sia installato insieme a Gradle, usato per l'esecuzione di attività di compilazione.</span><span class="sxs-lookup"><span data-stu-id="1abd5-147">To build Service Fabric services using Java, ensure you have JDK 1.8 installed along with Gradle which is used for running build tasks.</span></span> <span data-ttu-id="1abd5-148">Il frammento di codice seguente installa Open JDK 1.8 insieme a Gradle.</span><span class="sxs-lookup"><span data-stu-id="1abd5-148">The following snippet installs Open JDK 1.8 along with Gradle.</span></span> <span data-ttu-id="1abd5-149">Il pull delle librerie Java per Service Fabric viene eseguito da Maven.</span><span class="sxs-lookup"><span data-stu-id="1abd5-149">The Service Fabric Java libraries are pulled from Maven.</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-the-eclipse-neon-plug-in-optional"></a><span data-ttu-id="1abd5-150">Installare il plug-in Eclipse Neon (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="1abd5-150">Install the Eclipse Neon plug-in (optional)</span></span>

<span data-ttu-id="1abd5-151">È possibile installare il plug-in Eclipse per Service Fabric dall'**IDE di Eclipse per sviluppatori Java**.</span><span class="sxs-lookup"><span data-stu-id="1abd5-151">You can install the Eclipse plug-in for Service Fabric from within the **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="1abd5-152">È possibile usare Eclipse per creare applicazioni contenitore e applicazioni eseguibili guest di Service Fabric in aggiunta alle applicazioni Java di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1abd5-152">You can use Eclipse to create Service Fabric guest executable applications and container applications in addition to Service Fabric Java applications.</span></span>

1. <span data-ttu-id="1abd5-153">In Eclipse assicurarsi che sia installata l'ultima versione di Eclipse Neon e di Buildship (1.0.17 o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="1abd5-153">In Eclipse, ensure that you have latest Eclipse Neon and the latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="1abd5-154">Per controllare le versioni dei componenti installati, selezionare **Help** > **Installation Details** (? > Dettagli installazione).</span><span class="sxs-lookup"><span data-stu-id="1abd5-154">You can check the versions of installed components by selecting **Help** > **Installation Details**.</span></span> <span data-ttu-id="1abd5-155">È possibile aggiornare Buildship seguendo le istruzioni riportate in [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update] (Eclipse Buildship: plug-in Eclipse per Gradle).</span><span class="sxs-lookup"><span data-stu-id="1abd5-155">You can update Buildship by using the instructions at [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>

2. <span data-ttu-id="1abd5-156">Per installare il plug-in Service Fabric, selezionare **Help** > **Install New Software** (? > Installa nuovo software).</span><span class="sxs-lookup"><span data-stu-id="1abd5-156">To install the Service Fabric plug-in, select **Help** > **Install New Software**.</span></span>

3. <span data-ttu-id="1abd5-157">Nella casella **Work with** (Usa) digitare **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="1abd5-157">In the **Work with** box, type **http://dl.microsoft.com/eclipse**.</span></span>

4. <span data-ttu-id="1abd5-158">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1abd5-158">Click **Add**.</span></span>

    ![Pagina relativa al software disponibile][sf-eclipse-plugin]

5. <span data-ttu-id="1abd5-160">Selezionare il plug-in **ServiceFabric** e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="1abd5-160">Select the **ServiceFabric** plug-in, and then click **Next**.</span></span>

6. <span data-ttu-id="1abd5-161">Completare la procedura di installazione e quindi accettare il contratto di licenza con l'utente finale.</span><span class="sxs-lookup"><span data-stu-id="1abd5-161">Complete the installation steps, and then accept the end-user license agreement.</span></span>

<span data-ttu-id="1abd5-162">Se il plug-in Eclipse per Service Fabric è già installato, verificare che la versione sia la più recente.</span><span class="sxs-lookup"><span data-stu-id="1abd5-162">If you already have the Service Fabric Eclipse plug-in installed, make sure that you have the latest version.</span></span> <span data-ttu-id="1abd5-163">Per controllare, selezionare **Help** > **Installation Details** (? > Dettagli installazione) e quindi cercare Service Fabric nell'elenco dei plug-in installati. Se è disponibile una versione più recente, selezionare **Update** (Aggiorna).</span><span class="sxs-lookup"><span data-stu-id="1abd5-163">You can check by selecting **Help** > **Installation Details** and then searching for Service Fabric in the list of installed plug-ins. If a newer version is available, select **Update**.</span></span>

<span data-ttu-id="1abd5-164">Per altre informazioni, vedere [Plug-in Service Fabric per lo sviluppo di applicazioni Java in Eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="1abd5-164">For more information, see [Service Fabric plug-in for Eclipse Java application development](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-the-net-core-sdk-optional-if-you-want-to-use-the-net-core-programming-models"></a><span data-ttu-id="1abd5-165">Installare .NET Core SDK (facoltativo, per usare i modelli di programmazione .NET Core)</span><span class="sxs-lookup"><span data-stu-id="1abd5-165">Install the .NET Core SDK (optional, if you want to use the .NET Core programming models)</span></span>
<span data-ttu-id="1abd5-166">.NET Core SDK offre le librerie e i modelli necessari per creare servizi di Service Fabric con .NET Core.</span><span class="sxs-lookup"><span data-stu-id="1abd5-166">The .NET Core SDK provides the libraries and templates that are required to build Service Fabric services with .NET Core.</span></span> <span data-ttu-id="1abd5-167">Installare il pacchetto .NET Core SDK eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="1abd5-167">Install the .NET Core SDK package by running the following -</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-the-sdk-and-runtime"></a><span data-ttu-id="1abd5-168">Aggiornare SDK e runtime</span><span class="sxs-lookup"><span data-stu-id="1abd5-168">Update the SDK and runtime</span></span>

<span data-ttu-id="1abd5-169">Per aggiornare l'SDK e il runtime alla versione più recente, eseguire questi comandi deselezionando gli SDK da non aggiornare:</span><span class="sxs-lookup"><span data-stu-id="1abd5-169">To update to the latest version of the SDK and runtime, run the following commands (deselect the SDKs that you don't want):</span></span>

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
<span data-ttu-id="1abd5-170">Per aggiornare i file binari Java SDK da Maven, è necessario aggiornare i dettagli della versione del file binario corrispondente nel file ``build.gradle`` in modo che facciano riferimento alla versione più recente.</span><span class="sxs-lookup"><span data-stu-id="1abd5-170">To update the Java SDK binaries from Maven, you need to update the version details of the corresponding binary in the ``build.gradle`` file to point to the latest version.</span></span> <span data-ttu-id="1abd5-171">Per individuare esattamente il punto in cui è necessario aggiornare la versione, è possibile vedere qualsiasi file ``build.gradle`` negli esempi introduttivi di Service Fabric , disponibili [qui](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="1abd5-171">To know exactly where you need to update the version, you can refer to any ``build.gradle`` file in Service Fabric getting-started samples [here](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="1abd5-172">L'aggiornamento dei pacchetti può causare l'arresto dell'esecuzione del cluster di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="1abd5-172">Updating the packages might cause your local development cluster to stop running.</span></span> <span data-ttu-id="1abd5-173">Riavviare il cluster locale dopo un aggiornamento seguendo le istruzioni disponibili in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="1abd5-173">Restart your local cluster after an upgrade by following the instructions on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1abd5-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1abd5-174">Next steps</span></span>

* [<span data-ttu-id="1abd5-175">Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando Yeoman</span><span class="sxs-lookup"><span data-stu-id="1abd5-175">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="1abd5-176">Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando il plug-in Service Fabric per Eclipse</span><span class="sxs-lookup"><span data-stu-id="1abd5-176">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="1abd5-177">Creare la prima applicazione CSharp in Linux</span><span class="sxs-lookup"><span data-stu-id="1abd5-177">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="1abd5-178">Preparare l'ambiente di sviluppo in OSX</span><span class="sxs-lookup"><span data-stu-id="1abd5-178">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="1abd5-179">Usare l'interfaccia della riga di comando di Service Fabric per gestire le applicazioni</span><span class="sxs-lookup"><span data-stu-id="1abd5-179">Use the Service Fabric CLI to manage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="1abd5-180">Differenze in Service Fabric tra Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="1abd5-180">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
* [<span data-ttu-id="1abd5-181">Introduzione all'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1abd5-181">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
