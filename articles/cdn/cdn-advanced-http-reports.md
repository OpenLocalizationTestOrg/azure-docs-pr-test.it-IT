---
title: statistiche di utilizzo aaaAnalyze con la rete CDN Azure advanced report HTTP | Documenti Microsoft
description: "Informazioni su come toocreate advanced report HTTP nella rete CDN di Microsoft Azure. Questi report forniscono informazioni dettagliate sull'attività della rete CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ef90adc1-580e-4955-8ff1-bde3f3cafc5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 3184ec00d089613e25c62762f93043cb4ba68394
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-usage-statistics-with-azure-cdn-advanced-http-reports"></a>Analizzare le statistiche di utilizzo con i report HTTP avanzati della rete CDN di Azure
## <a name="overview"></a>Panoramica
Questo documento illustra la creazione di report HTTP avanzati nella rete CDN di Microsoft Azure. Questi report forniscono informazioni dettagliate sull'attività della rete CDN.

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="accessing-advanced-http-reports"></a>Accesso ai report HTTP avanzati
1. Dal Pannello di profilo CDN hello, fare clic su hello **Gestisci** pulsante.
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-advanced-http-reports/cdn-manage-btn.png)
   
    viene visualizzato il portale di gestione della rete CDN Hello.
2. Passare il mouse su hello **Analitica** scheda, quindi passare il mouse su hello **Advanced report HTTP** riquadro a comparsa.  Fare clic su **Piattaforma HTTP grande**.
   
    ![Portale di gestione della rete CDN, menu Report avanzati](./media/cdn-advanced-http-reports/cdn-advanced-reports.png)
   
    Vengono visualizzate le opzioni dei report.

## <a name="geography-reports-map-based"></a>Report geografici (basati su mappe)
Sono disponibili cinque report che sfruttano tooindicate una mappa aree hello da cui viene richiesto il contenuto. Questi report sono Mappa del mondo, Mappa Stati Uniti, Mappa Canada, Mappa Europa e Mappa Asia Pacifico.

Ogni report basata su mappa classifica geografica entità (ad esempio, paesi, stati e province) in base toohello percentuale di riscontri che ha originato da tale area. Inoltre, una mappa viene fornito toohelp visualizzare i percorsi di hello da cui viene richiesto il contenuto. È in grado di toodo in modo da ogni area di codifica a colori in base a quantità toohello di richiesta verificato in tale area. Le aree con una sfumatura più chiara indicano una domanda minore di contenuto, mentre le aree più scure indicano livelli più alti di domanda di contenuto.

Informazioni dettagliate di traffico e larghezza di banda per ogni area viene fornite direttamente sotto la mappa hello. In questo modo è totale hello tooview dei riscontri, percentuale di riscontri di hello, hello le quantità di dati trasferiti (in GB) e percentuale di hello dei dati trasferiti per ogni area. Visualizzare una descrizione per ogni metrica. Quando passa il mouse su un'area (ad esempio, paese, stato o provincia), infine, il nome di hello e la percentuale di hello di riscontri per cui si è verificato nell'area di hello verrà visualizzati come descrizione comando.

Di seguito viene fornita una breve descrizione di ogni tipo di report geografico basato su mappa.

| Nome report | Descrizione |
| --- | --- |
| Mappa del mondo |Questo report consente la domanda in tutto il mondo tooview hello per il contenuto della rete CDN. Ogni paese è contraddistinte da colori su hello world mappa tooindicate hello percentuale riscontri che ha originato da tale area. |
| Mappa Stati Uniti |Questo report consente richiesta hello tooview per il contenuto della rete CDN hello Stati Uniti. Ogni stato con colori diversi in questa percentuale di hello tooindicate mappa di accessi che ha originato da tale area. |
| Mappa Canada |Questo report consente richiesta hello tooview per il contenuto della rete CDN in Canada. Ogni province con colori diversi in questa percentuale di hello tooindicate mappa di accessi che ha originato da tale area. |
| Mappa Europa |Questo report consente richiesta hello tooview per il contenuto della rete CDN in Europa. Ogni singolo paese con colori diversi in questa percentuale di hello tooindicate mappa di accessi che ha originato da tale area. |
| Mappa Asia Pacifico |Questo report consente richiesta hello tooview per il contenuto della rete CDN in Asia. Ogni singolo paese con colori diversi in questa percentuale di hello tooindicate mappa di accessi che ha originato da tale area. |

