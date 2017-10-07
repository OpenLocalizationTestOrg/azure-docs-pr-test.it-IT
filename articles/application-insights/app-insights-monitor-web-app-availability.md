---
title: "aaaMonitor disponibilità e tempi di risposta di qualsiasi sito web | Documenti Microsoft"
description: Configurare i test Web in Application Insights. Ottenere avvisi se un sito Web diventa non disponibile o risponde lentamente.
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 46dc13b4-eb2e-4142-a21c-94a156f760ee
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: bwren
ms.openlocfilehash: 4c5425c948770cc57a648ca50e217c75ac75fbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-availability-and-responsiveness-of-any-web-site"></a>Monitorare la disponibilità e la velocità di risposta dei siti Web
Dopo aver distribuito l'app web o il sito web tooany server, è possibile impostare toomonitor test disponibilità e della velocità di risposta. [Azure Application Insights](app-insights-overview.md) invia le richieste web applicazione tooyour a intervalli regolari dai punti di tutto il mondo hello. Invia avvisi all'utente nel caso in cui l'applicazione risponda lentamente o non risponda affatto.

È possibile impostare i test di disponibilità per qualsiasi HTTP o hello di endpoint HTTPS accessibile dalla rete internet pubblica. Non è necessario tooadd qualsiasi sito web toohello che si sta testando. Anche non ha toobe del sito: è possibile testare un servizio API REST da cui dipendono.

Sono disponibili due tipi di test di disponibilità:

