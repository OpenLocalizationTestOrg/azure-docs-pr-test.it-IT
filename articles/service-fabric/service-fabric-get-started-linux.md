---
title: aaaSet dell'ambiente di sviluppo in Linux | Documenti Microsoft
description: "Installare SDK e il runtime hello e creare un cluster di sviluppo locale in Linux. Dopo aver completato il programma di installazione, sarà pronto toobuild applicazioni."
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
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="9db05-104">Preparare l'ambiente di sviluppo in Linux</span><span class="sxs-lookup"><span data-stu-id="9db05-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9db05-105">Windows</span><span class="sxs-lookup"><span data-stu-id="9db05-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="9db05-106">Linux</span><span class="sxs-lookup"><span data-stu-id="9db05-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="9db05-107">OSX</span><span class="sxs-lookup"><span data-stu-id="9db05-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="9db05-108">toodeploy ed eseguire [applicazioni Azure Service Fabric](service-fabric-application-model.md) nel computer di sviluppo di Linux, installare il runtime hello e SDK comuni.</span><span class="sxs-lookup"><span data-stu-id="9db05-108">toodeploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install hello runtime and common SDK.</span></span> <span data-ttu-id="9db05-109">È anche possibile installare SDK facoltativi per Java e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="9db05-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9db05-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9db05-110">Prerequisites</span></span>

<span data-ttu-id="9db05-111">Hello seguenti versioni del sistema operativo è supportato per lo sviluppo:</span><span class="sxs-lookup"><span data-stu-id="9db05-111">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="9db05-112">Ubuntu 16.04 (`Xenial Xerus`)</span><span class="sxs-lookup"><span data-stu-id="9db05-112">Ubuntu 16.04 (`Xenial Xerus`)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="9db05-113">Aggiornare le origini APT</span><span class="sxs-lookup"><span data-stu-id="9db05-113">Update your APT sources</span></span>
<span data-ttu-id="9db05-114">tooinstall hello SDK e hello runtime associato pacchetto tramite lo strumento da riga di comando di hello apt get, è innanzitutto necessario aggiornare le origini di strumento di creazione di pacchetti avanzate (APT).</span><span class="sxs-lookup"><span data-stu-id="9db05-114">tooinstall hello SDK and hello associated runtime package via hello apt-get command-line tool, you must first update your Advanced Packaging Tool (APT) sources.</span></span>

1. <span data-ttu-id="9db05-115">Aprire un terminale.</span><span class="sxs-lookup"><span data-stu-id="9db05-115">Open a terminal.</span></span>
2. <span data-ttu-id="9db05-116">Aggiungere l'elenco delle origini tooyour repository hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9db05-116">Add hello Service Fabric repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. <span data-ttu-id="9db05-117">Aggiungere hello `dotnet` elenco delle origini tooyour repository.</span><span class="sxs-lookup"><span data-stu-id="9db05-117">Add hello `dotnet` repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. <span data-ttu-id="9db05-118">Aggiungere hello keyring APT tooyour nuovo Guard di Privacy Gnu (GnuPG o GPG) della chiave.</span><span class="sxs-lookup"><span data-stu-id="9db05-118">Add hello new Gnu Privacy Guard (GnuPG, or GPG) key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="9db05-119">Aggiungere hello ufficiale Docker GPG tooyour chiave APT keyring.</span><span class="sxs-lookup"><span data-stu-id="9db05-119">Add hello official Docker GPG key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. <span data-ttu-id="9db05-120">Impostare il repository di Docker hello.</span><span class="sxs-lookup"><span data-stu-id="9db05-120">Set up hello Docker repository.</span></span>

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. <span data-ttu-id="9db05-121">Il pacchetto di aggiornamento elenchi basati su hello appena aggiunto repository.</span><span class="sxs-lookup"><span data-stu-id="9db05-121">Refresh your package lists based on hello newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a><span data-ttu-id="9db05-122">Installare e configurare hello SDK per l'installazione del cluster locale</span><span class="sxs-lookup"><span data-stu-id="9db05-122">Install and set up hello SDK for local cluster setup</span></span>

