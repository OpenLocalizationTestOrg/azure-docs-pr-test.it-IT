---
title: aaaDebugging di Azure servizio cloud o macchina virtuale in Visual Studio | Documenti Microsoft
description: Debug di un servizio cloud o di una macchina virtuale in Visual Studio
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 945e06e0-2100-41af-b218-72347367ddab
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 32a326430021ba2ea9317a6a71fa005d4b87c273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-an-azure-cloud-service-or-virtual-machine-in-visual-studio"></a>Debug di un servizio cloud o di una macchina virtuale di Azure in Visual Studio
Visual Studio offre diverse opzioni per il debug dei servizi cloud e delle macchine virtuali di Azure.

## <a name="debug-your-cloud-service-on-your-local-computer"></a>Eseguire il debug del servizio cloud sul computer locale
È possibile risparmiare tempo e denaro utilizzando toodebug emulatore di calcolo di Azure hello il servizio cloud in un computer locale. Eseguendo il debug di un servizio in locale prima della distribuzione, è possibile migliorare l'affidabilità e le prestazioni senza pagare per il tempo di calcolo. Tuttavia, potrebbero verificarsi alcuni errori solo quando si esegue un servizio cloud in Azure stesso. È possibile eseguire il debug di questi errori se si abilita il debug remoto quando si pubblica il servizio e quindi collega l'istanza del ruolo tooa debugger hello.