## <a name="geography-reports-bar-charts"></a>Report geografici (grafici a barre)
Esistono due altri report che forniscono informazioni statistiche in base toogeography, Top città e paesi superiore. Questi report classificano le città e paesi, rispettivamente, in base a numero toohello di accessi che proviene da tali aree. Dopo la generazione di questo tipo di report, un grafico a barre indicherà 10 città superiore hello o paesi che richiede il contenuto su una piattaforma specifica. Questo grafico a barre consente tooquickly valutare le aree di hello che generano hello il numero massimo di richieste per il contenuto.

lato sinistro di Hello del grafico hello (asse y) indica il numero di risultati nell'area specificata hello. Direttamente sotto il grafico di hello (asse x), si noterà un'etichetta per ognuna delle aree di 10 superiore hello.

### <a name="using-hello-bar-charts"></a>Utilizzo di grafici a barre hello
* Se si passa il mouse su una barra, nome hello e hello totale dei riscontri per cui si è verificato nell'area di hello verrà visualizzati come descrizione comando.
* descrizione comando Hello per hello report Top città identifica una città con il nome, la provincia e l'abbreviazione paese.
* Se non è stato possibile determinare la città hello o area geografica (ad esempio, la provincia) da cui viene originata una richiesta, verrà indicare che sono sconosciuti. Se paese hello è sconosciuto, due punti interrogativi (ad esempio??), verrà visualizzato.
* Un report può includere le metriche per "Europe" o hello "Area Asia-Pacifico /". Tali elementi non sono concepiti tooprovide informazioni statistiche su tutti gli indirizzi IP in queste aree. Piuttosto, sono applicabili unicamente toorequests provenienti da indirizzi IP che sono distribuiti su Europa o Asia/Pacifico anziché tooa specifica città o il paese.

dati Hello grafico a barre hello toogenerate utilizzate possono essere visualizzati sotto di essa. Sarà possibile trovare hello Totale riscontri, percentuale hello degli accessi, quantità hello di dati trasferiti (in GB) e percentuale di hello di dati trasferiti per hello 250 aree superiore. Visualizzare una descrizione per ogni metrica.

Per entrambi i tipi di report seguenti viene fornita una breve descrizione.

| Nome report | Descrizione |
| --- | --- |
| Città principali |Questo report classifica le città in base a numero toohello di accessi che ha originato da tale area. |
| Paesi principali |Questo report classifica i paesi in base a numero toohello di accessi che ha originato da tale area. |

## <a name="daily-summary"></a>Riepilogo giornaliero
report di riepilogo giornaliero Hello consente tooview hello Totale riscontri e i dati trasferiti in una determinata piattaforma su base giornaliera. Queste informazioni possono essere usate tooquickly discernere di modelli di attività della rete CDN. Questo report, ad esempio, consente di rilevare in quali giorni il traffico è stato superiore o inferiore al previsto.

Dopo la generazione di questo tipo di report, un grafico a barre verrà forniscono un'indicazione visiva come quantità toohello di esperti di richiesta specifici della piattaforma su base giornaliera hello periodo di tempo coperto dal report hello. Tale visualizzando una barra per ogni giorno report hello. Ad esempio, selezionando hello periodo di tempo denominato "Ultima settimana" verrà generato un grafico a barre con le barre di sette. Ogni barra indicherà hello totale dei riscontri che si è verificato nella stessa giornata.

Hello lato sinistro del grafico hello (asse y) indica il numero di risultati si è verificato in hello specificato Data. Direttamente sotto il grafico di hello (asse x), si noterà un'etichetta che indica la data di hello (formato: aaaa-MM-gg) per ogni giorno incluso nel rapporto di hello.

> [!TIP]
> Se si passa il mouse su una barra, hello il numero totale di riscontri per cui si è verificato in tale data verrà visualizzato come descrizione comando.
> 
> 

dati Hello grafico a barre hello toogenerate utilizzate possono essere visualizzati sotto di essa. Vi si noterà hello Totale riscontri e quantità hello di dati trasferiti (in GB) per ciascun giorno in cui la relazione hello.

## <a name="by-hour"></a>Per ora
report da ora Hello consente tooview hello Totale riscontri e i dati trasferiti in una determinata piattaforma su base oraria. Queste informazioni possono essere usate tooquickly discernere di modelli di attività della rete CDN. Ad esempio, questo report consente di rilevare hello periodi di tempo durante il giorno hello esperienza superiore o inferiore al traffico previsto.

