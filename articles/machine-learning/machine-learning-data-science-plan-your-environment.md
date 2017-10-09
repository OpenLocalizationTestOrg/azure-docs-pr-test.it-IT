---
title: scenari di aaaIdentify e pianificare il processo analitica - Azure | Documenti Microsoft
description: Pianificare l'analisi avanzata prendendo in considerazione una serie di domande chiave.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 421520dd-7728-4d29-889c-ebe6a0a6fb07
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: e445973be0d020a4f9949e5c9d8554fbbd4b515f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooidentify-scenarios-and-plan-for-advanced-analytics-data-processing"></a>Come tooidentify scenari e pianificare avanzate analitica l'elaborazione di dati
Quali risorse è opportuno tooinclude quando l'impostazione di un ambiente toodo avanzate analitica l'elaborazione di un set di dati? In questo articolo suggerisce una serie di domande tooask che consentiranno di identificare le attività di hello e risorse pertinenti lo scenario. ordine di Hello dei passaggi di alto livello per analitica predittiva viene indicato [novità hello Team Data Science processo (TDSP)?](data-science-process-overview.md). Ognuno di questi passaggi richiederà risorse specifiche per uno scenario specifico di hello attività tooyour pertinente. chiave Hello domande tooidentify nel logistica dati il problema di uno scenario, caratteristiche, hello di qualità del set di dati, hello e strumenti hello e lingue si preferisce analysis hello toodo.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="logistic-questions-data-locations-and-movement"></a>Logistica: percorsi dei dati e spostamento
domande logistica Hello riguardano la posizione di hello di hello **origine dati**, hello **destinazione** in Azure e i requisiti per lo spostamento dei dati hello, incluse le risorse, quantità e la pianificazione di hello coinvolti. dati Hello potrebbe essere necessario spostare più volte durante il processo di analitica hello toobe. Uno scenario comune è toomove dati locali in una forma di archiviazione in Azure e quindi in Machine Learning Studio.

1. **Qual è l'origine dati?** È locale o nel cloud hello? ad esempio:
   
   * dati Hello sono pubblicamente disponibili all'indirizzo HTTP.
   * dati Hello risiedono in un percorso di file di rete locale.
   * dati Hello sono in un database di SQL Server.
   * Hello dati vengono archiviati in un contenitore di archiviazione di Azure
2. **Che cos'è Azure destinazione hello?** In cui necessita di toobe per l'elaborazione o la modellazione? ad esempio:
   
   * Archiviazione BLOB di Azure
   * Database SQL Azure
   * Macchine virtuali SQL Server in Azure
   * Tabelle Hive o HDInsight (Hadoop in Azure)
   * Azure Machine Learning
   * Dischi rigidi virtuali di Azure montabili.
