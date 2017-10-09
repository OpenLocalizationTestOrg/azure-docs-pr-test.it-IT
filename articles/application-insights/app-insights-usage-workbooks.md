---
title: aaaInvestigate e condivisione di dati di utilizzo delle cartelle di lavoro interattivi in Azure Application Insights | Documenti Microsoft
description: Analisi demografica degli utenti dell'app Web.
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: bdcebe0f97fdad0a0b301df5950dc09698f5a4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a>Analizzare e condividere i dati di utilizzo con cartelle di lavoro interattive in Application Insights

Le cartelle di lavoro combinano le visualizzazioni dei dati di [Azure Application Insights](app-insights-overview.md), le [query di Analisi](app-insights-analytics.md) e il testo in documenti interattivi. Le cartelle di lavoro vengono modificati dagli altri membri del team con accesso toohello stessa risorsa di Azure. Ciò significa hello query e i controlli utilizzati toocreate una cartella di lavoro sono disponibili tooother connetteranno cartella di lavoro hello, rendendoli tooexplore facile estendere e verificare la presenza di errori.

Le cartelle di lavoro sono utili per scenari simili ai seguenti:

* Esplorazione dell'utilizzo di hello dell'app quando non si conoscono in anticipo le metriche di hello di interesse: numero di utenti, i tassi di conservazione, tassi di conversione, e così via. A differenza di altri strumenti di analisi dell'utilizzo di Application Insights, le cartelle di lavoro consentono di combinare più tipi di visualizzazioni e analisi risultando ideali per questo tipo di esplorazione in formato libero.
* Descrivere il team tooyour le prestazioni di una funzionalità rilasciata di recente, dall'utente che mostra i conteggi per chiave e le interazioni di altre metriche.
* Condivisione risultati hello di A / B provare in un'app con altri membri del team. È possibile illustrare gli obiettivi di hello per hello sperimentare testo, quindi mostrano ogni metrica di utilizzo e query Analitica utilizzato esperimento hello tooevaluate, insieme a deselezionare callout per se ogni metrica è di sopra o sotto-destinazione.
* Report impatto hello di un'interruzione all'utilizzo di hello dell'app, la combinazione di dati, spiegazione di testo e una descrizione delle interruzioni di tooprevent procedura successiva in hello future.