emulatore Hello simula il servizio di calcolo di Azure hello e viene eseguito nell'ambiente locale, eseguire il test e debug del servizio cloud prima di distribuirlo. gli handle di emulatore Hello hello del ciclo di vita delle istanze del ruolo e fornisce l'accesso alle risorse toosimulated, ad esempio l'archiviazione locale. Durante il debug o esegue il servizio da Visual Studio, automaticamente avvia emulatore hello come un'applicazione in background e quindi distribuisce l'emulatore toohello del servizio. È possibile utilizzare il servizio hello emulatore tooview quando viene eseguito nell'ambiente locale hello. È possibile eseguire hello versione o hello express dell'emulatore hello. (A partire da Azure 2.3, hello versione express dell'emulatore hello è predefinito hello.) Vedere [tooRun uso di Emulator Express ed eseguire il Debug locale di un servizio Cloud](https://msdn.microsoft.com/library/dn339018.aspx).

### <a name="toodebug-your-cloud-service-on-your-local-computer"></a>toodebug del servizio cloud nel computer locale
1. Nella barra dei menu hello, scegliere **Debug**, **Avvia debug** toorun il progetto servizio cloud di Azure. In alternativa, è possibile premere F5. Verrà visualizzato un messaggio hello emulatore di calcolo di avvio. Quando viene avviato l'emulatore hello, icona della barra delle applicazioni hello viene confermata.

    ![Emulatore Azure nella barra delle applicazioni hello](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC783828.png)
2. Visualizzare l'interfaccia utente di hello hello emulatore di calcolo aprendo il menu di scelta rapida hello hello Azure icona nell'area di notifica hello e quindi selezionare **Mostra interfaccia utente di emulatore di calcolo**.

    riquadro di sinistra Hello di hello dell'interfaccia utente mostra hello i servizi attualmente distribuiti toohello calcolo emulatore e hello istanze del ruolo che ogni servizio è in esecuzione. È possibile scegliere hello servizio o i ruoli toodisplay ciclo di vita, informazioni di diagnostica e sulla registrazione nel riquadro di destra hello. Se si seleziona hello sul margine superiore di una finestra inclusa hello, espande toofill riquadro di destra hello.
3. Passaggio a un'applicazione hello selezionando i comandi hello **Debug** menu e l'impostazione di punti di interruzione nel codice. Mentre si procede attraverso un'applicazione hello nel debugger hello, riquadri hello vengono aggiornati con lo stato corrente di hello di un'applicazione hello. Quando si arresta il debug, la distribuzione di applicazioni hello viene eliminata. Se l'applicazione include un ruolo web e browser web hello avvio azione proprietà toostart hello impostati, Visual Studio avvia l'applicazione web nel browser hello. Se si modifica il numero di hello di istanze di un ruolo nella configurazione del servizio hello, è necessario arrestare il servizio cloud e quindi riavviare il debug in modo che è possibile eseguire il debug di queste nuove istanze del ruolo hello.

    **Nota:** quando si arresta l'esecuzione o di debug del servizio, hello emulatore di calcolo locale e l'emulatore di archiviazione non vengono arrestati. È necessario arrestarli in modo esplicito dall'area di notifica hello.

## <a name="debug-a-cloud-service-in-azure"></a>Debug di un servizio cloud in Azure
toodebug un servizio cloud da un computer remoto, è necessario abilitare tale funzionalità in modo esplicito quando si distribuisce il servizio cloud in modo che sia necessario (ad esempio msvsmon.exe) siano installati nelle macchine virtuali hello che eseguono le istanze del ruolo. Se si non abilita il debug remoto quando il servizio di hello è pubblicato, è necessario servizio hello toorepublish con il debug remoto abilitato.

Se si abilita il debug remoto per un servizio cloud, esso non produce una riduzione delle prestazioni o costi aggiuntivi. È consigliabile utilizzare il debug remoto in un servizio di produzione, perché i client che utilizzano il servizio hello potrebbero essere influenzati negativamente.

> [!NOTE]
> Quando si pubblica un servizio cloud da Visual Studio, è possibile abilitare **IntelliTrace** per i ruoli in cui tale hello di destinazione .NET Framework 4 del servizio o hello .NET Framework 4.5. Utilizzando **IntelliTrace**, è possibile esaminare gli eventi generati in un'istanza del ruolo in hello precedente e riprodurre il contesto di hello da quel momento. Vedere [Debug di un servizio cloud pubblicato con IntelliTrace e Visual Studio](http://go.microsoft.com/fwlink/?LinkID=623016) e [Uso di IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx).
>
>

### <a name="tooenable-remote-debugging-for-a-cloud-service"></a>tooenable il debug remoto per un servizio cloud
1. Aprire il menu di scelta rapida hello per hello progetto Azure e quindi selezionare **pubblica**.
2. Seleziona hello **gestione temporanea** ambiente e hello **Debug** configurazione.

    Questa è solo un'indicazione. È possibile scegliere toorun gli ambienti di test in un ambiente di produzione. Tuttavia, possono verificarsi effetti negativi utenti se si abilita il debug remoto nell'ambiente di produzione hello. È possibile scegliere la configurazione di rilascio hello, ma la configurazione di Debug hello effettua il debug.

    ![Scegliere la configurazione di Debug hello](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746717.gif)
3. Attenersi alla procedura consueta hello, ma seleziona hello **Abilita Debugger remoto per tutti i ruoli** casella di controllo hello **impostazioni avanzate** scheda.

    ![Configurazione di debug](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746718.gif)

### <a name="tooattach-hello-debugger-tooa-cloud-service-in-azure"></a>servizio cloud in Azure tooattach hello debugger tooa
1. In Esplora Server, espandere il nodo di hello per il servizio cloud.
2. Menu di scelta rapida aprire hello ruolo hello o un ruolo istanza toowhich tooattach desiderato e quindi selezionare **collega Debugger**.

    Se si esegue il debug di un ruolo, il debugger di Visual Studio hello collega tooeach istanza di tale ruolo. Hello debugger verrà interrotta in un punto di interruzione per hello prima istanza del ruolo che esegue la riga di codice e soddisfa le condizioni del punto di interruzione. Se si esegue il debug di un'istanza, il debugger hello collega tooonly che l'istanza e si interrompe in un punto di interruzione solo se quell ' istanza esegue la riga di codice e soddisfa hello condizioni del punto di interruzione.

    ![Collega debugger](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746719.gif)
3. Dopo che il debugger hello Allega tooan istanza, eseguire il debug come di consueto. debugger Hello Collega automaticamente toohello di processo host appropriato per il ruolo. A seconda di quale hello è ruolo hello debugger collega toow3wp.exe, WaWorkerHost.exe o WaIISHost.exe. tooverify hello processo toowhich hello del debugger, espandere il nodo istanza hello in Esplora Server. Vedere [Architettura del ruolo di Azure](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx) per altre informazioni sui processi di Azure.

    ![Finestra di dialogo Seleziona tipo di codice](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
4. i processi di hello tooidentify toowhich hello del debugger, aprire hello processi finestra di dialogo in hello barra dei menu, scegliere Debug, Windows, i processi. (Tastiera: Ctrl + Alt + Z) toodetach un processo specifico, aprire il menu di scelta rapida e quindi selezionare **Disconnetti processo**. In alternativa, individuare il nodo di istanza hello in Esplora Server, trovare il processo di hello, aprire il menu di scelta rapida e quindi **Disconnetti processo**.

    ![Debug di processi](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC690787.gif)

> [!WARNING]
> Evitare interruzioni prolungate in corrispondenza dei punti di interruzione durante il debug remoto. Azure considera un processo che è stato arrestato per più di pochi minuti come non risponde e interrompe l'invio di istanza toothat di traffico. Se si arresta dura troppo, msvsmon.exe si disconnette dal processo di hello.
>
>

il debugger hello toodetach da tutti i processi in cui l'istanza o un ruolo, un menu di scelta rapida aprire hello hello ruolo o l'istanza che si sta eseguendo il debug e quindi selezionare **scollegare Debugger**.

## <a name="limitations-of-remote-debugging-in-azure"></a>Limitazioni del debug remoto in Azure
Da Azure SDK 2.3, il debug remoto presenta hello limitazioni seguenti.

* Con il debug remoto abilitato, non è possibile pubblicare un servizio cloud in cui un ruolo contiene più di 25 istanze.
* debugger Hello utilizza porte 30400 too30424, too31424 31400 e too32424 32400. Se si prova toouse qualsiasi di queste porte, non sarà in grado di toopublish il servizio e uno dei seguenti messaggi di errore hello verranno visualizzati nel registro attività hello per Azure:

  * Errore durante la convalida il file con estensione cscfg hello in file con estensione csdef hello.
    Hello riservato 'intervallo' intervallo di porte per l'endpoint che remotedebugger del 'ruolo del ruolo' si sovrappone a una porta già definita o un intervallo.
  * Allocazione non riuscita. Riprovare più tardi, provare a ridurre hello dimensioni della macchina virtuale o un numero di istanze del ruolo oppure provare a distribuire tooa diversa area.

## <a name="debugging-azure-virtual-machines"></a>Debug di macchine virtuali di Azure
È possibile eseguire il debug di programmi in esecuzione su macchine virtuali di Azure tramite Esplora server in Visual Studio. Quando si abilita il debug remoto in una macchina virtuale di Azure, estensione di debug remoto hello viene installata nella macchina virtuale hello. Quindi, è possibile collegare tooprocesses sulla macchina virtuale hello e debug come di consueto.

> [!NOTE]
> Macchine virtuali create dallo stack di hello Azure resource manager può essere eseguite in modalità remota da tramite Cloud Explorer in Visual Studio 2015. Per altre informazioni, vedere [Gestione delle risorse di Azure con Cloud Explorer](http://go.microsoft.com/fwlink/?LinkId=623031).
>
>

### <a name="toodebug-an-azure-virtual-machine"></a>toodebug una macchina virtuale di Azure
1. In Esplora Server, espandere i nodi di macchine virtuali hello e selezionare hello della macchina virtuale hello che si desidera toodebug.
2. Aprire il menu di scelta rapida hello e selezionare **Attiva debug**. Quando viene richiesto se si è certi se si desidera tooenable debug in hello macchina virtuale, seleziona **Sì**.

    Verrà installata l'estensione di debug remoto hello hello macchina virtuale tooenable debug.

    ![Comando di debug di abilitazione della macchina virtuale](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Finestra Log attività di Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
3. Dopo l'estensione di debug remoto hello al termine dell'installazione, aprire il menu di scelta rapida della macchina virtuale hello e selezionare **collega Debugger...**

    Azure Ottiene un elenco di processi hello nella macchina virtuale hello e li visualizza nella finestra di dialogo tooProcess Connetti hello.

    ![Comando Collega debugger](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
4. In hello **allegare tooProcess** nella finestra di dialogo **selezionare** elenco dei risultati di hello toolimit tooshow solo i tipi di hello del codice desiderato toodebug. È possibile eseguire il debug di codice gestito, codice nativo o entrambi a 32 o 64 bit.

    ![Finestra di dialogo Seleziona tipo di codice](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
5. Selezionare i processi di hello toodebug sulla macchina virtuale hello desiderato e quindi selezionare **collegamento**. Ad esempio, è possibile scegliere processo w3wp.exe hello se si desidera che un'app web nella macchina virtuale hello toodebug. Per altre informazioni, vedere [Debug di uno o più processi in Visual Studio](https://msdn.microsoft.com/library/jj919165.aspx) e [Architettura del ruolo di Azure](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx).

## <a name="create-a-web-project-and-a-virtual-machine-for-debugging"></a>Creare un progetto Web e una macchina virtuale per il debug
Prima di pubblicare il progetto Azure, può risultare utile tootest in un ambiente indipendente che supporta il debug e gli scenari di test e in cui è possibile installare i test e i programmi di controllo. Un modo toodo si tratta di tooremotely debug dell'app in una macchina virtuale.

Progetti di Visual Studio ASP.NET offrono un'opzione toocreate una pratica macchina virtuale che è possibile utilizzare per il test di app. macchina virtuale Hello include endpoint solitamente necessari, ad esempio PowerShell, desktop remoto e WebDeploy.

### <a name="toocreate-a-web-project-and-a-virtual-machine-for-debugging"></a>toocreate un progetto web e una macchina virtuale per il debug
1. Creare un'applicazione Web ASP.NET in Visual Studio.
2. Nella finestra di dialogo Nuovo progetto ASP.NET di hello, nella sezione di Azure, hello scegliere **macchina virtuale** nella casella di riepilogo a discesa hello. Lasciare hello **crea risorse remote** casella di controllo selezionata. Selezionare **OK** tooproceed.

    Hello **crea macchina virtuale in Azure** viene visualizzata la finestra di dialogo.

    ![Finestra di dialogo Crea progetto Web ASP.NET](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746723.png)

    **Nota:** verrà chiesto toosign in tooyour account Azure se non è già stato eseguito.

1. Selezionare varie impostazioni per la macchina virtuale hello hello e quindi selezionare **OK**. Per altre informazioni, vedere [Macchine virtuali](http://go.microsoft.com/fwlink/?LinkId=623033) .

    nome Hello che immesso come nome DNS sarà il nome di hello della macchina virtuale hello.

    ![Finestra di dialogo Crea macchina virtuale di Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746724.png)

    Azure crea macchina virtuale hello e quindi esegue il provisioning e configura l'endpoint di hello, ad esempio Desktop remoto e distribuzione Web
2. Dopo aver hello è configurata completamente la macchina virtuale, selezionare il nodo della macchina virtuale hello in Esplora Server.
3. Aprire il menu di scelta rapida hello e selezionare **Attiva debug**. Quando viene richiesto se si è certi se si desidera tooenable debug in hello macchina virtuale, seleziona **Sì**.

    Azure installa hello debug estensione toohello macchina virtuale tooenable debug remoto.

    ![Comando di debug di abilitazione della macchina virtuale](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Finestra Log attività di Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
4. Pubblicare il progetto come descritto in [Procedura: Distribuire un progetto Web tramite la pubblicazione con un clic in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx). Poiché si desidera toodebug nella macchina virtuale hello in hello **impostazioni** pagina di hello **pubblica sul Web** procedura guidata, selezionare **Debug** come configurazione hello. Ciò assicura che i simboli del codice siano disponibili durante il debug.

    ![Impostazioni di pubblicazione](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718349.png)
5. In hello **Opzioni pubblicazione File**selezionare **Rimuovi file aggiuntivi nella destinazione** se il progetto hello è già stato distribuito in un momento precedente.
6. Dopo la pubblicazione del progetto hello, nel menu di scelta rapida della macchina virtuale hello in Esplora Server, selezionare **collega Debugger...**

    Azure Ottiene un elenco di processi hello nella macchina virtuale hello e li visualizza nella finestra di dialogo tooProcess Connetti hello.

    ![Comando Collega debugger](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
7. In hello **allegare tooProcess** nella finestra di dialogo **selezionare** elenco dei risultati di hello toolimit tooshow solo i tipi di hello del codice desiderato toodebug. È possibile eseguire il debug di codice gestito, codice nativo o entrambi a 32 o 64 bit.

    ![Finestra di dialogo Seleziona tipo di codice](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
8. Selezionare i processi di hello toodebug sulla macchina virtuale hello desiderato e quindi selezionare **collegamento**. Ad esempio, è possibile scegliere processo w3wp.exe hello se si desidera che un'app web nella macchina virtuale hello toodebug. Per altre informazioni, vedere [Debug di uno o più processi in Visual Studio](https://msdn.microsoft.com/library/jj919165.aspx) .

## <a name="next-steps"></a>Passaggi successivi
* Utilizzare **Intellitrace** toocollect un log di chiamate e gli eventi da un server di versione. Vedere [Debug di un servizio cloud pubblicato con IntelliTrace e Visual Studio](http://go.microsoft.com/fwlink/?LinkID=623016).
* Utilizzare **diagnostica Azure** toolog informazioni dall'esecuzione di codice all'interno di ruoli, ruoli hello esecuzione nell'ambiente di sviluppo hello o in Azure. Vedere [Raccogliere dati di registrazione usando Diagnostica di Azure](http://go.microsoft.com/fwlink/p/?LinkId=400450).
