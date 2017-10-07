---
title: aaaCustomize Azure IoT Suite connesso factory | Documenti Microsoft
description: "Una descrizione delle modalità di comportamento hello toocustomize di hello connessione factory preconfigurato soluzione."
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
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a>Personalizzare la modalità di connessione factory soluzione consente di visualizzare dati dai server OPC UA hello

## <a name="introduction"></a>Introduzione

Hello factory connesso soluzione aggrega e visualizza i dati di hello OPC UA server connesso toohello soluzione. È possibile esplorare e inviare comandi toohello OPC UA server nella soluzione. Per ulteriori informazioni su OPC UA, vedere hello [connesso domande frequenti sulla factory](iot-suite-faq-cf.md).

Sono esempi di dati aggregati in soluzione hello hello l'efficienza di apparecchiature complessivo (OEE) e indicatori di prestazioni chiave (KPI) che è possibile visualizzare nel dashboard di hello livello di factory hello, riga e di espansione. Hello schermata riportata di seguito vengono illustrati hello OEE e indicatori KPI valori per hello **Assembly** nella stazione **produzione riga 1**, in hello **Monaco** factory:

![Esempio di valori OEE e un indicatore KPI nella soluzione hello][img-oee-kpi]

Consente di Hello è tooview informazioni dagli elementi di dati specifico da hello Server OPC UA, detti *stazioni*. Hello schermata seguente mostra tracciati totale hello degli articoli a una stazione specifico:

![Tracciati del numero di articoli prodotti][img-manufactured-items]

Se si fa clic su uno dei grafici hello, è possibile esplorare i dati di hello usando ora serie Insights (STI):

![Esplorare i dati con Time Series Insights][img-tsi]

L'articolo illustra:

- Come dati hello vengono resa disponibile toohello diverse visualizzazioni in soluzione hello.
- Come è possibile personalizzare soluzione hello hello Visualizza dati hello.

## <a name="data-sources"></a>Origini dati

Hello factory connesso soluzione consente di visualizzare dati da hello OPC UA server collegati toohello soluzione. installazione predefinita di Hello include diversi OPC UA che eseguono una simulazione di factory. È possibile aggiungere i propri server OPC UA che [connettersi tramite un gateway] [ lnk-connect-cf] tooyour soluzione.

È possibile esplorare gli elementi di dati hello che un server OPC UA connesso può inviare tooyour soluzione nel dashboard di hello:

1. Passare toohello **selezionare un server OPC UA** Vista:

    ![Passare toohello selezionare una visualizzazione di server UA OPC][img-select-server]

1. Selezionare un server e fare clic su **Connetti**. Fare clic su **procedere** quando viene visualizzata avviso di sicurezza hello.

    > [!NOTE]
    > Solo, questo avviso viene visualizzato una volta per ogni server e stabilisce una relazione di trust tra il dashboard di soluzione hello e server hello.

1. È ora Sfoglia hello gli elementi di dati hello server possono inviare toohello soluzione possibile. Gli elementi che vengono inviati toohello soluzione hanno un segno di spunta verde:

    ![Elementi pubblicati][img-published]

1. Se si è un *amministratore* nella soluzione hello, è possibile scegliere toopublish un toomake di elemento di dati è disponibile in hello connessa soluzione factory. Come amministratore, è anche possibile modificare il valore di hello di elementi di dati e chiamare metodi hello server UA OPC.

## <a name="map-hello-data"></a>Dati della mappa hello

Hello connessi factory soluzione mappe e hello aggregazioni elementi di dati pubblicati da hello OPC UA server toohello diverse visualizzazioni soluzione hello. Hello factory connesso soluzione distribuisce tooyour account Azure quando si esegue il provisioning di soluzione hello. Un file JSON di hello soluzione di Visual Studio connesso factory memorizza queste informazioni di mapping. È possibile visualizzare e modificare il file di configurazione JSON nella factory connesso hello soluzione di Visual Studio. Dopo aver apportato una modifica, è possibile ridistribuire la soluzione hello.

È possibile utilizzare file di configurazione hello:

- Modificare factory simulato esistente hello, linee di produzione e le stazioni.
- Eseguire il mapping di dati da Server OPC UA reali che si connette toohello soluzione.

una copia di hello tooclone connesso soluzione di Visual Studio factory, hello di utilizzare il comando di git seguente:

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

file Hello **ContosoTopologyDescription.json** definisce hello visualizzazioni del mapping di dati del server OPC UA hello elementi toohello nel dashboard di soluzione hello factory connesso. È possibile trovare questo file di configurazione in hello **Contoso\Topology** cartella hello **WebApp** progetto nella soluzione di Visual Studio hello.

