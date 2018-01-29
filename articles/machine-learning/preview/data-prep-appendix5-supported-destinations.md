---
title: Destinazioni di dati e output supportati disponibili per la preparazione dei dati di Azure Machine Learning | Microsoft Docs
description: Questo documento elenca tutte le destinazioni supportate e gli output disponibili per la preparazione dei dati di Azure Machine Learning
services: machine-learning
author: euangMS
ms.author: euang
manager: lanceo
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.custom: 
ms.devlang: 
ms.topic: article
ms.date: 09/07/2017
ms.openlocfilehash: 50d2d481b91199630bbfbf3cfdd21a1bf3062ff0
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2017
---
# <a name="supported-data-exports-for-this-preview"></a>Esportazioni di dati supportate per questa anteprima 
È possibile eseguire l'esportazione in diversi formati. Per conservare i risultati intermedi della preparazione dei dati prima dell'integrazione dei risultati nel restante flusso di lavoro di Machine Learning, è possibile usare questi formati.

## <a name="types"></a>Tipi 
### <a name="csv-file"></a>File CSV 
Scrivere un file con valori delimitati da virgole nella risorsa di archiviazione.

#### <a name="options"></a>Opzioni
- Terminazioni riga
- Sostituisci valori Null con
- Sostituisci errori con 
- Separatore


### <a name="parquet"></a>Parquet 
Scrivere un set di dati in un archivio come Parquet.

Il formato Parquet può avere forme diverse nella risorsa di archiviazione. Per i set di dati di dimensioni ridotte, viene usato a volte un file con estensione parquet singolo. Diverse librerie Python supportano la lettura e la scrittura in un singolo file con estensione parquet. 

Al momento, Azure Machine Learning Workbench si basa sulla raccolta Python PyArrow per la scrittura Parquet durante l'uso interattivo locale. Ciò significa che Parquet per singoli file è attualmente l'unico formato di output Parquet supportato durante l'uso interattivo locale.

Durante le esecuzioni con aumento del numero di istanze (in Spark), Azure Machine Learning Workbench fa uso delle funzionalità di lettura e scrittura Parquet di Spark. Il formato di output predefinito di Spark per Parquet, attualmente l'unico supportato, ha una struttura analoga a un set di dati Hive. Questo significa che una cartella contiene molti file con estensione parquet, ognuno dei quali è una partizione più piccola di un set di dati più grande. 

#### <a name="caveats"></a>Avvertenze 
Parquet come formato è relativamente recente e con alcune incoerenze di implementazione tra le diverse raccolte. Ad esempio, Spark specifica limitazioni sui caratteri validi nei nomi di colonne quando si esegue la scrittura in Parquet, a differenza di quanto accade con PyArrow. I caratteri seguenti non sono ammessi nei nomi di colonna: 
- ,
- ;
- {}
- ()
- \\n
- \\t
- =

>[!NOTE]
>- Per garantire la compatibilità con Spark, ogni volta che i dati vengono scritti in Parquet, le occorrenze di questi caratteri nei nomi di colonne vengono sostituite con un carattere di sottolineatura (_).
>- Per garantire la coerenza tra esecuzioni locali e con aumento del numero di istanze, tutti i dati scritti in Parquet, tramite l'app, Python o Spark, i nomi delle colonne devono essere purificati per la compatibilità con Spark. Per assicurare i nomi di colonna previsti quando si scrive in caratteri Parquet in Spark, il set non valido deve essere rimosso dalle colonne prima della scrittura.



## <a name="locations"></a>Località 
### <a name="local"></a>Local 
Posizione di archiviazione in rete mappata o in unità disco locale.

### <a name="azure-blob-storage"></a>Archivio BLOB di Azure
L'archivio BLOB di Azure richiede una sottoscrizione di Azure.