Dopo la generazione di questo tipo di report, un grafico a barre fornirà un'indicazione visiva come quantità toohello di richiesta specifici della piattaforma subito su base oraria hello periodo di tempo coperto dal report hello. Tale visualizzando una barra per ogni ora coperto dal report hello. Se, ad esempio, si seleziona un periodo di tempo di 24 ore, verrà generato un grafico con ventiquattro barre. Ogni barra indicherà hello totale dei riscontri che si è verificato durante quell'ora.

lato sinistro di Hello del grafico hello (asse y) indica il numero di risultati ora specificato hello. Direttamente sotto il grafico di hello (asse x), si noterà un'etichetta che indica data e ora hello (formato: aaaa-MM-gg hh.mm) per ogni ora incluso nel rapporto di hello. Tempo viene espresso nel formato 24 ore e viene specificata tramite hello fuso orario UTC/GMT.

> [!TIP]
> Se si passa il mouse su una barra, hello Totale riscontri per cui si è verificato durante quell'ora verrà visualizzato come descrizione comando.
> 
> 

dati Hello grafico a barre hello toogenerate utilizzate possono essere visualizzati sotto di essa. Vi sono disponibili hello Totale riscontri e quantità hello di dati trasferiti (in GB) per ogni ora coperto dal report hello.

## <a name="by-file"></a>Per file
Hello da File di report consente di tooview hello quantità di traffico di richiesta e hello sostenute su una determinata piattaforma per hello più richiesto asset. Dopo la generazione di questo tipo di report, verrà generato un grafico a barre sulle risorse di più richieste 10 superiore hello su hello periodo di tempo specificato.

> [!NOTE]
> Ai fini di hello di questo report, bordo CNAME URL sono URL CDN equivalenti tootheir convertito. In questo modo che un conteggio accurato per il numero totale di riscontri hello con un asset hello CDN indipendentemente edge URL CNAME utilizzato toorequest verrà associata.
> 
> 

lato sinistro di Hello del grafico hello (asse y) indica il numero di hello di richieste per ogni asset su hello periodo di tempo specificato. Direttamente sotto il grafico di hello (asse x), si noterà un'etichetta che indica il nome file hello per ognuna delle attività di richiesta 10 superiore hello.

dati Hello grafico a barre hello toogenerate utilizzate possono essere visualizzati sotto di essa. Sono disponibili le seguenti informazioni per ognuna delle attività di richiesta 250 superiore hello hello: percorso relativo, hello il numero totale di riscontri, percentuale di riscontri di hello, quantità hello di dati trasferiti (in GB) e la percentuale di hello di dati trasferiti.

## <a name="by-file-detail"></a>Per dettaglio file
report da File dettagli Hello consente tooview hello massima per la richiesta e hello traffico generato su una piattaforma particolare per un asset specifico. In hello parte superiore di questo report è hello dettagli per File. Questa opzione fornisce un elenco delle risorse più richiesti nella piattaforma selezionata hello. In un report dettagli del File da toogenerate di ordine, sarà necessario asset desiderato di hello tooselect da hello File dettagli per l'opzione. Dopo il quale, un grafico a barre indicherà quantità hello di domanda giornaliera generata su hello periodo di tempo specificato.

Hello il lato sinistro del grafico hello (asse y) indica hello totale delle richieste che si è verificato un asset in un determinato giorno. Direttamente sotto il grafico di hello (asse x), si noterà un'etichetta che indica la data di hello (formato: aaaa-MM-gg) per la quale richiesta della rete CDN per hello asset è stato segnalato.

dati Hello grafico a barre hello toogenerate utilizzate possono essere visualizzati sotto di essa. Vi si noterà hello Totale riscontri e quantità hello di dati trasferiti (in GB) per ciascun giorno in cui la relazione hello.

## <a name="by-file-type"></a>Per tipo di file
report per il tipo di File Hello consente si tooview hello quantità di traffico di richiesta e hello causato dal tipo di file. Dopo la generazione di questo tipo di report, un grafico ad anello indicherà la percentuale hello di riscontri generato hello top 10 tipi di file.

> [!TIP]
> Se si passa il mouse su una sezione di grafico ad anello hello, hello Internet tipo di supporto di che tipo di file verrà visualizzato come descrizione comando.
> 
> 

