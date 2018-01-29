---
title: Personalizzare la soluzione factory connesso - Azure | Documenti Microsoft
description: Una descrizione di come personalizzare il comportamento della soluzione factory connesso preconfigurato.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/14/2017
ms.author: dobett
ms.openlocfilehash: 48c8036d0bc9534ce94529b96d32b004769246c1
ms.sourcegitcommit: 0e4491b7fdd9ca4408d5f2d41be42a09164db775
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="customize-how-the-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a>Personalizzare la modalità di visualizzazione di dati dai server OPC UA la soluzione factory connesso

La soluzione factory connesso aggrega e visualizza i dati dai server OPC UA connesso alla soluzione. È possibile individuare e inviare comandi ai server OPC UA nella soluzione. Per altre informazioni su OPC UA, vedere le [domande frequenti sulla soluzione di connected factory](iot-suite-faq-cf.md).

Gli esempi di dati aggregati nella soluzione includono i valori OEE (Overall Equipment Efficiency) e gli indicatori KPI visualizzabili nel dashboard a livello di fabbrica, linea e stazione. Lo screenshot seguente mostra i valori OEE e gli indicatori KPI per la stazione **Assemblaggio** nella **Linea di produzione 1** di uno stabilimento a **Monaco**:

![Esempio di valori OEE e indicatori KPI nella soluzione][img-oee-kpi]

Questa soluzione consente di visualizzare informazioni dettagliate su dati specifici dai server OPC UA, chiamati *stazioni*. La schermata seguente mostra i tracciati del numero di articoli prodotti da una stazione specifica:

![Tracciati del numero di articoli prodotti][img-manufactured-items]

Facendo clic su uno dei grafici è possibile esplorare ulteriormente i dati tramite Time Series Insights (TSI):

![Esplorare i dati con Time Series Insights][img-tsi]

L'articolo illustra:

- Come i dati vengono resi disponibili per le diverse visualizzazioni nella soluzione.
- Come è possibile personalizzare il modo in cui la soluzione visualizza i dati.

## <a name="data-sources"></a>Origini dati

La soluzione factory connesso Visualizza i dati dai server OPC UA connesso alla soluzione. L'installazione predefinita include diversi server OPC UA che eseguono una simulazione di fabbrica. È possibile aggiungere i propri server OPC UA che [si connettono tramite un gateway][lnk-connect-cf] alla soluzione.

È possibile anche esplorare gli elementi dei dati che un server OPC UA connesso può inviare alla soluzione nel dashboard:

1. Scegliere **Browser** a cui passare la **selezionare un server OPC UA** Vista:

    ![Passare alla vista Selezionare un server OPC UA][img-select-server]

1. Selezionare un server e fare clic su **Connetti**. Fare clic su **Procedi** quando viene visualizzato l'avviso di sicurezza.

    > [!NOTE]
    > L'avviso viene visualizzato una sola volta per ciascun server e stabilisce una relazione di trust tra quest'ultimo e il dashboard della soluzione.

1. È ora possibile esplorare gli elementi dei dati che il server può inviare alla soluzione. Gli elementi che vengono inviati alla soluzione hanno un segno di spunta:

    ![Elementi pubblicati][img-published]

1. Se si è un *amministratore* nella soluzione, è possibile scegliere di pubblicare un elemento di dati per renderlo disponibile nella soluzione factory connesso. L'amministratore può anche modificare il valore degli elementi di dati e chiamare i metodi nel server OPC UA.

## <a name="map-the-data"></a>Eseguire il mapping di dati

La soluzione factory connesso viene eseguito il mapping e aggrega i dati pubblicati dal server UA OPC per le diverse visualizzazioni nella soluzione. Consente di distribuire la soluzione factory connesso al proprio account Azure quando si esegue il provisioning della soluzione. Un file JSON nella soluzione Visual Studio connesso factory memorizza queste informazioni di mapping. È possibile visualizzare e modificare il file di configurazione JSON nella factory connesso soluzione di Visual Studio. È possibile ridistribuire la soluzione dopo aver apportato una modifica.

È possibile usare il file di configurazione per:

- Modificare le stazioni, le linee di produzione e gli stabilimenti simulati esistenti.
- Eseguire il mapping di dati dai server OPC UA effettivi che si connettono alla soluzione.

Per ulteriori informazioni su mapping e aggregare i dati per soddisfare specifiche esigenze, vedere [come configurare la factory connessa preconfigurato soluzione ](iot-suite-connected-factory-configure.md).

## <a name="deploy-the-changes"></a>Distribuire le modifiche

Dopo avere apportato modifiche per il **ContosoTopologyDescription.json** file, è necessario ridistribuire la soluzione factory connesso al proprio account Azure.

Il repository **azure-iot-connected-factory** include uno script PowerShell **build.ps1** che è possibile usare per ricompilare e distribuire la soluzione.

## <a name="next-steps"></a>Fasi successive

Ulteriori informazioni sulla soluzione factory connesso preconfigurato, leggere gli articoli seguenti:

* [Procedura dettagliata per la soluzione preconfigurata di connected factory][lnk-rm-walkthrough]
* [Distribuire un gateway per la factory connesso][lnk-connect-cf]
* [Autorizzazioni per il sito azureiotsuite.com][lnk-permissions]
* [Domande frequenti sulla soluzione di connected factory](iot-suite-faq-cf.md)
* [Domande frequenti][lnk-faq]


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-v1-permissions.md
[lnk-faq]: iot-suite-v1-faq.md