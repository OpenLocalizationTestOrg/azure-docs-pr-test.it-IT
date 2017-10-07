---
title: "ripristino di emergenza e disponibilità elevato IoT Hub aaaAzure | Documenti Microsoft"
description: "Vengono descritte le funzionalità Azure e l'IoT Hub hello che consentono di toobuild soluzioni a disponibilità elevata a Azure IoT con funzionalità di ripristino di emergenza."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: ae320e58-aa20-45b9-abdc-fa4faae8e6dd
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: elioda
ms.openlocfilehash: 74e1fa1682258819ffb3fd84eb79e42fc6e4120f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-high-availability-and-disaster-recovery"></a>Disponibilità elevata e ripristino di emergenza dell'hub IoT
Come un servizio di Azure IoT Hub fornisce disponibilità elevata (HA) utilizzando ridondanze a livello di area di Azure hello, senza operazioni aggiuntive richieste dalla soluzione hello. piattaforma Microsoft Azure Hello include anche funzionalità toohelp la compilazione delle soluzioni con funzionalità di ripristino di emergenza di emergenza o di disponibilità tra più aree. Se si desidera globale tooprovide, la disponibilità elevata per i dispositivi o utenti, tra più aree di progettazione e preparare le soluzioni tootake sfruttare queste funzionalità di ripristino di emergenza di Azure. articolo Hello [informazioni tecniche sulla continuità aziendale Azure](../resiliency/resiliency-technical-guidance.md) vengono descritte le funzionalità predefinite hello in Azure per la continuità aziendale e ripristino di emergenza. Hello [il ripristino di emergenza e disponibilità elevata per applicazioni Azure] [ Disaster recovery and high availability for Azure applications] documento fornisce indicazioni sull'architettura sulle strategie per applicazioni Azure tooachieve a disponibilità elevata e ripristino di emergenza.

## <a name="azure-iot-hub-dr"></a>Ripristino di emergenza dell'hub IoT di Azure
In aggiunta a disponibilità elevata toointra area, IoT Hub implementi meccanismi di failover per il ripristino di emergenza che non richiedono alcun intervento da parte dell'utente hello. Ripristino di emergenza Hub IoT automatico viene avviato e ha un obiettivo del tempo di ripristino (RTO) di 2-26 ore e hello seguenti obiettivi punto di ripristino (RPO).

| Funzionalità | RPO |
| --- | --- |
| Disponibilità del servizio per le operazioni del Registro di sistema e di comunicazione |Possibile perdita di CName |
| Dati sull'identità nel registro delle identità |Perdita di dati da 0 a 5 minuti |
| Messaggi da dispositivo a cloud |Tutti i messaggi non letti vengono persi |
| Messaggi di monitoraggio delle operazioni |Tutti i messaggi non letti vengono persi |
| Messaggi da cloud a dispositivo |Perdita di dati da 0 a 5 minuti |
| Coda di commenti da cloud a dispositivo |Tutti i messaggi non letti vengono persi |

## <a name="regional-failover-with-iot-hub"></a>Failover di area con l'hub IoT
Trattare di topologie di distribuzione nelle soluzioni IoT è di fuori ambito hello di questo articolo. Hello descritti hello *internazionali failover* modello di distribuzione allo scopo hello di elevata disponibilità e ripristino di emergenza.

In un modello di failover regionale, hello soluzione back-end esegue principalmente nel percorso di un Data Center e un hub IoT secondario e un back-end vengono distribuiti in un'altra posizione Data Center. Se l'hub IoT hello in Data Center principale hello subisce un'interruzione o viene interrotta la connettività di rete hello dal Data Center principale hello dispositivo toohello. I dispositivi usano un endpoint del servizio secondario quando non è raggiungibile gateway primario hello. Con una capacità di failover tra più aree, disponibilità di una soluzione hello possono essere migliorate oltre hello un'elevata disponibilità una singola area.

In generale, tooimplement un modello di failover di area con l'IoT Hub, sono necessari i seguenti elementi di hello:

* **Un hub IoT e un dispositivo logica di routing secondario**: nel caso di hello di un'interruzione del servizio nell'area primaria, i dispositivi è necessario avviare connessione area secondaria di tooyour. Natura hello in grado di riconoscere lo stato della maggior parte dei servizi interessati, è comune per processo di failover tra area hello tootrigger amministratori soluzione. Hello migliore modo toocommunicate hello nuovo endpoint toodevices, mantenendo il controllo del processo di hello è toohave li controllare regolarmente un *concierge* servizio endpoint attivo corrente hello. Hello concierge servizio può essere un'applicazione web che viene replicata e mantenuta raggiungibile utilizzando tecniche di reindirizzamento di DNS (ad esempio, usando [Azure Traffic Manager][Azure Traffic Manager]).
* **La replica del Registro di sistema di identità** -toobe utilizzabile, hub IoT secondario hello deve contenere tutte le identità del dispositivo che è possono connettere la soluzione toohello. soluzione Hello deve mantenere i backup di replica geografica delle identità del dispositivo e caricarli hub IoT secondario toohello prima di passare l'endpoint attivo di hello per i dispositivi hello. funzionalità di esportazione identità dispositivo Hello dell'IoT Hub è utile in questo contesto. Per altre informazioni, vedere la [Guida per gli sviluppatori dell'hub IoT: registro delle identità][IoT Hub developer guide - identity registry].
* **L'unione logica** : se area primaria hello diventa nuovamente disponibile, tutti hello stato e dati che sono stati creati nel sito secondario hello devono essere migrati toohello indietro di area primaria. Questo stato e i dati si riferisce principalmente toodevice identità e i metadati dell'applicazione, che devono essere unito con l'hub IoT hello primario e di altri archivi di specifiche dell'applicazione nell'area primaria hello. toosimplify questo passaggio, è consigliabile utilizzare operazioni idempotente. Operazioni idempotente di ridurre al minimo hello effetti collaterali da eventuale distribuzione uniforme di hello degli eventi e dai duplicati o in ordine recapito dei messaggi di eventi. Inoltre, la logica dell'applicazione hello deve essere progettato tootolerate potenziali incoerenze o "leggermente" lo stato di Data. Questa situazione può verificarsi a causa di toohello ulteriore tempo impiegato per il sistema hello troppo "correzione" in base agli obiettivi punto di ripristino (RPO).

## <a name="next-steps"></a>Passaggi successivi
Seguire questi toolearn collegamenti ulteriori informazioni sull'IoT Hub di Azure:

* [Introduzione agli hub IoT (esercitazione)][lnk-get-started]
* [Che cos'è l'hub IoT di Azure?][What is Azure IoT Hub?]

[Disaster recovery and high availability for Azure applications]: ../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md
[Azure Business Continuity Technical Guidance]: https://azure.microsoft.com/documentation/articles/resiliency-technical-guidance/
[Azure Traffic Manager]: https://azure.microsoft.com/documentation/services/traffic-manager/
[IoT Hub developer guide - identity registry]: iot-hub-devguide-identity-registry.md

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[What is Azure IoT Hub?]: iot-hub-what-is-iot-hub.md
