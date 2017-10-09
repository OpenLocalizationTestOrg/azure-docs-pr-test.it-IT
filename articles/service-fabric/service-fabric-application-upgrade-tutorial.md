---
title: esercitazione di aggiornamento di aaaService infrastruttura app | Documenti Microsoft
description: In questo articolo vengono esaminati esperienza hello di distribuzione di un'applicazione di Service Fabric, modificare il codice hello e implementazione di un aggiornamento tramite Visual Studio.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a3181a7a-9ab1-4216-b07a-05b79bd826a4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: d069ff0b291018dbac846e65cddff1e9d73d156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-tutorial-using-visual-studio"></a>Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

Azure Service Fabric semplifica il processo di hello di aggiornamento di applicazioni cloud assicurando che vengano aggiornati solo i servizi modificati, e che lo stato di applicazioni sia monitorato durante l'intero processo di aggiornamento hello. Inoltre automaticamente il rollback hello toohello precedente versione dell'applicazione in presenza di problemi. Gli aggiornamenti dell'applicazione di Service Fabric sono *i tempi di inattività di Zero*, dal momento che un'applicazione hello può essere aggiornata senza tempi di inattività. Questa esercitazione sono trattati come toocomplete un aggiornamento in sequenza da Visual Studio.

## <a name="step-1-build-and-publish-hello-visual-objects-sample"></a>Passaggio 1: Creare e pubblicare: esempio hello oggetti visivi
Scaricare innanzitutto hello [oggetti visivi](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Actors/VisualObjects) da GitHub. Quindi, compilare e pubblicare un'applicazione hello facendo clic sul progetto di applicazione hello **VisualObjects**e selezionando hello **pubblica** comando nella voce di menu hello Service Fabric.

