---
title: aaaCreate un servizio affidabile di Azure Service Fabric con c#
description: Creare e distribuire un'applicazione Reliable Services basata su Azure Service Fabric ed eseguirne il debug con Visual Studio.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a>Creare la prima applicazione Reliable Services con stato C# di Service Fabric

Informazioni su come toodeploy della prima applicazione di Service Fabric per .NET su Windows in pochi minuti. Al termine, si avrà un cluster locale in esecuzione con un'applicazione Reliable Services.

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare, assicurarsi di avere [configurato l'ambiente di sviluppo](service-fabric-get-started.md). Questo include l'installazione di Service Fabric SDK hello e Visual Studio 2017 o 2015.

## <a name="create-hello-application"></a>Creare un'applicazione hello

Avviare Visual Studio come **amministratore**.

Creare un progetto con `CTRL`+`SHIFT`+`N`.

In hello **nuovo progetto** finestra di dialogo, scegliere **Cloud > applicazione di Service Fabric**.

Nome di un'applicazione hello **MyApplication** e premere **OK**.

   
![Finestra di dialogo Nuovo progetto in Visual Studio][1]

È possibile creare qualsiasi tipo di applicazione di Service Fabric dalla finestra di dialogo successiva hello. Per questa guida introduttiva scegliere **Servizio con stato**.

Nome servizio hello **MyStatefulService** e premere **OK**.

![Finestra di dialogo Nuovo servizio in Visual Studio][2]


Visual Studio crea il progetto di applicazione hello e il progetto di servizio con stato hello e li visualizza in Esplora soluzioni.

![Esplora soluzioni dopo la creazione dell'applicazione con servizio con stato][3]

progetto di applicazione Hello (**MyApplication**) non contiene il codice direttamente. Fa invece riferimento a un set di progetti di servizio. Include inoltre altri tre tipi di contenuto:

* **Profili di pubblicazione**  
Profili per la distribuzione di ambienti toodifferent.

* **Script**  
Script di PowerShell per distribuire o aggiornare l'applicazione.

* **Definizione di applicazione**  
Include file ApplicationManifest XML hello in *ApplicationPackageRoot* che descrive la composizione dell'applicazione. I file dei parametri dell'applicazione associati sono in *ApplicationParameters*, che può essere utilizzato toospecify parametri specifici dell'ambiente. Istruzioni SELECT di Visual Studio associato a un file di parametro dell'applicazione specificato nel hello profilo di pubblicazione durante l'ambiente di distribuzione tooa specifico.
    
Per una panoramica del contenuto di hello hello del progetto di servizio, vedere [Introduzione a servizi affidabili](service-fabric-reliable-services-quick-start.md).

## <a name="deploy-and-debug-hello-application"></a>Distribuire ed eseguire il debug di un'applicazione hello

A questo punto, eseguire l'applicazione creata.

In Visual Studio, premere `F5` toodeploy per il debug di un'applicazione hello.

>[!NOTE]
>Hello prima eseguire e distribuire un'applicazione hello in locale, Visual Studio crea un cluster locale per il debug. Questa operazione potrebbe richiedere tempo. lo stato di creazione di cluster Hello viene visualizzato nella finestra di output di hello Visual Studio.

Quando il cluster hello è pronto, si riceve una notifica di hello cluster locale Gestione applicazione area di notifica inclusa hello SDK.
   
![Notifica della barra delle applicazioni per il cluster locale][4]

Una volta viene avviata l'applicazione hello, Visual Studio automaticamente apparirà hello **Visualizzatore eventi di diagnostica**, in cui è possibile visualizzare l'output di traccia dai servizi.
   
![Visualizzatore eventi di diagnostica][5]

Hello modello di servizio con stato utilizzassimo mostra semplicemente un valore di contatore incremento in hello `RunAsync` metodo **MyStatefulService.cs**.

Espandere una delle hello eventi toosee ulteriori dettagli, incluso il nodo hello in cui è in esecuzione codice hello. In questo caso è \_Node\_2, anche se nel computer locale potrebbe essere diverso.
   
![Dettaglio del visualizzatore eventi di diagnostica][6]

cluster locale Hello contiene cinque nodi ospitati in un singolo computer. In un ambiente di produzione, ogni nodo è ospitato in una macchina virtuale o un computer fisico distinto. perdita di hello toosimulate di una macchina durante lo eserciterebbe hello Visual Studio del debugger in hello stessa ora e diamo un'occhiata a uno dei nodi cluster locale hello hello.

In hello **Esplora** finestra, aprire **MyStatefulService.cs**. 

Trovare hello `RunAsync` metodo e impostare un punto di interruzione della prima riga hello del metodo hello.

![Punto di interruzione nel metodo RunAsync del servizio con stato][7]

Avviare hello **Service Fabric Explorer** strumento facendo clic su hello **gestione Cluster locale** applicazione area di notifica e scegliere **gestire Cluster locale**.

![Avviare Service Fabric Explorer da hello gestione Cluster locale][systray-launch-sfx]

[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offre una rappresentazione visiva del cluster, Include set hello di applicazioni distribuite tooit e nodi fisici che compongono il set di hello.

Nel riquadro sinistro hello espandere **Cluster > nodi** e trova hello nodo in cui viene eseguito il codice.

Fare clic su **azioni > Disattiva (riavvio)** toosimulate un riavvio del computer.

![Arresto di un nodo in Service Fabric Explorer][sfx-stop-node]

Temporaneamente, verrà visualizzato il punto di interruzione raggiunto in Visual Studio come calcolo hello stavi facendo facilmente in un nodo viene eseguito il failover tooanother.


Successivamente, restituire toohello Visualizzatore eventi di diagnostica e osservare i messaggi hello. contatore Hello continua incremento, anche se gli eventi di hello effettivamente derivano da un nodo diverso.

![Visualizzatore eventi di diagnostica dopo il failover][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a>Pulizia dei cluster locale hello (facoltativo)

Tenere presente che il cluster locale è reale. Arrestare il debugger hello rimuove l'istanza dell'applicazione e Annulla la registrazione di tipo di applicazione hello. Tuttavia, i cluster hello continua toorun in background hello. Quando sarai pronto toostop cluster locale di hello, sono disponibili due opzioni.

### <a name="keep-application-and-trace-data"></a>Mantenere i dati applicazione e di traccia

Arrestare il cluster di hello facendo clic su hello **gestione Cluster locale** applicazione area di notifica e quindi scegliere **arrestare Cluster locale**.

### <a name="delete-hello-cluster-and-all-data"></a>Eliminare il cluster hello e tutti i dati

Rimuovere il cluster di hello facendo clic su hello **gestione Cluster locale** applicazione area di notifica e quindi scegliere **rimuovere Cluster locale**. 

Se si sceglie questa opzione, Visual Studio verrà distribuito nuovamente hello cluster hello successivo hello di eseguire l'applicazione. Scegliere questa opzione se non si prevede di cluster locale di hello toouse per un certo tempo o se è necessario tooreclaim risorse.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Reliable Services](service-fabric-reliable-services-introduction.md).
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
