---
title: le connessioni in uscita aaaUnderstanding in Azure | Documenti Microsoft
description: Questo articolo spiega come Azure consente toocommunicate di macchine virtuali con i servizi Internet pubblica.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 5f666f2a-3a63-405a-abcd-b2e34d40e001
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 5/31/2017
ms.author: kumud
ms.openlocfilehash: ffe59971b934a16c9f6f78e3b15869a0072320d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-outbound-connections-in-azure"></a>Informazioni sulle connessioni in uscita in Azure

Una macchina virtuale (VM) in Azure può comunicare con endpoint all'esterno di Azure nello spazio di indirizzi IP pubblici. Quando una macchina virtuale viene avviata una destinazione del flusso in uscita di tooa nello spazio di indirizzi IP pubblico, Azure esegue il mapping privata tooa pubblica indirizzo IP della macchina virtuale di hello e consente di hello tooreach il traffico di ritorno macchina virtuale.

Azure offre tre modi diversi di connettività in uscita tooachieve. Ogni metodo ha funzionalità e vincoli specifici. Leggere attentamente ogni metodo toochoose quello che soddisfa le proprie esigenze.

| Scenario | Metodo | Nota |
| --- | --- | --- |
| Macchina virtuale autonoma (nessun bilanciamento del carico, nessun indirizzo IP pubblico a livello di istanza) |SNAT predefinito |Azure associa un indirizzo IP pubblico per SNAT |
| Macchina virtuale con carico bilanciato (nessun indirizzo IP pubblico a livello di istanza nella VM) |Utilizzo di bilanciamento del carico hello SNAT |Azure Usa un indirizzo IP pubblico del servizio di bilanciamento del carico hello per SNAT |
| Macchina virtuale con indirizzo IP pubblico a livello di istanza (con o senza bilanciamento del carico) |SNAT non usato |Azure Usa hello IP pubblico assegnato toohello VM |