organizzazione Hello del contenuto del file JSON hello come una gerarchia di nodi di stazione, linea di produzione e factory. Questa gerarchia definisce la gerarchia di navigazione hello nel dashboard di hello factory connesso. I valori in ogni nodo della gerarchia hello determinano informazioni hello visualizzate nel dashboard di hello. Ad esempio, file JSON hello contiene hello seguenti valori per hello factory Monaco:

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

percorso, la descrizione e nome hello vengono visualizzati in questa visualizzazione nel dashboard di hello:

![Dati Monaco nel dashboard di hello][img-munich]

Ogni stabilimento, linea di produzione e stazione ha una proprietà immagine. È possibile trovare questi file JPEG in hello **Content\img** cartella hello **WebApp** progetto. Questi file di immagine visualizzano nel dashboard di factory connesso hello.

Ogni stazione include diverse proprietà dettagliate che definiscono i mapping di elementi di dati dalla hello OPC UA hello. Queste proprietà sono descritte in hello le sezioni seguenti:

### <a name="opcuri"></a>OpcUri

Hello **OpcUri** valore è hello OPC UA Application URI che identifica in modo univoco hello server UA OPC. Ad esempio, hello **OpcUri** stazione assembly hello nella riga di produzione 1 Monaco simile hello seguente valore: **urn: scada2194:ua:munich:productionline0:assemblystation**.

È possibile visualizzare hello URI del server OPC UA hello connesso nel dashboard di soluzione hello:

![Visualizzare gli URI dei server OPC UA][img-server-uris]

### <a name="simulation"></a>Simulazione

informazioni di hello Hello **simulazione** nodo è specifico toohello simulazione OPC UA che viene eseguito in hello Server OPC UA sottoposti a provisioning per impostazione predefinita. Non vengono usate per un server OPC UA reale.

### <a name="kpi1-and-kpi2"></a>Kpi1 e Kpi2

Questi nodi vengono descritti come dati di stazione hello contribuiscono toohello due valori di indicatore KPI nel dashboard di hello. In una distribuzione predefinita, questi indicatori KPI rappresentano unità all'ora e kWh all'ora. soluzione Hello calcola i valori di indicatore KPI a livello di hello una stazione e li aggrega alla linea di produzione hello e livelli di factory.

Ogni indicatore KPI ha un valore minimo, un valore massimo e un valore di destinazione Ogni valore dell'indicatore KPI è inoltre possibile definire le azioni di allarme per hello connesso factory soluzione tooperform. Hello frammento seguente mostra le definizioni KPI hello per stazione assembly hello nella riga di produzione 1 Monaco:

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

Hello seguente schermata Mostra dati KPI hello nel dashboard di hello.

![Informazioni relative ai KPI nel dashboard di hello][lnk-kpi]

### <a name="opcnodes"></a>OpcNodes

Hello **OpcNodes** nodi identificano gli elementi di dati pubblicati da hello server OPC UA hello e specificare come tooprocess tali dati.

Hello **NodeId** valore identifica hello NodeID di UA OPC specifico da hello server UA OPC. Hello primo nodo in una stazione di assembly hello per linea di produzione 1 Monaco ha un valore **ns = 2, i = 385**. Oggetto **NodeId** valore specifica hello dati elemento tooread dal server OPC UA hello e hello **SymbolicName** fornisce un nome descrittivo toouse nel dashboard di hello per tali dati.

Altri valori associati a ogni nodo sono riepilogati nella seguente tabella hello:

| Valore | Descrizione |
| ----- | ----------- |
| Pertinenza  | i valori di indicatore KPI e OEE Hello dati contribuiscono a. |
| OpCode     | Come vengono aggregati i dati hello. |
| Unità      | Hello unità toouse nel dashboard di hello.  |
| Visible    | Se toodisplay questo valore nelle dashboard hello. Alcuni valori vengono usati nei calcoli, ma non visualizzati.  |
| Massima    | valore massimo Hello che attiva un avviso nel dashboard di hello. |
| MaximumAlertActions | Tootake un'azione nell'avviso tooan di risposta. Ad esempio, inviare una stazione tooa di comando. |
| ConstValue | Un valore costante usato in un calcolo. |

## <a name="deploy-hello-changes"></a>Distribuire le modifiche di hello

Dopo avere apportato modifiche toohello **ContosoTopologyDescription.json** file, è necessario ridistribuire hello connesso factory soluzione tooyour account Azure.

Hello **azure iot-connessione-factory** repository include un **build.ps1** script di PowerShell, è possibile utilizzare toorebuild e distribuire la soluzione hello.

## <a name="next-steps"></a>Passaggi successivi

Ulteriori informazioni sulla soluzione factory preconfigurato hello connesso da lettura hello seguenti articoli:

* [Procedura dettagliata per la soluzione preconfigurata di connected factory][lnk-rm-walkthrough]
* [Distribuire un gateway per fabbrica connessa][lnk-connect-cf]
* [Autorizzazioni nel sito azureiotsuite.com hello][lnk-permissions]
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
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md