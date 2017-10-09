---
title: aaaVisualizing il cluster usando Service Fabric Explorer | Documenti Microsoft
description: "Service Fabric Explorer è uno strumento basato sul Web per analizzare e gestire nodi e applicazioni cloud in un cluster di Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a>Visualizzare il cluster con Service Fabric Explorer
Service Fabric Explorer è uno strumento basato sul web per analizzare e gestire applicazioni e nodi in un cluster di Service Fabric di Azure. Service Fabric Explorer è ospitato direttamente all'interno di cluster hello, pertanto è sempre disponibile, indipendentemente dal fatto in cui il cluster è in esecuzione.

## <a name="video-tutorial"></a>Esercitazione video

toolearn come toouse Service Fabric Explorer, guardare hello seguente video Microsoft Virtual Academy:

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a>Connettersi tooService Fabric Explorer
Se si sono seguite le istruzioni di hello troppo[preparare l'ambiente di sviluppo](service-fabric-get-started.md), è possibile avviare Service Fabric Explorer sul cluster locale passando toohttp://localhost:19080 / Explorer.

## <a name="understand-hello-service-fabric-explorer-layout"></a>Comprendere il layout di Service Fabric Explorer hello
È possibile spostarsi Service Fabric Explorer con struttura ad albero hello a sinistra di hello. Nella radice dell'albero di hello hello dashboard cluster hello viene fornita una panoramica del cluster, incluso un riepilogo dell'applicazione e l'integrità del nodo.

![Dashboard del cluster di Service Fabric Explorer][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a>Visualizzare il layout del cluster hello
I nodi in un cluster di Service Fabric sono posizionati in una griglia bidimensionale di domini di errore e domini di aggiornamento. Questa posizione assicura che le applicazioni rimangano disponibili in presenza di hello di errori hardware e gli aggiornamenti dell'applicazione. È possibile visualizzare il layout cluster corrente hello utilizzando hello cluster mappa.

![Mappa del cluster di Service Fabric Explorer][sfx-cluster-map]

### <a name="view-applications-and-services"></a>Visualizzare applicazioni e servizi
cluster Hello contiene due sottoalberi: uno per applicazioni e un altro per i nodi.

È possibile utilizzare hello applicazione vista toonavigate tramite la gerarchia logica dell'infrastruttura servizio: le applicazioni, servizi, partizioni e repliche.

Nel seguente esempio hello hello applicazione **MyApp** è costituito da due servizi, **MyStatefulService** e **WebService**. Poiché **MyStatefulService** è con stato, include una partizione con una replica primaria e due repliche secondarie. Al contrario, il WebSvcService è senza stato e contiene una singola istanza.

![Visualizzazione delle applicazioni di Service Fabric Explorer][sfx-application-tree]

Ogni livello della struttura ad albero hello riquadro principale hello Mostra le informazioni pertinenti elemento hello. Ad esempio, è possibile visualizzare lo stato di integrità hello e la versione per un determinato servizio.

![Riquadro essentials di Service Fabric Explorer][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a>Visualizzare i nodi del cluster hello
visualizzazione del nodo Hello Mostra struttura fisica di hello del cluster di hello. Per un determinato nodo, è possibile esaminare le applicazioni con il codice distribuito in quel nodo. In particolare, è possibile visualizzare le repliche attualmente in esecuzione.

## <a name="actions"></a>Azioni
Service Fabric Explorer offre un modo rapido di tooinvoke azioni sui nodi, applicazioni e servizi all'interno del cluster.

Ad esempio, toodelete un'istanza dell'applicazione, scegliere un'applicazione hello dalla struttura ad albero hello hello sinistra, quindi **azioni** > **Elimina applicazione**.

![Eliminazione di un'applicazione in Service Fabric Explorer][sfx-delete-application]

> [!TIP]
> È possibile eseguire hello stesse azioni facendo clic su elemento tooeach successivo di hello i puntini di sospensione.
>
>

Hello nella tabella seguente sono elencate le azioni di hello disponibili per ogni entità:

| **Entità** | **Azione** | **Descrizione** |
| --- | --- | --- |
| Tipo di applicazione |Annullare il provisioning del tipo |Rimuove il pacchetto di applicazione hello dall'archivio di immagini del cluster hello. Richiede tutte le applicazioni di tale tipo di toobe rimossa prima. |
| Applicazione |Elimina applicazione |Eliminare un'applicazione hello, inclusi tutti i relativi servizi e il relativo stato (se presente). |
| Service |Eliminare il servizio |Eliminare il servizio hello e del relativo stato (se presente). |
| Nodo |Activate |Attivare un nodo di hello. |
| Nodo | Disattivare (sospendere) | Sospendi nodo hello nello stato corrente. Servizi continuino toorun ma Service Fabric non in modo proattivo spostare nulla su o off, a meno che non è necessario tooprevent un'interruzione del servizio o un'incoerenza dei dati. Questa azione è in genere utilizzate tooenable debug dei servizi in un nodo specifico di tooensure che non passano durante il controllo. | |
| Nodo | Disattivare (riavviare) | Spostare tutti i servizi in memoria all'esterno di un nodo e chiudere i servizi permanenti in modo sicuro. In genere utilizzato quando i processi host hello o toobe necessità computer riavviato. | |
| Nodo | Disattivare (rimuovere i dati) | Chiudere tutti i servizi in esecuzione nel nodo di hello dopo la creazione di repliche riserva sufficienti. Questa azione viene in genere usata quando un nodo (o almeno lo spazio di archiviazione correlato) viene reso improduttivo in modo permanente. | |
| Nodo | Rimuovere lo stato del nodo | Rimuovere conoscenza delle repliche di un nodo dal cluster hello. Questa azione viene in genere usata quando un nodo che ha già avuto esito negativo viene ritenuto non recuperabile. | |
| Nodo | Riavvia | Riavviare il nodo hello per simulare un errore di nodo. Altre informazioni sono disponibili [qui](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps) | |

Poiché molte azioni sono distruttive, potrebbe essere richiesto tooconfirm lo scopo previsto prima che venga completato l'azione di hello.

> [!TIP]
> Ogni azione che può essere eseguita tramite Service Fabric Explorer può essere eseguite anche tramite PowerShell o un'API REST, tooenable automazione.
>
>

È anche possibile utilizzare le istanze dell'applicazione di Service Fabric Explorer toocreate per un tipo di applicazione specificata e la versione. Scegliere il tipo di applicazione hello nella visualizzazione ad albero di hello, quindi fare clic su hello **Crea istanza app** versione toohello successivo collegamento desiderato nel riquadro di destra hello.

![Creazione di un'istanza dell'applicazione in Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> Non è attualmente possibile impostare parametri per le istanze dell'applicazione create mediante Service Fabric Explorer, per le quali vengono usati valori di parametro predefiniti.
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a>Connettere il cluster di Service Fabric remoto tooa
Se si conosce l'endpoint del cluster hello e si dispone di autorizzazioni sufficienti per accedere Service Fabric Explorer da qualsiasi browser. Infatti, Service Fabric Explorer è semplicemente un altro servizio che viene eseguito nel cluster hello.

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a>Individuare l'endpoint di Service Fabric Explorer hello per un cluster remoto
tooreach Service Fabric Explorer per un determinato cluster, puntare il browser per:

http://&lt;your-cluster-endpoint&gt;:19080/Explorer

Per i cluster di Azure, l'URL completo hello disponibile anche nel riquadro di essentials cluster hello di hello portale di Azure.

### <a name="connect-tooa-secure-cluster"></a>Connettere il cluster protetto di tooa
È possibile controllare client accesso tooyour cluster di Service Fabric con certificati o tramite Azure Active Directory (AAD).

Se si tenta di tooconnect tooService Fabric Explorer in un cluster protetto, quindi a seconda della configurazione del cluster hello si essere toopresent richiesto un certificato client oppure accedi con Azure ad.

## <a name="next-steps"></a>Passaggi successivi
* [Panoramica di Testabilità](service-fabric-testability-overview.md)
* [Gestione delle applicazioni di Service Fabric in Visual Studio](service-fabric-manage-application-in-visual-studio.md)
* [Distribuzione di un'applicazione di Infrastruttura di servizi mediante PowerShell](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
