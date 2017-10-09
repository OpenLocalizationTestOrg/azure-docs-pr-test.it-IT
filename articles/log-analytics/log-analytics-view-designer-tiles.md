---
title: riferimento aaaTile per Progettazione viste in OMS Log Analitica | Documenti Microsoft
description: Visualizza finestra di progettazione nel Log Analitica consente toocreate personalizzato visualizzazioni nella console OMS hello contenenti visualizzazioni diverse dei dati nel repository OMS hello. Questo articolo fornisce informazioni di riferimento sulle impostazioni di hello per ognuna delle hello riquadri di toouse disponibili nelle visualizzazioni personalizzate.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 41787c8f-6c13-4520-b0d3-5d3d84fcf142
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 4706abb16b8a3719f5dbe8c89cd61739391ab8f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-tile-reference"></a>Informazioni di riferimento sui riquadri per Progettazione viste di Log Analytics
Visualizza finestra di progettazione nel Log Analitica Hello consente toocreate personalizzato visualizzazioni nella console OMS hello contenenti visualizzazioni diverse dei dati nel repository OMS hello. Questo articolo fornisce informazioni di riferimento sulle impostazioni di hello per ognuna delle hello riquadri di toouse disponibili nelle visualizzazioni personalizzate.

Altri articoli disponibili su Progettazione viste sono:

* [Visualizzare Progettazione](log-analytics-view-designer.md) -Panoramica hello Progettazione viste e procedure per la creazione e modifica delle visualizzazioni personalizzate.
* [Riferimento alla parte visualizzazione](log-analytics-view-designer-parts.md) -riferimento delle impostazioni di hello per ognuna delle hello riquadri toouse disponibili nelle visualizzazioni personalizzate.

