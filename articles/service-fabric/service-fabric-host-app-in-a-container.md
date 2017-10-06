---
title: un'applicazione .NET in tooAzure un contenitore Service Fabric aaaDeploy | Documenti Microsoft
description: Spiega in che modo un'applicazione .NET in Visual Studio in un contenitore Docker toopackage. Questa nuova app "container" viene quindi distribuita tooa cluster di Service Fabric.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a>Distribuire un'applicazione .NET in un tooAzure di contenitore di Windows Service Fabric

In questa esercitazione illustra come toodeploy un'applicazione ASP.NET esistente in un contenitore di Windows in Azure.

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare un progetto Docker in Visual Studio
> * Distribuire un'applicazione esistente in un contenitore
> * Configurare l'integrazione continua con Visual Studio e VSTS

## <a name="prerequisites"></a>Prerequisiti

1. Installare [Docker CE per Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) in modo da poter eseguire i contenitori in Windows 10.
2. Acquisire familiarità con hello [Guida introduttiva di contenitori di Windows 10][link-container-quickstart].
3. Scaricare hello [Fabrikam Fiber CallCenter] [ link-fabrikam-github] applicazione di esempio.
4. Installare [Azure PowerShell][link-azure-powershell-install]
5. Installare hello [estensione strumenti di distribuzione continua per Visual Studio 2017][link-visualstudio-cd-extension]
6. Creare una [sottoscrizione di Azure][link-azure-subscription] e un [account di Visual Studio Team Services][link-vsts-account]. 
7. [Creare un cluster in Azure](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a>Un'applicazione hello inserita in un contenitore

Dopo avere creato un [cluster di Service Fabric è in esecuzione in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) si toocreate pronto e distribuire un'applicazione nei contenitori. toostart in esecuzione l'applicazione in un contenitore, è necessario tooadd **Docker supporto** toohello progetto in Visual Studio. Quando si aggiungono **supporto Docker** toohello applicazione, si verifica quanto segue. Innanzitutto, un _Dockerfile_ è stato aggiunto il progetto toohello. Questo nuovo file viene descritto come immagine contenitore hello è toobe compilato. Quindi secondo, con un nuovo _comporre docker_ progetto viene aggiunto toohello soluzione. nuovo progetto Hello contiene alcuni docker-comporre i file. Comporre docker file possono essere utilizzati toodescribe le modalità di esecuzione contenitore hello.

Per altre informazioni, vedere [Visual Studio Container Tools][link-visualstudio-container-tools].

>[!NOTE]
>Se è hello prima volta che si eseguono le immagini contenitore di Windows nel computer in uso, Docker CE necessario abbassare di immagini di base per i contenitori di hello. le immagini di Hello utilizzate in questa esercitazione sono 14 GB. Procedo ed eseguo hello seguendo le immagini di base hello toopull comando terminal:
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a>Aggiungere il supporto di Docker

Aprire hello [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] file in Visual Studio.

Pulsante destro del mouse hello **FabrikamFiber.Web** progetto > **Aggiungi** > **Docker supporto**.

### <a name="add-support-for-sql"></a>Aggiungere il supporto per SQL

Questa applicazione Usa SQL come provider di dati hello, in modo da un server SQL è un'applicazione hello toorun obbligatorio. Fare riferimento a un'immagine del contenitore SQL Server nel file docker-compose.override.yml.

In Visual Studio, aprire **Esplora**, trovare **comporre docker**e i file aperti hello **docker compose.override.yml**.

Passare toohello `services:` nodo, aggiungere un nodo denominato `db:` che definisce una voce di SQL Server hello per contenitore hello.

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
>Per il debug locale è possibile usare un'istanza di SQL Server a scelta, a condizione che sia raggiungibile dall'host. **localdb**, tuttavia, non supporta la comunicazione `container -> host`.

>[!WARNING]
>L'esecuzione di SQL Server in un contenitore non consente di rendere persistenti i dati. Quando si arresta il contenitore di hello, i dati vengono cancellati. Non usare questa configurazione per la produzione.

Passare toohello `fabrikamfiber.web:` nodo e aggiungere un nodo figlio denominato `depends_on:`. Ciò garantisce che hello `db` avvio del servizio (contenitore di SQL Server hello) prima che l'applicazione web (fabrikamfiber.web).

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a>Aggiornamento configurazione web hello

In hello **FabrikamFiber.Web** del progetto, stringa di connessione di aggiornamento hello in hello **Web. config** file toopoint toohello SQL Server nel contenitore hello.

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
>Se si desidera creare un Server SQL diverso durante la compilazione di una versione dell'applicazione web toouse, aggiungere un altro file web.release.config tooyour della stringa connessione.

### <a name="test-your-container"></a>Testare il contenitore

Premere **F5** nel contenitore di un'applicazione hello toorun ed eseguire il debug.

Bordo verrà visualizzata la pagina di avvio definite dell'applicazione utilizzando l'indirizzo IP hello del contenitore hello in rete NAT interna hello (in genere 172.x.x.x). toolearn ulteriori informazioni su debug di applicazioni in contenitori usando Visual Studio 2017, vedere [questo articolo][link-debug-container].

![esempio di fabrikam in un contenitore][image-web-preview]

contenitore Hello è ora pronto toobe compilato e compresso in un'applicazione di Service Fabric. Dopo aver creato immagine contenitore hello compilato nel computer, è possibile inviare del Registro di sistema di tooany contenitore ed estrarlo tooany host toorun verso il basso.

## <a name="get-hello-application-ready-for-hello-cloud"></a>Prepararsi per il cloud hello applicazione hello

applicazione hello tooget pronta per l'esecuzione nell'infrastruttura di servizio in Azure, è necessario toocomplete due passaggi:

1. Esporre porta hello in cui desideriamo tooreach in grado di toobe l'applicazione web in cluster di Service Fabric hello.
2. Predisporre un database SQL di produzione pronto per l'applicazione.

### <a name="expose-hello-port-for-hello-app"></a>Esporre porta hello per app hello
cluster di Service Fabric Hello è stato configurato, è la porta *80* aperta per impostazione predefinita in hello bilanciamento del carico di Azure, che consente di bilanciare cluster toohello di traffico in ingresso. È possibile esporre il contenitore su questa porta tramite il file docker-compose.ym.

In Visual Studio, aprire **Esplora**, trovare **comporre docker**e i file aperti hello **docker compose.override.yml**.

Modificare hello `fabrikamfiber.web:` nodo, aggiungere un nodo figlio denominato `ports:`.

Aggiungere una voce di stringa `- "80:80"`.

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a>Usare un database SQL di produzione
Durante l'esecuzione nell'ambiente di produzione, è necessario mantenere i dati persistenti nel database. Non sono attualmente disponibili dati di permanente di tooguarantee modo in un contenitore, pertanto non è possibile archiviare dati di produzione in SQL Server in un contenitore.

È consigliabile usare un database SQL di Azure. tooset backup ed eseguire un Server gestito di SQL in Azure, visitare hello [Guida introduttiva di Azure SQL Database] [ link-azure-sql] articolo.

>[!NOTE]
>Occorre ricordare che toochange hello connessione stringhe toohello SQL server in hello **web.release.config** file hello **FabrikamFiber.Web** progetto.
>
>Questa applicazione non funziona correttamente se i database SQL non sono raggiungibili. È possibile scegliere toogo-ahead e distribuire un'applicazione hello senza un server SQL.

## <a name="deploy-with-visual-studio-team-services"></a>Distribuire con Visual Studio Team Services

tooset la distribuzione in Visual Studio Team Services, è necessario hello tooinstall [estensione strumenti di distribuzione continua per Visual Studio 2017][link-visualstudio-cd-extension]. Questa estensione rende facile toodeploy tooAzure tramite la configurazione di Visual Studio Team Services e ottenere il cluster di Service Fabric tooyour app distribuita.

tooget avviato, il codice deve essere ospitato in controllo del codice sorgente. resto Hello di questa sezione presuppone **git** è in uso.

### <a name="set-up-a-vsts-repo"></a>Configurare un repository VSTS
Nell'angolo in basso a destra di hello di Visual Studio, fare clic su **aggiungere tooSource controllo** > **Git** (o qualsiasi opzione desiderato).

![Premere il pulsante controllo origine hello][image-source-control]

In hello _Team Explorer_ riquadro, premere **pubblicare repository Git**.

Selezionare il nome dell'archivio VSTS e premere **Repository**.

![pubblicare tooVSTS repository][image-publish-repo]

Ora che il codice è sincronizzato con l'archivio del codice sorgente VSTS, è possibile configurare la distribuzione continua e il recapito continuo.

### <a name="setup-continuous-delivery"></a>Configurare il recapito continuo

In _Esplora_, hello rapida **soluzione** > **configurare la distribuzione continua**.

Selezionare hello sottoscrizione Azure.

Impostare **tipo Host** troppo**Cluster di Service Fabric**.

Impostare **Host di destinazione** creato nella sezione precedente hello cluster di toohello service fabric.

Scegliere un **Registro di sistema contenitore** toopublish nel contenitore.

>[!TIP]
>Hello utilizzare **modifica** pulsante toocreate del Registro di sistema un contenitore.

Premere **OK**.

![impostazione dell'integrazione continua di Service Fabric][image-setup-ci]
   
   Una volta completata la configurazione hello, il contenitore è distribuito tooService dell'infrastruttura. Ogni volta che si esegue il push del repository toohello aggiornamenti viene eseguita una nuova compilazione e versione.
   
   >[!NOTE]
   >Immagini contenitore di compilazione hello necessari circa 15 minuti.
   >cluster Service Fabric toohello Hello prima distribuzione comporta hello base Windows Server Core contenitore immagini toobe scaricato. download di Hello accetta toocomplete aggiuntive 5-10 minuti.

Esplora applicazione Fabrikam Call Center toohello utilizzando url hello del cluster: ad esempio, *http://mycluster.westeurope.cloudapp.azure.com*

Ora che si dispone di contenitore e di soluzione Fabrikam Call Center hello distribuita, è possibile aprire hello [portale di Azure] [ link-azure-portal] e vedere applicazione hello in esecuzione nell'infrastruttura del servizio. un'applicazione hello tootry, aprire un web browser e passare toohello URL del cluster di Service Fabric.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Creare un progetto Docker in Visual Studio
> * Distribuire un'applicazione esistente in un contenitore
> * Configurare l'integrazione continua con Visual Studio e VSTS

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