![Menu di scelta rapida per un'applicazione di Service Fabric][image1]

Selezione **pubblica** , viene visualizzata una finestra popup, ed è possibile impostare hello **profilo di destinazione** troppo**PublishProfiles\Local.xml**. Hello finestra dovrebbe essere simile hello seguenti prima di scegliere **pubblica**.

![Pubblicazione di un'applicazione di Service Fabric][image2]

Ora è possibile fare clic su **pubblica** nella finestra di dialogo hello. È possibile utilizzare [Service Fabric Explorer tooview cluster e hello applicazione hello](service-fabric-visualizing-your-cluster.md). applicazione di oggetti visivi Hello è un servizio web che è possibile passare tooby digitando [http://localhost:8081visualobjects/](http://localhost:8081/visualobjects/) nella barra degli indirizzi del browser hello.  Dovrebbe essere 10 oggetti visivi mobili gli spostamenti nella schermata Ciao.

**Nota:** se la distribuzione troppo`Cloud.xml` profilo (Azure Service Fabric), un'applicazione hello quindi deve essere disponibile all'indirizzo **http://{ServiceFabricName}. { Region}.cloudapp.Azure.com:8081/visualobjects/**. Assicurarsi di avere `8081/TCP` configurato nel servizio di bilanciamento del carico hello (trovare hello bilanciamento del carico in hello stesso gruppo di risorse come istanza di Service Fabric hello).

## <a name="step-2-update-hello-visual-objects-sample"></a>Passaggio 2: Aggiornare: esempio hello oggetti visivi
È possibile notare che con la versione di hello che è stato distribuito nel passaggio 1, gli oggetti visivi hello non ruotare. Eseguire l'aggiornamento si tooone questa applicazione in cui gli oggetti visivi hello inoltre ruotare.

Selezionare il progetto VisualObjects.ActorService hello all'interno di hello soluzione VisualObjects e aprire hello **VisualObjectActor.cs** file. All'interno del file, passare il metodo toohello `MoveObject`, impostare come commento `visualObject.Move(false)`e rimuovere il commento `visualObject.Move(true)`. Questa modifica del codice ruota oggetti hello dopo l'aggiornamento di servizio hello.  **È ora possibile creare (non ricompilare) hello soluzione**, quali compilazioni hello modificato progetti. Se si seleziona *Ricompila tutto*, si dispone di versioni di hello tooupdate per tutti i progetti di hello.

È anche necessario tooversion l'applicazione. modifica della versione di hello toomake dopo fare clic su hello **VisualObjects** progetto, è possibile utilizzare Visual Studio hello **modifica manifesto versioni** opzione. Se si seleziona questa opzione viene visualizzata la finestra di dialogo hello per le versioni edition come indicato di seguito:

![Finestra di dialogo del controllo delle versioni][image3]

Aggiornamento di versioni hello per hello modificare progetti e ai pacchetti di codice, insieme a tooversion applicazione hello 2.0.0. Dopo aver apportato modifiche di hello, manifesto hello dovrebbe essere simile hello seguente (parti in grassetto mostrano le modifiche di hello):

![Aggiornamento di versioni][image4]

strumenti di Visual Studio Hello è possono eseguire il rollup automatico delle versioni quando si seleziona **aggiornare automaticamente versioni dell'applicazione e servizio**. Se si utilizza [SemVer](http://www.semver.org), è necessario utilizzare codice hello tooupdate e/o configurazione pacchetto versione solo se tale opzione è selezionata.

Salvare le modifiche di hello e controllare hello **hello aggiornamento applicazione** casella.

## <a name="step-3--upgrade-your-application"></a>Passaggio 3: Aggiornare l'applicazione
Acquisire familiarità con hello [parametri di aggiornamento dell'applicazione](service-fabric-application-upgrade-parameters.md) hello e [processo di aggiornamento](service-fabric-application-upgrade.md) tooget una buona conoscenza di hello vari parametri, valori di timeout e criterio di integrità che è possibile l'aggiornamento applicare. Questa procedura dettagliata, criteri di valutazione di integrità servizio hello sono impostato toohello predefinito (modalità non monitorata). È possibile configurare queste impostazioni selezionando **configurare impostazioni di aggiornamento** e quindi modificando i parametri di hello in base alle esigenze.

Ora siamo tutti i set di un'applicazione hello toostart aggiornamento selezionando **pubblica**. Questa opzione consente di aggiornare il tooversion applicazione 2.0.0, in cui gli oggetti hello ruotare. Service Fabric aggiornato un dominio di aggiornamento alla volta (alcuni oggetti vengono aggiornati per primi, seguito da altri utenti) e il servizio hello rimane accessibile durante l'aggiornamento di hello. Servizio di accesso toohello può essere verificato tramite il client (browser).  

A questo punto, come hello viene eseguito l'aggiornamento dell'applicazione, è possibile monitorarlo con Service Fabric Explorer, utilizzando hello **gli aggiornamenti in corso** scheda applicazioni hello.

In pochi minuti, tutti i domini di aggiornamento devono essere aggiornati (completato) e finestra di output di Visual Studio hello deve indicare anche che l'aggiornamento hello viene completata. E che si trova *tutti* ora la rotazione di oggetti visivi di hello nella finestra del browser.

È possibile desidera tootry versioni hello e spostando dalla versione 2.0.0 tooversion 3.0.0 come esercizio, o anche da versione 2.0.0 nuovamente tooversion 1.0.0. Provare a usare toomake di criteri di integrità e timeout manualmente familiarità con esse. Durante la distribuzione di cluster di Azure come tooan anziché cluster locale tooa, parametri hello utilizzati potrebbero essere toodiffer. È consigliabile impostare i timeout hello conservativamente.

## <a name="next-steps"></a>Passaggi successivi
[Aggiornamento di un'applicazione di Service Fabric mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) descrive la procedura di aggiornamento di un'applicazione tramite PowerShell.

Controllare l'aggiornamento dell'applicazione tramite i [parametri di aggiornamento](service-fabric-application-upgrade-parameters.md).

Apportare aggiornamenti applicazione compatibile da learning come toouse [la serializzazione dei dati](service-fabric-application-upgrade-data-serialization.md).

Informazioni su come toouse funzionalità avanzate durante l'aggiornamento dell'applicazione riferendosi troppo[argomenti avanzati](service-fabric-application-upgrade-advanced.md).

Risolvere i problemi comuni negli aggiornamenti dell'applicazione riferendosi passaggi toohello [gli aggiornamenti dell'applicazione di risoluzione dei problemi](service-fabric-application-upgrade-troubleshooting.md).

[image1]: media/service-fabric-application-upgrade-tutorial/upgrade7.png
[image2]: media/service-fabric-application-upgrade-tutorial/upgrade1.png
[image3]: media/service-fabric-application-upgrade-tutorial/upgrade5.png
[image4]: media/service-fabric-application-upgrade-tutorial/upgrade6.png
