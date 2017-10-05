---
title: Configurare l'ambiente di sviluppo in Mac OS X per l'interazione con Azure Service Fabric| Microsoft Docs
description: "Installare il runtime, l'SDK e gli strumenti e creare un cluster di sviluppo locale. Al termine della configurazione, sarà possibile iniziare a creare applicazioni in Mac OS X."
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
ms.openlocfilehash: 8b4fc0ab9034263418cac42ced203035e0a8fcad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a>Configurare l'ambiente di sviluppo in Mac OS X
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

È possibile creare applicazioni di Service Fabric da eseguire in cluster Linux usando Mac OS X. Questo articolo illustra come configurare il computer Mac per lo sviluppo.

## <a name="prerequisites"></a>Prerequisiti
Service Fabric non viene eseguito in modo nativo in OS X. Per eseguire un cluster di Service Fabric locale, viene creata una macchina virtuale Ubuntu preconfigurata con Vagrant e VirtualBox. Prima di iniziare, sono necessari:

* [Vagrant (versione 1.8.4 o successiva)](http://www.vagrantup.com/downloads.html)
* [VirtualBox](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> È necessario usare versioni con supporto reciproco di Vagrant e VirtualBox. Vagrant potrebbe non funzionare correttamente in una versione di VirtualBox non supportata.
>

## <a name="create-the-local-vm"></a>Creare la VM locale
Per creare la VM locale contenente un cluster di Service Fabric a 5 nodi, seguire questa procedura:

1. Clonare il repository `Vagrantfile`

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    Questo passaggio scarica il file `Vagrantfile` contenente la configurazione della VM con il percorso da cui viene scaricata la VM.

2. Passare al clone locale del repository

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. (Facoltativo) Modificare le impostazioni predefinite della VM

    Per impostazione predefinita, la VM locale è configurata come segue:

   * 3 GB di memoria allocati
   * Rete host privata configurata all'indirizzo IP 192.168.50.50 che consente il pass-through del traffico dall'host Mac

     È possibile modificare una di queste impostazioni o aggiungere altre opzioni di configurazione della VM in `Vagrantfile`. Per l'elenco completo delle opzioni di configurazione, vedere la [documentazione di Vagrant](http://www.vagrantup.com/docs) .
4. Creare la VM

    ```bash
    vagrant up
    ```

   In questo passaggio viene scaricata e avviata in locale l'immagine di VM preconfigurata e vi viene quindi configurato un cluster di Service Fabric locale. È probabile che questo passaggio richieda alcuni minuti. Se la configurazione ha esito positivo, nell'output verrà visualizzato un messaggio che indica che è in corso l'avvio del cluster.

    ![Avvio della configurazione del cluster dopo il provisioning della VM][cluster-setup-script]

    >[!TIP]
    > Se il download della VM impiega troppo tempo, è possibile scaricarla con wget o curl oppure un browser passando al collegamento specificato da **config.vm.box_url** nel file `Vagrantfile`. Dopo averla scaricata in locale, modificare `Vagrantfile` in modo che punti al percorso locale in cui si è scaricata l'immagine. Se, ad esempio, si è scaricata l'immagine in /home/users/test/azureservicefabric.tp8.box, impostare **config.vm.box_url** su tale percorso.
    >

5. Verificare che il cluster sia stato configurato correttamente passando a Service Fabric Explorer all'indirizzo http://192.168.50.50:19080/Explorer, presupponendo che sia stato mantenuto l'IP predefinito della rete privata.

    ![Visualizzazione di Service Fabric Explorer dal Mac host][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a>Creare un'applicazione in Mac tramite Yeoman
Service Fabric offre gli strumenti di scaffolding che consentono di creare un'applicazione Service Fabric dal terminale tramite il generatore di modelli Yeoman. Seguire questa procedura per assicurarsi che nella macchina virtuale sia disponibile il generatore di modelli Yeoman di Service Fabric.

1. È necessario che Node.js e NPM siano installati nel computer Mac. In caso contrario, è possibile installare Node.js e NPM tramite Homebrew usando il comando seguente. Per verificare le versioni di Node.js e NPM installate nel computer Mac, è possibile usare l'opzione ``-v``.

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. Installare il generatore di modelli [Yeoman](http://yeoman.io/) nella macchina virtuale da NPM

  ```bash
  npm install -g yo
  ```
3. Installare il generatore Yeoman da usare, seguendo la procedura disponibile nella [documentazione](service-fabric-get-started-linux.md) introduttiva. Per creare applicazioni Service Fabric tramite Yeoman, seguire questa procedura:

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. Per compilare un'applicazione Java per Service Fabric nel computer Mac, è necessario che JDK 1.8 e Gradle siano installati nella macchina virtuale.


## <a name="install-the-service-fabric-plugin-for-eclipse-neon"></a>Installare il plug-in Service Fabric per Eclipse Neon

Service Fabric offre un plug-in per **Eclipse Neon per l'ambiente IDE Java** che può semplificare il processo di creazione, compilazione e distribuzione di servizi Java. È possibile seguire la procedura di installazione illustrata in questa [documentazione](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) generale sull'installazione e l'aggiornamento del plug-in Service Fabric Eclipse.

>[!TIP]
> Per impostazione predefinita, viene supportato l'indirizzo IP predefinito, come indicato in ``Vagrantfile`` nel file``Local.json`` dell'applicazione generata. Se si modifica tale impostazione e si distribuisce Vagrant con un indirizzo IP diverso, aggiornare anche l'indirizzo IP corrispondente nel file ``Local.json`` dell'applicazione.

## <a name="next-steps"></a>Passaggi successivi
<!-- Links -->
* [Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md) (Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando il plug-in Service Fabric per Eclipse)
* [Creare un cluster di Service Fabric nel portale di Azure](service-fabric-cluster-creation-via-portal.md)
* [Creare un cluster di Service Fabric con Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
* [Informazioni sul modello applicativo di Service Fabric](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
