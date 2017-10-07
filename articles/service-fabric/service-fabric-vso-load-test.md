---
title: aaaLoad testare l'applicazione tramite Visual Studio Team Services | Documenti Microsoft
description: Informazioni su come testare le applicazioni Azure Service Fabric di toostress utilizzando Visual Studio Team Services.
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: fc743585-0d1b-483f-981d-493f4552ac07
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 663cf8db5e8f0a4d0d7f27b585645d7f776392f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-test-your-application-by-using-visual-studio-team-services"></a>Eseguire test di carico dell'applicazione usando Visual Studio Team Services
Questo articolo illustra come toostress di funzionalità test di carico di toouse Microsoft Visual Studio test di un'applicazione. Viene usato un back-end del servizio con stato di Service Fabric di Azure e un front-end Web di un servizio senza stato. Hello applicazione di esempio utilizzato in questo argomento è un simulatore di percorso aereo. È necessario fornire l'ID dell'aereo, l'orario di partenza e la destinazione. back-end dell'applicazione Hello elabora le richieste di hello e front-end hello Visualizza in un aereo hello mappa che corrisponde ai criteri di hello.

Hello diagramma seguente illustra un'applicazione Service Fabric hello che verranno testate.

![Diagramma di un'applicazione hello esempio aereo percorso][0]

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare, è necessario seguente hello toodo:

* Ottenere un account di Visual Studio Team Services. È possibile ottenerne uno gratuitamente visitando [Visual Studio Team Services](https://www.visualstudio.com).
* Ottenere e installare Visual Studio 2013 o Visual Studio 2015. Questo articolo usa Visual Studio 2015 Enterprise Edition, ma Visual Studio 2013 e altre edizioni dovrebbero funzionare in modo simile.
* Distribuire l'applicazione tooa ambiente di gestione temporanea. Vedere [come toodeploy applicazioni tooa remoto cluster utilizzando Visual Studio](service-fabric-publish-app-remote-cluster.md) per informazioni su questo argomento.
* Comprendere il modello d'uso dell'applicazione. Queste informazioni sono il modello di carico hello toosimulate utilizzato.
* Comprendere l'obiettivo di hello per il test di carico. Consente di interpretare e analizzare i risultati del test di carico hello.

## <a name="create-and-run-hello-web-performance-and-load-test-project"></a>Creare ed eseguire il progetto di Test di carico e prestazioni Web hello
### <a name="create-a-web-performance-and-load-test-project"></a>Creare il progetto Test di carico e prestazioni Web
1. Aprire Visual Studio 2015. Scegliere **File** > **New** > **progetto** menu hello barra hello tooopen **nuovo progetto** la finestra di dialogo.
2. Espandere hello **Visual c#** nodo e scegliere **Test** > **progetto di Test di carico e prestazioni Web**. Assegnare un nome progetto hello e quindi scegliere hello **OK** pulsante.

    ![Cattura di schermata della finestra di dialogo Nuovo progetto hello][1]

    Verrà visualizzato il nuovo progetto di test di carico e prestazioni Web in Esplora soluzioni.

    ![Cattura di schermata della finestra Esplora soluzioni con un nuovo progetto hello][2]

### <a name="record-a-web-performance-test"></a>Registrare un test di prestazioni Web
1. Progetto WebTest hello aperto.
2. Scegliere hello **aggiungere registrazione** icona toostart una sessione di registrazione nel browser.

    ![Cattura di schermata dell'icona Aggiungi registrazione hello in un browser][3]

    ![Cattura di schermata del pulsante Record hello in un browser][4]
3. Individuare l'applicazione di Service Fabric toohello. Pannello registrazione Hello deve visualizzare le richieste web hello.

    ![Cattura di schermata delle richieste web in hello pannello registrazione][5]
4. Eseguire una sequenza di azioni che si prevede di hello utenti tooperform. Queste azioni vengono utilizzate come carico di hello toogenerate un modello.
5. Al termine, scegliere hello **arrestare** registrazione toostop pulsante.

    ![Cattura di schermata del pulsante di arresto hello][6]

    progetto WebTest Hello in Visual Studio deve avere acquisito una serie di richieste. I parametri dinamici vengono sostituiti automaticamente. A questo punto, è possibile eliminare qualsiasi richiesta aggiuntiva ripetuta di dipendenza che non fa parte dello scenario di test.
6. Salvare il progetto hello e quindi scegliere hello **Esegui Test** delle prestazioni web di comando toorun hello test in locale e assicurarsi che tutto funzioni correttamente.

    ![Cattura di schermata di hello comando Esegui Test][7]

### <a name="parameterize-hello-web-performance-test"></a>Test delle prestazioni web hello parametrizzare
Conversione di test delle prestazioni web codificato tooa e quindi modificando il codice hello, è possibile parametrizzare hello test delle prestazioni web. In alternativa, è possibile associare l'elenco di dati tooa test prestazioni web hello in modo che hello test scorre dati hello. Vedere [generare ed eseguire un test delle prestazioni web codificato](https://msdn.microsoft.com/library/ms182552.aspx) per informazioni dettagliate su come tooa test delle prestazioni di tooconvert hello web test codificato. Vedere [aggiungere un test delle prestazioni web tooa origine dati](https://msdn.microsoft.com/library/ms243142.aspx) per informazioni su come toobind tooa di dati delle prestazioni web test.

Per questo esempio, test codificato tooa test delle prestazioni web hello verrà convertito in modo è possibile sostituire hello aereo ID con un GUID generato e aggiungere ulteriori richieste toosend voli toodifferent percorsi.

### <a name="create-a-load-test-project"></a>Creare un progetto di test di carico
Un progetto di test di carico è costituito da uno o più scenari descritti dal test delle prestazioni web hello e unit test, insieme alle impostazioni di test di carico specificato aggiuntive. Hello alla procedura seguente mostra come progetto di test toocreate un carico:

1. Hello dal menu di scelta rapida del progetto di Test di carico e prestazioni Web, scegliere **Aggiungi** > **Test di carico**. In hello **dei Test di carico** procedura guidata, scegliere hello **Avanti** pulsante Impostazioni di test tooconfigure hello.
2. In hello **modello di carico** , scegliere se si desidera che un carico costante utente o un carico per passaggio, che inizia con alcuni utenti e aumenta hello gli utenti nel tempo.

    Se si hanno una buona stima della quantità di hello di carico utente, le prestazioni di sistema corrente hello toosee scegliere **carico costante**. Se l'obiettivo è toolearn se sistema hello viene eseguita in modo coerente in vari carichi, scegliere **carico per passaggio**.
3. In hello **combinazione di Test** , scegliere hello **Aggiungi** pulsante e quindi seleziona hello test che si desidera tooinclude hello test di carico. È possibile utilizzare hello **distribuzione** percentuale di hello toospecify colonna totale dell'esecuzione dei test per ogni test.
4. In hello **impostazioni di esecuzione** sezione, specificare la durata del test di carico hello.

   > [!NOTE]
   > Hello **iterazioni Test** opzione è disponibile solo quando si esegue un test di carico in locale utilizzando Visual Studio.
   >
   >
5. In hello **percorso** sezione **impostazioni di esecuzione**, specificare il percorso di hello in cui vengono generate richieste di test di carico. la procedura guidata Hello potrebbe richiedere toolog in tooyour account Team Services. Accedere e scegliere una posizione geografica. Al termine, scegliere hello **fine** pulsante.
6. Dopo aver creato il test di carico hello, aprire il progetto di LoadTest hello e scegliere l'impostazione di esecuzione, ad esempio corrente di hello **impostazioni di esecuzione** > **Run Settings1 [Active]**. Si apre le impostazioni di esecuzione hello in hello **proprietà** finestra.
7. In hello **risultati** sezione di hello **impostazioni di esecuzione** finestra Proprietà, hello **Intervallo archiviazione dettagli** impostazione deve avere **Nessuno** come il valore predefinito. Modificare questo valore troppo**tutti i singoli dettagli** tooget ulteriori informazioni sui risultati del test di carico hello. Vedere [test di carico](https://www.visualstudio.com/load-testing.aspx) per ulteriori informazioni su come tooconnect tooVisual Studio Team Services ed eseguire un carico di test.

### <a name="run-hello-load-test-by-using-visual-studio-team-services"></a>Eseguire il test di carico di hello utilizzando Visual Studio Team Services
Scegliere hello **esecuzione dei Test di carico** esecuzione dei test hello toostart comando.

![Cattura di schermata di hello comando Esegui Test di carico][8]

## <a name="view-and-analyze-hello-load-test-results"></a>Visualizzare e analizzare i risultati del test di carico hello
Come hello l'avanzamento del test di carico, le informazioni sulle prestazioni hello sono stato creato un grafico. Verrà visualizzato un codice simile toohello seguente grafico.

![Schermata del grafico delle prestazioni per i risultati di test di carico][9]

1. Scegliere hello **scaricare report** collegamento nella parte superiore di hello della pagina hello. Dopo aver scaricato report hello, scegliere hello **visualizzare report** pulsante.

    In hello **grafico** scheda è possibile visualizzare i grafici per diversi contatori di prestazioni. In hello **riepilogo** scheda hello complessiva risultati del test vengono visualizzati. Hello **tabelle** scheda Mostra numero totale di hello di test di carico non riuscita e non riusciti.
2. Scegliere i collegamenti numero hello hello **Test** > **Failed** hello e **errori** > **conteggio** colonne dettagli dell'errore toosee.

    Hello **dettaglio** scheda Mostra virtuale informazioni sullo scenario utente e test per richieste non riuscite. Questi dati possono essere utili se il test di carico hello include più scenari.

Vedere [analisi dei risultati Test di carico nella visualizzazione grafici dell'analizzatore Test di carico hello hello](https://www.visualstudio.com/load-testing.aspx) per ulteriori informazioni sulla visualizzazione carico risultati dei test.

## <a name="automate-your-load-test"></a>Automatizzare il test di carico
Visual Studio Team Services Test di carico fornisce API toohelp gestire test di carico e analizzare i risultati in un account Team Services. Per altre informazioni, vedere l'articolo relativo alle [API REST dei test di carico nel cloud](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) .

## <a name="next-steps"></a>Passaggi successivi
* [Monitoraggio e diagnosi dei servizi in una configurazione di sviluppo con computer locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[0]: ./media/service-fabric-vso-load-test/OverviewDiagram.png
[1]: ./media/service-fabric-vso-load-test/NewProjectDialog.png
[2]: ./media/service-fabric-vso-load-test/Project.png
[3]: ./media/service-fabric-vso-load-test/AddRecording.png
[4]: ./media/service-fabric-vso-load-test/AddRecording2.png
[5]: ./media/service-fabric-vso-load-test/ActionSequence.png
[6]: ./media/service-fabric-vso-load-test/StopRecording.png
[7]: ./media/service-fabric-vso-load-test/RunTest.png
[8]: ./media/service-fabric-vso-load-test/RunTest2.png
[9]: ./media/service-fabric-vso-load-test/Graph.png
