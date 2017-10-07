---
title: le quote di Azure IoT Hub aaaUnderstand e la limitazione | Documenti Microsoft
description: Guida per sviluppatori - descrizione delle quote di hello applicabili tooIoT Hub e hello previsto comportamento di limitazione.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 425e1b08-8789-4377-85f7-c13131fae4ce
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 023fa29bfbfb1de35708d6d121a1c56b50adfed9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-quotas-and-throttling"></a>Riferimento - Quote e limitazioni dell'hub IoT

## <a name="quotas-and-throttling"></a>Quote e limitazioni
Ogni sottoscrizione di Azure può avere al massimo 10 hub IoT e al massimo un hub gratuito.

Ogni hub IoT viene sottoposto a provisioning con un determinato numero di unità in uno SKU specifico. Per altre informazioni, vedere [Prezzi dell'hub IoT di Azure][lnk-pricing]. Hello SKU e il numero di unità determinano quota giornaliera hello massima dei messaggi che è possibile inviare.

Hello SKU determina inoltre hello limitazioni che impone l'IoT Hub per tutte le operazioni.

## <a name="operation-throttles"></a>Limitazioni per le operazioni
Le limitazioni di operazione sono limitazioni di frequenza che vengono applicate in intervalli minuto hello e sono destinati tooavoid abusi. IoT Hub tenta tooavoid restituendo errori laddove possibile, ma all'avvio di restituzione di eccezioni se velocità hello viene violata troppo a lungo.

Hello seguente tabella mostra hello applicate le limitazioni. I valori si riferiscono tooan singolo hub.

| Limitazione | Hub gratuiti e S1 | Hub S2 | Hub S3 | 
| -------- | ------- | ------- | ------- |
| Operazioni del registro delle identità (creazione, recupero, elenco, aggiornamento, eliminazione) | 1,67/sec/unità (100/min/unità) | 1,67/sec/unità (100/min/unità) | 83,33/sec/unità (5000/min/unità) |
| Connessioni del dispositivo | Al massimo 100/sec o 12/sec/unità <br/> Ad esempio, due unità S1 sono 2\*12 = 24/sec, ma si hanno almeno 100/sec tra le unità. Con nove unità S1 si otterrà 108/sec (9\*12) tra le unità. | 120/sec/unità | 6000/sec/unità |
| Inoltri dal dispositivo al cloud | Al massimo 100/sec o 12/sec/unità <br/> Ad esempio, due unità S1 sono 2\*12 = 24/sec, ma si hanno almeno 100/sec tra le unità. Con nove unità S1 si otterrà 108/sec (9\*12) tra le unità. | 120/sec/unità | 6000/sec/unità |
| Inoltri dal cloud al dispositivo | 1,67/sec/unità (100/min/unità) | 1,67/sec/unità (100/min/unità) | 83,33/sec/unità (5000/min/unità) |
| Ricezioni dal cloud al dispositivo <br/> (solo quando il dispositivo usa HTTP)| 16,67/sec/unità (1000/min/unità) | 16,67/sec/unità (1000/min/unità) | 833,33/sec/unità (50000/min/unità) |
| Caricamento di file | 1,67 notifice caricamento file/sec/unità (100/min/unità) | 1,67 notifice caricamento file/sec/unità (100/min/unità) | 83,33 notifice caricamento file/sec/unità (5000/min/unità) |
| Metodi diretti | 20/sec/unità | 60/sec/unità | 3000/sec/unità | 
| Letture del dispositivo gemello | 10/sec | Al massimo 10/sec o 1/sec/unità | 50/sec/unità |
| Aggiornamenti dei dispositivi gemelli | 10/sec | Al massimo 10/sec o 1/sec/unità | 50/sec/unità |
| Operazioni dei processi <br/> (creazione, aggiornamento, elenco, eliminazione) | 1,67/sec/unità (100/min/unità) | 1,67/sec/unità (100/min/unità) | 83,33/sec/unità (5000/min/unità) |
| Velocità effettiva delle operazioni dei processi per dispositivo | 10/sec | Al massimo 10/sec o 1/sec/unità | 50/sec/unità |

È importante tooclarify che hello *le connessioni ai dispositivi* velocità determina la frequenza di hello in corrispondenza del quale è possono stabilire nuove connessioni dispositivo con un hub IoT. Hello *le connessioni ai dispositivi* velocità non controllano il numero massimo di hello di dispositivi connessi contemporaneamente. velocità di Hello dipende dal numero di hello di unità che viene effettuato il provisioning per l'hub IoT hello.

Ad esempio, se si acquista una singola unità S1, si ottiene un limite di 100 connessioni al secondo. Pertanto, tooconnect 100.000 dispositivi, sono necessari almeno 1000 secondi (circa 16 minuti). Tuttavia, è consentito un numero di dispositivi connessi simultaneamente pari al numero di dispositivi registrati nel registro delle identità.

Per un'analisi approfondita dell'IoT Hub, comportamento di limitazione vedere hello post di blog [IoT Hub la limitazione delle richieste e si][lnk-throttle-blog].

> [!NOTE]
> In qualsiasi momento, è possibile tooincrease quote o limitare i limiti per aumentare il numero di hello unità sottoposte a provisioning in un hub IoT.
> 
> [!IMPORTANT]
> Le operazioni del registro delle identità sono destinate all'uso in fase di esecuzione negli scenari di gestione e provisioning dei dispositivi. L'operazione di lettura o aggiornamento di un numero elevato di identità dei dispositivi è supportata tramite i [processi di importazione ed esportazione][lnk-importexport].
> 
> 

## <a name="other-limits"></a>Altri limiti

L'hub IoT applica altri limiti operativi:

| Operazione | Limite |
| --------- | ----- |
| URI per il caricamento di file | 10000 URI di firma di accesso condiviso possono essere generati contemporaneamente per un account di archiviazione. <br/> 10 URI di firma di accesso condiviso/dispositivo possono essere generati contemporaneamente. |
| Processi | Backup too30 giorni viene conservata la cronologia di processo <br/> Il numero massimo di processi simultanei è 1 (per il livello Gratuito e S1, 5 (per S2), 10 (per S3). |
| Altri endpoint | Agli hub SKU a pagamento possono essere associati 10 endpoint aggiuntivi. Agli hub SKU gratuiti può essere associato solo un endpoint aggiuntivo. |
| Regole di routing dei messaggi | Agli hub SKU a pagamento possono essere associate 100 regole di routing. Agli hub SKU gratuiti possono essere associate cinque regole di routing. |
| Messaggistica da dispositivo a cloud | Dimensioni massime dei messaggi 256 KB |
| Messaggistica da cloud a dispositivo | Dimensioni massime dei messaggi 64 KB |
| Messaggistica da cloud a dispositivo | Il numero massimo di messaggi in sospeso è 50 |

> [!NOTE]
> Attualmente, hello numero massimo di dispositivi, è possibile connettere hub IoT singolo tooa è 500.000. Se si desidera tooincrease questo limite, contattare [supporto Microsoft](https://azure.microsoft.com/support/options/).

## <a name="latency"></a>Latency
IoT Hub è impegnata a bassa latenza tooprovide per tutte le operazioni. Tuttavia, a causa di condizioni toonetwork e altri fattori imprevedibili non garantisce una latenza massima. Quando si progetta la soluzione, è necessario:

* Evitare di apportare qualsiasi presupporre la latenza massima di hello di qualsiasi operazione di IoT Hub.
* Eseguire il provisioning dell'hub IoT nei dispositivi di tooyour hello regione di Azure più vicini.
* È consigliabile utilizzare operazioni sensibili alla latenza di Azure IoT Edge tooperform hello dispositivo o su un dispositivo di chiusura toohello gateway.

Più unità dell'hub IoT influiscono sulla limitazione come descritto in precedenza, ma non forniscono alcuna prestazione di latenza aggiuntiva o garanzia.
In caso di incremento imprevisto della latenza dell'operazione, contattare il [supporto tecnico Microsoft](https://azure.microsoft.com/support/options/).

## <a name="next-steps"></a>Passaggi successivi
Di seguito sono indicati altri argomenti di riferimento reperibili nella Guida per gli sviluppatori dell'hub IoT:

* [Endpoint dell'hub IoT][lnk-devguide-endpoints]
* [Linguaggio di query dell'hub IoT per dispositivi gemelli, processi e routing messaggi][lnk-devguide-query]
* [Supporto di MQTT nell'hub IoT][lnk-devguide-mqtt]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-throttle-blog]: https://azure.microsoft.com/blog/iot-hub-throttling-and-you/
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