* [Test di ping URL](#create): un test semplice che è possibile creare nel portale di Azure hello.
* [Test web multipassaggio](#multi-step-web-tests): creato in Visual Studio Enterprise portal toohello di caricamento.

È possibile creare i test di disponibilità too25 per ogni risorsa dell'applicazione.

## <a name="create"></a>1. Aprire una risorsa per i report dei test di disponibilità

**Se è già stato configurato Application Insights** per l'app web, aprire la risorsa di Application Insights in hello [portale di Azure](https://portal.azure.com).

**Oppure, se si desidera toosee dei report in una nuova risorsa** iscriversi troppo[Microsoft Azure](http://azure.com), visitare toohello [portale di Azure](https://portal.azure.com)e creare una risorsa di Application Insights.

![New > Application Insights](./media/app-insights-monitor-web-app-availability/11-new-app.png)

Fare clic su **tutte le risorse** pannello della panoramica tooopen hello per le nuove risorse hello.

## <a name="setup"></a>2. Creare un test di ping URL
Aprire il pannello di disponibilità hello e aggiungere un test.

![Riempimento hello almeno l'URL del sito Web](./media/app-insights-monitor-web-app-availability/13-availability.png)

* **URL di Hello** può essere una pagina web si desidera tootest, ma deve essere visibile da hello rete internet pubblica. URL di Hello può includere una stringa di query. In questo modo, ad esempio, è possibile esercitarsi nell'uso del database. Se l'URL hello risolve tooa reindirizzamento, è seguire i reindirizzamenti too10.
* **Analizzare le richieste dipendenti**: se questa opzione è selezionata, il test di hello richiede immagini, script, file di tipo e altri file che fanno parte della pagina web hello sottoposta a test. Hello tempi di risposta registrato includono hello scattato tooget questi file. test di Hello non riesce se tutte le risorse non possono essere scaricate entro il timeout di hello per intero test hello. 

    Se non è selezionata l'opzione hello, test hello richiede solo file hello hello URL specificato.
* **Consentire tentativi**: se questa opzione è selezionata, hello test ha esito negativo, si è eseguito un nuovo tentativo dopo un breve intervallo. Un errore viene segnalato solo se tre tentativi successivi non riescono. I test successivi vengono quindi eseguiti con una frequenza di test consuete hello. Riprova è temporaneamente sospesa fino al completamento di hello successivo. Questa regola viene applicata in modo indipendente in ogni località di test. Questa opzione è consigliata. In media, circa l'80% degli errori non si ripresenta al nuovo tentativo.
* **Frequenza di test**: imposta la frequenza con cui hello test viene eseguito da ogni posizione di test. Con una frequenza di cinque minuti e cinque località di test, il sito verrà testato in media ogni minuto.
* **Posizioni di test** sono hello colloca in cui il server invia URL tooyour di richieste web. Sceglierne più di una, per poter distinguere i problemi del sito Web dai problemi di rete. È possibile selezionare le destinazioni di too16.
* **Criteri di successo**:

    **Timeout di prova**: ridurre il valore toobe generato un avviso per una risposta lenta. test di Hello viene conteggiato come un errore se le risposte hello del sito non sono state ricevute entro questo periodo. Se si seleziona **analizzare le richieste dipendenti**, quindi hello tutte le immagini, file di stile, script e altre risorse dipendenti sono stati ricevuti entro questo periodo.

    **Risposta HTTP**: hello ha restituito il codice di stato che viene conteggiato come un caso di esito positivo. 200 è codice hello che indica che una pagina web normale è stato restituito.

    **Il contenuto corrisponde a**: stringa, ad esempio "Benvenuto", Verifichiamo che in ogni risposta ci una corrispondenza esatta di maiuscolo e minuscolo. Deve trattarsi di una stringa di testo normale, senza caratteri jolly. Non dimenticare che, se le modifiche di contenuto della pagina potrebbe essere tooupdate è.
* **Avvisi** , per impostazione predefinita, inviati tooyou se sono presenti errori in tre posizioni più di cinque minuti. È di un errore in un'unica posizione, probabilmente toobe un problema di rete e non è un problema con il sito. Ma è possibile modificare hello soglia toobe più o meno sensibili ed è possibile inoltre modifica chi ha hello messaggi di posta elettronica deve essere inviato.

    È possibile configurare un [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) che verrà chiamato quando viene generato un avviso. Si noti però che attualmente i parametri di query non vengono passati come proprietà.

### <a name="test-more-urls"></a>Testare più URL
Aggiungere altri test. Ad esempio, In aggiunta tootesting home page, è possibile verificare che il database è in esecuzione eseguendo i test hello URL per una ricerca.


## <a name="monitor"></a>3. Visualizzare i risultati del test di disponibilità

Dopo alcuni minuti, fare clic su **aggiornamento** toosee risultati dei test. 

![Risultati di riepilogo nel pannello principale hello](./media/app-insights-monitor-web-app-availability/14-availSummary-3.png)

Hello scatterplot vengono mostrati esempi di hello risultati dei test con i dettagli di diagnostica di passo del test. motore dei test hello archivia i dettagli relativi diagnostica per i test che sono stati rilevati errori. Per i test superati, di diagnostica viene archiviati per un subset di esecuzioni di hello. Passare il mouse su una qualsiasi delle hello punti verde/rosso toosee hello test timestamp, durata del test, percorso e nome del test. Fare clic su tramite qualsiasi punto nei dettagli hello dispersione tracciato toosee hello hello dei risultati di test.  

Selezionare un determinato test, percorso, o ridurre il tempo di hello toosee periodo ulteriori risultati intorno hello periodo di tempo di interesse. Utilizzare Esplora ricerche toosee risultati da tutte le esecuzioni o utilizzare report personalizzati di Analitica query toorun per i dati.

Nei risultati non elaborati toohello di addizione, esistono due metriche di disponibilità in Esplora metriche: 

1. Disponibilità: Percentuale di test hello che hanno avuto esito positivo, in tutte le esecuzioni di test. 
2. Durata test: durata media dei test rispetto a tutte le esecuzioni di test.

È possibile applicare filtri sul nome del test hello, le tendenze tooanalyze percorso di un determinato test e/o il percorso.

## <a name="edit"></a> Esaminare e modificare i test

Pagina Riepilogo hello, selezionare un test specifico. Sarà possibile visualizzarne i risultati specifici e modificarlo o disabilitarlo temporaneamente.

![Modificare o disabilitare un test Web](./media/app-insights-monitor-web-app-availability/19-availEdit-3.png)

È possibile toodisable disponibilità test o un avviso di hello regole associate mentre si esegue la manutenzione del servizio. 

## <a name="failures"></a>In caso di errori
Fare clic su un punto rosso.

![Click a red dot](./media/app-insights-monitor-web-app-availability/open-instance-3.png)


Dal risultato di un test di disponibilità è possibile eseguire le operazioni seguenti:

* Controllare risposta hello ricevuta dal server.
* Aprire i dati di telemetria hello inviati all'applicazione server durante l'elaborazione di istanza di hello richieste non riuscite.
* Elemento di lavoro problema di hello tootrack Git o Visual Studio Team Services o un problema. bug Hello conterrà un evento toothis di collegamento.
* Aprire il risultato del test web hello in Visual Studio.


*Ha un aspetto corretto ma è segnalato come errore?* Controllare tutte le immagini di hello, script, fogli di stile e qualsiasi altro file caricato dalla pagina hello. Se uno di essi ha esito negativo, prova hello viene segnalato come non riuscita, anche se una pagina html principale hello carica OK.

*Nessun elemento correlato?* Se Application Insights è configurato per l'applicazione lato server, il motivo può essere l'esecuzione del [campionamento](app-insights-sampling.md). 

## <a name="multi-step-web-tests"></a>Test Web in più passaggi
È possibile monitorare uno scenario che comporta una sequenza di URL. Ad esempio, se si sta monitorando un sito Web di vendita, è possibile verificare che l'aggiunta di elementi toohello carrello funziona correttamente.

> [!NOTE] 
> È prevista una tariffa per i test Web in più passaggi. Vedere lo [schema dei prezzi](http://azure.microsoft.com/pricing/details/application-insights/).
> 

toocreate un test di più passaggi, si registra scenario hello utilizzando Visual Studio Enterprise e quindi carica hello tooApplication informazioni di registrazione. Application Insights riproduce scenario hello a intervalli e verifica le risposte hello.

> [!NOTE]
> Non è possibile usare funzioni codificate o cicli nei test. test di Hello deve essere completamente contenuto in uno script di hello WebTest. È tuttavia possibile usare plug-in standard.
>

#### <a name="1-record-a-scenario"></a>1. Registrare uno scenario
Utilizzare Visual Studio Enterprise toorecord una sessione web.

1. Creare un progetto di test delle prestazioni Web.

    ![In Visual Studio Enterprise edition, creare un progetto dal modello di Test di carico e prestazioni Web hello.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-create.png)

 * *Non è visualizzato hello delle prestazioni Web e il modello di Test di carico?* chiudere Visual Studio Enterprise. Aprire **programma di installazione di Visual Studio** toomodify l'installazione di Visual Studio Enterprise. In **Singoli componenti** selezionare **Strumenti per test di carico e delle prestazioni Web**.

2. Apre file hello. WebTest e avviare la registrazione.

    ![Aprire file hello. WebTest e fare clic su Registra.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-start.png)
3. Hello desiderato toosimulate nel test di azioni dell'utente: aprire il sito Web, aggiungere un carrello toohello prodotto e così via. Quindi, arrestare il test.

    ![esecuzione di registrazione dei test web Hello in Internet Explorer.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-record.png)

    Non creare uno scenario lungo, in quanto è presente un limite di 100 passaggi e 2 minuti.
4. Modifica del test hello:

   * Aggiungere le convalide toocheck hello ricevuto testo e risposta codici.
   * Rimuovere tutte le interazioni superflue. È anche possibile rimuovere le richieste dipendenti per le immagini o tooad o siti di rilevamento.

     Tenere presente che è possibile modificare solo script di test hello - non è possibile aggiungere codice personalizzato o chiamare altri test web. Non inserire i cicli nel test hello. È possibile utilizzare i plug-in del test web standard.
5. Eseguire test hello in Visual Studio toomake verificarne che il funzionamento.

    un web browser verrà visualizzato Hello web test runner e si ripete hello azioni registrate. Verificare che funzioni come previsto.

    ![In Visual Studio, aprire il file webtest hello e fare clic su Esegui.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-run.png)

#### <a name="2-upload-hello-web-test-tooapplication-insights"></a>2. Caricare hello web test tooApplication Insights
1. Nel portale Application Insights hello, creare un test web.

    ![Nel Pannello di test web hello, scegliere Aggiungi.](./media/app-insights-monitor-web-app-availability/16-another-test.png)
2. Selezionare il test di più passaggi e caricare il file hello. WebTest.

    ![Selezionare Test Web in più passaggi.](./media/app-insights-monitor-web-app-availability/appinsights-71webtestUpload.png)

    Posizioni di test hello set, frequenza e parametri di avviso in hello stesso modo per ping verifica.

#### <a name="3-see-hello-results"></a>3. Visualizzare i risultati di hello

Visualizzare il test di risultati e gli eventuali errori in hello stesso modo come url singolo test.

Inoltre, è possibile scaricare tooview risultati test di hello usarle in Visual Studio.

#### <a name="too-many-failures"></a>Numero di errori elevato

* Una causa comune di errore è che il test hello dura troppo a lungo. L'esecuzione non deve superare i due minuti.

* Non dimenticare che tutte le risorse di hello di una pagina è necessario caricare correttamente per hello test toosucceed, inclusi script, fogli di stile, immagini e così via.

* Hello test web deve essere contenuto interamente in script WebTest hello: non è possibile utilizzare funzioni codificate nel test hello.

### <a name="plugging-time-and-random-numbers-into-your-multi-step-test"></a>Inserimento di plug-in relativi a tempo e numeri casuali nel test in più passaggi
Si supponga di voler testare uno strumento che riceva dati dipendenti dal tempo, come ad esempio valori di scorte da un feed esterno. Quando si registra il test web, sono toouse orari, ma si impostano come testare i parametri di hello, StartTime ed EndTime.

![Un test Web con parametri.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-parameters.png)

Quando si esegue il test di hello, desideri toobe hello presentano sempre ora EndTime e StartTime deve essere di 15 minuti fa.

Plug-in Test Web forniscono il modo di hello toodo parametrizzare volte.

1. Aggiungere un plug-in del test Web per ciascun valore di parametro desiderato. Nella barra degli strumenti test hello web, scegliere **aggiungere plug-in Test Web**.

    ![Scegliere Aggiungi plug-in test Web e selezionare un tipo.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugins.png)

    In questo esempio, si usa due istanze di hello plug-in fase di Data. una per "15 minuti fa" e l'altra per "ora".
2. Aprire le proprietà di hello di ogni plug-in. Assegnare un nome e impostarlo hello toouse ora corrente. Per uno di essi, impostare Aggiungi minuti = -15.

    ![Set name, Use Current Time e Add Minutes.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-parameters.png)
3. Nei parametri di test web hello, utilizzare {{plug-in name}} tooreference un nome del plug-in.

    ![Nel parametro di test hello, utilizzare {{plug-in name}}.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-name.png)

A questo punto, caricare il portale toohello del test. Usa i valori dinamici hello in ogni fase di esecuzione del test di hello.

## <a name="dealing-with-sign-in"></a>Gestione degli accessi
Se gli utenti accedono tooyour app, si sono disponibili varie opzioni per la simulazione di accesso in modo da poter testare pagine Accedi hello. Hello sia l'approccio utilizzato dipende dal tipo di hello di sicurezza fornito da app hello.

In tutti i casi, è necessario creare un account nell'applicazione solo a scopo di hello del test. Se possibile, limitare le autorizzazioni di hello di questo account di test in modo che non vi è alcuna possibilità di test web hello che interessano gli utenti reali.

### <a name="simple-username-and-password"></a>Nome utente e password semplici
Registrare un test web in hello come di consueto. Eliminare prima di tutto i cookie.

### <a name="saml-authentication"></a>SAML Authentication
Utilizzare i plug-in SAML hello che è disponibile per i test web.

### <a name="client-secret"></a>Segreto client
Se l'app ha un percorso di accesso che prevede un segreto client, usare tale percorso. Un servizio che offre l'accesso con segreto client è ad esempio Azure Active Directory (AAD). In AAD, segreto client hello è hello chiave dell'applicazione.

Ecco un test Web di esempio di un'app Web di Azure che usa una chiave dell'app:

![Esempio di segreto client](./media/app-insights-monitor-web-app-availability/110.png)

1. Ottenere il token da AAD usando il segreto client (AppKey).
2. Estrarre il token di connessione dalla risposta.
3. Chiamare API usando il token di connessione nell'intestazione di autorizzazione hello.

Assicurarsi che i test web hello è un client effettivo, che dispone di un'app in Azure ad - e utilizzare il clientId + appkey. Sottoposta a test è anche un'app in AAD: hello appID URI di questa app viene riflessa nel test web hello nel campo "resource" hello.

### <a name="open-authentication"></a>Autenticazione aperta
Un esempio di autenticazione aperta è l'accesso con il proprio account Microsoft o Google. Molte applicazioni che utilizzano OAuth fornire hello alternativa segreto client, pertanto la prima strategia dovrebbe essere tooinvestigate il possibilità.

Se il test sarà necessario accedere con OAuth, l'approccio generale hello è:

* Utilizzare uno strumento come il traffico di hello Fiddler tooexamine tra web browser, il sito di autenticazione hello e app.
* Eseguire due o più accessi computer diversi o browser, o a intervalli di tempo (tooallow token tooexpire).
* Tramite il confronto tra sessioni diverse, identificare token hello restituiti da hello l'autenticazione del sito, che viene quindi passato server app tooyour dopo l'accesso.
* Registrare un test Web usando Visual Studio.
* Parametrizzare token hello, impostando il parametro hello quando il token hello viene restituito da autenticatore hello e utilizzarla nel sito di toohello query hello.
  (Visual Studio tenta test hello tooparameterize, ma non correttamente parametrizzare token hello.)


## <a name="performance-tests"></a>Test delle prestazioni
È possibile eseguire un test di carico nel sito Web. Come test di disponibilità hello, è possibile inviare le richieste semplici o più passaggi richieste dai nostri punti tutto il mondo hello. A differenza dei test di disponibilità, vengono inviate molte richieste, simulando più utenti simultanei.

Dal pannello della panoramica hello, aprire **impostazioni**, **test delle prestazioni**. Quando si crea un test, si è stati invitati tooconnect tooor creare un account di Visual Studio Team Services.

Una volta completato il test di hello, vengono visualizzati i tempi di risposta e percentuali di successo.


![Test delle prestazioni](./media/app-insights-monitor-web-app-availability/perf-test.png)

> [!TIP]
> effetti hello tooobserve di un test delle prestazioni, utilizzare [flusso Live](app-insights-live-stream.md) e [Profiler](app-insights-profiler.md).
>

## <a name="automation"></a>Automazione
* [Utilizzare tooset gli script di PowerShell di un test di disponibilità](app-insights-powershell.md#add-an-availability-test) automaticamente.
* Configurare un [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) che verrà chiamato quando viene generato un avviso.

## <a name="qna"></a>Domande? Problemi?
* *È possibile chiamare codice da un test Web?*

    No. passaggi di Hello del test di hello devono essere nel file hello. WebTest. Inoltre non è possibile chiamare altri test web o utilizzare cicli. Esistono diversi plug-in che potrebbero risultare utili.
* *HTTPS è supportato?*

    Sono supportati TLS 1.1 e TLS 1.2.
* *Esiste una differenza tra "test Web" e "test di disponibilità"?*

    Hello due termini è possibile fare riferimento in modo intercambiabile. Test di disponibilità è un termine più generico che comprende i ping di URL singolo hello verifica inoltre toohello multipassaggio web test.
* *Imposta come test di disponibilità toouse nel server interno che esegue un firewall.*

    Le soluzioni possono essere due:
    
    * Configurare il firewall toopermit le richieste in ingresso da hello [gli agenti di test di indirizzi IP dei nostri web](app-insights-ip-addresses.md).
    * Scrivere test tooperiodically codice server interno. Eseguire codice hello come un processo in background in un server di prova protetto da firewall. Il processo di test può inviare i risultati tooApplication Insights usando [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) API nel pacchetto di hello core SDK. Questo richiede il test toohave in uscita accesso toohello Application Insights inserimento endpoint del server, ma che è un quantità inferiore dei rischi di protezione di alternativa hello di consentire le richieste in ingresso. risultati di Hello non verranno visualizzati nei pannelli di test web disponibilità hello, ma viene visualizzato come risultati di disponibilità in Analitica, ricerca e metrica Explorer.
* *Non è possibile caricare un test Web in più passi*

    È previsto un limite di dimensioni pari a 300 KB.

    I cicli non sono supportati.

    I test web tooother riferimenti non sono supportati.

    Le origini dati non sono supportate.
* *Il test in più passi non viene completato*

    È previsto un limite di 100 richieste per ogni test.

    test di Hello viene arrestato se viene eseguito più di due minuti.
* *È possibile eseguire un test con certificati client?*

    Questa funzionalità non è supportata.


## <a name="next"></a>Passaggi successivi
[Ricerca nei registri di diagnostica][diagnostic]

[Risoluzione dei problemi][qna]

[Indirizzi IP degli agenti di test Web](app-insights-ip-addresses.md)

<!--Link references-->

[azure-availability]: ../insights-create-web-tests.md
[diagnostic]: app-insights-diagnostic-search.md
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
