---
title: aaaIoT flussi di dati in tempo reale e Analitica di flusso di Azure | Documenti Microsoft
description: Tag dei sensori IoT e flussi di dati con l'elaborazione dei dati in tempo reale e l'analisi di flusso
keywords: soluzione IoT, introduzione a IoT
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 3e829055-75ed-469f-91f5-f0dc95046bdb
ms.service: stream-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 422e6b719d0289880aa7f17fdc585e2b768c63d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stream-analytics-tooprocess-data-from-iot-devices"></a>Introduzione ai dati di Azure flusso Analitica tooprocess dai dispositivi IoT
In questa esercitazione si apprenderà come toocreate dati toogather logica di elaborazione del flusso da dispositivi Internet delle cose (IoT). Si utilizzerà un toodemonstrate case di utilizzo reali, di Internet delle cose (IoT) come toobuild la soluzione in modo rapido ed economico.

## <a name="prerequisites"></a>Prerequisiti
* [Sottoscrizione di Azure](https://azure.microsoft.com/pricing/free-trial/)
* File di dati e query di esempio scaricabili da [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)

## <a name="scenario"></a>Scenario
Contoso, che è una società nello spazio di automazione industriale hello, ha completamente automatizzato il processo di produzione. macchine Hello in questo laboratorio sono sensori che sono in grado di creazione di flussi di dati in tempo reale. In questo scenario, un piano di produzione manager desidera toohave informazioni in tempo reale da hello sensore dati toolook per modelli e intraprendere le azioni necessarie. Si utilizzerà hello flusso Analitica Query Language (SAQL) con modelli interessanti toofind hello sensore dati dal flusso in ingresso di hello dei dati.

In questo caso, i dati vengono generati da un dispositivo SensorTag di Texas Instruments.

![SensorTag di Texas Instruments](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-01.jpg)

il payload di Hello di hello dati è in formato JSON e simile hello seguente:

    {
        "time": "2016-01-26T20:47:53.0000000",  
        "dspl": "sensorE",  
        "temp": 123,  
        "hmdt": 34  
    }  

In uno scenario reale possono essere presenti centinaia di questi sensori che generano eventi come un flusso. In teoria, un dispositivo gateway verrebbe eseguito codice toopush questi eventi troppo[hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/) o [hub IoT Azure](https://azure.microsoft.com/services/iot-hub/). Il processo di flusso Analitica sarebbe questi eventi dagli hub eventi di inserimento e di eseguire query in tempo reale analitica su flussi hello. Quindi, è possibile inviare hello risultati tooone di hello [supportati output](stream-analytics-define-outputs.md).

Per semplicità d'uso, questa guida introduttiva include un file di dati di esempio acquisito da dispositivi SensorTag reali. È possibile eseguire query su dati di esempio hello e visualizzare i risultati. Nelle esercitazioni successive, si apprenderà come tooconnect il processo tooinputs e output e distribuirli toohello servizio di Azure.

## <a name="create-a-stream-analytics-job"></a>Creare un processo di Analisi di flusso.
1. In hello [portale di Azure](http://portal.azure.com), fare clic su hello sul segno più e quindi digitare **analisi di flusso** in hello testo finestra toohello a destra. Selezionare quindi **processo flusso Analitica** nell'elenco risultati hello.
   
    ![Creare un nuovo processo di Analisi di flusso](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-02.png)
2. Immettere un nome univoco di processo e verificare la sottoscrizione hello è hello quello corretto per il processo. Creare quindi un nuovo gruppo di risorse o selezionarne uno esistente.
3. Selezionare una località per il processo. Per una velocità di elaborazione e riduzione dei costi di trasferimento di dati selezionando hello è consigliabile stesso percorso del gruppo di risorse hello e account di archiviazione desiderato.
   
    ![Informazioni sulla creazione di un nuovo processo di Analisi di flusso](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03.png)
   
   > [!NOTE]
   > È consigliabile creare un solo account di archiviazione di questo tipo per ogni area. Questa risorsa di archiviazione verrà condivisa tra tutti i processi di Analisi di flusso creati in tale area.
   > 
   > 
4. Tooplace casella hello, controllare il processo nel dashboard e quindi fare clic su **crea**.
   
    ![creazione del processo in corso](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03a.png)
5. Verrà visualizzata una distribuzione' avviata...' visualizzato in hello in alto a destra della finestra del browser. Non appena verrà modificato finestra tooa completata come illustrato di seguito.
   
    ![creazione del processo in corso](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03b.png)

### <a name="create-an-azure-stream-analytics-query"></a>Creare una query di analisi di flusso di Azure
Al termine del processo creato è ora tooopen e compilazione di una query. Fare clic sul riquadro hello per tale, è possibile accedere facilmente al processo.

![Riquadro del processo](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-04.png)

In hello **processo topologia** riquadro fare clic su hello **QUERY** casella toogo toohello Editor di Query. Hello **QUERY** l'editor consente query tooenter T-SQL che esegue la trasformazione hello su dati dell'evento hello in arrivo.

![Riquadro della query](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-05.png)

### <a name="query-archive-your-raw-data"></a>Query: Archiviazione dei dati non elaborati
forma più semplice di Hello di query è una query pass-through che consente di archiviare tutti i dati di input tooits designato di output. Scaricare i file di dati di esempio hello [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) tooa percorso nel computer. 

1. Incollare la query hello dal file PassThrough.txt hello. 
   
    ![Test del flusso di input](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06.png)
2. Fare clic su Avanti tooyour input di hello tre punti e selezionare **caricare i dati di esempio dal file** casella.
   
    ![Test del flusso di input](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06a.png)
3. Un riquadro si apre in hello direttamente come risultato, dal percorso di download di file e fare clic su dati selezionare hello HelloWorldASA InputStream.json **OK** nella parte inferiore di hello del riquadro hello.
   
    ![Test del flusso di input](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06b.png)
4. Quindi fare clic su hello **Test** ingranaggio nella parte superiore di hello sinistra della finestra hello e l'elaborazione della query test hello set di dati campione. Verrà aperta una finestra di risultati di sotto della query come hello elaborazione è stata completata.
   
    ![Risultati del test](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-07.png)

### <a name="query-filter-hello-data-based-on-a-condition"></a>Di query: In base a una condizione dati hello del filtro
Provare i risultati di hello toofilter in base a una condizione. Desideriamo tooshow risultati solo per gli eventi provenienti da "sensorA". query Hello è nel file Filtering.txt hello.

![Filtro di un flusso di dati](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-08.png)

Si noti che la query tra maiuscole e minuscole hello Confronta un valore stringa. Fare clic su hello **Test** ingranaggio nuovamente query hello tooexecute. query Hello deve restituire le righe di 389 1860 eventi.

![Secondo risultato di output del test di query](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-09.png)

### <a name="query-alert-tootrigger-a-business-workflow"></a>Query: Avviso tootrigger un flusso di lavoro di business
La query verrà ora resa più dettagliata. Per ogni tipo di sensore, si desidera toomonitor temperatura media per ogni finestra di 30 secondi e visualizzare i risultati solo se la temperatura media hello supera 100 gradi. Viene illustrato come scrivere seguente hello query e quindi fare clic su **Test** risultati hello toosee. query Hello è nel file ThresholdAlerting.txt hello.

![Query di filtro per 30 secondi](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-10.png)

Dovrebbe essere risultati che contengono solo 245 righe e i nomi dei sensori in Media hello temperature è maggiore di 100. Questa query raggruppa il flusso di hello di eventi per **dspl**, ovvero nome sensore hello, più un **finestra a cascata** di 30 secondi. Le query temporali devono indicare come si desidera ora tooprogress. Utilizzando hello **TIMESTAMP BY** clausola specificati hello **OUTPUTTIME** volte tooassociate colonna con tutti i calcoli temporali. Per informazioni dettagliate, leggere gli articoli MSDN hello su [gestione del tempo](https://msdn.microsoft.com/library/azure/mt582045.aspx) e [funzioni finestra](https://msdn.microsoft.com/library/azure/dn835019.aspx).

### <a name="query-detect-absence-of-events"></a>Query: rilevare l'assenza di eventi
Come possiamo è scrivere una query toofind una mancanza di eventi di input? Conoscere hello ultima volta che un sensore di inviata dati e quindi non ha inviato gli eventi per hello minuto successivo. query Hello è nel file AbsenseOfEvent.txt hello.

![Rilevare l'assenza di eventi](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-11.png)

Nell'esempio si utilizza un **LEFT OUTER** join toohello del flusso di dati stesso (self-join). In caso di **INNER JOIN** viene restituito un risultato solo quando viene trovata una corrispondenza.  Per un **LEFT OUTER** join, se un evento dal lato sinistro di join hello hello è non corrispondente, che per tutte le colonne del lato destro hello di hello è NULL viene restituita una riga. Questa tecnica è molto utile toofind un'assenza di eventi. Per altre informazioni sui [JOIN](https://msdn.microsoft.com/library/azure/dn835026.aspx), vedere la documentazione MSDN.

## <a name="conclusion"></a>Conclusioni
scopo di Hello di questa esercitazione è la vista dei risultati nel Visualizzatore hello toowrite diverso linguaggio di Query di flusso Analitica query e vedere toodemonstrate. Si tratta, tuttavia, di informazioni di base, perché Analisi di flusso consente di eseguire molte altre attività. Flusso Analitica supporta un'ampia gamma di input e output e possono anche utilizzare le funzioni in Azure Machine Learning toomake è uno strumento affidabile per l'analisi dei flussi di dati. È possibile avviare tooexplore informazioni sul flusso Analitica con il nostro [mappa di apprendimento](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/). Per ulteriori informazioni su come query toowrite, leggere l'articolo hello su [modelli di query comuni](stream-analytics-stream-analytics-query-patterns.md).

