---
title: aaaSet dell'ambiente di sviluppo in Mac OS X toowork con Azure Service Fabric | Documenti Microsoft
description: "Installare il runtime di hello, SDK e strumenti e creare un cluster di sviluppo locale. Dopo aver completato il programma di installazione, sarà pronto toobuild applicazioni su Mac OS X."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2017
ms.author: saysa
ms.openlocfilehash: 0b8a6c1fc1871fa76f3e21cefbc7f66f79072797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a>Configurare l'ambiente di sviluppo in Mac OS X
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

È possibile compilare toorun applicazioni di Service Fabric su cluster Linux utilizzando Mac OS X. Questo articolo descrive come tooset backup Mac per lo sviluppo.

## <a name="prerequisites"></a>Prerequisiti
Infrastruttura del servizio non viene eseguita in modo nativo su OS X. toorun un cluster di Service Fabric locale, offre una macchina virtuale di Ubuntu preconfigurata con Vagrant e VirtualBox. Prima di iniziare, sono necessari:

* [Vagrant (versione 1.8.4 o successiva)](http://www.vagrantup.com/downloads.html)
* [VirtualBox](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> È necessario toouse reciprocamente supportate versioni Vagrant e VirtualBox. Vagrant potrebbe non funzionare correttamente in una versione di VirtualBox non supportata.
>

## <a name="create-hello-local-vm"></a>Creare hello macchina virtuale locale
toocreate hello macchina virtuale locale che contiene un cluster di Service Fabric 5 nodi, eseguire hello alla procedura seguente:

1. Hello clone `Vagrantfile` repository

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    Questa procedura porta elenchi hello file `Vagrantfile` contenente hello VM configurazione insieme hello percorso hello VM viene scaricato dal.

2. Passare toohello clone locale del repository hello

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. (Facoltativo) Modificare le impostazioni di macchina virtuale di hello predefinite

    Per impostazione predefinita, hello macchina virtuale locale è configurato come segue:

   * 3 GB di memoria allocati
   * Rete privata host configurate all'indirizzo IP 192.168.50.50 abilitazione pass-through di traffico da hello Mac host

     È possibile modificare queste impostazioni o aggiungere altri toohello configurazione macchina virtuale in hello `Vagrantfile`. Vedere hello [documentazione Vagrant](http://www.vagrantup.com/docs) per l'elenco completo di hello delle opzioni di configurazione.
4. Creare VM hello

    ```bash
    vagrant up
    ```

   Questo passaggio Scarica l'immagine di macchina virtuale hello preconfigurato, in locale e quindi impostare un'infrastruttura locale di servizio del cluster all'avvio. Si dovrebbero e tootake qualche minuto. Se il programma di installazione viene completata correttamente, viene visualizzato un messaggio nell'output di hello che indica il che avvio di tale cluster hello.

    ![Avvio della configurazione del cluster dopo il provisioning della VM][cluster-setup-script]

    >[!TIP]
    > Se il download VM hello richiede molto tempo, è possibile scaricare con wget o curl o tramite un browser passando toohello collegamento specificato dal **config.vm.box_url** nel file hello `Vagrantfile`. Dopo aver scaricato localmente, modificare `Vagrantfile` toopoint toohello percorso locale in cui è stato scaricato immagine hello. Ad esempio se è stato scaricato hello immagine too/home/users/test/azureservicefabric.tp8.box, quindi impostata **config.vm.box_url** toothat percorso.
    >

5. Verificare che hello cluster è stato configurato correttamente passando tooService Fabric Explorer in http://192.168.50.50:19080/Esplora (presupponendo che si tiene hello predefinito IP di rete privata).

    ![Visualizzato dall'host hello Mac Service Fabric Explorer][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a>Creare un'applicazione in Mac tramite Yeoman
Service Fabric offre gli strumenti di scaffolding che consentono di creare un'applicazione Service Fabric dal terminale tramite il generatore di modelli Yeoman. Eseguire procedure hello sotto tooensure che si dispone di hello Service Fabric modello yeoman generatore utilizzo nel computer.

1. È necessario toohave Node.js e NPM installato è mac. Se non è possibile installare Node.js e NPM utilizzando Homebrew con hello seguenti. versioni di hello toocheck di Node.js e NPM installata nel Mac, è possibile utilizzare hello ``-v`` opzione.

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. Installare il generatore di modelli [Yeoman](http://yeoman.io/) nella macchina virtuale da NPM

  ```bash
  npm install -g yo
  ```
3. Installare hello Yeoman generatore desiderato toouse, i passaggi hello hello Introduzione [documentazione](service-fabric-get-started-linux.md). Applicazioni di infrastruttura servizio toocreate utilizzando Yeoman, seguire i passaggi hello-

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. toobuild un'applicazione di servizio Fabric Java su Mac, è necessario - JDK 1.8 e installato nel computer di hello Gradle.


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a>Installazione di plug-in Service Fabric hello per Eclipse Neon

Service Fabric fornisce un plug-in per hello **Neon Eclipse IDE Java** che può semplificare il processo di hello di creazione, compilazione e distribuzione di servizi di linguaggio. È possibile seguire i passaggi di installazione hello indicati in questa generale [documentazione](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) sull'installazione o aggiornamento plug-in servizi dell'infrastruttura Eclipse.

>[!TIP]
> Per impostazione predefinita è supporta hello predefinito IP come indicato in hello ``Vagrantfile`` in hello ``Local.json`` dell'applicazione hello generato. Nel caso in cui si modifica e si distribuiscono Vagrant con un indirizzo IP diverso, aggiornare hello IP corrispondente in ``Local.json`` anche dell'applicazione.

## <a name="next-steps"></a>Passaggi successivi
<!-- Links -->
* [Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md) (Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando il plug-in Service Fabric per Eclipse)
* [Creare un cluster di Service Fabric in hello portale di Azure](service-fabric-cluster-creation-via-portal.md)
* [Creare un cluster di Service Fabric utilizzando hello Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
* [Comprendere il modello di applicazione del hello Service Fabric](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
