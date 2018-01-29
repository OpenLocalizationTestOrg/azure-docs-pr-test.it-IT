---
title: Combinazioni supportate di esecuzione e ambienti di dati per la preparazione dati di Azure Machine Learning | Microsoft Docs
description: Questo documento elenca tutte le combinazioni supportate di diversi runtime e origini dati disponibili per la preparazione dati di Azure Machine Learning
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
ms.date: 09/15/2017
ms.openlocfilehash: 248cbcfe35db646a8bc71c6f825dcaa8a4661e91
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2017
---
# <a name="supported-matrix-for-this-release"></a>Matrice supportata per questa versione 
Quando il codice carica i dati usando le origini dati o la preparazione dati di Azure Machine Learning, recuperando i dataframe di Pandas o Spark, sono supportate le combinazioni seguenti di ambienti di calcolo per la sperimentazione e le posizioni dei dati:

|     |File locali  |Archivio BLOB di Azure  |Database SQL Server***  |
|---------|---------|---------|---------|---------|
|Python in locale    |     Supportato    |Non supportate         | Non supportate        |         |
|Python di Docker (macchina virtuale Linux)     |Supportato solo nei file di progetto*         | Non supportate        |        Non supportate |         |
|PySpark di Docker (macchina virtuale Linux)     |Supportato solo nei file di progetto*     |Supportato         | Supportato**        |         |
|Python della macchina virtuale per data science di Azure     |Supportato solo nei file di progetto*         |Non supportate         |Non supportate         |         |
|PySPark della macchina virtuale per data science di Azure     | Supportato solo nei file di progetto*        |Non supportate         |Non supportate         |         |
|PySPark HDInsight di Azure     | Non supportate        |Supportato         |Supportato**         |         |
|Python HDInsight di Azure     | Non supportate        | Non supportate        | Non supportate        |         |

Azure Data Lake Store non è attualmente supportato per le destinazioni di calcolo.

*Quando vengono usati percorsi di file locali, i file all'interno del progetto vengono copiati nell'ambiente di calcolo e quindi vengono letti qui. I file esterni al progetto non vengono copiati e i percorsi non saranno più risolvibili nell'ambiente di calcolo. È consigliabile usare la sostituzione dell'origine dati in modo che il codice possa usare un file locale durante l'esecuzione in locale. Passare a un BLOB di Archiviazione di Microsoft Azure per una configurazione di esecuzione diversa. È anche possibile usare il supporto di campionamento sulle origini dati per gestire le esecuzioni solo per dati di grandi dimensioni in determinate configurazioni di esecuzione.

**Usa il driver SQL Server JDBC di Maven 6.2.1. È necessario assicurarsi che questo pacchetto, o un pacchetto compatibile, sia incluso nel file spark_dependencies.yml per l'ambiente di calcolo.

Supporta il Database SQL Azure o SQL Server fornito con che il database può essere raggiunto dall'ambiente di calcolo. 
