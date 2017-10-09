---
title: manutenzione aaaPredictive preconfigurato soluzione | Documenti Microsoft
description: Una descrizione di manutenzione predittiva di hello Azure IoT Suite preconfigurato soluzione.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a>Panoramica della soluzione preconfigurata di manutenzione predittiva

Hello *manutenzione predittiva* [preconfigurato soluzione] [ lnk_preconfigured_solutions] è uno dei hello [Microsoft Azure IoT Suite] [ lnk_iot_suite] preconfigurato soluzioni. Questa soluzione integra una raccolta di dati di telemetria in tempo reale dei dispositivi con un modello predittivo creato utilizzando [Azure Machine Learning][lnk-machine-learning].

Con Azure IoT Suite, è possibile rapidamente e facilmente connettersi asset monitoraggio tooand e analizzare dati di telemetria in tempo reale nei dashboard e visualizzazioni. Nella soluzione di manutenzione predittiva hello, visualizzazioni e dashboard hello offrono nuova informazione che può unità efficienza e migliorare i profitti.

## <a name="hello-scenario"></a>Hello Scenario

Fabrikam è una compagnia aerea locale che si concentra sulle esperienze eccezionali dei clienti a prezzi competitivi. Una causa di ritardi dei voli sono i problemi di manutenzione e la manutenzione dei motori degli aeromobili è particolarmente complessa. Fabrikam deve evitare malfunzionamenti del motore durante la fase di trasferimento tutti i costi, in modo che controlla regolarmente i motori e pianificazioni in base tooa piano di manutenzione. Tuttavia, aereo motori non sempre accenti hello stesso. Sui motori viene eseguita manutenzione superflua. Ancora più importante, si verificano problemi che possono forzare a terra un aereo fino a quando non viene eseguita la manutenzione. Se un aereo si trova nella posizione in cui hello destra tecnici o pezzi di ricambio non sono disponibili, questi problemi possono risultare particolarmente onerosa.

motori di Hello di aereo Fabrikam vengono instrumentati con sensori che consentono di monitorare le condizioni del motore durante la fase di trasferimento. Fabrikam Usa hello manutenzione predittiva soluzione toocollect hello sensore dati raccolti durante il volo hello. Dopo aver anni accumulo di motore operativo e dati di errore, gli esperti di dati di Fabrikam hanno modellata un hello toopredict modo vita utile rimanente (RUL) di un motore aereo. modello di Hello utilizza una correlazione tra dati provenienti da quattro dei sensori motore hello e usura motore che provoca l'errore tooeventual. Mentre è ancora sicurezza tooensure di un controllo periodico tooperform Fabrikam, ora possibile usare hello modelli toocompute hello RUL per ogni motore dopo ogni volo. modello di Hello utilizza dati di telemetria hello raccolti dai motori di hello durante il volo hello. Fabrikam può prevedere i futuri punti di malfunzionamento e pianificare la manutenzione e la riparazione in anticipo.

> [!NOTE]
> modello di soluzione Hello utilizza dati usura motore effettivo.

Per stimare il punto di hello quando è necessaria una manutenzione, Fabrikam possibile ottimizzare i costi di tooreduce operazioni.

I coordinatori della manutenzione usano utilità di pianificazione per:

- Piano di manutenzione toocoincide con un aereo arresto in una determinata posizione.
- Verificare un tempo sufficiente sia disponibile per hello aereo toobe fuori servizio senza provocare interruzioni di pianificazione.
- tooschedule tooensure di tecnici che aereo viene gestiti in modo efficiente senza tempo di attesa.

I responsabili del controllo di inventario ricevono i piani di manutenzione, pertanto possono ottimizzare il processo di ordinazione e l'inventario delle parti di ricambio.

Queste attività ora terra aereo toominimize di Fabrikam e ridurre i costi operativi assicurando sicurezza hello di passeggeri e personale.

toounderstand come [Azure IoT Suite] [ lnk_iot_suite] fornisce ai clienti funzionalità hello necessario potenziale hello toorealize della manutenzione predittiva, esaminare questo [infografica] [lnk_infographic].

## <a name="how-hello-predictive-maintenance-solution-is-built"></a>La modalità di compilazione di soluzioni di manutenzione predittiva hello

soluzione Hello utilizza un modello di Azure Machine Learning esistente come un modello tooshow queste funzionalità di utilizzo dal dispositivo telemetria raccolto tramite servizi IoT Suite. Microsoft ha creato un [modello di regressione] [ lnk_regression_model] di un motore aereo in base ai dati disponibili pubblicamente<sup>\[1\]</sup>e dettagliate informazioni aggiuntive su come toouse hello modello.

Hello soluzione manutenzione predittiva IoT di Azure Usa il modello di regressione hello creato da questo modello. modello Hello è distribuito nella sottoscrizione di Azure ed esposta attraverso un'API generata automaticamente. soluzione Hello include un subset di dati che rappresenta 4 (pari a 100 totale) di testing hello motori e flussi di dati del sensore hello 4 (pari a 21 totale). Questi dati sono sufficiente tooprovide risultati corretti dal modello con training hello.

*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*

## <a name="get-started-with-predictive-maintenance"></a>Introduzione alla manutenzione predittiva

Questa esercitazione viene illustrato come tooprovision hello soluzione manutenzione predittiva. Illustra anche funzionalità di base della soluzione di manutenzione predittiva hello hello. È possibile accedere a molte di queste funzionalità tramite il dashboard di soluzione hello che distribuisce insieme soluzione hello preconfigurato.

