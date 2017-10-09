---
title: ricerca nei log toonew aaaUpgrading Analitica di Log di Azure | Documenti Microsoft
description: "è possibile partecipare in anteprima pubblica di hello e il nuovo linguaggio di query Log Analitica di Hello è quasi.  Questo articolo vengono descritti i vantaggi di hello della nuova lingua di hello e come tooconvert l'area di lavoro."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 7659c9d1467cab79d3a16e73b52b507ed281b002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-azure-log-analytics-workspace-toonew-log-search"></a>Aggiornare la ricerca di log toonew dell'area di lavoro Analitica di Log di Azure

> [!NOTE]
> Il nuovo linguaggio di query Log Analitica di aggiornamento toohello è attualmente facoltativo consentendo di troppo[familiarità nuovo linguaggio hello](https://go.microsoft.com/fwlink/?linkid=856078).  

il nuovo linguaggio di query Log Analitica di Hello è qui e occorre tooupgrade comodamente tootake dell'area di lavoro di esso.  Questo articolo vengono descritti i vantaggi di hello della nuova lingua di hello e come tooconvert l'area di lavoro.  Se non si sceglie tooupgrade a questo punto, l'area di lavoro continuerà toooperate esattamente come è stata sempre, ma verranno convertito automaticamente in un secondo momento.  Si riceverà la notifica della data prestabilita con molto anticipo.

In questo articolo vengono fornite informazioni dettagliate sul nuovo linguaggio hello e processo di aggiornamento hello.

## <a name="why-hello-new-language"></a>Motivo per cui hello nuovo linguaggio?
Siamo consapevoli che vi sia deboli in qualsiasi fase di transizione è semplicemente non modifica il linguaggio di query hello per fun hello di esso.  Esistono vari motivi che questa modifica verrà offrire valore aggiunto significativo tooour Analitica di Log.

- **Semplice e potente.** nuovo linguaggio Hello è più facile toounderstand e tooSQL simile con più costrutti come lingua naturale da legacy quella hello.
- **Linguaggio di piping completo.**  nuovo linguaggio Hello ha più ampie funzionalità di invio tramite pipe di linguaggio legacy hello.  Praticamente qualsiasi output può essere reindirizzato tooanother comando toocreate query più complesse rispetto possibile in precedenza.
- **Estrazione di campi in fase di ricerca.**  nuovo linguaggio Hello supporta i campi di runtime calcolato più avanzati rispetto a linguaggio legacy hello.  È possibile utilizzare i calcoli complessi per campi estesi e quindi utilizzare i campi calcolato hello per altri comandi, inclusi i join e aggregazioni.
- **Join avanzati.**  nuovo linguaggio Hello fornisce join più avanzate rispetto a linguaggio legacy di hello incluse le tabelle di toojoin possibilità hello in più campi, utilizzare join inner e outer join sui campi estesi.
- **Funzioni di data/ora.**  nuovo linguaggio Hello funzioni di data/ora ha più avanzato linguaggio legacy hello.
- **Funzioni di analisi avanzate.**  nuovo linguaggio Hello presenta avanzate dei modelli di tooevaluate algoritmi in set di dati e di confronto diversi set di dati.
- **Portale Advanced Analytics.**  portale Analitica avanzate Hello offre funzionalità di analisi non disponibili nel portale di Log Analitica hello inclusi su più righe modifica di query, altre visualizzazioni e la diagnostica avanzata.
- **Coerenza con altre applicazioni.**  Hello nuovo linguaggio e hello portale Analitica avanzate vengono già utilizzati per analitica in Application Insights.  La sua implementazione per Log Analytics aggiunge coerenza tra i servizi di Azure.
- **Migliore integrazione con Power BI.** Le query nella lingua nuova hello possono essere esportati tooPower BI Desktop, pertanto è possibile utilizzare le funzionalità di trasformazione di dati complessi.
- **E altro ancora.** Fare riferimento toohello [linguaggio di Query Azure Log Analitica](https://docs.loganalytics.io) sito per informazioni dettagliate ed esercitazioni sul nuovo linguaggio hello.


## <a name="when-can-i-upgrade"></a>Quando è possibile eseguire l'aggiornamento?
aggiornamento di Hello sarà distribuito di tutte le aree di Azure potrebbe essere disponibile in alcune aree prima degli altri.  Quando l'area di lavoro è disponibile toobe aggiornati quando viene visualizzato il banner di hello viola in alto hello dell'area di lavoro invito tooupgrade saprà.

![Aggiornamento 1](media/log-analytics-log-search-upgrade/upgrade-01a.png)

## <a name="what-happens-when-i-upgrade"></a>Cosa succede quando si esegue l'aggiornamento?
Quando si converte l'area di lavoro, eventuali ricerche salvate, le regole di avviso e viste create con hello Visualizza finestra di progettazione sono automaticamente convertiti toohello nuova lingua.  Ricerche incluse nelle soluzioni non vengono convertite automaticamente, ma invece convertiti in tempo reale di hello quando vengono aperti.  Si tratta di tooyou completamente trasparente.

## <a name="can-i-go-back-after-i-upgrade"></a>Dopo aver eseguito l'aggiornamento è possibile tornare indietro?
Quando si esegue l'aggiornamento, viene creata una copia di backup completa dell'area di lavoro che include uno snapshot di tutte le ricerche, le regole di avviso e le viste.  In questo modo è toorestore l'area di lavoro precedente se desiderato in un secondo momento.

toorestore l'area di lavoro legacy, andare troppo**impostazioni** nell'area di lavoro e quindi **riepilogo aggiornamento**.  È quindi possibile selezionare opzione hello troppo**ripristinare l'area di lavoro legacy**.  

![Ripristino dell'area di lavoro precedente](media/log-analytics-log-search-upgrade/restore-legacy-b.png)

## <a name="how-do-i-perform-hello-upgrade"></a>Come eseguire l'aggiornamento di hello?
È possibile aggiornare l'area di lavoro quando viene visualizzato il banner hello viola nella parte superiore di hello del portale hello.  

1.  Avviato processo di aggiornamento hello facendo clic sul messaggio hello viola indicante **ulteriori informazioni ed eseguire l'aggiornamento**.<br>![Aggiornamento 2](media/log-analytics-log-search-upgrade/upgrade-01a.png)<br>
2.  Leggere informazioni aggiuntive sull'aggiornamento di hello hello nella pagina di informazioni sull'aggiornamento hello.<br>![Aggiornamento 2](media/log-analytics-log-search-upgrade/upgrade-03.png)<br>
3.  Fare clic su **Aggiorna** aggiornamento hello toostart.<br>![Aggiornamento 4](media/log-analytics-log-search-upgrade/upgrade-04.png)<br>Una notifica nell'angolo superiore destro di hello Mostra stato hello.<br>![Aggiornamento 5](media/log-analytics-log-search-upgrade/upgrade-05.png)
4.  La procedura è terminata.  Discutere toohave pagina di ricerca nei Log toohello esaminare l'area di lavoro aggiornato.<br>![Aggiornamento 6](media/log-analytics-log-search-upgrade/upgrade-06.png)<br>

Se si verifica un problema che causa hello toofail di aggiornamento, è possibile passare toohello [forum di discussione](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) e inviare una domanda o [creare una richiesta di supporto](../azure-supportability/how-to-create-azure-support-request.md) da hello portale di Azure.

## <a name="how-do-i-learn-hello-new-language"></a>Come controllare il nuovo linguaggio hello?
Perché è usato da più servizi abbiamo creato un [documentazione di hello toohost sito esterno](https://docs.loganalytics.io/) per il nuovo linguaggio di hello.  Ciò include esercitazioni, esempi e un riferimento completo di toohelp che è risultata toospeed. È possibile seguire un'esercitazione di hello nuovo linguaggio [Guida introduttiva a query](https://go.microsoft.com/fwlink/?linkid=856078) e accedere ai riferimenti al linguaggio hello in [Analitica di Log di query lingua](https://go.microsoft.com/fwlink/?linkid=856079).  

Se si ha già familiarità con hello legacy Analitica Log query tuttavia linguaggio, quindi è possibile utilizzare hello language convertitore che viene aggiunto tooyour dell'area di lavoro come parte dell'aggiornamento hello.

È sufficiente digitare la query precedente e quindi fare clic su **convertire** toosee hello convertite versione.  È possibile fare clic su hello pulsante toorun hello una ricerca o copia e Incolla toouse query hello convertito in un altro, ad esempio una regola di avviso.

![Convertitore di linguaggio](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="next-steps"></a>Passaggi successivi
- Estrarre un [esercitazione sul nuovo linguaggio hello](https://go.microsoft.com/fwlink/?linkid=856078).
- Procedura dettagliata un [esercitazione sul tramite il portale di ricerca nei Log hello](log-analytics-log-search-log-search-portal.md) con il nuovo linguaggio di query hello.
- Ottenere un toohello introduzione nuovo [portale avanzate Analitica](https://go.microsoft.com/fwlink/?linkid=856587).
