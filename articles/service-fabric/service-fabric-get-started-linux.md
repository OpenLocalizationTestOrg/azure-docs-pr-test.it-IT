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
# <a name="prepare-your-development-environment-on-linux"></a>Preparare l'ambiente di sviluppo in Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

toodeploy ed eseguire [applicazioni Azure Service Fabric](service-fabric-application-model.md) nel computer di sviluppo di Linux, installare il runtime hello e SDK comuni. È anche possibile installare SDK facoltativi per Java e .NET Core.

## <a name="prerequisites"></a>Prerequisiti

Hello seguenti versioni del sistema operativo è supportato per lo sviluppo:

* Ubuntu 16.04 (`Xenial Xerus`)

## <a name="update-your-apt-sources"></a>Aggiornare le origini APT
tooinstall hello SDK e hello runtime associato pacchetto tramite lo strumento da riga di comando di hello apt get, è innanzitutto necessario aggiornare le origini di strumento di creazione di pacchetti avanzate (APT).

1. Aprire un terminale.
2. Aggiungere l'elenco delle origini tooyour repository hello Service Fabric.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. Aggiungere hello `dotnet` elenco delle origini tooyour repository.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. Aggiungere hello keyring APT tooyour nuovo Guard di Privacy Gnu (GnuPG o GPG) della chiave.

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. Aggiungere hello ufficiale Docker GPG tooyour chiave APT keyring.

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. Impostare il repository di Docker hello.

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. Il pacchetto di aggiornamento elenchi basati su hello appena aggiunto repository.

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a>Installare e configurare hello SDK per l'installazione del cluster locale

