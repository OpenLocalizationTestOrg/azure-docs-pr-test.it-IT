---
title: aaaStream dati dal flusso Analitica in archivio Data Lake | Documenti Microsoft
description: Utilizzare i dati di toostream Analitica di flusso di Azure in archivio Azure Data Lake
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a>Trasmettere i dati dal BLOB di archiviazione di Azure ad Archivio Data Lake usando Analisi di flusso di Azure
In questo articolo si apprenderà come toouse archivio Azure Data Lake come output per un processo Analitica di flusso di Azure. In questo articolo viene illustrato un semplice scenario che legge i dati da un blob di archiviazione di Azure (input) e scrive hello archivio data Lake a tooData (output).

> [!NOTE]
> In questo momento, creazione e configurazione di archivio Data Lake restituisce per Analitica di flusso è supportato solo in hello [portale di Azure classico](https://manage.windowsazure.com). Di conseguenza, alcune parti di questa esercitazione verranno utilizzato hello portale classico di Azure.
>
>

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Account di archiviazione di Azure**. Si utilizzerà un contenitore di blob da dati tooinput account per un processo di flusso Analitica. Per questa esercitazione, si supponga di avere un account di archiviazione denominato **storageforasa** e un contenitore nell'account hello chiamato **storageforasacontainer**. Dopo aver creato il contenitore di hello, caricare un tooit file dati di esempio. 
  
* **Account di Archivio Data Lake di Azure**. Seguire le istruzioni di hello in [introduzione archivio Azure Data Lake tramite il portale di Azure hello](data-lake-store-get-started-portal.md). Si supponga di avere un account Data Lake denominato **asadatalakestore**. 

## <a name="create-a-stream-analytics-job"></a>Creare un processo di Analisi di flusso
Iniziare creando un processo di Analisi di flusso che include un'origine di input e una destinazione di output. Per questa esercitazione, origine hello è un contenitore blob di Azure e la destinazione hello è archivio Data Lake.

1. Accesso toohello [portale Azure](https://portal.azure.com).

2. Nel riquadro di sinistra hello, fare clic su **i processi di flusso Analitica**, quindi fare clic su **Aggiungi**.

    ![Creare un processo di Analisi di flusso](./media/data-lake-store-stream-analytics/create.job.png "Creare un processo di Analisi di flusso")

    > [!NOTE]
    > Assicurarsi che si crea un processo in hello stessa area come account di archiviazione hello o comporta costi aggiuntivi per lo spostamento dei dati tra aree.
    >

## <a name="create-a-blob-input-for-hello-job"></a>Creare un Blob di input per il processo di hello

1. Pagina hello Open per il processo di flusso Analitica hello, hello nel riquadro di sinistra fare clic su hello **input** scheda e quindi fare clic su **Aggiungi**.

    ![Aggiungere un processo di input tooyour](./media/data-lake-store-stream-analytics/create.input.1.png "aggiungere un processo tooyour input")

2. In hello **nuovo input** pannello fornire hello seguenti valori.

    ![Aggiungere un processo di input tooyour](./media/data-lake-store-stream-analytics/create.input.2.png "aggiungere un processo tooyour input")

    * Per **alias di Input**, immettere un nome univoco per l'input processo hello.
    * Per **Tipo di origine** selezionare **Flusso dati**.
    * Per **Origine** selezionare **Archiviazione BLOB**.
    * Per **Sottoscrizione** selezionare **Usa l'archiviazione BLOB della sottoscrizione corrente**.
    * Per **account di archiviazione**, selezionare l'account di archiviazione di hello creato come parte dei prerequisiti di hello. 
    * Per **contenitore**, selezionare il contenitore hello creati in hello selezionato di account di archiviazione.
    * In **Formato di serializzazione eventi** scegliere **CSV**.
    * Per **Delimitatore** selezionare **scheda**.
    * Per **Codifica** selezionare **UTF-8**.

    Fare clic su **Crea**. portale Hello ora aggiunge input hello e verifica tooit connessione hello.


## <a name="create-a-data-lake-store-output-for-hello-job"></a>Creare un archivio Data Lake di output per il processo di hello

1. Aprire la pagina hello per il processo di flusso Analitica hello, fare clic su hello **output** scheda e quindi fare clic su **Aggiungi**.

    ![Aggiungere un processo tooyour output](./media/data-lake-store-stream-analytics/create.output.1.png "aggiungere un processo tooyour output")

2. In hello **nuovo output** pannello fornire hello seguenti valori.

    ![Aggiungere un processo tooyour output](./media/data-lake-store-stream-analytics/create.output.2.png "aggiungere un processo tooyour output")

    * Per **alias di Output**, immettere un nome univoco per l'output del processo hello. Si tratta di un nome descrittivo utilizzato nella query toodirect hello query output toothis archivio Data Lake.
    * Per **Sink** selezionare **Data Lkae Store**.
    * Sarà richiesto tooauthorize accedere tooData Lake archivio account. Fare clic su **Autorizza**.

3. In hello **nuovo output** pannello hello tooprovide seguente i valori di continuare.

    ![Aggiungere un processo tooyour output](./media/data-lake-store-stream-analytics/create.output.3.png "aggiungere un processo tooyour output")

    * Per **nome Account**, selezionare account archivio Data Lake hello sia già stato creato in cui si desidera hello processo output toobe inviati.
    * Per **modello prefisso del percorso**, immettere toowrite di percorso utilizzato un file del file all'interno di hello specificati account archivio Data Lake.
    * Per **formato data**, se si utilizza un token di data nel percorso di prefisso hello, è possibile selezionare il formato di data hello in cui sono organizzati i file.
    * Per **formato ora**, se è stato usato un token di tempo nel percorso di prefisso hello, specificare il formato di ora hello in cui sono organizzati i file.
    * In **Formato di serializzazione eventi** scegliere **CSV**.
    * Per **Delimitatore** selezionare **scheda**.
    * Per **Codifica** selezionare **UTF-8**.
    
    Fare clic su **Crea**. portale Hello ora aggiunge l'output di hello e verifica tooit connessione hello.
    
## <a name="run-hello-stream-analytics-job"></a>Eseguire il processo di flusso Analitica hello

1. un processo di flusso Analitica toorun, è necessario eseguire una query da hello **Query** scheda. Per questa esercitazione, è possibile eseguire query di esempio hello sostituendo i segnaposto hello con hello processo gli alias di input e outpui, come illustrato nella cattura di schermata hello riportato di seguito.

    ![Eseguire query](./media/data-lake-store-stream-analytics/run.query.png "Eseguire query")

2. Fare clic su **salvare** hello superiore hello e quindi da hello **Panoramica** scheda, fare clic su **avviare**. Nella finestra di dialogo hello selezionare **ora personalizzato**, quindi impostare hello data e ora correnti.

    ![Impostare l'ora del processo](./media/data-lake-store-stream-analytics/run.query.2.png "Impostare l'ora del processo")

    Fare clic su **avviare** processo hello toostart. Può richiedere il processo hello toostart di tooa alcuni minuti.

3. tootrigger hello toopick hello dati del processo da blob hello, copiare un contenitore blob di toohello file di dati di esempio. È possibile ottenere un file di dati di esempio da hello [Git Repository di Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt). Per questa esercitazione, copia il file hello **vehicle1_09142014.csv**. È possibile utilizzare vari client, ad esempio [Azure Storage Explorer](http://storageexplorer.com/), contenitore blob tooa di tooupload dati.

4. Da hello **Panoramica** scheda **monitoraggio**, vedere la modalità di elaborazione dati hello.

    ![Monitorare il processo](./media/data-lake-store-stream-analytics/run.query.3.png "Monitorare il processo")

5. Infine, è possibile verificare che i dati di output di hello processo sono disponibili account archivio Data Lake hello. 

    ![Verificare l'output](./media/data-lake-store-stream-analytics/run.query.4.png "Verificare l'output")

    Nel riquadro di esplorazione di dati hello, si noti che hello output scritto tooa percorso della cartella come specificato nel hello archivio Data Lake impostazioni di output (`streamanalytics/job/output/{date}/{time}`).  

## <a name="see-also"></a>Vedere anche
* [Creare un toouse cluster HDInsight archivio Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
