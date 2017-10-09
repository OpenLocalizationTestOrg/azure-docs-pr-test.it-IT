---
title: procedura dettagliata sulla soluzione di Azure IoT Suite factory aaaConnected | Documenti Microsoft
description: Una descrizione di hello Azure IoT preconfigurato soluzione connesso factory e dalla relativa architettura.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a>Procedura dettagliata per la soluzione preconfigurata di connected factory

Hello IoT Suite connesso factory [preconfigurato soluzione] [ lnk-preconfigured-solutions] è un'implementazione di una soluzione industriale end-to-end che:

* Consente di connettere i dispositivi di settore tooboth simulato server in esecuzione OPC UA nelle righe di produzione simulato factory e dispositivi server UA OPC. Per ulteriori informazioni su OPC UA, vedere hello [connesso domande frequenti sulla factory](iot-suite-faq-cf.md).
* Visualizza KPI e OEE di tali dispositivi e delle linee di produzione.
* Viene illustrato come un'applicazione basata su cloud potrebbe essere toointeract utilizzati con i sistemi server UA OPC.
* Consente di tooconnect dispositivi server UA OPC.
* Consente di toobrowse e modificare i dati del server OPC UA hello.
* Si integra con hello Azure ora serie Insights (STI) servizio tooprovide visualizzazioni personalizzate dei dati di hello dai server UA OPC.

È possibile utilizzare la soluzione hello come punto di partenza per la propria implementazione e [personalizzare] [ lnk-customize] è toomeet i requisiti aziendali specifici.

Questo articolo vengono illustrati alcuni elementi chiave hello, di hello connesso factory soluzione tooenable toounderstand il funzionamento. Queste informazioni consentono di:

* Risolvere i problemi nella soluzione hello.
* Pianificare la modalità toocustomize toohello soluzione toomeet esigenze specifiche.
* Progettare la propria soluzione IoT che usa i servizi di Azure.

Per ulteriori informazioni, vedere hello [connesso domande frequenti sulla factory](iot-suite-faq-cf.md).

## <a name="logical-architecture"></a>Architettura logica

Hello seguente diagramma illustra i componenti logici hello della soluzione preconfigurata hello:

![Architettura logica di connected factory][connected-factory-logical]

## <a name="communication-patterns"></a>Modelli di comunicazione