dati Hello grafico ad anello di hello toogenerate utilizzate possono essere visualizzati sotto di essa. Sono presenti i tipo di supporto/Internet estensione nome file hello, totale hello dei riscontri, percentuale di riscontri di hello, quantità hello di dati trasferiti (in GB) e percentuale di dati trasferiti per ognuna delle hello hello primi 250 tipi di file.

## <a name="by-directory"></a>Per directory
report dalla Directory Hello consente quantità hello tooview di richiesta e hello traffico generato su una determinata piattaforma per il contenuto da una directory specifica. Dopo la generazione di questo tipo di report, un grafico a barre indicherà hello totale dei riscontri generati dal contenuto nella 10 directory superiore hello.

### <a name="using-hello-bar-chart"></a>Utilizzare hello grafico a barre
* Passare il mouse su una barra di directory corrispondente toohello tooview hello percorso relativo.
* Il contenuto archiviato in una sottocartella di una directory non viene considerato durante il calcolo della domanda per directory. Questo calcolo si basa unicamente sulla numero hello di richieste di generato per il contenuto memorizzato nella directory effettivo hello.
* Ai fini di hello di questo report, bordo CNAME URL sono URL CDN equivalenti tootheir convertito. In questo modo che un conteggio accurato per tutte le statistiche con un asset hello CDN indipendentemente edge URL CNAME utilizzato toorequest verrà associata.

Hello lato sinistro del grafico hello (asse y) indica hello il numero totale di richieste di contenuto hello archiviata nella directory di superiore a 10. Ogni barra nel grafico hello rappresenta una directory. Hello utilizzare codifica a colori toomatch lo schema di una barra tooa directory elencati nella sezione superiore 250 completo directory hello.

dati Hello grafico a barre hello toogenerate utilizzate possono essere visualizzati sotto di essa. Sono disponibili le seguenti informazioni per ogni directory superiore a 250 hello hello: percorso relativo, hello il numero totale di riscontri, percentuale di riscontri di hello, quantità hello di dati trasferiti (in GB) e la percentuale di hello di dati trasferiti.

## <a name="by-browser"></a>Per browser
Hello report dal Browser consente tooview quali browser sono stati utilizzati toorequest contenuto. Dopo la generazione di questo tipo di report, un grafico a torta indicherà la percentuale hello di richieste gestite dal 10 browser superiore hello.

### <a name="using-hello-pie-chart"></a>Usa grafico a torta hello
* Passare il mouse su una sezione di hello grafico a torta tooview nome di un browser e la versione.
* Ai fini di hello di questo report, ogni combinazione di browser/versione univoco viene considerato un browser diverso.
* sezione Hello denominata "Altro" indica la percentuale hello di richieste gestite da tutti gli altri browser e le versioni.

dati Hello che è stato utilizzato toogenerate hello grafico a torta possono essere visualizzati sotto di essa. Non esiste, si noterà hello browser tipo/numero di versione, numero totale di hello di accessi e la percentuale di hello dei riscontri per ognuno dei 250 browser superiore hello.

## <a name="by-referrer"></a>Per referrer
report da Referrer Hello consente tooview hello principali riferimenti toocontent nella piattaforma selezionata hello. Un riferimento indica il nome host hello da cui è stata generata una richiesta. Dopo la generazione di questo tipo di report, un grafico a barre indicherà quantità hello di richiesta (ad esempio, di riscontri) generato da 10 riferimenti principali hello.

lato sinistro di Hello del grafico hello (asse y) indica hello totale delle richieste che si è verificato un asset per ogni riferimento. Ogni barra nel grafico hello rappresenta un riferimento. Hello utilizzare codifica a colori toomatch lo schema di una barra tooa referrer elencati nella sezione di inizio 250 Referrer hello.

dati Hello grafico a barre hello toogenerate utilizzate possono essere visualizzati sotto di essa. Sarà possibile trovare URL hello, hello Totale riscontri e hello percentuale di riscontri generati da ognuno dei riferimenti di 250 principali hello.

## <a name="by-download"></a>Per download
Hello da scaricare report permette tooanalyze modelli di download per il contenuto più richiesto. parte superiore di Hello di hello report contiene un grafico a barre che confronta ha tentato di download con download completato per hello le prime 10 asset richiesti. Ogni barra è contraddistinti dal colore in base toowhether che è un tentativo di download (blu) o un download completato (verde).

