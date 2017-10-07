---
title: Opzioni aaaAzure IoT Hub cloud a dispositivo | Documenti Microsoft
description: "Guida per sviluppatori - indicazioni su quando toouse diretta di metodi, di un doppio dispositivo proprietà desiderate o cloud a dispositivo messaggi per le comunicazioni cloud a dispositivo."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: bb95445054fa2711e34fc1d928c3665e0246c81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-to-device-communications-guidance"></a>Indicazioni sulle comunicazioni da cloud a dispositivo
IoT Hub fornisce tre opzioni per app di back-end tooa dispositivo App tooexpose funzionalità:

* [Metodi di indirizzare] [ lnk-methods] per le comunicazioni che richiedono la conferma immediata dei risultati di hello. I metodi diretti vengono spesso usati per il controllo interattivo dei dispositivi, ad esempio l'accensione di una ventola.
* [Le proprietà del desiderate doppi] [ lnk-twins] per i comandi con esecuzione prolungata destinati desiderato di dispositivo hello tooput in un determinato stato. Ad esempio set hello telemetria inviare interval too30 minuti.
* [I messaggi da cloud a dispositivo] [ lnk-c2d] per app per dispositivi toohello notifiche unidirezionale.

Ecco un confronto dettagliato di hello varie opzioni di comunicazione cloud a dispositivo.

|  | Metodi diretti | Proprietà desiderate del dispositivo gemello | Messaggi da cloud a dispositivo |
| ---- | ------- | ---------- | ---- |
| Scenario | Comandi che richiedono una conferma immediata, ad esempio l'accensione di una ventola. | I comandi con esecuzione prolungata deve dispositivo hello tooput in un determinato stato desiderato. Ad esempio set hello telemetria inviare interval too30 minuti. | App per dispositivi toohello notifiche unidirezionale. |
| Flusso di dati | Bidirezionale. app per dispositivi Hello può rispondere toohello metodo sin da subito. back-end di Hello soluzione riceve il risultato di hello contestualmente toohello richiesta. | Unidirezionale. app per dispositivi Hello riceve una notifica con la modifica di proprietà hello. | Unidirezionale. app per dispositivi Hello riceve il messaggio hello
| Durabilità | I dispositivi disconnessi non vengono contattati. back-end di Hello soluzione viene notificato che il dispositivo hello non è connesso. | In un doppio dispositivo hello vengono mantenuti i valori di proprietà. Il dispositivo li leggerà alla riconnessione successiva. I valori delle proprietà vengono recuperati con hello [il linguaggio di query di IoT Hub][lnk-query]. | I messaggi possono essere mantenuti dall'IoT Hub per le ore too48. |
| Destinazioni | Singolo dispositivo che usa **deviceId** o più dispositivi che usano [processi][lnk-jobs]. | Singolo dispositivo che usa **deviceId** o più dispositivi che usano [processi][lnk-jobs]. | Singolo dispositivo in base a **deviceId**. |
| Dimensione | Backup too8KB richieste e risposte di 8KB. | Le dimensioni massime per le proprietà desiderate sono 8 KB. | I messaggi too64KB. |
| Frequenza | Elevata. Per altre informazioni, vedere i [limiti dell'hub IoT][lnk-quotas]. | Media. Per altre informazioni, vedere i [limiti dell'hub IoT][lnk-quotas]. | Bassa. Per altre informazioni, vedere i [limiti dell'hub IoT][lnk-quotas]. |
| Protocol | Attualmente disponibile solo quando si usa MQTT. | Attualmente disponibile solo quando si usa MQTT. | Disponibile in tutti i protocolli. Il dispositivo deve eseguire il polling quando usa HTTP. |

Informazioni su come toouse diretto i metodi, proprietà desiderate e i messaggi da cloud a dispositivo nelle seguenti esercitazioni hello:

* [Usare i metodi diretti ][lnk-methods-tutorial], per i metodi diretti.
* [Utilizzare i dispositivi di proprietà desiderato tooconfigure][lnk-twin-properties], per le proprietà; del desiderate da un doppio dispositivo 
* [Inviare messaggi da cloud a dispositivo][lnk-c2d-tutorial], per messaggi da cloud a dispositivo.

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-tutorial]: iot-hub-node-node-c2d.md
