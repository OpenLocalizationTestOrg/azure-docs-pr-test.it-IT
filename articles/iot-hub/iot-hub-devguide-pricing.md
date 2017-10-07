---
title: prezzi di IoT Hub Azure aaaUnderstand | Documenti Microsoft
description: Guida per sviluppatori - Informazioni sulle misurazioni e sui prezzi nell'hub IoT ed esempi reali.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2016
ms.author: elioda
ms.openlocfilehash: e294c0b7f483e042ca3f63e93c14e0c2d773ae7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-pricing-information"></a>Informazioni sui prezzi dell'hub IoT di Azure

[IoT Hub Azure prezzi] [ lnk-pricing] vengono fornite informazioni generali hello su diverse SKU e prezzi per l'IoT Hub. In questo articolo contiene informazioni più dettagliate su come hello che varie funzionalità di IoT Hub sono misurate come messaggi dall'IoT Hub.

## <a name="charges-per-operation"></a>Addebiti per ogni operazione

| Operazione | Informazioni di fatturazione | 
| --------- | ------------------- |
| Operazioni del registro delle identità <br/> (creazione, recupero, elenco, aggiornamento, eliminazione) | Nessun addebito. |
| Messaggi da dispositivo a cloud | Per i messaggi inviati correttamente è previsto un addebito in base a blocchi di 4 KB in ingresso nell'hub IoT, ad esempio un messaggio di 6 KB viene addebitato come 2 messaggi. |
| Messaggi da cloud a dispositivo | Per i messaggi inviati correttamente è previsto un addebito in base a blocchi di 4 KB, ad esempio un messaggio di 6 KB viene addebitato come 2 messaggi. |
| Caricamenti di file | Trasferimento di file tooAzure archiviazione non è a consumo dall'IoT Hub. I messaggi di avvio e di completamento del trasferimento di file vengono addebitati come messaggi misurati in incrementi di 4 KB. Trasferimento di un file di 10 MB, ad esempio, viene addebitato due messaggi in aggiunta toohello i costi di archiviazione di Azure. |
| Metodi diretti | Le richieste di metodo completate vengono addebitate in blocchi di 4 KB, le risposte con corpi non vuoti vengono addebitate in blocchi di 4 KB, come messaggi aggiuntivi. I dispositivi toodisconnected le richieste vengono addebitati come messaggi suddivisi in blocchi a 4 KB. Ad esempio, un metodo con un corpo 6 KB che comporta una risposta senza il corpo dal dispositivo hello, viene addebitato come due messaggi. un metodo con un corpo 6 KB che comporta una risposta di 1 KB dal dispositivo hello viene addebitato come due messaggi di richiesta di hello più di un altro messaggio di risposta hello. |
| Letture del dispositivo gemello | Un doppio dispositivo legge dal dispositivo hello e dalla soluzione hello nuovamente fine vengono addebitate come messaggi suddivisi in blocchi a 512 byte. Ad esempio, la lettura di un messaggio di 6 KB del dispositivo gemello viene addebitata come 12 messaggi. |
| Aggiornamenti del dispositivo gemello (tag e proprietà) | Aggiornamenti del dispositivo doppi da dispositivi hello e hello vengono addebitati come messaggi suddivisi in blocchi a 512 byte. Ad esempio, la lettura di un messaggio di 6 KB del dispositivo gemello viene addebitata come 12 messaggi. |
| Query del dispositivo gemello | Le query vengono addebitate come messaggi a seconda delle dimensioni del risultato hello in blocchi a 512 byte. |
| Operazioni dei processi <br/> (creazione, aggiornamento, elenco, eliminazione) | Nessun addebito. |
| Operazioni dei processi per ogni dispositivo | Le operazioni dei processi, ad esempio gli aggiornamenti del dispositivo gemello e i metodi, vengono addebitati come messaggi normali. Ad esempio, un processo che provoca 1000 chiamate del metodo con richieste di 1 KB e risposte con corpo vuoto viene addebitato come 1000 messaggi. |

> [!NOTE]
> Tutte le dimensioni vengono calcolate considerando dimensioni del payload hello in byte (il frame di protocollo viene ignorato). In caso di messaggi, che hanno proprietà e corpo, dimensioni hello viene calcolata in modo indipendente dal protocollo, come descritto in hello [IoT Hub Guida per gli sviluppatori di messaggistica][lnk-message-size].

## <a name="example-1"></a>Esempio 1

Un dispositivo invia un messaggio da dispositivo a cloud 1 KB al minuto tooIoT Hub, che viene letto da Analitica di flusso di Azure. back-end di Hello soluzione richiama un metodo (con payload di 512 byte) nel dispositivo hello ogni tootrigger di dieci minuti un'azione specifica. dispositivo Hello risponde toohello metodo con un risultato 200 byte.

dispositivo Hello utilizza 1 messaggio * 60 minuti * 24 ore = 1440 messaggi al giorno per la richiesta e risposta di messaggi da dispositivo a cloud hello e 2 * 6 volte all'ora * 24 ore = 288 messaggi per i metodi di hello, per un totale di messaggi 1728 al giorno.

## <a name="example-2"></a>Esempio n. 2

Un dispositivo invia un messaggio da dispositivo a cloud di 100 KB ogni ora. Aggiorna anche il relativo dispositivo gemello con payload di 1 KB ogni 4 ore. soluzione Hello nuovamente terminare letture hello 14 KB dispositivo doppi, una volta al giorno e viene aggiornato con le configurazioni toochange payload a 512 byte.

dispositivo Hello utilizza messaggi (100KB / 4KB) 25 * 24 ore per i messaggi da dispositivo a cloud, oltre a 1 messaggio * 6 volte al giorno per gli aggiornamenti, doppi per un totale di 156 messaggi al giorno.
Hello soluzione back-end Usa un doppio dispositivo di hello tooread 28 messaggi (KB 14/0,5 KB), più 1 messaggio tooupdate che, per un totale di messaggi di 29.

In totale, dispositivo hello e hello soluzione back-end utilizzare 185 messaggi al giorno.


[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-message-size]: iot-hub-devguide-messages-construct.md