Se non si desidera toocommunicate una macchina virtuale con gli endpoint all'esterno di Azure nello spazio di indirizzi IP pubblico, è possibile utilizzare accesso tooblock di sicurezza gruppi (rete). Per informazioni più dettagliate sull'uso dei gruppi di sicurezza di rete, vedere [Prevenzione della connettività pubblica](#preventing-public-connectivity).

## <a name="standalone-vm-with-no-instance-level-public-ip-address"></a>Macchina virtuale autonoma senza indirizzo IP pubblico a livello di istanza

In questo scenario, hello VM non fa parte di un pool di bilanciamento del carico di Azure e non dispone di un indirizzo di istanza livello pubblica IP (ILPIP) assegnato tooit. Quando hello macchina virtuale viene creato un flusso in uscita, Azure traduce l'indirizzo IP di origine privata hello dell'indirizzo IP di hello flusso in uscita tooa origine pubblico. indirizzo IP pubblico Hello utilizzato per il flusso in uscita non è configurabile e non si tiene conto per limite di risorse IP pubbliche della sottoscrizione hello. Azure Usa tooperform origine rete indirizzo traduzione (SNAT) questa funzione. Porte effimere dell'indirizzo IP pubblico hello sono flussi di singoli toodistinguish utilizzati originati dal hello macchina virtuale. SNAT assegna dinamicamente le porte temporanee dopo che sono stati creati i flussi. In questo contesto, porte effimere di hello utilizzate per SNAT sono le porte SNAT tooas cui viene fatto riferimento.

Le porte SNAT sono una risorsa limitata che può esaurirsi. È importante toounderstand la modalità di utilizzo. Una porta SNAT viene consumata da ciascun flusso tooa singolo indirizzo IP. Per più flussi toohello stesso indirizzo IP, ogni flusso utilizza una singola porta SNAT. Ciò garantisce che i flussi di hello siano univoco quando ha avuto origine hello stesso toohello di indirizzo IP pubblico stesso indirizzo IP di destinazione. Più flussi, ogni indirizzo IP di destinazione diverse tooa utilizzano una singola porta SNAT per ogni destinazione. indirizzo IP di destinazione Hello rende hello flussi univoco.

È possibile utilizzare [Log Analitica di bilanciamento del carico](load-balancer-monitor-log.md) e [toomonitor i registri eventi di avviso per i messaggi di esaurimento delle porte SNAT](load-balancer-monitor-log.md#alert-event-log). Quando si esauriscono le risorse di porte SNAT, i flussi in uscita vengono completati dopo che le porte SNAT sono state rilasciate da flussi esistenti. Il timeout di inattività di Load Balancer è di 4 minuti per il recupero di porte SNAT.

## <a name="load-balanced-vm-with-no-instance-level-public-ip-address"></a>Macchina virtuale con carico bilanciato senza indirizzo IP pubblico a livello di istanza

In questo scenario, hello macchina virtuale fa parte di un pool di bilanciamento del carico di Azure.  Hello macchina virtuale non dispone di un indirizzo IP pubblico assegnato tooit. Hello risorsa di bilanciamento del carico deve essere configurato con un regola toolink hello pubblico IP front-end con pool back-end hello.  Se non si completa questa configurazione, il comportamento di hello è come descritto nella sezione hello sopra per [Standalone VM con nessun IP pubblico a livello di istanza](load-balancer-outbound-connections.md#standalone-vm-with-no-instance-level-public-ip-address).

Quando hello macchina virtuale con bilanciamento del carico viene creato un flusso in uscita, Azure traduce l'indirizzo IP di origine privata hello di hello flusso in uscita toohello indirizzo IP pubblico del hello pubblico front-end bilanciamento del carico. Azure Usa tooperform origine rete indirizzo traduzione (SNAT) questa funzione. Porte effimere dell'indirizzo IP pubblico del bilanciamento carico di hello sono flussi di singoli toodistinguish utilizzati originati dal hello macchina virtuale. SNAT assegna dinamicamente le porte temporanee dopo che sono stati creati i flussi in uscita. In questo contesto, porte effimere di hello utilizzate per SNAT sono le porte SNAT tooas cui viene fatto riferimento.

Le porte SNAT sono una risorsa limitata che può esaurirsi. È importante toounderstand la modalità di utilizzo. Una porta SNAT viene consumata da ciascun flusso tooa singolo indirizzo IP. Per più flussi toohello stesso indirizzo IP, ogni flusso utilizza una singola porta SNAT. Ciò garantisce che i flussi di hello siano univoco quando ha avuto origine hello stesso toohello di indirizzo IP pubblico stesso indirizzo IP di destinazione. Più flussi, ogni indirizzo IP di destinazione diverse tooa utilizzano una singola porta SNAT per ogni destinazione. indirizzo IP di destinazione Hello rende hello flussi univoco.

È possibile utilizzare [Log Analitica di bilanciamento del carico](load-balancer-monitor-log.md) e [toomonitor i registri eventi di avviso per i messaggi di esaurimento delle porte SNAT](load-balancer-monitor-log.md#alert-event-log). Quando si esauriscono le risorse di porte SNAT, i flussi in uscita vengono completati dopo che le porte SNAT sono state rilasciate da flussi esistenti. Il timeout di inattività di Load Balancer è di 4 minuti per il recupero di porte SNAT.

## <a name="vm-with-an-instance-level-public-ip-address-with-or-without-load-balancer"></a>Macchina virtuale con indirizzo IP pubblico a livello di istanza (con o senza bilanciamento del carico)

In questo scenario, hello VM dispone di un'istanza livello pubblica IP (ILPIP) assegnato tooit. Non è importante se hello macchina virtuale con carico bilanciato o non. Quando si usa un IP pubblico a livello di istanza, non si applica SNAT. Hello VM utilizza hello ILPIP per tutti i flussi in uscita. Se l'applicazione avvia numerosi flussi in uscita e si verifica un esaurimento SNAT, è consigliabile assegnare un tooavoid ILPIP vincoli SNAT.

## <a name="discovering-hello-public-ip-used-by-a-given-vm"></a>Individuazione hello utilizzato da una macchina virtuale specificata indirizzo IP pubblico

Esistono diversi modi toodetermine hello pubblica indirizzo IP di origine di una connessione in uscita. OpenDNS fornisce un servizio che consente di visualizzare hello indirizzo IP pubblico della macchina virtuale. Uso del comando nslookup hello, è possibile inviare una query DNS per il resolver OpenDNS toohello di hello nomi myip.opendns.com. servizio Hello restituisce hello origine IP che è stata query hello toosend utilizzato. Quando si esegue hello seguendo query dalla macchina virtuale, la risposta hello è hello che IP pubblico utilizzato per la macchina virtuale.

    nslookup myip.opendns.com resolver1.opendns.com

## <a name="preventing-public-connectivity"></a>Prevenzione della connettività pubblica

In alcuni casi non è auspicabile per una macchina virtuale toobe consentito toocreate un flusso in uscita oppure potrebbero esserci toomanage un requisito che le destinazioni raggiungibili con flussi in uscita. In questo caso, utilizzare [gruppi di sicurezza (rete)](../virtual-network/virtual-networks-nsg.md) toomanage hello destinazioni che hello VM può raggiungere. Quando si applica un gruppo tooa con bilanciamento del carico macchina virtuale, è necessario toopay attenzione toohello [predefinito tag](../virtual-network/virtual-networks-nsg.md#default-tags) e [regole predefinite](../virtual-network/virtual-networks-nsg.md#default-rules).

È necessario assicurarsi che hello VM può ricevere le richieste di probe di integrità dal bilanciamento del carico di Azure. Se un gruppo blocchi probe le richieste di integrità da hello tag predefinito AZURE_LOADBALANCER, i probe di integrità macchina virtuale non riesce e hello macchina virtuale è contrassegnato come inattivo. Servizio di bilanciamento del carico interrompe l'invio di nuovi flussi toothat macchina virtuale.

## <a name="limitations"></a>Limitazioni

Se [a un servizio di bilanciamento del carico sono associati più indirizzi IP (pubblici)](load-balancer-multivip-overview.md), uno qualsiasi di questi IP indirizzi pubblici è idoneo per i flussi in uscita.

Azure Usa un numero di hello toodetermine algoritmo di SNAT porte disponibili in base alle dimensioni di hello del pool di hello.  Al momento questo parametro non è configurabile.

È importante toorememember che hello numero di porte SNAT disponibili non convertiti direttamente toonumber di connessioni. Vedi sopra per informazioni dettagliate su quando e come vengono allocate porte SNAT e come toomanage esauribile risorsa.
