---
title: riferimento aaaPart per Progettazione viste in OMS Log Analitica | Documenti Microsoft
description: Visualizza finestra di progettazione nel Log Analitica consente toocreate personalizzato visualizzazioni nella console OMS hello contenenti visualizzazioni diverse dei dati nel repository OMS hello. Questo articolo fornisce informazioni di riferimento sulle impostazioni di hello per ognuna delle hello visualizzazione parti toouse disponibili nelle visualizzazioni personalizzate.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 5718d620-b96e-4d33-8616-e127ee9379c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 6a19a451cf4cefd2fa5c94e6f61d812c4f820f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-visualization-part-reference"></a>Riferimento alla parte di visualizzazione relativa a Progettazione viste di Log Analytics
Visualizza finestra di progettazione nel Log Analitica Hello consente toocreate le visualizzazioni personalizzate nella console OMS hello contenenti visualizzazioni diverse dei dati dal repository OMS hello. Questo articolo fornisce informazioni di riferimento sulle impostazioni di hello per ognuna delle hello visualizzazione parti toouse disponibili nelle visualizzazioni personalizzate.

Altri articoli disponibili su Progettazione viste sono:

* [Visualizzare Progettazione](log-analytics-view-designer.md) -Panoramica hello Progettazione viste e procedure per la creazione e modifica delle visualizzazioni personalizzate.
* [Riquadro riferimento](log-analytics-view-designer-tiles.md) -riferimento delle impostazioni di hello per ognuna delle hello riquadri toouse disponibili nelle visualizzazioni personalizzate.

