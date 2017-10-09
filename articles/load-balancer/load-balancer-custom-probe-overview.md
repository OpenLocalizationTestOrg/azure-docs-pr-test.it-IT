---
title: monitoraggio dello stato e probe personalizzati di bilanciamento del aaaLoad | Documenti Microsoft
description: Informazioni su come toouse personalizzata viene eseguita la ricerca per le istanze di bilanciamento del carico di Azure toomonitor bilanciamento del carico
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 46b152c5-6a27-4bfc-bea3-05de9ce06a57
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3dfcfcd2d5cffa58b160cb38d63acffbd997d452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-load-balancer-probes"></a>Informazioni sui probe di bilanciamento del carico

Bilanciamento del carico di Azure offre l'integrità di hello funzionalità toomonitor hello istanze del server tramite probe. Quando un probe ha esito negativo toorespond, bilanciamento del carico interrompe l'invio di nuova istanza di tipo non integro toohello connessioni. le connessioni esistenti Hello non sono interessate e le nuove connessioni vengono inviate toohealthy istanze.

I ruoli del servizio cloud, ovvero i ruoli di lavoro e i ruoli Web, usano un agente guest per il monitoraggio probe. I probe TCP o HTTP personalizzati devono essere configurati quando si usano macchine virtuali monitorate tramite il servizio di bilanciamento del carico.

## <a name="understand-probe-count-and-timeout"></a>Informazioni su conteggio e timeout dei probe

Il comportamento dei probe dipende dagli elementi seguenti:

* numero di Hello di probe ha esito positivo che consentono a un'istanza toobe etichettato come attività.
* numero di Hello di probe non riusciti che causano toobe un'istanza denominata come inattivi.

valore di timeout e la frequenza di Hello impostato in SuccessFailCount determinare se un'istanza è confermata toobe in esecuzione o non è in esecuzione. Nel portale di Azure hello, timeout di hello è impostato tootwo volte hello valore di frequenza hello.

configurazione di probe Hello di tutte le istanze con bilanciamento del carico per un endpoint (ovvero, un set con bilanciamento del carico) deve essere hello stesso. Questo significa che non è possibile avere una configurazione di probe diverso per ogni istanza del ruolo o una macchina virtuale in hello stesso ospitato il servizio per una combinazione di endpoint in questione. Ad esempio, ogni istanza deve avere porte locali e i timeout identici.

> [!IMPORTANT]
> Un probe di bilanciamento del carico Usa indirizzo IP hello 168.63.129.16. Questo indirizzo IP pubblico facilita le risorse di piattaforma toointernal di comunicazione per hello bring-your-proprietari-IP uno scenario di rete virtuale di Azure. Hello virtuale indirizzo IP pubblico 168.63.129.16 viene utilizzata in tutte le aree e non cambia. È consigliabile consentire questo indirizzo IP in tutti i criteri firewall locali. Non deve essere considerato un rischio per la sicurezza perché un messaggio da tale indirizzo di origine può solo hello interno piattaforma Azure. Se non si eseguire questa operazione, sarà presente un comportamento imprevisto in un'ampia gamma di scenari, ad esempio la configurazione di hello stesso intervallo di indirizzi IP di 168.63.129.16 e con gli indirizzi IP di duplicati.

## <a name="learn-about-hello-types-of-probes"></a>Informazioni sui tipi di hello di probe

### <a name="guest-agent-probe"></a>Probe dell'agente guest

Questo probe è disponibile solo per i servizi cloud di Azure. Bilanciamento del carico Usa l'agente guest hello hello macchina virtuale, quindi è in ascolto e risponde con una risposta HTTP 200 OK solo quando hello istanza è nello stato Ready hello (ovvero, non in un altro stato, ad esempio disponibilità, il riciclo o arresto).

