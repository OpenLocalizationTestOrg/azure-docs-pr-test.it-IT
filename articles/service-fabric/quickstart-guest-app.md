---
title: aaaQuickly distribuire un cluster di Azure Service Fabric tooan app esistente
description: Usare un toohost di cluster di Azure Service Fabric un'applicazione Node.js esistente con Visual Studio.
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a>Ospitare un'applicazione Node.js in Azure Service Fabric

Questa Guida rapida consente di distribuire un cluster di Service Fabric tooa applicazione (Node.js in questo esempio) esistente in esecuzione in Azure.

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare, assicurarsi di avere [configurato l'ambiente di sviluppo](service-fabric-get-started.md). Che include l'installazione di Service Fabric SDK hello e Visual Studio 2017 o 2015.

È inoltre necessario toohave un'applicazione Node.js esistente per la distribuzione. In questa guida introduttiva viene usato un semplice sito Web Node.js che può essere scaricato [qui][download-sample]. Estrarre il file tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` cartella dopo aver creato il progetto di hello nel passaggio successivo hello.

Se non si ha una sottoscrizione di Azure, creare un [account gratuito][create-account].

## <a name="create-hello-service"></a>Creare il servizio hello

Avviare Visual Studio come **amministratore**.

Creare un progetto con `CTRL`+`SHIFT`+`N`.

In hello **nuovo progetto** finestra di dialogo, scegliere **Cloud > applicazione di Service Fabric**.

Nome di un'applicazione hello **MyGuestApp** e premere **OK**.

>[!IMPORTANT]
>Node.js corre il limite di caratteri per i percorsi di windows con 260 hello. Usare un percorso breve per il progetto hello stesso, ad esempio **c:\code\svc1**.
   
![Finestra di dialogo Nuovo progetto in Visual Studio][new-project]

È possibile creare qualsiasi tipo di servizio di Service Fabric dalla finestra di dialogo successiva hello. Per questa guida introduttiva scegliere **Eseguibile guest**.

Nome servizio hello **MyGuestService** e impostare le opzioni di hello in toohello destra hello seguenti valori:

| Impostazione                   | Valore |
| ------------------------- | ------ |
| Cartella del pacchetto di codice       | _&lt;cartella Hello con l'app Node.js&gt;_ |
| Comportamento del pacchetto di codice     | Copiare tooproject contenuto cartella |
| Programma                   | node.exe |
| Argomenti                 | server.js |
| Cartella di lavoro            | CodePackage |

Premere **OK**.

![Finestra di dialogo Nuovo servizio in Visual Studio][new-service]

Visual Studio crea il progetto di applicazione hello e il progetto di servizio actor hello e li visualizza in Esplora soluzioni.

progetto di applicazione Hello (**MyGuestApp**) non contiene il codice direttamente. Fa invece riferimento a un set di progetti di servizio. Include inoltre altri tre tipi di contenuto:

* **Profili di pubblicazione**  
Preferenze relative agli strumenti per diversi ambienti.

* **Script**  
Script di PowerShell per distribuire o aggiornare l'applicazione.

* **Definizione di applicazione**  
Manifesto dell'applicazione hello in include *ApplicationPackageRoot*. I file dei parametri dell'applicazione associati sono in *ApplicationParameters*, che definiscono l'applicazione hello e consentono di tooconfigure in modo specifico per un determinato ambiente.
    
Per una panoramica del contenuto di hello hello del progetto di servizio, vedere [Introduzione a servizi affidabili](service-fabric-reliable-services-quick-start.md).

## <a name="set-up-networking"></a>Configurare la rete

esempio Hello app Node.js si sta distribuendo utilizza la porta **80** e dobbiamo tootell Service Fabric che è necessario che la porta esposti.

Aprire hello **ServiceManifest.xml** file nel progetto hello. Nella parte inferiore di hello del manifesto di hello, sussiste un `<Resources> \ <Endpoints>` con una voce già definita. Modificare tooadd tale voce `Port`, `Protocol`, e `Type`. 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a>Distribuire tooAzure

Se si preme **F5** ed eseguire il progetto di hello, è cluster locale toohello distribuito. Tuttavia, consente di distribuire tooAzure invece.

Fare clic sul progetto hello e scegliere **pubblica...**  che viene aperto un tooAzure toopublish finestra di dialogo.

![Finestra di dialogo tooazure per un servizio di service fabric pubblicazione][publish]

Seleziona hello **PublishProfiles\Cloud.xml** profilo di destinazione.

Se non è stato in precedenza, scegliere un account di Azure di toodeploy per. Se non si ha ancora un account, è possibile [iscriversi per ottenerne uno][create-account].

In **Endpoint della connessione**, selezionare hello toodeploy cluster Service Fabric per. Se non si dispone di uno, selezionare  **&lt;creare un nuovo Cluster... &gt;**  che apre toohello di finestra del browser web portale di Azure. Per ulteriori informazioni, vedere [creare un cluster nel portale di hello](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal). 

Quando si crea il cluster di Service Fabric hello, assicurarsi che hello tooset **endpoint personalizzato** impostazione troppo**80**.

![Configurazione del tipo di nodo di Service Fabric con endpoint personalizzato][custom-endpoint]

Creare un nuovo cluster di Service Fabric accetta alcuni toocomplete ora. Dopo che è stato creato, andare toohello back-finestra di dialogo pubblicazione e selezionare  **&lt;aggiornamento&gt;**. il nuovo cluster di Hello è elencato nella casella di riepilogo a discesa hello. selezionarla.

Premere **pubblica** e attendere hello toofinish di distribuzione.

L'operazione potrebbe richiedere alcuni minuti. Una volta completato, potrebbe richiedere alcuni minuti per toobe applicazione hello completamente disponibile.

## <a name="test-hello-website"></a>Sito Web hello di test

Dopo che è stato pubblicato, testare il servizio in un Web browser. 

Innanzitutto, aprire hello portale di Azure e trovare il servizio Service Fabric.

Controllare il pannello Panoramica hello hello nell'indirizzo di assistenza. Utilizza il nome di dominio da hello hello _endpoint della connessione Client_ proprietà. ad esempio `http://mysvcfab1.westus2.cloudapp.azure.com`.

![Pannello della panoramica dell'infrastruttura del servizio nel portale di Azure hello][overview]

Passare l'indirizzo toothis in cui verrà visualizzato hello `HELLO WORLD` risposta.

## <a name="delete-hello-cluster"></a>Eliminare il cluster hello

Non dimenticare toodelete tutte le risorse di hello che hai creato per questa Guida rapida, come vengono addebitate per tali risorse.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni sugli [eseguibili guest](service-fabric-deploy-existing-app.md).

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F