>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), le query in tutte le visualizzazioni devono essere scritti in hello [nuovo linguaggio di query](https://go.microsoft.com/fwlink/?linkid=856078).  Le viste che sono state create prima dell'area di lavoro di hello è stato aggiornato sarà venga convertito.

Hello nella tabella seguente vengono descritti hello diversi tipi di riquadri disponibili in hello Visualizza finestra di progettazione.  Hello nelle sezioni seguenti vengono descrivono ogni tipo di riquadro nel dettaglio e le relative proprietà.

| Tipo di visualizzazione | Descrizione |
|:--- |:--- |
| [Elenco di query](#list-of-queries-part) |Visualizza l'elenco delle query di ricerca log.  Hello utente può fare clic su ogni toodisplay query i risultati. |
| [Numero ed elenco](#number-amp-list-part) |L'intestazione presenta un numero singolo che mostra il conteggio dei record risultanti da una query di ricerca log.  Elenco Visualizza hello primi dieci risultati da una query con un grafico che indica il valore relativo di hello di una colonna numerica o la variazione nel tempo. |
| [Due numeri ed elenco](#two-numbers-amp-list-part) |L'intestazione presenta due numeri che mostrano il conteggio dei record risultanti da query di ricerca log separate.  Elenco Visualizza hello primi dieci risultati da una query con un grafico che indica il valore relativo di hello di una colonna numerica o la variazione nel tempo. |
| [Anello ed elenco](#donut-amp-list-part) |Nell'intestazione viene visualizzato un singolo numero riepilogato da una colonna di valore in una query di log.  anello Hello graficamente i risultati di tre record hello superiore. |
| [Due sequenze temporali ed elenco](#two-timelines-amp-list-part) |Visualizza intestazione hello i risultati di due query nel tempo come istogramma con una didascalia di visualizzazione di un singolo numero riepilogati da una colonna del valore in una query log.  Elenco Visualizza hello primi dieci risultati da una query con un grafico che indica il valore relativo di hello di una colonna numerica o la variazione nel tempo. |
| [Informazioni](#information-part) |L'intestazione mostra il testo statico e un collegamento opzionale.  L'elenco mostra uno o più elementi con titolo e testo statico. |
| [Grafico a linee, callout ed elenco](#line-chart-callout-amp-list-part) |Nell'intestazione viene visualizzato un grafico a linee con più serie provenienti da una query di log nel tempo e un callout con un valore riepilogato.  Elenco Visualizza hello primi dieci risultati da una query con un grafico che indica il valore relativo di hello di una colonna numerica o la variazione nel tempo. |
| [Grafico a linee ed elenco](#line-chart-amp-list-part) |Nell'intestazione viene visualizzato un grafico a linee con più serie provenienti da una query di log nel tempo.  Elenco Visualizza hello primi dieci risultati da una query con un grafico che indica il valore relativo di hello di una colonna numerica o la variazione nel tempo. |
| [Parte relativa allo stack dei grafici a linee](#stack-of-line-charts-part) |Vengono visualizzati grafici a linee con più serie provenienti da una query di log nel tempo. |

## <a name="list-of-queries-part"></a>Parte relativa all'elenco delle query
Visualizza l'elenco delle query di ricerca log.  Hello utente può fare clic su ogni toodisplay query i risultati.  Hello vista includerà una singola query per impostazione predefinita, e che è possibile fare clic su **+ Query** tooadd altre query.

![Visualizzazione dell'elenco delle query](media/log-analytics-view-designer/view-list-queries.png)

| Impostazione | Descrizione |
|:--- |:--- |
| **Generale** | |
| Titolo |Toodisplay di testo nella parte superiore di hello della vista hello. |
| Nuovo gruppo |Selezionare toocreate un nuovo gruppo nella visualizzazione di hello a partire da vista corrente hello. |
| Filtri preselezionati |Elenco di proprietà tooinclude nel riquadro sinistro filtro hello è delimitato da virgole hello selezione di una query. |
| Modalità di rendering |Visualizzazione iniziale visualizzata quando si seleziona query hello.  utente Hello è possibile selezionare le viste disponibili dopo l'apertura di query hello. |
| **Query** | |
| Query di ricerca |Eseguire una query toorun. |
| Nome descrittivo |Nome descrittivo di hello query toodisplay toohello sull'utente. |

## <a name="number--list-part"></a>Parte relativa al numero e all'elenco
L'intestazione presenta un numero singolo che mostra il conteggio dei record risultanti da una query di ricerca log.  Elenco Visualizza hello primi dieci risultati da una query con un grafico che indica il valore relativo di hello di una colonna numerica o la variazione nel tempo.

![Visualizzazione dell'elenco delle query](media/log-analytics-view-designer/view-number-list.png)

| Impostazione | Descrizione |
|:--- |:--- |
| **Generale** | |
| Titolo gruppo |Toodisplay di testo nella parte superiore di hello della vista hello. |
| Nuovo gruppo |Selezionare toocreate un nuovo gruppo nella visualizzazione di hello a partire da vista corrente hello. |
| Icona |Immagine file toodisplay toohello risultato successivo nell'intestazione di hello. |
| Usa icona |Selezionare la visualizzazione dell'icona di toohave hello. |
| **Titolo** | |
| Legenda |Toodisplay di testo nella parte superiore di hello dell'intestazione hello. |
| Query |Eseguire una query toorun per intestazione hello.  verrà visualizzato il conteggio di Hello del numero di hello di record restituiti dalla query hello. |
| **Elenco** | |
| Query |Eseguire una query toorun per elenco hello.  Hello prime due proprietà per hello primi dieci record nei risultati di hello verranno visualizzate.  proprietà prima di Hello deve essere un valore e hello secondo proprietà text un valore numerico.  Le barre vengono create automaticamente in base a hello valore relativo di una colonna numerica hello.<br><br>Utilizzare il comando di ordinamento hello hello query toosort hello record hello elenco.  Consente di Hello vedere hello toorun tutte le query e restituire tutti i record. |
| Nascondi grafico |Selezionare toodisable hello grafico toohello diritto di colonna numerica hello. |
| Abilita grafici sparkline |Selezionare grafico sparkline toodisplay anziché una barra orizzontale.  Per i dettagli, vedere le [impostazioni comuni](#sparklines). |
| Colore |Colore delle barre di hello o grafici sparkline. |
| Nome e separatore valori |Delimitatore carattere singolo Se si desidera proprietà text di tooparse hello in più valori.  Per i dettagli, vedere le [impostazioni comuni](#name-value-separator). |
| Query di navigazione |Eseguire una query toorun hello selezione di un elemento nell'elenco di hello.  Per i dettagli, vedere le [impostazioni comuni](#navigation-query). |
| **Elenco** |**&gt; Titoli di colonna** |
| Nome |Toodisplay di testo nella parte superiore di hello della prima colonna hello dell'elenco di hello. |
| Valore |Toodisplay di testo nella parte superiore di hello della seconda colonna hello dell'elenco di hello. |
| **Elenco** |**&gt; Thresholds** (Soglie) |
| Abilitare le soglie |Selezionare tooenable soglie.  Per i dettagli, vedere le [impostazioni comuni](#thresholds). |

## <a name="two-numbers--list-part"></a>Parte relativa a Due numeri e all'elenco
L'intestazione presenta due numeri che mostrano il conteggio dei record risultanti da query di ricerca log separate.  Elenco Visualizza hello primi dieci risultati da una query con un grafico che indica il valore relativo di hello di una colonna numerica o la variazione nel tempo.

![Visualizzazione Due numeri ed elenco](media/log-analytics-view-designer/view-two-numbers-list.png)

| Impostazione | Descrizione |
|:--- |:--- |
| **Generale** | |
| Titolo gruppo |Toodisplay di testo nella parte superiore di hello della vista hello. |
| Nuovo gruppo |Selezionare toocreate un nuovo gruppo nella visualizzazione di hello a partire da vista corrente hello. |
| Icona |Immagine file toodisplay toohello risultato successivo nell'intestazione di hello. |
| Usa icona |Selezionare la visualizzazione dell'icona di toohave hello. |
| **Titolo** | |
| Legenda |Toodisplay di testo nella parte superiore di hello dell'intestazione hello. |
| Query |Eseguire una query toorun per intestazione hello.  verrà visualizzato il conteggio di Hello del numero di hello di record restituiti dalla query hello. |
| **Elenco** | |
| Query |Eseguire una query toorun per elenco hello.  Hello prime due proprietà per hello primi dieci record nei risultati di hello verranno visualizzate.  proprietà prima di Hello deve essere un valore e hello secondo proprietà text un valore numerico.  Le barre vengono create automaticamente in base a hello valore relativo di una colonna numerica hello.<br><br>Utilizzare il comando di ordinamento hello hello query toosort hello record hello elenco.  Consente di Hello vedere hello toorun tutte le query e restituire tutti i record. |
| Nascondi grafico |Selezionare toodisable hello grafico toohello diritto di colonna numerica hello. |
| Abilita grafici sparkline |Selezionare grafico sparkline toodisplay anziché una barra orizzontale.  Per i dettagli, vedere le [impostazioni comuni](#sparklines). |
| Colore |Colore delle barre di hello o grafici sparkline. |
| Operazione |Operazione tooperform per grafico sparkline hello.  Per i dettagli, vedere le [impostazioni comuni](#sparklines). |
| Nome e separatore valori |Delimitatore carattere singolo Se si desidera proprietà text di tooparse hello in più valori.  Per i dettagli, vedere le [impostazioni comuni](#name-value-separator). |
| Query di navigazione |Eseguire una query toorun hello selezione di un elemento nell'elenco di hello.  Per i dettagli, vedere le [impostazioni comuni](#navigation-query). |
| **Elenco** |**&gt; Titoli di colonna** |
| Nome |Toodisplay di testo nella parte superiore di hello della prima colonna hello dell'elenco di hello. |
| Valore |Toodisplay di testo nella parte superiore di hello della seconda colonna hello dell'elenco di hello. |
| **Elenco** |**&gt; Thresholds** (Soglie) |
| Abilitare le soglie |Selezionare tooenable soglie.  Per i dettagli, vedere le [impostazioni comuni](#thresholds). |

## <a name="donut--list-part"></a>Parte relativa all'anello e all'elenco
Nell'intestazione viene visualizzato un singolo numero riepilogato da una colonna di valore in una query di log.  anello Hello graficamente i risultati di tre record hello superiore.

![Visualizzazione dell'anello e dell'elenco](media/log-analytics-view-designer/view-donut-list.png)

| Impostazione | Descrizione |
|:--- |:--- |
| **Generale** | |
| Titolo gruppo |Riquadro testo toodisplay nella parte superiore di hello di hello. |
| Nuovo gruppo |Selezionare toocreate un nuovo gruppo nella visualizzazione di hello a partire da vista corrente hello. |
| Icona |Immagine file toodisplay toohello risultato successivo nell'intestazione di hello. |
| Usa icona |Selezionare la visualizzazione dell'icona di toohave hello. |
| **Intestazione** | |
| Titolo |Toodisplay di testo nella parte superiore di hello dell'intestazione hello. |
| Sottotitolo |Testo toodisplay in hello titolo nella parte superiore di hello dell'intestazione hello. |
| **Anello** | |
| Query |Eseguire una query toorun per anello hello.  proprietà prima di Hello deve essere un valore e hello secondo proprietà text un valore numerico. |
| **Anello** |**> Centro** |
| Text |Testo toodisplay in valore hello all'interno di hello anello. |
| Operazione |Hello operazione tooperform su hello valore proprietà toosummarize tooa un singolo valore.<br><br>-Somma: Aggiungere i valori hello di tutti i record.<br>-Percentuale: Percentuale di record hello restituiti dai valori hello **comportare valori utilizzati nell'operazione center** toohello record totali nella query hello. |
| I valori dei risultati usati nell'operazione centrale |Facoltativamente, fare clic su hello segno tooadd uno o più valori.  risultati di Hello di hello query sarà limitato toorecords con valori di proprietà hello specificati.  Se non vengono aggiunto alcun valore, tutti i record sono inclusi nella query hello. |
| **Opzioni aggiuntive** |**&gt; Colors** (Colori) |
| Colore 1<br>Colore 2<br>Colore 3 |Selezionare il colore di hello per hello valori hello visualizzati nell'anello hello. |
| **Opzioni aggiuntive** |**> Advanced Color Mapping** (Mappa colori avanzata) |
| Valore campo |Nome di un campo di toodisplay hello del tipo come un colore diverso se è incluso nell'anello hello. |
| Colore |Selezionare il colore di hello per campo univoco hello. |
| **Elenco** | |
| Query |Eseguire una query toorun per elenco hello.  verrà visualizzato il conteggio di Hello del numero di hello di record restituiti dalla query hello. |
| Nascondi grafico |Selezionare toodisable hello grafico toohello diritto di colonna numerica hello. |
| Abilita grafici sparkline |Selezionare grafico sparkline toodisplay anziché una barra orizzontale.  Per i dettagli, vedere le [impostazioni comuni](#sparklines). |
| Colore |Colore delle barre di hello o grafici sparkline. |
| Operazione |Operazione tooperform per grafico sparkline hello.  Per i dettagli, vedere le [impostazioni comuni](#sparklines). |
| Nome e separatore valori |Delimitatore carattere singolo Se si desidera proprietà text di tooparse hello in più valori.  Per i dettagli, vedere le [impostazioni comuni](#name-value-separator). |
| Query di navigazione |Eseguire una query toorun hello selezione di un elemento nell'elenco di hello.  Per i dettagli, vedere le [impostazioni comuni](#navigation-query). |
| **Elenco** |**&gt; Titoli di colonna** |
| Nome |Toodisplay di testo nella parte superiore di hello della prima colonna hello dell'elenco di hello. |
| Valore |Toodisplay di testo nella parte superiore di hello della seconda colonna hello dell'elenco di hello. |
| **Elenco** |**&gt; Thresholds** (Soglie) |
| Abilitare le soglie |Selezionare tooenable soglie.  Per i dettagli, vedere le [impostazioni comuni](#thresholds). |

## <a name="two-timelines--list-part"></a>parte relativa alle due sequenze temporali e all'elenco
Visualizza intestazione hello i risultati di due query nel tempo come istogramma con una didascalia di visualizzazione di un singolo numero riepilogati da una colonna del valore in una query log.  Elenco Visualizza hello primi dieci risultati da una query con un grafico che indica il valore relativo di hello di una colonna numerica o la variazione nel tempo.

![Visualizzazione di due sequenze temporali e dell'elenco](media/log-analytics-view-designer/view-two-timelines-list.png)

| Impostazione | Descrizione |
|:--- |:--- |
| **Generale** | |
| Titolo gruppo |Riquadro testo toodisplay nella parte superiore di hello di hello. |
| Nuovo gruppo |Selezionare toocreate un nuovo gruppo nella visualizzazione di hello a partire da vista corrente hello. |
| Icona |Immagine file toodisplay toohello risultato successivo nell'intestazione di hello. |
| Usa icona |Selezionare la visualizzazione dell'icona di toohave hello. |
| **Primo grafico<br>Secondo grafico** | |
| Legenda |Testo toodisplay in didascalia hello prima serie hello. |
| Colore |Toouse di colore per le colonne di hello in serie hello. |
| Query |Eseguire una query toorun prima serie hello.  conteggio di Hello del numero di hello di record in ogni intervallo di tempo rappresentato da colonne del grafico hello. |
| Operazione |Hello operazione tooperform hello valore toosummarize tooa singolo valore della proprietà per hello callout.<br><br>-Somma: La somma del valore di hello da tutti i record.<br>-Media: Media del valore di hello da tutti i record.<br>-Ultimo campione: Valore dall'ultimo intervallo di hello incluso nel grafico hello.<br>-Esempio first: Valore dal primo intervallo di hello incluso nel grafico hello.<br>-Conteggio: Conteggio di tutti i record restituiti dalla query hello. |
| **Elenco** | |
| Query |Eseguire una query toorun per elenco hello.  verrà visualizzato il conteggio di Hello del numero di hello di record restituiti dalla query hello. |
| Nascondi grafico |Selezionare toodisable hello grafico toohello diritto di colonna numerica hello. |
| Abilita grafici sparkline |Selezionare grafico sparkline toodisplay anziché una barra orizzontale.  Per i dettagli, vedere le [impostazioni comuni](#sparklines). |
| Colore |Colore delle barre di hello o grafici sparkline. |
| Operazione |Operazione tooperform per grafico sparkline hello.  Per i dettagli, vedere le [impostazioni comuni](#sparklines). |
| Query di navigazione |Eseguire una query toorun hello selezione di un elemento nell'elenco di hello.  Per i dettagli, vedere le [impostazioni comuni](#navigation-query). |
| **Elenco** |**&gt; Titoli di colonna** |
| Nome |Toodisplay di testo nella parte superiore di hello della prima colonna hello dell'elenco di hello. |
| Valore |Toodisplay di testo nella parte superiore di hello della seconda colonna hello dell'elenco di hello. |
| **Elenco** |**&gt; Thresholds** (Soglie) |
| Abilitare le soglie |Selezionare tooenable soglie.  Per i dettagli, vedere le [impostazioni comuni](#thresholds). |

## <a name="information-part"></a>Parte relativa alle informazioni
L'intestazione mostra il testo statico e un collegamento opzionale.  L'elenco mostra uno o più elementi con titolo e testo statico.

![Visualizzazione delle informazioni](media/log-analytics-view-designer/view-information.png)

| Impostazione | Descrizione |
|:--- |:--- |
| **Generale** | |
| Titolo gruppo |Riquadro testo toodisplay nella parte superiore di hello di hello. |
| Nuovo gruppo |Selezionare toocreate un nuovo gruppo nella visualizzazione di hello a partire da vista corrente hello. |
| Colore |Colore di sfondo per l'intestazione hello. |
| **Intestazione** | |
| Image |Toodisplay file di immagine nell'intestazione di hello. |
| Etichetta |Toodisplay testo nell'intestazione di hello. |
| **Intestazione** |**&gt; Collegamento** |
| Etichetta |Testo del collegamento. |
| Url |URL del collegamento. |
| **Elementi informazione** | |
| Titolo |Toodisplay testo del titolo di ogni elemento. |
| Content |Toodisplay di testo per ogni elemento. |

## <a name="line-chart-callout--list-part"></a>Parte relativa al grafico a linee, al callout e all'elenco
Nell'intestazione viene visualizzato un grafico a linee con più serie provenienti da una query di log nel tempo e un callout con un valore riepilogato.  Elenco Visualizza hello primi dieci risultati da una query con un grafico che indica il valore relativo di hello di una colonna numerica o la variazione nel tempo.

![Visualizzazione del grafico a linee, del callout e dell'elenco](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| Impostazione | Descrizione |
|:--- |:--- |
| **Generale** | |
| Titolo gruppo |Riquadro testo toodisplay nella parte superiore di hello di hello. |
| Nuovo gruppo |Selezionare toocreate un nuovo gruppo nella visualizzazione di hello a partire da vista corrente hello. |
| Icona |Immagine file toodisplay toohello risultato successivo nell'intestazione di hello. |
| Usa icona |Selezionare la visualizzazione dell'icona di toohave hello. |
| **Intestazione** | |
| Titolo |Toodisplay di testo nella parte superiore di hello dell'intestazione hello. |
| Sottotitolo |Testo toodisplay in hello titolo nella parte superiore di hello dell'intestazione hello. |
| **Grafico a linee** | |
| Query |Eseguire una query toorun per grafico a linee hello.  proprietà prima di Hello deve essere un valore e hello secondo proprietà text un valore numerico.  In genere si tratta di una query che utilizza hello **misura** risultati toosummarize (parola chiave).  Se la query hello utilizza hello **intervallo** (parola chiave), quindi hello asse x del grafico hello utilizzerà l'intervallo di tempo.  Se la query hello include hello **intervallo** intervalli (parola chiave), quindi ogni ora vengono utilizzati per hello asse x. |
| **Grafico a linee** |**> Callout** |
| Titolo del callout |Testo toodisplay sopra il valore di callout hello. |
| Nome della serie |Valore della proprietà hello toouse di serie per il valore di callout hello.  Se non viene fornita alcun serie, vengono utilizzati tutti i record da query hello. |
| Operazione |Hello operazione tooperform hello valore toosummarize tooa singolo valore della proprietà per hello callout.<br><br>-Media: Media del valore di hello da tutti i record.<br>-Conteggio conteggio di tutti i record restituiti dalla query hello.<br>-Ultimo campione: Valore dall'ultimo intervallo di hello incluso nel grafico hello.<br>Max: Valore massimo da intervalli hello inclusi nel grafico hello.<br>: Min: Valore minimo da intervalli hello inclusi nel grafico hello.<br>-Somma: La somma del valore di hello da tutti i record. |
| **Grafico a linee** |**> Asse Y** |
| Usa scala logaritmica |Selezionare toouse una scala logaritmica per hello asse y. |
| Unità |Specificare unità hello per i valori hello restituiti dalla query hello.  Queste informazioni sono etichette toodisplay utilizzati nel grafico hello che indica i tipi di valore hello e, facoltativamente, per la conversione di valori hello.  Hello tipo di unità specifica categoria di hello dell'unità hello e definisce i valori di tipo unità corrente hello che sono disponibili.  Se si seleziona un valore in Convert toothen hello numerico valori vengono convertiti da hello unità corrente tipo toohello Convert tootype. |
| Etichetta personalizzata |Testo toodisplay per etichetta successiva toohello hello asse Y per il tipo di unità di hello.  Se l'etichetta non è specificato, viene visualizzato solo il tipo di unità hello. |
| **Elenco** | |
| Query |Eseguire una query toorun per elenco hello.  verrà visualizzato il conteggio di Hello del numero di hello di record restituiti dalla query hello. |
| Nascondi grafico |Selezionare toodisable hello grafico toohello diritto di colonna numerica hello. |
| Abilita grafici sparkline |Selezionare grafico sparkline toodisplay anziché una barra orizzontale.  Per i dettagli, vedere le [impostazioni comuni](#sparklines). |
| Colore |Colore delle barre di hello o grafici sparkline. |
| Operazione |Operazione tooperform per grafico sparkline hello.  Per i dettagli, vedere le [impostazioni comuni](#sparklines). |
| Nome e separatore valori |Delimitatore carattere singolo Se si desidera proprietà text di tooparse hello in più valori.  Per i dettagli, vedere le [impostazioni comuni](#name-value-separator). |
| Query di navigazione |Eseguire una query toorun hello selezione di un elemento nell'elenco di hello.  Per i dettagli, vedere le [impostazioni comuni](#navigation-query). |
| **Elenco** |**&gt; Titoli di colonna** |
| Nome |Toodisplay di testo nella parte superiore di hello della prima colonna hello dell'elenco di hello. |
| Valore |Toodisplay di testo nella parte superiore di hello della seconda colonna hello dell'elenco di hello. |
| **Elenco** |**&gt; Thresholds** (Soglie) |
| Abilitare le soglie |Selezionare tooenable soglie.  Per i dettagli, vedere le [impostazioni comuni](#thresholds). |

## <a name="line-chart--list-part"></a>Parte relativa al grafico a linee e all'elenco
Nell'intestazione viene visualizzato un grafico a linee con più serie provenienti da una query di log nel tempo.  Elenco Visualizza hello primi dieci risultati da una query con un grafico che indica il valore relativo di hello di una colonna numerica o la variazione nel tempo.

![Visualizzazione del grafico a linee e dell'elenco](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| Impostazione | Descrizione |
|:--- |:--- |
| **Generale** | |
| Titolo gruppo |Riquadro testo toodisplay nella parte superiore di hello di hello. |
| Nuovo gruppo |Selezionare toocreate un nuovo gruppo nella visualizzazione di hello a partire da vista corrente hello. |
| Icona |Immagine file toodisplay toohello risultato successivo nell'intestazione di hello. |
| Usa icona |Selezionare la visualizzazione dell'icona di toohave hello. |
| **Intestazione** | |
| Titolo |Toodisplay di testo nella parte superiore di hello dell'intestazione hello. |
| Sottotitolo |Testo toodisplay in hello titolo nella parte superiore di hello dell'intestazione hello. |
| **Grafico a linee** | |
| Query |Eseguire una query toorun per grafico a linee hello.  proprietà prima di Hello deve essere un valore e hello secondo proprietà text un valore numerico.  In genere si tratta di una query che utilizza hello **misura** risultati toosummarize (parola chiave).  Se la query hello utilizza hello **intervallo** (parola chiave), quindi hello asse x del grafico hello utilizzerà l'intervallo di tempo.  Se la query hello include hello **intervallo** intervalli (parola chiave), quindi ogni ora vengono utilizzati per hello asse x. |
| **Grafico a linee** |**> Asse Y** |
| Usa scala logaritmica |Selezionare toouse una scala logaritmica per hello asse y. |
| Unità |Specificare unità hello per i valori hello restituiti dalla query hello.  Queste informazioni sono etichette toodisplay utilizzati nel grafico hello che indica i tipi di valore hello e, facoltativamente, per la conversione di valori hello.  Hello tipo di unità specifica categoria di hello dell'unità hello e definisce i valori di tipo unità corrente hello che sono disponibili.  Se si seleziona un valore in Convert toothen hello numerico valori vengono convertiti da hello unità corrente tipo toohello Convert tootype. |
| Etichetta personalizzata |Testo toodisplay per etichetta successiva toohello hello asse Y per il tipo di unità di hello.  Se l'etichetta non è specificato, viene visualizzato solo il tipo di unità hello. |
| **Elenco** | |
| Query |Eseguire una query toorun per elenco hello.  verrà visualizzato il conteggio di Hello del numero di hello di record restituiti dalla query hello. |
| Nascondi grafico |Selezionare toodisable hello grafico toohello diritto di colonna numerica hello. |
| Abilita grafici sparkline |Selezionare grafico sparkline toodisplay anziché una barra orizzontale.  Per i dettagli, vedere le [impostazioni comuni](#sparklines). |
| Colore |Colore delle barre di hello o grafici sparkline. |
| Operazione |Operazione tooperform per grafico sparkline hello.  Per i dettagli, vedere le [impostazioni comuni](#sparklines). |
| Nome e separatore valori |Delimitatore carattere singolo Se si desidera proprietà text di tooparse hello in più valori.  Per i dettagli, vedere le [impostazioni comuni](#name-value-separator). |
| Query di navigazione |Eseguire una query toorun hello selezione di un elemento nell'elenco di hello.  Per i dettagli, vedere le [impostazioni comuni](#navigation-query). |
| **Elenco** |**&gt; Titoli di colonna** |
| Nome |Toodisplay di testo nella parte superiore di hello della prima colonna hello dell'elenco di hello. |
| Valore |Toodisplay di testo nella parte superiore di hello della seconda colonna hello dell'elenco di hello. |
| **Elenco** |**&gt; Thresholds** (Soglie) |
| Abilitare le soglie |Selezionare tooenable soglie.  Per i dettagli, vedere le [impostazioni comuni](#thresholds). |

## <a name="stack-of-line-charts-part"></a>Stack dei grafici a linee
Vengono visualizzati grafici a linee con più serie provenienti da una query di log nel tempo.

![Stack dei grafici a linee](media/log-analytics-view-designer/view-stack-line-charts.png)

| Impostazione | Descrizione |
|:--- |:--- |
| **Generale** | |
| Titolo gruppo |Riquadro testo toodisplay nella parte superiore di hello di hello. |
| Nuovo gruppo |Selezionare toocreate un nuovo gruppo nella visualizzazione di hello a partire da vista corrente hello. |
| Icona |Immagine file toodisplay toohello risultato successivo nell'intestazione di hello. |
| **Grafico 1<br>Grafico 2<br>Grafico 3** |**&gt; Header** (Intestazione) |
| Titolo |Toodisplay di testo nella parte superiore di hello del grafico hello. |
| Sottotitolo |Testo toodisplay in hello titolo nella parte superiore di hello del grafico hello. |
| **Grafico 1<br>Grafico 2<br>Grafico 3** |**Grafico a linee** |
| Query |Eseguire una query toorun per grafico a linee hello.  proprietà prima di Hello deve essere un valore e hello secondo proprietà text un valore numerico.  In genere si tratta di una query che utilizza hello **misura** risultati toosummarize (parola chiave).  Se la query hello utilizza hello **intervallo** (parola chiave), quindi hello asse x del grafico hello utilizzerà l'intervallo di tempo.  Se la query hello include hello **intervallo** intervalli (parola chiave), quindi ogni ora vengono utilizzati per hello asse x. |
| **Grafico** |**> Asse Y** |
| Usa scala logaritmica |Selezionare toouse una scala logaritmica per hello asse y. |
| Unità |Specificare unità hello per i valori hello restituiti dalla query hello.  Queste informazioni sono etichette toodisplay utilizzati nel grafico hello che indica i tipi di valore hello e, facoltativamente, per la conversione di valori hello.  Hello tipo di unità specifica categoria di hello dell'unità hello e definisce i valori di tipo unità corrente hello che sono disponibili.  Se si seleziona un valore in Convert toothen hello numerico valori vengono convertiti da hello unità corrente tipo toohello Convert tootype. |
| Etichetta personalizzata |Testo toodisplay per etichetta successiva toohello hello asse Y per il tipo di unità di hello.  Se l'etichetta non è specificato, viene visualizzato solo il tipo di unità hello. |

## <a name="common-settings"></a>Impostazioni comuni
Hello le sezioni seguenti vengono descritte le parti comuni tooseveral visualizzazione impostazioni.

### <a name="name-value-separator">Nome e separatore valori</a>
Delimitatore carattere singolo Se si desidera proprietà text di hello tooparse da una query di elenco in più valori.  Se si specifica un delimitatore, è possibile fornire nomi per ogni campo separandoli hello stesso delimitatore nella casella Nome hello.

Si consideri, ad esempio, una proprietà denominata *Sede* nella quale vengono inclusi dei valori, come *Redmond-Building 41* e *Bellevue-Building12*.  È possibile specificare – per nome hello & valore separatore e *città compilazione* per hello Name.  Ciò comporterebbe l'analisi di ciascun valore in due proprietà chiamate *City* e *Building*.

### <a name="navigation-query">Query di navigazione</a>
Eseguire una query toorun hello selezione di un elemento nell'elenco di hello.  Utilizzare *{elemento selezionato}* sintassi hello tooinclude per elemento hello selezionato dall'utente.

Ad esempio, se hello query contengono una colonna denominata *Computer* e query di navigazione hello è *{elemento selezionato}*, una query, ad esempio *Computer = "MyComputer"* verrebbe eseguito quando Hello utente ha selezionato un computer.  Se la query di navigazione hello è *tipo = evento {elemento selezionato}* quindi query di hello *tipo Computer evento = = "MyComputer"* verrebbe eseguito.

### <a name="sparklines">Grafici sparkline</a>
Un grafico sparkline è un grafico a linee di piccole dimensioni che mostra il valore di hello di una voce di elenco nel tempo.  Per le parti di visualizzazione con un elenco, è possibile selezionare se toodisplay una barra orizzontale che indica il valore relativo di una colonna numerica di hello o un grafico sparkline che indica il valore nel tempo.

Hello nella tabella seguente vengono descritte le impostazioni di hello per i grafici sparkline.

| Impostazione | Description |
|:--- |:--- |
| Abilita grafici sparkline |Selezionare grafico sparkline toodisplay anziché una barra orizzontale. |
| Operazione |Se sono abilitati i grafici sparkline, si tratta di hello operazione tooperform su ogni proprietà hello elenco toocalculate hello i valori per grafico sparkline hello.<br><br>-Ultimo campione: Ultimo valore per la serie hello intervallo di tempo hello.<br>Max: Valore massimo per serie hello intervallo di tempo hello.<br>-Minimo: Valore minimo serie hello intervallo di tempo hello.<br>-Somma: Somma dei valori delle serie di hello intervallo di tempo hello.<br>-Summary: Usa hello stesso comando misura come query hello nell'intestazione di hello. |

### <a name="thresholds">Soglie</a>
Le soglie consentono toodisplay un elemento tooeach successivo icona colorata in un elenco è un indicatore visivo rapido di elementi che superano un determinato valore o rientrano in un intervallo specifico.  Ad esempio, è possibile visualizzare un'icona verde per gli elementi con un valore accettabile, il giallo se il valore di hello è all'interno di un intervallo che indica un avviso e rosso se supera un valore di errore.

Quando si abilitano le soglie, è necessario specificarne una o più.  Se il valore di hello di un elemento è minore del valore soglia Avanti hello e maggiore del valore soglia, viene utilizzato il colore.  Se l'elemento hello è maggiore del valore di soglia quindi più alta, tale colore è impostato.   

A ogni soglia è associato il valore **Default** (Predefinito).  Questo è il colore di hello impostato se nessun altro valore vengono superato.  È possibile aggiungere o rimuovere le soglie facendo hello  **+**  o **x** pulsante.

Hello nella tabella seguente vengono descritte le impostazioni di hello per soglie.

| Impostazione | Description |
|:--- |:--- |
| Abilitare le soglie |Selezionare toodisplay che toohello di icona un colore a sinistra di ogni valore che indica le soglie toospecified relativo relativa integrità. |
| Nome |Nome del valore di soglia hello tooidentify. |
| Soglia |Valore di soglia hello.  colore di integrità Hello per ciascun elemento dell'elenco è impostato toohello colori hello massimo valore di soglia superata dal valore dell'elemento hello.  È una soglia predefinita che rappresenta il colore di hello se nessun valore di soglia vengono superato. |
| Colore |Colore per il valore di soglia hello. |

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [log ricerche](log-analytics-log-searches.md) query hello toosupport in parti di visualizzazione.