Per ulteriori informazioni, vedere [configurazione hello file di definizione servizio (csdef) per le ricerche di integrità](https://msdn.microsoft.com/library/azure/ee758710.aspx) o [Introduzione alla creazione di un bilanciamento del carico con connessione Internet per i servizi cloud](load-balancer-get-started-internet-classic-cloud.md#check-load-balancer-health-status-for-cloud-services).

### <a name="what-makes-a-guest-agent-probe-mark-an-instance-as-unhealthy"></a>Perché un probe dell'agente guest contrassegna un'istanza come non integra

Se l'agente guest hello non riesce toorespond HTTP 200 OK, segni di bilanciamento carico di hello hello istanza e arresta l'istanza toothat il traffico di invio. servizio di bilanciamento del carico Hello continua istanza hello tooping. Se l'agente guest hello risponde con un HTTP 200, bilanciamento del carico hello invia nuovamente istanza toothat di traffico.

Quando si utilizza un ruolo web, in genere codice del sito Web hello viene eseguito in w3wp.exe, non è monitorato da hello infrastruttura di Azure né dall'agente guest. Ciò significa che gli errori in w3wp.exe (ad esempio, le risposte HTTP 500) non saranno segnalate toohello l'agente guest e bilanciamento del carico hello non avranno istanza dalla rotazione.

### <a name="http-custom-probe"></a>Probe HTTP personalizzato

probe di bilanciamento del carico HTTP personalizzato Hello sostituzioni hello guest agente probe predefinito, il che significa che è possibile creare la propria integrità hello toodetermine di logica personalizzata hello istanza del ruolo. servizio di bilanciamento del carico Hello le ricerche dell'endpoint ogni 15 secondi, per impostazione predefinita. istanza di Hello viene considerato toobe nella rotazione di bilanciamento del carico hello se il servizio risponde con un HTTP 200 entro il periodo di timeout hello (31 secondi per impostazione predefinita).

Questo può essere utile se si desidera tooimplement proprie istanze tooremove logica dalla rotazione del bilanciamento del carico. Ad esempio, è possibile decidere tooremove un'istanza se è superiore al 90% della CPU e restituisce uno stato non-200. Se si dispone di ruoli web che utilizzano w3wp.exe, ciò significa anche viene visualizzato automaticamente il monitoraggio del sito Web, poiché gli errori nel codice del sito Web verranno restituito un probe di bilanciamento del carico toohello stato non-200.

> [!NOTE]
> probe personalizzato di Hello HTTP supporta solo i protocolli HTTP e percorsi relativi. HTTPS non è supportato.

### <a name="what-makes-an-http-custom-probe-mark-an-instance-as-unhealthy"></a>Perché un probe HTTP personalizzato contrassegna un'istanza come non integra

* Hello applicazione HTTP restituisce un codice di risposta HTTP diversi da 200 (ad esempio, 403, 404 o 500). Si tratta di un riconoscimento positivo hello applicazione istanza deve essere messo fuori servizio sin da subito.
* server HTTP Hello non risponde affatto dopo il periodo di timeout di hello. A seconda di hello valore di timeout è impostato, ciò potrebbe indicare che più probe richiede go senza risposta prima di probe hello viene contrassegnato come non in esecuzione (vale a dire prima SuccessFailCount probe vengono inviati).
* server Hello chiude la connessione hello tramite una reimpostazione TCP.

### <a name="tcp-custom-probe"></a>Probe TCP personalizzato

Probe TCP avviano una connessione mediante l'esecuzione di un handshake a tre vie con porta hello definito.

### <a name="what-makes-a-tcp-custom-probe-mark-an-instance-as-unhealthy"></a>Perché un probe TCP personalizzato contrassegna un'istanza come non integra

* Hello TCP server non risponde affatto dopo il periodo di timeout di hello. Quando i probe hello viene contrassegnata come non in esecuzione dipende dal numero di hello del probe non richiede che sono stato configurato toogo senza risposta prima di contrassegnare probe hello come non in esecuzione.
* probe Hello riceve un TCP ripristinare le impostazioni nell'istanza del ruolo hello.

Per altre informazioni sulla configurazione di un probe di integrità HTTP o di un probe TCP, vedere [Introduzione alla creazione di un servizio di bilanciamento del carico per Internet in Gestione risorse con PowerShell](load-balancer-get-started-internet-arm-ps.md).

## <a name="add-healthy-instances-back-into-load-balancer-rotation"></a>Aggiungere di nuovo le istanze integre alla rotazione del servizio di bilanciamento del carico

Probe TCP e HTTP sono considerati integro e contrassegnare l'istanza del ruolo hello come integro quando:

* servizio di bilanciamento del carico Hello Ottiene un probe positivo hello prima ora hello che avvia macchina virtuale.
* numero di Hello SuccessFailCount (descritto in precedenza) definisce il valore di hello di probe ha esito positivo di istanza del ruolo obbligatorio toomark hello come integro. Se un'istanza del ruolo è stato rimosso, il numero di hello di esito positivo, successivi probe deve essere uguale o superare il valore di hello SuccessFailCount toomark hello istanza del ruolo in esecuzione.

> [!NOTE]
> Se sta fluttuando. potete integrità hello di un'istanza del ruolo, servizio di bilanciamento del carico hello attende più prima di inserire l'istanza del ruolo hello in stato integro hello. Questa operazione viene eseguita tramite criteri tooprotect hello infrastruttura di utenti e hello.

## <a name="use-log-analytics-for-load-balancer"></a>Usare Analisi dei log per il servizio di bilanciamento del carico

È possibile utilizzare [log analitica per il bilanciamento del carico](load-balancer-monitor-log.md) toocheck hello probe integrità dello stato e un probe numero. Consente la registrazione con Power BI o Azure Operational Insights statistiche tooprovide sullo stato di integrità di bilanciamento del carico.
