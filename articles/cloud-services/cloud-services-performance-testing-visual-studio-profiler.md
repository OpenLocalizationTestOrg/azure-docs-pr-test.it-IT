---
title: un Cloud servizio localmente nell'emulatore di calcolo hello aaaProfiling | Documenti Microsoft
services: cloud-services
description: Analizzare i problemi di prestazioni nei servizi cloud con il profiler di Visual Studio hello
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
tags: 
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: fc37c85dad4db4cc0310f73afad56fc0fe5f3963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a>Test delle prestazioni di locale di un servizio Cloud hello in hello Azure Compute Emulator tramite hello Profiler di Visual Studio
Un'ampia gamma di strumenti e tecniche sono disponibili per il test delle prestazioni di hello dei servizi cloud.
Quando si pubblica un tooAzure servizio cloud, è possibile impostare Visual Studio raccogliere dati di profilatura e analizzarli in locale, come descritto in [profilatura di un'applicazione Azure][1].
È inoltre possibile utilizzare diagnostica tootrack contatori delle prestazioni diverse, come descritto in [mediante i contatori delle prestazioni in Azure][2].
È inoltre possibile tooprofile l'applicazione localmente nell'emulatore di calcolo hello prima della distribuzione cloud toohello.

Questo articolo descrive il metodo di campionamento CPU di hello di profilatura, che può essere eseguito localmente nell'emulatore hello. Si tratta di un metodo di profilatura non eccessivamente invasivo. In un intervallo di campionamento designato, il profiler hello accetta uno snapshot dello stack di chiamate hello. dati Hello vengono raccolti in un periodo di tempo e presenti in un report. Questo metodo di profilatura tende tooindicate in cui in un'applicazione con calcoli complessi la maggior parte del lavoro hello CPU viene eseguita.  In questo modo si hello toofocus opportunità tracciato hello"attivo" in cui l'applicazione sta impiegando hello la maggior parte di tempo.

## <a name="1-configure-visual-studio-for-profiling"></a>1: Configurare Visual Studio per la profilatura
Visual Studio include alcune opzioni di configurazione che possono risultare utili per la profilatura. senso toomake di hello i rapporti di profilatura, è necessario simboli (PDB) per l'applicazione e anche i simboli per le librerie di sistema. È opportuno assicurarsi di fare riferimento a server dei simboli disponibili hello toomake. toodo questo su hello **strumenti** menu in Visual Studio, scegliere **opzioni**, quindi scegliere **debug**, quindi **simboli**. Verificare che Server dei simboli Microsoft sia elencato in **Percorsi dei file di simboli (pdb)**.  È inoltre possibile fare riferimento a http://referencesource.microsoft.com/symbols, dove potrebbero essere disponibili file di simboli aggiuntivi.

![Opzioni dei simboli][4]

Se si desidera, è possibile semplificare hello segnala che il profiler hello genera impostando Just My Code. Con Just My Code attivata, gli stack di chiamate di funzione sono stati semplificati in modo che chiama toolibraries completamente interno e hello .NET Framework sono nascosti da report hello. In hello **strumenti** menu, scegliere **opzioni**. Espandere quindi hello **strumenti di prestazioni** nodo e scegliere **generale**. Selezionare una casella di controllo hello **Abilita Just My Code per i rapporti del profiler**.

![Opzioni di Just My Code][17]

Queste istruzioni sono applicabili a un progetto esistente o a un nuovo progetto.  Se si crea un nuovo hello tootry progetto tecniche descritte di seguito, scegliere c# **servizio Cloud di Azure** del progetto e selezionare un **ruolo Web** e un **ruolo di lavoro**.

![Ruoli del progetto Servizi cloud di Azure][5]

Scopi, ad esempio aggiungere un progetto di codice tooyour che richiede molto tempo e illustra alcuni problemi di prestazioni ovvio. Ad esempio, aggiungere hello progetto ruolo di lavoro tooa di codice seguente:

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

Chiamare il codice da hello RunAsync metodo nella classe derivata da RoleEntryPoint del ruolo di lavoro hello. (Ignora avviso hello sul metodo hello in esecuzione in modo sincrono).

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

Compilare ed eseguire il servizio cloud in locale senza eseguire debug (Ctrl + F5), con la configurazione della soluzione hello impostato troppo**versione**. Ciò garantisce che tutti i file e cartelle vengono create per l'esecuzione di un'applicazione hello in locale e assicura che tutti gli emulatori di hello siano avviati. Avviare hello interfaccia utente dell'emulatore di calcolo da hello barra delle applicazioni tooverify che esegue il ruolo di lavoro.

## <a name="2-attach-tooa-process"></a>2: connessione del processo tooa
Anziché un'applicazione hello avviandolo hello IDE di Visual Studio 2010, è necessario collegare hello profiler tooa esecuzione processo. 

tooattach hello profiler tooa processo, di hello **Analizza** menu, scegliere **Profiler** e **collegamento/scollegamento**.

![Opzione per il collegamento del profilo][6]

Per un ruolo di lavoro, trovare il processo di WaWorkerHost.exe hello.

![Processo WaWorkerHost][7]

Se la cartella di progetto è un'unità di rete, il profiler hello chiederà tooprovide hello di toosave percorso un altro report per la profilatura.

 È inoltre possibile allegare il ruolo web tooa collegando tooWaIISHost.exe.
Se sono presenti più processi di ruolo di lavoro nell'applicazione, è necessario toouse hello processID toodistinguish li. È possibile eseguire query a livello di codice hello processID accedendo all'oggetto processo hello. Ad esempio, se si aggiunge questo metodo di esecuzione di codice toohello della classe derivata RoleEntryPoint hello in un ruolo, è possibile esaminare il log hello tooknow di interfaccia utente dell'emulatore di calcolo tooconnect il processo di.

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

log di hello tooview, hello avvio dell'interfaccia utente emulatore di calcolo.

![Avviare hello interfaccia utente dell'emulatore di calcolo][8]

Aprire la finestra console hello lavoro ruolo log in hello interfaccia utente dell'emulatore di calcolo facendo clic sulla barra del titolo della finestra di console hello. È possibile visualizzare l'ID del processo nel registro hello hello.

![Visualizzare l'ID processo][9]

È stata associata, una procedura hello nello scenario di hello tooreproduce dell'interfaccia utente (se necessario) dell'applicazione.

Quando si desidera toostop profilatura, scegliere hello **arrestare profilatura** collegamento.

![Opzione Arresta profilatura][10]

## <a name="3-view-performance-reports"></a>3: Visualizzare i rapporti relativi alle prestazioni
report prestazioni Hello per l'applicazione viene visualizzato.

A questo punto, hello profiler interrompe l'esecuzione, Salva i dati in un file con estensione vsp e consente di visualizzare un report contenente un'analisi dei dati.

![Report del profiler][11]

Se viene visualizzato String.wstrcpy in hello percorso ricorrente, fare clic su hello toochange Just My Code consente di visualizzare tooshow solo codice utente.  Se String. Concat, provare a pulsante Mostra tutto il codice hello.

Si dovrebbe essere metodo Concatenate hello e String. Concat occupando gran parte del tempo di esecuzione hello.

![Analisi del report][12]

Se è stato aggiunto codice concatenazione di stringa hello in questo articolo, si verrà visualizzato un avviso in hello elenco attività per questo oggetto. È inoltre possibile visualizzare un avviso che vi sia una quantità eccessiva di garbage collection, ovvero a causa di toohello numero di stringhe che vengono creati ed eliminato.

![Avvisi di prestazioni][14]

## <a name="4-make-changes-and-compare-performance"></a>4: Apportare modifiche e confrontare le prestazioni
È inoltre possibile confrontare le prestazioni di hello prima e dopo una modifica del codice.  Arresta esecuzione processo hello e modificare hello codice tooreplace hello stringa operazione di concatenazione con utilizzo hello di StringBuilder:

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

Eseguire un'altra esecuzione sulle prestazioni e quindi confrontare le prestazioni di hello. In Esplora prestazioni hello, se hello esecuzioni sono in hello stessa sessione, è solo possibile selezionare entrambi i report, aprire il menu di scelta rapida hello e scegliere **Confronta report di prestazioni**. Se si desidera toocompare con un'esecuzione in un'altra sessione di prestazioni, aprire hello **Analizza** menu, scegliere **Confronta report di prestazioni**. Specificare entrambi i file nella finestra di dialogo hello visualizzata.

![Opzione Confronta report di prestazioni][15]

i report di Hello evidenziare le differenze tra due esecuzioni hello.

![Report di confronto][16]

Congratulazioni. È stato avviato con il profiler di hello.

## <a name="troubleshooting"></a>Risoluzione dei problemi
* Assicurarsi di eseguire la profilatura di una compilazione di rilascio e avviarla senza eseguire il debug.
* Se l'opzione di collegamento/scollegamento hello non è abilitato nel menu di Profiler hello, eseguire hello procedura guidata.
* Utilizzare hello interfaccia utente dell'emulatore di calcolo tooview hello lo stato dell'applicazione. 
* Se si verificano problemi durante l'avvio delle applicazioni nell'emulatore hello o associare hello profiler, arrestare l'emulatore di calcolo hello e riavviarlo. Se non viene risolto il problema di hello, provare a riavviare. Questo problema può verificarsi se si utilizza toosuspend emulatore di calcolo hello e rimuovere le distribuzioni in esecuzione.
* Se è stato utilizzato uno dei comandi dalla riga di comando di profilatura hello, soprattutto hello impostazioni globali, assicurarsi che sia stato chiamato VSPerfClrEnv /globaloff e che VsPerfMon.exe è stato arrestato.
* Se durante il campionamento, viene visualizzato il messaggio hello "PRF0025: è stato raccolto alcun dato," verificare che hello processo allegato attività toohas della CPU. È possibile che le applicazioni che non eseguono attività di calcolo non producano dati di campionamento.  È anche possibile hello terminata prima che qualsiasi campionamento è stato eseguito. Controllare toosee che non termina il metodo Run hello per un ruolo che si esegue la profilatura.

## <a name="next-steps"></a>Passaggi successivi
Strumentazione di binari Azure nell'emulatore hello non è supportata nel profiler di Visual Studio hello, ma se si desidera tootest l'allocazione della memoria, è possibile selezionare l'opzione durante l'analisi. È anche possibile scegliere la profilatura della concorrenza, che consente di determinare se sono un inutile consumo di thread concorrenti ora per i blocchi o profilatura di interazione tra livelli consente di tenere traccia dei problemi di prestazioni durante l'interazione tra livelli di un'applicazione, più spesso tra il livello di dati hello e un ruolo di lavoro.  È possibile visualizzare le query di database hello che genera l'app e usare hello l'utilizzo del database hello tooimprove dati di profilatura. Per informazioni sulla profilatura interazione tra livelli, vedere hello post di blog [procedura dettagliata: utilizzo di Profiler di interazione tra livelli in Visual Studio Team System 2010 hello][3].

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png
