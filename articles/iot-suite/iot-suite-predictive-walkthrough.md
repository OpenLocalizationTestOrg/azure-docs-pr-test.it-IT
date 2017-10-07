---
title: procedura dettagliata di manutenzione aaaPredictive | Documenti Microsoft
description: Procedura dettagliata di manutenzione predittiva di hello Azure IoT preconfigurato soluzione.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3c48a716-b805-4c99-8177-414cc4bec3de
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 900d6351019489a8e2f4b98908364e3bd14975c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-walkthrough"></a>Procedura dettagliata della soluzione preconfigurata di manutenzione predittiva

soluzione manutenzione predittiva preconfigurata Hello è una soluzione end-to-end per uno scenario di business che stima il punto di hello in corrispondenza del quale è probabile che toooccur un errore. È possibile usare questa soluzione preconfigurata in modo proattivo per attività come l'ottimizzazione della manutenzione. soluzione Hello combina servizi Azure IoT Suite chiave, ad esempio l'IoT Hub, analitica di flusso e un [Azure Machine Learning] [ lnk-machine-learning] dell'area di lavoro. L'area di lavoro contiene un modello, basato su un set di dati di esempio pubblica toopredict hello vita utile rimanente (RUL) di un motore aereo. soluzione Hello completamente implementa uno scenario di business IoT hello come punto di partenza per si tooplan e implementare una soluzione che soddisfi i requisiti aziendali specifici.

## <a name="logical-architecture"></a>Architettura logica

Hello seguente diagramma illustra i componenti logici hello della soluzione preconfigurata hello:

![][img-architecture]

gli elementi di Hello blu sono servizi di Azure il provisioning in area hello in cui è distribuita la soluzione hello preconfigurato. elenco di Hello delle regioni in cui è possibile distribuire la soluzione hello preconfigurato vengono visualizzati nel hello [pagina provisioning][lnk-azureiotsuite].

elemento Hello verde è un dispositivo simulato che rappresenta un motore aereo. Maggiori informazioni su questi dispositivi simulati nella seguente sezione hello.

gli elementi di colore grigio Hello rappresentano i componenti che implementano *gestione dei dispositivi* funzionalità. versione corrente di Hello della soluzione di manutenzione predittiva preconfigurata hello non eseguire il provisioning di queste risorse. toolearn più sulla gestione dei dispositivi, fare riferimento toohello [soluzione preconfigurata di monitoraggio remoto][lnk-remote-monitoring].

## <a name="simulated-devices"></a>Dispositivi simulati

Nella soluzione hello preconfigurato, un dispositivo simulato rappresenta un motore aereo. soluzione Hello viene eseguito il provisioning con due motori che eseguono il mapping aereo singolo tooa. Ogni motore genera quattro tipi di dati di telemetria: sensore 9, 11 sensore, sensore 14 e 15 sensore forniscono dati hello necessari per hello Machine Learning modello toocalculate hello RUL per il motore di hello. Ogni dispositivo simulato invia hello seguenti messaggi di dati di telemetria tooIoT Hub:

*Conteggio dei cicli*. Un ciclo rappresenta un volo completato con una durata compresa tra due e dieci ore. Durante il volo hello, i dati di telemetria vengono acquisiti ogni mezz'ora.

*Telemetria*. Sono presenti quattro sensori che rappresentano gli attributi del motore. sensori di Hello sono contrassegnati in modo generico sensore 9, 11 sensore, sensore 14 e 15 sensore. Queste quattro sensori rappresentano dati di telemetria sufficienti tooobtain utile risultati dal modello RUL hello. modello Hello utilizzato nella soluzione hello preconfigurato viene creato da un set di dati pubblico che include i dati del sensore motore reale. Per ulteriori informazioni sulla modalità di creazione del modello di hello dal set di dati originale hello, vedere hello [modello manutenzione predittiva di Cortana Intelligence raccolta][lnk-cortana-analytics].

dispositivi Hello simulato è possono gestire hello seguendo i comandi inviati dall'hub IoT hello nella soluzione hello:

| Comando | Descrizione |
| --- | --- |
| StartTelemetry |Controlli hello lo stato di simulazione hello.<br/>Dispositivo hello viene avviato l'invio di dati di telemetria |
| StopTelemetry |Controlli hello lo stato di simulazione hello.<br/>Dispositivo hello si interrompe l'invio di dati di telemetria |

L'hub IoT fornisce il riconoscimento dei comandi del dispositivo.

## <a name="azure-stream-analytics-job"></a>Processo di Analisi di flusso di Azure

**: Processo Dati di telemetria** opera su hello in arrivo dispositivo telemetria flusso utilizzando due istruzioni:

* Hello innanzitutto Seleziona tutti i dati di telemetria dai dispositivi hello e invia l'archiviazione dei dati tooblob. In questa finestra vengono visualizzati nell'app web hello.
* Hello calcola secondo sensore medio valori su una finestra temporale scorrevole di due minuti e invia i dati tramite hello evento hub tooan **processore di eventi**.

## <a name="event-processor"></a>Processore di eventi
Hello **host processore di eventi** viene eseguito in un processo Web di Azure. Hello **processore di eventi** accetta i valori medio sensore hello per un ciclo completato. Passa quindi tali tooan valori API che espone hello toocalculate di modello con training RUL per un motore. Hello API viene esposta da un'area di lavoro di Machine Learning che viene eseguito il provisioning come parte della soluzione hello.

## <a name="machine-learning"></a>Machine Learning
componente di Machine Learning Hello utilizza un modello derivato dai dati raccolti dai motori reale. È possibile passare l'area di lavoro Machine Learning toohello dal riquadro hello hello [azureiotsuite.com] [ lnk-azureiotsuite] pagina per la soluzione di provisioning. Hello affiancata è disponibile quando la soluzione hello è in hello **pronto** stato.


## <a name="next-steps"></a>Passaggi successivi
Dopo avere visto componenti chiave di hello della soluzione di hello manutenzione predittiva preconfigurata, è opportuno toocustomize è. Vedere [Guida alla personalizzazione di soluzioni preconfigurate][lnk-customize].

È anche possibile esplorare alcune hello altre caratteristiche e funzionalità di soluzioni di IoT Suite preconfigurato hello:

* [Domande frequenti su IoT Suite][lnk-faq]
* [Sicurezza di IoT da hello messa a terra][lnk-security-groundup]

[img-architecture]: media/iot-suite-predictive-walkthrough/architecture.png

[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-cortana-analytics]: http://gallery.cortanaintelligence.com/Collection/Predictive-Maintenance-Template-3
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/