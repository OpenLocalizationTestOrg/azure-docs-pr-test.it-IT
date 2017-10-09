---
title: modelli di navigazione aaaAnalyze utente con l'utente scorre in Azure Application Insights | Documenti Microsoft
description: "Analizzare la modalità di spostamento degli utenti tra pagine hello e le funzionalità dell'app web."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 08/02/2017
ms.author: cfreeman
ms.openlocfilehash: d3f35dc78e9874e4b7974604bf91c40a5e5b78eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-user-navigation-patterns-with-user-flows-in-application-insights"></a>Analizzare i modelli di spostamento degli utenti con Flussi utente in Application Insights

![Strumento Flussi utente di Application Insights](./media/app-insights-usage-flows/flows.png)

strumento utente scorre Hello Visualizza come utenti spostarsi tra pagine hello e le funzionalità del sito. È utile per rispondere a domande simili alle seguenti:
* In che modo gli utenti lasciano una pagina del sito?
* Su quali elementi di una pagina del sito fanno clic gli utenti?
* In cui sono hello inserisce che gli utenti varianza la maggior parte del sito?
* Quali sono le posizioni in cui gli utenti di ripetere l'operazione hello stessa azione ripetutamente?

strumento utente scorre Hello inizia da una visualizzazione di pagina iniziale o l'evento specificato. Questa visualizzazione pagina o un evento personalizzato, flussi di utente specificato. Mostra hello visualizzazioni pagina ed eventi personalizzati che gli utenti inviati immediatamente in un secondo momento durante una sessione, due i passaggi in seguito, e così via. Le linee di spessore variabile mostrano quante volte ogni percorso è stato seguito dagli utenti. Nodi speciali "Sessione" mostrano il numero di utenti non inviato alcun visualizzazioni di pagina o eventi personalizzati dopo hello precedente nodo evidenziazione in cui gli utenti probabilmente lasciato il sito.



