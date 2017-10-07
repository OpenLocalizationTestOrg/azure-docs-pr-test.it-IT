---
title: i filtri di connessione IP Hub IoT aaaAzure | Documenti Microsoft
description: "Come toouse filtro connessioni tooblock da IP specifici indirizzi per l'hub IoT Azure tooyour. È possibile bloccare le connessioni da singoli indirizzi IP o da intervalli di indirizzi IP."
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a>Usare i filtri IP

La sicurezza è un aspetto importante di qualsiasi soluzione IoT basata su un hub IoT di Azure. Talvolta è necessario tooexplicitly specificare gli indirizzi IP hello da cui i dispositivi possano connettersi come parte della configurazione di sicurezza. Hello _filtro IP_ funzionalità permette tooconfigure regole per il rifiuto o accettare il traffico da specifici indirizzi IPv4.

## <a name="when-toouse"></a>Quando toouse

Esistono due casi di utilizzo specifici, in questo caso gli endpoint Hub IoT di hello tooblock utili per determinati indirizzi IP:

- L'hub IoT deve ricevere il traffico solo da un intervallo di indirizzi IP specificato e rifiutare tutto il resto. Ad esempio, si utilizza l'hub IoT con [Express Route di Azure] toocreate connessioni private tra un hub IoT e l'infrastruttura locale.
- È necessario tooreject traffico da indirizzi IP che sono stati identificati come sospetto dall'amministratore di hub IoT hello.

## <a name="how-filter-rules-are-applied"></a>Come vengono applicate le regole di filtro

regole di filtro IP Hello vengono applicate a livello di servizio IoT Hub hello. Pertanto le regole di filtro IP hello applicano tooall connessioni dai dispositivi e applicazioni back-end utilizzando qualsiasi protocollo supportato.

Qualsiasi tentativo di connessione da un indirizzo IP corrispondente a una regola di rifiuto nell'hub IoT riceve un codice di stato 401 - Non autorizzato e la descrizione. messaggio di risposta Hello non è menzionato regola IP hello.

## <a name="default-setting"></a>Impostazione predefinita

Per impostazione predefinita, hello **filtro IP** griglia nel portale di hello per un hub IoT è vuota. Questa impostazione predefinita indica che l'hub accetta connessioni da qualsiasi indirizzo IP. Questa impostazione predefinita è regola tooa equivalente che accetta l'intervallo di indirizzi IP di hello 0.0.0.0/0.

![Impostazioni predefinite del filtro IP dell'hub IoT][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a>Aggiungere o modificare una regola del filtro IP

Quando si aggiunge una regola di filtro IP, viene chiesto di hello seguenti valori:

- Un **nome regola di filtro IP** che deve essere una stringa di alfanumerica univoca, distinzione dei caratteri too128. Solo caratteri alfanumerici di hello ASCII a 7 bit più `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` vengono accettate.
- Selezionare un **rifiutare** o **accettare** come hello **azione** per regola di filtro IP hello.
- Specificare un singolo indirizzo IPv4 o un blocco di indirizzi IP in notazione CIDR. Ad esempio, in CIDR notazione 192.168.100.0/22 rappresenta gli indirizzi IPv4 hello 1024 da 192.168.100.0 too192.168.103.255.

![Aggiungi un hub IoT tooan IP filtro regola][img-ip-filter-add-rule]

Dopo aver salvato la regola hello, è visualizzato un avviso che indica che gli aggiornamenti di hello in corso.

![Notifica sul salvataggio di una regola di filtro IP][img-ip-filter-save-new-rule]

Hello **Aggiungi** opzione è disabilitata quando si raggiunge il massimo di hello di 10 regole di filtro IP.

È possibile modificare una regola esistente facendo doppio clic sulla riga hello che contiene la regola di hello.

> [!NOTE]
> Rifiuto IP indirizzi possono impedire ad altri servizi di Azure (ad esempio Azure flusso Analitica, macchine virtuali di Azure o hello Esplora dispositivi nel portale di hello) l'interazione con l'hub IoT hello.

> [!WARNING]
> Se si utilizzano i messaggi tooread Analitica di flusso di Azure (ASA) da un hub IoT con abilitati i filtri IP, utilizzare hello Hub eventi compatibile con nome e l'endpoint dell'IoT Hub nella stringa di connessione ASA hello.

## <a name="delete-an-ip-filter-rule"></a>Eliminare una regola del filtro IP

toodelete una regola di filtro IP, selezionare una o più regole nella griglia di hello e fare clic su **eliminare**.

![Eliminare una regola del filtro IP dell'hub IoT][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a>Valutazione delle regole del filtro IP

Le regole di filtro IP vengono applicate nell'ordine e regola di hello prima che l'indirizzo IP di corrispondenze hello determina hello accettare o rifiutare l'azione.

Ad esempio, se si desidera che gli indirizzi tooaccept 192.168.100.0/22 intervallo hello e rifiutare tutti gli altri elementi, hello prima regola griglia hello deve accettare hello indirizzo intervallo 192.168.100.0/22. la regola successiva Hello dovrebbe rifiutare tutti gli indirizzi tramite 0.0.0.0/0 intervallo hello.

Puoi modificare l'ordine di hello le regole di filtro IP nella griglia hello facendo clic su tre punti verticali hello all'avvio di hello di una riga e mediante trascinamento e rilascio.

filtrare il nuovo indirizzo IP toosave ordine della regola, fare clic su **salvare**.

![Modificare l'ordine di hello le regole di filtro IP Hub IoT][img-ip-filter-rule-order]

## <a name="next-steps"></a>Passaggi successivi

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

- [Monitoraggio delle operazioni][lnk-monitor]
- [Metriche di Hub IoT][lnk-metrics]

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Express Route di Azure]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md