> [!NOTE]
> Ai fini di hello di questo report, bordo CNAME URL sono URL CDN equivalenti tootheir convertito. In questo modo che un conteggio accurato per tutte le statistiche con un asset hello CDN indipendentemente edge URL CNAME utilizzato toorequest verrà associata.
> 
> 

lato sinistro di Hello del grafico hello (asse y) indica il nome file hello per ognuna delle attività di richiesta 10 superiore hello. Direttamente sotto il grafico di hello (asse x), si noterà etichette che indicano hello il numero totale dei download tentato completata.

Direttamente sotto grafico a barre hello, verrà elencato hello le seguenti informazioni per le risorse di richiesta 250 superiore hello: percorso relativo (incluso il nome file), il numero di hello di volte in cui è stato scaricato toocompletion, hello numero di volte in cui è stata richiesta e hello percentuale di richieste che ha comportato un download completo.

> [!TIP]
> La rete CDN non viene informata da un client HTTP (ad esempio, un browser) quando un asset è stato scaricato completamente. Di conseguenza, abbiamo toocalculate se un asset è stato completamente scaricato secondo toostatus codici e le richieste di intervallo di byte. Hello in primo luogo presi in considerazione questo calcolo è se hello richiesta determina un codice di 200 stato OK. In questo caso, quindi verranno esaminate tooensure le richieste di intervallo di byte che coprono asset intera hello. Confrontare infine quantità hello delle dimensioni dati trasferiti toohello hello richiesto asset. Se i dati hello trasferiti è maggiore di dimensioni del file hello tooor uguale e le richieste di intervallo di byte hello sono appropriate per tale risorsa, quindi premere hello viene conteggiato come un download completo.
> 
> A causa di toohello natura interpretativi di questo report, è necessario tenere hello presente seguendo i punti che potrebbero modificare la coerenza hello e l'accuratezza di questo report.
> 
> * I modelli di traffico non possono essere previsti con precisione quando gli agenti utente si comportano in modo diverso. Ciò può generare risultati di download completato superiori al 100%.
> * È possibile che gli asset che sfruttano il download progressivo HTTP non vengano rappresentati accuratamente da questo report Ciò è dovuto toousers ricerca toodifferent posizioni in un video.
> 
> 

## <a name="by-404-errors"></a>Per errori 404
report errori da 404 Hello consente tipo hello tooidentify di contenuto che genera l'errore hello massimo numero di codici di stato 404 non trovato. parte superiore di Hello di hello report contiene un grafico a barre per le risorse di hello primi 10 per il quale è stato restituito un codice di stato 404 non trovato. Questo grafico a barre Confronta hello Totale richieste con le richieste che hanno generato un 404 non trovato. codice di stato per tali risorse. Ogni barra è contraddistinta dal colore. Viene utilizzata una barra gialla tooindicate che hello richiesta ha restituito un codice di stato 404 non trovato. Viene utilizzata una barra rossa totale hello tooindicate delle richieste per asset hello.

> [!NOTE]
> Ai fini di hello di questo report, si noti seguenti hello:
> 
> * Un riscontro rappresenta una richiesta per un asset indipendentemente dal codice di stato.
> * Gli URL di CNAME Edge sono URL CDN equivalenti tootheir convertito. In questo modo che un conteggio accurato per tutte le statistiche con un asset hello CDN indipendentemente edge URL CNAME utilizzato toorequest verrà associata.
> 
> 

lato sinistro di Hello del grafico hello (asse y) indica il nome file hello hello top 10 asset richiesti che hanno restituito un codice di stato 404 non trovato. Direttamente sotto il grafico di hello (asse x), si noterà che le etichette che indicano totale hello delle richieste e il numero di hello di richieste che hanno restituito un codice di stato 404 non trovato.

Direttamente sotto grafico a barre hello, verrà elencato hello le seguenti informazioni per le risorse di richiesta 250 superiore hello: percorso relativo (incluso il nome file), il numero di hello di richieste che ha comportato un 404 non trovato. codice di stato, numero totale di hello di volte in cui hello asset: richiesta e hello percentuale di richieste che hanno restituito un codice di stato 404 non trovato.

## <a name="see-also"></a>Vedere anche
* [Panoramica della rete CDN di Azure](cdn-overview.md)
* [Statistiche in tempo reale nella rete CDN di Microsoft Azure](cdn-real-time-stats.md)
* [Override del comportamento HTTP predefinito utilizzando il motore regole di hello](cdn-rules-engine.md)
* [Analizzare delle prestazioni edge](cdn-edge-performance.md)

