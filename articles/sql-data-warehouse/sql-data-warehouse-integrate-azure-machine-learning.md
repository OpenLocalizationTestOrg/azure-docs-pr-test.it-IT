---
title: Azure Machine Learning con SQL Data Warehouse aaaUse | Documenti Microsoft
description: Suggerimenti per l'uso di Azure Machine Learning con Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a>Usare Azure Machine Learning con SQL Data Warehouse
Azure Machine Learning è un servizio completamente gestito analitica predittiva, che è possibile utilizzare modelli predittivi toocreate basati sui dati in SQL Data Warehouse e quindi pubblicare come servizi web pronto all'uso. È possibile apprendere nozioni di base di hello di analitica predittiva e machine learning leggendo [tooMachine introduzione di apprendimento in Azure][Introduction tooMachine Learning on Azure].  Sarà possibile apprendere come toocreate, eseguire il training, assegnare un punteggio e testare un modello di machine learning usando hello [crea esperimento esercitazione][Create experiment tutorial].

In questo articolo si apprenderà come hello toodo seguenti utilizzando hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:

* Dati letti da toocreate il database, eseguire il training e un modello predittivo di punteggio
* Scrittura dati tooyour database

## <a name="read-data-from-sql-data-warehouse"></a>Leggere dati da SQL Data Warehouse
Si verranno leggere dati dalla tabella Product nel database AdventureWorksDW hello.

### <a name="step-1"></a>Passaggio 1
Avviare un esperimento di nuovo facendo clic su + Nuovo nella parte inferiore di hello di hello finestra Machine Learning Studio, selezionare ESPERIMENTO, quindi provare vuoto. Predefinito selezionare hello sperimentare nome nella parte superiore di hello dell'area di disegno hello e rinominarlo toosomething significativo, ad esempio, stima di prezzo di biciclette.

### <a name="step-2"></a>Passaggio 2
Cerca modulo del lettore hello nella tavolozza hello dei set di dati e i moduli in a sinistra dell'area di disegno esperimento hello hello. Trascinare l'area di disegno hello modulo toohello esperimento.
![][drag_reader]

### <a name="step-3"></a>Passaggio 3
Selezionare modulo del lettore hello e compilare riquadro Proprietà hello.

1. Selezionare i Database SQL di Azure come hello origine dati.
2. Nome del server di database: nome del server di tipo hello. È possibile utilizzare hello [portale di Azure] [ Azure portal] toofind questo.

![][server_name]

1. Nome del database: nome hello del tipo di un database nel server di hello è stato specificato.
2. Nome dell'account utente server: digitare il nome utente hello di un account che disponga delle autorizzazioni di accesso per il database di hello.
3. Password dell'account utente server: fornire password hello per hello l'account utente specificato.
4. Accettare qualsiasi certificato server: usare questa opzione (meno sicura) se si desidera tooskip revisione certificato del sito hello prima di leggere i dati.
5. Query di database: immettere un'istruzione SQL che descrive i dati di hello da tooread. In questo caso, si verranno leggere dati dalla tabella di prodotto usando hello seguente query.

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a>Passaggio 4
1. Eseguire l'esperimento di hello facendo clic su Esegui in area di disegno di hello esperimento.
2. Al termine dell'esperimento hello, il modulo del lettore hello avrà tooindicate un segno di spunta verde che è stata completata correttamente. Si noti inoltre hello completato allo stato in esecuzione nell'angolo superiore destro di hello.

![][run]

1. toosee hello dati importati, fare clic sulla porta di output di hello nella parte inferiore di hello del set di dati automobili hello e selezionare Visualizza.

## <a name="create-train-and-score-a-model"></a>Creare, eseguire il training e assegnare un punteggio a un modello
A questo punto è possibile utilizzare questo set di dati per:

* Creare un modello: elaborare i dati e definire le funzionalità
* Modello di training hello: scegliere e applica un algoritmo di apprendimento
* Punteggio e test hello modello: stimare di nuovo prezzo di biciclette

![][model]

informazioni su come toocreate, eseguire il training, assegnare un punteggio e testare un machine learning hello utilizzare modello toolearn [crea esperimento esercitazione][Create experiment tutorial].

## <a name="write-data-tooazure-sql-data-warehouse"></a>Scrivere dati tooAzure SQL Data Warehouse
Tabella tooProductPriceForecast set di risultati hello verrà scritto nel database AdventureWorksDW hello.

### <a name="step-1"></a>Passaggio 1
Cerca modulo Writer hello nella tavolozza hello dei set di dati e i moduli in a sinistra dell'area di disegno esperimento hello hello. Trascinare l'area di disegno hello modulo toohello esperimento.

![][drag_writer]

### <a name="step-2"></a>Passaggio 2
Selezionare il modulo di scrittura hello e compilare riquadro Proprietà hello.

1. Selezionare il Database di SQL Azure come destinazione dei dati hello.
2. Nome del server di database: nome del server di tipo hello. È possibile utilizzare hello [portale di Azure] [ Azure portal] toofind questo.
3. Nome del database: nome hello del tipo di un database nel server di hello è stato specificato.
4. Nome dell'account utente server: digitare il nome utente hello di un account che disponga di autorizzazioni di scrittura per il database di hello.
5. Password dell'account utente server: fornire password hello per hello l'account utente specificato.
6. Accettare qualsiasi certificato del server (non protetto): selezionare questa opzione se non si desidera certificato hello tooview.
7. Elenco delimitato da virgole di colonne toobe salvato: fornire un elenco di colonne di set di dati o un risultato hello che si desidera toooutput.
8. Nome della tabella dati: specificare il nome di hello della tabella di dati hello.
9. Elenco delimitato da virgole delle colonne di datatable: specificare toouse i nomi di colonna hello hello nuova tabella. Hello i nomi di colonna possono essere diversi da hello quelli hello DataSet di origine, ma è necessario elencare hello stesso numero di colonne qui definite per la tabella di output di hello.
10. Numero di righe scritte per ogni operazione di SQL Azure: È possibile configurare hello numero di righe che vengono scritti i database SQL tooa in un'unica operazione.

![][writer_properties]

### <a name="step-3"></a>Passaggio 3
1. Eseguire l'esperimento di hello facendo clic su Esegui in area di disegno di hello esperimento.
2. Al termine dell'esperimento hello, tutti i moduli avrà tooindicate un segno di spunta verde che è stata completata correttamente.

## <a name="next-steps"></a>Passaggi successivi
Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