>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), le query in tutte le visualizzazioni devono essere scritti in hello [nuovo linguaggio di query](https://go.microsoft.com/fwlink/?linkid=856078).  Le viste che sono state create prima dell'area di lavoro di hello è stato aggiornato sarà venga convertito.

Hello nella tabella seguente sono elencati hello diversi tipi di riquadri disponibili in hello Visualizza finestra di progettazione.  Hello nelle sezioni seguenti vengono descrivono ogni tipo di riquadro nel dettaglio e le relative proprietà.

| Riquadro | Descrizione |
|:--- |:--- |
| [Number](#number-tile) |Un numero singolo che indica la quantità di record prodotti da una query. |
| [Due numeri](#two-numbers-tile) |Due numeri singoli che indicano la quantità di record prodotti da due query diverse. |
| [Anello](#donut-tile) |Grafico ad anello in base a una query con un valore di riepilogo nel centro hello. |
| [Grafico a linee e callout](#line-chart-amp-callout-tile) |Un grafico a linee basato su una query e un callout con un valore di riepilogo. |
| [Grafico a linee](#line-chart-tile) |Un grafico a linee basato su una query. |
| [Due sequenze temporali](#two-timelines-tile) |Un istogramma con due serie, ognuna basata su una query separata. |

## <a name="number-tile"></a>Riquadro Numero
Hello **numero** riquadro Visualizza un singolo numero che mostra il conteggio di hello di record da una query log e un'etichetta.

![Riquadro Numero](media/log-analytics-view-designer/tile-number.png)

| Impostazione | Description |
|:--- |:--- |
| Nome |Riquadro testo toodisplay nella parte superiore di hello di hello. |
| Descrizione |Testo toodisplay sotto il nome di sezione hello. |
| **Riquadro** | |
| Legenda |Testo toodisplay in valore hello. |
| Query |Eseguire una query toorun.  verrà visualizzato il conteggio di Hello del numero di hello di record restituiti dalla query hello. |
| **Funzionalità avanzate** |**&gt; Verifica del flusso di dati** |
| Enabled |Selezionare se la verifica del flusso di dati deve essere abilitata per il riquadro hello.  Ciò fornisce un messaggio alternativo se non sono disponibili per il riquadro hello dati.  Si tooprovide in genere utilizzato un messaggio hello temporanea quando è installato Vista hello e dati disponibili. |
| Query |Eseguire una query toorun toocheck se sono disponibili dati per la visualizzazione hello.  Se la query hello non restituisce alcun risultato, anziché il valore di hello dalla query principale hello viene visualizzato un messaggio. |
| Message |Messaggio toodisplay se query di verifica del flusso di dati hello non restituisce dati.  Se non si specifica alcun messaggio, viene visualizzato *Esecuzione della valutazione*. |


## <a name="two-numbers-tile"></a>Riquadro Due numeri
Hello **numero due** riquadro Visualizza due numeri con hello conteggi di record da un'etichetta e due query di log diverso.

![Riquadro Due numeri](media/log-analytics-view-designer/tile-two-numbers.png)

| Impostazione | Description |
|:--- |:--- |
| Nome |Riquadro testo toodisplay nella parte superiore di hello di hello. |
| Descrizione |Testo toodisplay sotto il nome di sezione hello. |
| **Primo riquadro** | |
| Legenda |Testo toodisplay in valore hello. |
| Query |Eseguire una query toorun.  verrà visualizzato il conteggio di Hello del numero di hello di record restituiti dalla query hello. |
| **Secondo riquadro** | |
| Legenda |Testo toodisplay in valore hello. |
| Query |Eseguire una query toorun.  verrà visualizzato il conteggio di Hello del numero di hello di record restituiti dalla query hello. |
| **Funzionalità avanzate** |**&gt; Verifica del flusso di dati** |
| Enabled |Selezionare se la verifica del flusso di dati deve essere abilitata per il riquadro hello.  Ciò fornisce un messaggio alternativo se non sono disponibili per il riquadro hello dati.  Si tooprovide in genere utilizzato un messaggio hello temporanea quando è installato Vista hello e dati disponibili. |
| Query |Eseguire una query toorun toocheck se sono disponibili dati per la visualizzazione hello.  Se la query hello non restituisce alcun risultato, anziché il valore di hello dalla query principale hello viene visualizzato un messaggio. |
| Message |Messaggio toodisplay se query di verifica del flusso di dati hello non restituisce dati.  Se non si specifica alcun messaggio, viene visualizzato *Esecuzione della valutazione*. |


## <a name="donut-tile"></a>Riquadro Anello
Hello **anello** riquadro Visualizza un singolo numero riepilogato da una colonna del valore in una query log.  anello Hello graficamente i risultati di tre record hello superiore.

![Riquadro Anello](media/log-analytics-view-designer/tile-donut.png)

| Impostazione | Description |
|:--- |:--- |
| Nome |Riquadro testo toodisplay nella parte superiore di hello di hello. |
| Descrizione |Testo toodisplay sotto il nome di sezione hello. |
| **Anello** | |
| Query |Eseguire una query toorun per anello hello.  proprietà prima di Hello deve essere un valore e hello secondo proprietà text un valore numerico.  In genere si tratta di una query che utilizza hello **misura** risultati toosummarize (parola chiave). |
| **Anello** |**> Centro** |
| Text |Testo toodisplay in valore hello all'interno di hello anello. |
| Operazione |Hello operazione tooperform su hello valore proprietà toosummarize tooa un singolo valore.<br><br>-Somma: Aggiungere i valori hello di tutti i record con valore della proprietà hello.<br>-Percentuale: Percentuale di valori hello sommato dai record con hello proprietà valore confrontato toohello sommati i valori di tutti i record. |
| I valori dei risultati usati nell'operazione centrale |Facoltativamente, fare clic su hello segno tooadd uno o più valori.  risultati di Hello di hello query sarà limitato toorecords con valori di proprietà hello specificati.  Se nessun valore vengono aggiunti, rispetto a tutti i record sono inclusi nella query hello. |
| **Anello** |**> Opzioni aggiuntive** |
| Colori |Hello toodisplay di colore per ogni proprietà hello tre superiore.  Se si desidera toospecify alternativo colori per i valori di proprietà specifico, utilizzare avanzate del Mapping di colore. |
| Mappa colori avanzata |Visualizza un colore per valori di proprietà specifici.  Se il valore di hello specificato si trova in hello tre superiore, quindi viene visualizzato il colore alternativo hello anziché colori standard hello.  Se la proprietà hello non è hello tre superiore, quindi colori hello non viene visualizzata. |
| **Funzionalità avanzate** |**&gt; Verifica del flusso di dati** |
| Enabled |Selezionare se la verifica del flusso di dati deve essere abilitata per il riquadro hello.  Ciò fornisce un messaggio alternativo se non sono disponibili per il riquadro hello dati.  Si tooprovide in genere utilizzato un messaggio hello temporanea quando è installato Vista hello e dati disponibili. |
| Query |Eseguire una query toorun toocheck se sono disponibili dati per la visualizzazione hello.  Se la query hello non restituisce alcun risultato, anziché il valore di hello dalla query principale hello viene visualizzato un messaggio. |
| Message |Messaggio toodisplay se query di verifica del flusso di dati hello non restituisce dati.  Se non si specifica alcun messaggio, viene visualizzato *Esecuzione della valutazione*. |


## <a name="line-chart-tile"></a>Riquadro Grafico a linee
Hello **grafico a linee** riquadro Visualizza un grafico a linee con più serie da una query del log nel tempo.  

![Riquadro Grafico a linee e callout](media/log-analytics-view-designer/tile-line-chart.png)

| Impostazione | Description |
|:--- |:--- |
| Nome |Riquadro testo toodisplay nella parte superiore di hello di hello. |
| Descrizione |Testo toodisplay sotto il nome di sezione hello. |
| **Grafico a linee** | |
| Query |Eseguire una query toorun per grafico a linee hello.  proprietà prima di Hello deve essere un valore e hello secondo proprietà text un valore numerico.  In genere si tratta di una query che utilizza hello **misura** risultati toosummarize (parola chiave).  Se la query hello utilizza hello **intervallo** (parola chiave), quindi hello asse x del grafico hello utilizzerà l'intervallo di tempo.  Se la query hello include hello **intervallo** intervalli (parola chiave), quindi ogni ora vengono utilizzati per hello asse x. |
| **Grafico a linee** |**> Asse Y** |
| Usa scala logaritmica |Selezionare toouse una scala logaritmica per hello asse y. |
| Unità |Specificare unità hello per i valori hello restituiti dalla query hello.  Queste informazioni sono etichette toodisplay utilizzati nel grafico hello che indica i tipi di valore hello e, facoltativamente, per la conversione di valori hello.  Hello **tipo di unità** specifica categoria di hello dell'unità hello e definisce hello **tipo unità corrente** valori disponibili.  Se si seleziona un valore in **convertire** quindi i valori numerici hello vengono convertiti da hello **unità corrente** digitare toohello **convertire** tipo. |
| Etichetta personalizzata |Testo toodisplay per etichetta successiva toohello hello asse Y per il tipo di unità di hello.  Se l'etichetta non è specificato, viene visualizzato solo il tipo di unità hello. |
| **Funzionalità avanzate** |**&gt; Verifica del flusso di dati** |
| Enabled |Selezionare se la verifica del flusso di dati deve essere abilitata per il riquadro hello.  Ciò fornisce un messaggio alternativo se non sono disponibili per il riquadro hello dati.  Si tooprovide in genere utilizzato un messaggio hello temporanea quando è installato Vista hello e dati disponibili. |
| Query |Eseguire una query toorun toocheck se sono disponibili dati per la visualizzazione hello.  Se la query hello non restituisce alcun risultato, anziché il valore di hello dalla query principale hello viene visualizzato un messaggio. |
| Message |Messaggio toodisplay se query di verifica del flusso di dati hello non restituisce dati.  Se non si specifica alcun messaggio, viene visualizzato *Esecuzione della valutazione*. |


## <a name="line-chart--callout-tile"></a>Riquadro Grafico a linee e callout
Hello **linea di callout & grafico** riquadro Visualizza un grafico a linee con più serie da una query del log nel tempo e un callout con un valore di riepilogo.  

![Riquadro Grafico a linee e callout](media/log-analytics-view-designer/tile-line-chart-callout.png)

| Impostazione | Description |
|:--- |:--- |
| Nome |Riquadro testo toodisplay nella parte superiore di hello di hello. |
| Descrizione |Testo toodisplay sotto il nome di sezione hello. |
| **Grafico a linee** | |
| Query |Eseguire una query toorun per grafico a linee hello.  proprietà prima di Hello deve essere un valore e hello secondo proprietà text un valore numerico.  In genere si tratta di una query che utilizza hello **misura** risultati toosummarize (parola chiave).  Se la query hello utilizza hello **intervallo** (parola chiave), quindi hello asse x del grafico hello utilizzerà l'intervallo di tempo.  Se la query hello include hello **intervallo** intervalli (parola chiave), quindi ogni ora vengono utilizzati per hello asse x. |
| **Grafico a linee** |**> Callout** |
| Callout |Toodisplay di testo titolo sopra il valore di callout hello. |
| Nome della serie |Valore della proprietà hello toouse di serie per il valore di callout hello.  Se non viene fornita alcun serie, vengono utilizzati tutti i record da query hello. |
| Operazione |Hello operazione tooperform hello valore toosummarize tooa singolo valore della proprietà per hello callout.<br>-Media: Media del valore di hello da tutti i record.<br><br>-Conteggio: Conteggio di tutti i record restituiti dalla query hello.<br>-Ultimo campione: Valore dall'ultimo intervallo di hello incluso nel grafico hello.<br>Max: Valore massimo da intervalli hello inclusi nel grafico hello.<br>: Min: Valore minimo da intervalli hello inclusi nel grafico hello.<br>-Somma: La somma del valore di hello da tutti i record. |
| **Grafico a linee** |**> Asse Y** |
| Usa scala logaritmica |Selezionare toouse una scala logaritmica per hello asse y. |
| Unità |Specificare unità hello per i valori hello restituiti dalla query hello.  Queste informazioni sono etichette toodisplay utilizzati nel grafico hello che indica i tipi di valore hello e, facoltativamente, per la conversione di valori hello.  Hello **tipo di unità** specifica categoria di hello dell'unità hello e definisce hello **tipo unità corrente** valori disponibili.  Se si seleziona un valore in **convertire** quindi i valori numerici hello vengono convertiti da hello **unità corrente** digitare toohello **convertire** tipo. |
| Etichetta personalizzata |Testo toodisplay per etichetta successiva toohello hello asse Y per il tipo di unità di hello.  Se l'etichetta non è specificato, viene visualizzato solo il tipo di unità hello. |
| **Funzionalità avanzate** |**&gt; Verifica del flusso di dati** |
| Enabled |Selezionare se la verifica del flusso di dati deve essere abilitata per il riquadro hello.  Ciò fornisce un messaggio alternativo se non sono disponibili per il riquadro hello dati.  Si tooprovide in genere utilizzato un messaggio hello temporanea quando è installato Vista hello e dati disponibili. |
| Query |Eseguire una query toorun toocheck se sono disponibili dati per la visualizzazione hello.  Se la query hello non restituisce alcun risultato, anziché il valore di hello dalla query principale hello viene visualizzato un messaggio. |
| Message |Messaggio toodisplay se query di verifica del flusso di dati hello non restituisce dati.  Se non si specifica alcun messaggio, viene visualizzato *Esecuzione della valutazione*. |


## <a name="two-timelines-tile"></a>Riquadro Due sequenze temporali
Hello **due sequenze temporali** riquadro Visualizza i risultati di hello di due query log nel tempo come istogramma.  Viene visualizzato un callout per ogni serie.  

![Riquadro Due sequenze temporali](media/log-analytics-view-designer/tile-two-timelines.png)

| Impostazione | Description |
|:--- |:--- |
| Nome |Riquadro testo toodisplay nella parte superiore di hello di hello. |
| Descrizione |Testo toodisplay sotto il nome di sezione hello. |
| Primo grafico | |
| Legenda |Testo toodisplay in didascalia hello prima serie hello. |
| Colore |Toouse di colore per le colonne di hello prima serie hello. |
| Query grafico |Eseguire una query toorun prima serie hello.  conteggio di Hello del numero di hello di record in ogni intervallo di tempo rappresentato da colonne del grafico hello. |
| Operazione |Hello operazione tooperform hello valore toosummarize tooa singolo valore della proprietà per hello callout.<br><br>-Media: Media del valore di hello da tutti i record.<br>-Conteggio: Conteggio di tutti i record restituiti dalla query hello.<br>-Ultimo campione: Valore dall'ultimo intervallo di hello incluso nel grafico hello.<br>Max: Valore massimo da intervalli hello inclusi nel grafico hello. |
| **Secondo grafico** | |
| Legenda |Testo toodisplay in hello callout per la seconda serie hello. |
| Colore |Toouse di colore per le colonne di hello nella seconda serie hello. |
| Query grafico |Eseguire una query toorun per la seconda serie hello.  conteggio di Hello del numero di hello di record in ogni intervallo di tempo rappresentato da colonne del grafico hello. |
| Operazione |Hello operazione tooperform hello valore toosummarize tooa singolo valore della proprietà per hello callout.<br><br>-Media: Media del valore di hello da tutti i record.<br>-Conteggio: Conteggio di tutti i record restituiti dalla query hello.<br>-Ultimo campione: Valore dall'ultimo intervallo di hello incluso nel grafico hello.<br>Max: Valore massimo da intervalli hello inclusi nel grafico hello. |
| **Funzionalità avanzate** |**&gt; Verifica del flusso di dati** |
| Enabled |Selezionare se la verifica del flusso di dati deve essere abilitata per il riquadro hello.  Ciò fornisce un messaggio alternativo se non sono disponibili per il riquadro hello dati.  Si tooprovide in genere utilizzato un messaggio hello temporanea quando è installato Vista hello e dati disponibili. |
| Query |Eseguire una query toorun toocheck se sono disponibili dati per la visualizzazione hello.  Se la query hello non restituisce alcun risultato, anziché il valore di hello dalla query principale hello viene visualizzato un messaggio. |
| Message |Messaggio toodisplay se query di verifica del flusso di dati hello non restituisce dati.  Se non si specifica alcun messaggio, viene visualizzato *Esecuzione della valutazione*. |


## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [log ricerche](log-analytics-log-searches.md) query hello toosupport nei riquadri.
* Aggiungere [visualizzazione parti](log-analytics-view-designer-parts.md) tooyour di visualizzazione personalizzata.
