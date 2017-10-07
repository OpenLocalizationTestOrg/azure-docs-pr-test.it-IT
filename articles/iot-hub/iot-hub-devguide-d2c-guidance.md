---
title: Opzioni aaaAzure IoT Hub dispositivo a cloud | Documenti Microsoft
description: "Guida per sviluppatori - indicazioni su quando i messaggi da dispositivo a cloud toouse, proprietà segnalata o file di caricamento per le comunicazioni cloud a dispositivo."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 979136db-c92d-4288-870c-f305e8777bdd
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: 2caefc4f59e16ad28b0d8cf4b3bb627b4cba803b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-communications-guidance"></a>Indicazioni sulle comunicazioni da dispositivo a cloud
Quando si inviano informazioni da hello dispositivo app toohello soluzione back-end, l'IoT Hub espone tre opzioni:

* [Messaggi da dispositivo a cloud][lnk-d2c] per dati di telemetria e avvisi relativi alle serie temporali.
* [Proprietà segnalati] [ lnk-twins] per la segnalazione di informazioni sullo stato di dispositivi, ad esempio le funzionalità disponibili, le condizioni o hello stato dei flussi di lavoro a esecuzione prolungata. come aggiornamenti della configurazione e del software.
* [Caricamenti di file] [ lnk-fileupload] per il supporto batch di telemetria di grandi dimensioni e i file caricati dai dispositivi connessi in modo intermittente o compressi toosave della larghezza di banda.

Ecco un confronto dettagliato di hello varie opzioni di comunicazione da dispositivo a cloud.

|  | Messaggi da dispositivo a cloud | Proprietà segnalate | Caricamenti di file |
| ---- | ------- | ---------- | ---- |
| Scenario | Serie temporale di telemetria e avvisi. Ad esempio, batch di dati di sensori di 256 KB inviati ogni 5 minuti. | Funzionalità disponibili e condizioni. Ad esempio, hello dispositivo connettività modalità corrente, ad esempio cellulare o Wi-Fi. Sincronizzazione di flussi di lavoro a esecuzione prolungata, ad esempio aggiornamenti della configurazione e del software. | File multimediali. Batch di telemetria di grandi dimensioni, in genere compressi. |
| Archiviazione e recupero | Archiviati temporaneamente in IoT Hub, impostare i giorni too7. Solo lettura sequenziale. | Archiviati in un doppio dispositivo hello IoT Hub. Recuperabili tramite hello [il linguaggio di query di IoT Hub][lnk-query]. | Archiviati nell'account di Archiviazione di Azure specificato dall'utente. |
| Dimensione | I messaggi too256 KB. | Le dimensioni massime per le proprietà segnalate sono 8 KB. | Dimensioni di file massime supportate dall'Archiviazione BLOB di Azure. |
| Frequenza | Elevata. Per altre informazioni, vedere i [limiti dell'hub IoT][lnk-quotas]. | Media. Per altre informazioni, vedere i [limiti dell'hub IoT][lnk-quotas]. | Bassa. Per altre informazioni, vedere i [limiti dell'hub IoT][lnk-quotas]. |
| Protocol | Disponibile in tutti i protocolli. | Attualmente disponibile solo quando si usa MQTT. | Disponibile quando si utilizza qualsiasi protocollo, ma richiede HTTP sul dispositivo hello. |

È possibile che un'applicazione richiede informazioni di trasmissione tooboth come una serie di dati di telemetria ora o avviso e anche toomake disponibile in un doppio dispositivo hello. In questo scenario, è possibile scegliere di hello le opzioni seguenti:

* app del dispositivo Hello invia un messaggio da dispositivo a cloud e i report di modifica di una proprietà.
* back-end di Hello soluzione possibile archiviare informazioni hello nei tag del doppi hello dispositivo quando viene ricevuto un messaggio hello.

Poiché i messaggi da dispositivo a cloud abilita una velocità effettiva superiore rispetto agli aggiornamenti del dispositivo doppi, è talvolta utile tooavoid aggiornamento doppi hello dispositivo per tutti i messaggi da dispositivo a cloud.


[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-fileupload]: iot-hub-devguide-file-upload.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
