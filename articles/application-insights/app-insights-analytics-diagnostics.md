---
title: diagnostica aaaSmart delle modifiche delle prestazioni di app web in Azure Application Insights | Documenti Microsoft
description: Diagnosi automatica di modifiche improvvise nella telemetria delle prestazioni da parte di un'app web.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a>Diagnosticare modifiche improvvise nella telemetria dell'app

*Questa funzionalità è in anteprima.*

Diagnosticare modifiche improvvise delle prestazioni e dell'uso dell'app Web con un solo clic. funzionalità di diagnostica Smart Hello è disponibile quando si crea un grafico temporale nella [Analitica](app-insights-analytics.md) in [Application Insights](app-insights-overview.md). In caso di una modifica insolita dalla tendenza hello dei risultati, ad esempio un picco o un dip, diagnostica Smart identifica il pattern di dimensioni e i valori correlati che potrebbero spiegare modifica hello. Ciò consente di diagnosticare il problema di hello rapidamente. 

In questo esempio, diagnostica Smart ha identificato un modello di valori di proprietà associato modifica hello e viene evidenziata hello differenza tra i risultati con e senza tale modello:

![Risultato di esempio della diagnostica di Analytics](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a>Diagnosticare le modifiche ai dati

1.  Eseguire una query in Analytics e creare un grafico del tempo. 
2.  Fare clic su qualsiasi punto di picco evidenziato, se presente.
 
    ![Punto di picco](./media/app-insights-analytics-diagnostics/peak.png)

    Diagnostica richiede pochi secondi toodiscover un modello.

3. scheda dei risultati diagnostica Hello Mostra un modello che può spiegare i discontinuità di dati.

    ![risultato](./media/app-insights-analytics-diagnostics/result.png)
 
    testo Hello Mostra i valori delle dimensioni hello visualizzati toocorrelate con il tasto MAIUSC hello. In questo esempio, lo spostamento è associato a una determinata richiesta e a una versione particolare del browser.

    Si noti inoltre componenti hello due grafico hello, con hello filtro true e false. componente false Hello Mostra una tendenza subisce modifica. In altre parole, è invariato nei risultati di telemetria hello, se si esclude hello problematico combinazione dimensioni identificati diagnostica. Al contrario, i risultati di hello all'interno di tale combinazione mostrano notevoli modifiche nell'area di hello evidenziato di analisi. Questo indica che la diagnostica è disponibile una combinazione di proprietà che spiega modifica hello.

4.  Se il modello di hello è complesso, è necessario toohover su **Mostra tutto** dimensioni hello toosee.

    ![Mostra tutto](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  In caso di diagnostica consente di trovare alcun toonotify modello significativo su, verrà visualizzata la pagina "Nessun risultato" hello. A questo punto, è possibile modificare la query. Ad esempio, è possibile limitare l'ambito intervallo di tempo hello e binning nella query Analitica, per un'ulteriore analisi e potenzialmente migliori risultati.

Grazie a informazioni hello che una determinata pagina del sito Web disponga di un problema in un determinato browser, è possibile passare pagina problema toohello retta e provare a utilizzare le modifiche recenti.

## <a name="try-hello-demo"></a>Provare la demo hello

[Fare clic qui toosee una dimostrazione](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) su dati di esempio.

## <a name="how-it-works"></a>Funzionamento

Diagnostica smart utilizza un algoritmo di apprendimento non supervisionato avanzato basato su hello [DiffPatterns](app-insights-analytics-reference.md) operazione. La ricerca di modelli candidati che potrebbero spiegare hello modifica dei dati. Analizza l'impatto di hello di ciascun candidato metrica hello e Mostra il modello di hello che mette in correlazione migliore con modifica hello.

## <a name="no-diagnostic-points"></a>Nessun punto di diagnostica?

Diagnostica smart funziona solo quando viene soddisfatte hello seguenti criteri:

 * L'impostazione Smart Diagnostics è attivata. Guarda sotto l'icona di impostazioni hello in Analitica.
 * opzione Smart diagnostica nelle impostazioni Analitica Hello è selezionata. 
 * Asse temporale: hello asse x del grafico hello deve essere di tipo `datetime`.
 * Grafico a linee o ad area: la diagnostica funziona solo con questi tipi di grafico. Utilizzare `| render timechart` o `| render areachart` alla fine della query; hello o selezionare grafico a linee o Area dal selettore di hello elenco a discesa.
 * Discontinuità: Deve esistere una discontinuità significativa nei dati hello.
 * Tooanalyze di punti sufficiente.
 * Non più di un riepilogo di clausola di query hello.
 * Nessuna clausola del progetto che contiene una definizione di nome prima di hello riepilogare clausola.

 
 ## <a name="related-articles"></a>Articoli correlati

 * [Esercitazione su Analisi](app-insights-analytics-tour.md)
 * [Rilevamento smart](app-insights-proactive-diagnostics.md) utente viene avvisato automaticamente tooperformance problemi.
