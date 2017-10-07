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
# <a name="create-your-first-azure-service-fabric-application"></a>Creare la prima applicazione di Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Service Fabric mette a disposizione SDK per la compilazione di servizi su Linux in .NET Core e Java. In questa esercitazione viene illustrato come toocreate un'applicazione per Linux e creazione di un servizio utilizzando il linguaggio c# (Core .NET).

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare, assicurarsi di avere [configurato l'ambiente di sviluppo di Linux](service-fabric-get-started-linux.md). Se si usa Mac OS X è possibile [configurare un ambiente con un solo computer Linux in una macchina virtuale usando Vagrant](service-fabric-get-started-mac.md).

È anche possibile hello tooinstall [servizio infrastruttura CLI](service-fabric-cli.md)

### <a name="install-and-set-up-hello-generators-for-csharp"></a>Installare e configurare i generatori di hello per CSharp
Service Fabric offre gli strumenti di scaffolding che consentono di creare un'applicazione CSharp per Service Fabric dal terminale tramite il generatore di modelli Yeoman. Eseguire procedure hello sotto tooensure che si dispone di hello Service Fabric modello yeoman generatore per CSharp utilizzo nel computer.
1. Installare nodejs e NPM nella macchina virtuale

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Installare il generatore di modelli [Yeoman](http://yeoman.io/) nella macchina virtuale da NPM

  ```bash
  sudo npm install -g yo
  ```
3. Installare generatore di applicazione di servizio Fabric Yeo Java hello da NPM

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a>Creare un'applicazione hello
Un'applicazione di Service Fabric può contenere uno o più servizi, ognuno con un ruolo specifico nell'offerta di funzionalità dell'applicazione hello. Hello Service Fabric [Yeoman](http://yeoman.io/) toocreate facile rende generatore per CSharp, cui è installato nell'ultimo passaggio, il primo servizio e tooadd più avanti. Consente di usare Yeoman toocreate un'applicazione con un singolo servizio.

1. In un terminale, digitare hello compilazione lo scaffolding hello toostart di comando seguente:`yo azuresfcsharp`
2. Assegnare un nome all'applicazione.
3. Scegliere il tipo di hello del primo servizio e il nome. Ai fini di hello di questa esercitazione, si sceglie un servizio Actor affidabile.

   ![Generatore Yeoman di Service Fabric per C#][sf-yeoman]

> [!NOTE]
> Per ulteriori informazioni sulle opzioni di hello, vedere [Cenni preliminari sul modello di programmazione di Service Fabric](service-fabric-choose-framework.md).
>
>

## <a name="build-hello-application"></a>Compilare un'applicazione hello
modelli di servizio dell'infrastruttura Yeoman Hello includono uno script di compilazione che è possibile utilizzare l'applicazione hello toobuild da hello terminal (dopo una navigazione toohello cartella dell'applicazione).

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-hello-application"></a>Distribuire un'applicazione hello

Una volta creata l'applicazione hello, è possibile distribuire cluster locale toohello.

1. Connettere il cluster di Service Fabric locale toohello.

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. Eseguire script di installazione di hello fornito in hello modello toocopy applicazione hello pacchetto archivio immagini toohello del cluster, registrare il tipo di applicazione hello e creare un'istanza di un'applicazione hello.

    ```bash
    ./install.sh
    ```

Distribuire un'applicazione hello compilato è hello stesso come qualsiasi altra applicazione di Service Fabric. Vedere la documentazione di hello su [la gestione di un'applicazione di Service Fabric con hello servizio infrastruttura CLI](service-fabric-application-lifecycle-sfctl.md) per istruzioni dettagliate.

I parametri toothese comandi sono disponibili nei manifesti hello generato all'interno del pacchetto di applicazione hello.

Dopo la distribuzione di un'applicazione hello, aprire un browser e passare a [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) in [http://localhost:19080/Esplora](http://localhost:19080/Explorer). Espandere quindi hello **applicazioni** nodo e notare che è ora disponibile una voce per il tipo di applicazione e un altro per hello prima istanza di quel tipo.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Avviare il client di prova hello ed eseguire un failover
I progetti Actor non eseguono alcuna operazione in modo indipendente. Un altro servizio o client di toosend richiedono tali messaggi. modello attore Hello include uno script di test semplice che è possibile utilizzare toointeract con servizio actor hello.

1. Eseguire script hello utilizzando hello espressioni di controllo utilità toosee hello output del servizio actor hello.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. In Service Fabric Explorer, individuare il nodo che ospita la replica primaria di hello per servizio actor hello. Nella schermata di hello riportata di seguito, è il nodo 3.

    ![Trovare la replica primaria hello in Service Fabric Explorer][sfx-primary]
3. Fare clic sul nodo hello è stata individuata nel passaggio precedente hello, scegliere **Deactivate (riavvio)** dal menu Azioni hello. Questa azione riavvia un nodo del cluster locale, forzando una replica secondaria tooa failover in esecuzione in un altro nodo. Come eseguire questa azione, si paga output toohello attenzione dal client di prova hello e annotare che tale contatore hello continua tooincrement nonostante hello failover.

## <a name="adding-more-services-tooan-existing-application"></a>Aggiunta di ulteriori servizi tooan esistente dell'applicazione

tooadd già un'altra applicazione tooan di servizio creato utilizzando `yo`, eseguire hello alla procedura seguente:
1. Cambiare directory toohello principale di un'applicazione hello esistente.  Ad esempio, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` è un'applicazione hello creata da Yeoman.
2. Eseguire `yo azuresfcsharp:AddService`

## <a name="migrating-from-projectjson-toocsproj"></a>La migrazione da Project too.csproj
1. In esecuzione 'dotnet eseguire la migrazione' nella directory radice del progetto verrà eseguita la migrazione toocsproj formato JSON di tutti i hello.
2. Aggiornamento hello progetto fa riferimento a conseguenza toocsproj file nei file di progetto.
3. Aggiornare i file hello progetto file nomi toocsproj in build.sh.

## <a name="next-steps"></a>Passaggi successivi

* [Altre informazioni su Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [L'interazione con i cluster di Service Fabric usando hello servizio infrastruttura CLI](service-fabric-cli.md)
* Informazioni sulle [opzioni di supporto di Service Fabric](service-fabric-support.md)
* [Introduzione all'interfaccia della riga di comando di Service Fabric](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
