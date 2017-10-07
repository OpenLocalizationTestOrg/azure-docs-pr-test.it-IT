---
title: "approfondire aaaDeep stimare integrità veicolo e Guida abitudini - Azure | Documenti Microsoft"
description: "Utilizzare funzionalità di hello di insights di predittiva e in tempo reale toogain Intelligence Cortana sull'integrità del veicolo e abitudini di Guida."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a>Playbook soluzione analitica telemetria di veicolo: approfondimento soluzione hello
Questo **menu** collegamenti toohello sezioni di questo playbook: 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

Questa sezione drill-down in ognuna delle fasi di hello rappresentate hello architettura della soluzione con le istruzioni e i puntatori per la personalizzazione. 

## <a name="data-sources"></a>Origini dati
soluzione Hello utilizza due origini dati diverse:

* **set di dati di diagnostica e segnali del veicolo simulati** e 
* **catalogo dei veicoli**

Nella soluzione è incluso un simulatore di dati telematici relativi al veicolo. Genera informazioni di diagnostica ed segnala stato toohello corrispondente del veicolo hello e toohello gestiscono modello in un determinato punto nel tempo. Fare clic su [veicolo telematiche simulatore](http://go.microsoft.com/fwlink/?LinkId=717075) hello toodownload **veicolo telematiche simulatore soluzione Visual Studio** per le personalizzazioni in base alle esigenze. catalogo veicolo Hello contiene un set di dati di riferimento con un mapping toomodel VPN.

![Simulatore di dati telematici del veicolo](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

*Figura 1: Simulatore di dati telematici del veicolo*

Si tratta di un set di dati in formato JSON che contiene hello seguente schema.

| Colonna | Descrizione | Valori |
| --- | --- | --- |
| vin |Numero identificativo del veicolo generato in modo casuale |Viene ottenuto da un elenco master di 10.000 numeri identificativi di veicoli generati in modo casuale. |
| outsideTemperature |Hello all'esterno di temperatura in cui è piedi veicolo hello |Numero da 0 a 100 generato in modo casuale |
| engineTemperature |temperatura del motore di Hello del veicolo hello |Numero da 0 a 500 generato in modo casuale |
| Velocità |velocità del motore di Hello determina in quali hello veicolo |Numero da 0 a 100 generato in modo casuale |
| fuel |livello di carburante Hello del veicolo hello |Numero da 0 a 100 generato in modo casuale (indica la percentuale del livello di carburante) |
| engineoil |livello di petrolio motore Hello del veicolo hello |Numero da 0 a 100 generato in modo casuale (indica la percentuale del livello di olio del motore) |
| Tire pressure |pressione tire Hello del veicolo hello |Numero da 0 a 50 generato in modo casuale (indica la percentuale del livello di pressione degli pneumatici) |
| odometer |lettura di chilometraggio Hello del veicolo hello |Numero da 0 a 200000 generato in modo casuale |
| accelerator_pedal_position |posizione pedali Hello di tasti di scelta rapida del veicolo hello |Numero da 0 a 100 generato in modo casuale (indica la percentuale del livello dell'acceleratore) |
| parking_brake_status |Indica se il veicolo hello è disattivato o meno |true o false |
| headlamp_status |Indica dove proiettore hello è attiva o non |true o false |
| brake_pedal_status |Indica se viene premuto pedale freni hello o non |true o false |
| transmission_gear_position |posizione di ingranaggio trasmissione Hello del veicolo hello |Stati: first, second, third, fourth, fifth, sixth, seventh, eighth |
| ignition_status |Indica se il veicolo hello è in esecuzione o arrestato |true o false |
| windshield_wiper_status |Indica se è attivato Tergicristallo parabrezza hello o non |true o false |
| abs |Indica se l'ABS è attivato o meno |true o false |
| Timestamp |timestamp di Hello quando viene creato il punto di dati hello |Date |
| city |percorso di Hello del veicolo hello |4 città in questa soluzione: Bellevue, Redmond, Sammamish, Seattle |

set di dati riferimento modello veicolo Hello contiene mapping del modello toohello VPN. 

| vin | Modello |
| --- | --- |
| FHL3O1SA4IEHB4WU1 |Berlina |
| 8J0U8XCPRGW4Z3NQE |Ibrido |
| WORG68Z2PLTNZDBI7 |Berlina familiare |
| JTHMYHQTEPP4WBMRN |Berlina |
| W9FTHG27LZN1YWO0Y |Ibrido |
| MHTP9N792PHK08WJM |Berlina familiare |
| EI4QXI2AXVQQING4I |Berlina |
| 5KKR2VB4WHQH97PF8 |Ibrido |
| W9NSZ423XZHAONYXB |Berlina familiare |
| 26WJSGHX4MA5ROHNL |Decappottabile |
| GHLUB6ONKMOSI7E77 |Station Wagon |
| 9C2RHVRVLMEJDBXLP |Utilitaria |
| BRNHVMZOUJ6EOCP32 |SUV di piccole dimensioni |
| VCYVW0WUZNBTM594J |Auto sportiva |
| HNVCE6YFZSA5M82NY |SUV di medie dimensioni |
| 4R30FOR7NUOBL05GJ |Station Wagon |
| WYNIIY42VKV6OQS1J |SUV di grandi dimensioni |
| 8Y5QKG27QET1RBK7I |SUV di grandi dimensioni |
| DF6OX2WSRA6511BVG |Coupé |
| Z2EOZWZBXAEW3E60T |Berlina |
| M4TV6IEALD5QDS3IR |Ibrido |
| VHRA1Y2TGTA84F00H |Berlina familiare |
| R0JAUHT1L1R3BIKI0 |Berlina |
| 9230C202Z60XX84AU |Ibrido |
| T8DNDN5UDCWL7M72H |Berlina familiare |
| 4WPYRUZII5YV7YA42 |Berlina |
| D1ZVY26UV2BFGHZNO |Ibrido |
| XUF99EW9OIQOMV7Q7 |Berlina familiare |
| 8OMCL3LGI7XNCC21U |Decappottabile |
| ……. | |

### <a name="references"></a>Riferimenti
[Soluzione Vehicle Telematics Simulator di Visual Studio](http://go.microsoft.com/fwlink/?LinkId=717075) 

[Hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/)

[Data factory di Azure](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a>Ingestion
Combinazioni di hub eventi di Azure, flusso Analitica e Data Factory vengono sfruttate tooingest hello veicolo segnali, gli eventi di diagnostica hello e in tempo reale e analitica del batch. Tutti questi componenti creati e configurati come parte della distribuzione della soluzione hello. 

### <a name="real-time-analysis"></a>Analisi in tempo reale
Hello gli eventi generati dal simulatore telematiche veicolo hello vengono pubblicati con Hub eventi toohello hello SDK Hub eventi. il processo di flusso Analitica Hello inserisce questi eventi dalla hello Hub eventi e processi hello dati integrità del veicolo hello tooanalyze in tempo reale. 

![Dashboard di Hub eventi](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

*Figura 4: Dashboard di Hub eventi*

![Elaborazione dei dati da parte del processo di Analisi di flusso](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

*Figura 5: Elaborazione dei dati da parte del processo di Analisi di flusso*

processo di flusso Analitica Hello.

* Inserisce i dati da hello Hub eventi 
* esegue un join con hello modello dati di riferimento toomap hello veicolo VPN toohello corrispondente 
* Li rende persistenti nell'archivio BLOB di Azure per l'analisi in batch avanzata 

Hello seguente query Analitica di flusso è usato toopersist hello dati nell'archiviazione blob di Azure. 

![Query del processo di Analisi di flusso per l'inserimento di dati](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

*Figura 6: Query del processo di Analisi di flusso per l'inserimento di dati*

### <a name="batch-analysis"></a>Analisi batch
Viene anche generato un volume aggiuntivo di set di dati di diagnostica e segnali del veicolo simulati per rendere più completa l'analisi batch. Questo è necessario tooensure un volume di dati rappresentativo validi per l'elaborazione batch. A tale scopo, si sta usando una pipeline denominata "PrepareSampleDataPipeline" in toogenerate del flusso di lavoro di Azure Data Factory hello segnali veicolo simulata e set di dati diagnostici relativi a un anno. Fare clic su [attività personalizzata di Data Factory](http://go.microsoft.com/fwlink/?LinkId=717077) hello toodownload attività Data Factory personalizzata DotNet soluzione di Visual Studio per le personalizzazioni in base alle esigenze. 

![Preparazione dei dati di esempio per il flusso di lavoro dell'elaborazione batch](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

*Figura 7: Preparazione dei dati di esempio per il flusso di lavoro dell'elaborazione batch*

Hello pipeline è costituita da .net personalizzato ADF attività Mostra qui:

![Attività PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

*Figure 8: PrepareSampleDataPipeline*

Una volta pipeline hello viene eseguita correttamente e set di dati "RawCarEventsTable" è contrassegnato "Pronto", un anno vale la pena di segnali veicolo simulata e di diagnostica vengono generati i dati. Verrà visualizzata hello seguente cartella e il file creato nell'account di archiviazione nel contenitore "connectedcar" hello:

![Output di PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

*Figura 9: Output di PrepareSampleDataPipeline*

### <a name="references"></a>Riferimenti
[Azure Event Hub SDK per l'inserimento di flussi](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

[Funzionalità di spostamento dei dati di Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)
[Attività DotNet di Azure Data Factory](../data-factory/data-factory-use-custom-activities.md)

[Soluzione di Visual Studio per l'attività DotNet di Data factory di Azure per la preparazione dei dati di esempio](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a>Set di dati di partizione hello
segnali raw veicolo semistrutturati Hello e set di dati diagnostici vengono partizionati in fase di preparazione dei dati hello in un formato di mese/anno. Questo partizionamento Alza di livello più efficiente l'esecuzione di query e archiviazione a lungo termine scalabile abilitando errore failover da un blob account toohello successivamente come primo account hello è piena. 

>[!NOTE] 
>Questo passaggio nella soluzione hello è applicabile toobatch solo elaborazione.

Gestione dati di input e di output:

* Hello **i dati di output** (con etichetta *PartitionedCarEventsTable*) è toobe mantenere per un lungo periodo di tempo come modulo fondamentali / "rawest" hello, di dati "Data Lake" del cliente hello. 
* Hello **dati di input** toothis pipeline verrebbe in genere eliminata come dati di output di hello sono toohello di fedeltà completo di input: appena archiviato (partizionata) meglio per l'utilizzo successivo.

![Flusso di lavoro PartitionCarEvents](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

*Figura 10: Flusso di lavoro PartitionCarEvents*

dati non elaborati Hello sono partizionati usando un'attività Hive di HDInsight in "PartitionCarEventsPipeline". i dati di esempio Hello generati nel passaggio 1 per un anno vengono partizionati per anno/mese. le partizioni di Hello sono utilizzati toogenerate veicolo segnali e dati di diagnostica per ogni mese (totale 12 partizioni) di un anno. 

![Attività PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

*Figura 11: PartitionCarEventsPipeline*

***Script Hive PartitionConnectedCarEvents***

Hello seguenti script Hive, denominato "partitioncarevents.hql", viene utilizzato per il partizionamento e si trova nella cartella "\demo\src\connectedcar\scripts" hello di zip scaricato hello. 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

Quando la pipeline hello viene eseguita correttamente, viene visualizzato hello seguendo le partizioni generate nell'account di archiviazione nel contenitore "connectedcar" hello.

![Output partizionato](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

*Figura 12: Output partizionato*

dati Hello ora è ottimizzato, è più gestibile e pronto per l'ulteriore elaborazione insights batch rich toogain. 

## <a name="data-analysis"></a>Analisi dei dati
In questa sezione viene visualizzato come toocombine Analitica di flusso di Azure, Azure Machine Learning, Data Factory di Azure e Azure HDInsight per rich avanzate abitudini analitica integrità veicolo e la Guida. Sono presenti tre sottosezioni:

1. **Machine Learning**: in questa sottosezione contiene informazioni su esperimento di rilevamento di anomalie hello che è stata usata in questo veicoli toopredict soluzioni che richiedono manutenzione e che richiedono richiami a causa di problemi toosafety veicoli di manutenzione.
2. **Analisi in tempo reale**: in questa sottosezione contiene informazioni relative alle hello in tempo reale analitica utilizzando il linguaggio di Query di flusso Analitica hello e operatività apprendimento hello sperimentare in tempo reale mediante un'applicazione personalizzata.
3. **Batch analysis**: in questa sottosezione contiene informazioni riguardanti hello di trasformazione e di elaborazione dei dati di batch hello utilizzando Azure HDInsight e operativi da Azure Data Factory di Azure Machine Learning.

### <a name="machine-learning"></a>Machine Learning
Il nostro obiettivo è veicoli hello toopredict che richiedono manutenzione o il richiamo in base a determinate statistiche di integrità. Rendiamo hello seguenti presupposti

* Se uno dei seguenti tre condizioni hello è vere, veicoli hello richiedono **manutenzione manutenzione**:
  
  * La pressione degli pneumatici è bassa
  * Il livello di olio del motore è basso
  * La temperatura del motore è elevata
* Se uno di hello seguenti condizioni è vere, potrebbero essere veicoli hello un **problema di sicurezza** e richiedono **richiamo**:
  
  * La temperatura del motore è elevata, ma la temperatura esterna è bassa
  * La temperatura del motore è bassa, ma la temperatura esterna è elevata

In base ai requisiti precedenti hello, è stata creata anomalie di toodetect due modelli separati, uno per il rilevamento di manutenzione veicolo e uno per il rilevamento di richiamo vehicle. In entrambi questi modelli, algoritmo di analisi in componenti principali (PCA) incorporato hello viene utilizzato per il rilevamento di anomalie. 

**Modello di rilevamento per la manutenzione**

Se uno dei tre indicatori pressione tire, olio motore o temperatura del motore - soddisfa la condizione corrispondente, il modello di rilevamento di hello manutenzione segnala un'anomalia. Di conseguenza, è necessario solo tooconsider questi tre variabili di compilazione del modello di hello. In questo esperimento in Azure Machine Learning, viene utilizzata una **selezionare le colonne nel set di dati** tooextract modulo queste tre variabili. Quindi utilizziamo hello anomalie basato su PCA modulo toobuild hello anomalie rilevamento modello di rilevamento. 

Analisi in componenti principali (PCA) è una tecnica consolidata in machine learning che può essere il rilevamento di anomalie, classificazione e selezione toofeature applicato. Converte un set di casi contenente variabili probabilmente correlate in un set di valori denominati componenti principali. Hello concetto principale alla base della modellazione basato su PCA è tooproject dati in uno spazio inferiore-dimensionale, in modo che le funzionalità e anomalie più facilmente identificabili.

Per ogni nuovo input hello troppo modello di rilevamento, il rilevamento di anomalie hello Calcola prima relativa proiezione di hello autovettori e quindi Calcola hello normalizzato errore ricostruzione. Questo errore normalizzato è il punteggio di anomalie hello. Errore di hello superiore Hello, hello più anomali hello istanza è. 

Problema di rilevamento di manutenzione hello, ogni record può essere considerato come un punto in uno spazio 3D definito da pressione tire, olio motore e temperatura del motore coordinate. toocapture queste anomalie, è possibile hello originale dati progetto nello spazio 3D hello in uno spazio 2 dimensioni utilizzando PCA. Pertanto, viene impostato il parametro hello numero di componenti toouse in PCA toobe 2. Questo parametro ha un ruolo importante nell'applicazione del rilevamento delle anomalie basato su PCA. Dopo aver eseguito la proiezione dei dati con l'analisi PCA, è possibile identificare più facilmente queste anomalie.

**Modello di rilevamento di anomalie di richiamo** nel modello di rilevamento di anomalie richiamo hello, utilizziamo hello selezionare le colonne nel set di dati e delle anomalie basato su PCA moduli di rilevamento in modo analogo. Nello specifico, abbiamo estrarre innanzitutto tre variabili - temperatura del motore, temperatura esterna e velocità - utilizzando hello **selezionare le colonne nel set di dati** modulo. È inoltre includere velocità hello variabile poiché temperatura del motore di hello è in genere correlato toohello velocità. È quindi utilizzare dati di hello tooproject modulo rilevamento delle anomalie basato su PCA dallo spazio di 3-dimensionale hello in uno spazio 2 dimensioni. Hello richiamo criteri vengono soddisfatti e modo veicolo hello è necessario tenere presente quando temperatura del motore e la temperatura esterna sono correlate elevata negativamente. Utilizza l'algoritmo di rilevamento delle anomalie basato su PCA, è possibile acquisire eventuali anomalie hello dopo l'esecuzione di PCA. 

Durante il training di un modello, è necessario toouse dati normale, che non richiedono manutenzione o un richiamo come modello di rilevamento delle anomalie basato su PCA tootrain hello hello dati di input. In hello esperimento di assegnazione dei punteggi, utilizziamo toodetect modello rilevamento anomalie di hello training veicolo hello richiede manutenzione o il richiamo o meno. 

### <a name="real-time-analysis"></a>Analisi in tempo reale
Hello flusso Analitica nella Query SQL seguente viene utilizzato il Media hello tooget di tutte hello parametri veicolo importanti come velocità del veicolo, livello di carburante, temperatura del motore, lettura chilometraggio, pressione tire, livello di motore petrolio e altri. medie Hello vengono utilizzati toodetect anomalie, generano avvisi e determinare hello condizioni di integrità complessivo dei veicoli usati in area specifica e quindi ne esegue la correlazione toodemographics. 

![Query di Analisi di flusso per l'elaborazione in tempo reale](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

*Figura 13: Query di Analisi di flusso per l'elaborazione in tempo reale*

Tutti i valori medi di hello vengono calcolate su un TumblingWindow 3 secondi. In questo caso viene usata la finestra a cascata perché sono necessari intervalli di tempo contigui e non sovrapposti. 

Fare clic su toolearn ulteriori informazioni su tutte le funzionalità di "Windowing" hello in Azure flusso Analitica, [Windowing (Analitica del flusso di Azure)](https://msdn.microsoft.com/library/azure/dn835019.aspx).

**Stima in tempo reale**

Un'applicazione è inclusa come parte del modello di soluzione toooperationalize hello machine learning hello in tempo reale. Questa applicazione denominata "RealTimeDashboardApp" viene creata e configurata come parte della distribuzione della soluzione hello. un'applicazione Hello esegue l'esempio hello:

1. È in ascolto tooan istanza dell'Hub di eventi in cui Analitica flusso pubblica eventi hello in un modello in modo continuo. ![Query Analitica di flusso per la pubblicazione di dati hello](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *figura 14: query Analitica di flusso per la pubblicazione di hello dati tooan istanza dell'Hub di eventi di output* 
2. Per ogni evento ricevuto dall'applicazione: 
   
   * Processi hello dati utilizzando l'endpoint di Machine Learning richiesta-risposta di punteggio (RR). endpoint RR Hello viene pubblicato automaticamente come parte della distribuzione hello.
   * output di Hello RR è set di dati di Power BI tooa pubblicati tramite push hello API.

Questo modello è inoltre applicabile tooscenarios in cui si desidera toointegrate un'applicazione Line of Business (LoB) con il flusso in tempo reale analitica hello, per gli scenari, ad esempio gli avvisi, notifiche e messaggistica.

Fare clic su [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) hello toodownload RealtimeDashboardApp soluzione Visual Studio per le personalizzazioni. 

**hello tooexecute applicazione Dashboard in tempo reale**
1. Estrarre e salvare in locale. ![Cartella RealtimeDashboardApp](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figura 16: Cartella RealtimeDashboardApp*  
2. Eseguire un'applicazione hello RealtimeDashboardApp.exe
3. Fornire credenziali di Power BI valide, accedere e fare clic su Accetta. ![Dashboard in tempo reale app Accedi tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Dashboard in tempo reale app fine Accedi tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

*Figura 17: RealtimeDashboardApp: Accedi tooPower BI*

>[!NOTE] 
>Se si desidera il set di dati di tooflush hello Power BI, eseguire hello RealtimeDashboardApp con il parametro "flushdata" hello: 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a>Analisi batch
obiettivo Hello è tooshow come motori di Contoso utilizza hello calcolo di Azure funzionalità tooharness dati toogain dettagliate sull'ottimizzazione del modello, il comportamento di utilizzo e integrità vehicle. In questo modo è possibile:

* Migliorare l'esperienza dei clienti hello e renderlo più economica, fornendo informazioni sulla Guida dell'utente e i comportamenti di Guida efficiente di carburante
* Conoscere in modo proattivo di clienti e le decisioni di business toogovern modelli di Guida e fornire hello meglio in classe prodotti e servizi

In questa soluzione, destinazione hello seguenti metriche:

1. **Aggressivo piedi comportamento**: identifica tendenza hello di modelli di hello, posizioni, condizioni di Guida e tempo di insights di toogain anno hello aggressiva modelli determinante. Contoso Motors può usare queste informazioni per creare campagne di marketing, nuove funzionalità personalizzate e assicurazioni basate sull'utilizzo.
2. **Comportamento determinante efficiente alimentano**: identifica tendenza hello di modelli di hello, percorsi, le condizioni di Guida e tempo di insights di toogain anno hello modelli determinante efficiente carburante. Motori di Contoso può utilizzare queste informazioni per campagne di marketing piedi nuove funzionalità e proattivo driver toohello reporting per costo abitudini determinante descrittive validità e di ambiente. 
3. **Tenere presente i modelli**: identifica i modelli che richiedono richiamate da operatività esperimento di machine learning rilevamento di anomalie di hello

Esaminare i dettagli di hello di ognuna di queste metriche,

**Stile di guida aggressivo**

Hello partizionati segnali veicolo e dati di diagnostica vengono elaborati nella pipeline hello denominata "AggresiveDrivingPatternPipeline" utilizzando i modelli di hello toodetermine Hive, percorso, veicolo, determinano le condizioni e gli altri parametri che presenta aggressiva modello di Guida.

![Flusso di lavoro per lo stile di guida aggressivo](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figura 18: Flusso di lavoro per lo stile di guida aggressivo*


***Query Hive per lo stile di guida aggressivo***

Hello script Hive denominato "aggresivedriving.hql" usato per l'analisi aggressiva modello condizione Guida si trova nella cartella "\demo\src\connectedcar\scripts" di zip scaricato hello. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


Utilizza la combinazione hello del veicolo trasmissione ingranaggio posizione, stato pedali freni e velocità toodetect reckless/aggressiva determinano il comportamento in base a frenatura modello ad alta velocità. 

Quando la pipeline hello viene eseguita correttamente, viene visualizzato hello seguendo le partizioni generate nell'account di archiviazione nel contenitore "connectedcar" hello.

![Output di AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

*Figura 19: Output di AggressiveDrivingPatternPipeline*

**Stile di guida attento ai consumi**

Hello partizionata segnali veicolo e dati di diagnostica vengono elaborati nella pipeline hello denominata "FuelEfficientDrivingPatternPipeline". Hive è usato toodetermine hello modelli, percorso, veicolo, condizioni di Guida e altre proprietà con carburante efficiente determinante.

![Stile di guida attento ai consumi](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

*Figura 20: Flusso di lavoro per lo stile di guida attento ai consumi*

***Query Hive per lo stile di guida attento ai consumi***

Hello script Hive denominato "fuelefficientdriving.hql" usato per l'analisi aggressiva modello condizione Guida si trova nella cartella "\demo\src\connectedcar\scripts" di zip scaricato hello. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


Combinazione di hello di trasmissione a forma di ingranaggio posizione del veicolo, stato pedali freni, velocità e carburante toodetect pedali posizione di tasti di scelta rapida efficiente comportamento Guida basato sull'accelerazione, frenatura, utilizza e velocizzare i modelli. 

Quando la pipeline hello viene eseguita correttamente, viene visualizzato hello seguendo le partizioni generate nell'account di archiviazione nel contenitore "connectedcar" hello.

![Output di FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

*Figura 21: Output di FuelEfficientDrivingPatternPipeline*

**Previsioni di richiamo**

Hello esperimento di machine learning è stato eseguito il provisioning e pubblicata come servizio web come parte della distribuzione della soluzione hello. punto finale di punteggio batch di Hello viene usata in questo flusso di lavoro operativi utilizzando l'attività di punteggio batch di data factory e registrato come un servizio di data factory collegato.

![Endpoint di Machine Learning](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

*Figura 22: Endpoint di Machine Learning registrato come servizio collegato in Data factory*

servizio collegato registrato Hello viene utilizzato nei dati di hello DetectAnomalyPipeline tooscore hello utilizzando il modello di rilevamento delle anomalie di hello. 

![Attività di assegnazione punteggio batch di Machine Learning in Data factory](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

*Figura 23: Attività di assegnazione punteggio batch di Azure Machine Learning in Data factory* 

Esistono alcuni passaggi eseguiti nella pipeline per la preparazione dei dati, in modo che può essere operationalized con il servizio web di punteggio batch di hello. 

![DetectAnomalyPipeline per la stima dei veicoli da richiamare](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

*Figura 24: DetectAnomalyPipeline per la stima dei veicoli da richiamare* 

***Query Hive per il rilevamento delle anomalie***

Una volta completato il punteggio di hello, un'attività di HDInsight è tooprocess utilizzati e i dati di aggregazione hello sono classificati come anomalie dal modello hello con un punteggio di probabilità di 0.60 o versione successiva.

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


Quando la pipeline hello viene eseguita correttamente, viene visualizzato hello seguendo le partizioni generate nell'account di archiviazione nel contenitore "connectedcar" hello.

![Output di DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

*Figura 25: Output di DetectAnomalyPipeline*

## <a name="publish"></a>Pubblica

### <a name="real-time-analysis"></a>Analisi in tempo reale
Una delle query hello nel processo di flusso Analitica hello pubblica output di hello eventi tooan istanza dell'Hub di eventi. 

![Processo di flusso Analitica pubblica output tooan istanza dell'Hub eventi](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

*Figura 26-processo di flusso Analitica pubblica output tooan istanza dell'Hub eventi*

![Istanza di Hub di eventi di output flusso Analitica query toopublish toohello](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

*Figura 27-istanza di Hub di eventi di output flusso Analitica query toopublish toohello*

Questo flusso di eventi è utilizzato da hello che realtimedashboardapp inclusi nella soluzione hello. L'applicazione utilizza il servizio web di Machine Learning richiesta-risposta hello per il punteggio in tempo reale e pubblica hello dati risultante tooa Power BI dataset per l'utilizzo. 

### <a name="batch-analysis"></a>Analisi batch
risultati Hello del batch di hello ed elaborazione in tempo reale sono tabelle di Database SQL di Azure toohello pubblicati per l'utilizzo. Hello Azure SQL Server, Database e tabelle hello vengono create automaticamente come parte dello script di installazione di hello. 

![Flusso di lavoro mart toodata di copiare i risultati di elaborazione batch](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

*Figura 28-risultati copia toodata mart flusso di lavoro di elaborazione Batch*

![Processo di flusso Analitica pubblica toodata mart](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

*Figura 29-processo di flusso Analitica pubblica toodata mart*

![Impostazione di data mart nel processo di Analisi di flusso](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

*Figura 30: Impostazione di data mart nel processo di Analisi di flusso*

## <a name="consume"></a>Utilizzo
Power BI offre alla soluzione un dashboard completo per la visualizzazione di dati in tempo reale e di analisi predittive. 

Fare clic qui per informazioni dettagliate su come configurare i report di Power BI hello e dashboard hello. dashboard di Hello finale è simile al seguente:

![Dashboard di Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

*Figura 31: Dashboard di Power BI*

## <a name="summary"></a>Riepilogo
Questo documento contiene un drill-down dettagliato di hello veicolo telemetria Analitica soluzione. Questa presenta un modello di architettura lambda per l'analisi batch e in tempo reale completa di stime e azioni. Questo modello viene applicato tooa ampia gamma di casi d'uso che richiedono percorso a caldo (in tempo reale) e analitica freddo percorso (batch). 