> [!NOTE]
> La risorsa di Application Insights deve contenere le visualizzazioni di pagina o lo strumento di utente flussi di eventi personalizzati toouse hello. [Informazioni su come tooset verso l'alto la pagina toocollect app Visualizza automaticamente con Application Insights JavaScript SDK hello](app-insights-javascript.md).
> 
> 

## <a name="start-by-choosing-an-initial-page-view-or-custom-event"></a>Per iniziare, scegliere una visualizzazione di pagina o un evento personalizzato iniziale

![Scegliere un evento iniziale per Flussi utente](./media/app-insights-usage-flows/flows-initial-event.png)

tooget avviato rispondere alle domande con lo strumento utente scorre hello, scegliere una visualizzazione di pagina iniziale o un evento personalizzato tooserve come punto di partenza per la visualizzazione hello hello:
1. Fare clic sul collegamento hello in hello "cosa gli utenti eseguito dopo …?" titolo oppure fare clic sul pulsante Modifica hello. 
2. Dall'elenco a discesa "Evento iniziale" hello, selezionare una visualizzazione della pagina o un evento personalizzato.
3. Fare clic su "Crea grafico".

colonna "Passaggio 1" Hello di visualizzazione hello Mostra ciò che gli utenti ha più di frequente subito dopo l'evento iniziale hello, ordinate dall'alto al basso da tooleast frequente. Hello "Passaggio 2" e Mostra le colonne successive degli utenti a cui è stati successivamente, creazione di un'immagine di tutti gli utenti di modi hello lo spostamento all'interno del sito.

Per impostazione predefinita, lo strumento di hello utente scorre un campionamento casuale solo hello ultime 24 ore di visualizzazioni di pagina e l'evento personalizzato dal sito. È possibile aumentare l'intervallo di tempo hello e modificare il bilanciamento hello di prestazioni e accuratezza per il campionamento casuale nel menu di modifica hello.

Se alcune delle visualizzazioni pagina hello ed eventi personalizzati non sono rilevanti tooyou, fare clic su "X" hello nei nodi hello desiderato toohide. Dopo aver selezionato i nodi di hello toohide desiderati, fare clic sul pulsante "Crea grafico" hello seguito visualizzazione hello. toosee tutti i nodi di hello nascosti, fare clic sul pulsante Modifica hello, quindi cerca nella sezione "Eventi esclusi" hello.

Se le visualizzazioni di pagina o a eventi personalizzati non sono presenti che si prevede di toosee sulla visualizzazione hello:
* Verificare nella sezione "Eventi esclusi" hello nel menu di modifica hello.
* Utilizzare il controllo di "Livello di dettaglio" hello hello modifica menu tooinclude meno frequenti gli eventi nella visualizzazione hello.
* Se da parte degli utenti viene inviato raramente visualizzazione pagina hello o si prevede di evento personalizzato, provare a intervallo di tempo hello crescente di visualizzazione hello nel menu di modifica hello.
* Assicurarsi di visualizzazione della pagina che hello o un evento personalizzato che previsto impostato toobe raccolti da hello Application Insights SDK nel codice sorgente hello del sito. [Altre informazioni sulla raccolta di eventi personalizzati](app-insights-api-custom-events-metrics.md).

Se si desidera più passaggi nella visualizzazione hello, utilizzare hello "Numero di passaggi" dispositivo di scorrimento hello toosee menu di modifica.

## <a name="after-visiting-a-page-or-feature-where-do-users-go-and-what-do-they-click"></a>Dopo aver visitato una pagina o una funzionalità, dove si spostano gli utenti e su quali elementi fanno clic?

![Utilizzare flussi utente toounderstand in cui gli utenti fanno clic](./media/app-insights-usage-flows/flows-one-step.png)

Se l'evento iniziale è una visualizzazione di pagina, hello prima colonna ("passaggio 1") della visualizzazione hello è toounderstand un modo rapido degli utenti a cui è state immediatamente dopo la visita la pagina hello. Provare ad aprire il sito in un toohello successiva finestra visualizzazione utente scorre. Confrontare le aspettative di interazione degli utenti con hello pagina toohello elencati eventi nella colonna "Passaggio 1" hello. Spesso, un elemento dell'interfaccia utente nella pagina hello apparentemente irrilevante tooyour team può essere tra più utilizzati nella pagina hello hello. Può trattarsi di un punto di partenza ideale per il sito tooyour miglioramenti di progettazione.

Se l'evento iniziale è un evento personalizzato, prima colonna hello Mostra ciò che gli utenti ha subito dopo l'esecuzione di tale azione. Come con le visualizzazioni di pagina, prendere in considerazione se hello osservata comportamento degli utenti soddisfi gli obiettivi del team e le aspettative dei clienti. Se l'evento iniziale selezionato è "Elemento aggiunto tooShopping carrello", ad esempio, un aspetto toosee se "Go tooCheckout" e "Completamento acquisto" vengono visualizzati nella visualizzazione hello dopo poco tempo. Se il comportamento di utente è molto diverso rispetto alle aspettative, utilizzare toounderstand visualizzazione hello come gli utenti vengono recupero "intercettati" in base alla progettazione corrente del sito.

## <a name="where-are-hello-places-that-users-churn-most-from-your-site"></a>In cui sono hello inserisce che gli utenti varianza la maggior parte del sito?

Espressioni di controllo per i nodi "Sessione" apparentemente elevata-up in una colonna di visualizzazione di hello, in particolare all'inizio di un flusso. Ciò significa che molti utenti probabilmente variati dal sito dopo l'esempio hello percorso precedente delle pagine e le interazioni dell'interfaccia utente. In alcuni casi l'abbandono è previsto, ad esempio dopo aver completato un acquisto in un sito di e-commerce, ma in genere è segno di problemi di progettazione, prestazioni insoddisfacenti o altri aspetti del sito che è possibile migliorare.

Tenere presente che i nodi "Sessione terminata" si basano unicamente sui dati di telemetria raccolti da questa risorsa di Application Insights. Se Application Insights non riceve dati di telemetria per alcune interazioni dell'utente, gli utenti Impossibile hanno ancora interagire con il sito in tale dopo strumento utente scorre hello afferma hello sessione è terminata.

## <a name="are-there-places-where-users-repeat-hello-same-action-over-and-over"></a>Quali sono le posizioni in cui gli utenti di ripetere l'operazione hello stessa azione ripetutamente?

Cercare una visualizzazione della pagina o di un evento personalizzato che viene ripetuta da molti utenti i passaggi successivi in visualizzazione hello. In genere, ciò significa che gli utenti eseguono azioni ripetitive nel sito. Se si ritiene di ripetizioni, considerare Modifica progettazione hello del sito o l'aggiunta di ripetizioni di tooreduce nuove funzionalità. Ad esempio, aggiungere la funzionalità di modifica in blocco se gli utenti eseguono azioni ripetitive in ogni riga di un elemento tabella.

## <a name="common-questions"></a>Domande frequenti

### <a name="why-do-steps-appear-disconnected"></a>Perché i passaggi appaiono disconnessi?

![Flussi utente con passaggi disconnessi](./media/app-insights-usage-flows/flows-disconnected.png)

Se i passaggi (colonne) in una visualizzazione utente flussi vengono disconnessi, ciò significa nessuno dei percorsi di hello eseguiti dagli utenti tra i passaggi di hello sono sufficientemente frequenti toobe illustrato. tooshow meno frequenti eventi nella visualizzazione hello i passaggi di hello visualizzati connessi, regolare il dispositivo di scorrimento di hello "Livello di dettaglio" nel menu di modifica hello.

### <a name="does-hello-initial-event-represent-hello-first-time-hello-event-appears-in-a-session-or-any-time-it-appears-in-a-session"></a>Hello evento iniziale rappresentano hello prima ora hello evento viene visualizzato in una sessione o ogni volta che viene visualizzato in una sessione?

evento iniziale di Hello sulla visualizzazione hello rappresenta solo hello prima volta che un utente inviate tale visualizzazione della pagina o un evento personalizzato durante una sessione. Se gli utenti possono inviare l'evento iniziale hello più volte in una sessione, colonna "Passaggio 1" hello Mostra solo il comportano di utenti dopo hello *prima* istanza evento iniziale, non tutte le istanze.

## <a name="next-steps"></a>Passaggi successivi

* [Panoramica sull'uso](app-insights-usage-overview.md)
* [Utenti, Sessioni ed Eventi](app-insights-usage-segmentation.md)
* [Conservazione](app-insights-usage-retention.md)
* [Aggiunta di eventi personalizzati tooyour app](app-insights-api-custom-events-metrics.md)