3. **Come si prevede dati hello toomove?**  hello procedure e le risorse disponibili tooingest o caricare i dati in un'ampia gamma di archiviazione diversi e gli ambienti di elaborazione vengono illustrati nelle seguenti argomenti hello.
   
   * [Caricare i dati in ambienti di archiviazione per l'analisi](machine-learning-data-science-ingest-data.md)
   * [Importare dati di training in Azure Machine Learning Studio da varie origini dati](machine-learning-data-science-import-data.md).
4. **Dati hello necessita toobe spostati a intervalli regolari o modificati durante la migrazione?** Considerare l'utilizzo di Azure Data Factory (ADF) quando toobe esigenze dati migrati continuamente, in particolare se uno scenario ibrido per l'accesso sia in locale e le risorse cloud è coinvolto o quando dati hello supporta le transazioni o deve toobe modificato o logica di business aggiunto tooit nel corso di hello di viene eseguita la migrazione. Per ulteriori informazioni, vedere [spostare i dati da un tooSQL di server SQL Azure con Data Factory di Azure in locale](machine-learning-data-science-move-sql-azure-adf.md)
5. **La quantità di dati hello è spostato toobe tooAzure?** Set di dati molto grandi possono superare la capacità di archiviazione hello di alcuni ambienti. Per un esempio, vedere la discussione di hello dei limiti di dimensioni per Machine Learning Studio nella sezione successiva hello. In tali casi un campione di dati hello può essere utilizzato durante l'analisi di hello. Per informazioni dettagliate su come toodown-esempio un set di dati in vari ambienti Azure, vedere [campionare i dati nel processo di analisi scientifica dei dati di Team hello](machine-learning-data-science-sample-data.md).

## <a name="data-characteristics-questions-type-format-and-size"></a>Domande sulle caratteristiche dei dati: tipo, formato e dimensione
Queste domande sono tooplanning chiave di archiviazione e l'elaborazione, ognuno dei quali sono toovarious appropriati tipi di dati e ognuno dei quali si applicano alcune restrizioni.

1. **Quali sono i tipi di dati hello?** ad esempio:
   
   * Numerico
   * Categorical
   * Stringhe
   * Binary
2. **Come sono formattati i dati?** ad esempio:
   
   * File flat delimitati da virgole (CSV) o delimitati da tabulazioni (TSV)
   * Compressi o non compressi
   * BLOB di Azure
   * Tabelle Hive di Hadoop
   * Tabelle di SQL Server
3. **Quali sono le dimensioni dei dati?**
   
   * Piccole: meno di 2 GB
   * Medie: compresi tra 2 GB e 10 GB
   * Grandi: più di 10 GB

Si consideri ad esempio ambiente Azure Machine Learning Studio hello:

* Per un elenco dei formati di dati hello e i tipi supportati da Azure Machine Learning Studio, vedere [formati di dati e i tipi di dati supportati](machine-learning-data-science-import-data.md#data-formats-and-data-types-supported) sezione.
* Per informazioni sui limiti di dati per Azure Machine Learning Studio, vedere hello **come grandi set di dati hello è possibile per my i moduli?** sezione [importazione ed esportazione di dati per l'apprendimento automatico](machine-learning-faq.md#machine-learning-studio-questions)

Per informazioni sui limiti di hello di altri servizi Azure utilizzati nel processo di hello analitica, vedere [sottoscrizione Azure e limiti dei servizi, quote e vincoli](../azure-subscription-service-limits.md).

## <a name="data-quality-questions-exploration-and-pre-processing"></a>Domande sulla qualità dei dati: esplorazione e pre-elaborazione
1. **Quali sono le informazioni necessarie sui dati?** Esplorare i dati quando è necessario toogain un comprendere le caratteristiche di base. i modelli o le tendenze, gli outlier o gli eventuali valori mancanti. Questo passaggio è importante per determinare la portata hello di pre-elaborazione necessario per la formulazione di ipotesi che potrebbe suggerire funzionalità più appropriate hello o tipo di analisi e per la formulazione dei piani per la raccolta di dati aggiuntivi. Alcune tecniche utili per l'analisi dei dati consistono nel calcolare statistiche descrittive e tracciare visualizzazioni. Per informazioni dettagliate su come tooexplore un set di dati in vari ambienti Azure, vedere [esplorare i dati nel processo di analisi scientifica dei dati di Team hello](machine-learning-data-science-explore-data.md).
2. **Pre-elaborazione o la pulizia dei dati hello richiede correttamente?**
   La pre-elaborazione e la pulizia dei dati rappresentano attività importanti che in genere devono essere eseguite prima di poter usare un set di dati in modo efficace per Machine Learning. I dati non elaborati sono fastidiosi, non affidabili e potrebbero non contenere alcuni valori. Utilizzare tali dati per la modellazione può produrre risultati fuorvianti. Per una descrizione, vedere [tooprepare dati per l'apprendimento automatico migliorato attività](machine-learning-data-science-prepare-data.md).

## <a name="tools-and-languages-questions"></a>Domande su strumenti e linguaggi
Sono disponibili numerose opzioni a seconda dei linguaggi e degli strumenti o ambienti di sviluppo usati.

1. **Lingue cosa si preferisce toouse per l'analisi?**  
   
   * R
   * Python
   * SQL
2. **Quali strumenti usare per l'analisi dei dati?**
   
   * [Microsoft Azure Powershell](/powershell/azure/overview) -un linguaggio di scripting utilizzato tooadminister le risorse di Azure in un linguaggio di scripting.
   * [Azure Machine Learning Studio](machine-learning-what-is-ml-studio.md)
   * [Revolution Analytics](http://www.revolutionanalytics.com/revolution-r-open)
   * [RStudio](http://www.rstudio.com)
   * [Python Tools per Visual Studio](http://microsoft.github.io/PTVS/)
   * [Anaconda](https://www.continuum.io/why-anaconda)
   * [Notebook Jupyter](http://jupyter.org/)
   * [Microsoft Power BI](http://powerbi.microsoft.com)

## <a name="identify-your-advanced-analytics-scenario"></a>Identificare lo scenario di analisi avanzata
Dopo aver risposto alle domande hello nella sezione precedente di hello, si è pronti toodetermine lo scenario migliore adatta al caso. vengono descritti gli scenari di esempio Hello in [scenari per analitica avanzate in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md).