<span data-ttu-id="9db05-123">Dopo aver aggiornato le origini, è possibile installare hello SDK.</span><span class="sxs-lookup"><span data-stu-id="9db05-123">After you have updated your sources, you can install hello SDK.</span></span> <span data-ttu-id="9db05-124">Installare il pacchetto di Service Fabric SDK hello, confermare l'installazione di hello e accettare il contratto di licenza toohello.</span><span class="sxs-lookup"><span data-stu-id="9db05-124">Install hello Service Fabric SDK package, confirm hello installation, and agree toohello license agreement.</span></span>

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   <span data-ttu-id="9db05-125">Hello seguenti comandi automatizzare accettazione licenza hello per i pacchetti di Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="9db05-125">hello following commands automate accepting hello license for Service Fabric packages:</span></span>
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a><span data-ttu-id="9db05-126">Configurare un cluster locale</span><span class="sxs-lookup"><span data-stu-id="9db05-126">Set up a local cluster</span></span>
  <span data-ttu-id="9db05-127">Se l'installazione hello ha esito positivo, dovrebbe essere in grado di toostart un cluster locale.</span><span class="sxs-lookup"><span data-stu-id="9db05-127">If hello installation is successful, you should be able toostart a local cluster.</span></span>

  1. <span data-ttu-id="9db05-128">Eseguire lo script di installazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9db05-128">Run hello cluster setup script.</span></span>

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. <span data-ttu-id="9db05-129">Aprire un web browser e andare troppo[Service Fabric Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="9db05-129">Open a web browser and go too[Service Fabric Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="9db05-130">Se il cluster hello è avviato, vedrai il dashboard di Service Fabric Explorer hello.</span><span class="sxs-lookup"><span data-stu-id="9db05-130">If hello cluster has started, you should see hello Service Fabric Explorer dashboard.</span></span>

      ![Service Fabric Explorer in Linux][sfx-linux]

  <span data-ttu-id="9db05-132">A questo punto, è possibile distribuire pacchetti di applicazione di Service Fabric predefiniti o nuovi pacchetti basati su contenitori o eseguibili guest.</span><span class="sxs-lookup"><span data-stu-id="9db05-132">At this point, you can deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="9db05-133">toobuild nuovi servizi tramite Java hello o .NET Core SDK, seguire i passaggi di configurazione facoltativi hello fornite nelle sezioni successive.</span><span class="sxs-lookup"><span data-stu-id="9db05-133">toobuild new services by using hello Java or .NET Core SDKs, follow hello optional setup steps that are provided in subsequent sections.</span></span>


  > [!NOTE]
  > <span data-ttu-id="9db05-134">I cluster autonomi non sono supportati in Linux.</span><span class="sxs-lookup"><span data-stu-id="9db05-134">Standalone clusters aren't supported in Linux.</span></span> <span data-ttu-id="9db05-135">Hello anteprima supporta solo a una casella e i cluster con più computer Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="9db05-135">hello preview supports only one-box and Azure Linux multi-machine clusters.</span></span>
  >

## <a name="set-up-hello-service-fabric-cli"></a><span data-ttu-id="9db05-136">Impostare i servizi dell'infrastruttura CLI hello</span><span class="sxs-lookup"><span data-stu-id="9db05-136">Set up hello Service Fabric CLI</span></span>

<span data-ttu-id="9db05-137">Hello [servizio infrastruttura CLI](service-fabric-cli.md) sono disponibili comandi per l'interazione con le entità di Service Fabric, incluse le applicazioni e i cluster.</span><span class="sxs-lookup"><span data-stu-id="9db05-137">hello [Service Fabric CLI](service-fabric-cli.md) has commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="9db05-138">È basato su python, è necessario che toohave python e pip installato prima di procedere con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9db05-138">It is based on python, so be sure toohave python and pip installed before you proceed with hello following command:</span></span>

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a><span data-ttu-id="9db05-139">Installare e configurare i generatori di hello per contenitori e i file eseguibili di guest</span><span class="sxs-lookup"><span data-stu-id="9db05-139">Install and set up hello generators for containers and guest-executables</span></span>
<span data-ttu-id="9db05-140">Service Fabric offre gli strumenti di scaffolding che consentono di creare applicazioni Service Fabric dal terminale tramite il generatore di modelli Yeoman.</span><span class="sxs-lookup"><span data-stu-id="9db05-140">Service Fabric provides scaffolding tools which will help you create a Service Fabric applications from terminal using Yeoman template generator.</span></span> <span data-ttu-id="9db05-141">Eseguire procedure hello sotto tooensure che si dispone di hello Service Fabric modello yeoman generatore per l'utilizzo nel computer.</span><span class="sxs-lookup"><span data-stu-id="9db05-141">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for working on your machine.</span></span>

1. <span data-ttu-id="9db05-142">Installare nodejs e NPM nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="9db05-142">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="9db05-143">Installare il generatore di modelli [Yeoman](http://yeoman.io/) nella macchina virtuale da NPM</span><span class="sxs-lookup"><span data-stu-id="9db05-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="9db05-144">Installare generatore di hello Yeo dell'infrastruttura del servizio contenitore e il generatore di execuatble guest da NPM</span><span class="sxs-lookup"><span data-stu-id="9db05-144">Install hello Service Fabric Yeo container generator and guest execuatble generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

<span data-ttu-id="9db05-145">Dopo aver installato hello sopra i generatori, dovrebbe essere in grado di toocreate App con i servizi guest di file eseguibile o un contenitore eseguendo `yo azuresfguest` o `yo azuresfcontainer` rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="9db05-145">After you have installed hello above generators, you should be able toocreate apps with guest executable or container services by running `yo azuresfguest` or `yo azuresfcontainer` respectively.</span></span>

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a><span data-ttu-id="9db05-146">Installare hello Java gli elementi necessari (facoltativi, se si desidera toouse hello Java di modelli di programmazione)</span><span class="sxs-lookup"><span data-stu-id="9db05-146">Install hello necessary Java artifacts (optional, if you want toouse hello Java programming models)</span></span>

<span data-ttu-id="9db05-147">servizi di Service Fabric toobuild Usa Java, verificare di aver 1.8 JDK installata insieme a Gradle viene utilizzato per l'esecuzione di attività di compilazione.</span><span class="sxs-lookup"><span data-stu-id="9db05-147">toobuild Service Fabric services using Java, ensure you have JDK 1.8 installed along with Gradle which is used for running build tasks.</span></span> <span data-ttu-id="9db05-148">seguente frammento di codice Hello installa Open JDK 1.8, insieme a Gradle.</span><span class="sxs-lookup"><span data-stu-id="9db05-148">hello following snippet installs Open JDK 1.8 along with Gradle.</span></span> <span data-ttu-id="9db05-149">librerie di Hello Service Fabric Java vengono estratti da Maven.</span><span class="sxs-lookup"><span data-stu-id="9db05-149">hello Service Fabric Java libraries are pulled from Maven.</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a><span data-ttu-id="9db05-150">Installare hello Neon Eclipse plug-in (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="9db05-150">Install hello Eclipse Neon plug-in (optional)</span></span>

<span data-ttu-id="9db05-151">È possibile installare hello plug-in Eclipse per l'infrastruttura di servizio all'interno di hello **Eclipse IDE per gli sviluppatori Java**.</span><span class="sxs-lookup"><span data-stu-id="9db05-151">You can install hello Eclipse plug-in for Service Fabric from within hello **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="9db05-152">È possibile utilizzare applicazioni eseguibile guest Eclipse toocreate Service Fabric e applicazioni contenitore nelle applicazioni Java infrastruttura tooService di addizione.</span><span class="sxs-lookup"><span data-stu-id="9db05-152">You can use Eclipse toocreate Service Fabric guest executable applications and container applications in addition tooService Fabric Java applications.</span></span>

1. <span data-ttu-id="9db05-153">In Eclipse, assicurarsi di disporre di più recente Neon Eclipse e hello versione più recente di Buildship (1.0.17 o versione successiva) installato.</span><span class="sxs-lookup"><span data-stu-id="9db05-153">In Eclipse, ensure that you have latest Eclipse Neon and hello latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="9db05-154">È possibile controllare le versioni di hello dei componenti installati selezionando **Guida** > **i dettagli di installazione**.</span><span class="sxs-lookup"><span data-stu-id="9db05-154">You can check hello versions of installed components by selecting **Help** > **Installation Details**.</span></span> <span data-ttu-id="9db05-155">È possibile aggiornare Buildship utilizzando istruzioni hello in [Buildship Eclipse: Plug-in Eclipse per Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="9db05-155">You can update Buildship by using hello instructions at [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>

2. <span data-ttu-id="9db05-156">tooinstall hello selezionare plug-in Service Fabric **Guida** > **installa nuovo Software**.</span><span class="sxs-lookup"><span data-stu-id="9db05-156">tooinstall hello Service Fabric plug-in, select **Help** > **Install New Software**.</span></span>

3. <span data-ttu-id="9db05-157">In hello **utilizzano** digitare **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="9db05-157">In hello **Work with** box, type **http://dl.microsoft.com/eclipse**.</span></span>

4. <span data-ttu-id="9db05-158">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9db05-158">Click **Add**.</span></span>

    ![pagina Software disponibili Hello][sf-eclipse-plugin]

5. <span data-ttu-id="9db05-160">Seleziona hello **ServiceFabric** plug-in, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9db05-160">Select hello **ServiceFabric** plug-in, and then click **Next**.</span></span>

6. <span data-ttu-id="9db05-161">Completare i passaggi di installazione hello e quindi accettare i termini del contratto hello.</span><span class="sxs-lookup"><span data-stu-id="9db05-161">Complete hello installation steps, and then accept hello end-user license agreement.</span></span>

<span data-ttu-id="9db05-162">Se si dispone già di hello servizio infrastruttura Eclipse plug-in installato, accertarsi di avere la versione più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="9db05-162">If you already have hello Service Fabric Eclipse plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="9db05-163">È possibile controllare selezionando **Guida** > **i dettagli di installazione** e quindi la ricerca per l'infrastruttura del servizio nell'elenco di hello di installato plug-in. Se è disponibile una versione più recente, selezionare **Update** (Aggiorna).</span><span class="sxs-lookup"><span data-stu-id="9db05-163">You can check by selecting **Help** > **Installation Details** and then searching for Service Fabric in hello list of installed plug-ins. If a newer version is available, select **Update**.</span></span>

<span data-ttu-id="9db05-164">Per altre informazioni, vedere [Plug-in Service Fabric per lo sviluppo di applicazioni Java in Eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="9db05-164">For more information, see [Service Fabric plug-in for Eclipse Java application development](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a><span data-ttu-id="9db05-165">Installare hello .NET Core SDK (facoltativo, se si desidera che i modelli di programmazione .NET Core hello toouse)</span><span class="sxs-lookup"><span data-stu-id="9db05-165">Install hello .NET Core SDK (optional, if you want toouse hello .NET Core programming models)</span></span>
<span data-ttu-id="9db05-166">Hello .NET Core SDK fornisce modelli di servizi di Service Fabric toobuild obbligatorio con .NET Core e librerie di hello.</span><span class="sxs-lookup"><span data-stu-id="9db05-166">hello .NET Core SDK provides hello libraries and templates that are required toobuild Service Fabric services with .NET Core.</span></span> <span data-ttu-id="9db05-167">Installare il pacchetto di .NET Core SDK hello seguenti hello in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="9db05-167">Install hello .NET Core SDK package by running hello following -</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a><span data-ttu-id="9db05-168">Aggiornamento hello SDK e runtime</span><span class="sxs-lookup"><span data-stu-id="9db05-168">Update hello SDK and runtime</span></span>

<span data-ttu-id="9db05-169">tooupdate toohello ultima versione di hello SDK e di runtime, esegue i comandi seguenti hello (deselezionate SDK hello che non si desidera):</span><span class="sxs-lookup"><span data-stu-id="9db05-169">tooupdate toohello latest version of hello SDK and runtime, run hello following commands (deselect hello SDKs that you don't want):</span></span>

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
<span data-ttu-id="9db05-170">file binari SDK per Java di hello tooupdate Maven, è necessario dettagli della versione del file binario corrispondente hello in hello tooupdate hello ``build.gradle`` versione più recente del file toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="9db05-170">tooupdate hello Java SDK binaries from Maven, you need tooupdate hello version details of hello corresponding binary in hello ``build.gradle`` file toopoint toohello latest version.</span></span> <span data-ttu-id="9db05-171">tooknow esattamente in cui è necessario versione hello tooupdate, è possibile fare riferimento tooany ``build.gradle`` file negli esempi di Guida introduttiva di Service Fabric [qui](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9db05-171">tooknow exactly where you need tooupdate hello version, you can refer tooany ``build.gradle`` file in Service Fabric getting-started samples [here](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="9db05-172">L'aggiornamento di pacchetti hello potrebbe causare il toostop di cluster di sviluppo locale in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9db05-172">Updating hello packages might cause your local development cluster toostop running.</span></span> <span data-ttu-id="9db05-173">Riavviare il cluster locale dopo un aggiornamento seguendo le istruzioni di hello in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="9db05-173">Restart your local cluster after an upgrade by following hello instructions on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9db05-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9db05-174">Next steps</span></span>

* [<span data-ttu-id="9db05-175">Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando Yeoman</span><span class="sxs-lookup"><span data-stu-id="9db05-175">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="9db05-176">Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando il plug-in Service Fabric per Eclipse</span><span class="sxs-lookup"><span data-stu-id="9db05-176">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="9db05-177">Creare la prima applicazione CSharp in Linux</span><span class="sxs-lookup"><span data-stu-id="9db05-177">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="9db05-178">Preparare l'ambiente di sviluppo in OSX</span><span class="sxs-lookup"><span data-stu-id="9db05-178">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="9db05-179">Utilizzare le applicazioni di hello servizio infrastruttura CLI toomanage</span><span class="sxs-lookup"><span data-stu-id="9db05-179">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="9db05-180">Differenze in Service Fabric tra Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="9db05-180">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
* [<span data-ttu-id="9db05-181">Introduzione all'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9db05-181">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