Dopo aver aggiornato le origini, è possibile installare hello SDK. Installare il pacchetto di Service Fabric SDK hello, confermare l'installazione di hello e accettare il contratto di licenza toohello.

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   Hello seguenti comandi automatizzare accettazione licenza hello per i pacchetti di Service Fabric:
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a>Configurare un cluster locale
  Se l'installazione hello ha esito positivo, dovrebbe essere in grado di toostart un cluster locale.

  1. Eseguire lo script di installazione di cluster hello.

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. Aprire un web browser e andare troppo[Service Fabric Explorer](http://localhost:19080/Explorer). Se il cluster hello è avviato, vedrai il dashboard di Service Fabric Explorer hello.

      ![Service Fabric Explorer in Linux][sfx-linux]

  A questo punto, è possibile distribuire pacchetti di applicazione di Service Fabric predefiniti o nuovi pacchetti basati su contenitori o eseguibili guest. toobuild nuovi servizi tramite Java hello o .NET Core SDK, seguire i passaggi di configurazione facoltativi hello fornite nelle sezioni successive.


  > [!NOTE]
  > I cluster autonomi non sono supportati in Linux. Hello anteprima supporta solo a una casella e i cluster con più computer Linux di Azure.
  >

## <a name="set-up-hello-service-fabric-cli"></a>Impostare i servizi dell'infrastruttura CLI hello

Hello [servizio infrastruttura CLI](service-fabric-cli.md) sono disponibili comandi per l'interazione con le entità di Service Fabric, incluse le applicazioni e i cluster. È basato su python, è necessario che toohave python e pip installato prima di procedere con hello comando seguente:

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a>Installare e configurare i generatori di hello per contenitori e i file eseguibili di guest
Service Fabric offre gli strumenti di scaffolding che consentono di creare applicazioni Service Fabric dal terminale tramite il generatore di modelli Yeoman. Eseguire procedure hello sotto tooensure che si dispone di hello Service Fabric modello yeoman generatore per l'utilizzo nel computer.

1. Installare nodejs e NPM nella macchina virtuale

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Installare il generatore di modelli [Yeoman](http://yeoman.io/) nella macchina virtuale da NPM

  ```bash
  sudo npm install -g yo
  ```
3. Installare generatore di hello Yeo dell'infrastruttura del servizio contenitore e il generatore di execuatble guest da NPM

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

Dopo aver installato hello sopra i generatori, dovrebbe essere in grado di toocreate App con i servizi guest di file eseguibile o un contenitore eseguendo `yo azuresfguest` o `yo azuresfcontainer` rispettivamente.

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a>Installare hello Java gli elementi necessari (facoltativi, se si desidera toouse hello Java di modelli di programmazione)

servizi di Service Fabric toobuild Usa Java, verificare di aver 1.8 JDK installata insieme a Gradle viene utilizzato per l'esecuzione di attività di compilazione. seguente frammento di codice Hello installa Open JDK 1.8, insieme a Gradle. librerie di Hello Service Fabric Java vengono estratti da Maven.

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a>Installare hello Neon Eclipse plug-in (facoltativo)

È possibile installare hello plug-in Eclipse per l'infrastruttura di servizio all'interno di hello **Eclipse IDE per gli sviluppatori Java**. È possibile utilizzare applicazioni eseguibile guest Eclipse toocreate Service Fabric e applicazioni contenitore nelle applicazioni Java infrastruttura tooService di addizione.

1. In Eclipse, assicurarsi di disporre di più recente Neon Eclipse e hello versione più recente di Buildship (1.0.17 o versione successiva) installato. È possibile controllare le versioni di hello dei componenti installati selezionando **Guida** > **i dettagli di installazione**. È possibile aggiornare Buildship utilizzando istruzioni hello in [Buildship Eclipse: Plug-in Eclipse per Gradle][buildship-update].

2. tooinstall hello selezionare plug-in Service Fabric **Guida** > **installa nuovo Software**.

3. In hello **utilizzano** digitare **http://dl.microsoft.com/eclipse**.

4. Fare clic su **Aggiungi**.

    ![pagina Software disponibili Hello][sf-eclipse-plugin]

5. Seleziona hello **ServiceFabric** plug-in, quindi fare clic su **Avanti**.

6. Completare i passaggi di installazione hello e quindi accettare i termini del contratto hello.

Se si dispone già di hello servizio infrastruttura Eclipse plug-in installato, accertarsi di avere la versione più recente di hello. È possibile controllare selezionando **Guida** > **i dettagli di installazione** e quindi la ricerca per l'infrastruttura del servizio nell'elenco di hello di installato plug-in. Se è disponibile una versione più recente, selezionare **Update** (Aggiorna).

Per altre informazioni, vedere [Plug-in Service Fabric per lo sviluppo di applicazioni Java in Eclipse](service-fabric-get-started-eclipse.md).


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a>Installare hello .NET Core SDK (facoltativo, se si desidera che i modelli di programmazione .NET Core hello toouse)
Hello .NET Core SDK fornisce modelli di servizi di Service Fabric toobuild obbligatorio con .NET Core e librerie di hello. Installare il pacchetto di .NET Core SDK hello seguenti hello in esecuzione:

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a>Aggiornamento hello SDK e runtime

tooupdate toohello ultima versione di hello SDK e di runtime, esegue i comandi seguenti hello (deselezionate SDK hello che non si desidera):

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
file binari SDK per Java di hello tooupdate Maven, è necessario dettagli della versione del file binario corrispondente hello in hello tooupdate hello ``build.gradle`` versione più recente del file toopoint toohello. tooknow esattamente in cui è necessario versione hello tooupdate, è possibile fare riferimento tooany ``build.gradle`` file negli esempi di Guida introduttiva di Service Fabric [qui](https://github.com/Azure-Samples/service-fabric-java-getting-started).

> [!NOTE]
> L'aggiornamento di pacchetti hello potrebbe causare il toostop di cluster di sviluppo locale in esecuzione. Riavviare il cluster locale dopo un aggiornamento seguendo le istruzioni di hello in questa pagina.

## <a name="next-steps"></a>Passaggi successivi

* [Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando il plug-in Service Fabric per Eclipse](service-fabric-get-started-eclipse.md)
* [Creare la prima applicazione CSharp in Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
* [Preparare l'ambiente di sviluppo in OSX](service-fabric-get-started-mac.md)
* [Utilizzare le applicazioni di hello servizio infrastruttura CLI toomanage](service-fabric-application-lifecycle-sfctl.md)
* [Differenze in Service Fabric tra Windows e Linux](service-fabric-linux-windows-differences.md)
* [Introduzione all'interfaccia della riga di comando di Service Fabric](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