soluzione Hello utilizza hello [specifica OPC UA Pub/Sub](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA telemetria dati tooIoT Hub in formato JSON. soluzione Hello utilizza hello [Publisher OPC](https://github.com/Azure/iot-edge-opc-publisher) modulo IoT Edge per questo scopo.

soluzione Hello ha anche un client di OPC UA integrato in un'applicazione web in grado di stabilire connessioni con server OPC UA locali. Hello client utilizza un [proxy inverso](https://wikipedia.org/wiki/Reverse_proxy) e riceve la Guida dalla connessione di IoT Hub toomake hello senza che sia necessario aprire le porte nel firewall locale hello. Questo modello di comunicazione è denominato [modello di comunicazione assistita con servizi](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/). soluzione Hello utilizza hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) modulo IoT Edge per questo scopo.


## <a name="simulation"></a>Simulazione

Hello simulati stazioni e l'esecuzione di produzione hello simulato sistemi (MES) costituiscono una linea di produzione di factory. Hello dispositivi simulati e hello OPC Publisher modulo sono basati su hello [OPC UA .NET Standard] [ lnk-OPC-UA-NET-Standard] pubblicati da hello Foundation OPC.

Hello OPC Proxy e server di pubblicazione OPC vengono implementati come moduli basati su [Azure IoT Edge][lnk-Azure-IoT-Gateway]. Ogni linea di produzione simulata ha un gateway designato collegato.

Tutti i componenti di simulazione vengono eseguiti in contenitori Docker ospitati in una macchina virtuale Linux di Azure. simulazione di Hello è configurato toorun otto simulato le righe di produzione per impostazione predefinita.

## <a name="simulated-production-line"></a>Linea di produzione simulata

Una linea di produzione produce parti. È composta da postazioni diverse, ovvero montaggio, collaudo e imballaggio.

simulazione di Hello viene eseguito e aggiorna i dati di hello esposto tramite nodi OPC UA hello. Tutte le stazioni line simulato di produzione vengono orchestrate da hello MES tramite UA OPC.

## <a name="simulated-manufacturing-execution-system"></a>MES (Manufacturing Execution System) simulato

Hello MES controlla ogni stazione in linea di produzione hello tramite modifiche dello stato di OPC UA toodetect stazione. Chiama OPC UA stazioni di metodi toocontrol hello e passa un prodotto da una postazione toohello Avanti fino al completamento.

## <a name="gateway-opc-publisher-module"></a>Modulo di pubblicazione OPC del gateway

Modulo di server di pubblicazione OPC connette toohello stazione OPC UA server e sottoscrive toohello OPC nodi toobe pubblicato. modulo Hello converte i dati del nodo hello in formato JSON, crittografa e invia tooIoT Hub come messaggi OPC UA pubblicazione/sottoscrizione.

modulo server di pubblicazione OPC Hello solo richiede una porta in uscita https (443) e può funzionare con un'infrastruttura aziendale esistente.

## <a name="gateway-opc-proxy-module"></a>Modulo proxy OPC del gateway

Hello Gateway OPC UA Proxy modulo tunnel messaggi di comando e controllo UA OPC binari e richiede solo una porta in uscita https (443). Può funzionare con l'infrastruttura aziendale esistente, inclusi i proxy Web.

Utilizza dispositivo Hub IoT metodi tootransfer delicate TCP/IP dati a livello di applicazione hello e garantisce pertanto trust endpoint, la crittografia dei dati e l'integrità mediante SSL/TLS.

protocollo binario di OPC UA inoltrato tramite proxy hello Hello Usa la crittografia e autenticazione agente utente.

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

Hello Gateway OPC Publisher modulo sottoscrive tooOPC UA server nodi toodetect modifica i valori dei dati hello. Se viene rilevata una modifica di dati in uno dei nodi di hello, questo modulo Invia messaggi tooAzure IoT Hub.

IoT Hub fornisce un tooAzure origine evento STI. STI archivia i dati per 30 giorni basate sui timestamp associato toohello messaggi. Questi dati includono:

* ApplicationUri OPC UA
* NodeId OPC UA
* Valore del nodo hello
* Timestamp di origine
* DisplayName OPC UA

Attualmente, STI non consentono i clienti desiderano dati hello tookeep per quanto tempo toocustomize.

Time Series Insights esegue query sui dati del nodo usando una funzione SearchSpan (Time.From, Time.To) ed esegue l'aggregazione in base ad ApplicationUri OPC UA, NodeId OPC UA oppure DisplayName OPC UA.

dati di hello tooretrieve per hello OEE e indicatori KPI misuratori e grafici di serie temporali hello, i dati vengono aggregati per numero di eventi, Sum, Avg, Min e Max.

serie temporale Hello vengono compilate mediante un processo diverso. OEE e indicatori KPI vengono calcolati dai dati di base di stazione e trasmessi a topologia hello (righe di produzione, le factory, enterprise) in un'applicazione hello.

Inoltre, serie temporale per topologia OEE e un indicatore KPI viene calcolato in app hello, ogni volta che un intervallo di tempo visualizzato è pronto. Ad esempio, visualizzazione giorno hello viene aggiornato ogni ora completa.

visualizzazione di Hello time serie di dati del nodo provenienti direttamente da STI utilizzando un'aggregazione per timespan.

## <a name="iot-hub"></a>Hub IoT
Hello [hub IoT] [ lnk-IoT Hub] riceve i dati inviati da hello OPC Publisher modulo in cloud hello e rende il servizio di Azure STI toohello disponibili. 

Hello IoT Hub nella soluzione hello inoltre:
- Gestisce un registro di sistema di identità che archivia gli ID hello per tutti OPC Publisher modulo e tutti i moduli di Proxy OPC.
- Viene utilizzato come canale di trasporto per la comunicazione bidirezionale di hello modulo Proxy OPC.

## <a name="azure-storage"></a>Archiviazione di Azure
soluzione Hello utilizza l'archiviazione blob di Azure come archiviazione su disco per i dati di distribuzione di macchina virtuale e toostore hello.

## <a name="web-app"></a>App Web
app web Hello distribuita come parte della soluzione hello preconfigurato è costituito da un client OPC UA integrato, di elaborazione degli avvisi e visualizzazione di dati di telemetria.

## <a name="next-steps"></a>Passaggi successivi

È possibile continuare introduzione IoT Suite leggendo hello seguenti articoli:

* [Autorizzazioni nel sito azureiotsuite.com hello][lnk-permissions]
* [Distribuire un gateway in Windows o Linux per la soluzione factory preconfigurato hello connesso](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
