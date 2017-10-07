---
title: Guida di aaaDeveloper per l'IoT Hub di Azure | Documenti Microsoft
description: "Guida per sviluppatori Azure IoT Hub Hello include discussioni di endpoint, sicurezza, del Registro di sistema di hello identità, la gestione dei dispositivi, metodi diretti, gemelli di dispositivo, il caricamento di file, processi, hello linguaggio di query IoT Hub e messaggistica."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: d534ff9d-2de5-4995-bb2d-84a02693cb2e
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 2d3f18399e4cef6f9c4850a5caeb170a2d091a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-developer-guide"></a>Guida per gli sviluppatori dell'hub IoT di Azure

L'hub IoT di Azure è un servizio completamente gestito che consente di abilitare comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione.

L'hub IoT di Azure offre:

* Comunicazioni protette con credenziali di sicurezza per singoli dispositivi e controllo di accesso.
* Più opzioni di comunicazione da dispositivo a cloud e da cloud a dispositivo su vasta scala.
* Archivio disponibile per query con informazioni di stato e metadati per ogni dispositivo.
* Connettività semplice dispositivo con le librerie di dispositivo per i linguaggi più diffusi hello e piattaforme.

Questa Guida per sviluppatori di IoT Hub include hello seguenti articoli:

* [Device-to-cloud communications guidance][lnk-d2c-guidance] (Indicazioni sulla comunicazione da dispositivo a cloud), utile nella scelta tra messaggi da dispositivo a cloud, proprietà segnalate del dispositivo gemello e caricamento di file.
* [Cloud-to-device communication guidance][lnk-c2d-guidance] (Indicazioni sulla comunicazione da cloud a dispositivo), utile nella scelta tra metodi diretti, proprietà desiderate del dispositivo gemello e messaggi da cloud a dispositivo.
* [Dispositivo a cloud e messaggistica con l'IoT Hub cloud a dispositivo] [ devguide-messaging] descrive hello le funzionalità di messaggistica (per dispositivo a cloud e cloud a dispositivo) che espone l'IoT Hub.
  * [Inviare i messaggi da dispositivo a cloud tooIoT Hub][devguide-messages-d2c].
  * [Leggere messaggi da dispositivo a cloud da endpoint predefiniti hello][devguide-builtin].
  * [Usare endpoint personalizzati e regole di routing per i messaggi da dispositivo a cloud][devguide-custom].
  * [Inviare messaggi da cloud a dispositivo dall'hub IoT][devguide-messages-c2d].
  * [Creare e leggere messaggi dell'hub IoT][devguide-format].
* [Upload files from a device][devguide-upload] (Caricare file da un dispositivo), che descrive come caricare file da un dispositivo. articolo Hello include anche informazioni sugli argomenti, ad esempio hello può inviare il processo di caricamento hello notifiche.
* [Manage device identities in IoT Hub][devguide-identities] (Gestire le identità dei dispositivi nell'hub IoT), che descrive le informazioni archiviate nel registro delle identità di ogni hub IoT e spiega come accedere alle informazioni e modificarle.
* [Controllare l'accesso tooIoT Hub] [ devguide-security] illustra hello sicurezza modello usato toogrant tooIoT Hub funzionalità di accesso per i dispositivi e componenti di cloud. articolo Hello include informazioni sull'uso di token e i certificati x. 509 e i dettagli di è possibile concedere le autorizzazioni di hello.
* [Usare le configurazioni e lo stato del dispositivo gemelli toosynchronize] [ devguide-device-twins] descrive hello *doppi dispositivo* funzionalità concetto e hello espone ad esempio la sincronizzazione di un dispositivo con il relativo dispositivo doppi. articolo Hello include informazioni sui dati hello archiviati in una coppia di dispositivo.
* [Richiamare un metodo diretto su un dispositivo] [ devguide-directmethods] descrive hello del ciclo di vita di un metodo diretto, informazioni su come metodo tooinvoke metodi in un dispositivo da hello di app e gestire il back-end diretto nel dispositivo.
* [Pianificare processi in più dispositivi][devguide-jobs], che descrive come pianificare processi in più dispositivi. Hello articolo viene descritto come i processi che toosubmit eseguire attività come l'esecuzione di un metodo diretto, l'aggiornamento di un dispositivo utilizzando una coppia di dispositivo. Viene inoltre descritto come tooquery hello stato di un processo.
* [Fare riferimento - scegliere un protocollo di comunicazione] [ devguide-protocol] vengono descritti i protocolli di comunicazione hello che supporta IoT Hub per la comunicazione tra i dispositivi e gli elenchi di hello porte che devono essere aperte.
* [Riferimento - gli endpoint IoT Hub] [ devguide-endpoints] descrive hello vari endpoint che espone ogni hub IoT per operazioni di runtime e gestione. articolo Hello descrive inoltre come è possibile creare endpoint aggiuntivi nell'hub IoT e come un campo gateway tooenable dispositivi connettività tooyour IoT Hub toouse gli endpoint in scenari non standard.
* [Riferimento - linguaggio di query IoT Hub per gemelli di dispositivo, processi e il routing dei messaggi] [ devguide-query] descrive il linguaggio di query IoT Hub consente tooretrieve informazioni dell'hub sul gemelli di dispositivo e i processi.
* [Riferimento - quote e limitazioni] [ devguide-quotas] vengono riepilogate le quote di hello impostate nella hello servizio IoT Hub e hello comportamento è possibile prevedere toosee quando si supera una quota di limitazione.
* [Fare riferimento - prezzi] [ devguide-pricing] fornisce informazioni generali sulle diverse SKU e ai prezzi per l'IoT Hub e informazioni dettagliate su come hello varie funzionalità di IoT Hub sono misurate come messaggi dall'IoT Hub.
* [Riferimento - dispositivo e il servizio SDK] [ devguide-sdks] elenchi hello Azure IoT SDK, è possibile utilizzare toodevelop dispositivo sia il servizio App che interagiscono con l'hub IoT. articolo Hello comprende la documentazione di collegamenti tooonline API.
* [Riferimento - supporto di IoT Hub MQTT] [ devguide-mqtt] fornisce informazioni dettagliate sulle modalità di supporto del protocollo MQTT hello IoT Hub. articolo Hello viene descritto il supporto hello hello MQTT protocollo incorporato toohello IoT di Azure SDK e fornisce informazioni sull'utilizzo di protocollo MQTT hello direttamente.
* Il [glossario][devguide-glossary], che include un elenco dei termini più comuni correlati all'hub IoT.

[devguide-messaging]: iot-hub-devguide-messaging.md
[devguide-upload]: iot-hub-devguide-file-upload.md
[devguide-identities]: iot-hub-devguide-identity-registry.md
[devguide-security]: iot-hub-devguide-security.md
[devguide-device-twins]: iot-hub-devguide-device-twins.md
[devguide-directmethods]: iot-hub-devguide-direct-methods.md
[devguide-jobs]: iot-hub-devguide-jobs.md
[devguide-endpoints]: iot-hub-devguide-endpoints.md
[devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[devguide-query]: iot-hub-devguide-query-language.md
[devguide-sdks]: iot-hub-devguide-sdks.md
[devguide-mqtt]: iot-hub-mqtt-support.md
[devguide-glossary]: iot-hub-devguide-glossary.md
[devguide-pricing]: iot-hub-devguide-pricing.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[devguide-messages-d2c]: iot-hub-devguide-messages-d2c.md
[devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[devguide-custom]: iot-hub-devguide-messages-read-custom.md
[devguide-messages-c2d]: iot-hub-devguide-messages-c2d.md
[devguide-format]: iot-hub-devguide-messages-construct.md
[devguide-protocol]: iot-hub-devguide-protocols.md