toocomplete questa esercitazione, è necessaria una sottoscrizione di Azure attiva.

> [!NOTE]
> Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk_free_trial].

1. Accesso troppo[azureiotsuite.com] [ lnk-azureiotsuite] di Azure utilizzando le credenziali dell'account e fare clic su  **+**  toocreate una soluzione.
1. Fare clic su **selezionare** hello **manutenzione predittiva** riquadro.
1. Immettere un valore in **Nome soluzione** per la soluzione preconfigurata di manutenzione predittiva.
1. Seleziona hello **area** e **sottoscrizione** si desidera toouse tooprovision hello soluzione.
1. Fare clic su **crea soluzione** hello toobegin processo di provisioning. Questo processo è in genere richiede diversi minuti toorun.

### <a name="wait-for-hello-provisioning-process-toocomplete"></a>Attendere hello toocomplete processo di provisioning

1. Fare clic sul riquadro hello per la soluzione con **Provisioning** stato.
1. Hello preavviso **Provisioning stati** come servizi di Azure vengono distribuiti nella sottoscrizione di Azure.
1. Una volta al termine del provisioning, hello modifiche allo stato troppo**pronto**.
1. Fare clic su dettagli di hello riquadro toosee hello della soluzione nel riquadro di destra hello. In questo riquadro è possibile avviare hello soluzione dashboard e accesso hello Machine Learning dell'area di lavoro.

> [!NOTE]
> Se si verificano problemi di distribuzione di soluzioni hello preconfigurato, esaminare [le autorizzazioni nel sito azureiotsuite.com hello] [ lnk-permissions] hello e [domande frequenti su] [ lnk-faq]. Se persistono problemi hello, creare un ticket di servizio in hello [portale][lnk-portal].

Sono presenti dettagli che ci si aspetta toosee che non sono elencati per la soluzione? è possibile inviare suggerimenti sulle funzionalità usando i [suggerimenti degli utenti](https://feedback.azure.com/forums/321918-azure-iot).

## <a name="view-hello-solution"></a>Visualizza soluzione hello

In questa sezione descrive la soluzione hello dell'interfaccia utente.

### <a name="predictive-maintenance-dashboard"></a>Dashboard di manutenzione predittiva

Questa pagina in un'applicazione hello web utilizza PowerBI JavaScript controlli (vedere hello [repository PowerBI-visuals][lnk-powerbi]) toovisualize:

* dati di output di Hello dai processi di flusso Analitica hello nell'archiviazione blob.
* Hello RUL e ciclo di conteggio per il motore di aereo.

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a>Osservare il comportamento di hello della soluzione cloud hello

In hello portale di Azure, passare il gruppo di risorse toohello con il nome di soluzione hello scelto tooview le risorse di provisioning.

![][img-resource-group]

Quando si esegue il provisioning di soluzione hello preconfigurato, viene visualizzato un messaggio di posta elettronica con un'area di lavoro di collegamento toohello Machine Learning. È inoltre possibile passare l'area di lavoro Machine Learning toohello da hello [azureiotsuite.com] [ lnk-azureiotsuite] pagina per la soluzione di provisioning. Un riquadro è disponibile in questa pagina quando la soluzione hello è in hello **pronto** stato.

![][img-machine-learning]

Nel portale di soluzione hello, è possibile visualizzare che tale esempio hello viene eseguito il provisioning con due aereo di quattro dispositivi simulati toorepresent con due motori per aereo, ognuno con quattro sensori. Quando si esce prima di tutto il portale di soluzione toohello, simulazione hello è stato arrestato.

![][img-simulation-stopped]

Fare clic su **avviare simulazione** simulazione hello toobegin. Hello cronologia sensore, RUL, cicli e RUL cronologia popolare dashboard hello.

![][img-simulation-running]

Quando RUL è inferiore a 160 (una valore soglia arbitraria scelta per scopi dimostrativi), il portale di soluzione hello viene visualizzato un avviso simbolo successivo toohello RUL visualizzare. portale di soluzione Hello evidenzia inoltre motore aereo hello in giallo. Si noti come valori RUL hello presentano una tendenza verso il basso generale globale, ma tendono toobounce su e giù. Questo comportamento è dovuta diverse lunghezze di ciclo hello e accuratezza del modello hello.

![][img-simulation-warning]

simulazione completa Hello richiede circa 35 minuti toocomplete 148 cicli. Hello 160 RUL viene raggiunta la soglia per hello prima volta in circa 5 minuti e motori di raggiunto la soglia di hello circa 8 minuti.

simulazione di Hello attraversa hello set di dati completo per i cicli di 148 e si posiziona su valori di ciclo e RUL finali.

È possibile arrestare la simulazione di hello in qualsiasi punto, ma facendo clic su **avviare simulazione** riproduzioni hello simulazione dall'inizio di hello del set di dati hello.

## <a name="next-steps"></a>Passaggi successivi

informazioni su come IoT di Azure consente scenari di manutenzione predittiva, leggere toolearn [acquisire valore hello Internet of Things][lnk_capture_value].

Richiedere un [procedura dettagliata] [ lnk-predictive-walkthrough] della soluzione di manutenzione predittiva hello.

È anche possibile esplorare alcune hello altre caratteristiche e funzionalità di soluzioni di IoT Suite preconfigurato hello:

* [Domande frequenti su IoT Suite][lnk-faq]
* [Sicurezza di IoT da hello messa a terra][lnk-security-groundup]

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/