> [!NOTE]
> La risorsa di Application Insights deve contenere le visualizzazioni di pagina o le cartelle di lavoro toouse eventi personalizzati. [Informazioni su come tooset verso l'alto la pagina toocollect app Visualizza automaticamente con Application Insights JavaScript SDK hello](app-insights-javascript.md).
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a>Modifica, ridisposizione, clonazione ed eliminazione di sezioni delle cartelle di lavoro

Una cartella di lavoro è costituita da sezioni: visualizzazioni dell'utilizzo modificabili separatamente, grafici, tabelle, testo o risultati delle query di Analisi.

contenuto di hello tooedit di una sezione di cartella di lavoro, fare clic su hello **modifica** pulsante riportato di seguito e toohello destra della sezione di hello cartella di lavoro.

![Controlli di modifica delle sezioni delle cartelle di controllo di Application Insights](./media/app-insights-usage-workbooks/editing-controls.png)

1. Dopo avere una sezione di modifica, fare clic su **modifica eseguita** in hello inferiore sinistro della sezione hello.

2. toocreate un duplicato di una sezione, fare clic su hello **Clone di questa sezione** icona. La creazione di sezioni duplicate è un tooiterate tooway grande su una query senza perdere iterazioni precedenti.

3. toomove una sezione in una cartella di lavoro, fare clic su hello **spostare verso l'alto** o **Sposta giù** icona.

4. tooremove una sezione in modo permanente, fare clic su hello **rimuovere** icona.

## <a name="adding-usage-data-visualization-sections"></a>Aggiunta di sezioni di visualizzazioni dei dati di utilizzo

Le cartelle di lavoro offrono quattro tipi di visualizzazioni di analisi di utilizzo predefiniti. Ogni risponde alle domande comuni sull'utilizzo hello dell'app. tooadd tabelle e grafici diversi da questi quattro sezioni, aggiungere sezioni query Analitica (vedere sotto).

tooadd utenti, sessioni, eventi o memorizzazione sezione tooyour cartella di lavoro, utilizzare hello **Aggiungi utenti** o altro pulsante corrispondente nella parte inferiore di hello della cartella di lavoro hello o nella parte inferiore di hello di ogni sezione.

![Sezione Utenti nelle cartelle di lavoro](./media/app-insights-usage-workbooks/users-section.png)

Le sezioni **Utenti** rispondono alla domanda "Quanti utenti hanno visualizzato una pagina o usato una funzionalità del sito?"

Le sezioni **Sessioni** rispondono alla domanda "Per quante sessioni gli utenti hanno visualizzato una pagina o usato una funzionalità del sito?"

Le sezioni **Eventi** rispondono alla domanda "Quante volte gli utenti hanno visualizzato una pagina o usato una funzionalità del sito?"

Ognuno di questi tipi di tre sezione offre hello stessi set di controlli e le visualizzazioni:

* Vedere le [informazioni sulla modifica delle sezioni Utenti, Sessioni ed Eventi](app-insights-usage-segmentation.md)
* Attivare o disattivare grafico principale hello, griglie istogramma, insights automatico e visualizzazioni di utenti di esempio con hello **Mostra grafico**, **Mostra griglia**, **Insights Mostra**e **Esempio di questi utenti** caselle di controllo nella parte superiore di hello di ogni sezione.

![Sezione Conservazione nelle cartelle di lavoro](./media/app-insights-usage-workbooks/retention-section.png)

Le sezioni **Conservazione** rispondono alla domanda "Degli utenti che hanno visualizzato una pagina o usato una funzionalità in un determinato giorno o settimana quanti sono tornati un giorno o una settimana successiva?"

* Vedere le [informazioni sulla modifica delle sezioni Conservazione](app-insights-usage-retention.md)
* Attiva/Disattiva hello facoltativo memorizzazione globale grafico utilizzando hello **Mostra grafico di memorizzazione globale** casella di controllo nella parte superiore di hello della sezione hello.

## <a name="adding-application-insights-analytics-sections"></a>Aggiunta di sezioni di analisi di Application Insights

![Sezione di analisi nelle cartelle di lavoro](./media/app-insights-usage-workbooks/analytics-section.png)

un'applicazione Insights Analitica query sezione tooyour cartella di lavoro tooadd utilizzare hello **query Analitica aggiungere** pulsante nella parte inferiore di hello della cartella di lavoro hello o nella parte inferiore di hello di ogni sezione.

Le sezioni delle query di Analisi consentono di aggiungere query arbitrarie nei dati di Application Insights nelle cartelle di lavoro. Questa flessibilità consente a sezioni di query Analitica devono essere il go-toofor rispondere alle domande sul sito diverso da hello quattro elencati in precedenza per gli utenti, sessioni, eventi e memorizzazione, ad esempio:

* Il numero di eccezioni ha throw del sito durante hello stesso periodo, come una diminuzione dell'utilizzo?
* Qual era distribuzione hello dei tempi di caricamento pagina per gli utenti che visualizzeranno alcuni pagina?
* Quanti utenti hanno visualizzato un insieme di pagine nel sito ma non un altro insieme di pagine? Se si dispone di gruppi di utenti che utilizzano subset diversi di funzionalità del sito, questo può essere utile toounderstand (utilizzare hello `join` operatore con hello `kind=leftanti` modificatore nel linguaggio di query Log Analitica hello).

Hello utilizzare [riferimenti al linguaggio di query Log Analitica](https://docs.loganalytics.io/) toolearn ulteriori informazioni sulla scrittura di query.

## <a name="adding-text-and-markdown-sections"></a>Aggiunta di sezioni di testo e Markdown

Aggiunta di intestazioni, spiegazioni e le cartelle di lavoro di commenti tooyour consente di trasformare un set di tabelle e grafici in un resoconto. Le sezioni di testo nelle cartelle di lavoro supportano hello [sintassi Markdown](https://daringfireball.net/projects/markdown/) per la formattazione del testo, ad esempio intestazioni, grassetto, corsivo ed elenchi puntati.

cartella di lavoro tooyour, sezione testo tooadd utilizzare hello **aggiungere testo** pulsante nella parte inferiore di hello della cartella di lavoro hello o nella parte inferiore di hello di ogni sezione.

## <a name="saving-and-sharing-workbooks-with-your-team"></a>Salvataggio e condivisione delle cartelle di lavoro con il team

Le cartelle di lavoro vengono salvati all'interno di una risorsa di Application Insights in hello **report personali** sezione tooyou privata o in hello **report condivisi** sezione tooeveryone accessibili con accesso toohello risorsa di Application Insights. tooview tutte le cartelle di lavoro di hello in risorsa hello, fare clic su hello **aprire** pulsante nella barra delle azioni hello.

una cartella di lavoro è attualmente in tooshare **report personali**:

1. Fare clic su **aprire** nella barra delle azioni hello
2. Fare clic sul pulsante "…" hello accanto a cartella di lavoro hello desiderato tooshare
3. Fare clic su **spostare report tooShared**.

Fare clic su una cartella di lavoro con un collegamento o tramite posta elettronica, tooshare **condivisione** nella barra delle azioni hello. Tenere presente che i destinatari del collegamento hello necessitano accedere toothis risorsa nella cartella di lavoro hello hello tooview portale Azure. toomake modifiche, i destinatari devono almeno le autorizzazioni di collaboratore per la risorsa hello.

toopin un tooan di cartella di lavoro di collegamento tooa Dashboard di Azure:

1. Fare clic su **aprire** nella barra delle azioni hello
2. Fare clic sul pulsante "…" hello accanto a cartella di lavoro hello desiderato toopin
3. Fare clic su **toodashboard Pin**.

## <a name="next-steps"></a>Passaggi successivi

## <a name="next-steps"></a>Passaggi successivi
- utilizzo di tooenable esperienze, avviare l'invio [eventi personalizzati](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [visualizzazioni pagina](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Se si invia già hello utilizzo strumenti toolearn di esplorare gli eventi personalizzati o le visualizzazioni di pagina, come gli utenti di usare il servizio.
    - [Utenti, sessioni ed eventi](app-insights-usage-segmentation.md)
    - [Grafici a imbuto](usage-funnels.md)
    - [Conservazione](app-insights-usage-retention.md)
    - [Flussi degli utenti](app-insights-usage-flows.md)
    - [Aggiungere il contesto utente](app-insights-usage-send-user-context.md)
    
