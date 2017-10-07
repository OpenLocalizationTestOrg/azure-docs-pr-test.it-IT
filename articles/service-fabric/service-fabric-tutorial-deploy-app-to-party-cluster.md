---
title: aaaDeploy un tooa applicazione Azure Service Fabric Cluster di terze parti | Documenti Microsoft
description: Informazioni su come toodeploy tooa un'applicazione Cluster di terze parti.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: db16b6418fa2533ed915c8b6e612b7a8e7311bed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-party-cluster-in-azure"></a>Distribuire un tooa applicazione Cluster di terze parti in Azure
In questa esercitazione fa parte di due di una serie e illustra come toodeploy un tooa applicazione Azure Service Fabric Cluster di terze parti in Azure.

Nel parte due serie di esercitazioni hello, si apprenderà come:
> [!div class="checklist"]
> * Distribuire un cluster remoto tooa applicazione con Visual Studio
> * Rimuovere un'applicazione da un cluster usando Service Fabric Explorer

In questa serie di esercitazioni si apprenderà come:
> [!div class="checklist"]
> * [Creare un'applicazione di Service Fabric .NET](service-fabric-tutorial-create-dotnet-app.md)
> * Distribuire hello applicazione tooa remota del cluster
> * [Configurare l'integrazione continua e la distribuzione continua usando Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione:
- Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Installare Visual Studio 2017](https://www.visualstudio.com/) e installare hello **lo sviluppo di Azure** e **sviluppo web ASP.NET e** i carichi di lavoro.
- [Installare hello Service Fabric SDK](service-fabric-get-started.md)

## <a name="download-hello-voting-sample-application"></a>Scaricare l'applicazione di esempio hello voto
Se si non compila l'applicazione di esempio hello voto [parte 1 di questa serie di esercitazioni](service-fabric-tutorial-create-dotnet-app.md), è possibile scaricarlo. In una finestra di comando, eseguire hello successivo comando tooclone hello esempio app repository tooyour computer locale.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a>Configurare un cluster di entità
Cluster di terze parti sono i cluster di Service Fabric gratuito, periodo di tempo limitato ospitati in Azure e vengono eseguiti dal team di Service Fabric hello in tutti gli utenti possono distribuire le applicazioni e informazioni sulla piattaforma hello. Gratuitamente.

tooget accesso tooa Cluster di terze parti, visitare il sito di toothis: http://aka.ms/tryservicefabric e seguire hello istruzioni tooget tooa cluster di accesso. È necessario un Facebook o GitHub account tooget accesso tooa Cluster di terze parti.

> [!NOTE]
> Cluster di terze parti non sono protetti in modo le applicazioni e tutti i dati inseriti in essi contenuti possono essere tooothers visibile. Non eseguire la distribuzione di qualsiasi elemento non si desidera che altri toosee. Essere tooread che le condizioni di utilizzo per tutti i dettagli di hello.

## <a name="configure-hello-listening-port"></a>Configurare una porta di attesa hello
Quando viene creato hello servizio front-end VotingWeb, Visual Studio seleziona casualmente una porta per toolisten servizio hello in.  Hello VotingWeb servizio agisce come front-end per l'applicazione hello e accetta il traffico esterno, andiamo associare tooa tale servizio predefinito e porta conosciuto. In Esplora soluzioni aprire *VotingWeb/PackageRoot/ServiceManifest.xml*.  Trovare hello **Endpoint** risorsa hello **risorse** sezione e modificare hello **porta** too80 valore.

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

Aggiornare anche il valore della proprietà URL dell'applicazione hello nel progetto di voto hello in modo da un web browser apre la porta corretta toohello quando si esegue il debug utilizzando 'F5'.  In Esplora soluzioni selezionare hello **voto** hello progetto e aggiornare **URL applicazione** proprietà.

![URL applicazione](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-hello-app-toohello-azure"></a>Distribuire toohello app hello Azure
Ora che un'applicazione hello è pronta, è possibile distribuire toohello Cluster di terze parti direttamente da Visual Studio.

1. Fare doppio clic su **voto** in hello Esplora soluzioni e scegliere **pubblica**.

    ![Finestra di dialogo Pubblica](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. Digitare hello Endpoint della connessione di hello Cluster di terze parti in hello **Endpoint della connessione** campo e fare clic su **pubblica**.

    Una volta pubblicare hello è completata, dovrebbe essere in grado di toosend un'applicazione toohello richiesta tramite un browser.

3. Aprire preferito browser e digitare l'indirizzo del cluster hello (endpoint hello connessione senza le informazioni sulla porta hello - ad esempio, win1kw5649s.westus.cloudapp.azure.com).

    Dovrebbe essere hello stesso risultato, come specificato durante l'esecuzione di un'applicazione hello in locale.

    ![Risposta API dal cluster](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-hello-application-from-a-cluster-using-service-fabric-explorer"></a>Rimuovere un'applicazione hello da un cluster usando Service Fabric Explorer
Service Fabric Explorer è un tooexplore di interfaccia utente grafica e gestire le applicazioni in un cluster di Service Fabric.

applicazione hello tooremove da hello Cluster di terze parti:

1. Sfoglia toohello Service Fabric Explorer, usando il collegamento di hello fornito dalla pagina di iscrizione di hello Cluster di terze parti. Ad esempio, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.

2. In Service Fabric Explorer, passare toohello **fabric://Voting** nodo di treeview hello sul lato sinistro di hello.

3. Fare clic su hello **azione** pulsante hello destro **Essentials** riquadro, quindi scegliere **Elimina applicazione**. Conferma eliminazione istanza dell'applicazione hello, che consente di rimuovere l'applicazione in esecuzione nel cluster hello istanza hello.

![Eliminare un'applicazione in Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-hello-application-type-from-a-cluster-using-service-fabric-explorer"></a>Rimuovere il tipo di applicazione hello da un cluster usando Service Fabric Explorer
Le applicazioni vengono distribuite come tipi di applicazioni in un cluster di Service Fabric, che consente di toohave più istanze e versioni di un'applicazione hello in esecuzione all'interno di cluster hello. Dopo la rimozione di hello in esecuzione l'istanza dell'applicazione, è anche possibile rimuovere tipo hello, pulizia hello toocomplete della distribuzione hello.

Per ulteriori informazioni sul modello di applicazione hello nell'infrastruttura del servizio, vedere [un'applicazione nell'infrastruttura del servizio del modello](service-fabric-application-model.md).

1. Passare toohello **VotingType** nodo di treeview hello.

2. Fare clic su hello **azione** pulsante hello destro **Essentials** riquadro e scegliere **tipo annullamento del provisioning**. Confermare l'annullamento del provisioning del tipo di applicazione hello.

![Annullare il provisioning del tipo di applicazione in Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

Questo conclude l'esercitazione hello.

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Distribuire un cluster remoto tooa applicazione con Visual Studio
> * Rimuovere un'applicazione da un cluster usando Service Fabric Explorer

Esercitazione successiva toohello avanzate:
> [!div class="nextstepaction"]
> [Impostare l'integrazione continua usando Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)